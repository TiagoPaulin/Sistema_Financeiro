# Technology Stack

## 1. Introdução

Este documento apresenta as tecnologias e ferramentas escolhidas ou consideradas para o desenvolvimento do sistema de gestão financeira.

O objetivo é centralizar o stack tecnológico do projeto, registrando a finalidade de cada tecnologia e seu respectivo status de adoção.

As decisões arquiteturais e os motivos que justificam escolhas específicas são documentados separadamente nos Architecture Decision Records (ADRs).

### 1.1 Legenda de Status

| Status | Significado |
|---|---|
| Definido | Tecnologia ou ferramenta escolhida para fazer parte do projeto. |
| Em análise | Tecnologia considerada como uma possibilidade, mas cuja adoção ainda não foi decidida. |

## 2. Backend

| Tecnologia | Finalidade | Status |
|---|---|---|
| Java | Linguagem de programação do backend. | Definido |
| Spring Boot | Framework para desenvolvimento da aplicação backend e disponibilização da API REST. | Definido |
| Maven | Gerenciamento de dependências e automação do processo de build do projeto Java. | Definido |
| Spring Security | Gerenciamento de autenticação e autorização. | Definido |
| Spring Data JPA | Abstração e gerenciamento da persistência de dados por meio de repositórios. | Definido |
| Hibernate | Implementação ORM para mapeamento entre objetos Java e banco de dados relacional. | Definido |
| Spring Modulith | Suporte à organização, validação e documentação das fronteiras entre módulos do monólito modular. | Definido |

## 3. Frontend

| Tecnologia | Finalidade | Status |
|---|---|---|
| React | Biblioteca para construção da interface de usuário. | Em análise |
| JavaScript ou TypeScript | Linguagem de programação do frontend. | Em análise |

A escolha definitiva do framework e das tecnologias do frontend será realizada durante a etapa de desenvolvimento, considerando os requisitos do sistema e os objetivos de aprendizado.

## 4. Banco de Dados e Persistência

| Tecnologia | Finalidade | Status |
|---|---|---|
| PostgreSQL | Sistema gerenciador de banco de dados relacional utilizado para persistência dos dados. | Definido |
| Flyway | Gerenciamento e versionamento das migrações do schema do banco de dados. | Definido |

## 5. Segurança

| Tecnologia | Finalidade | Status |
|---|---|---|
| JWT | Utilizado para representar tokens de autenticação e controlar o acesso à API. | Definido |
| BCrypt | Algoritmo de hash para armazenamento seguro de senhas. | Definido |
| HTTPS | Proteção da comunicação entre cliente e servidor em ambientes de hospedagem. | Definido |

## 6. Testes

| Tecnologia | Finalidade | Status |
|---|---|---|
| JUnit | Framework para execução de testes automatizados no backend. | Definido |
| Mockito | Criação de objetos simulados para testes unitários. | Definido |
| Testcontainers | Execução de testes de integração utilizando containers com dependências reais, como PostgreSQL. | Definido |

## 7. Documentação da API

| Tecnologia | Finalidade | Status |
|---|---|---|
| OpenAPI | Especificação da documentação e dos contratos da API REST. | Definido |
| Swagger UI | Interface visual para consultar e testar os endpoints documentados. | Definido |

## 8. Containers e Infraestrutura

| Tecnologia | Finalidade | Status |
|---|---|---|
| Docker | Containerização dos serviços da aplicação. | Definido |
| Docker Compose | Orquestração dos containers do frontend, backend e banco de dados no ambiente local. | Definido |

Inicialmente, a aplicação será executada localmente, utilizando containers Docker para padronizar o ambiente de desenvolvimento.

A definição de uma plataforma de hospedagem e implantação em ambiente externo será realizada posteriormente.

## 9. CI/CD, Versionamento e Fluxo de Desenvolvimento

| Tecnologia ou Prática | Finalidade | Status |
|---|---|---|
| Git | Controle de versão do código-fonte e da documentação. | Definido |
| GitHub | Hospedagem do repositório e colaboração no desenvolvimento. | Definido |
| GitHub Actions | Automação de pipelines para build, execução de testes e verificações de qualidade. | Definido |
| GitHub Flow | Estratégia de branching baseada em branches curtas por funcionalidade, integradas à main por Pull Requests. | Definido |

Inicialmente, os pipelines serão voltados à integração contínua (CI). A implantação automatizada (CD) será considerada quando o projeto possuir um ambiente de hospedagem.

O fluxo de desenvolvimento utilizará branches independentes para funcionalidades, correções e outras alterações, integradas à branch principal (`main`) por meio de Pull Requests.

## 10. Hospedagem e Implantação

A implantação inicial será realizada exclusivamente em ambiente local.

A escolha de um provedor de hospedagem e a definição da estratégia de deploy serão avaliadas futuramente, conforme a evolução do projeto e a necessidade de disponibilizá-lo externamente.