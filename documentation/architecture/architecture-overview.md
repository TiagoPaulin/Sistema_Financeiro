# Visão Geral da Arquitetura

## 1. Introdução

Este documento apresenta a arquitetura geral do sistema, descrevendo sua organização, seus principais componentes, a comunicação entre eles e as decisões arquiteturais que orientarão o desenvolvimento.

O sistema será desenvolvido como uma aplicação de gerenciamento financeiro pessoal, permitindo o controle de contas, movimentações financeiras, transferências e investimentos.

A arquitetura deverá priorizar a organização do código, a separação de responsabilidades, a facilidade de manutenção e a possibilidade de evolução do sistema, evitando complexidade desnecessária para o escopo inicial do projeto.

## 2. Estilo Arquitetural

O backend adotará uma arquitetura de **Monólito Modular (Modular Monolith)**, com organização interna em camadas.

### 2.1. Monólito Modular

O backend será desenvolvido como uma única aplicação, executada e implantada de maneira independente, mas organizada internamente em módulos que representam diferentes áreas funcionais do sistema.

Cada módulo será responsável por suas próprias funcionalidades e regras de negócio, mantendo suas implementações internas encapsuladas.

Inicialmente, serão considerados os seguintes módulos:

- Usuários;
- Contas;
- Categorias;
- Movimentações;
- Transferências;
- Investimentos.

Essa organização permitirá separar as responsabilidades do sistema sem a necessidade de criar aplicações ou serviços independentes, como aconteceria em uma arquitetura de microsserviços.

### 2.2. Arquitetura em Camadas

Cada módulo poderá ser organizado internamente em camadas, separando as responsabilidades relacionadas à exposição de funcionalidades, execução das regras de negócio e acesso aos dados.

As principais camadas serão:

- **Controller:** responsável por receber as requisições HTTP e direcioná-las aos serviços correspondentes.
- **Service:** responsável pela execução dos casos de uso e das regras de negócio.
- **Repository:** responsável pelo acesso e pela persistência dos dados.
- **Entity:** responsável pela representação das entidades persistidas no banco de dados.
- **DTO:** responsável pela transferência de dados entre as diferentes partes da aplicação.

Essa separação busca evitar que responsabilidades distintas fiquem concentradas em uma única classe, facilitando a manutenção e os testes.

## 3. Visão Geral do Sistema

O sistema será dividido em duas aplicações principais:

### 3.1. Backend

O backend será responsável pela implementação das regras de negócio, autenticação, autorização, validações e persistência dos dados.

Será desenvolvido em Java com Spring Boot, expondo uma API REST para permitir a comunicação com o frontend.

### 3.2. Frontend

O frontend será responsável pela interface com o usuário, permitindo visualizar informações financeiras e realizar operações por meio das funcionalidades disponibilizadas pelo backend.

A tecnologia utilizada no frontend ainda será definida posteriormente.

## 4. Organização do Backend

O backend será organizado por módulos funcionais, mantendo dentro de cada módulo suas respectivas camadas e responsabilidades.

Cada módulo deverá possuir autonomia sobre suas regras de negócio e sua implementação interna, evitando dependências desnecessárias entre diferentes partes do sistema.

### 4.1. Comunicação entre Módulos

A comunicação entre os módulos será realizada por meio de **APIs públicas internas (Public APIs)**, que funcionarão como contratos de comunicação entre eles.

Cada módulo poderá disponibilizar, por meio de um pacote `api/`, as interfaces ou classes responsáveis por expor as funcionalidades que outros módulos precisam utilizar.

Os demais módulos deverão depender exclusivamente desses contratos públicos, sem acessar diretamente componentes internos de outros módulos, como repositories, entidades JPA ou classes de implementação dos serviços.

Por exemplo, caso o módulo de movimentações precise realizar um débito ou crédito em uma conta, ele deverá utilizar uma funcionalidade disponibilizada pela API pública do módulo de contas, em vez de acessar diretamente seu repository ou manipular suas entidades.

Essa abordagem permitirá que cada módulo mantenha o controle sobre sua própria implementação, expondo somente as operações necessárias para os demais módulos.

### 4.2. Redução do Acoplamento

A utilização de contratos públicos busca reduzir o acoplamento entre os módulos por meio de alguns princípios:

- **Encapsulamento:** os detalhes internos de implementação de cada módulo permanecem ocultos para os demais.
- **Dependência de contratos:** os módulos consumidores dependem das funcionalidades disponibilizadas pelas APIs públicas, e não de classes concretas ou estruturas internas.
- **Flexibilidade de implementação:** alterações internas em um módulo poderão ser realizadas sem exigir mudanças nos módulos consumidores, desde que seus contratos públicos sejam preservados.
- **Controle de dependências:** o acesso às funcionalidades de outros módulos deverá ocorrer por pontos de comunicação definidos, evitando dependências diretas e desnecessárias.

Dessa forma, as mudanças internas de um módulo terão menor probabilidade de impactar outras partes do sistema.

É importante destacar que a existência de um pacote `api/` não garante, por si só, o baixo acoplamento. Essa separação dependerá do respeito aos contratos estabelecidos e da restrição de acesso às implementações internas dos módulos.

### 4.3. Exemplo de Organização

Uma estrutura inicial poderá seguir o seguinte modelo:

```text
modules/
├── account/
│   ├── api/
│   ├── controller/
│   ├── service/
│   ├── repository/
│   ├── entity/
│   └── dto/
│
├── transaction/
│   ├── api/
│   ├── controller/
│   ├── service/
│   ├── repository/
│   ├── entity/
│   └── dto/
│
├── transfer/
├── category/
├── investment/
└── user/
```

