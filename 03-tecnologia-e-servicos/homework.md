# Homework — Módulo 3: Tecnologia e Serviços

> 🎯 **Objetivo:** consolidar os principais serviços AWS (compute, storage, database, network, integration) com **desafios práticos** que simulam cenários reais.
>
> ⏱️ **Tempo estimado:** 4 a 6 horas.
>
> 💸 **Custo estimado:** **US$ 0 a US$ 3** se feito conforme as instruções (a maioria é Free Tier).

---

## ⚠️ Antes de começar — Limites do Free Tier (12 meses, salvo nota)

| Serviço | Limite mensal | Cuidado |
|---------|---------------|---------|
| **EC2** t2.micro / t3.micro | 750 horas | Termine ao final |
| **S3** | 5 GB + 20k GET + 2k PUT | Suficiente |
| **RDS** db.t3.micro | 750 horas + 20 GB | **Vilão #1 esquecido** |
| **DynamoDB** | 25 GB + 25 RCU/WCU | Sempre grátis |
| **Lambda** | 1M invocações + 400k GB-s | Sempre grátis |
| **CloudFront** | 1 TB egress + 10M reqs | Sempre grátis |
| **SQS / SNS** | 1M reqs cada | Free Tier 12 meses |
| **EBS** snapshots | 1 GB | Volumes cobram US$ 0,08/GB |
| **NAT Gateway** | ❌ **Sem free tier** | **US$ 32/mês** — não criar |
| **ALB** | ❌ **Sem free tier** | **US$ 16/mês** — não criar |

---

## Desafio 1 — Site estático completo (S3 + CloudFront) 🟡 grátis

**Cenário:** Sua empresa precisa hospedar uma landing page com **HTTPS** e **baixa latência global**.

### Tarefas
1. Crie um `index.html` simples com seu nome e foto (ou só texto).
2. Suba num bucket S3 com **Static website hosting** habilitado.
3. Crie uma distribuição **CloudFront** apontando para esse bucket usando **Origin Access Control (OAC)**.
4. Configure redirect HTTP → HTTPS.
5. Acesse o site pelos **dois endpoints**:
   - URL do bucket S3 (HTTP, sem cache global)
   - URL do CloudFront (HTTPS, com cache global)
6. **Compare os tempos de carregamento** com `curl -w "%{time_total}\n"` ou DevTools.

### Pergunta de raciocínio
> *"Por que o CloudFront é mais rápido na 2ª requisição que na 1ª? E por que o S3 sozinho é mais lento para usuários distantes?"*

### Entregáveis
- URL do CloudFront funcionando
- Print do site servido por HTTPS
- Resposta da pergunta (3-5 linhas)

> 🟡 **Custo:** zero dentro do Free Tier. Delete a distribuição ao terminar.

---

## Desafio 2 — Aplicação 3-tier serverless 🟡 grátis

**Cenário:** Construir uma API simples sem servidor para registrar usuários.

### Tarefas
1. Crie tabela DynamoDB `Users` com PK `email`.
2. Crie um Lambda `register-user` (Python) que recebe um JSON `{ "email": "x", "nome": "y" }` e grava no DynamoDB.
3. Anexe ao Lambda uma role com permissão `dynamodb:PutItem` apenas na tabela `Users`.
4. Teste pelo console do Lambda com **Test event**.
5. Verifique no DynamoDB que o item foi gravado.

### Pergunta de raciocínio
> *"Quais 3 vantagens do serverless (Lambda + DynamoDB) vs subir uma EC2 com Postgres para esse mesmo caso de uso?"*

### Entregáveis
- Print do Lambda executando com sucesso
- Print do item no DynamoDB
- Código do Lambda (`register-user.py`)

> 🟡 100% grátis dentro do Free Tier (e Lambda + DynamoDB têm tier perpétuo).

---

## Desafio 3 — Defesa em camadas de rede 🟡 grátis com t2.micro

**Cenário:** Subir uma aplicação que **só pode ser acessada via Load Balancer** — nunca direto.

### Tarefas (sem usar ALB pago — simulamos com SG)
1. Suba uma EC2 `app-server` em **subnet privada** (use a VPC do Lab 3.4).
2. Configure o SG da EC2 para aceitar HTTP **apenas** de outro SG `lb-sg` (que será o "balanceador").
3. Suba uma 2ª EC2 `bastion` em **subnet pública** com SG `lb-sg`.
4. Mostre que:
   - Internet **não** acessa direto a `app-server` (sem rota e sem SG)
   - O `bastion` consegue acessar a `app-server` (SG referenciando SG)

