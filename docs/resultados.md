# Resultados da avaliação

Reprise de **55 segundos turnos** (5 de presidente e 50 de governador, de 2010 a 2026), cada um com **3 ordens de chegada** das urnas, liberando as seções em fatias de 0,5% a 90% do eleitorado. São 1675 momentos avaliados.

## Como o teste foi feito

- **Base**: para cada eleição, o 1º turno de cada seção e o resultado final do 2º turno na mesma seção (dados abertos do TSE).
- **Ordem de chegada**: horários reais de chegada das urnas medidos nos arquivos de cada urna do TSE em 2026 (cerca de 55 mil urnas do 1º turno e 47 mil do 2º). Para eleições antigas, cada seção recebe o horário de uma urna do mesmo município (ou do mesmo estado e porte de cidade). As 3 ordens diferem por sorteio.
- **Sem colar na prova**: a escolha das variantes e a calibração da incerteza usam só 2010–2022; cada eleição desse período é avaliada com coeficientes ajustados **sem ela**. As 6 eleições de 2026 (presidente e 5 governadores) são **teste fora da amostra**.
- **DF fica de fora**: o Distrito Federal tem um único município, e o TSE divulga um único resultado para ele durante a apuração; não há como projetar por município.
- **v1** é o modelo exatamente como rodou na noite de 25/10/2026 (mesma faixa ×1,5). **v2** é a versão nova.

## Glossário das métricas

- **Erro médio**: diferença média, em pontos percentuais, entre a projeção e o resultado final do vencedor.
- **Cobertura**: em quantos momentos o resultado final caiu dentro da faixa de 90%. O ideal é **90%**: mais que isso é faixa larga demais (cautela sem necessidade), menos é faixa estreita demais (confiança demais).
- **Largura**: tamanho médio da faixa de 90%.
- **Brier**: erro da chance de vitória (0 = perfeito). Mede ao mesmo tempo se a chance está certa e se ela é decidida. Menor é melhor.
- **Chamada errada**: chance acima de 95% para quem perdeu.

## Todas as eleições (55 eleições)

Resumo de todos os momentos: erro médio **0,57 (v1) → 0,54 (v2)** pontos; cobertura da faixa 97% → **90%**; Brier 0,0117 → **0,0064**; acerto do vencedor 99,0% → 99,2% (contagem do TSE: 89,1%); chamadas erradas: 0 → 0.

Momento de cravar (chance ≥ 95% e não cai mais), mediana: v1 1% apurado, v2 1%; cravadas erradas: 0 e 0.

**Erro médio da projeção (pontos percentuais)**

| Apurado | Contagem do TSE | v1 | v2 | v2 vs v1 |
|---|---|---|---|---|
| 0,5% | 4,37 | 1,59 | 1,52 | −4% |
| 1% | 4,21 | 1,52 | 1,51 | −1% |
| 2% | 3,94 | 1,09 | 1,01 | −7% |
| 3% | 3,69 | 0,91 | 0,84 | −7% |
| 5% | 3,19 | 0,69 | 0,74 | +7% |
| 10% | 2,62 | 0,33 | 0,30 | −7% |
| 20% | 2,13 | 0,27 | 0,25 | −6% |
| 30% | 1,81 | 0,20 | 0,17 | −13% |
| 50% | 1,27 | 0,13 | 0,12 | −13% |
| 70% | 0,79 | 0,08 | 0,07 | −13% |
| 90% | 0,30 | 0,03 | 0,03 | −5% |

**Incerteza**

| Apurado | Cobertura v1 | Cobertura v2 | Largura v1 | Largura v2 | Brier v1 | Brier v2 |
|---|---|---|---|---|---|---|
| 0,5% | 93% | 92% | 8,2 pt | 8,4 pt | 0,0288 | 0,0251 |
| 1% | 92% | 87% | 8,1 pt | 6,5 pt | 0,0231 | 0,0144 |
| 2% | 92% | 92% | 7,4 pt | 4,8 pt | 0,0256 | 0,0182 |
| 3% | 96% | 90% | 6,6 pt | 3,7 pt | 0,0186 | 0,0101 |
| 5% | 99% | 92% | 5,8 pt | 2,7 pt | 0,0150 | 0,0062 |
| 10% | 100% | 90% | 4,0 pt | 1,6 pt | 0,0106 | 0,0028 |
| 20% | 99% | 90% | 3,4 pt | 1,1 pt | 0,0085 | 0,0018 |
| 30% | 99% | 91% | 2,9 pt | 0,9 pt | 0,0061 | 0,0005 |
| 50% | 99% | 90% | 1,9 pt | 0,5 pt | 0,0023 | 0,0000 |
| 70% | 98% | 92% | 1,1 pt | 0,3 pt | 0,0007 | 0,0000 |
| 90% | 98% | 85% | 0,4 pt | 0,1 pt | 0,0000 | 0,0000 |

