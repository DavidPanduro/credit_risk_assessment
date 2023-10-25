# Credit Risk Assessment Model
Por David Panduro 💻<br><br>
![image](https://github.com/DavidPanduro/credit_risk_assessment/assets/45201867/51c1c1f3-79cb-469c-99aa-b35fc862aef8)

<br><br>
CONTEXTO:<br><br>
No seguinte estudo trabalharemos sobre o suposto de uma Empresa Financeira que já possui uma (Política AS-IS) de gestão de risco de crédito, que consiste em reprovar qualquer pessoa que tenha idade igual ou inferior a 28 anos. Ou seja: se alguém nessa faixa etária solicita crédito à instituição financeira, sua solicitação é negada.
<br><br>
OBJETIVO:<br><br>
Atualmente, a Empresa deseja desenvolver um modelo de concessão de crédito (classificação binário) que consiga calcular o score dos clientes, em termos de probabilidade para convertirse em um bom/mau pagador (lembrando que a regra do negócio para ser mau pagador consiste em que o cliente registre atraso > 60 dias). <br><br>

O score gerado pelo modelo de machine learning proposto pode ser utilizado para gerar uma segunda política: uma vez que ele mapeia a propensão da pessoa não honrar o empréstimo, o cliente pode substituir o ponto de corte em Idade para um novo ponto de corte no Score. Perceba que a reprovação do crédito agora ocorrerá acima do ponto de corte, e não abaixo, como ocorreu com a idade. Ou seja, se o ponto de corte for T (com T entre 0 e 1), então os reprovados serão aqueles com score score >= T.<br><br>

ANÁLISE FINANCEIRA: <br><br>

Para realizar a análise financeira do seu modelo, suponha que todas as pessoas da base de Teste solicitaram crédito à instituição financeira, na forma de um empréstimo de R$1000,00. Faça o seguinte:<br><br>

1. Calcule qual o tamanho da carteira de crédito aprovado (i.e. quanto de dinheiro a Financeira emprestou) na base de Teste, pela Política AS-IS.
2. Calcule qual a dívida total (suponha que os inadimplentes não pagaram nenhuma parcela do empréstimo), pela Política AS-IS.
3. Calcule qual o percentual das pessoas da base de Teste que tiveram a solicitação negada. Agora crie um ponto de corte de seu Score que nega o empréstimo para exatamente o mesmo percentual de pessoas (i.e. o empréstimo será negado para quem tiver o Score igual ou superior ao ponto de corte). Essa é a Política do Modelo.
4. Calcule o novo tamanho da carteira de crédito aprovado e a dívida total na Política AS-IS.






