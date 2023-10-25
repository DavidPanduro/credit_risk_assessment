# Credit Risk Assessment Model
Por David Panduro 💻<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/51c1c1f3-79cb-469c-99aa-b35fc862aef8)<br><br>

CONTEXTO:<br><br>

Neste estudo, abordaremos o cenário de uma Empresa Financeira que já possui uma Política (AS-IS) de gestão de risco de crédito. Essa política consiste em rejeitar qualquer pessoa que tenha 28 anos de idade ou menos. Em outras palavras, se alguém dentro dessa faixa etária solicitar crédito à instituição financeira, a solicitação é negada.<br><br>

OBJETIVO:<br><br>

Atualmente, a empresa deseja desenvolver um modelo de concessão de crédito (Política do Modelo - classificação binária) capaz de calcular o score dos clientes em termos de probabilidade de se tornarem bons ou maus pagadores. É importante destacar que, para ser classificado como mau pagador de acordo com as regras do negócio, o cliente deve apresentar atrasos superiores a 60 dias em seus pagamentos.<br><br>

O score gerado pelo modelo de machine learning proposto pode ser utilizado para criar uma segunda política. Essa política permite que a empresa substitua o critério de idade por um novo critério baseado no Score. Nesse caso, a reprovação do crédito ocorrerá acima do ponto de corte do Score, ao contrário do que ocorria com a idade. Em outras palavras, se o ponto de corte for denotado como "T" (com "T" variando entre 0 e 1), os solicitantes com um score maior ou igual a "T" terão suas solicitações negadas.<br><br>

Para realizar a análise financeira do modelo, suponha que todas as pessoas na base de Teste solicitaram crédito à instituição financeira na forma de um empréstimo de R$1000,00. Nesse contexto, faça o seguinte:<br><br>

1. Calcule o valor total da carteira de crédito aprovado (ou seja, o montante de dinheiro emprestado pela instituição financeira) de acordo com a Política AS-IS.
2. Calcule o valor total da dívida (supondo que os inadimplentes não tenham pago nenhuma parcela do empréstimo) de acordo com a Política AS-IS.
3. Calcule a porcentagem de pessoas na base de Teste que tiveram suas solicitações negadas de acordo com a Política AS-IS. Em seguida, defina um ponto de corte para o Score de modo que o mesmo percentual de pessoas tenha suas solicitações negadas (ou seja, o empréstimo será negado para quem tiver um Score igual ou superior ao ponto de corte). Essa será a Política do Modelo.
4. Calcule o novo valor total da carteira de crédito aprovado e o valor total da dívida de acordo com a Política AS-IS.
<br><br>

BASES:<br><br>

A base de dados contém 150 variáveis, a maioria das quais está mascarada. Utilize a coluna ID como chave primária.<br><br>

A variável alvo é denominada TARGET e possui os seguintes valores:<br><br>

1: Bom Pagador, para atrasos superiores a 60 dias em 2 meses.<br>
0: Mau Pagador, caso contrário.<br>
O objetivo do modelo de classificação é mapear a classe "Bom Pagador."<br><br>

Conjuntos de Dados:<br><br> 

* Treino: conjunto de dados usado para o treinamento, abrangendo o período de janeiro a agosto de 2017.<br>
* Teste: conjunto de dados usado para testes, também abrangendo o período de janeiro a agosto de 2017.<br><br>

![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/6afd5262-969e-4a5f-9ff8-5c5c87bcf9d8)<br>
Podemos observar que as variáveis estão mascaradas.


i) Regra de Negócio: Não trabalharemos com Variáveis que apresentem mais de 40% de valores ausentes <br><br>
Preferimos deixar essas colunas para futuras análises.<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/2324ebd5-1d5c-440b-bbc3-6c62412a4b58)<br>
Procedemos a remover essas colunas do nosso conjunto de dados<br><br>
ii) Regra de Negócio: Trabalharemos com Idade menor de 90 anos <br><br>
Seguindo a política da maioría dos bancos brasileiros, que tem como idade limite para empréstimos, 80 anos de idade. Consideraremos um margen de erro de 10 anos para empréstimos e a partir disso desconsideraremos no nosso conjunto de dados<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/860d8606-90d5-4360-85ca-f168535da9a3)<br><br>

DIMENSÂO DO DATASET:<br><br>
A dimensão dos nossos dados em relação à variável resposta é como segue:<br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/f65e7b1d-4d75-474e-89f1-750709cd4158)<br><br>

TRATAMENTO DE OUTLIERS:<br><br>
Detectamos 05 variáveis com outliers significativos, e resolvimos trata-los mediante o método IQR.

IMPUTAÇÂO DE VALORES NULOS: <BR><BR>
Em alguns casos resolvimos usar uma nova categoria "outros", em outros casos aplicamos a média para variáveis numéricas e para variáveis categóricas aplicamos a "moda".
<br><br>
Finalmente, observamos a quantidade de dados nulos no conjuntos de dados e temos:
<br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/c686a907-9037-4bd2-aa6f-472bb2291abc)<br><br>
Verificamos mostrando a Matríz de dados faltantes:<br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/5f221f1a-18bd-47bb-a2f4-5f7f8abbb45e)<br><br>
TRANFORMAÇÔES:<br><br>
Aplicamos diferentes transformações segundo o tipo e comportamento dos nossos dados, entre as diferentes transformações temos:<br>
  * Tranformação por Natureza: Usada para capturar padrões cíclicos nos dados.
  * MCA: Análise de correspondência múltipla, é uma técnica estatística para analisar dados categóricos, semelhante à PCA que é usada para daddos numéricos.
  * Criação de Macro-Regiões: Tratamos a coluna estados do Brasil, transformando a macro-regios e assim evitar piorar o dimensionamento no nosso conjunto de dados.
  * Encoders: Aplicando LabelEnconder (quando os nossos dados não respondem a uma ordem), OrdinalEncoders (quando os nossos dados obedecem uma ordem).
  * Rescaling: RobustScaler (quando os nossos dados tem presença de outliers), MinMaxScaler (quando os nossos dados não apresentam outliers).
