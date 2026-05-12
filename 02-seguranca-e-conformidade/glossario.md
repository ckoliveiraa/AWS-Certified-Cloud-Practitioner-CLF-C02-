# Glossário — Módulo 2

## Responsabilidade Compartilhada

| Termo | Definição |
|-------|-----------|
| **Segurança DA nuvem** | Responsabilidade da AWS — hardware, hipervisor, rede global, data centers. |
| **Segurança NA nuvem** | Responsabilidade do cliente — dados, IAM, SO do guest, SG/NACL, criptografia. |
| **IaaS / PaaS / SaaS** | Modelos de serviço — patches do SO são do cliente em IaaS (EC2), da AWS em PaaS/SaaS (RDS, WorkMail). |

## Identidade e Acesso

| Termo | Definição |
|-------|-----------|
| **IAM** | Identity and Access Management — gerencia identidades e permissões. Global e gratuito. |
| **Usuário IAM** | Pessoa ou aplicação com credenciais permanentes. |
| **Grupo IAM** | Conjunto de usuários com permissões comuns. |
| **Role** | Identidade **temporária** assumida por usuários ou serviços (ex.: EC2 → S3). |
| **Policy** | Documento JSON com Effect, Action e Resource que define permissões. |
| **AWS Managed Policy** | Policy criada e mantida pela AWS. |
| **Customer Managed Policy** | Policy criada por você, reutilizável. |
| **Inline Policy** | Policy anexada a um único usuário/grupo/role. |
| **Root account** | Conta com acesso total — usar só para tarefas iniciais, com MFA. |
| **MFA** | Multi-Factor Authentication — algo que sabe + algo que tem (app, U2F, TOTP). |
| **Princípio do menor privilégio** | Conceder somente as permissões estritamente necessárias. |
| **IAM Access Analyzer** | Identifica recursos expostos externamente. |
| **IAM Identity Center** | Antigo AWS SSO — login único para múltiplas contas AWS e apps SaaS (integra AD, Okta, Azure AD). |

## Organizations e Governança

| Termo | Definição |
|-------|-----------|
| **AWS Organizations** | Gerencia múltiplas contas AWS centralizadamente. |
| **Management Account** | Conta-mãe (root) que controla a organização. |
| **OU** | Organizational Unit — agrupa contas (Dev, Prod, Finance). |
| **SCP** | Service Control Policy — guardrail que **restringe** (nunca concede) permissões em contas/OUs. |
| **Consolidated Billing** | Fatura única para várias contas, com descontos por volume agregados. |
| **AWS Control Tower** | Automatiza criação de **Landing Zone** multi-conta com guardrails preventivos e detectivos. |
| **Landing Zone** | Ambiente AWS multi-conta padronizado e seguro desde o início. |

## Criptografia

| Termo | Definição |
|-------|-----------|
| **KMS** | Key Management Service — chaves criptográficas multi-tenant, FIPS 140-2 Level 2. |
| **CMK / KMS Key** | Chave gerenciada pelo KMS. Tipos: AWS Managed, Customer Managed, AWS Owned. |
| **CloudHSM** | Hardware Security Module **dedicado** (single-tenant), FIPS 140-2 **Level 3** — AWS não tem acesso à chave. |
| **HSM** | Hardware Security Module — dispositivo físico para gerar/guardar chaves. |
| **FIPS 140-2** | Padrão NIST que valida módulos criptográficos. Level 2 (KMS) × Level 3 (CloudHSM, com resistência ativa). |
| **ACM** | AWS Certificate Manager — certificados SSL/TLS **gratuitos** com renovação automática (ELB, CloudFront, API Gateway). |
| **Secrets Manager** | Armazena segredos com **rotação automática** (ex.: senha do RDS); pago. |
| **Parameter Store** | (Systems Manager) Configs e segredos simples; gratuito no tier padrão; SecureString via KMS; sem rotação nativa. |
| **Criptografia em trânsito** | Dados protegidos na rede (TLS via ACM). |
| **Criptografia em repouso** | Dados protegidos no disco (KMS, SSE-KMS, SSE-S3). |

## Proteção de Rede

| Termo | Definição |
|-------|-----------|
| **WAF** | Web Application Firewall — protege contra ataques de **camada 7** (SQL injection, XSS) em CloudFront, ALB, API Gateway, AppSync. |
| **Shield Standard** | Proteção DDoS L3/L4 **gratuita e automática**. |
| **Shield Advanced** | USD 3.000/mês — proteção L7, DRT (DDoS Response Team), reembolso de custos de DDoS, WAF incluso. |
| **DDoS** | Distributed Denial of Service — ataque volumétrico (L3/L4) ou aplicacional (L7). |
| **Firewall Manager** | Gerencia WAF, Shield e SGs centralmente em várias contas via Organizations. |
| **Network Firewall** | Firewall **stateful** em VPC com inspeção profunda e regras Suricata. |
| **SG** | Security Group — firewall **stateful** de instância; só regras Allow. |
| **NACL** | Network ACL — firewall **stateless** de subnet; Allow + Deny; ordem numérica. |
| **Stateful** | "Lembra" da conexão — resposta sai automaticamente. |
| **Stateless** | Trata cada pacote isolado — precisa liberar portas efêmeras (1024-65535) na saída. |

## Detecção e Resposta

| Termo | Definição |
|-------|-----------|
| **GuardDuty** | Detecção de **ameaças em andamento** com ML sobre CloudTrail, VPC Flow Logs e DNS logs. |
| **Inspector** | Escaneamento de **vulnerabilidades** (CVEs) em EC2, imagens ECR e funções Lambda. |
| **Macie** | Descoberta de **PII/PHI** com ML — **apenas em S3**. |
| **Security Hub** | Dashboard central que agrega achados de GuardDuty, Inspector, Macie, Config; verifica CIS, PCI-DSS, AWS Foundational. |
| **Detective** | Investigação de **causa raiz** com grafos (pós-alerta do GuardDuty). |
| **Trusted Advisor** | Recomendações em 5 pilares (custo, performance, segurança, FT, limites). Basic/Developer = 6 checks; Business/Enterprise = todos. |

## Auditoria e Conformidade

| Termo | Definição |
|-------|-----------|
| **CloudTrail** | Registra **quem** chamou qual API (90 dias padrão; S3 para retenção longa). |
| **CloudWatch** | Métricas, logs de aplicação, alarms, dashboards. |
| **AWS Config** | Histórico de **configurações** dos recursos ao longo do tempo; regras de conformidade. |
| **Artifact** | Portal **gratuito** para baixar relatórios SOC, ISO, PCI-DSS. |
| **Audit Manager** | Automatiza coleta de **evidências** para auditorias (CIS, GDPR, HIPAA, PCI-DSS). |
| **PII** | Personally Identifiable Information — dados pessoais identificáveis. |
| **PHI** | Protected Health Information — dados de saúde sensíveis (HIPAA). |
| **CIS Benchmark** | Conjunto de melhores práticas de segurança do Center for Internet Security. |

---

[← Voltar ao módulo](./README.md)
