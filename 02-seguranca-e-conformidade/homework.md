# Homework — Módulo 2: Segurança e Conformidade

> 🎯 **Objetivo:** consolidar o aprendizado do módulo 2 com **desafios práticos** que simulam cenários reais de prova e do dia a dia. Diferente dos labs (passo a passo), aqui você decide **como resolver**.
>
> ⏱️ **Tempo estimado:** 3 a 5 horas, divididas como preferir.
>
> 💸 **Custo total estimado se feito conforme as instruções:** **US$ 0 a US$ 2** (a maior parte é Free Tier ou grátis sempre). Veja avisos em cada desafio.

---

## ⚠️ Antes de começar — Limites do Free Tier (12 meses)

| Serviço | Limite mensal grátis | Cuidado |
|---------|---------------------|---------|
| **EC2** t2.micro / t3.micro | 750 horas/mês | Termine ao final |
| **S3** | 5 GB storage + 20k GET + 2k PUT | Suficiente para labs |
| **KMS** | 20.000 requests | Chave custa US$ 1/mês |
| **CloudWatch** | 10 métricas + 5 GB logs | Geralmente não estoura |
| **CloudTrail** | 1 trail de Management events | Data events **cobram** |
| **GuardDuty** | 30 dias trial | DESLIGUE depois |
| **Config** | ❌ **Sem free tier** | US$ 0,003 por item |
| **Secrets Manager** | 30 dias trial | US$ 0,40/segredo/mês |
| **Macie** | 30 dias trial | Pode ser caro em datalake |
| **Inspector** | 15 dias trial | Pago por instância |

> 🛡️ **Regra de ouro:** ao final de cada desafio, **delete tudo que criou** ou siga o checklist de limpeza no final.

---

## Desafio 1 — IAM com Princípio do Menor Privilégio 🟢 grátis

**Cenário:** Sua empresa contratou um analista de dados júnior (`dev-junior`) que precisa apenas:
- Ler arquivos no bucket `learning-clf-data` (do Lab 2.4)
- Listar buckets S3
- **Não pode** deletar nada nem acessar outros serviços

### Tarefas
1. Crie o usuário IAM `dev-junior` (somente console, sem CLI key).
2. Crie uma **policy customizada** (não use a `AmazonS3ReadOnlyAccess`) que dê acesso apenas ao bucket `learning-clf-data`.
3. Anexe a policy ao usuário.
4. **Teste no IAM Policy Simulator:**
   - `s3:GetObject` no bucket → deve ser **allowed** ✅
   - `s3:DeleteObject` → deve ser **denied** ❌
   - `ec2:DescribeInstances` → **denied** ❌

### Entregáveis (anote ou tire print)
- JSON da policy criada
- Print do Policy Simulator com os 3 testes

> 💡 **Dica:** estude o JSON de policy no doc [aula 2.2 — IAM](./2.2-iam.md). Use `Effect`, `Action`, `Resource`.

---

## Desafio 2 — Criptografia em Camadas 🟡 ~US$ 1

**Cenário:** Você precisa armazenar uma senha de banco de dados de forma segura **e** criptografar um relatório financeiro com chave que **só sua empresa controla**.

### Tarefas
1. Crie uma **CMK no KMS** chamada `finance-cmk`.
2. Faça upload de um arquivo `relatorio-financeiro.txt` no S3 com **SSE-KMS** usando a `finance-cmk`.
3. Armazene a senha do banco em **Secrets Manager** (chave: `prod/db/password`) usando a `finance-cmk` como chave de criptografia.
4. Compare custos: faça o mesmo segredo no **Parameter Store SecureString** e calcule a economia mensal.

### Pergunta de raciocínio
> *"Por que usar KMS Customer Managed Key em vez da `aws/s3` padrão? Em qual cenário isso seria obrigatório?"*

### Entregáveis
- ARN da KMS key
- Print do objeto S3 mostrando a chave KMS
- Resposta da pergunta (3-5 linhas)

> 🟡 **Custo:** KMS = US$ 1/chave/mês. Secrets Manager = US$ 0,40/segredo/mês. **Schedule deletion da KMS (7 dias) e delete o secret ao terminar.**

