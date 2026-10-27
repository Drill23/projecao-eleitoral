# Como o modelo funciona

Este documento explica o modelo de projeção passo a passo, do dado bruto do TSE até o número
que aparece na tela. A versão em produção é a **v2**. A v1 é a que rodou ao vivo na noite de
25/10/2026; as diferenças estão no fim.

![Fluxo](../img/fluxo.svg)

## 1. O problema: a contagem engana no começo

As urnas não chegam ao TSE em ordem aleatória. Fuso horário, tamanho da cidade e a logística
de cada estado decidem quem chega primeiro. Se os primeiros lugares a chegar votam mais em
um candidato, ele aparece na frente mesmo que vá perder.

Na noite de 25/10/2026 isso aconteceu de verdade: com 20% das urnas apuradas, a contagem do
TSE mostrava o candidato que perderia a eleição na frente. A projeção nunca mostrou isso.

## 2. A ideia central: cada urna já votou uma vez

![Método](../img/metodo.svg)

O 2º turno usa **as mesmas seções eleitorais** do 1º turno, três semanas antes. Para cada uma
das ~517 mil seções sabemos o voto do 1º turno: quanto teve cada finalista (A e B), cada
candidato eliminado e quantas pessoas não escolheram ninguém (abstenção, branco ou nulo).

Quando uma urna é apurada no 2º turno, comparamos com o 1º turno **da mesma urna**. Essa
comparação, repetida em milhares de urnas, mostra:

- para onde foram os eleitores dos candidatos eliminados;
- como votaram os "novos": quem não tinha escolhido ninguém no 1º turno e agora votou;
- quanto cada região, estado e município se moveu além disso;
- como mudou o comparecimento.

Para cada urna que ainda falta, aplicamos o que foi aprendido ao 1º turno dela. A projeção
final é a soma dos votos já apurados com a previsão de cada urna pendente.

## 3. A conta, em detalhe

Para a parte já apurada de cada município *m* (as mesmas seções nos dois turnos):

```
base_m = log( (A1 + Σk qk·Ok + qN·N) / (B1 + Σk (1−qk)·Ok + (1−qN)·N) )
y_m    = log( A2 / B2 )
y_m    = base_m + efeito do país + desvio da região + β·porte + desvio do estado + desvio do município + ruído
```

| Símbolo | O que é |
|---|---|
| A1, B1 | votos dos dois finalistas no 1º turno, nas seções já apuradas |
| Ok | votos de cada candidato eliminado (os 3 maiores separados, o resto junto) |
| qk | fração dos eleitores de Ok que foi para A (estimada) |
| N | votos válidos "novos": quanto o total de válidos cresceu em relação ao 1º turno |
| qN | fração dos novos que foi para A (estimada). Usado só para governador: para presidente o teste mostrou que piorava a projeção |
| A2, B2 | votos de A e B no 2º turno, já apurados |

Os parâmetros são estimados por mínimos quadrados ponderados (municípios com mais votos
pesam mais), com **priores**: palpites iniciais frouxos que os dados corrigem. Se houver
apoio declarado de um eliminado, ele pode entrar como prior na configuração.

Os desvios de estado e de município são **encolhidos** (estimativa empírico-bayesiana): onde
há poucos votos apurados, o modelo confia pouco no que viu e puxa o desvio para perto da
média. Isso evita que poucas urnas façam a projeção pular.

![Camadas](../img/hierarquia.svg)

## 4. Urnas que faltam

Para cada seção pendente:

- **quantos votos válidos vai ter** = comparecimento dela no 1º turno × variação de
  comparecimento já vista na sua região × proporção de votos válidos da região;
- **como eles se dividem** = o 1º turno dela, com as transferências, os novos e os desvios
  estimados para o lugar dela.

Uma etapa de conciliação cuida dos momentos em que os arquivos do TSE andam em ritmos
diferentes (por exemplo, uma urna marcada como apurada antes de o resultado do município
incluí-la).

## 5. A incerteza: faixa de 90% e chance de vitória

O modelo repete a conta 60 a 150 vezes por ciclo, sorteando a cada vez:

1. valores plausíveis para os parâmetros (pela curvatura do ajuste, a aproximação de Laplace);
2. desvios para estados/regiões e municípios que ainda não apareceram;
3. variações de comparecimento nos lugares pouco apurados.

A dispersão desses sorteios (sd) é então ajustada por uma fórmula **aprendida em 2º turnos
passados** (2010 a 2022):

```
sd_final = sqrt( (m·sd)² + (b·pendente)² + d² )
m        = exp( α + β·log10(% apurado) + γ·[é presidente] )
```

Em palavras: no começo da apuração a faixa é alargada (os sorteios sozinhos subestimam o
quanto o quadro ainda pode mudar); depois de uns 10% apurado ela é estreitada (os sorteios
sozinhos ficam cautelosos demais); para presidente há uma folga extra. Os valores estão em
[resultados.md](resultados.md#calibração-final-da-incerteza).

A faixa de 90% é projeção ± 1,645·sd_final e a chance de vitória é a probabilidade, numa
normal, de o resultado passar de 50%. No teste, a faixa da v2 contém o resultado final em
**90% dos momentos** — exatamente o que ela promete. A da v1 continha em 97%, ou seja, era larga
demais.

## 6. Governador

O mesmo modelo serve para governador. A diferença está nas camadas: em vez de região e UF,
os municípios do estado são agrupados pela posição geográfica dos locais de votação em
4 grupos de vizinhos e 12 subgrupos. Cada grupo recebe o nome do seu maior município.

## 7. O que mudou da v1 para a v2

| | v1 (noite de 25/10/2026) | v2 |
|---|---|---|
| Incerteza | sorteios × 1,5 fixo | sorteios ajustados por estágio da apuração, cargo e quanto falta, calibrados em 49 eleições |
| Camadas para governador | só o estado | 4 grupos + 12 subgrupos de municípios vizinhos |
| Votos "novos" (abstenção/branco/nulo que viram voto) | — | termo próprio para governador |
| Eleições | só presidente 2026 | qualquer 2º turno de presidente ou governador, por configuração |
| Prior de pesquisa | — | opcional, por configuração |
| Robô | horários fixos, reiniciado por agendamentos atrasados | só manual, renovação automática, foto de cada ciclo para análise |

Testamos também, e deixamos de fora por não melhorar: o termo de votos novos para presidente,
um prior para a variação entre estados, um índice de cobertura na incerteza e pistas tiradas da
eleição anterior. Detalhes em [resultados.md](resultados.md#o-que-testamos-e-não-entrou).
