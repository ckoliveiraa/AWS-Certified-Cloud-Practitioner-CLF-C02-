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

## Lab 3.4 — Explorar a Default VPC 🟢

> Pratica a [aula 3.5 — Rede](./3.5-rede.md).

> ℹ️ **Não vamos criar VPC** — toda conta AWS já vem com uma **Default VPC** pronta em cada região. Vamos explorá-la para entender os componentes na prática.

### Passos

1. **VPC** → **Your VPCs** → identifique a VPC com **Default VPC = Yes**.
2. Clique nela e observe:
   - **CIDR:** `172.31.0.0/16` (padrão da default)
   - **State:** Available
   - **DHCP options, Route tables, Network ACLs** associadas
3. **Resource map** (aba) — mostra a topologia visual: VPC + Subnets + Internet Gateway.

4. **Subnets** (menu lateral) → filtre por `Default VPC` → veja:
   - Uma **subnet pública por AZ** (geralmente 3-6 dependendo da região).
   - CIDR de cada uma (ex: `172.31.0.0/20`, `172.31.16.0/20`...).
   - **Auto-assign public IPv4 = Yes** (default VPC sempre dá IP público).

5. **Internet Gateways** → existe 1 IGW anexado à default VPC.

6. **Route Tables** → veja a tabela principal:
   - Rota local: `172.31.0.0/16 → local`
   - Rota internet: `0.0.0.0/0 → igw-xxxxx`

7. **Security Groups** → veja o **default SG** (criado automaticamente):
   - Inbound: permite tráfego do **próprio SG**.
   - Outbound: permite **tudo** (`0.0.0.0/0`).

8. **Network ACLs** → veja a default NACL:
   - Permite **tudo** entrada e saída (depois você restringe se quiser).

### Conceitos para fixar
- **Default VPC** = pronta para uso, todas subnets públicas, IGW anexado.
- **CIDR padrão:** `172.31.0.0/16`.
- **Cada conta AWS tem uma Default VPC por região.**
- **Se deletada por engano**, dá pra recriar via console (botão "Create default VPC").

### Pergunta para fixar
> *"Por que a Default VPC é prática para começar mas não recomendada para produção?"*
>
> Resposta: tudo é público por padrão, sem segregação entre tiers, CIDR fixo (pode conflitar com on-prem). Em produção use **VPC customizada** com subnets públicas/privadas separadas.

> 🟢 Tudo grátis — apenas leitura/exploração. Para criar VPC customizada com subnets pública + privada, ver Desafio 3 do homework.

---

## Lab 3.5 — DynamoDB (tour pelo console) 🟢

> Pratica a [aula 3.4 — Bancos de Dados](./3.4-bancos-de-dados.md).

> ℹ️ **Não vamos criar tabela** — apenas explorar a interface para entender o serviço. Criar/operar fica para o homework.

### Passos
1. **DynamoDB** → **Tables** → clique em **Create table** (mas **não finalize**).
2. Observe os campos:
   - **Partition key** e **Sort key** (chave composta).
   - **Capacity mode:** **On-demand** (paga por request) vs **Provisioned** (reserva RCU/WCU).
   - **Encryption** habilitada por padrão (KMS).
3. **Cancel** sem criar.
4. No menu lateral, explore: **Backups, Streams, Global Tables, DAX**.
5. Veja em **Explore items** o exemplo (sem dados).

### Conceitos para fixar
- **NoSQL key-value serverless** — escala para milhões de req/s.
- **Latência single-digit ms**.
- **Global Tables** = multi-região ativo-ativo.
- **DAX** = cache em memória (microssegundos).

> 🟢 Só navegar é grátis. Criar/popular tabela: ver Desafio 7 do homework.

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

### Parte C — Disparar o alarme (opcional, para ver funcionando)

1. Conecte na EC2 do Lab 3.1 via **Session Manager** (ver Lab 3.14).
2. Rode `yes > /dev/null & yes > /dev/null & yes > /dev/null &` para subir CPU a 100%.
3. Aguarde ~5 min → alarme muda para **In alarm** e você recebe **e-mail do SNS**.
4. Mate os processos: `pkill yes`.

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

## Lab 3.9 — RDS (tour pelo console) 🟢

> Pratica a [aula 3.4 — Bancos de Dados](./3.4-bancos-de-dados.md).

