# Banco de dados - SQL 	:books:

Este banco de dados foi criado em um trabalho do primeiro semestre da faculdade de Desenvolvimento de Software Multiplataforma, na Fatec Franca.

# Cenário :bookmark_tabs:

A empresa "Banco Tech" está buscando a implementação de um novo sistema de controle bancário para aprimorar suas operações diárias, melhorar a eficiência do atendimento ao cliente e garantir maior segurança no gerenciamento de dados financeiros. Este sistema terá como foco principal a gestão de clientes, suas contas, transações financeiras e produtos financeiros oferecidos pelo banco.
As principais funcionalidades do banco de dados dessa empresa incluem clientes, contas bancárias, transações financeiras, produtos financeiros e funcionários. Com campos específicos que armazenam informações relevantes para o funcionamento do banco.
Um cliente pode ter uma ou várias contas bancárias, e cada conta bancária está associada a um único cliente. Da mesma forma, uma transação financeira está vinculada a uma conta bancária específica.
Além disso, o sistema contempla a oferta de produtos financeiros, como empréstimos pessoais e investimentos em renda fixa, e os clientes podem aderir a esses produtos.

# Modelagem Conceitual 	:card_index_dividers:


<img src="img/modelo_conceitual.png">


# Modelagem Lógica 	:card_index_dividers:


<img src="img/modelo_logico.png">


# Dados 	:bar_chart:

Os dados foram inseridos através do sistema SQL Server Management Studio

Verificar o código no arquivo: dados.sql

<img src="img/modelagem_fisica.png">

# Relatórios :memo:

:desktop_computer: Consulta 1: Informações Detalhadas do Cliente e suas Contas:

SELECT c.id_cliente, c.nome, c.cpf, cb.id_conta, cb.tipo, cb.saldo
FROM cliente c
JOIN conta cb ON c.id_cliente = cb.id_cliente;

<img src="img/consulta1.png">

:desktop_computer: Consulta 2: Transações Realizadas por um Cliente:

SELECT c.nome, t.id_transacao, t.tipo, t.valor, t.data
FROM cliente c
JOIN conta cb ON c.id_cliente = cb.id_cliente
JOIN transacao t ON cb.id_conta = t.id_conta
WHERE c.nome = 'João Silva';

<img src="img/consulta2.png">

:desktop_computer: Consulta 3: Produtos Financeiros Associados a uma Conta Bancária:

SELECT c.nome, cb.id_conta, pf.nome AS produto_financeiro
FROM cliente c
JOIN conta cb ON c.id_cliente = cb.id_cliente
JOIN cliente_produto_financeiro cpf ON c.id_cliente = cpf.id_cliente
JOIN produto_financeiro pf ON cpf.id_produto = pf.id_produto;

<img src="img/consulta3.png">

:desktop_computer: Consulta 4: Saldo Atual de Todas as Contas Bancárias:

SELECT cb.id_conta, c.nome, cb.saldo
FROM conta cb
JOIN cliente c ON cb.id_cliente = c.id_cliente
ORDER BY cb.saldo DESC;

<img src="img/consulta4.png">

:desktop_computer: Consulta 5: Histórico de Transações por Tipo e Valor:

SELECT t.tipo, t.valor, t.data, c.nome AS cliente, cb.id_conta
FROM transacao t
JOIN conta cb ON t.id_conta = cb.id_conta
JOIN cliente c ON cb.id_cliente = c.id_cliente
WHERE t.tipo = 'Depósito' AND t.valor > 1000
ORDER BY t.data DESC;

<img src="img/consulta5.png">

:desktop_computer: Consulta 6: Produtos Financeiros com Taxa de Juros Superior a 7%

SELECT nome, descricao, taxa_juros
FROM produto_financeiro
WHERE taxa_juros > 7;

<img src="img/consulta6.png">

:desktop_computer: Consulta 7: Clientes que Adquiriram Produtos Financeiros:

SELECT c.nome, pf.nome AS produto_financeiro
FROM cliente c
JOIN cliente_produto_financeiro cpf ON c.id_cliente = cpf.id_cliente
JOIN produto_financeiro pf ON cpf.id_produto = pf.id_produto;

<img src="img/consulta7.png">

:desktop_computer: Consulta 8: Lista de funcionários ordenados por data de contratação (do mais novo para o mais antigo):

SELECT nome, data_contratacao
FROM funcionario
ORDER BY data_contratacao DESC;

<img src="img/consulta8.png">

:desktop_computer: Consulta 9: Soma total do saldo de todas as contas:

SELECT SUM(saldo) AS saldo_total
FROM conta;

<img src="img/consulta9.png">

:desktop_computer: Consulta 10: Funcionários que são Gerentes de Contas

SELECT *
FROM funcionario
WHERE cargo = 'Gerente de Contas';

<img src="img/consulta10.png">






























