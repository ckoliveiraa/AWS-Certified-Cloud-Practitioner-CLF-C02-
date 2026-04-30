# Laboratórios — Módulo 4 *(Homework)*

> 📚 **Estes labs são homework** — execute por conta própria após estudar as aulas. São consultas a serviços de billing/suporte, em sua maioria sem custo, e reforçam os conceitos cobrados no CLF-C02. Faça no seu ritmo e marque o checklist no final.

---

## Lab 4.1 — Explorar o Billing Dashboard

1. Console → **Billing and Cost Management**.
2. Veja **Bills** do mês atual.
3. **Payment Methods** — confirme cartão.

**Validação**: você vê o total estimado do mês.

---

## Lab 4.2 — Criar um Budget de custo

1. **Budgets** → **Create budget** → **Cost budget**.
2. Valor: **US$ 5/mês**.
3. Alertas: 50%, 80%, 100% do valor → email.

**Validação**: email de confirmação de alertas.

---

## Lab 4.3 — Analisar com Cost Explorer

1. **Cost Explorer** → **Launch**.
2. Filtre por **Service** últimos 3 meses.
3. Gere **Forecast** para os próximos 3 meses.

**Validação**: gráfico exibido.

---

## Lab 4.4 — Aplicar Cost Allocation Tags

1. **EC2** → tagueie instância: `Project=Learning`, `Owner=Carlos`.
2. **Billing** → **Cost allocation tags** → ative as tags `Project` e `Owner`.

**Validação**: após 24h, tags aparecem como filtros no Cost Explorer.

---

## Lab 4.5 — Usar o Trusted Advisor

1. **Trusted Advisor** (na conta Basic).
2. Reveja os **7 checks grátis** (security groups abertos, MFA root, etc.).
3. Corrija achados relevantes.

**Validação**: MFA root marcado como OK (Lab 1.2).

---

## Lab 4.6 — Abrir um caso no re:Post

1. Acesse [repost.aws/pt](https://repost.aws/pt).
2. Faça login com sua conta AWS.
3. Faça uma pergunta real ou navegue por tags (ex.: `aws-free-tier`).

**Validação**: você tem perfil ativo.

---

## Lab 4.7 — Estimar TCO com Pricing Calculator

1. [calculator.aws](https://calculator.aws/#/).
2. Monte uma arquitetura: 2× EC2 t3.small + RDS + S3.
3. Compare **On-Demand vs 3-year Savings Plan**.
4. Exporte em PDF.

**Validação**: estimativa mensal e anual geradas.

---

## Lab 4.8 — CloudWatch Billing Alarm (us-east-1)

1. **Mude para us-east-1** (N. Virginia) — métrica `EstimatedCharges` só existe lá.
2. **CloudWatch** → **Alarms** → **Create alarm** → **Billing**.
3. Métrica: **Total Estimated Charge** (USD).
4. Condição: `Greater than US$ 5`.
5. Ação: notificação **SNS** → seu email (confirme a inscrição).

**Validação**: alarme em estado `OK` na console de us-east-1.

---

## Lab 4.9 — Cost Anomaly Detection

1. **Billing** → **Cost Anomaly Detection** → **Create monitor**.
2. Tipo: **AWS services** (monitora todos os serviços).
3. Crie um **subscription** com email e threshold (ex.: US$ 1).
4. Aguarde — alertas chegam quando o ML detectar gasto fora do padrão.

**Validação**: monitor ativo na lista.

---

## Lab 4.10 — Compute Optimizer (rightsizing)

1. **Compute Optimizer** → **Get started** → **Opt in**.
2. Aguarde ~12h após ter EC2/EBS rodando para gerar dados.
3. Veja recomendações em **EC2 instances**, **EBS volumes**, **Lambda functions**.
4. Identifique uma instância marcada como **Over-provisioned** (se houver).

**Validação**: dashboard com recomendações exibido (mesmo que vazio se não houver workload).

---

## Lab 4.11 — AWS Well-Architected Tool

1. **AWS Well-Architected Tool** → **Define workload**.
2. Nome: `lab-clf-c02`; região: `sa-east-1`.
3. Selecione o lens **AWS Well-Architected Framework**.
4. Responda às perguntas dos **6 pilares** (pode marcar "Question does not apply").
5. Veja o **Improvement plan** com riscos identificados (HRI/MRI).

**Validação**: workload criada e pelo menos 1 pilar respondido.

---

## Lab 4.12 — AWS Health Dashboard

1. Console → **AWS Health Dashboard** (canto superior direito → ícone de sino).
2. Aba **Service health** — veja status público dos serviços.
3. Aba **Your account health** — eventos que afetam **sua conta** (Open / Scheduled changes / Other notifications).
4. (Opcional) **EventBridge** → criar regra que dispara em eventos do Health.

**Validação**: ambas as abas acessadas.

---

## Limpeza Final (IMPORTANTE)

Ao concluir todos os labs, **remova recursos** para não ser cobrado:

- [ ] **Terminar EC2** (Lab 3.1)
- [ ] **Esvaziar e deletar buckets S3**
- [ ] **Deletar Lambda, DynamoDB, VPC customizada**
- [ ] **Desativar CloudTrail** se quiser (não gera custo significativo)
- [ ] **Desativar GuardDuty** após trial (custo após 30 dias)
- [ ] **Deletar NAT Gateway** se criado (cobrança por hora)

---

## Checklist
- [ ] Budget de US$ 5 criado
- [ ] Cost Explorer explorado
- [ ] Tags de alocação ativas
- [ ] Trusted Advisor revisado
- [ ] Perfil re:Post ativo
- [ ] Estimativa TCO salva
- [ ] Billing Alarm criado em us-east-1
- [ ] Cost Anomaly Detection ativo
- [ ] Compute Optimizer habilitado
- [ ] Workload no Well-Architected Tool criada
- [ ] Health Dashboard explorado
- [ ] Recursos limpos

---

[← Voltar ao módulo](./README.md)
