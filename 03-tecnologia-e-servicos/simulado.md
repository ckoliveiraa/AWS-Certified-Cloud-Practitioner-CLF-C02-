# Simulado — Módulo 3 (Tecnologia e Serviços)

---

### 1. Qual serviço é serverless para executar código sob eventos?
- A) EC2
- B) Lambda
- C) ECS
- D) Beanstalk

### 2. Qual classe S3 é mais econômica para dados raramente acessados com recuperação em 12h?
- A) Standard
- B) Glacier Instant Retrieval
- C) Glacier Deep Archive
- D) One Zone-IA

### 3. Um cliente precisa banco relacional compatível com PostgreSQL e 3x mais rápido. Qual?
- A) RDS PostgreSQL
- B) Aurora
- C) DynamoDB
- D) Redshift

### 4. Qual serviço fornece CDN global?
- A) Route 53
- B) CloudFront
- C) Global Accelerator
- D) Direct Connect

### 5. Qual serviço é usado para data warehouse?
- A) DynamoDB
- B) RDS
- C) Redshift
- D) ElastiCache

### 6. Qual modelo de preço EC2 oferece maior desconto mas pode ser interrompido?
- A) On-Demand
- B) Reserved
- C) Spot
- D) Dedicated Host

### 7. Qual serviço orquestra workflows entre Lambda e outros serviços?
- A) SQS
- B) SNS
- C) Step Functions
- D) EventBridge

### 8. Para migrar 100 PB offline, qual usar?
- A) Snowcone
- B) Snowball
- C) Snowmobile
- D) DataSync

### 9. Qual serviço faz SQL diretamente em arquivos no S3?
- A) Redshift
- B) Athena
- C) Glue
- D) QuickSight

### 10. Qual fornece infra AWS no data center do cliente?
- A) Direct Connect
- B) Outposts
- C) Storage Gateway
- D) Wavelength

---

## Gabarito

| # | Resposta | Justificativa |
|---|----------|---------------|
| 1 | **B** | Lambda é serverless orientado a eventos. |
| 2 | **C** | Deep Archive = mais barato, 12h de recuperação. |
| 3 | **B** | Aurora é 3x PostgreSQL / 5x MySQL. |
| 4 | **B** | CloudFront é o CDN global. |
| 5 | **C** | Redshift é o DW da AWS. |
| 6 | **C** | Spot até 90% off. |
| 7 | **C** | Step Functions orquestra. |
| 8 | **C** | Snowmobile = 100 PB. |
| 9 | **B** | Athena = SQL serverless no S3. |
| 10 | **B** | Outposts leva AWS para o DC do cliente. |

---

[← Voltar ao módulo](./README.md)