---

## Desafio 3 — Defesa em Profundidade na Rede 🟡 grátis com t2.micro

**Cenário:** Subir uma aplicação web (nginx) e configurá-la para que **apenas** acesso HTTPS de IPs do Brasil cheguem nela.

### Tarefas
1. Suba uma EC2 t2.micro com nginx (use o User Data do Lab 2.7).
2. Configure o **Security Group** para liberar:
   - HTTP (80) de qualquer lugar (para teste)
   - SSH (22) **apenas** do seu IP (use `https://checkip.amazonaws.com`)
3. Configure a **NACL** da subnet para **bloquear** explicitamente o range `185.220.100.0/22` (range conhecido de Tor exit nodes — exemplo).
4. Documente: por que SG sozinho não bloqueia o range Tor, mas a NACL sim?

### Entregáveis
- Print das regras de SG e NACL
- Acesso `http://<public-ip>` funcionando
- Resposta sobre SG vs NACL

> 🟡 **Free Tier:** 750h/mês de t2.micro nos 12 primeiros meses. **Termine a EC2** ao final.

---

## Desafio 4 — Auditoria Forense 🟢 grátis

**Cenário:** Um bucket S3 da empresa foi deletado misteriosamente às 03h. Use os serviços de auditoria para reconstruir o que aconteceu.

### Tarefas
1. Garanta que o **CloudTrail** está ativo (Lab 2.8) com Management events.
2. Crie um bucket S3 chamado `vai-ser-deletado-<seu-nome>`.
3. Aguarde 5 min.
4. Delete o bucket.
5. Aguarde **15 minutos** para os logs do CloudTrail aparecerem.
6. No **Event history**, encontre:
   - Quem deletou (`User name`)
   - Quando (timestamp UTC)
   - De qual IP
   - Qual evento (`DeleteBucket`)

### Entregáveis
- Print do evento `DeleteBucket` com os 4 campos acima destacados
- Responda: *"Se o atacante tivesse desabilitado o CloudTrail antes de deletar, conseguiríamos saber? Como mitigar isso?"*

> 🟢 **Custo:** zero — Management events são grátis.

---

## Desafio 5 — Compliance Automatizada 🔴 ~US$ 0,50

**Cenário:** Sua empresa precisa garantir que **nenhum bucket S3 fique público** automaticamente.

### Tarefas
1. Ative o **AWS Config** (apenas para recurso `S3 Bucket` para limitar custo).
2. Adicione a regra gerenciada **`s3-bucket-public-read-prohibited`**.
3. Crie um bucket de teste e remova o "Block Public Access".
4. Aguarde alguns minutos. Veja o bucket marcado como **Non-compliant** no Config.
5. Recoloque o bloqueio. Veja voltar para **Compliant**.

### Pergunta de raciocínio
> *"Qual a diferença entre o Config detectar a violação e impedir a violação? Que serviço AWS impede de fato?"* (dica: SCP em Organizations).

### Entregáveis
- Print do Config mostrando o bucket Non-compliant → Compliant
- Resposta da pergunta

> 🔴 **Custo:** Config cobra ~US$ 0,003 por item gravado + US$ 0,001 por avaliação. Custo total do desafio: **menos de US$ 0,50 se desligar logo depois**. **Stop recording** ao terminar.

---

## Desafio 6 — Triagem de Alertas de Segurança 🟠 grátis no trial

**Cenário:** Você é o oncall de segurança. Aprenda a usar a stack de detecção da AWS.

### Tarefas
1. Ative **GuardDuty**, **Security Hub** e **Trusted Advisor** (já feito nos labs).
2. No **GuardDuty**, gere **sample findings** (Settings → Generate sample findings).
3. No **Security Hub**, observe que os findings do GuardDuty aparecem **agregados**.
4. No **Trusted Advisor**, identifique pelo menos **1 problema real** de segurança da sua conta (ex.: chave root sem MFA, SG com SSH aberto).
5. **Resolva** o problema.

