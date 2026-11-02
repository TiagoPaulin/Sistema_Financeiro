# Elicitação de Requisitos do Projeto

Este documento registra os requisitos não funcionais que definem as características de qualidade e as restrições que o sistema deve atender.

## Requisitos Não Funcionais

### Segurança

- **RNF01**: O sistema deve armazenar as senhas dos usuários utilizando algoritmos de hash próprios para senhas, com proteção contra recuperação direta das senhas originais, utilizando BCrypt.
- **RNF02**: O sistema deve impedir o acesso de usuários não autenticados aos recursos protegidos, permitindo acesso público apenas às funcionalidades de cadastro, login e recuperação de senha.
- **RNF03**: O sistema deve gerar tokens de acesso JWT com validade de 15 minutos após a autenticação do usuário.
- **RNF04**: O sistema deve utilizar refresh tokens com validade de 7 dias para permitir a renovação dos tokens de acesso, mantendo seu controle e possibilitando sua invalidação.
- **RNF05**: O sistema deve garantir que cada usuário tenha acesso exclusivamente aos seus próprios dados, impedindo consultas, alterações ou exclusões de informações pertencentes a outros usuários.
- **RNF06**: O sistema deve limitar tentativas consecutivas de autenticação malsucedidas, aplicando mecanismos de proteção contra ataques de força bruta.
- **RNF07**: O sistema deve retornar mensagens genéricas em falhas de autenticação, evitando revelar se o email informado está cadastrado na plataforma.
- **RNF08**: O sistema deve evitar revelar, por meio das respostas da API, se um endereço de email já está cadastrado durante o processo de registro.
- **RNF09**: O sistema deve validar os dados recebidos nas requisições, verificando formatos, tipos, tamanhos e valores permitidos, além de implementar mecanismos de proteção contra ataques de injeção de código e comandos.
- **RNF10**: O sistema não deve expor informações sensíveis dos usuários, como senhas, hashes de senhas, tokens de autenticação e tokens de recuperação de senha, em respostas da API ou registros de logs.
- **RNF11**: O sistema deve utilizar HTTPS para proteger a comunicação entre cliente e servidor, garantindo a confidencialidade e integridade dos dados transmitidos.


### Confiabilidade

- **RNF12**: O sistema deve utilizar representações numéricas de precisão exata para armazenar e realizar cálculos financeiros, evitando tipos de ponto flutuante que possam introduzir erros de precisão.
- **RNF13**: O sistema deve garantir a atomicidade das operações financeiras que envolvam múltiplos registros, assegurando que todas as alterações sejam persistidas ou que nenhuma delas seja efetivada em caso de falha.
- **RNF14**: O sistema deve possuir mecanismos de backup e recuperação dos dados persistidos, permitindo restaurar as informações em caso de falhas ou perda de dados.
- **RNF15**: O sistema deve fornecer respostas de erro padronizadas, apresentando informações compreensíveis ao cliente sem expor detalhes internos da aplicação ou infraestrutura.

### Manutenibilidade

- **RNF16**: O sistema deve manter o esquema do banco de dados versionado por meio de migrações, permitindo rastrear e reproduzir alterações na estrutura do banco.
- **RNF17**: O sistema deve disponibilizar a documentação dos contratos da API, descrevendo endpoints, parâmetros, formatos de requisição, respostas e possíveis erros, utilizando o padrão OpenAPI.

### Privacidade

- **RNF18**: O sistema deve proteger os dados pessoais dos usuários, permitindo que sejam tratados e armazenados somente para finalidades relacionadas às funcionalidades oferecidas, respeitando os princípios e requisitos aplicáveis da LGPD.