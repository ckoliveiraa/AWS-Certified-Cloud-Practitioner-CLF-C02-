# Simulado — Módulo 3 (Tecnologia e Serviços)

---

### 1. Qual serviço é serverless para executar código em resposta a eventos?
- A) EC2
- B) Lambda
- C) ECS
- D) Beanstalk

### 2. Qual classe S3 é mais econômica para arquivamento de longo prazo com recuperação em até 12h?
- A) Standard
- B) Glacier Instant Retrieval
- C) Glacier Deep Archive
- D) One Zone-IA

### 3. Uma empresa precisa de banco relacional compatível com PostgreSQL e 3x mais rápido. Qual?
- A) RDS PostgreSQL
- B) Aurora
- C) DynamoDB
- D) Redshift

### 4. Qual serviço fornece CDN global com cache HTTP/HTTPS?
- A) Route 53
- B) CloudFront
- C) Global Accelerator
- D) Direct Connect

### 5. Qual serviço é usado para data warehouse OLAP em escala de petabytes?
- A) DynamoDB
- B) RDS
- C) Redshift
- D) ElastiCache

### 6. Qual modelo de preço EC2 oferece maior desconto mas pode ser interrompido?
- A) On-Demand
- B) Reserved
- C) Spot
- D) Dedicated Host

### 7. Qual serviço orquestra workflows com lógica condicional e retries entre Lambdas?
- A) SQS
- B) SNS
- C) Step Functions
- D) EventBridge

### 8. Para migrar 100 PB offline, qual usar?
- A) Snowcone
- B) Snowball Edge
- C) Snowmobile
- D) DataSync

### 9. Qual serviço faz SQL diretamente sobre arquivos no S3, sem servidor?
- A) Redshift
- B) Athena
- C) Glue
- D) QuickSight

### 10. Qual serviço fornece infraestrutura AWS no data center do cliente?
- A) Direct Connect
- B) Outposts
- C) Storage Gateway
- D) Wavelength

### 11. Qual o limite de timeout de uma função Lambda?
- A) 5 minutos
- B) 15 minutos
- C) 1 hora
- D) Ilimitado

### 12. Sobre o S3, qual a durabilidade?
- A) 99,9%
- B) 99,99%
- C) 99,999999999% (11 noves)
- D) 100%

### 13. Qual serviço acessa S3 e DynamoDB a partir da VPC sem passar pela internet, gratuitamente?
- A) NAT Gateway
- B) Interface Endpoint
- C) Gateway Endpoint
- D) Transit Gateway

### 14. Para garantir alta disponibilidade do RDS com failover automático, deve-se usar:
- A) Read Replica
- B) Multi-AZ
- C) Backup automático
- D) Snapshot

### 15. Qual serviço orienta como reduzir custos identificando recursos super-dimensionados (EC2, EBS, Lambda)?
- A) Cost Explorer
- B) Trusted Advisor
- C) Compute Optimizer
- D) Budgets

### 16. Qual serviço gerencia containers sem você gerenciar servidores (nem EC2, nem cluster)?
- A) ECS no EC2
- B) EKS no EC2
- C) Fargate
- D) ECR

### 17. Qual a diferença entre ALB e NLB?
- A) ALB = TCP, NLB = HTTP
- B) ALB = camada 7 (HTTP/HTTPS), NLB = camada 4 (TCP/UDP)
- C) NLB faz cache, ALB não
- D) NLB é mais lento

### 18. Para garantir que as mensagens em uma fila SQS sejam processadas **em ordem e sem duplicação**, deve-se usar:
- A) SQS Standard
- B) SQS FIFO
- C) SNS
- D) EventBridge

### 19. Qual ferramenta permite criar infraestrutura como código usando TypeScript ou Python e gera CloudFormation por baixo?
- A) CloudFormation StackSets
- B) AWS CDK
- C) Terraform
- D) AWS SAM

### 20. Qual serviço permite acessar uma EC2 via shell sem precisar abrir a porta 22 nem usar chave SSH?
- A) EC2 Instance Connect
- B) Systems Manager Session Manager
- C) Direct Connect
- D) Bastion Host

### 21. Memória e disco de uma EC2 não aparecem no CloudWatch por padrão. Por quê?
- A) CloudWatch não suporta esses dados
- B) Precisa habilitar Detailed Monitoring
- C) Precisa instalar o CloudWatch Agent
- D) São métricas pagas

### 22. Qual serviço entrega streams automaticamente para S3, Redshift ou OpenSearch sem código?
- A) Kinesis Data Streams
- B) Kinesis Data Firehose
- C) MSK
- D) SQS

### 23. Qual o serviço para tracing distribuído em arquitetura de microsserviços?
- A) CloudWatch Logs
- B) X-Ray
- C) CloudTrail
- D) Inspector

### 24. Qual estratégia do CodeDeploy mantém o ambiente antigo enquanto o novo recebe tráfego, permitindo rollback rápido?
- A) In-place
- B) Blue/Green
- C) Linear
- D) All-at-once

