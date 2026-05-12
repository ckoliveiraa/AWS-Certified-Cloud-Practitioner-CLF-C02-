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

### 6. Qual serviço deve ser usado para armazenar senhas com rotação automática integrada ao RDS?

- A) S3
- B) Parameter Store
- C) Secrets Manager
- D) KMS

### 7. Qual serviço fornece relatórios de conformidade (SOC, ISO, PCI-DSS) para download?

- A) Artifact
- B) Config
- C) Audit Manager
- D) Security Hub

### 8. Sobre Security Groups, qual afirmação é correta?

- A) São stateless
- B) São stateful
- C) Aplicados a subnets
- D) Permitem regras de Deny

### 9. Qual serviço fornece certificados SSL/TLS gratuitos para ELB e CloudFront?

- A) KMS
- B) CloudHSM
- C) ACM
- D) IAM

### 10. Qual serviço é o dashboard central que agrega achados de GuardDuty, Inspector e Macie?

- A) Detective
- B) Security Hub
- C) CloudTrail
- D) Config

### 11. Uma empresa precisa de **FIPS 140-2 Level 3** e que a AWS não tenha acesso às chaves. Qual serviço?

- A) KMS
- B) CloudHSM
- C) Secrets Manager
- D) ACM

### 12. Qual serviço escaneia vulnerabilidades (CVEs) em instâncias EC2, imagens ECR e funções Lambda?

- A) GuardDuty
- B) Macie
- C) Inspector
- D) Detective

### 13. Após um alerta do GuardDuty, qual serviço ajuda a investigar a causa raiz com visualização em grafos?

- A) Security Hub
- B) CloudTrail
- C) Detective
- D) Config

### 14. Qual ataque é mitigado pelo AWS WAF (e não pelo Shield Standard)?

- A) UDP flood
- B) SYN flood
- C) SQL injection
- D) Ping flood

### 15. Um administrador liberou HTTPS de entrada em uma NACL, mas a aplicação não responde. Qual a causa mais provável?

- A) SG bloqueando saída
- B) Faltou liberar portas efêmeras na saída da NACL
- C) ACM expirado
- D) WAF bloqueando

### 16. Para que serve o IAM Identity Center?

- A) Criar policies JSON
- B) Login único (SSO) para múltiplas contas AWS e apps SaaS
- C) Detectar credenciais expostas
- D) Rotacionar chaves de acesso

### 17. Sobre o IAM, qual afirmação é verdadeira?

- A) É regional e tem custo mensal
- B) É global e gratuito
- C) É regional e gratuito
- D) É global e tem custo por usuário

### 18. Qual serviço armazena valores de configuração de forma **gratuita** (tier padrão), com suporte a SecureString via KMS?

- A) Secrets Manager
- B) Systems Manager Parameter Store
- C) CloudHSM
- D) Artifact

### 19. Quem é responsável pelos patches do engine MySQL em uma instância RDS?

- A) Cliente
- B) AWS
- C) Ambos
- D) Fornecedor do MySQL

### 20. Qual recurso do AWS Organizations permite agrupar contas (Dev, Prod, Finance) e aplicar SCPs em conjunto?

- A) IAM Groups
- B) OUs (Organizational Units)
- C) Resource Groups
- D) Tags

### 21. Qual serviço automatiza uma Landing Zone multi-conta com guardrails desde o início?

- A) AWS Organizations
- B) AWS Control Tower
- C) AWS Config
- D) AWS Firewall Manager

### 22. Para liberar **todos** os checks do Trusted Advisor, qual plano de Support é necessário?

- A) Basic
- B) Developer
- C) Business ou Enterprise
- D) Qualquer plano

### 23. Qual serviço responde melhor à pergunta "como esse Security Group estava configurado ontem às 14h?"

- A) CloudTrail
- B) CloudWatch
- C) AWS Config
- D) Trusted Advisor

### 24. Qual serviço gerencia WAF, Shield e Security Groups de forma centralizada em múltiplas contas via Organizations?

- A) Control Tower
- B) Firewall Manager
- C) Security Hub
- D) Network Firewall

### 25. Uma empresa precisa detectar PII em um banco RDS. Qual serviço deve usar?

- A) Macie
- B) GuardDuty
- C) Nenhum dos acima — Macie só funciona em S3
- D) Inspector

---

## Gabarito

| # | Resposta | Justificativa |
|---|----------|---------------|
| 1 | **B** | SO em EC2 (IaaS) é sempre do cliente. |
| 2 | **C** | Macie é especializado em PII no S3. |
| 3 | **B** | CloudTrail = audit log de chamadas de API. |
| 4 | **C** | SCPs são guardrails restritivos; nunca concedem. |
| 5 | **B** | Shield Standard é grátis e automático. |
| 6 | **C** | Secrets Manager tem rotação nativa integrada ao RDS. |
| 7 | **A** | Artifact é o portal de relatórios de conformidade. |
| 8 | **B** | SG é stateful; NACL é stateless. |
| 9 | **C** | ACM emite/renova certificados gratuitamente. |
| 10 | **B** | Security Hub é o dashboard central de segurança. |
| 11 | **B** | CloudHSM = FIPS 140-2 Level 3, single-tenant. |
| 12 | **C** | Inspector escaneia CVEs em EC2, ECR e Lambda. |
| 13 | **C** | Detective investiga causa raiz pós-alerta. |
| 14 | **C** | SQL injection é ataque L7 — WAF. Shield trata L3/L4. |
| 15 | **B** | NACL é stateless: precisa liberar portas efêmeras 1024-65535 na saída. |
| 16 | **B** | Identity Center = SSO multi-conta, integra AD/Okta/Azure AD. |
| 17 | **B** | IAM é global e gratuito. |
| 18 | **B** | Parameter Store é grátis no tier padrão e suporta SecureString. |
| 19 | **B** | RDS é PaaS — AWS cuida de SO e engine. |
| 20 | **B** | OUs agrupam contas para aplicação de SCPs. |
| 21 | **B** | Control Tower automatiza Landing Zone. |
| 22 | **C** | Apenas Business/Enterprise liberam todos os checks. |
| 23 | **C** | Config mantém linha do tempo das configurações. |
| 24 | **B** | Firewall Manager faz gestão centralizada via Organizations. |
| 25 | **C** | Macie funciona somente em S3 — não em RDS/DynamoDB/EBS. |

---

[← Voltar ao módulo](./README.md)
