# Simulado — Módulo 2 (Segurança e Conformidade)

---

### 1. Segundo o Modelo de Responsabilidade Compartilhada, quem é responsável por aplicar patches no SO de uma instância EC2?

- A) AWS
- B) Cliente
- C) Ambos
- D) Fornecedor do SO

### 2. Qual serviço detecta dados sensíveis (PII) em buckets S3?

- A) GuardDuty
- B) Inspector
- C) Macie
- D) Detective

### 3. Qual serviço registra chamadas de API na conta AWS?

- A) CloudWatch
- B) CloudTrail
- C) Config
- D) Trusted Advisor

### 4. O que é uma SCP no AWS Organizations?

- A) Concede permissões a usuários
- B) Gerencia faturamento
- C) Limita o que contas-filho podem fazer
- D) Cria novas contas

### 5. Qual plano AWS Shield é gratuito e ativado automaticamente?

- A) Shield Basic
- B) Shield Standard
- C) Shield Advanced
- D) Shield Premium

### 6. Qual serviço deve ser usado para armazenar senhas com rotação automática?

- A) S3
- B) Parameter Store
- C) Secrets Manager
- D) KMS

### 7. Qual serviço fornece relatórios de conformidade (SOC, ISO)?

- A) Artifact
- B) Config
- C) Audit Manager
- D) Security Hub

### 8. Security Groups são:

- A) Stateless
- B) Stateful
- C) Aplicados a subnets
- D) Permitem regras de Deny

### 9. Qual serviço fornece certificados SSL gratuitos para ELB e CloudFront?

- A) KMS
- B) CloudHSM
- C) ACM
- D) IAM

### 10. Qual serviço é o dashboard central que agrega achados de GuardDuty, Inspector e Macie?

- A) Detective
- B) Security Hub
- C) CloudTrail
- D) Config

---

## Gabarito

| # | Resposta | Justificativa |
|---|----------|---------------|
| 1 | **B** | SO em EC2 é sempre do cliente. |
| 2 | **C** | Macie é especializado em PII no S3. |
| 3 | **B** | CloudTrail = API audit log. |
| 4 | **C** | SCPs são guardrails restritivos. |
| 5 | **B** | Shield Standard é grátis e automático. |
| 6 | **C** | Secrets Manager tem rotação nativa. |
| 7 | **A** | Artifact é o portal de relatórios. |
| 8 | **B** | SG é stateful; NACL é stateless. |
| 9 | **C** | ACM fornece certificados gratuitos. |
| 10 | **B** | Security Hub é o dashboard central. |

---

[← Voltar ao módulo](./README.md)
