# Flashcards — Módulo 2

---

**1. Quem é responsável pelos patches do SO em uma instância EC2?**
<details><summary>Ver resposta</summary>
O **cliente**. Em IaaS, SO é responsabilidade do cliente.
</details>

---

**2. Quem é responsável pelos patches do engine MySQL em RDS?**
<details><summary>Ver resposta</summary>
A **AWS**. RDS é serviço gerenciado (PaaS).
</details>

---

**3. Qual serviço detecta ameaças por ML na conta AWS?**
<details><summary>Ver resposta</summary>
**Amazon GuardDuty**.
</details>

---

**4. Qual serviço identifica dados sensíveis (PII) no S3?**
<details><summary>Ver resposta</summary>
**Amazon Macie**.
</details>

---

**5. Diferença entre CloudTrail e CloudWatch?**
<details><summary>Ver resposta</summary>
- **CloudTrail**: registra **chamadas de API** (quem fez o quê).
- **CloudWatch**: **métricas, logs e alarmes** de recursos.
</details>

---

**6. O que é uma SCP?**
<details><summary>Ver resposta</summary>
Service Control Policy — **guardrail** em Organizations que **limita** o que contas/OUs podem fazer. Não concede permissões.
</details>

---

**7. Diferença entre KMS e CloudHSM?**
<details><summary>Ver resposta</summary>
- **KMS**: multi-tenant, FIPS 140-2 L2, mais barato.
- **CloudHSM**: dedicado (single-tenant), **FIPS L3**, você controla 100% das chaves.
</details>

---

**8. Qual serviço fornece certificados SSL/TLS gratuitos?**
<details><summary>Ver resposta</summary>
**AWS Certificate Manager (ACM)**.
</details>

---

**9. Onde baixar o relatório SOC 2 da AWS?**
<details><summary>Ver resposta</summary>
**AWS Artifact**.
</details>

---

**10. Security Group é stateful ou stateless?**
<details><summary>Ver resposta</summary>
**Stateful** (NACL é stateless).
</details>

---

[← Voltar ao módulo](./README.md)
