# Como construímos

A história do projeto, do zero até a v2. Foi feito por Adriano em parceria com o Claude
(assistente de IA da Anthropic), em poucos dias, com dados públicos e ferramentas gratuitas.

## Linha do tempo

| Quando | O que aconteceu |
|---|---|
| Madrugada de 25/10/2026 | A ideia: dá para mostrar, na noite do 2º turno, não só a contagem, mas para onde ela vai? |
| 01h–03h | Exploração dos arquivos públicos do TSE a partir do GitHub (o site do TSE só aceita acesso de algumas redes; os servidores do GitHub conseguem). Descoberta da estrutura: andamento por UF, resultado por município, configuração de seções. |
| 01h | Decisão-chave: usar o **1º turno da mesma seção** como base, em vez de uma eleição antiga. Mesmos candidatos, mesmo eleitorado, encaixe de 100% das urnas. |
| 02h–05h | Base por seção (517 mil urnas), modelo v1, reprise do 2º turno de 2022 e página. |
| 05h | Descoberta importante no teste: os horários de chegada que estávamos usando eram de reprocessamento, não de chegada real. Coletamos uma amostra de 55 mil horários reais nos arquivos de cada urna e refizemos o teste. |
| 25/10, 16h–17h | O robô deveria ligar sozinho às 16h47; o agendamento do GitHub atrasou e ele foi ligado manualmente. |
| 17h | O STF prorrogou a votação até as 19h e o TSE pausou a divulgação. |
| 17h30 | Correção ao vivo: os arquivos por município do TSE estavam atrasados em relação ao total de cada estado. O robô passou a conferir o total de cada estado e buscar os municípios que faltavam. |
| 17h40 | Robô passou a se renovar sozinho antes do limite de 6 horas do GitHub. |
| 19h07 | Primeira projeção, com 1% apurado: 52,4%. |
| 20h12 | Com ~30% apurado, a projeção (51,6%) estava estável havia 15 minutos. Decisão de "cravar". A contagem bruta ainda mostrava o outro candidato à frente minutos antes. |
| 21h12 | Resultado com 99,74% apurado: 51,75%. A projeção errou por 0,1 ponto ou menos desde os 20% apurados, e o resultado ficou dentro da faixa de 90% em todos os momentos. |
| 27/10 | v2: aprendizado com 2º turnos de presidente e governador de 2010 a 2026, novo termo para os votos "novos", camadas para governador, incerteza calibrada, robô genérico e desligado até ser chamado. |

## Decisões que fizeram diferença

1. **Base no 1º turno da mesma urna.** É o melhor "antes" possível: três semanas de distância,
   os mesmos dois finalistas e a mesma seção. Nada precisa ser estimado por endereço.
2. **Teste com a ordem real de chegada.** Um teste com urnas em ordem aleatória fica bonito,
   mas mente: na vida real, regiões inteiras chegam juntas. Só com horários reais o teste
   mostra os erros que acontecem de verdade.
3. **Tudo no GitHub.** O robô roda no GitHub Actions, os dados ficam num ramo do próprio
   repositório e a página no GitHub Pages. Custo zero, sem servidor.
4. **Honestidade na incerteza.** Na noite da eleição, a chance de vitória chegou a 100% com 2%
   apurado, cedo demais. A v2 corrige isso com um termo que depende de quais lugares já
   entraram, calibrado em eleições passadas.

## Ferramentas

- Python (numpy, scipy, pandas) para o modelo e o processamento;
- GitHub Actions para o robô e para o processamento pesado dos dados do TSE;
- GitHub Pages para a página, um único arquivo HTML;
- dados públicos do TSE: resultados da divulgação e dados abertos por seção.
