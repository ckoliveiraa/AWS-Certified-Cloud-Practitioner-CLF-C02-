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
4. **Key pair:** `Proceed without a key pair` (vamos usar EC2 Instance Connect pelo navegador).
5. **Network:** VPC default, subnet pública, **Auto-assign public IP = Enable**.
6. **Security Group:** crie `web-lab-sg` permitindo:
   - **HTTP (80)** de `0.0.0.0/0`
   - **SSH (22)** de `0.0.0.0/0` (necessário pro EC2 Instance Connect)
7. **Launch instance** e aguarde **`2/2 checks passed`** (~2 min).

### Conectar via EC2 Instance Connect

8. Selecione a instância → botão **Connect** → aba **EC2 Instance Connect** → **Connect**.
9. Vai abrir um terminal no navegador. Rode os comandos abaixo **um por um** (não cole tudo junto, o terminal pode capturar caracteres estranhos do paste):

   ```bash
   sudo dnf install -y httpd
   ```

   ```bash
   echo "<h1>Olá CLF-C02 - Lab 3.1</h1>" | sudo tee /var/www/html/index.html
   ```

   ```bash
   sudo systemctl enable --now httpd
   ```

   ```bash
   curl localhost
   ```

   O `curl localhost` deve retornar `<h1>Olá CLF-C02 - Lab 3.1</h1>` — confirma que o Apache subiu.

**Validação:** abra `http://<public-ip>` no navegador → vê o título *"Olá CLF-C02 - Lab 3.1"*.

> ⚠️ **Use `http://`, não `https://`** — o navegador costuma forçar HTTPS e dá erro (a EC2 só responde na porta 80).


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
2. **Antes de criar o alarme**, ative **Detailed monitoring** na EC2 para permitir period de 1 min: EC2 → instância `web-lab-ec2` → **Actions** → **Monitor and troubleshoot** → **Manage detailed monitoring** → **Enable**.
3. **Threshold:** Static, Greater than `50`. **Period: 1 minuto** (o **mínimo possível** para métrica de EC2). **Datapoints to alarm: 1 of 1** — dispara no primeiro ponto acima de 50%.
4. **Notification:** Create new SNS topic `alarms-lab` → inscreva seu e-mail.
5. **Confirme** a inscrição no e-mail recebido (link "Confirm subscription").
6. **Alarm name:** `cpu-alarm-lab`.

**Validação:** alarme criado com estado `Insufficient data` ou `OK`. Confirme inscrição SNS.

### Parte C — Disparar o alarme (opcional, para ver funcionando)

1. Conecte na EC2 do Lab 3.1 via **EC2 Instance Connect** (botão **Connect** → aba **EC2 Instance Connect** → **Connect**).
2. No terminal, rode para saturar a CPU:
   ```bash
   yes > /dev/null & yes > /dev/null & yes > /dev/null &
   ```
   - `yes` imprime "y" infinitamente (queima CPU); `> /dev/null` descarta a saída; `&` joga em background → 3 processos paralelos levam a `t2/t3.micro` a ~100%.
3. (opcional) Confirme com `top` — você vê 3 processos `yes` no topo. Aperte `q` pra sair.
4. Aguarde ~1-2 min → alarme muda para **In alarm** e você recebe **e-mail do SNS**.
5. Mate os processos:
   ```bash
   pkill yes
   ```
   Confirme com `top` que sumiram — senão a EC2 fica fervendo CPU à toa.

### Parte D — CloudWatch Logs: inspecionar log de um job do Glue 🔴

> **Por que aqui?** CloudWatch não é só métrica/alarme — é também o **destino padrão de logs** de quase todo serviço AWS (Lambda, ECS, Glue, API Gateway…). Vamos ver isso na prática com o **AWS Glue**, que escreve logs automaticamente em **CloudWatch Logs**.

> ⚠️ **Custo:** Glue **não tem free tier**. Um job Python Shell de poucos segundos custa ~**US$ 0,03** (1/16 DPU × tempo). Se preferir não pagar, pule para a Parte D-bis abaixo (apenas explorar a interface do CloudWatch Logs).