> ℹ️ **Não vamos criar instância** — RDS esquecido é o **vilão #1 de surpresa de fatura**. Apenas tour pela interface. Quem quiser criar, ver Desafio 7 do homework.

### Passos
1. **RDS** → **Create database** (mas **não finalize**).
2. Observe as opções:
   - **Engine:** MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, **Aurora**.
   - **Templates:** Production, Dev/Test, **Free tier**.
   - **Multi-AZ deployment:** standby síncrono em outra AZ (HA).
   - **Read replicas:** assíncrono (escala leitura — visível depois da criação).
   - **Storage autoscaling**.
3. **Cancel** sem criar.
4. No menu lateral, explore: **Snapshots, Automated backups, Reserved instances, Performance Insights**.

### Conceitos para fixar
- **Multi-AZ** = HA (failover automático em ~60s).
- **Read Replica** = performance de leitura (não é HA).
- **Aurora** = 5x MySQL / 3x PostgreSQL, 6 cópias em 3 AZs.
- **Engines suportadas:** MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Db2, Aurora.

> 🟢 Só navegar é grátis. **Subir RDS de verdade só no homework, e SEMPRE delete ao terminar.**

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

## Lab 3.14 — Session Manager: acessar EC2 sem SSH 🟢

> Pratica a [aula 3.6 — Monitoramento e Gestão](./3.6-monitoramento-gestao.md) (Systems Manager).

**Cenário:** acessar a EC2 do Lab 3.1 **sem abrir porta 22 (SSH) e sem key pair**.

### Pré-requisito
A EC2 precisa ter a **role `AmazonSSMManagedInstanceCore`** anexada. Se não tiver:
1. **IAM** → **Roles** → Create role → AWS service → EC2.
2. Adicione policy `AmazonSSMManagedInstanceCore`. Nome: `EC2-SSM-Role`.
3. EC2 → instância → **Actions** → **Security** → **Modify IAM role** → anexe.
4. Reinicie a instância (ou aguarde ~5 min para o agente conectar).

### Passos
1. **Systems Manager** → **Session Manager** → **Start session**.
2. Selecione a EC2 `web-lab-ec2` → **Start session**.
3. Shell abre no navegador. Rode:
   ```bash
   whoami
   curl http://localhost
   sudo cat /var/log/cloud-init-output.log | tail -20
   ```

**Validação:** você está dentro da EC2 sem SSH, sem chave, sem porta 22.

> 🟢 Session Manager é **gratuito**. **Bônus:** agora você pode **remover a regra SSH (22)** do `web-lab-sg` — segurança extra.

---

## Lab 3.15 — Athena: SQL serverless sobre S3 🟢

> Pratica a [aula 3.9 — Analytics, IA e ML](./3.9-analytics-ia-ml.md).

**Cenário:** rodar SQL diretamente sobre um CSV no S3, sem subir banco.

### Passos

1. Crie um arquivo `vendas.csv` local:
   ```csv
   id,produto,valor,regiao
   1,Notebook,3500,SP
   2,Mouse,80,RJ
   3,Teclado,250,SP
   4,Monitor,1200,MG
   5,Cabo USB,15,RJ
   ```

2. **S3** → use o bucket do Lab 3.2 → crie pasta `athena-lab/` → suba o `vendas.csv`.

3. **Athena** → **Query editor** → ao primeiro acesso, configure **Settings** → **Manage** → defina **Query result location**: `s3://<seu-bucket>/athena-results/` → **Save**.

4. Crie a tabela:
   ```sql
   CREATE EXTERNAL TABLE vendas (
     id int,
     produto string,
     valor double,
     regiao string
   )
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
   STORED AS TEXTFILE
   LOCATION 's3://SEU-BUCKET/athena-lab/'
   TBLPROPERTIES ('skip.header.line.count'='1');
   ```

5. Rode queries:
   ```sql
   SELECT * FROM vendas;
   SELECT regiao, SUM(valor) AS total FROM vendas GROUP BY regiao;
   ```

**Validação:** resultado aparece no editor e no S3 (`athena-results/`).

> 🟢 Athena cobra **US$ 5/TB scaneado** — esse CSV de poucos KB custa **frações de centavo**. Free tier não cobre, mas é praticamente grátis.

---

## Lab 3.16 — Polly: texto vira fala 🟡

> Pratica a [aula 3.9 — Analytics, IA e ML](./3.9-analytics-ia-ml.md) (IA pronta).

