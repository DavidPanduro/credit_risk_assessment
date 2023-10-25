# Credit Risk Assessment Model
Por David Panduro 💻<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/51c1c1f3-79cb-469c-99aa-b35fc862aef8)

<br><br>
CONTEXTO:<br><br>
No seguinte estudo trabalharemos sobre o suposto de uma Empresa Financeira que já possui uma Política (AS-IS) de gestão de risco de crédito, que consiste em reprovar qualquer pessoa que tenha idade igual ou inferior a 28 anos. Ou seja: se alguém nessa faixa etária solicita crédito à instituição financeira, sua solicitação é negada.
<br><br>
OBJETIVO:<br><br>
Atualmente, a Empresa deseja desenvolver um modelo de concessão de crédito (Política do Modelo - classificação binário) que consiga calcular o score dos clientes, em termos de probabilidade para convertirse em um bom/mau pagador (lembrando que a regra do negócio para ser mau pagador consiste em que o cliente registre atraso > 60 dias). <br><br>

O score gerado pelo modelo de machine learning proposto pode ser utilizado para gerar uma segunda política: uma vez que ele mapeia a propensão da pessoa não honrar o empréstimo, o cliente pode substituir o ponto de corte em Idade para um novo ponto de corte no Score. Perceba que a reprovação do crédito agora ocorrerá acima do ponto de corte, e não abaixo, como ocorreu com a idade. Ou seja, se o ponto de corte for T (com T entre 0 e 1), então os reprovados serão aqueles com score score >= T.<br><br>

Para realizar a análise financeira do seu modelo, suponha que todas as pessoas da base de Teste solicitaram crédito à instituição financeira, na forma de um empréstimo de R$1000,00. Faça o seguinte:<br><br>

1. Calcule qual o tamanho da carteira de crédito aprovado (i.e. quanto de dinheiro a Financeira emprestou) na base de Teste, pela Política AS-IS.
2. Calcule qual a dívida total (suponha que os inadimplentes não pagaram nenhuma parcela do empréstimo), pela Política AS-IS.
3. Calcule qual o percentual das pessoas da base de Teste que tiveram a solicitação negada. Agora crie um ponto de corte de seu Score que nega o empréstimo para exatamente o mesmo percentual de pessoas (i.e. o empréstimo será negado para quem tiver o Score igual ou superior ao ponto de corte). Essa é a Política do Modelo.
4. Calcule o novo tamanho da carteira de crédito aprovado e a dívida total na Política AS-IS.
<br><br>

BASES:<br><br>
A base contém 150 variáveis, a maioria das quais está mascarada. Utilize a coluna ID como uma key.<br><br>

A variável alvo é denominada TARGET e possui os seguintes valores:<br><br>

1: Bom Pagador, atraso > 60 dias em 2 meses.<br>
0: Mau Pagador, caso contrário.<br><br>
O score do modelo de classificação deve mapear a classe Bom Pagador.<br><br>

Treino: base usada para treinamento contendo dados de janeiro a agosto de 2017<br>
Teste: base usada para testes contendo dados de janeiro a agosto de 2017<br><br>
<br>
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

FEATURES SELECTION - RANDOM FOREST:<br><br>
Neste caso, a importancia das variáveis medida pela diminuição na pontuação de impureza Gini ou pela diminuição na métrica de erro médio.<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/72fefb4e-6c2f-440d-9b4c-5d83bd34e9aa)
<br><br>
FEATURES SELECTION - MÈTODO LASSO:<br><br>
Lasso é uma técnica eficaz para reduzir a dimensionalidade dos dados, eliminando características menos importantes. O Lasso é uma técnica de regularização que adiciona uma penalização L1 à função de custo do modelo. 
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/1085c724-0e6d-48d7-926c-2b76eb7ca74c)<br><br>
FEATURES SELECTION - RECURSIVE FEATURE ELIMINATION (RFE) <br><br>
RFE funciona eliminando iterativamente as características menos importantes de um conjunto de dados.<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/26dbae96-e54a-4f25-8c07-c9687b68049c)<br><br>
FEATURES SELECTION - MÉTODO BORUTA<br><br>
Boruta opera por meio de uma abordagem de eliminação gradual de recursos, comparando as características originais com um conjunto de características aleatórias (ruído).<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/37dc3aa5-fb8e-4296-b829-54f48e7f7823)<br><br>
BALANCEAMENTO DOS DADOS:<br><br>
Utilizamos uma abordagem para ajustar o modelo de classificação, neste caso, um RandomForestClassifier, usando a técnica de sobreamostragem (SMOTE) para lidar com desequilíbrio de classes. Realizamos uma busca em grade para otimizar a estratégia de amostragem do SMOTE usando validação cruzada olhando as pontuações F1 em relação às diferentes estratégias de amostragem.<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/6688228e-84d4-49c2-a7d9-02d12d7fb751)<br>
Assim usamos a **sampling_strategy = 0.2469**
<br><br>
APLICAÇÂO DE ALGORITMOS:
<br><br>
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

**Em termos financeiros, com a aplicação do Modelo conseguimos um incremento de 1.4% de lucro e uma diminução de 1.4% de dívida.** 




