<br><br>
CONJUNTO DE DADOS FINAL:<br><br>
Finalmente temos 27 variáveis preditoras mais a variável TARGET<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/4b730f05-f7d4-4bc3-9319-48d160779ee5)<br><br>

FEATURES SELECTION - RANDOM FOREST:<br>
Neste caso, a importancia das variáveis medida pela diminuição na pontuação de impureza Gini ou pela diminuição na métrica de erro médio.<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/72fefb4e-6c2f-440d-9b4c-5d83bd34e9aa)
<br><br>
FEATURES SELECTION - MÈTODO LASSO:<br>
Lasso é uma técnica eficaz para reduzir a dimensionalidade dos dados, eliminando características menos importantes. O Lasso é uma técnica de regularização que adiciona uma penalização L1 à função de custo do modelo. 
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/1085c724-0e6d-48d7-926c-2b76eb7ca74c)<br><br>
FEATURES SELECTION - RECURSIVE FEATURE ELIMINATION (RFE) <br>
RFE funciona eliminando iterativamente as características menos importantes de um conjunto de dados.<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/26dbae96-e54a-4f25-8c07-c9687b68049c)<br><br>
FEATURES SELECTION - MÉTODO BORUTA<br>
Boruta opera por meio de uma abordagem de eliminação gradual de recursos, comparando as características originais com um conjunto de características aleatórias (ruído).<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/37dc3aa5-fb8e-4296-b829-54f48e7f7823)<br><br>
BALANCEAMENTO DOS DADOS:<br>
Utilizamos uma abordagem para ajustar o modelo de classificação, neste caso, um RandomForestClassifier, usando a técnica de sobreamostragem (SMOTE) para lidar com desequilíbrio de classes. Realizamos uma busca em grade para otimizar a estratégia de amostragem do SMOTE usando validação cruzada olhando as pontuações F1 em relação às diferentes estratégias de amostragem.<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/6688228e-84d4-49c2-a7d9-02d12d7fb751)<br>
Assim usamos a **sampling_strategy = 0.2469**
<br><br>
APLICAÇÂO DE ALGORITMOS:
<br>
Aplicamos diferentes algoritmos, com validação cruzada, para a obtenção de um modelo que consiga performar melhor. A continuação os resultados<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/873a1714-7830-4874-96cc-9987dca1a394)<br><br>
A principio, os resultados não são os melhores que desejariamos ter obtido, mas serve como um baseline para trabalhar na procura de uma solução mais robusta.<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/891295fa-890e-4b70-97e2-681319462c08)<br>
Observamos a Matríz de Confusão do modelo LGBM<br><br>

Nesse sentido, escolheremos o **Modelo LightGBM** para continuar com o estudo.  <br>

EXPLICABILIDADE DO MODELO:<br><br>
O SHAP é baseado em teoria dos jogos e atribui valores Shapley a cada característica, indicando a importância relativa de cada uma para uma previsão específica. <br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/53189266-349d-490f-8929-7ff9f7cf79b6)<br><br>

DISTRIBUIÇÂO DE PROBABILIDADES DAS PREVISÔES DO MODELO: <br><br>
Agora tentaremos ver se o nosso modelo está conseguindo discriminar ambas classes.<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/2e6bff55-6931-48e8-be53-e8cf957e5203)<br>
Por ser um baseline, ainda estamos distantes de conseguir distanciar de maneira ótima as duas classes.<br>
<br>

ANÁLISE FINANCEIRA:<br><br>

![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/e939d62c-a324-435e-8ba4-a0051b4b4985)<br><br>

![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/c5255a41-6629-4830-9b79-cb0b6e71ccc2)<br><br>

![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/8c14d4ea-30d2-4d3e-8b1b-29b94dee52c5)<br><br>

![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/13c4acfe-5b0b-427d-bd79-fe7036b25e4b)<br>
DIstribuição dos nossos scores definidos pelo Modelo <br><br>

![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/c072749c-093d-4fc9-b3ca-74c4ec814f2b)<br><br>
Com a Política do Modelo, para poder ter o mesmo percentual de 22.5% aprox de solicitações de Empréstimo Negadas dado pela Política AS-IS.
Devemos fazer o CORTE em 42% aprox . Menor que esse Score, deve ser negado o crédito.<br><br>

![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/c52110da-dc55-4d7a-8a34-468514b82ea5)<br>
Com a Política do Modelo conseguimos uma tendencia positiva nos cliente "Bom", conseguindo estabilizar e até criar uma tendencia negativa nas perdas (clientes "MAU").
<br><br>

**Em termos financeiros, com a aplicação do Modelo e a definição do Threshold conseguimos:<br><br>
* Incrementar em 1.4% de lucro.
* Diminuir em 1.4% de dívida. 




