#### Passos

1. **IAM** → **Roles** → **Create role** → AWS service → **Glue**.
   - Adicione policies: `AWSGlueServiceRole` e `CloudWatchLogsFullAccess`.
   - Nome: `GlueLabRole`.

2. **AWS Glue** → **ETL jobs** → **Create job** → **Script editor** → **Engine: Python shell** → **Create script**.

3. **Job details:**
   - **Name:** `glue-log-lab`
   - **IAM Role:** `GlueLabRole`
   - **Type:** Python Shell
   - **Python version:** 3.9
   - **Data processing units:** **1/16 DPU** (o menor — mais barato)

4. Aba **Script** → cole:
   ```python
   import logging, sys, time

   logger = logging.getLogger()
   logger.setLevel(logging.INFO)
   handler = logging.StreamHandler(sys.stdout)
   logger.addHandler(handler)

   logger.info("=== Lab 3.6 — log do Glue indo para CloudWatch ===")
   for i in range(1, 6):
       logger.info(f"Processando item {i}/5")
       time.sleep(1)
   logger.warning("Exemplo de WARNING")
   logger.info("Job concluido com sucesso")
   ```

5. **Save** → **Run**. Aguarde status **Succeeded** (~30 s) na aba **Runs**.

6. Na linha do run, clique em **Output logs** (link azul) — abre direto o **CloudWatch Logs** no log group `/aws-glue/python-jobs/output`, no log stream do run.

7. No CloudWatch Logs, observe:
   - Cada `logger.info(...)` virou um evento com timestamp.
   - Use **Filter events** (campo de busca) → digite `WARNING` → filtra só o aviso.
   - Aba **Logs Insights** → selecione o log group `/aws-glue/python-jobs/output` → rode:
     ```
     fields @timestamp, @message
     | filter @message like /Processando/
     | sort @timestamp desc
     ```

**Validação:** você vê os 5 "Processando item N/5" + o WARNING no CloudWatch Logs, vindos do job do Glue.

#### Conceitos para fixar
- **Glue grava 2 log groups por job:** `/aws-glue/python-jobs/output` (stdout/`logger`) e `/aws-glue/python-jobs/error` (stderr/exceptions). Em jobs Spark é `/aws-glue/jobs/...`.
- Cada **execução do job** = um **log stream** próprio dentro do log group.
- **Logs Insights** = SQL-like sobre logs (mesma sintaxe serve pra Lambda, ECS, VPC Flow Logs).

#### 🧹 Limpeza
- **Glue** → job `glue-log-lab` → **Delete**.
- **CloudWatch Logs** → log groups `/aws-glue/python-jobs/output` e `/error` → **Delete** (opcional, mas evita acúmulo).
- **IAM role** `GlueLabRole` → delete se não for reutilizar.

### Parte D-bis — Alternativa grátis (se não quiser rodar o Glue) 🟢

Se quiser pular o custo do Glue, dá pra ver o mesmo conceito com a Lambda do **Lab 3.3**:

1. Lambda `hello-clf` → aba **Test** → execute 2-3 vezes.
2. Aba **Monitor** → **View CloudWatch logs** → entra no log group `/aws/lambda/hello-clf`.
3. Abra o log stream mais recente → veja `START / END / REPORT` + qualquer `print()` que a função fez.
4. **Logs Insights** funciona igual:
   ```
   fields @timestamp, @message
   | filter @type = "REPORT"
   | stats avg(@duration), max(@duration)
   ```

> 💡 **Mesmo princípio:** todo serviço gerenciado AWS manda logs para CloudWatch Logs sem você configurar nada — basta a role ter permissão de escrita.

> 🟡 10 alarmes + 1.000 publicações SNS grátis/mês por 12 meses.
> 🔴 Glue Python Shell 1/16 DPU ≈ **US$ 0,06/h** — um job de 30 s sai ~US$ 0,001. Mesmo assim, **delete o job ao final** pra não esquecer rodando agendado.

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