## Presidente (5 eleições)

Resumo de todos os momentos: erro médio **0,16 (v1) → 0,16 (v2)** pontos; cobertura da faixa 92% → **94%**; Brier 0,0000 → **0,0000**; acerto do vencedor 100,0% → 100,0% (contagem do TSE: 50,9%); chamadas erradas: 0 → 0.

Momento de cravar (chance ≥ 95% e não cai mais), mediana: v1 0,5% apurado, v2 0,5%; cravadas erradas: 0 e 0.

**Erro médio da projeção (pontos percentuais)**

| Apurado | Contagem do TSE | v1 | v2 | v2 vs v1 |
|---|---|---|---|---|
| 0,5% | 4,55 | 0,45 | 0,45 | −0% |
| 1% | 4,17 | 0,52 | 0,52 | +0% |
| 2% | 4,45 | 0,29 | 0,29 | +0% |
| 3% | 4,47 | 0,18 | 0,18 | +0% |
| 5% | 4,34 | 0,10 | 0,10 | +0% |
| 10% | 3,88 | 0,07 | 0,07 | +0% |
| 20% | 3,43 | 0,07 | 0,07 | +0% |
| 30% | 3,20 | 0,04 | 0,04 | −0% |
| 50% | 2,69 | 0,02 | 0,02 | −0% |
| 70% | 2,01 | 0,01 | 0,01 | +0% |
| 90% | 0,85 | 0,00 | 0,00 | −0% |

**Incerteza**

| Apurado | Cobertura v1 | Cobertura v2 | Largura v1 | Largura v2 | Brier v1 | Brier v2 |
|---|---|---|---|---|---|---|
| 0,5% | 93% | 80% | 1,8 pt | 2,3 pt | 0,0000 | 0,0001 |
| 1% | 73% | 80% | 1,5 pt | 1,6 pt | 0,0000 | 0,0000 |
| 2% | 67% | 80% | 1,0 pt | 1,0 pt | 0,0000 | 0,0000 |
| 3% | 87% | 93% | 0,8 pt | 0,9 pt | 0,0000 | 0,0000 |
| 5% | 87% | 100% | 0,6 pt | 0,8 pt | 0,0000 | 0,0000 |
| 10% | 100% | 100% | 0,6 pt | 0,7 pt | 0,0000 | 0,0000 |
| 20% | 100% | 100% | 0,5 pt | 0,6 pt | 0,0000 | 0,0000 |
| 30% | 100% | 100% | 0,5 pt | 0,5 pt | 0,0000 | 0,0000 |
| 50% | 100% | 100% | 0,3 pt | 0,4 pt | 0,0000 | 0,0000 |
| 70% | 100% | 100% | 0,2 pt | 0,2 pt | 0,0000 | 0,0000 |
| 90% | 100% | 100% | 0,1 pt | 0,1 pt | 0,0000 | 0,0000 |

## Governador (50 eleições)

Resumo de todos os momentos: erro médio **0,61 (v1) → 0,58 (v2)** pontos; cobertura da faixa 98% → **90%**; Brier 0,0130 → **0,0071**; acerto do vencedor 98,9% → 99,1% (contagem do TSE: 93,2%); chamadas erradas: 0 → 0.

Momento de cravar (chance ≥ 95% e não cai mais), mediana: v1 1% apurado, v2 1%; cravadas erradas: 0 e 0.

**Erro médio da projeção (pontos percentuais)**

| Apurado | Contagem do TSE | v1 | v2 | v2 vs v1 |
|---|---|---|---|---|
| 0,5% | 4,34 | 1,76 | 1,68 | −5% |
| 1% | 4,21 | 1,65 | 1,64 | −1% |
| 2% | 3,88 | 1,18 | 1,09 | −8% |
| 3% | 3,60 | 0,99 | 0,92 | −8% |
| 5% | 3,06 | 0,76 | 0,81 | +7% |
| 10% | 2,50 | 0,35 | 0,33 | −7% |
| 20% | 2,00 | 0,29 | 0,27 | −6% |
| 30% | 1,67 | 0,21 | 0,18 | −13% |
| 50% | 1,13 | 0,14 | 0,12 | −13% |
| 70% | 0,67 | 0,09 | 0,08 | −14% |
| 90% | 0,25 | 0,03 | 0,03 | −5% |

**Incerteza**

