# Laboratórios — Módulo 1

> Práticas de fixação. Custo: **Free Tier** (use conta nova ou t2/t3.micro).

---

## Lab 1.1 — Criar sua conta AWS

**Objetivo**: ter uma conta Free Tier funcional.

1. Acesse [aws.amazon.com/pt](https://aws.amazon.com/pt/) → **Criar conta AWS**.
2. Forneça email, senha e dados de cartão (necessário, mas Free Tier não cobra).
3. Verifique telefone.
4. Escolha **Basic Support (grátis)**.
5. Faça login como **root**.

**Validação**: o console abre em `https://console.aws.amazon.com`.

---

## Lab 1.2 — Ativar MFA no usuário root

1. Console → **IAM** → clique no nome da conta (topo direito) → **Security Credentials**.
2. Em **Multi-factor authentication (MFA)** → **Assign MFA device**.
3. Escolha **Authenticator app** → escaneie QR no Google Authenticator/Authy.
4. Digite 2 códigos consecutivos.

**Validação**: logout e login com MFA.

---

## Lab 1.3 — Explorar o Well-Architected Tool

1. Console → **AWS Well-Architected Tool**.
2. **Define workload** → nome fictício, região `sa-east-1`.
3. Responda o questionário de ao menos 1 pilar (ex.: **Segurança**).
4. Gere o **relatório**.

**Validação**: você vê os riscos identificados.

---

## Lab 1.4 — Usar o Pricing Calculator

1. Abra [calculator.aws](https://calculator.aws/#/).
2. Adicione uma instância **EC2 t3.micro** em `sa-east-1`.
3. Compare On-Demand vs 1-year Reserved.
4. Exporte a estimativa em PDF.

**Validação**: estimativa mensal gerada.

---

## Checklist
- [ ] Conta AWS criada
- [ ] MFA ativado
- [ ] Workload Well-Architected criado
- [ ] Estimativa Pricing Calculator gerada

---

[← Voltar ao módulo](./README.md)
