# Glossário — Módulo 4

## Modelos de Preço

| Termo | Definição |
|-------|-----------|
| **On-Demand** | Pagamento por uso sem compromisso. |
| **Reserved Instance (RI)** | Compromisso de 1 ou 3 anos para desconto de até 72%. |
| **Savings Plan** | Compromisso flexível em $/hora (Compute SP cobre EC2 + Fargate + Lambda). |
| **Spot** | Instância com até 90% off, interruptível. |
| **Dedicated Host** | Servidor físico dedicado (BYOL com afinidade de socket/core). |
| **Dedicated Instance** | Hardware dedicado, sem visibilidade do host físico. |
| **Capacity Reservation** | Capacidade garantida em uma AZ (sem desconto, cobra On-Demand). |
| **Free Tier** | Uso gratuito AWS — 12 meses, Always Free, Trials. |
| **TCO** | Total Cost of Ownership — comparação on-prem vs nuvem. |

## Ferramentas de Custos

| Termo | Definição |
|-------|-----------|
| **Pricing Calculator** | Estimador oficial de custos AWS (gratuito). |
| **Cost Explorer** | Análise visual de custos, previsão 12 meses, recomenda SP/RI. |
| **Budgets** | Orçamentos e alertas; 2 grátis. |
| **CloudWatch Billing Alarm** | Alarme legado de billing — só funciona em **us-east-1**. |
| **CUR** | Cost and Usage Report — relatório detalhado (hora/recurso) em S3. |
| **Cost Allocation Tag** | Tag que aparece na fatura (AWS-generated ou User-defined). |
| **Cost Categories** | Agrupa custos por regras personalizadas. |
| **Cost Anomaly Detection** | ML detecta gastos anormais. |
| **Compute Optimizer** | Recomendações de rightsizing (EC2, EBS, Lambda, ASG). |
| **Billing Conductor** | Customiza fatura para BUs/resellers. |

## Organizations

| Termo | Definição |
|-------|-----------|
| **Consolidated Billing** | Fatura única para várias contas, com descontos agregados. Gratuito. |
| **Management Account** | Conta pagadora no Organizations (não é afetada por SCPs). |
| **Member Account** | Conta-membro da organização. |
| **OU** | Organizational Unit — agrupa contas em hierarquia. |
| **SCP** | Service Control Policy — guardrail que **restringe** (não concede) permissões. |
| **AWS Control Tower** | Landing zone multi-conta pronta sobre o Organizations. |

## Suporte

| Termo | Definição |
|-------|-----------|
| **TAM** | Technical Account Manager — técnico (Enterprise dedicado / On-Ramp em pool). |
| **Account Manager** | Contato comercial (não é TAM). |
| **Concierge** | Equipe de suporte para billing/account (Enterprise e On-Ramp). |
| **IEM** | Infrastructure Event Management — preparação para eventos de pico (incluso no On-Ramp/Enterprise). |
| **Trusted Advisor** | Verificador de boas práticas — **6 categorias**; Basic/Developer veem 7 core checks. |
| **AWS Well-Architected Tool** | Review gratuito da workload contra os 6 pilares. |
| **AWS Health Dashboard** | Service health (público) + Your account health (sua conta). |

## Recursos e Comunidade

| Termo | Definição |
|-------|-----------|
| **re:Post** | Comunidade oficial AWS (estilo Stack Overflow). Gratuito. |
| **Knowledge Center** | Base de artigos para problemas comuns. |
| **AWS Whitepapers** | Documentos técnicos oficiais (inclui Well-Architected Framework). |
| **Architecture Center** | Arquiteturas de referência por caso de uso. |
| **Prescriptive Guidance** | Guias passo-a-passo oficiais. |
| **Solutions Library** | Soluções prontas para implantar. |
| **APN** | AWS Partner Network — Consulting / Technology Partners; tiers Select/Advanced/Premier. |
| **AWS IQ** | Marketplace para contratar AWS Certified experts (freelancers). |
| **Professional Services** | Consultoria paga da AWS. |
| **AMS** | AWS Managed Services — AWS opera sua infra. |
| **Skill Builder** | Treinamento para indivíduos (grátis + pago). |
| **Educate** | Treinamento para estudantes 13+. |
| **Academy** | Currículo formal para instituições de ensino. |
| **Abuse Team** | abuse@amazonaws.com — reportar atividade maliciosa. |

---

[← Voltar ao módulo](./README.md)