O exemplo representa uma possível organização, que poderá ser ajustada conforme as necessidades de cada módulo. Nem todos precisarão necessariamente possuir todas as camadas ou pacotes.

## 5. Organização do Repositório

O projeto será desenvolvido em um único repositório Git, seguindo a abordagem de **Monorepo**.

A estrutura inicial será organizada da seguinte maneira:

```text
project/
├── backend/
├── frontend/
└── documentation/
```

- **backend/**: código-fonte da API REST e implementação das regras de negócio.
- **frontend/**: código-fonte da aplicação de interface com o usuário.
- **documentation/**: documentação do projeto, incluindo requisitos, arquitetura, diagramas e decisões arquiteturais.

Essa organização permitirá manter os componentes do sistema centralizados em um único repositório, facilitando seu versionamento e gerenciamento.

## 6. Comunicação e Fluxo de Dados

A comunicação entre frontend e backend ocorrerá por meio de requisições HTTP, utilizando os endpoints disponibilizados pela API REST.

De maneira geral, o fluxo de uma requisição seguirá as seguintes etapas:

1. O frontend envia uma requisição HTTP para um endpoint do backend.
2. O Controller recebe a requisição e realiza as validações de entrada necessárias.
3. O Service executa o caso de uso e aplica as regras de negócio.
4. Quando necessário, o Service utiliza os Repositories para consultar ou persistir dados.
5. O resultado é retornado ao Controller, que disponibiliza a resposta HTTP ao frontend.

Quando um caso de uso precisar utilizar funcionalidades de outro módulo, a comunicação deverá ocorrer por meio de sua API pública interna, respeitando os limites de responsabilidade de cada módulo.

## 7. Segurança

A segurança será tratada como uma responsabilidade compartilhada entre frontend e backend, considerando as particularidades e responsabilidades de cada camada.

O frontend será responsável por implementar validações iniciais e mecanismos de proteção na interface, contribuindo para uma experiência de uso segura e reduzindo o envio de dados inválidos.

O backend será responsável por aplicar as validações definitivas, autenticar e autorizar as requisições, proteger os dados e garantir que as regras de segurança sejam respeitadas independentemente da origem das requisições.

Serão considerados mecanismos como:

- **Autenticação e autorização:** utilização de JWT e controle de acesso aos endpoints, com validação das permissões no backend.
- **Proteção de credenciais:** armazenamento seguro de senhas utilizando BCrypt.
- **Validação de entradas:** validações no frontend para oferecer feedback imediato ao usuário e no backend para garantir a integridade e segurança dos dados recebidos.
- **Proteção contra ataques:** adoção de medidas para prevenir vulnerabilidades como SQL Injection, Cross-Site Scripting (XSS) e outras ameaças pertinentes a cada camada.
- **Proteção dos dados:** garantia de que cada usuário tenha acesso somente às informações de sua propriedade.
- **Tratamento de erros:** tratamento seguro de exceções, evitando a exposição de informações sensíveis ou detalhes internos da aplicação.

## 8. Persistência e Integridade dos Dados

O sistema utilizará um banco de dados relacional para armazenar as informações dos usuários, contas, movimentações, transferências e investimentos.

A camada de persistência será implementada por meio dos Repositories, responsáveis pela comunicação entre a aplicação e o banco de dados.

As operações que envolverem múltiplas alterações relacionadas deverão preservar a integridade dos dados, utilizando transações quando necessário.

A comunicação entre módulos não deverá comprometer a consistência das operações. Quando um caso de uso envolver mais de um módulo, sua execução deverá respeitar a atomicidade necessária, mantendo as operações relacionadas dentro de uma mesma transação quando aplicável.

## 9. Diagramas Arquiteturais

A documentação arquitetural poderá incluir os seguintes diagramas para representar diferentes perspectivas do sistema:

- **C4 - Contexto:** apresenta o sistema e sua interação com usuários e sistemas externos.
- **C4 - Containers:** apresenta os principais componentes executáveis, como frontend, backend e banco de dados.
- **C4 - Componentes:** detalha a organização interna dos principais componentes do backend.
- **Diagrama Entidade-Relacionamento (DER):** representa a estrutura do banco de dados e seus relacionamentos.
- **Diagramas de sequência:** representam os fluxos de execução e a interação entre os componentes em casos de uso específicos.

## 10. Decisões Arquiteturais

As decisões relevantes para a arquitetura serão documentadas individualmente por meio de Architecture Decision Records (ADRs).

- [ADR-001](./decisions/ADR-001.md): Adoção de Monólito Modular
- [ADR-002](./decisions/ADR-002.md): Organização Interna em Camadas
- [ADR-003](./decisions/ADR-003.md): Comunicação entre Módulos por meio de APIs Públicas Internas
- [ADR-004](./decisions/ADR-004.md): Adoção de Monorepo
- [ADR-005](./decisions/ADR-005.md): Adoção de API REST para Comunicação entre Frontend e Backend
- [ADR-006](./decisions/ADR-006.md): Adoção do PostgreSQL
- [ADR-007](./decisions/ADR-007.md): Adoção do Flyway para Gerenciamento de Migrações do Banco de Dados
- [ADR-008](./decisions/ADR-008.md): Adoção do Docker para Containerização da Aplicação
- [ADR-009](./decisions/ADR-009.md): Adoção do Spring Modulith