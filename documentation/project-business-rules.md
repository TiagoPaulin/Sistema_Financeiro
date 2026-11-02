# Regras de Negócio

Este documento registra as regras que definem as restrições e condições que devem ser respeitadas pelo sistema.

## Usuários

- **BR01**: Cada endereço de email deve ser único, não sendo permitido que dois usuários possuam o mesmo email cadastrado.
- **BR02**: O endereço de email deve ser armazenado em formato padronizado, não diferenciando letras maiúsculas de minúsculas para fins de identificação e validação de unicidade.

## Contas

- **BR03**: O saldo inicial de uma conta deve representar o valor disponível na data de referência informada pelo usuário.
- **BR04**: Movimentações com data anterior à data de referência do saldo inicial não devem afetar o saldo atual da conta.
- **BR05**: O saldo atual de uma conta deve ser calculado considerando o saldo inicial e as movimentações que afetam seu saldo na data de referência ou posteriormente.
- **BR06**: Contas arquivadas não devem estar disponíveis para novos lançamentos ou transferências, mas seu histórico deve permanecer acessível.
- **BR07**: O saldo de uma conta pode assumir valores negativos, não devendo o sistema bloquear movimentações exclusivamente por insuficiência de saldo.

## Categorias

- **BR08**: Uma categoria deve possuir exclusivamente um tipo, podendo ser classificada como entrada ou saída.
- **BR09**: Categorias arquivadas não devem estar disponíveis para novos lançamentos, mas devem permanecer associadas às movimentações históricas.
- **BR10**: Não deve ser permitido alterar o tipo de uma categoria que já esteja vinculada a movimentações financeiras.
- **BR11**: Uma categoria que possua movimentações associadas não deve ser excluída definitivamente, devendo ser arquivada para preservar o histórico financeiro.

## Movimentações

- **BR12**: O valor de uma movimentação deve ser sempre maior que zero. Sua natureza de entrada ou saída deve ser definida pelo tipo da movimentação, e não pelo sinal do valor.
- **BR13**: Uma movimentação deve utilizar uma categoria compatível com seu tipo: entradas devem utilizar categorias de entrada e saídas devem utilizar categorias de saída.
- **BR14**: A alteração ou exclusão de uma movimentação deve refletir automaticamente nos saldos das contas e nos indicadores financeiros relacionados.
- **BR15**: Movimentações registradas em datas anteriores à data de referência do saldo inicial de uma conta devem permanecer disponíveis no histórico, mesmo sem afetar o saldo atual.

## Transferências

- **BR16**: Uma transferência deve envolver duas contas distintas: uma conta de origem e uma conta de destino.
- **BR17**: O valor transferido deve ser debitado da conta de origem e creditado na conta de destino, sem alterar o patrimônio financeiro total do usuário.
- **BR18**: Uma transferência deve ser considerada uma operação única, garantindo que o débito na conta de origem e o crédito na conta de destino sejam registrados conjuntamente.
- **BR19**: A alteração ou exclusão de uma transferência deve refletir em ambas as contas envolvidas.
- **BR20**: Contas arquivadas não podem ser utilizadas como origem ou destino de novas transferências.

## Investimentos

- **BR21**: Todo aporte em investimento deve estar vinculado a uma conta de origem, da qual será debitado o valor aplicado.
- **BR22**: Todo resgate de investimento deve estar vinculado a uma conta de destino, na qual será creditado o valor informado pelo usuário.
- **BR23**: Aportes e resgates não devem ser contabilizados como receitas ou despesas nos indicadores financeiros.
- **BR24**: Todo investimento e suas respectivas operações devem estar vinculados ao usuário proprietário.
- **BR25**: A quantidade de ativos disponível em uma posição de renda variável não pode ser inferior a zero.
- **BR26**: A quantidade vendida ou o valor resgatado não pode ser superior à posição disponível no respectivo investimento.
- **BR27**: O valor informado em uma venda ou resgate deve ser creditado integralmente na conta de destino, considerando-o como o valor líquido recebido pelo usuário.
- **BR28**: O cadastro de posições de investimento existentes deve permitir informar os dados da posição e uma conta vinculada, sem gerar movimentações financeiras ou alterar o saldo dessa conta.
- **BR29**: Posições de investimento cadastradas anteriormente ao uso do sistema devem ser consideradas no patrimônio investido do usuário, mesmo sem possuir operações de aporte registradas no sistema.