| Apurado | Cobertura v1 | Cobertura v2 | Largura v1 | Largura v2 | Brier v1 | Brier v2 |
|---|---|---|---|---|---|---|
| 0,5% | 93% | 94% | 9,1 pt | 9,2 pt | 0,0330 | 0,0287 |
| 1% | 94% | 88% | 8,9 pt | 7,1 pt | 0,0261 | 0,0162 |
| 2% | 95% | 93% | 8,2 pt | 5,2 pt | 0,0285 | 0,0203 |
| 3% | 97% | 90% | 7,3 pt | 4,0 pt | 0,0207 | 0,0113 |
| 5% | 100% | 91% | 6,4 pt | 2,9 pt | 0,0167 | 0,0069 |
| 10% | 100% | 89% | 4,3 pt | 1,6 pt | 0,0116 | 0,0031 |
| 20% | 99% | 89% | 3,6 pt | 1,2 pt | 0,0094 | 0,0020 |
| 30% | 99% | 90% | 3,1 pt | 0,9 pt | 0,0067 | 0,0006 |
| 50% | 99% | 89% | 2,1 pt | 0,6 pt | 0,0025 | 0,0000 |
| 70% | 98% | 91% | 1,2 pt | 0,3 pt | 0,0008 | 0,0000 |
| 90% | 97% | 84% | 0,4 pt | 0,1 pt | 0,0000 | 0,0000 |

## Teste fora da amostra: 2026 (6 eleições)

Resumo de todos os momentos: erro médio **0,49 (v1) → 0,49 (v2)** pontos; cobertura da faixa 96% → **97%**; Brier 0,0168 → **0,0065**; acerto do vencedor 99,5% → 99,5% (contagem do TSE: 86,7%); chamadas erradas: 0 → 0.

Momento de cravar (chance ≥ 95% e não cai mais), mediana: v1 1% apurado, v2 0,8%; cravadas erradas: 0 e 0.

**Erro médio da projeção (pontos percentuais)**

| Apurado | Contagem do TSE | v1 | v2 | v2 vs v1 |
|---|---|---|---|---|
| 0,5% | 3,53 | 1,43 | 1,50 | +5% |
| 1% | 2,66 | 1,41 | 1,40 | −1% |
| 2% | 2,49 | 0,70 | 0,71 | +1% |
| 3% | 2,44 | 0,51 | 0,60 | +18% |
| 5% | 2,32 | 0,33 | 0,42 | +29% |
| 10% | 2,02 | 0,31 | 0,26 | −18% |
| 20% | 2,13 | 0,35 | 0,26 | −27% |
| 30% | 2,20 | 0,23 | 0,13 | −44% |
| 50% | 1,77 | 0,14 | 0,09 | −33% |
| 70% | 1,12 | 0,08 | 0,06 | −21% |
| 90% | 0,35 | 0,03 | 0,03 | −12% |

**Incerteza**

| Apurado | Cobertura v1 | Cobertura v2 | Largura v1 | Largura v2 | Brier v1 | Brier v2 |
|---|---|---|---|---|---|---|
| 0,5% | 100% | 100% | 13,4 pt | 11,4 pt | 0,0296 | 0,0183 |
| 1% | 94% | 94% | 8,4 pt | 6,0 pt | 0,0246 | 0,0148 |
| 2% | 89% | 100% | 6,1 pt | 3,8 pt | 0,0338 | 0,0225 |
| 3% | 89% | 100% | 5,7 pt | 3,0 pt | 0,0193 | 0,0080 |
| 5% | 89% | 100% | 5,0 pt | 2,2 pt | 0,0154 | 0,0021 |
| 10% | 100% | 100% | 3,8 pt | 1,5 pt | 0,0221 | 0,0052 |
| 20% | 100% | 100% | 2,9 pt | 1,0 pt | 0,0212 | 0,0018 |
| 30% | 100% | 100% | 2,3 pt | 0,8 pt | 0,0129 | 0,0000 |
| 50% | 100% | 94% | 1,6 pt | 0,5 pt | 0,0055 | 0,0000 |
| 70% | 100% | 94% | 1,0 pt | 0,3 pt | 0,0012 | 0,0000 |
| 90% | 94% | 83% | 0,4 pt | 0,1 pt | 0,0000 | 0,0000 |

## Disputas apertadas (até 3 pontos de diferença) (4 eleições)

Resumo de todos os momentos: erro médio **0,76 (v1) → 0,76 (v2)** pontos; cobertura da faixa 100% → **95%**; Brier 0,0554 → **0,0210**; acerto do vencedor 96,9% → 98,4% (contagem do TSE: 70,3%); chamadas erradas: 0 → 0.

Momento de cravar (chance ≥ 95% e não cai mais), mediana: v1 60% apurado, v2 15%; cravadas erradas: 0 e 0.

**Erro médio da projeção (pontos percentuais)**

