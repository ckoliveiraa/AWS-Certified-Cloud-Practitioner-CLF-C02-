# Laboratórios — Módulo 3

> **Legenda de custo**
> 🟢 **Grátis sempre** &nbsp;|&nbsp; 🟡 **Free Tier** (limite mensal/12 meses) &nbsp;|&nbsp; 🟠 **Trial** (período limitado) &nbsp;|&nbsp; 🔴 **Cobra desde o 1º uso** (lembre de desligar)

---

## Lab 3.1 — Lançar uma instância EC2 com web server 🟡

> Pratica a [aula 3.2 — Computação](./3.2-computacao.md).

### Passos

1. **EC2** → **Launch instance**.
2. **Name:** `web-lab-ec2`.
3. **AMI:** Amazon Linux 2023. **Tipo:** `t2.micro` ou `t3.micro` (Free Tier).
4. **Key pair:** `Proceed without a key pair` (não precisamos de SSH).
5. **Network:** VPC default, subnet pública, **Auto-assign public IP = Enable**.
6. **Security Group:** crie `web-lab-sg` permitindo:
   - **HTTP (80)** de `0.0.0.0/0`
   - **SSH (22)** apenas do **seu IP** (descubra em https://checkip.amazonaws.com)
7. **IAM role:** `EC2-S3-ReadOnly` (criada no Lab 2.3 do Módulo 2).
8. **Advanced details → User data:**
   ```bash
   #!/bin/bash
   dnf install -y httpd
   echo "<h1>Olá CLF-C02 - Lab 3.1</h1>" > /var/www/html/index.html
   systemctl enable --now httpd
   ```
9. **Launch instance**.

**Validação:** após ~2 min, abra `http://<public-ip>` no navegador → vê o título *"Olá CLF-C02 - Lab 3.1"*.

> 🟡 **Free Tier:** 750h/mês de t2/t3.micro nos 12 primeiros meses. **Mantenha a EC2 rodando** durante os labs 3.6 e 3.10 — termine apenas no final.

---

## Lab 3.2 — Site estático no S3 🟡

> Pratica a [aula 3.3 — Armazenamento](./3.3-armazenamento.md).

### Passos

1. **S3** → **Create bucket** → nome único global (ex.: `site-lab-<seu-nome>-<data>`).
2. **Desmarque** *Block all public access* (confirme com `confirm`).
3. Após criar: **Properties** → **Static website hosting** → **Enable** → Index document: `index.html`.
4. Crie um arquivo `index.html` local com o conteúdo abaixo e faça upload:

   ```html
   <!DOCTYPE html>
   <html lang="pt-BR">
   <head>
     <meta charset="UTF-8">
     <title>Site Estático no S3</title>
     <style>
       body { font-family: Arial, sans-serif; max-width: 600px; margin: 50px auto; text-align: center; }
       h1 { color: #ff9900; }
       .badge { background: #232f3e; color: white; padding: 8px 16px; border-radius: 4px; display: inline-block; }
     </style>
   </head>
   <body>
     <h1>🚀 Site Estático no S3</h1>
     <p class="badge">Lab 3.2 — AWS CLF-C02</p>
     <p>Servido diretamente do Amazon S3, sem servidor!</p>
     <p>Aluno: <strong>Seu Nome Aqui</strong></p>
   </body>
   </html>
   ```
5. **Permissions** → **Bucket policy** → cole (substitua `SEU-BUCKET-AQUI`):
   ```json
   {
     "Version": "2012-10-17",
     "Statement": [{
       "Sid": "PublicRead",
       "Effect": "Allow",
       "Principal": "*",
       "Action": "s3:GetObject",
       "Resource": "arn:aws:s3:::SEU-BUCKET-AQUI/*"
     }]
   }
   ```

**Validação:** acesse a URL exibida em **Static website hosting** (formato `http://<bucket>.s3-website-<região>.amazonaws.com`) → vê o site.

> ⚠️ **Nunca use bucket público com dados reais.** Para o lab é OK porque é só HTML estático.
> 🟡 5 GB grátis/mês. **Não delete o bucket** — vamos usá-lo no Lab 3.10 (CloudFront).

---

## Lab 3.3 — Lambda "Hello World" 🟡

> Pratica a [aula 3.2 — Computação](./3.2-computacao.md) (serverless).

1. **Lambda** → **Create function** → **Author from scratch**.
2. **Name:** `hello-clf`. **Runtime:** Python 3.12. **Architecture:** x86_64.
3. **Permissions:** Create new role with basic Lambda permissions.
4. Substitua o código:
   ```python
   def lambda_handler(event, context):
       nome = event.get("nome", "mundo")
       return {"statusCode": 200, "body": f"Olá {nome} do Lambda!"}
   ```
5. **Deploy** → aba **Test** → **Create new test event** com nome `meuTeste`:
   ```json
   { "nome": "Carlos" }
   ```
6. **Test**.

**Validação:** resposta `200` com body `Olá Carlos do Lambda!`.

> 🟡 1M de invocações + 400.000 GB-seconds **grátis sempre** (não é só 12 meses).

---

## Lab 3.4 — VPC customizada com subnets 🟢

> Pratica a [aula 3.5 — Rede](./3.5-rede.md).

1. **VPC** → **Create VPC** → **VPC and more**.
2. **Name:** `lab-vpc`. **CIDR:** `10.0.0.0/16`.
3. **AZs:** 2. **Public subnets:** 1. **Private subnets:** 1. **NAT gateway:** **None** (NAT cobra US$ 32/mês — não criar!).
4. **VPC endpoints:** None.
5. **Create VPC**.

**Validação:** veja na aba **Resource map**: 1 VPC + 2 subnets + 1 IGW + 2 route tables, todos conectados.

> 🟢 VPC, subnets, route tables e IGW são **grátis sempre**. **NAT Gateway e VPC Endpoints cobram** — não crie.

---

## Lab 3.5 — DynamoDB com item 🟡

> Pratica a [aula 3.4 — Bancos de Dados](./3.4-bancos-de-dados.md).

1. **DynamoDB** → **Create table**.
2. **Name:** `Users`. **Partition key:** `id` (String).
3. **Settings:** Default settings (capacity mode On-demand).
4. **Create**.
5. Tabela criada → **Explore items** → **Create item**:
   ```json
   { "id": "1", "nome": "Carlos", "cargo": "Engenheiro de Dados" }
   ```
6. **Create item**.

**Validação:** item listado com 3 atributos.

> 🟡 25 GB + 25 RCU + 25 WCU **grátis sempre** (On-demand cobra por request, mas tem free tier).

---

## Lab 3.6 — Alarme CloudWatch + SNS (conceitual + prático) 🟡

> Pratica a [aula 3.6 — Monitoramento](./3.6-monitoramento-gestao.md).

### Parte A — Conceitual
- **CloudWatch Alarm** observa uma métrica (ex.: `CPUUtilization`).
- Quando passa do threshold, muda de estado (`OK → In alarm`).
- Dispara ação: publica num **SNS topic**.
- **SNS** entrega para inscritos (e-mail, SMS, Lambda, SQS).

### Parte B — Prática (use a EC2 do Lab 3.1)
1. **CloudWatch** → **Alarms** → **Create alarm** → **Select metric** → **EC2** → **Per-Instance Metrics** → instância `web-lab-ec2` → métrica `CPUUtilization`.
2. **Threshold:** Static, Greater than `70`. Period: 5 min.
3. **Notification:** Create new SNS topic `alarms-lab` → inscreva seu e-mail.
4. **Confirme** a inscrição no e-mail recebido (link "Confirm subscription").
5. **Alarm name:** `cpu-alarm-lab`.

**Validação:** alarme criado com estado `Insufficient data` ou `OK`. Confirme inscrição SNS.

> 🟡 10 alarmes + 1.000 publicações SNS grátis/mês por 12 meses.

---

## Lab 3.7 — EBS Snapshot e restore 🟡

> Pratica a [aula 3.3 — Armazenamento](./3.3-armazenamento.md) (block storage).

1. **EC2** → **Volumes** → identifique o volume da EC2 do Lab 3.1.
2. Selecione → **Actions** → **Create snapshot**. Nome: `web-lab-snapshot`.
3. Vá em **Snapshots** e aguarde status **Completed**.
4. Selecione o snapshot → **Actions** → **Create volume from snapshot** → AZ qualquer → **Create**.
5. Veja em **Volumes** o novo volume `Available` (não anexado a nada).

**Validação:** snapshot `Completed` + novo volume criado a partir dele.

### 🧹 Limpeza
- Delete o **volume restaurado** (Actions → Delete).
- **Delete o snapshot** (Actions → Delete).

> 🟡 1 GB de snapshot grátis/mês. Volumes EBS cobram US$ 0,08/GB-mês — delete logo.

---

## Lab 3.8 — S3 Lifecycle (Standard → IA → Glacier) 🟢

> Pratica a [aula 3.3 — Armazenamento](./3.3-armazenamento.md) (storage classes).

1. **S3** → bucket do Lab 3.2 → aba **Management** → **Create lifecycle rule**.
2. **Name:** `archive-rule`. **Scope:** Apply to all objects.
3. Marque **This rule will apply to all objects in the bucket**.
4. **Lifecycle rule actions:** marque **Move current versions of objects between storage classes**.
5. Adicione transições:
   - Após **30 dias** → **Standard-IA**
   - Após **90 dias** → **Glacier Flexible Retrieval**
   - Após **365 dias** → **Glacier Deep Archive**
6. **Create rule**.

**Validação:** regra ativa listada na aba Management.

> 🟢 Configurar lifecycle é grátis. As **transições futuras** podem cobrar (depende da classe). Para o lab, basta ter a regra criada — não há objetos suficientes para gerar custo real.

---

## Lab 3.9 — RDS MySQL t3.micro (free tier) 🟡

> Pratica a [aula 3.4 — Bancos de Dados](./3.4-bancos-de-dados.md).

> ⚠️ Demora ~10 min para o RDS ficar disponível. Ative apenas se for de fato testar; senão pule e leia a teoria.

1. **RDS** → **Create database** → **Standard create**.
2. **Engine:** MySQL. **Edition:** Community. **Version:** padrão.
3. **Templates:** **Free tier**.
4. **DB instance identifier:** `lab-db`.
5. **Master username:** `admin`. **Master password:** anote.
6. **Instance class:** `db.t3.micro`.
7. **Storage:** 20 GB gp2. Desmarque **Storage autoscaling**.
8. **Connectivity:**
   - **Public access:** No
   - **VPC security group:** crie `rds-lab-sg` permitindo MySQL (3306) **só** do `web-lab-sg` (do Lab 3.1).
9. **Multi-AZ:** No. **Backup:** 0 dias (para evitar custo).
10. **Create database**.

**Validação:** após ~10 min, status **Available**. Endpoint visível em **Connectivity & security**.

### 🧹 Limpeza obrigatória
- **RDS** → instância → **Actions** → **Delete** → desmarque "Create final snapshot" → confirme.

> 🟡 750h/mês de db.t3.micro + 20 GB grátis nos 12 primeiros meses. **Sempre delete** ao terminar — RDS esquecido é o vilão #1 de surpresa de fatura.

---

## Lab 3.10 — CloudFront na frente do bucket S3 🟡

> Pratica a [aula 3.5 — Rede](./3.5-rede.md) (CDN).

1. **CloudFront** → **Create distribution**.
2. **Origin domain:** selecione o bucket do Lab 3.2 (formato `bucket.s3.amazonaws.com`, não o endpoint de website).
3. **Origin access:** **Origin access control settings (recommended)** → **Create new OAC**.
4. **Viewer protocol policy:** Redirect HTTP to HTTPS.
5. **Default root object:** `index.html`.
6. **Create distribution**.
7. CloudFront vai pedir para você **atualizar a bucket policy** → copie o JSON sugerido e cole na bucket policy do S3 (substitui o do Lab 3.2).
8. Aguarde ~5 min para o status virar **Deployed**.

**Validação:** acesse `https://<distribution-id>.cloudfront.net` → vê o site do Lab 3.2 servido com HTTPS pela CDN.

### 🧹 Limpeza
- **CloudFront** → distribution → **Disable** (aguarda 15 min) → **Delete**.

> 🟡 1 TB de egress + 10M requests grátis/mês **sempre** (não é só 12 meses).

---

## Lab 3.11 — SQS + SNS fan-out 🟡

> Pratica a [aula 3.7 — Integração e Mensageria](./3.7-integracao-mensageria.md).

### Passos

1. **SQS** → **Create queue** → tipo **Standard** → nome `lab-queue` → **Create**.
2. **SNS** → **Topics** → **Create topic** → tipo **Standard** → nome `lab-topic` → **Create**.
3. No SNS topic → **Create subscription** → Protocol **Amazon SQS** → escolha `lab-queue` → **Create**.
4. No tópico SNS → **Publish message** → body: `Mensagem teste fan-out` → **Publish**.
5. Volte ao **SQS** → `lab-queue` → **Send and receive messages** → **Poll for messages**.

**Validação:** a mensagem aparece na fila SQS — chegou via SNS → SQS (fan-out).

### 🧹 Limpeza
- Delete a subscription, o topic SNS e a queue SQS.

> 🟡 1M de requests SQS + 1M publicações SNS grátis/mês por 12 meses.

---

## Lab 3.12 — CloudFormation: stack com S3 🟢

> Pratica a [aula 3.8 — Ferramentas de Desenvolvedor](./3.8-ferramentas-desenvolvedor.md) (IaC).

1. **CloudFormation** → **Create stack** → **With new resources (standard)** → **Choose an existing template** → **Create template in Infrastructure Composer** ou cole o YAML abaixo em **Template source: Upload a template file**:

   ```yaml
   AWSTemplateFormatVersion: '2010-09-09'
   Description: Lab 3.12 - bucket simples via IaC
   Resources:
     LabBucket:
       Type: AWS::S3::Bucket
       Properties:
         BucketName: !Sub 'cfn-lab-${AWS::AccountId}-${AWS::Region}'
         VersioningConfiguration:
           Status: Enabled
   Outputs:
     BucketName:
       Value: !Ref LabBucket
   ```

2. **Stack name:** `lab-iac-stack`. Sem parâmetros. Sem capabilities. Próximo, próximo, **Submit**.
3. Aguarde status **CREATE_COMPLETE**.

**Validação:** aba **Outputs** mostra o nome do bucket criado. Vá no S3 e confirme.

### 🧹 Limpeza
- **CloudFormation** → stack → **Delete** → confirme. O bucket é removido junto.

> 🟢 CloudFormation é **grátis** — você só paga pelos recursos criados pelo template.

---

## Lab 3.13 — Auto Scaling Group + ELB (apenas conceitual)

> ℹ️ **Não vamos criar** — apenas entenda o fluxo, que cai na prova:
>
> 1. **Launch Template** define a "receita" da EC2 (AMI + tipo + user data + SG).
> 2. **Auto Scaling Group (ASG)** mantém **N instâncias rodando** (mín / desejado / máx) baseado em métrica (ex.: CPU > 70%).
> 3. **Application Load Balancer (ALB)** distribui tráfego HTTP entre as instâncias do ASG.
> 4. Se uma instância falhar, ASG mata e cria outra automaticamente.
>
> 🎯 **Frase para a prova:** *"Auto Scaling = elasticidade horizontal automática; ELB = distribuição de tráfego."*
>
> 💡 Por que não fazer prático? ALB cobra **US$ 16/mês fixo**, mesmo sem tráfego. Não vale a pena para conta de estudo.

---

## Checklist Final do Módulo 3

- [ ] Lab 3.1 — EC2 com web server (mantenha rodando)
- [ ] Lab 3.2 — Site estático no S3
- [ ] Lab 3.3 — Lambda Hello World
- [ ] Lab 3.4 — VPC customizada (sem NAT)
- [ ] Lab 3.5 — DynamoDB com item
- [ ] Lab 3.6 — Alarme CloudWatch + SNS
- [ ] Lab 3.7 — EBS snapshot + restore
- [ ] Lab 3.8 — S3 lifecycle rule
- [ ] Lab 3.9 — RDS MySQL (opcional, leva 10 min)
- [ ] Lab 3.10 — CloudFront na frente do S3
- [ ] Lab 3.11 — SNS → SQS fan-out
- [ ] Lab 3.12 — CloudFormation stack
- [ ] Lab 3.13 — Auto Scaling + ELB (conceitual)

## Limpeza pós-laboratórios (CRÍTICO)

Para evitar custo inesperado, ao terminar **delete na ordem**:

- [ ] **CloudFront** distribution (Lab 3.10) — disable → wait 15 min → delete
- [ ] **RDS** instance (Lab 3.9) — sem snapshot final
- [ ] **EC2** `web-lab-ec2` (Lab 3.1) — Terminate
- [ ] **EBS volumes não anexados** (Lab 3.7) — delete
- [ ] **EBS snapshots** (Lab 3.7) — delete
- [ ] **CloudFormation** stack (Lab 3.12) — delete (remove bucket junto)
- [ ] **SQS queue + SNS topic** (Lab 3.11) — delete
- [ ] **S3 bucket** do Lab 3.2 — empty + delete (após CloudFront sumir)
- [ ] **DynamoDB** table `Users` (Lab 3.5) — delete
- [ ] **CloudWatch Alarm** + **SNS topic alarms-lab** (Lab 3.6) — delete
- [ ] **VPC custom** `lab-vpc` (Lab 3.4) — delete (não delete a default)

> 💰 No dia seguinte, confira **Billing → Free Tier** para ter certeza de que nada está cobrando.

---

[← Voltar ao módulo](./README.md)