### Passos

1. **Amazon Polly** → **Text-to-Speech**.
2. **Engine:** Neural. **Language:** Portuguese (Brazilian).
3. **Voice:** Camila (ou outra).
4. Cole no editor:
   ```
   Olá! Estou estudando para a certificação AWS Cloud Practitioner.
   Hoje aprendi sobre Amazon Polly, um serviço que converte texto em fala.
   ```
5. **Listen** para ouvir no navegador.
6. **Download MP3** para baixar o áudio.

**Validação:** áudio MP3 baixado com a voz neural em português.

> 🟡 5M caracteres/mês (Standard) ou 1M (Neural) **grátis nos 12 primeiros meses**. Esse lab usa <500 caracteres.

---

## Lab 3.17 — Step Functions: workflow visual 🟡

> Pratica a [aula 3.7 — Integração e Mensageria](./3.7-integracao-mensageria.md).

**Cenário:** orquestrar 2 Lambdas em sequência com lógica condicional.

### Passos

1. **Lambda** → crie 2 funções Python:
   - `validate-order` — retorna `{ "valid": true }` se `valor > 100`, senão `false`:
     ```python
     def lambda_handler(event, context):
         valor = event.get("valor", 0)
         return {"valid": valor > 100, "valor": valor}
     ```
   - `process-order` — retorna `{ "status": "approved" }`:
     ```python
     def lambda_handler(event, context):
         return {"status": "approved", "valor": event["valor"]}
     ```

2. **Step Functions** → **Create state machine** → **Design your workflow visually** → **Standard**.

3. No **Workflow Studio**:
   - Arraste **Lambda Invoke** → selecione `validate-order`.
   - Arraste **Choice** após o primeiro Lambda.
   - Configure: se `$.Payload.valid == true` → próximo bloco; senão → **Fail**.
   - No "true": arraste outro **Lambda Invoke** → `process-order`.
   - No "false": arraste **Fail** state com motivo "Pedido inválido".

4. **Name:** `order-workflow`. Permissões: criar nova role.
5. **Create state machine**.

6. **Start execution** com:
   ```json
   { "valor": 200 }
   ```
   Veja o fluxo passar pelos dois Lambdas no diagrama animado.

7. Teste com `{ "valor": 50 }` → deve cair em **Fail**.

**Validação:** dois execuções no histórico, uma com sucesso e outra falhada, com diagrama visual mostrando o caminho.

### 🧹 Limpeza
- Delete a state machine + os 2 Lambdas + as roles geradas.

> 🟡 4.000 transições/mês grátis (Standard) — esse lab usa <10. Lambdas estão no free tier.

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
- [ ] Lab 3.4 — Default VPC (tour conceitual)
- [ ] Lab 3.5 — DynamoDB (tour conceitual)
- [ ] Lab 3.6 — Alarme CloudWatch + SNS
- [ ] Lab 3.7 — EBS snapshot + restore
- [ ] Lab 3.8 — S3 lifecycle rule
- [ ] Lab 3.9 — RDS (tour conceitual)
- [ ] Lab 3.10 — CloudFront na frente do S3
- [ ] Lab 3.11 — SNS → SQS fan-out
- [ ] Lab 3.12 — CloudFormation stack
- [ ] Lab 3.13 — Auto Scaling + ELB (conceitual)
- [ ] Lab 3.14 — Session Manager (acessar EC2 sem SSH)
- [ ] Lab 3.15 — Athena (SQL no S3)
- [ ] Lab 3.16 — Polly (texto → fala)
- [ ] Lab 3.17 — Step Functions (workflow visual)

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
- [ ] **CloudWatch Alarm** + **SNS topic alarms-lab** (Lab 3.6) — delete
- [ ] **Step Functions state machine** + Lambdas (Lab 3.17) — delete
- [ ] **Athena tabela e query results** (Lab 3.15) — delete a tabela e limpe a pasta `athena-results/` no S3
- [ ] **IAM role** `EC2-SSM-Role` (Lab 3.14) — manter se for reutilizar; senão delete
> ℹ️ Labs 3.4 (Default VPC), 3.5 (DynamoDB) e 3.9 (RDS) são **conceituais** — sem recursos para limpar.

> 💰 No dia seguinte, confira **Billing → Free Tier** para ter certeza de que nada está cobrando.

---

[← Voltar ao módulo](./README.md)