| Apurado | Contagem do TSE | v1 | v2 | v2 vs v1 |
|---|---|---|---|---|
| 0,5% | 4,12 | 1,53 | 1,15 | −25% |
| 1% | 3,57 | 2,56 | 2,45 | −4% |
| 2% | 3,01 | 0,85 | 0,93 | +9% |
| 3% | 3,07 | 1,57 | 1,76 | +12% |
| 5% | 2,45 | 1,02 | 1,24 | +22% |
| 10% | 1,72 | 0,34 | 0,29 | −16% |
| 20% | 1,51 | 0,34 | 0,31 | −9% |
| 30% | 1,25 | 0,20 | 0,19 | −6% |
| 50% | 1,06 | 0,12 | 0,13 | +8% |
| 70% | 0,73 | 0,05 | 0,06 | +8% |
| 90% | 0,37 | 0,01 | 0,01 | +5% |

**Incerteza**

| Apurado | Cobertura v1 | Cobertura v2 | Largura v1 | Largura v2 | Brier v1 | Brier v2 |
|---|---|---|---|---|---|---|
| 0,5% | 100% | 100% | 9,7 pt | 8,2 pt | 0,0376 | 0,0363 |
| 1% | 100% | 92% | 12,1 pt | 9,3 pt | 0,0400 | 0,0274 |
| 2% | 100% | 100% | 12,3 pt | 7,2 pt | 0,1061 | 0,0635 |
| 3% | 100% | 92% | 10,8 pt | 5,7 pt | 0,0664 | 0,0201 |
| 5% | 100% | 92% | 9,7 pt | 4,3 pt | 0,0693 | 0,0169 |
| 10% | 100% | 100% | 4,2 pt | 1,6 pt | 0,0984 | 0,0390 |
| 20% | 100% | 100% | 3,7 pt | 1,2 pt | 0,0821 | 0,0254 |
| 30% | 100% | 92% | 3,0 pt | 0,9 pt | 0,0645 | 0,0072 |
| 50% | 100% | 83% | 2,0 pt | 0,5 pt | 0,0292 | 0,0001 |
| 70% | 100% | 100% | 1,1 pt | 0,3 pt | 0,0095 | 0,0000 |
| 90% | 100% | 100% | 0,4 pt | 0,1 pt | 0,0000 | 0,0000 |

## O que testamos e não entrou

Comparação das variantes do v2 no histórico (2010–2022), erro médio com todas as fatias de apuração pesando igual:

| Variante | Presidente | Governador |
|---|---|---|
| completa (votos novos + prior de variância) | 0,216 | 0,662 |
| sem o termo de votos novos | 0,166 | 0,665 |
| sem o prior de variância | 0,214 | 0,660 |
| sem os dois | 0,165 | 0,663 |

Escolhidas: **sem os dois** para presidente e **sem o prior de variância** para governador.

- O termo de **votos novos** (quem se absteve ou anulou no 1º turno e votou no 2º) piorou a projeção de presidente em cerca de 30% e quase não mudou a de governador. Ele continua ligado só para governador.
- O **prior de variância** entre estados/regiões não ajudou e foi desligado.
- O **índice de cobertura** (peso dos lugares ainda sem apuração) foi testado como termo da incerteza; a calibração deu peso praticamente zero a ele, porque o multiplicador por estágio da apuração já captura o mesmo efeito.
- Na versão inicial, usar o comportamento da seção entre 1º e 2º turno da eleição anterior como pista também não melhorou (testado com 2018 prevendo 2022).
- O **prior de pesquisa** está disponível na configuração, mas não foi avaliado: não há pesquisas de 2º turno de governador padronizadas para todas essas eleições.

## Calibração final da incerteza

`sd_final = sqrt( (m·sd)² + (b·pendente)² + d² )`, com `m = exp(α + β·log10(% apurado) + γ·[presidente])`

| α | β | γ | b | d |
|---|---|---|---|---|
| 0,110 | -0,813 | 0,250 | 0,0021 | 0,00029 |

Leitura: com 1% apurado a faixa do modelo é alargada cerca de 1,1×; com 10%, encolhida para 0,49×; para presidente, mais 28% de folga.

## Limitações

- O teste reproduz a apuração com dados finais por seção. Na vida real, os arquivos do TSE às vezes atrasam ou chegam fora de ordem (como na noite de 25/10/2026); isso não aparece na reprise.
- A ordem de chegada das eleições antigas é aproximada pelos horários de 2026. Até 2018 as urnas fechavam às 17h do horário local; desde 2022, às 17h de Brasília.
- Só 4 eleições ficaram a até 3 pontos de diferença; os números das disputas apertadas têm amostra pequena.
- Na faixa final (90% apurado) a cobertura do v2 fica em torno de 85%, um pouco abaixo da meta, com erros de poucos centésimos de ponto.
