# Diagrama de contexto (C4 nível 1)

```mermaid
C4Context
    title Diagrama de Contexto para o Sistema Financeiro
    Person(costumer, "Usuário", "Pessoa que utiliza o sistema para gerenciar suas próprias finanças")
    Enterprise_Boundary(b0, "Sistema Financeiro") {
        System(system, "Sistema Financeiro Pessoal", "Permite gerenciar contas, receitas, despesas, transferências e investimentos, oferecendo uma visão consolidada da situação financeira do usuário.")
    }
    System_Ext(system_ext, "Serviço de E-mail", "Serviço externo responsável pelo envio de e-mails de recuperação de senha.")
    Rel(costumer, system, "Utiliza o sistema")
    Rel(system, system_ext, "Solicita o envio do email com link de redefinição de senha")
    Rel(system_ext, costumer, "Envia email de recuperação de senha")
```