### Pergunta de raciocínio
> *"Qual a diferença entre referenciar um SG por ID (`sg-xxx`) e por CIDR (`0.0.0.0/0`)? Por que o primeiro é mais seguro?"*

### Entregáveis
- Print do `curl <ip-app-server>` falhando da internet ✅
- Print do `curl <ip-app-server>` funcionando do bastion ✅
- Resposta da pergunta

> 🟡 2 EC2 t2.micro = 1.500h/mês — ainda dentro de 750h se forem usadas alternadamente. **Termine ambas ao final.**

---

## Desafio 4 — Backup e desastre 🟡 ~US$ 0,10

**Cenário:** Sua EC2 do Lab 3.1 corrompeu. Recupere a partir de backup.

### Tarefas
1. Tire um **snapshot EBS** do volume da EC2 (Lab 3.7).
2. Termine a EC2 original (simulando "corrupção").
3. **Restaure** uma nova EC2 a partir do snapshot:
   - Crie uma AMI a partir do snapshot (EC2 → Snapshots → Actions → Create image)
   - Lance nova EC2 a partir dessa AMI
4. Verifique que a página `Olá CLF-C02` ainda está lá.

### Pergunta de raciocínio
> *"Qual a diferença entre **snapshot EBS** e **AMI**? Por que precisamos da AMI para criar uma nova EC2 e não só do snapshot?"*

### Entregáveis
- Print da AMI criada
- Print da nova EC2 funcionando com o conteúdo restaurado
- Resposta da pergunta

> 🟡 **Custo:** ~US$ 0,05 por GB-mês de snapshot. Delete tudo ao final (nova EC2, AMI, snapshot).

---

## Desafio 5 — Mensageria desacoplada (SNS → SQS) 🟡 grátis

**Cenário:** Você tem um serviço de **upload de imagens** que precisa disparar **3 ações independentes**: gerar thumbnail, indexar no banco, enviar e-mail.

### Tarefas
1. Crie 1 SNS topic `image-uploaded`.
2. Crie 3 SQS queues: `thumbnail-queue`, `index-queue`, `email-queue`.
3. Inscreva as 3 queues no topic SNS.
4. Publique uma mensagem no topic.
5. Confirme que **as 3 queues** receberam a mensagem (fan-out).

### Pergunta de raciocínio
> *"Por que esse padrão (SNS → múltiplas SQS) é melhor que o serviço de upload chamar os 3 consumidores diretamente? Pense em falhas."*

### Entregáveis
- Print das 3 queues com a mensagem recebida
- Diagrama (rascunho mesmo) da arquitetura
- Resposta da pergunta

> 🟡 1M reqs grátis/mês. **Delete tudo ao terminar.**

---

## Desafio 6 — Infraestrutura como Código 🟢 grátis

**Cenário:** Sua empresa quer **automatizar** a criação de ambientes idênticos para dev/staging/prod.

### Tarefas
1. Crie um template CloudFormation que cria:
   - 1 bucket S3 com versionamento
   - 1 DynamoDB table `Items` com PK `id`
   - 1 SQS queue `tasks`
2. Use **Parameters** para receber o nome do ambiente (`dev`/`staging`/`prod`).
3. Use o nome do ambiente nos nomes dos recursos (ex.: `bucket-${Env}`).
4. Lance a stack 2 vezes (uma para `dev`, outra para `staging`).
5. **Delete uma das stacks** e veja todos os recursos sumirem juntos.

### Pergunta de raciocínio
> *"Liste 3 vantagens de usar CloudFormation vs criar recursos no console manualmente."*

### Entregáveis
- Template YAML/JSON
- Print das 2 stacks com `CREATE_COMPLETE`
- Resposta da pergunta

> 🟢 CloudFormation é grátis; só os recursos criados podem cobrar (S3 e DynamoDB têm tier grátis generoso).

---

## Desafio 7 — Banco de dados gerenciado vs auto-gerenciado 🟡 ~US$ 0

**Cenário:** Compare RDS (gerenciado) com DynamoDB (NoSQL) para um caso real.

### Tarefas (escolha A ou B; ambas valem)

