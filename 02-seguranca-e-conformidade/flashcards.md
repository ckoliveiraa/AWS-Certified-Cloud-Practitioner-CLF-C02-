# Flashcards — Módulo 2

---

**1. Quem é responsável pelos patches do SO em uma instância EC2?**
<details><summary>Ver resposta</summary>
O **cliente**. Em IaaS, SO do guest é responsabilidade do cliente.
</details>

---

**2. Quem é responsável pelos patches do engine MySQL em RDS?**
<details><summary>Ver resposta</summary>
A **AWS**. RDS é serviço gerenciado (PaaS) — AWS cuida de SO e engine.
</details>

---

**3. Qual serviço detecta ameaças por ML usando CloudTrail, VPC Flow Logs e DNS logs?**
<details><summary>Ver resposta</summary>
**Amazon GuardDuty** — sem agentes, ativação com 1 clique.
</details>

---

**4. Qual serviço identifica dados sensíveis (PII/PHI) e funciona APENAS no S3?**
<details><summary>Ver resposta</summary>
**Amazon Macie**. Não escaneia RDS, DynamoDB, EBS ou Redshift.
</details>

---

**5. Diferença entre CloudTrail, CloudWatch e Config?**
<details><summary>Ver resposta</summary>
- **CloudTrail**: **quem** chamou qual API.
- **CloudWatch**: métricas, logs de aplicação, alarmes.
- **Config**: **o que mudou** na configuração de um recurso (linha do tempo).
</details>

---

**6. O que é uma SCP e o que ela pode fazer?**
<details><summary>Ver resposta</summary>
Service Control Policy — guardrail em Organizations que **limita** o que contas/OUs podem fazer. **Nunca concede** permissões, apenas restringe.
</details>

---

**7. Quando usar CloudHSM em vez de KMS?**
<details><summary>Ver resposta</summary>
Quando exigir **FIPS 140-2 Level 3**, single-tenant, ou quando a AWS **não pode ter acesso** às chaves (compliance bancário/governamental). KMS é Level 2 e multi-tenant.
</details>

---

**8. Qual serviço fornece certificados SSL/TLS gratuitos para ELB, CloudFront e API Gateway?**
<details><summary>Ver resposta</summary>
**AWS Certificate Manager (ACM)** — renovação automática. Não exporta chave privada para servidores fora da AWS.
</details>

---

**9. Onde baixar relatórios SOC 2, ISO e PCI-DSS da AWS?**
<details><summary>Ver resposta</summary>
**AWS Artifact** (gratuito, autoatendimento).
</details>

---

**10. Security Group é stateful ou stateless? E NACL?**
<details><summary>Ver resposta</summary>
- **SG = stateful** (nível de instância, só Allow, lembra da conexão).
- **NACL = stateless** (nível de subnet, Allow + Deny, ordem numérica, precisa liberar portas efêmeras na saída).
</details>

---

**11. WAF protege contra qual tipo de ataque e em quais serviços?**
<details><summary>Ver resposta</summary>
Ataques de **camada 7** (SQL injection, XSS, bots). Funciona em **CloudFront, ALB, API Gateway, AppSync**.
</details>

---

**12. Diferença entre Shield Standard e Shield Advanced?**
<details><summary>Ver resposta</summary>
- **Standard**: grátis, automático, proteção DDoS L3/L4.
- **Advanced**: USD 3.000/mês, L7, DDoS Response Team (DRT), reembolso de custos DDoS, WAF incluso.
</details>

---

**13. Qual serviço investiga a causa raiz APÓS um alerta do GuardDuty?**
<details><summary>Ver resposta</summary>
**Amazon Detective** — visualiza relações entre entidades, não detecta (investiga).
</details>

---

**14. Qual serviço escaneia CVEs em EC2, imagens ECR e Lambda?**
<details><summary>Ver resposta</summary>
**Amazon Inspector** — avaliação contínua de vulnerabilidades.
</details>

---

**15. Qual serviço é o dashboard central que agrega GuardDuty, Inspector, Macie e Config?**
<details><summary>Ver resposta</summary>
**AWS Security Hub** — verifica CIS, PCI-DSS, AWS Foundational Best Practices.
</details>

---

**16. Quando usar Secrets Manager vs Parameter Store?**
<details><summary>Ver resposta</summary>
- **Secrets Manager**: segredos sensíveis com **rotação automática** (ex.: senha RDS).
- **Parameter Store**: configs gerais, **grátis** no tier padrão, SecureString via KMS, sem rotação nativa.
</details>

---

**17. IAM é regional ou global? Custa quanto?**
<details><summary>Ver resposta</summary>
**Global** (sem região) e **gratuito**.
</details>

---

**18. Quais são as boas práticas obrigatórias do root account?**
<details><summary>Ver resposta</summary>
Usar **apenas para tarefas iniciais**, habilitar **MFA**, criar usuários IAM com menor privilégio para uso diário.
</details>

---

**19. O que é AWS Control Tower?**
<details><summary>Ver resposta</summary>
**Landing Zone automatizada** multi-conta com guardrails preventivos e detectivos. Usa Organizations + IAM Identity Center + Config + CloudTrail por baixo.
</details>

---

**20. Quem libera todos os checks do Trusted Advisor?**
<details><summary>Ver resposta</summary>
Apenas planos **Business ou Enterprise Support**. Basic/Developer dão somente 6 checks básicos.
</details>

---

**21. Como automatizar a coleta de evidências para uma auditoria PCI/HIPAA?**
<details><summary>Ver resposta</summary>
**AWS Audit Manager** — frameworks prontos (CIS, GDPR, HIPAA, PCI-DSS).
</details>

---

**22. Você precisa gerenciar WAF, Shield e SGs em múltiplas contas. Qual serviço?**
<details><summary>Ver resposta</summary>
**AWS Firewall Manager** (requer Organizations).
</details>

---

**23. Pegadinha NACL: liberei HTTPS de entrada na subnet, mas a aplicação não responde. Por quê?**
<details><summary>Ver resposta</summary>
NACL é **stateless** — falta liberar **portas efêmeras (1024-65535) na saída** para o tráfego de retorno.
</details>

---

**24. IAM Identity Center é usado para quê?**
<details><summary>Ver resposta</summary>
**SSO** (login único) para múltiplas contas AWS e apps SaaS, integrando com Active Directory, Okta, Azure AD.
</details>

---

[← Voltar ao módulo](./README.md)
