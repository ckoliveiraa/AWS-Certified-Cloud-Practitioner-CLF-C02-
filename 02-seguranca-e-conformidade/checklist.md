# Checklist de Revisão — Módulo 2

## 2.1 Responsabilidade Compartilhada
- [ ] Distingo segurança **DA** nuvem (AWS) vs. **NA** nuvem (cliente)
- [ ] Sei quem patcha SO: **EC2 = cliente**, **RDS/Lambda = AWS**
- [ ] IAM e criptografia dos dados **sempre** são do cliente
- [ ] Hardware, hipervisor e data center físico são da AWS
- [ ] Sei classificar IaaS, PaaS, SaaS quanto à responsabilidade

## 2.2 IAM
- [ ] Diferencio Usuário, Grupo, Role e Policy
- [ ] Sei que IAM é **gratuito e global** (sem região)
- [ ] Leio policy JSON (Effect, Action, Resource)
- [ ] AWS Managed vs Customer Managed vs Inline policy
- [ ] Boas práticas: root só inicial + **MFA no root**, menor privilégio, grupos > usuários
- [ ] Uso **Roles** para serviços (EC2 → S3), nunca chaves no código
- [ ] **IAM Identity Center** = SSO multi-conta + AD/Okta/Azure AD
- [ ] **IAM Access Analyzer** detecta recursos expostos
- [ ] Tipos de MFA: virtual, U2F, hardware TOTP

## 2.3 Organizations & Control Tower
- [ ] Consolidated Billing + descontos por volume
- [ ] **SCPs restringem, nunca concedem** permissão
- [ ] OUs agrupam contas (Dev, Prod, Finance)
- [ ] Conta pode estar em **apenas uma** organização
- [ ] **Control Tower** = Landing Zone automatizada (Orgs + SSO + Config + CloudTrail)

## 2.4 Criptografia
- [ ] **KMS**: multi-tenant, FIPS **Level 2**, integrado a serviços AWS
- [ ] **CloudHSM**: dedicado, FIPS **Level 3**, AWS não tem acesso à chave
- [ ] Gatilho exame: **"FIPS 140-2 Level 3" → CloudHSM**
- [ ] Tipos de KMS Key: AWS Managed, Customer Managed, AWS Owned
- [ ] **ACM** = certificados SSL/TLS **grátis** (ELB, CloudFront, API Gateway)
- [ ] ACM **não exporta chave privada** (não serve para servidor fora da AWS)
- [ ] **Secrets Manager**: pago, rotação automática (integra RDS)
- [ ] **Parameter Store**: grátis, SecureString via KMS, **sem rotação nativa**
- [ ] Em trânsito = TLS (ACM); em repouso = KMS/SSE

## 2.5 Proteção de Rede
- [ ] Camadas: **L3/L4 = Shield**, **L7 = WAF**
- [ ] WAF protege: CloudFront, ALB, API Gateway, AppSync
- [ ] **Shield Standard** = grátis e automático (L3/L4)
- [ ] **Shield Advanced** = USD 3.000/mês, inclui WAF + DRT + reembolso DDoS
- [ ] **Firewall Manager** = gestão centralizada via Organizations
- [ ] **Network Firewall** = stateful em VPC, regras Suricata
- [ ] **SG = stateful** (instância, só Allow)
- [ ] **NACL = stateless** (subnet, Allow+Deny, ordem numérica)
- [ ] Pegadinha NACL: liberar **portas efêmeras (1024-65535) na saída**

## 2.6 Detecção e Resposta
- [ ] **GuardDuty** = ameaças em andamento (ML sobre CloudTrail/VPC Flow/DNS)
- [ ] **Inspector** = vulnerabilidades/CVE em EC2, ECR, Lambda
- [ ] **Macie** = PII/PHI **apenas no S3** (não RDS, não DynamoDB)
- [ ] **Security Hub** = dashboard central (CIS, PCI-DSS, Foundational)
- [ ] **Detective** = investigação de causa raiz (pós-alerta)
- [ ] **Trusted Advisor**: Basic/Developer = 6 checks; **Business/Enterprise = todos**
- [ ] Fluxo: GuardDuty → Security Hub → Detective

## 2.7 Auditoria e Conformidade
- [ ] **CloudTrail** = **quem** chamou a API (90 dias padrão, S3 para retenção)
- [ ] **CloudWatch** = métricas, logs de aplicação, alarms, dashboards
- [ ] **Config** = **o que mudou** na configuração (linha do tempo)
- [ ] CloudTrail responde "quem"; Config responde "o que/como estava"
- [ ] **Artifact** = baixar relatórios SOC, ISO, PCI (gratuito)
- [ ] **Audit Manager** = automatiza coleta de evidências (CIS, GDPR, HIPAA, PCI)

## Prática
- [ ] Simulado ≥ 80%
- [ ] Flashcards revisados
- [ ] Glossário dominado
- [ ] Laboratórios/homework concluídos

---

[← Voltar ao módulo](./README.md)
