# Laboratórios — Módulo 2

---

## Lab 2.1 — Criar usuário admin e parar de usar a conta root

> **Boas práticas AWS**: a conta **root** deve ser usada **apenas** para tarefas que exigem o root (ex.: alterar plano de suporte, fechar conta). Para o dia a dia, crie um usuário IAM com permissões administrativas.

### Passo 1 — Criar grupo `Admins`
1. Faça login com a conta **root** (apenas desta vez).
2. Console → **IAM** → **User groups** → **Create group**.
3. Nome do grupo: `Admins`.
4. Em **Attach permissions policies**, selecione a policy gerenciada **`AdministratorAccess`**.
5. Clique em **Create group**.

### Passo 2 — Criar o usuário administrador
1. **IAM** → **Users** → **Create user**.
2. Nome: `admin-carlos`.
3. Marque **Provide user access to the AWS Management Console**.
4. Escolha **I want to create an IAM user**.
5. Defina uma senha forte (e marque "User must create a new password at next sign-in" se desejar).
6. Em **Permissions options**, escolha **Add user to group** e selecione o grupo **`Admins`**.
7. Revise e clique em **Create user**.
8. **Salve** o link de login da conta (ex.: `https://<account-id>.signin.aws.amazon.com/console`), o nome de usuário e a senha inicial.

### Passo 3 — Habilitar MFA no usuário admin (obrigatório)
1. **IAM** → **Users** → `admin-carlos` → aba **Security credentials**.
2. Em **Multi-factor authentication (MFA)** → **Assign MFA device**.
3. Escolha **Authenticator app** (Google Authenticator / Authy) e siga os passos.

### Passo 4 — Sair do root e passar a usar o admin
1. **Sign out** da conta root.
2. Acesse o link de login da conta e entre como `admin-carlos`.
3. A partir de agora, **use sempre o `admin-carlos`** para administrar a AWS.

**Validação**:
- `admin-carlos` consegue acessar todos os serviços (S3, EC2, IAM, etc.).
- Conta root e `admin-carlos` ambos com **MFA ativo** (✅ verde no painel do IAM).
- Você não precisa mais logar como root no dia a dia.

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
