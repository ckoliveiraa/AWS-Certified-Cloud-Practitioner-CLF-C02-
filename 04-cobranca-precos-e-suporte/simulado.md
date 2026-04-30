# Simulado — Módulo 4 (Cobrança, Preços e Suporte)

---

### 1. Qual modelo de preço é melhor para cargas tolerantes a falhas com máximo desconto?
- A) On-Demand
- B) Reserved
- C) Spot
- D) Dedicated Host

### 2. Qual plano de suporte inclui TAM dedicado?
- A) Developer
- B) Business
- C) Enterprise On-Ramp
- D) Enterprise

### 3. Qual serviço permite criar alertas de custo por email?
- A) Cost Explorer
- B) Budgets
- C) CUR
- D) Trusted Advisor

### 4. Tráfego de entrada de dados na AWS é:
- A) Sempre cobrado
- B) Gratuito
- C) Cobrado apenas em regiões fora dos EUA
- D) Cobrado após 1 TB

### 5. O que é Consolidated Billing?
- A) Fatura única para várias contas no Organizations
- B) Método de pagamento recorrente
- C) Relatório detalhado de custos
- D) Plano de suporte premium

### 6. Qual serviço fornece análise visual de custos com previsão de 12 meses?
- A) CUR
- B) Budgets
- C) Cost Explorer
- D) Pricing Calculator

### 7. Qual plano tem Trusted Advisor com todos os checks?
- A) Basic
- B) Developer
- C) Business
- D) Somente Enterprise

### 8. Qual serviço permite contratar freelancers AWS certificados?
- A) AWS Marketplace
- B) AWS IQ
- C) APN
- D) AMS

### 9. Qual relatório é o mais detalhado (por hora e recurso)?
- A) Cost Explorer
- B) Billing Dashboard
- C) Cost & Usage Report
- D) Trusted Advisor

### 10. Savings Plan pode ser aplicado a quais serviços?
- A) Apenas EC2
- B) EC2, Fargate e Lambda
- C) Apenas S3
- D) Todos os serviços AWS

### 11. Qual recurso do AWS Organizations permite **restringir** o que contas-membro podem fazer (sem conceder permissão)?
- A) IAM Policy
- B) Resource Policy
- C) Service Control Policy (SCP)
- D) Permission Boundary

### 12. Em qual Região deve-se criar um **CloudWatch Billing Alarm**?
- A) Qualquer Região
- B) us-east-1 (N. Virginia)
- C) us-west-2 (Oregon)
- D) Na mesma Região da conta

### 13. Quantas categorias o AWS Trusted Advisor possui atualmente?
- A) 4
- B) 5
- C) 6
- D) 7

### 14. Um cliente no plano **Basic** precisa abrir um caso técnico no Support Center. O que ele consegue?
- A) Pode abrir; resposta em 24h
- B) Pode abrir apenas casos de severidade baixa
- C) **Não pode abrir** caso técnico — só billing/account
- D) Pode abrir após pagar uma taxa

### 15. Qual serviço provê uma **landing zone multi-conta** pronta sobre o AWS Organizations?
- A) AWS Config
- B) AWS Control Tower
- C) AWS Service Catalog
- D) AWS Systems Manager

### 16. Sobre **Capacity Reservation** no EC2:
- A) Garante até 72% de desconto
- B) Garante capacidade reservada, mas cobra preço On-Demand
- C) É equivalente a Spot
- D) Substitui Reserved Instances

### 17. Qual ferramenta **gratuita** permite avaliar uma workload contra os 6 pilares do Well-Architected Framework?
- A) Trusted Advisor
- B) Compute Optimizer
- C) AWS Well-Architected Tool
- D) AWS Config

### 18. Qual o SLA de resposta para severidade **business-critical down** no plano **Enterprise On-Ramp**?
- A) < 15 minutos
- B) < 30 minutos
- C) < 1 hora
- D) < 4 horas

### 19. Uma empresa quer customizar a fatura mostrada para diferentes unidades de negócio internas. Qual serviço usar?
- A) Cost Categories
- B) Cost Allocation Tags
- C) AWS Billing Conductor
- D) Consolidated Billing

### 20. Qual a diferença entre **AWS Skill Builder** e **AWS Academy**?
- A) Skill Builder é pago; Academy é grátis
- B) Skill Builder é para indivíduos; Academy é para instituições de ensino
- C) São o mesmo produto com nomes diferentes
- D) Academy é só para certificados; Skill Builder não

### 21. Transferência de dados **entre AZs diferentes** na mesma Região é:
- A) Sempre gratuita
- B) Cobrada (em ambos os sentidos)
- C) Gratuita até 1 TB/mês
- D) Cobrada apenas se sair para a internet

### 22. Qual visão do **AWS Health Dashboard** mostra eventos que afetam **especificamente sua conta**?
- A) Service health
- B) Your account health
- C) Trusted Advisor
- D) Personal Cost Dashboard

---

## Gabarito

| # | Resposta | Justificativa |
|---|----------|---------------|
| 1 | **C** | Spot até 90% off, adequado para cargas tolerantes. |
| 2 | **D** | TAM dedicado só no Enterprise. |
| 3 | **B** | Budgets envia alertas. |
| 4 | **B** | Entrada é grátis. |
| 5 | **A** | Fatura única para contas Organizations. |
| 6 | **C** | Cost Explorer tem previsão 12 meses. |
| 7 | **C** | Business tem Trusted Advisor completo. |
| 8 | **B** | AWS IQ é marketplace de freelancers. |
| 9 | **C** | CUR é o mais granular. |
| 10 | **B** | Compute Savings Plan cobre EC2, Fargate e Lambda (não cobre RDS/DynamoDB). |
| 11 | **C** | SCP é guardrail do Organizations — restringe, não concede; não se aplica à management account. |
| 12 | **B** | A métrica EstimatedCharges é publicada apenas em us-east-1, então o alarme deve ser criado lá. |
| 13 | **C** | 6 categorias: Custo, Performance, Segurança, Tolerância a falhas, Limites e Operational Excellence. |
| 14 | **C** | Basic não permite caso técnico; só billing/account. Casos técnicos a partir do Developer. |
| 15 | **B** | AWS Control Tower provisiona ambiente multi-conta com guardrails (SCP + Config). |
| 16 | **B** | Capacity Reservation só garante capacidade — cobra On-Demand, sem desconto. |
| 17 | **C** | AWS Well-Architected Tool é gratuito no console e gera plano de melhoria. |
| 18 | **B** | Enterprise On-Ramp = < 30 min para business-critical; Enterprise = < 15 min para mission-critical. |
| 19 | **C** | Billing Conductor cria billing groups com pricing customizado para BUs/clientes. |
| 20 | **B** | Skill Builder = indivíduos; Educate = estudantes; Academy = instituições de ensino. |
| 21 | **B** | Tráfego entre AZs é cobrado nos dois sentidos. Mesma AZ via IP privado = grátis. |
| 22 | **B** | Your account health (era Personal Health Dashboard) mostra eventos da sua conta. |

---

[← Voltar ao módulo](./README.md)