**Cenário:** colocar uma CDN global na frente do site estático do Lab 3.2 para servir com **HTTPS (cadeado)** e cache nas edge locations.

> ℹ️ O console novo do CloudFront usa um wizard de **5 passos com escolha de plano**. Para o lab usamos o plano **Free** ($0).

### Passos

**Step 1 — Choose a plan**
1. **CloudFront** → **Create distribution**.
2. Selecione o plano **Free** ($0/month) → **Next**.
   - Inclui: Global CDN, DDoS protection, TLS certificate, WAF básico, 1 M requests + 100 GB/mês.

**Step 2 — Get started**
3. **Distribution name:** `web-lab-cloud-front`.
4. **Distribution type:** **Single website or app**.
5. **Route 53 managed domain:** deixe em branco (vamos usar o domínio `cloudfront.net` que a AWS dá de graça).
6. **Next**.

**Step 3 — Specify origin**
7. **Origin type:** **Amazon S3**.
8. **S3 origin:** clique em **Browse S3** → selecione o bucket do Lab 3.2.
9. ⚠️ Vai aparecer o aviso: *"This S3 bucket has static web hosting enabled… Use website endpoint"* → **NÃO clique** em "Use website endpoint". Deixe o **bucket endpoint** (`bucket.s3.region.amazonaws.com`).
   - **Por quê?** O website endpoint é HTTP-only e público. Usando o REST endpoint, o CloudFront pode fechar o bucket (OAC) e ainda servir como site.
10. **Allow private S3 bucket access to CloudFront:** ✅ **marque** (Recommended). Isso é o **OAC** — CloudFront vai atualizar a bucket policy automaticamente para que só ele acesse o bucket.
11. **Origin settings:** **Use recommended origin settings**.
12. **Next**.

**Step 4 — Enable security**
13. **WAF:** já vem incluso no Free, deixe ativo.
14. **Use monitor mode:** desmarcado (em produção você ligaria para auditar antes de bloquear).
15. **Next**.

**Step 5 — Review and create**
16. Revise e clique **Create distribution**.
17. Após criar, vá em **General → Settings → Edit** → **Default root object:** `index.html` → **Save**.
    - Sem isso, acessar `https://xxx.cloudfront.net/` retorna erro — o CloudFront não sabe qual arquivo servir na raiz.
18. Aguarde ~5 min até o **Status: Deployed**.

### Validação
- Copie o **Distribution domain name** (ex: `d1a2b3c4.cloudfront.net`).
- Acesse `https://d1a2b3c4.cloudfront.net` no navegador.
- ✅ Site do Lab 3.2 carrega **com cadeado** 🔒.
- ✅ Tente `http://...` → redireciona para `https://` automaticamente.
- ✅ Tente acessar o bucket direto pelo endpoint S3 → agora dá **403 Access Denied** (OAC fechou).

### 🧹 Limpeza
1. **CloudFront** → distribution → **Disable** → confirme.
2. Aguarde ~15 min até `Last modified` parar de atualizar e status virar **Disabled**.
3. **Delete**.

> 🟢 Plano **Free**: 1 M requests + 100 GB/mês para sempre (não é só 12 meses). Bloqueios DDoS e WAF não contam na franquia. Tráfego entre S3 e CloudFront é **isento**.

---

## Lab 3.11 — CloudFormation: stack com S3 🟢

> Pratica a [aula 3.8 — Ferramentas de Desenvolvedor](./3.8-ferramentas-desenvolvedor.md) (IaC — Infraestrutura como Código).

**Cenário:** criar um bucket S3 via **template YAML** em vez do console. Mostra a essência do CloudFormation: você descreve, ele provisiona.

### Pré-requisito — salve o template localmente

Crie o arquivo `lab-iac.yaml` no seu computador com este conteúdo:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Lab 3.11 - bucket simples via IaC
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

> 💡 `!Sub` injeta variáveis (account ID + região) para garantir nome único globalmente.

### Passos (wizard de 4 steps)

