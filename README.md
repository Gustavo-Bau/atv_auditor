A organização das pastas e classes foi definida com base na Arquitetura Hexagonal, buscando separar a regra de negócio da parte técnica da aplicação. O principal objetivo foi deixar o sistema mais organizado, desacoplado e fácil de manter.

A camada domain concentra as entidades, regras e contratos principais do sistema. Nela ficam apenas as responsabilidades relacionadas ao negócio, sem dependência de frameworks, banco de dados ou mensageria. Isso permite testar a lógica da aplicação de forma simples e independente.

A camada application foi criada para conter os casos de uso da aplicação. Ela coordena o fluxo do processamento, como receber a mensagem da DLQ, calcular a severidade e encaminhar os dados para persistência. Dessa forma, a regra de negócio fica centralizada e bem definida.

Além da organização, essa estrutura melhora a legibilidade do projeto, reduz acoplamento entre componentes e evita que uma única classe fique responsável por várias funções diferentes. Com isso, o sistema se torna mais escalável, reutilizável e fácil de evoluir futuramente.

src/main/java/br/com/atvarquitetura/dlqauditor
├── application
│   └── AuditDlqMessageService.java      # caso de uso
├── domain
│   ├── model                            # entidades/records de domínio
│   └── port
│       ├── in                           # entrada do caso de uso
│       └── out                          # saída para persistência
├── infrastructure
│   ├── sqs                              # adapter de entrada (consumer DLQ)
│   └── persistence                      # adapter de saída (JPA)
└── DlqAuditorApplication.java
