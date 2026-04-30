# Flashcards — Módulo 4

---

**1. Qual modelo EC2 oferece até 90% de desconto mas pode ser interrompido?**
<details><summary>Ver resposta</summary>
**Spot Instances**. Bom para batch, big data, CI/CD e workloads tolerantes a falhas.
</details>

---

**2. Qual a diferença entre Reserved Instance e Savings Plan?**
<details><summary>Ver resposta</summary>
- **RI**: compromisso com tipo específico de instância.
- **Savings Plan**: compromisso em $/hora, mais flexível (Compute SP cobre EC2 + Fargate + Lambda).
- ⚠ Savings Plans **não cobrem RDS, DynamoDB, Redshift** — esses têm RI próprio.
</details>

---

**3. Qual ferramenta estima custos antes de provisionar?**
<details><summary>Ver resposta</summary>
**AWS Pricing Calculator** — gratuito, sem login obrigatório.
</details>

---

**4. Qual serviço envia alertas quando o custo ultrapassa um valor?**
<details><summary>Ver resposta</summary>
**AWS Budgets** (recomendado). Alternativa legada: **CloudWatch Billing Alarm** — só funciona em **us-east-1**.
</details>

---

**5. Qual plano de suporte tem TAM dedicado?**
<details><summary>Ver resposta</summary>
**Enterprise**. O **Enterprise On-Ramp** tem TAM em **pool**.
</details>

---

**6. A partir de qual plano o Trusted Advisor é completo (todos os checks)?**
<details><summary>Ver resposta</summary>
**Business**. Basic e Developer têm apenas **7 core checks** (Segurança e Limites de Serviço).
</details>

---

**7. Quantas categorias o Trusted Advisor tem?**
<details><summary>Ver resposta</summary>
**6 categorias**: Custo, Performance, Segurança, Tolerância a falhas, Limites de serviço e **Operational Excellence**.
</details>

---

**8. Qual é a comunidade oficial da AWS (estilo Stack Overflow)?**
<details><summary>Ver resposta</summary>
**AWS re:Post** — gratuito, substituiu o AWS Forums.
</details>

---

**9. Tráfego de entrada (ingress) na AWS é cobrado?**
<details><summary>Ver resposta</summary>
**Não**. Entrada é gratuita; saída para internet é cobrada. Transferência entre AZs ou entre Regiões também é cobrada.
</details>

---

**10. O que é Consolidated Billing?**
<details><summary>Ver resposta</summary>
Recurso do **Organizations** que unifica faturas de várias contas em uma só, com **descontos por volume agregado** e compartilhamento de RIs/SPs. Gratuito.
</details>

---

**11. Qual SLA de resposta para severidade crítica no Enterprise?**
<details><summary>Ver resposta</summary>
**Menos de 15 minutos** (mission-critical). Enterprise On-Ramp = **< 30 min** (business-critical).
</details>

---

**12. SCP concede ou restringe permissões?**
<details><summary>Ver resposta</summary>
**Restringe** — define o **máximo** de permissões. A permissão efetiva é a interseção entre IAM e SCP. **Não se aplica à management account.**
</details>

---

**13. Qual ferramenta provê uma landing zone multi-conta sobre o Organizations?**
<details><summary>Ver resposta</summary>
**AWS Control Tower** — provisiona ambiente multi-conta com guardrails (SCP + Config) e dashboard centralizado.
</details>

---

**14. Qual plano de suporte permite abrir caso técnico?**
<details><summary>Ver resposta</summary>
A partir do **Developer**. **Basic não permite** caso técnico — só billing/account.
</details>

---

**15. Qual ferramenta faz review gratuito da workload contra os 6 pilares do Well-Architected?**
<details><summary>Ver resposta</summary>
**AWS Well-Architected Tool** (no console, gratuita).
</details>

---

**16. Diferença entre AWS IQ, APN e Professional Services?**
<details><summary>Ver resposta</summary>
- **AWS IQ**: contratar **freelancers certificados** sob demanda (projetos curtos).
- **APN (AWS Partner Network)**: empresas parceiras (Consulting / Technology) com tiers Select/Advanced/Premier.
- **Professional Services**: consultoria **paga** da própria AWS para projetos estratégicos.
- **AMS**: AWS **opera** sua infra (patches, backup, monitoramento).
</details>

---

**17. Capacity Reservation dá desconto?**
<details><summary>Ver resposta</summary>
**Não.** Cobra preço **On-Demand** — só garante capacidade reservada em uma AZ.
</details>

---

**18. Quais são as duas visões do AWS Health Dashboard?**
<details><summary>Ver resposta</summary>
- **Service health** — status público dos serviços AWS.
- **Your account health** — eventos que afetam **sua conta** (era *Personal Health Dashboard*).
</details>

---

**19. Diferença entre Skill Builder, Educate e Academy?**
<details><summary>Ver resposta</summary>
- **Skill Builder**: indivíduos (cursos grátis + assinaturas pagas).
- **Educate**: estudantes 13+, autoatendimento.
- **Academy**: instituições de ensino (currículo formal).
</details>

---

**20. Qual ferramenta customiza fatura para diferentes BUs ou clientes finais (resellers)?**
<details><summary>Ver resposta</summary>
**AWS Billing Conductor**. Cria *billing groups* com pricing customizado — não muda o que a AWS cobra do payer, só como é repartido.
</details>

---

[← Voltar ao módulo](./README.md)
