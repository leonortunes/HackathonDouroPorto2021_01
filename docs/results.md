---
layout: page
title: Resultados
description: Resultados do objectivo 1
---

# Resultados

## Preparação dos dados

Os dados, gentilmente cedidos pela ADVID, correspodem a dados da Quinta de Soutelo com as seguintes características:

| Parâmetro | Anos | Frequência | Início | Fim | Tipo de Recolha |
| ---       | ---  |  ----      | ---    | --- | ---   |
| Precepitação | desde 2015 | 15 min. | 01/01/2015 | 26/10/2021 | Estação Meteorológica |
| Temperatura  | desde 2015 | 15 min. | 01/01/2015 | 26/10/2021 | Estação Meteorológica |
| Humidade Relativa | desde 2015 | 15 min. | 01/01/2015 | 26/10/2021 |  Estação Meteorológica |
| Insolação | desde fev. 2020 | 15 min. | 01/02/2020 | 26/10/2021 |  Estação Meteorológica |
| Velocidade do Vento | desde fev. 2020 | 15 min. | 01/02/2020 | 26/10/2021 |  Estação Meteorológica |
| Direção do Vento | desde fev. 2020 | 15 min. | 01/02/2020 | 26/10/2021 |  Estação Meteorológica |
| ET0 | desde fev. 2020|  1 hora | 01/02/2020 | 26/10/2021 |  Estação Meteorológica |
| PH base[^1] | desde jun. 2015 | 1 semana[^2] | 25/06/2015 | 02/09/2021 | Manual |
| Humidade do Solo | desde maio 2020 | 15 min. | 25/05/2020 | 25/10/2021 | Sondas |

A figura seguinte mostra alguns dos dados a analisar.

![Imgur](https://i.imgur.com/XFZpbQ4.png)

Numa primeira seleção, decidiu-se analisar os dados de 2020. Somente os anos de 2020 e 2021 englobavam todos os parâmetros e o ano de 2021 tinha mais falhas nos dados do PH base. 

Como os dados têm diferentes frequências de amostragem, procedeu-se a uma uniformização tendo como base uma frequência diária. 

![Imgur](https://i.imgur.com/atbEPhc.png)

Os dados do Potencial Hídrico de base têm uma frequência semanal sendo, por isso, necessário utilizar uma aproximação linear para 'preencher' os dados em falta.

## Avaliação

Depois destes passos na preparação dos dados, foi utilizada uma plataforma para Data Science e Machine Learning - [RapidMiner](https://rapidminer.com/), tendo sido obtidos os seguintes resultados:



|Model	|Correlation	|Standard Deviation|	Total Time (ms)	|Training Time (1,000 Rows)	|Scoring Time (1,000 Rows)|
| :--- | :---: | :---: | :---: | :---: | :---: | 
|Generalized Linear Model |	0,923 |	0,000754 |	4821 |	173,6 |	43,4 |
|Deep Learning |	0,933 |	0,000058 |	9761 |	1525,5 |	257,2 |
|Decision Tree |	1,000 |	0,000000 |	505	 | 10,4	 | 31,8 |
|Random Forest |	1,000 |	0,000000 |	7935 |	134,3 |	598,3 |
|Gradient Boosted Trees |	1,000 |	0,000000 |	41547 |	501,2 |	46,2 |
|Support Vector Machine	| 0,979	| 0,002604 |	102634 |	7169,0 |	69,4 |

Deste modo, vemos que existem pelo menos 3 modelos (Decision Tree, Random Forest e Gradient Boosted Trees), que garantem uma correlação perfeita entre a humidade do solo e o Potencial Hídrico de base.

A título meramente de exemplo, apresenta-se o gráfico de dispersão entre a Humidade do Solo e o Potencial Hídrico de base, e o Potencial Hídrico de base previsto, sendo que o erro máximo é na ordem 0,081 %.

![Dispersão 1](https://i.imgur.com/z9xLT66.png)

Na imagem seguinte podemos ver o gráfico de dispersão entre os valores reais e previstos do Potencial Hídrico de base:

![Dispersão 2](https://i.imgur.com/87DR9Id.png)

Nas próximas imagens podemos observar dois modelos: Gradient Boosted Trees e Random Forest.

![Gradient Boosted Trees Model](https://i.imgur.com/UwCe8GJ.png)

![Random Forest Model](https://i.imgur.com/BGGf4S6.png)

### Avalição sem considerar a humidade do solo

As simulações realizadas, onde se obtiveram excelentes resultados, recorreram a dados da humidade do solo de bastante qualidade e confiança. Esses dados, foram obtidos através de uma sonda [EnviroSCAN da Sentek](https://sentektechnologies.com/product-range/soil-data-probes/enviroscan/?gclid=CjwKCAiAtdGNBhAmEiwAWxGcUtl4S30Mympqj6JVECBYYTX3DGccX_9WpkWaLC3ry23Ulh-RGx94ChoCn1kQAvD_BwE). No entanto, trata-se de um equipamento dispendioso e fora do alcance de muitos produtores. Como esteve sempre presente a ideia de 'low cost' para este desafio, foi também feita uma avaliação não considerando as medições do sensor de humidade do solo, tendo sido obtidos os seguintes resultados:

|Model |	Correlation |	Standard Deviation |
| :--- | :---: | :---: |
|Generalized Linear Model	| 0,872	| 0,008 |
|Deep Learning |	0,871 |	0,008 |
|Decision Tree	| 0,878	| 0,006 |
|Random Forest	| 0,874	| 0,006 |
|Gradient Boosted Trees	| 0,874	| 0,006 |
|Support Vector Machine	| 0,838	| 0,018 |

Com uma validação na ordem dos 37.81 %.

Obtendo-se os seguintes modelos:

![Decision Tree](https://i.imgur.com/bEjhnzS.png)

![Random Forest](https://i.imgur.com/zsNxOks.png)

Obtendo o seguinte gráfio de previsões.

![SVM Predictions Chart](https://i.imgur.com/sYAoIfC.png)


[^1]: PH base - Potencial Hídrico de base. [Medido através da Câmara de Scholander](https://www.advid.pt/pt/servicos/viticultura/monitorizacao-do-estado-hidrico-da-videira).
[^2]: Como a recolha dos dados é manual, recorrendo à Câmara de Scholander, a frequência é, aproximadamente, semanal. No entanto, existem semanas onde não existiu recolha de dados.

&nbsp;

*** 

&nbsp;

[![CC BY 4.0](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)

This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/)
