# Glossário — Módulo 1

## Conceitos Fundamentais

| Termo | Definição |
|-------|-----------|
| **Computação em Nuvem** | Entrega sob demanda de recursos de TI via internet, com pay-as-you-go. |
| **On-Premises** | Infraestrutura própria, instalada no data center do cliente. |
| **Pay-as-you-go** | Cobrança por consumo efetivo, sem compromisso de longo prazo. |
| **CapEx** | *Capital Expenditure* — despesa de capital (compra de ativos). |
| **OpEx** | *Operational Expenditure* — despesa operacional (pagamento por uso). |
| **TCO** | *Total Cost of Ownership* — custo total de propriedade (HW + energia + pessoal + manutenção). |
| **Elasticidade** | Capacidade de aumentar **e diminuir** recursos automaticamente conforme a demanda. |
| **Escalabilidade** | Capacidade de crescer — vertical (máquina maior) ou horizontal (mais máquinas). |
| **Sob demanda** | Provisionamento imediato, sem intervenção humana. |
| **Autoatendimento** | Console, CLI ou API — usuário cria recursos sozinho. |
| **Alta Disponibilidade (HA)** | Sistema que continua funcionando mesmo com falhas (múltiplas AZs). |
| **Tolerância a Falhas** | Continuidade do serviço mesmo com falha de componentes. |
| **Agilidade** | Velocidade para experimentar, criar e descartar recursos. |

## Modelos de Serviço

| Termo | Definição |
|-------|-----------|
| **IaaS** | *Infrastructure as a Service* — você gerencia SO + app (ex.: EC2, EBS, VPC). |
| **PaaS** | *Platform as a Service* — você gerencia só o código (ex.: Beanstalk, Lambda, RDS). |
| **SaaS** | *Software as a Service* — software pronto, você só consome (ex.: WorkMail, Chime, Connect). |
| **FaaS** | *Function as a Service* — funções serverless orientadas a eventos (Lambda). |
| **Serverless** | Modelo onde o cliente não gerencia servidores (Lambda, Fargate, Aurora Serverless). |

## Modelos de Implantação

| Termo | Definição |
|-------|-----------|
| **Nuvem Pública** | Recursos compartilhados via internet (AWS, Azure, GCP). |
| **Nuvem Privada** | Infra dedicada a uma única organização (on-prem ou hospedada). |
| **Nuvem Híbrida** | Combinação de nuvem pública + on-premises/privada. |
| **Multi-cloud** | Uso de múltiplos provedores de nuvem (AWS + Azure, por exemplo). |
| **AWS Outposts** | Hardware AWS instalado no data center do cliente (cenário híbrido). |
| **Storage Gateway** | Integra storage on-prem com S3/EBS/FSx. |
| **Direct Connect** | Link de fibra dedicado on-prem ↔ AWS. |
| **VMware Cloud on AWS** | VMware nativo rodando em infraestrutura AWS. |

## Well-Architected Framework

| Termo | Definição |
|-------|-----------|
| **WAF (Framework)** | *Well-Architected Framework* — boas práticas em 6 pilares. ⚠️ Não confundir com **WAF (Web Application Firewall)**. |
| **Excelência Operacional** | Pilar 1 — automação, monitoramento, melhoria contínua. |
| **Segurança** | Pilar 2 — proteger dados, sistemas e ativos. |
| **Confiabilidade** | Pilar 3 — recuperar-se de falhas e atender demanda. |
| **Eficiência de Performance** | Pilar 4 — usar recursos de forma eficiente. |
| **Otimização de Custos** | Pilar 5 — entregar valor pelo menor preço. |
| **Sustentabilidade** | Pilar 6 — minimizar impacto ambiental (adicionado em **2021**). |
| **Well-Architected Tool** | Ferramenta gratuita no console que avalia workloads contra os 6 pilares. |

## Migração — 6 Rs

| Termo | Definição |
|-------|-----------|
| **Rehost** | "Lift-and-shift" — move sem alterar. |
| **Replatform** | "Lift-tinker-and-shift" — pequenas otimizações (ex.: BD próprio → RDS). |
| **Repurchase** | "Drop-and-shop" — substituir por SaaS (ex.: CRM próprio → Salesforce). |
| **Refactor / Re-architect** | Reescrever para arquitetura cloud-native (microsserviços, serverless). |
| **Retire** | Descontinuar workloads sem uso. |
| **Retain** | Manter on-prem por enquanto (restrição regulatória, custo, etc.). |
| **Migration Hub** | Visibilidade central da migração. |
| **MGN** | *Application Migration Service* — rehost automatizado (sucessor do CloudEndure). |
| **DMS** | *Database Migration Service* — migra bancos homogêneos e heterogêneos. |
| **SCT** | *Schema Conversion Tool* — converte schema entre engines (Oracle → PostgreSQL). |
| **DataSync** | Transferência online incremental on-prem ↔ AWS. |
| **Snow Family** | Migração offline (Snowcone 8 TB, Snowball Edge 80-210 TB, Snowmobile 100 PB). |

## Cloud Adoption Framework (CAF)

| Termo | Definição |
|-------|-----------|
| **AWS CAF** | *Cloud Adoption Framework* — guia em 6 perspectivas (3 negócio + 3 técnicas). |
| **Business (perspectiva)** | Alinhar TI a resultados de negócio. |
| **People (perspectiva)** | Cultura, habilidades, gestão de mudança. |
| **Governance (perspectiva)** | Gerenciar iniciativas e riscos. |
| **Platform (perspectiva)** | Arquitetar, construir e operar workloads. |
| **Security (perspectiva)** | Confidencialidade, integridade, disponibilidade (≠ pilar de Segurança do WAF). |
| **Operations (perspectiva)** | Entregar serviços conforme esperado. |
| **ESG** | *Environmental, Social, Governance* — métricas de sustentabilidade corporativa. |

---

[← Voltar ao módulo](./README.md)
