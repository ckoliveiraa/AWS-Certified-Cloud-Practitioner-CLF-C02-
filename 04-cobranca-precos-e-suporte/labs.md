# Laboratórios — Módulo 4

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
- [ ] Recursos limpos

---

[← Voltar ao módulo](./README.md)
