# Laboratórios — Módulo 3

---

## Lab 3.1 — Lançar uma instância EC2

1. **EC2** → **Launch instance**.
2. Nome: `web-lab`. AMI: **Amazon Linux 2023**. Tipo: **t2.micro**.
3. Crie key pair (`.pem`) e baixe.
4. Security Group: abrir **HTTP (80)** e **SSH (22)** apenas do seu IP.
5. IAM role: `EC2-S3-ReadOnly` (do Lab 2.2).
6. User data:
   ```bash
   #!/bin/bash
   yum install -y httpd
   echo "Olá CLF-C02" > /var/www/html/index.html
   systemctl enable --now httpd
   ```
7. Launch.

**Validação**: acesse o **Public IPv4** pelo navegador.

**⚠️ Termine** ao final para não gastar Free Tier.

---

## Lab 3.2 — Hospedar site estático no S3

1. Bucket S3 público (desabilite Block Public Access).
2. **Properties → Static website hosting** → Enable.
3. Upload `index.html`.
4. Bucket policy para leitura pública.

**Validação**: abra a URL do endpoint estático.

---

## Lab 3.3 — Criar um Lambda "Hello World"

1. **Lambda** → **Create function** → **Author from scratch**.
2. Runtime: **Python 3.12**.
3. Código:
   ```python
   def lambda_handler(event, context):
       return {"statusCode": 200, "body": "Olá do Lambda"}
   ```
4. **Test** com evento vazio.

**Validação**: resposta 200.

---

## Lab 3.4 — Criar uma VPC com subnets

1. **VPC** → **Create VPC** → **VPC and more**.
2. CIDR `10.0.0.0/16`, 2 AZs, 1 pública + 1 privada.

**Validação**: VPC criada com IGW e route tables.

---

## Lab 3.5 — Criar DynamoDB e inserir item

1. **DynamoDB** → **Create table** → nome `Users`, PK `id` (String).
2. **Explore items** → **Create item** → `{ id: "1", nome: "Carlos" }`.

**Validação**: item listado.

---

## Lab 3.6 — Alarme CloudWatch

1. **CloudWatch** → **Alarms** → **Create alarm**.
2. Métrica: **EC2 CPUUtilization** da instância do Lab 3.1.
3. Limiar: `> 70% por 5 min`.
4. Crie SNS topic com seu email.

**Validação**: confirme inscrição no email.

---

## Checklist
- [ ] EC2 com site funcional (e terminada após o teste)
- [ ] Site estático S3
- [ ] Lambda executou
- [ ] VPC customizada
- [ ] DynamoDB com item
- [ ] Alarme CloudWatch

---

[← Voltar ao módulo](./README.md)