**Step 1 — Create stack**
1. **CloudFormation** → **Create stack**.
2. **Prepare template:** **Choose an existing template**.
3. **Template source:** **Upload a template file** → **Choose file** → selecione o `lab-iac.yaml`.
4. **Next**.

**Step 2 — Specify stack details**
5. **Stack name:** `lab-iac-stack` (apenas letras, números e hífen).
6. **Parameters:** o template não tem parâmetros — vai aparecer *"No parameters"*.
7. **Next**.

**Step 3 — Configure stack options**
8. **Tags** (opcional): pule.
9. **Permissions → IAM role:** deixe **em branco** — CloudFormation usa as suas credenciais.
10. **Stack failure options:** mantenha **Roll back all stack resources** (default). Se algo falhar, ele desfaz tudo.
11. **Delete newly created resources during a rollback:** mantenha **Use deletion policy** (default).
12. **Next**.

**Step 4 — Review and create**
13. Revise. No final marque ✅ *"I acknowledge..."* se aparecer (não deve aparecer aqui — só pede quando o template cria IAM).
14. **Submit**.

### Acompanhar a criação
- A stack abre na aba **Events** mostrando cada recurso sendo criado em ordem (`CREATE_IN_PROGRESS` → `CREATE_COMPLETE`).
- Aguarde o status final **CREATE_COMPLETE** (~30 s para esse template).

### Validação
- Aba **Outputs** → veja o `BucketName` (ex: `cfn-lab-123456789012-us-east-2`).
- Vá em **S3** → confirme o bucket existe.
- Aba **Resources** mostra todos os recursos da stack (aqui só `LabBucket`).

### 🧹 Limpeza
- **CloudFormation** → stack → **Delete** → confirme.
- ✅ O bucket é apagado **junto** com a stack — não precisa esvaziá-lo no S3 (porque o template não tem objetos dentro).

> 🟢 CloudFormation é **grátis** — você paga só pelos recursos provisionados.

> 🎯 **Frase para a prova:** *"CloudFormation = IaC nativa da AWS. Você descreve em YAML/JSON, ele provisiona, atualiza e destrói tudo de forma idempotente."*

---

## Lab 3.12 — Athena: SQL serverless sobre S3 🟢

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

## Lab 3.13 — Polly: texto vira fala 🟡

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

## Lab 3.14 — Step Functions: workflow visual 🟡

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
- [ ] Lab 3.11 — CloudFormation stack
- [ ] Lab 3.12 — Athena (SQL no S3)
- [ ] Lab 3.13 — Polly (texto → fala)
- [ ] Lab 3.14 — Step Functions (workflow visual)

## Limpeza pós-laboratórios (CRÍTICO)

Para evitar custo inesperado, ao terminar **delete na ordem**:

- [ ] **CloudFront** distribution (Lab 3.10) — disable → wait 15 min → delete
- [ ] **RDS** instance (Lab 3.9) — sem snapshot final
- [ ] **EC2** `web-lab-ec2` (Lab 3.1) — Terminate
- [ ] **EBS volumes não anexados** (Lab 3.7) — delete
- [ ] **EBS snapshots** (Lab 3.7) — delete
- [ ] **CloudFormation** stack (Lab 3.11) — delete (remove bucket junto)
- [ ] **S3 bucket** do Lab 3.2 — empty + delete (após CloudFront sumir)
- [ ] **CloudWatch Alarm** + **SNS topic alarms-lab** (Lab 3.6) — delete
- [ ] **Glue job `glue-log-lab`** + log groups `/aws-glue/python-jobs/*` + role `GlueLabRole` (Lab 3.6 Parte D) — delete
- [ ] **Step Functions state machine** + Lambdas (Lab 3.14) — delete
- [ ] **Athena tabela e query results** (Lab 3.12) — delete a tabela e limpe a pasta `athena-results/` no S3
> ℹ️ Labs 3.4 (Default VPC), 3.5 (DynamoDB) e 3.9 (RDS) são **conceituais** — sem recursos para limpar.

> 💰 No dia seguinte, confira **Billing → Free Tier** para ter certeza de que nada está cobrando.

---

[← Voltar ao módulo](./README.md)
