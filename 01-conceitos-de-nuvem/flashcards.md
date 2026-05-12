# Flashcards — Módulo 1

> Formato: **Pergunta** → clique/revele a **Resposta**.

---

**1. Qual a definição oficial de computação em nuvem segundo a AWS?**
<details><summary>Ver resposta</summary>
Entrega **sob demanda** de poder computacional, banco de dados, armazenamento, aplicações e outros recursos de TI **via internet**, com precificação **pay-as-you-go**.
</details>

---

**2. Quais são as 5 características essenciais da nuvem?**
<details><summary>Ver resposta</summary>
1. Sob demanda
2. Autoatendimento (console, CLI ou API)
3. Elástico (escala automaticamente)
4. Medido (paga pelo que usa)
5. Amplo acesso (via internet)
</details>

---

**3. Diferença entre CapEx e OpEx?**
<details><summary>Ver resposta</summary>
- **CapEx** (Capital Expenditure): investimento inicial em ativos (servidores físicos).
- **OpEx** (Operational Expenditure): despesa variável conforme o consumo (pay-as-you-go).
</details>

---

**4. Diferença entre elasticidade e escalabilidade?**
<details><summary>Ver resposta</summary>
- **Elasticidade**: aumenta **e diminui** recursos automaticamente conforme a demanda.
- **Escalabilidade**: capacidade de crescer (vertical = máquina maior; horizontal = mais máquinas).
</details>

---

**5. Quais são os 6 benefícios da nuvem AWS (na ordem)?**
<details><summary>Ver resposta</summary>
1. Trocar CapEx por OpEx
2. Economias de escala massivas
3. Parar de adivinhar capacidade
4. Aumentar velocidade e agilidade
5. Parar de manter data centers
6. Tornar-se global em minutos
</details>

---

**6. Diferença entre "economias de escala" e "parar de adivinhar capacidade"?**
<details><summary>Ver resposta</summary>
- **Economias de escala**: AWS agrega uso de milhões de clientes → preços menores.
- **Parar de adivinhar capacidade**: você escala para cima/baixo sob demanda, sem superprovisionar.
</details>

---

**7. Qual a diferença entre IaaS, PaaS e SaaS?**
<details><summary>Ver resposta</summary>
- **IaaS**: você gerencia SO, runtime e aplicação (ex.: EC2)
- **PaaS**: você gerencia apenas o código e dados (ex.: Elastic Beanstalk, Lambda)
- **SaaS**: você apenas consome (ex.: WorkMail, Gmail)
</details>

---

**8. Classifique: EC2, Beanstalk, Lambda, WorkMail.**
<details><summary>Ver resposta</summary>
- **EC2** = IaaS
- **Beanstalk** = PaaS
- **Lambda** = PaaS (ou FaaS)
- **WorkMail** = SaaS
</details>

---

**9. Quais os 3 modelos de implantação?**
<details><summary>Ver resposta</summary>
- **Pública**: AWS, Azure, GCP
- **Privada**: infra dedicada (on-premises)
- **Híbrida**: combinação pública + privada/on-prem
</details>

---

**10. Quais serviços AWS para cenários híbridos?**
<details><summary>Ver resposta</summary>
- **AWS Outposts** — hardware AWS no seu DC
- **Storage Gateway** — storage on-prem ↔ S3/EBS/FSx
- **Direct Connect** — link de fibra dedicada
- **VMware Cloud on AWS** — VMware nativo na AWS
</details>

---

**11. Quais são os 6 pilares do Well-Architected Framework?**
<details><summary>Ver resposta</summary>
1. Excelência Operacional
2. Segurança
3. Confiabilidade
4. Eficiência de Performance
5. Otimização de Custos
6. **Sustentabilidade** (adicionado em 2021)
</details>

---

**12. Qual pilar do WAF foi adicionado mais recentemente?**
<details><summary>Ver resposta</summary>
**Sustentabilidade** — adicionado em **2021** como 6º pilar. Foca em minimizar impacto ambiental.
</details>

---

**13. O que é a AWS Well-Architected Tool?**
<details><summary>Ver resposta</summary>
Ferramenta **gratuita** no console que avalia seus workloads contra os 6 pilares do WAF.
</details>

---

**14. Quais são os 6 Rs da migração?**
<details><summary>Ver resposta</summary>
- **Rehost** (lift-and-shift)
- **Replatform** (lift-tinker-and-shift)
- **Repurchase** (drop-and-shop — trocar por SaaS)
- **Refactor / Re-architect** (reescrever para nuvem)
- **Retire** (descontinuar)
- **Retain** (manter on-premises)
</details>

---

**15. Qual a diferença entre Rehost e Replatform?**
<details><summary>Ver resposta</summary>
- **Rehost**: move sem alterações (lift-and-shift) — mais rápido.
- **Replatform**: pequenas otimizações sem mudar a arquitetura (ex.: migrar BD próprio para RDS).
</details>

---

**16. Qual estratégia substitui o sistema atual por um SaaS?**
<details><summary>Ver resposta</summary>
**Repurchase** (drop-and-shop). Ex.: substituir CRM próprio pelo Salesforce.
</details>

---

**17. Quais serviços AWS apoiam migração?**
<details><summary>Ver resposta</summary>
- **Migration Hub**: visibilidade central
- **Application Migration Service (MGN)**: rehost automatizado
- **DMS**: migração de bancos
- **SCT**: conversão de schemas entre engines
- **DataSync**: transferência online
- **Snow Family**: migração offline em massa
</details>

---

**18. Quais são as 6 perspectivas do AWS CAF?**
<details><summary>Ver resposta</summary>
**Negócio (3):** Business, People, Governance
**Técnicas (3):** Platform, Security, Operations
</details>

---

**19. Em qual grupo está a perspectiva "Pessoas" do CAF?**
<details><summary>Ver resposta</summary>
**Negócio** — trata de cultura, habilidades e gestão de mudança (não tecnologia).
</details>

---

**20. A perspectiva Security do CAF é a mesma coisa que o pilar Segurança do WAF?**
<details><summary>Ver resposta</summary>
**Não.** São conceitos distintos:
- **CAF Security**: perspectiva organizacional de governança de segurança.
- **WAF Security**: pilar arquitetural de boas práticas técnicas.
</details>

---

**21. O que significa pay-as-you-go?**
<details><summary>Ver resposta</summary>
Modelo de cobrança por **consumo** — você paga apenas pelos recursos que efetivamente usa, sem compromisso de longo prazo.
</details>

---

**22. O que é TCO?**
<details><summary>Ver resposta</summary>
**Total Cost of Ownership** — custo total de propriedade (inclui hardware, energia, espaço, pessoal, manutenção). Geralmente menor na nuvem do que on-premises.
</details>

---

[← Voltar ao módulo](./README.md)