### Pergunta de raciocínio
> *"Se o GuardDuty detecta um ataque, o Security Hub agrega, e o Trusted Advisor recomenda boas práticas — qual serviço você usaria para investigar **a causa raiz** do ataque com visualização gráfica?"*

### Entregáveis
- Print do Security Hub com findings do GuardDuty agregados
- Print do Trusted Advisor com check resolvido (de ❌ para ✅)
- Resposta da pergunta

> 🟠 **Trial 30 dias** do GuardDuty. **Disable** ao terminar.

---

## Desafio 7 — Simulado de Cenários (sem mexer no console)

Resolva sem consultar (depois confira com o gabarito no fim):

1. *"Empresa precisa de módulo criptográfico FIPS 140-2 Level 3."* → Qual serviço?
2. *"Detectar PII em arquivos parquet num bucket S3 do data lake."* → Qual serviço?
3. *"Bloquear ataque de SQL injection em uma API exposta via API Gateway."* → Qual serviço?
4. *"Identificar quem mudou um Security Group ontem às 14h."* → Qual serviço?
5. *"Saber como o Security Group estava configurado na semana passada."* → Qual serviço?
6. *"Centralizar gestão de WAF em 50 contas AWS via Organizations."* → Qual serviço?
7. *"Armazenar 200 endpoints de configuração da aplicação **gratuitamente**."* → Qual serviço?
8. *"Rotacionar a senha do RDS automaticamente a cada 30 dias."* → Qual serviço?
9. *"Baixar o relatório SOC 2 da AWS para entregar a um auditor."* → Qual serviço?
10. *"Investigar a cadeia de eventos após o GuardDuty alertar uma intrusão."* → Qual serviço?

<details>
<summary>🎯 Gabarito (clique para ver)</summary>

1. **CloudHSM** (FIPS L3 = sempre CloudHSM)
2. **Macie** (PII em S3)
3. **AWS WAF** (camada 7 / aplicação)
4. **CloudTrail** ("quem")
5. **AWS Config** ("como estava")
6. **AWS Firewall Manager**
7. **Parameter Store** (grátis, sem rotação)
8. **Secrets Manager** (rotação automática)
9. **AWS Artifact**
10. **Amazon Detective**

</details>

---

## Bônus (opcional) — Diagrama da sua arquitetura

Desenhe (Draw.io, Lucidchart, ou no caderno) a arquitetura que você construiu nos desafios:

- VPC com subnet pública
- EC2 com SG e NACL
- S3 + KMS
- CloudTrail enviando para S3
- Config monitorando o S3
- GuardDuty observando tudo

> 💡 Esse exercício consolida a **visão sistêmica** que cai no exame.

---

## ✅ Checklist de Limpeza (CRÍTICO)

Após terminar tudo, **delete na ordem** para evitar cobrança:

- [ ] **EC2 do Desafio 3** → Terminate
- [ ] **Bucket S3 do Desafio 4** (já deletado pelo desafio)
- [ ] **AWS Config** → Settings → Stop recording (Desafio 5)
- [ ] **GuardDuty** → Settings → Disable (Desafio 6)
- [ ] **Secret do Secrets Manager** → Schedule deletion 7 dias (Desafio 2)
- [ ] **KMS Customer Managed Key** → Schedule deletion 7-30 dias (Desafio 2)
- [ ] **Usuário IAM `dev-junior`** → Delete (Desafio 1, opcional)
- [ ] Verifique **Billing → Free Tier** no dia seguinte para confirmar que nada está cobrando

---

## Como entregar

Crie uma pasta `homework-modulo-2/` no seu computador com:
- `desafio-1-iam-policy.json`
- `desafio-1-policy-simulator.png`
- `desafio-2-resposta.md`
- `desafio-3-sg-nacl.png`
- `desafio-4-cloudtrail-event.png`
- `desafio-5-config.png`
- `desafio-6-securityhub.png`
- `simulado-respostas.md`
- `arquitetura.png` (opcional)

> 📚 **Ao terminar, você estará pronto para responder ~80% das questões de Segurança da prova CLF-C02.**

---

[← Voltar ao módulo](./README.md)