### 25. Qual serviço da AWS oferece IA generativa via API com modelos como Claude, Llama e Titan?
- A) SageMaker
- B) Bedrock
- C) Comprehend
- D) Polly

### 26. Qual serviço extrai texto, tabelas e formulários de documentos PDF e imagens?
- A) Rekognition
- B) Comprehend
- C) Textract
- D) Transcribe

### 27. Para detectar mudanças manuais feitas no console em recursos criados por uma stack CloudFormation, usa-se:
- A) Drift Detection
- B) Change Set
- C) Rollback
- D) Stack Sets

### 28. Qual serviço fornece ETL serverless com catálogo de metadados e suporte a Spark?
- A) EMR
- B) Athena
- C) Glue
- D) DMS

### 29. Quando usar Amazon MQ em vez de SNS+SQS?
- A) Quando precisa de pub/sub puro
- B) Quando o sistema legado usa AMQP, MQTT ou STOMP
- C) Quando precisa de alta escalabilidade
- D) Quando é uma aplicação cloud-native nova

### 30. Qual a retenção máxima de uma mensagem no SQS?
- A) 1 dia
- B) 4 dias
- C) 14 dias
- D) 30 dias

### 31. Para conectar 20 VPCs entre si de forma centralizada, deve-se usar:
- A) VPC Peering
- B) Transit Gateway
- C) Direct Connect
- D) NAT Gateway

### 32. Qual serviço fornece terminal AWS pré-autenticado no navegador, gratuitamente?
- A) Cloud9
- B) CloudShell
- C) Session Manager
- D) AWS Toolkit

### 33. Qual serviço orquestra um pipeline de CI/CD na AWS?
- A) CodeBuild
- B) CodeDeploy
- C) CodePipeline
- D) CodeCommit

### 34. Qual o risco de armazenar dados em S3 One Zone-IA?
- A) Latência alta
- B) Custo elevado
- C) Se a AZ for destruída, o dado é perdido
- D) Falta de criptografia

### 35. Qual serviço fornece Kafka gerenciado pela AWS?
- A) Kinesis Data Streams
- B) MSK
- C) SQS
- D) Amazon MQ

---

## Gabarito

| # | Resposta | Justificativa |
|---|----------|---------------|
| 1 | **B** | Lambda é serverless orientado a eventos. |
| 2 | **C** | Glacier Deep Archive: armazenamento mais barato, 12-48h de recuperação. |
| 3 | **B** | Aurora = 3x PostgreSQL / 5x MySQL. |
| 4 | **B** | CloudFront é o CDN global HTTP/HTTPS. |
| 5 | **C** | Redshift é o data warehouse OLAP. |
| 6 | **C** | Spot até 90% off, com interrupção possível. |
| 7 | **C** | Step Functions orquestra workflows com lógica. |
| 8 | **C** | Snowmobile transporta até 100 PB. |
| 9 | **B** | Athena = SQL serverless no S3. |
| 10 | **B** | Outposts leva AWS para o DC do cliente. |
| 11 | **B** | Lambda tem timeout máximo de 15 minutos. |
| 12 | **C** | S3 = 11 noves de durabilidade. |
| 13 | **C** | Gateway Endpoint para S3 e DynamoDB, grátis. |
| 14 | **B** | Multi-AZ = standby síncrono com failover automático. |
| 15 | **C** | Compute Optimizer detecta over-provisioning (gratuito). |
| 16 | **C** | Fargate = serverless para containers (ECS/EKS). |
| 17 | **B** | ALB = L7 HTTP/HTTPS; NLB = L4 TCP/UDP com IP estático. |
| 18 | **B** | SQS FIFO garante ordem e exactly-once. |
| 19 | **B** | CDK = IaC em código que gera CloudFormation. |
| 20 | **B** | Session Manager elimina a necessidade de SSH/porta 22. |
| 21 | **C** | Memória/disco exigem o CloudWatch Agent instalado. |
| 22 | **B** | Kinesis Firehose entrega streams a destinos sem código. |
| 23 | **B** | X-Ray = tracing distribuído com mapa de serviços. |
| 24 | **B** | Blue/Green mantém ambiente paralelo para rollback rápido. |
| 25 | **B** | Bedrock = foundation models (Claude, Llama, Titan) via API. |
| 26 | **C** | Textract extrai texto + tabelas + formulários. |
| 27 | **A** | Drift Detection compara estado real vs template. |
| 28 | **C** | Glue = ETL serverless + Data Catalog + Spark. |
| 29 | **B** | MQ atende protocolos legados (AMQP, MQTT, STOMP). |
| 30 | **C** | SQS retém mensagens por até 14 dias. |
| 31 | **B** | Transit Gateway é hub central para muitas VPCs. |
| 32 | **B** | CloudShell é grátis, pré-autenticado, com CLI no navegador. |
| 33 | **C** | CodePipeline orquestra; Build/Deploy são etapas. |
| 34 | **C** | One Zone-IA tem dados em única AZ — sem redundância multi-AZ. |
| 35 | **B** | MSK = Managed Streaming for Apache Kafka. |

---

[← Voltar ao módulo](./README.md)
