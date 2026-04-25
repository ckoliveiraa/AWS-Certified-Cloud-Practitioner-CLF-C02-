# Laboratórios — Módulo 2

> **Legenda de custo**
> 🟢 **Grátis sempre** &nbsp;|&nbsp; 🟡 **Free Tier** (limite mensal/12 meses) &nbsp;|&nbsp; 🟠 **Trial** (30 dias) &nbsp;|&nbsp; 🔴 **Cobra desde o 1º uso** (lembre de desligar)

---

## Lab 2.1 — Criar usuário admin e parar de usar a conta root 🟢

> Pratica a [aula 2.2 — IAM](./2.2-iam.md).
>
> **Boas práticas AWS**: a conta **root** deve ser usada **apenas** para tarefas que exigem o root (ex.: alterar plano de suporte, fechar conta). Para o dia a dia, crie um usuário IAM com permissões administrativas.

### Passo 1 — Criar grupo `Admins`
1. Faça login com a conta **root** (apenas desta vez).
2. Console → **IAM** → **User groups** → **Create group**.
3. Nome do grupo: `Admins`.
4. Em **Attach permissions policies**, selecione **`AdministratorAccess`**.
5. Clique em **Create group**.

### Passo 2 — Criar o usuário administrador
1. **IAM** → **Users** → **Create user**.
2. Nome: `admin-carlos`.
3. Marque **Provide user access to the AWS Management Console**.
4. Escolha **I want to create an IAM user**.
5. Defina senha forte.
6. Em **Permissions options**, escolha **Add user to group** → `Admins`.
7. **Salve** o link de login (`https://<account-id>.signin.aws.amazon.com/console`).

### Passo 3 — Habilitar MFA
1. **IAM** → **Users** → `admin-carlos` → **Security credentials** → **Assign MFA device**.
2. **Authenticator app** (Google Authenticator / Authy).

### Passo 4 — Sair do root
- Sign out da root, entre como `admin-carlos`. **Use sempre o admin** daqui para frente.

**Validação:** `admin-carlos` acessa todos os serviços; root + admin ambos com MFA ✅.

---

## Lab 2.2 — Testar permissões com IAM Policy Simulator 🟢

> Pratica a [aula 2.2 — IAM](./2.2-iam.md). Pratica o conceito de **least privilege** sem aplicar políticas reais.

