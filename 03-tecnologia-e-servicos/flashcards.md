# Flashcards — Módulo 3

---

**1. Qual a diferença entre Região e AZ?**
<details><summary>Ver resposta</summary>
Região = localização geográfica. AZ = data center isolado dentro de uma região (mínimo 3 por região).
</details>

---

**2. EC2 Spot oferece até quanto de desconto?**
<details><summary>Ver resposta</summary>
Até **90%** — mas a instância pode ser interrompida com 2 minutos de aviso.
</details>

---

**3. Qual limite de execução do Lambda?**
<details><summary>Ver resposta</summary>
**15 minutos**.
</details>

---

**4. Qual a durabilidade do S3?**
<details><summary>Ver resposta</summary>
**99,999999999%** (11 noves).
</details>

---

**5. Diferença entre EBS e EFS?**
<details><summary>Ver resposta</summary>
- **EBS**: bloco, ligado a **1 EC2**, **AZ-específico**.
- **EFS**: NFS, compartilhado entre **várias EC2**, **multi-AZ**.
</details>

---

**6. O que é Aurora?**
<details><summary>Ver resposta</summary>
Banco relacional compatível com MySQL/PostgreSQL, **5x/3x mais rápido**, com 6 cópias em 3 AZs.
</details>

---

**7. Qual a diferença entre CloudFront e Global Accelerator?**
<details><summary>Ver resposta</summary>
- **CloudFront**: CDN HTTP/HTTPS, com cache.
- **Global Accelerator**: TCP/UDP, sem cache, 2 IPs estáticos.
</details>

---

**8. Qual serviço fornece SQL serverless sobre dados no S3?**
<details><summary>Ver resposta</summary>
**Amazon Athena**.
</details>

---

**9. SNS vs SQS?**
<details><summary>Ver resposta</summary>
- **SNS**: pub/sub, push.
- **SQS**: fila, pull.
</details>

---

**10. Qual serviço fornece IA generativa com modelos de fundação?**
<details><summary>Ver resposta</summary>
**Amazon Bedrock**.
</details>

---

[← Voltar ao módulo](./README.md)
