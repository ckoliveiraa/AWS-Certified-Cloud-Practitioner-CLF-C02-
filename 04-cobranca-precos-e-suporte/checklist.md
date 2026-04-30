# Checklist de Revisão — Módulo 4

## Modelos de Preço
- [ ] **3 princípios**: pay as you go / save when reserve / pay less by using more
- [ ] On-Demand, Reserved, Savings Plan, Spot, Dedicated Host, Dedicated Instance, Capacity Reservation
- [ ] Capacity Reservation **não dá desconto** (cobra On-Demand)
- [ ] RI: Standard vs Convertible; pagamentos (All/Partial/No Upfront)
- [ ] Savings Plans: Compute (EC2 + Fargate + Lambda) vs EC2 Instance
- [ ] Savings Plans **não cobrem** RDS / DynamoDB / ElastiCache / Redshift
- [ ] Free Tier: 12 meses, Always Free, Trials
- [ ] Pricing Calculator vs TCO
- [ ] Entrada = grátis; saída = cobrada
- [ ] Transferência: mesma AZ (grátis) vs entre AZs vs entre Regiões
- [ ] Preço varia por Região

## Ferramentas de Custos
- [ ] Billing & Cost Management
- [ ] Cost Explorer (visualização + previsão 12 meses + recomendações SP/RI)
- [ ] Budgets (alertas; 2 grátis)
- [ ] CloudWatch Billing Alarm (**só em us-east-1**)
- [ ] Cost & Usage Report (CUR — granular hora/recurso, em S3)
- [ ] Cost Allocation Tags (AWS-generated vs User-defined)
- [ ] Cost Categories (agrupar por regras)
- [ ] Cost Anomaly Detection (ML)
- [ ] Compute Optimizer (rightsizing)
- [ ] Trusted Advisor — pilar Cost Optimization
- [ ] Billing Conductor (resellers/BUs)
- [ ] Free Tier usage alerts

## Consolidated Billing & Organizations
- [ ] Parte do Organizations, gratuito
- [ ] Descontos por volume agregado
- [ ] Compartilhamento de RIs/SPs (pode desabilitar por conta)
- [ ] Management vs Member accounts
- [ ] Feature sets: All features vs Consolidated billing only
- [ ] OUs (Organizational Units)
- [ ] **SCPs** restringem (não concedem) permissões; não se aplicam à management account
- [ ] Sair da org exige conta standalone-ready
- [ ] **AWS Control Tower** = landing zone multi-conta sobre Organizations

## Planos de Suporte
- [ ] Basic (grátis) — **não permite caso técnico**
- [ ] Developer (US$ 29) — email, horário comercial
- [ ] Business (US$ 100) — Trusted Advisor completo, 24/7, SLA < 1h prod down
- [ ] Enterprise On-Ramp (US$ 5.500) — TAM em pool, SLA < 30 min, IEM incluso
- [ ] Enterprise (US$ 15.000) — TAM dedicado, SLA < 15 min, IEM incluso
- [ ] Concierge no On-Ramp e Enterprise
- [ ] SLAs por severidade memorizados

## Recursos de Suporte
- [ ] Support Center
- [ ] **Trusted Advisor — 6 categorias** (Custo, Performance, Segurança, Tolerância a falhas, Limites, Operational Excellence)
- [ ] **7 core checks** (Basic/Developer) — apenas em Segurança e Limites de Serviço
- [ ] **AWS Health Dashboard**: Service health (público) vs Your account health (sua conta)
- [ ] **AWS Well-Architected Tool** (review gratuito contra 6 pilares)
- [ ] re:Post, Knowledge Center
- [ ] Whitepapers, Architecture Center, Prescriptive Guidance, Solutions Library
- [ ] AWS IQ (freelancers certificados)
- [ ] APN — Consulting/Technology; tiers Select/Advanced/Premier
- [ ] Professional Services (consultoria paga)
- [ ] AMS (AWS opera sua infra)
- [ ] Skill Builder (indivíduos) vs Educate (estudantes) vs Academy (instituições)
- [ ] TAM (técnico) vs Account Manager (comercial)
- [ ] Abuse Team (abuse@amazonaws.com)

## Prática
- [ ] Simulado ≥ 80%
- [ ] Flashcards
- [ ] Glossário

---

[← Voltar ao módulo](./README.md)