1. Acesse **IAM** → **Policy simulator** ([policysim.aws.amazon.com](https://policysim.aws.amazon.com)).
2. Selecione o usuário `admin-carlos`.
3. Em **Service**, escolha `S3` → ações `GetObject` e `DeleteBucket`.
4. Clique **Run simulation** e veja `allowed`.
5. Crie um usuário de teste `dev-junior` sem políticas anexadas e simule novamente — todas as ações virão `denied`.

**Validação:** entender por que `dev-junior` não consegue nada (deny implícito) e `admin-carlos` consegue tudo (Allow explícito via grupo).

---

## Lab 2.3 — Criar Role para EC2 acessar S3 🟢

> Pratica a [aula 2.2 — IAM](./2.2-iam.md) (conceito de **Roles**).

1. **IAM** → **Roles** → **Create role**.
2. Trusted entity: **AWS service** → **EC2**.
3. Anexe `AmazonS3ReadOnlyAccess`.
4. Nome: `EC2-S3-ReadOnly`.

**Validação:** role aparece listada (será usada no Módulo 3 ao subir uma EC2).

---

## Lab 2.4 — Bucket S3 criptografado com SSE-S3 🟡

> Pratica a [aula 2.4 — Criptografia](./2.4-criptografia.md) (criptografia em repouso).

1. **S3** → **Create bucket** → nome único global (ex.: `learning-clf-<seu-nome>-<data>`).
2. **Block all public access** ✅ (deixe marcado).
3. **Default encryption** → **SSE-S3** (padrão).
4. **Bucket Versioning** → Enable.
5. Faça upload de um arquivo, edite localmente, faça upload de novo e veja **Show versions**.

**Validação:** vê duas versões do arquivo + cadeado de criptografia.

> 🟡 5 GB grátis/mês por 12 meses.

---

## Lab 2.5 — KMS Customer Managed Key + SSE-KMS 🟡

> Pratica o conceito de **chave gerenciada pelo cliente** (CMK) visto na [aula 2.4 — Criptografia](./2.4-criptografia.md).

1. **KMS** → **Customer managed keys** → **Create key**.
2. **Key type:** Symmetric. **Key usage:** Encrypt and decrypt.
3. Alias: `learning-clf-key`.
4. Key administrators: `admin-carlos`. Key users: `admin-carlos`.
5. **Finish**.
6. Volte ao bucket do Lab 2.4 → **Properties** → **Default encryption** → mude para **SSE-KMS** → escolha `learning-clf-key`.
7. Faça upload de um novo arquivo. Em **Properties** do objeto, veja **AWS-KMS** + ARN da sua chave.

**Validação:** o objeto agora exibe a chave **customer managed** em vez de `aws/s3`.

> 🟡 20.000 requests KMS grátis/mês para sempre. Chave custa **US$ 1/mês**. **Delete a chave (schedule deletion 7 dias)** ao terminar.

---

## Lab 2.6 — Secrets Manager vs Parameter Store 🟢🟠

> Pratica a [aula 2.4 — Criptografia](./2.4-criptografia.md) — comparação direta entre os dois.

### Parte A — Parameter Store (🟢 grátis)
1. **Systems Manager** → **Parameter Store** → **Create parameter**.
2. Nome: `/learning/db/host`. Tipo: **String**. Valor: `db.example.com`.
3. Crie outro: `/learning/db/password`. Tipo: **SecureString** (criptografa via KMS). Valor: `senha-fake-123`.

### Parte B — Secrets Manager (🟠 30 dias trial)
1. **Secrets Manager** → **Store a new secret**.
2. **Other type of secret** → key/value: `password = senha-fake-123`.
3. Nome: `learning/db-secret`. **Sem rotação** por enquanto.

### Comparação
- Liste o custo estimado em cada tela: Parameter Store = US$ 0; Secrets Manager = **US$ 0,40/segredo/mês** + chamadas.
- Recupere ambos via CLI:
  ```bash
  aws ssm get-parameter --name /learning/db/password --with-decryption
  aws secretsmanager get-secret-value --secret-id learning/db-secret
  ```

**Validação:** entender quando vale pagar Secrets Manager (rotação automática) vs usar Parameter Store grátis.

> 🔴 **Delete o secret do Secrets Manager** após o lab (Schedule deletion 7 dias).

---

## Lab 2.7 — Security Group vs NACL na prática 🟡

> Pratica a [aula 2.5 — Proteção de Rede](./2.5-protecao-rede.md). Use a VPC default para não criar custo extra.

1. **EC2** → **Launch instance** → **Name:** `learning-web-ec2` → AMI **Amazon Linux 2023** → tipo **t2.micro** ou **t3.micro** (Free Tier).
2. **Network settings:** VPC default, subnet pública, **Auto-assign public IP = Enable**.
3. Crie SG `learning-web-sg` permitindo **HTTP (80)** de `0.0.0.0/0`.
4. **User data** (instala nginx):
   ```bash
   #!/bin/bash
   dnf install -y nginx
   systemctl enable --now nginx
   echo "<h1>Lab 2.7</h1>" > /usr/share/nginx/html/index.html
   ```
5. Após 2 min, acesse `http://<public-ip>` no navegador → vê a página.

### Teste 1 — Stateful do SG
1. Edite o SG: remova a regra de HTTP. O navegador para de responder.
2. Recoloque a regra. Volta a funcionar **sem precisar adicionar regra de saída**. Isso prova o **stateful**.

### Teste 2 — Stateless da NACL
1. **VPC** → **Network ACLs** → NACL da subnet usada.
2. **Inbound rules:** adicione `Rule 100` Allow HTTP (80) de `0.0.0.0/0`. **Inbound default 200** Allow All ainda está ativo.
3. **Outbound rules:** **REMOVA** o `Allow All`. Acesse `http://<public-ip>` → **trava** (a resposta sai por porta efêmera bloqueada).
4. Adicione `Rule 100` Outbound Allow TCP `1024-65535` para `0.0.0.0/0`. Volta a funcionar.

**Validação:** você sentiu na pele a diferença entre stateful (SG) e stateless (NACL).

> 🔴 **Termine a EC2** ao final (`Instance state` → `Terminate`). 750h/mês grátis para t2/t3.micro nos 12 primeiros meses.

---

## Lab 2.8 — CloudTrail (Management Events) 🟢

> Pratica a [aula 2.7 — Auditoria](./2.7-auditoria-conformidade.md). Usa **só Management events** (grátis). **Data events em S3 cobram** desde o 1º evento.

1. **CloudTrail** → **Trails** → **Create trail**.
2. Nome: `trail-learning`.
3. Storage: bucket S3 criado (ou crie um novo).
4. **Log events:** apenas **Management events** (Read + Write). **NÃO marque Data events**.
5. Create.
6. Vá ao S3 e crie/delete um arquivo qualquer.
7. Aguarde ~15 min. **CloudTrail** → **Event history** → filtre por `Event name = PutObject` ou `DeleteObject`.

**Validação:** vê quem chamou cada API, com timestamp e IP de origem.

> 🟢 1 trail de management events é **grátis sempre**.

---

## Lab 2.9 — CloudWatch Logs + Alarm 🟡

> Pratica a [aula 2.7 — Auditoria](./2.7-auditoria-conformidade.md) — diferença entre log de aplicação (CloudWatch) e log de API (CloudTrail).

### Parte A — Criar Log Group e Log Stream
1. **CloudWatch** → **Log groups** → **Create log group** → nome `/learning/app` → **Create**.
2. Clique no nome `/learning/app` para entrar nele → **Create log stream** → nome `test-stream` → **Create**.

### Parte B — Inserir um log event (precisa de CLI)
> ⚠️ O console do CloudWatch **não permite** inserir log events manualmente — só leitura. Use **CloudShell** (ícone `>_` no topo do console, já autenticado) ou AWS CLI local:

```bash
aws logs put-log-events \
  --log-group-name /learning/app \
  --log-stream-name test-stream \
  --log-events timestamp=$(date +%s000),message="Erro fake na app"
```

> 💡 **Conta nova?** O CloudShell pode ficar indisponível por até 48h enquanto a AWS verifica a conta. Alternativas: instalar AWS CLI local (https://aws.amazon.com/cli/) ou pular essa parte e seguir para o alarme.

Volte ao log stream no console — a mensagem aparece listada.

### Parte C — Criar Alarme com SNS
1. **CloudWatch** → **Alarms** → **Create alarm** → **Select metric**.
2. Escolha **EC2** → **Per-Instance Metrics** → instância do Lab 2.7 → métrica **`CPUUtilization`**.
3. Threshold: **Static** → **Greater than 80**.
4. **Notification:** crie novo SNS topic `learning-alarms` → inscreva seu e-mail.
5. Confirme a inscrição no e-mail recebido (link "Confirm subscription").
6. Nome do alarme: `cpu-high-learning`.

**Validação:** força CPU na EC2 (via SSH/Session Manager rodando `stress --cpu 2 --timeout 300`) e veja o alarme passar para **In alarm** + e-mail chegando.

> 🟡 10 métricas customizadas e 5 GB de logs grátis/mês por 12 meses.

---

## Lab 2.10 — AWS Config (audita mudanças) 🔴

> Pratica a [aula 2.7 — Auditoria](./2.7-auditoria-conformidade.md). **Atenção:** Config cobra por item gravado.

1. **Config** → **Get started** → **1-click setup**.
2. Resources: marque apenas **S3 Bucket** e **Security Group** (limita custo).
3. Adicione regra gerenciada: `s3-bucket-public-read-prohibited`.
4. Vá ao bucket do Lab 2.4 e tire o bloqueio público (apenas para teste).
5. Volte ao Config → veja o bucket marcado como **Non-compliant**.
6. Recoloque o bloqueio → volta a **Compliant**.

**Validação:** entende compliance contínua e linha do tempo de configuração.

> 🔴 **Desligue o Config** ao terminar (Settings → Stop recording). Custo: US$ 0,003 por item gravado + US$ 0,001 por avaliação de regra.

---

## Lab 2.11 — GuardDuty (com aviso) 🟠

> Pratica a [aula 2.6 — Detecção e Resposta](./2.6-deteccao-resposta.md).

1. **GuardDuty** → **Get Started** → **Enable**.
2. Aguarde alguns minutos. Findings reais podem demorar dias.
3. Em **Settings** → **Sample findings** → **Generate sample findings** para ver o painel populado.

**Validação:** dashboard com findings de exemplo (Recon, Trojan, Behavior, etc.).

> 🟠 **30 dias grátis**. **DESABILITE** após o estudo (Settings → **Disable**), senão começa a cobrar por GB de logs analisados.

---

## Lab 2.12 — Trusted Advisor (checks grátis) 🟢

> Pratica a [aula 2.6 — Detecção e Resposta](./2.6-deteccao-resposta.md).

1. **Trusted Advisor** no console.
2. Veja os **6 checks gratuitos** (Basic Support):
   - MFA on Root
   - IAM Use
   - Security Groups – Specific Ports Unrestricted
   - Service Limits
   - S3 Bucket Permissions
   - EBS Public Snapshots
3. Resolva qualquer ❌ que aparecer (ex.: SG com SSH 0.0.0.0/0).

**Validação:** checks ✅ verdes para os 6 itens críticos.

> 🟢 Grátis sempre no Basic Support. Para os 5 pilares completos, precisa Business/Enterprise Support.

---

## Lab 2.13 — AWS Artifact (baixar relatório) 🟢

> Pratica a [aula 2.7 — Auditoria](./2.7-auditoria-conformidade.md).

1. **AWS Artifact** → **Reports**.
2. Filtre por **SOC 2** ou **ISO 27001**.
3. Aceite o NDA e baixe o PDF.

**Validação:** você tem em mãos o relatório de compliance para entregar a auditor/cliente.

> 🟢 100% grátis sempre.

---

## Checklist Final do Módulo 2

- [ ] Lab 2.1 — Usuário IAM admin + MFA + parou de usar root
- [ ] Lab 2.2 — Policy Simulator testado
- [ ] Lab 2.3 — Role EC2→S3 criada
- [ ] Lab 2.4 — Bucket S3 com SSE-S3 e versioning
- [ ] Lab 2.5 — Customer Managed Key e SSE-KMS
- [ ] Lab 2.6 — Parameter Store + Secrets Manager comparados
- [ ] Lab 2.7 — Stateful (SG) vs Stateless (NACL) na prática
- [ ] Lab 2.8 — CloudTrail capturando management events
- [ ] Lab 2.9 — CloudWatch Logs + Alarm com SNS
- [ ] Lab 2.10 — Config detectando bucket público
- [ ] Lab 2.11 — GuardDuty com sample findings
- [ ] Lab 2.12 — Trusted Advisor 6 checks grátis
- [ ] Lab 2.13 — Relatório SOC 2 baixado no Artifact

## Limpeza pós-laboratórios (importante!)

Para evitar custo inesperado, ao terminar:

- [ ] **Terminate** EC2 do Lab 2.7
- [ ] **Schedule deletion** da KMS key do Lab 2.5 (7 dias)
- [ ] **Delete** secret do Secrets Manager (Lab 2.6)
- [ ] **Stop recording** no AWS Config (Lab 2.10)
- [ ] **Disable** GuardDuty (Lab 2.11)
- [ ] **Delete** alarm e log group do CloudWatch se não for usar (Lab 2.9)

---

[← Voltar ao módulo](./README.md)