#### Opção A — RDS
1. Crie um RDS MySQL `db.t3.micro` (Lab 3.9).
2. Conecte via CloudShell: `mysql -h <endpoint> -u admin -p`.
3. Crie database `loja`, tabela `produtos` e insira 3 linhas.
4. Liste com `SELECT *`.

#### Opção B — DynamoDB
1. Use a tabela `Users` do Lab 3.5.
2. Insira 5 itens (com `cargo` variando).
3. Use **Scan** filtrando por `cargo = "Eng. de Dados"`.

### Pergunta de raciocínio
> *"Quando usar RDS vs DynamoDB? Liste 2 cenários ideais para cada um."*

### Entregáveis
- Print do `SELECT` (RDS) ou Scan (DynamoDB)
- Resposta da pergunta

> 🟡 RDS dentro do Free Tier; DynamoDB sempre grátis nesse volume. **Delete o RDS imediatamente após o teste.**

---

## Desafio 8 — Simulado de Cenários

Resolva sem consultar:

1. *"Workload com pico de 1h por dia, sem servidores fixos."* → Compute?
2. *"App precisa servir vídeos para 50 países com baixa latência."* → Serviço?
3. *"Banco relacional com schema rígido para sistema bancário."* → Serviço?
4. *"Storage barato para arquivos acessados 1x ao ano."* → Classe S3?
5. *"Comunicação assíncrona entre microsserviços com retry e DLQ."* → Serviço?
6. *"Notificar e-mail + SMS + Lambda quando um arquivo chega no S3."* → Padrão?
7. *"Replicar EC2 para outra AZ automaticamente em caso de falha."* → Serviço?
8. *"DNS com health check para failover automático entre regiões."* → Serviço?
9. *"Servir contêineres Docker sem gerenciar EC2."* → Serviço?
10. *"Criar 50 buckets idênticos com mesma config em segundos."* → Serviço?

<details>
<summary>🎯 Gabarito (clique)</summary>

1. **Lambda** (serverless, paga só quando executa)
2. **CloudFront** (CDN global)
3. **RDS** ou **Aurora**
4. **S3 Glacier Deep Archive**
5. **SQS** (com DLQ configurável)
6. **SNS fan-out** com múltiplas subscriptions
7. **Auto Scaling Group** com health checks
8. **Route 53** com routing policy de failover
9. **AWS Fargate** (containers serverless)
10. **CloudFormation** (IaC)

</details>

---

## Bônus — Diagrama da arquitetura 3-tier

Desenhe (Draw.io / Lucidchart) a arquitetura clássica de uma webapp na AWS:

```
Usuário → Route 53 → CloudFront → ALB → ASG (EC2) → RDS Multi-AZ
                                              ↓
                                        S3 (uploads)
                                              ↓
                                        Lambda (processa)
                                              ↓
                                        SNS → SQS → Worker
```

> 💡 Esse diagrama é **a arquitetura referência** que cai em ~30% das questões de "qual combinação de serviços resolve o cenário X".

---

## ✅ Checklist de Limpeza (CRÍTICO)

Após terminar **delete na ordem**:

- [ ] **CloudFront** distribution (Desafio 1) — disable → wait → delete
- [ ] **RDS** instance (Desafio 7A) — **sem snapshot final**
- [ ] **EC2** instances de todos os desafios — Terminate
- [ ] **AMIs e snapshots** (Desafio 4) — Deregister AMI + Delete snapshots
- [ ] **CloudFormation stacks** (Desafio 6) — Delete (remove tudo junto)
- [ ] **SNS topics + SQS queues** (Desafios 1, 5) — Delete
- [ ] **Lambda functions + IAM roles** (Desafio 2) — Delete
- [ ] **DynamoDB tables** — Delete
- [ ] **S3 buckets** — Empty + Delete
- [ ] **VPC custom** (Desafio 3) — Delete (mantém a default)
- [ ] No dia seguinte: confira **Billing → Free Tier**

---

## Como entregar

Crie pasta `homework-modulo-3/` com:
- `desafio-1-cloudfront.png`
- `desafio-2-lambda.py` + `desafio-2-dynamodb.png`
- `desafio-3-network.png`
- `desafio-4-restore.png`
- `desafio-5-fanout.png`
- `desafio-6-template.yaml`
- `desafio-7-resposta.md`
- `simulado-respostas.md`
- `arquitetura-3tier.png` (bônus)

> 📚 **Ao terminar, você estará pronto para responder ~80% das questões de Tecnologia da prova CLF-C02.**

---

[← Voltar ao módulo](./README.md)
