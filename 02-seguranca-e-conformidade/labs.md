# Laboratórios — Módulo 2

---

## Lab 2.1 — Criar usuário IAM e grupo

1. Console → **IAM** → **Users** → **Create user**.
2. Nome: `dev-carlos`. Habilite acesso ao console.
3. Criar grupo `Developers` com policy `PowerUserAccess`.
4. Adicione o usuário ao grupo.
5. Salve a senha inicial.

**Validação**: login incógnito com o novo usuário.

---

## Lab 2.2 — Criar uma Role para EC2 acessar S3

1. **IAM** → **Roles** → **Create role**.
2. Trusted entity: **AWS service** → **EC2**.
3. Anexe `AmazonS3ReadOnlyAccess`.
4. Nome: `EC2-S3-ReadOnly`.

**Validação**: role aparece listada. (Usaremos no Módulo 3.)

---

## Lab 2.3 — Criar um bucket S3 criptografado

1. **S3** → **Create bucket** → nome único global.
2. Habilite **Block all public access**.
3. Habilite **SSE-S3** (padrão).
4. Habilite **Versioning**.

**Validação**: upload de um arquivo e veja versões.

---

## Lab 2.4 — Ativar CloudTrail

1. **CloudTrail** → **Create trail** → nome `trail-learning`.
2. Entrega no bucket S3 criado.
3. Eventos: Management + Data events (S3).

**Validação**: após 15min, visualize eventos no console.

---

## Lab 2.5 — Ativar GuardDuty

1. **GuardDuty** → **Get Started** → **Enable**.
2. Aguarde análise (minutos).

**Validação**: dashboard acessível (findings podem não aparecer ainda).

---

## Checklist
- [ ] Usuário IAM + grupo criados
- [ ] Role EC2→S3
- [ ] Bucket S3 seguro
- [ ] CloudTrail ativo
- [ ] GuardDuty ativo

---

[← Voltar ao módulo](./README.md)
