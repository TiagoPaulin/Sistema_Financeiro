# Elicitação de Requisitos do Projeto

Este documento registra os requisitos funcionais que definem os comportamentos e funcionalidades esperados do sistema.

## Requisitos Funcionais

### Usuário

- **RF01**: O sistema deve permitir que o usuário realize login na plataforma informando email e senha cadastrados gerando um token de acesso para o cliente e um refresh token no servidor.
- **RF02**: O sistema deve permitir que o usuário realize cadastro informando nome, email e senha.
- **RF03**: O sistema deve permitir que o usuário realize logout descartando o token de acesso dele no cliente e invalidando o refresh token no servidor.
- **RF04**: O sistema deve permitir que o usuário autenticado altere seu nome.
- **RF05**: O sistema deve permitir que o usuário autenticado altere seu email.
- **RF06**: O sistema deve permitir que o usuário autenticado altere sua senha mediante confirmação da senha atual.
- **RF07**: O sistema deve permitir que o usuário solicite a recuperação de senha informando seu email cadastrado.
- **RF08**: O sistema deve enviar um link de recuperação de senha para o email cadastrado quando uma solicitação de recuperação for realizada.
- **RF09**: O sistema deve permitir que o usuário redefina sua senha por meio de um link de recuperação válido.

### Contas

- **RF10**: O sistema deve permitir que o usuário autenticado cadastre uma conta informando nome, tipo (corrente, poupança ou carteira), saldo inicial e data de referência do saldo inicial.
- **RF11**: O sistema deve permitir que o usuário autenticado altere o nome e o tipo de uma conta cadastrada.
- **RF12**: O sistema deve permitir que o usuário arquive uma conta cadastrada.
- **RF13**: O sistema deve permitir que o usuário desarquive uma conta anteriormente arquivada.
- **RF14**: O sistema deve listar as contas não arquivadas do usuário autenticado, exibindo o saldo atual de cada conta, o saldo total disponível nas contas, o valor total dos investimentos e o patrimônio financeiro total do usuário.
- **RF15**: O sistema deve permitir selecionar uma conta para ver o histórico de movimentações.
- **RF16**: O sistema deve permitir que o usuário registre transferências entre suas contas, gerando uma saída na conta de origem e uma entrada na conta de destino, sem contabilizar a operação como receita ou despesa nos indicadores financeiros.
- **RF17**: O sistema deve calcular o saldo atual de uma conta considerando seu saldo inicial e as movimentações que afetam seu saldo, respeitando a respectiva data de referência.
- **RF18**: O sistema deve permitir que o usuário registre ajustes de saldo em suas contas, informando o valor do ajuste, a data e uma descrição.

### Categorias

- **RF19**: O sistema deve permitir que o usuário crie uma categoria informando nome e tipo (entrada ou saída).
- **RF20**: O sistema deve permitir que o usuário renomeie uma categoria.
- **RF21**: O sistema deve permitir que o usuário arquive uma categoria.
- **RF22**: O sistema deve permitir que o usuário desarquive uma categoria arquivada.
- **RF23**: O sistema deve ocultar categorias arquivadas das opções de seleção em novos lançamentos, mantendo-as disponíveis para consulta no histórico de movimentações.
- **RF24**: O sistema deve permitir que o usuário visualize o total de entradas e saídas agrupadas por categoria, considerando um período definido.
- **RF25**: O sistema deve permitir que o usuário visualize o total de entradas e saídas agrupadas por categoria e conta, considerando um período definido.

### Movimentações

- **RF26**: O sistema deve permitir que o usuário registre um lançamento informando tipo (entrada ou saída), data, valor, descrição, categoria e conta.
- **RF27**: O sistema deve permitir que o usuário altere o valor de um lançamento.
- **RF28**: O sistema deve permitir que o usuário altere a data de um lançamento.
- **RF29**: O sistema deve permitir que o usuário altere a descrição de um lançamento.
- **RF30**: O sistema deve permitir que o usuário altere o tipo de um lançamento.
- **RF31**: O sistema deve permitir que o usuário altere a categoria de um lançamento.
- **RF32**: O sistema deve permitir que o usuário altere a conta à qual uma movimentação financeira está vinculada.
- **RF33**: O sistema deve permitir que o usuário exclua um lançamento.
- **RF34**: O sistema deve listar os lançamentos de um mês, permitindo filtrar por tipo, categoria, conta e data.

### Investimentos

- **RF35**: O sistema deve permitir registrar um aporte em investimento de renda fixa, informando a conta de origem, o valor aplicado, a modalidade do investimento (CDB, LCI ou LCA), o tipo de rentabilidade (prefixada ou pós-fixada), a taxa contratada (% a.a. ou % do CDI), a data da aplicação e a data de vencimento.
- **RF36**: O sistema deve permitir registrar a compra de ações, informando a conta de origem, o código do ativo (ex.: BBAS3, PETR4), a quantidade de ações compradas, o preço unitário de compra, a data da operação e eventuais custos operacionais.
- **RF37**: O sistema deve exibir o total aportado em cada modalidade de investimento, considerando os aportes realizados e os resgates ou vendas registrados.
- **RF38**: O sistema deve permitir visualizar os valores investidos agrupados por instituição financeira responsável pela custódia dos investimentos.
- **RF39**: O sistema deve permitir visualizar os detalhes de cada aplicação ou posição de investimento, incluindo os dados de contratação, aportes, resgates e situação atual.
- **RF40**: O sistema deve permitir visualizar a quantidade total de ações de cada ativo em carteira, o valor total investido e o preço médio de aquisição.
- **RF41**: O sistema deve permitir registrar o resgate total ou parcial de um investimento de renda fixa, informando o valor recebido, a data do resgate e a conta de destino.
- **RF42**: O sistema deve registrar automaticamente uma entrada na conta de destino correspondente ao valor recebido pelo resgate de um investimento.
- **RF43**: O sistema deve permitir visualizar o lucro ou prejuízo realizado em cada investimento após seu resgate, considerando a diferença entre o valor recebido e o valor investido correspondente.
- **RF44**: O sistema deve permitir registrar a venda total ou parcial de ações, informando o ativo, a quantidade de ações vendidas, o preço unitário de venda, a data da operação, os custos operacionais e a conta de destino.
- **RF45**: O sistema deve permitir cadastrar posições de investimentos já existentes, informando seus dados e uma data de referência, sem gerar movimentações financeiras fictícias nas contas do usuário.
- **RF46**: O sistema deve permitir que o usuário corrija ou cancele operações de investimento registradas incorretamente, atualizando os saldos e posições afetados.

