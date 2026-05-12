# Glossário — Módulo 3

## Infraestrutura Global

| Termo | Definição |
|-------|-----------|
| **Região** | Localização geográfica isolada com múltiplas AZs (ex.: sa-east-1). |
| **AZ** | Availability Zone — uma ou mais data centers isolados dentro de uma região. Mínimo 3 por região. |
| **Edge Location** | PoP da AWS para CloudFront e Route 53 (400+ no mundo). |
| **Regional Edge Cache** | Camada intermediária de cache entre origem e Edge Locations. |
| **Local Zone** | Extensão de região próxima a grandes centros urbanos. |
| **Wavelength Zone** | Infra AWS dentro de redes 5G de telecoms. |
| **Outposts** | Hardware AWS instalado no data center do cliente. |
| **PoP** | Point of Presence — inclui Edge Locations e Regional Edge Caches. |
| **Serviço global** | Sem região (IAM, Route 53, CloudFront, WAF, Organizations). |
| **Serviço regional** | Vive numa região específica (EC2, S3, RDS, Lambda). |

## Computação

| Termo | Definição |
|-------|-----------|
| **EC2** | Elastic Compute Cloud — VMs sob demanda. |
| **AMI** | Amazon Machine Image — template da instância. |
| **EC2 Image Builder** | Pipeline para criar AMIs. |
| **Família de instância** | T/M (geral), C (compute), R/X (memória), I/D (storage), P/G (GPU). |
| **On-Demand** | Pagamento por hora/segundo sem compromisso. |
| **Reserved Instance (RI)** | Compromisso 1-3 anos com até **72%** de desconto. |
| **Savings Plan** | Compromisso flexível de $/h — cobre EC2, **Fargate e Lambda**. |
| **Spot** | Instância com até **90%** de desconto; pode ser interrompida com aviso de 2 min. |
| **Capacity Reservation** | Reserva capacidade em uma AZ sem compromisso de tempo. |
| **Dedicated Host** | Servidor físico dedicado para BYOL (Oracle, SQL Server). |
| **Dedicated Instance** | Hardware dedicado sem visibilidade do host. |
| **Auto Scaling Group (ASG)** | Define min/max/desejado e distribui instâncias em AZs. |
| **Launch Template** | Configuração reutilizável para instâncias EC2. |
| **ELB** | Elastic Load Balancer — distribui tráfego. |
| **ALB / NLB / GLB** | Application (L7) / Network (L4) / Gateway (L3) Load Balancer. |
| **Lambda** | Função serverless; timeout 15 min; 128 MB-10 GB de memória. |
| **Provisioned Concurrency** | Pré-aquece Lambdas para eliminar cold start. |
| **ECS** | Elastic Container Service — orquestrador AWS nativo. |
| **EKS** | Elastic Kubernetes Service — Kubernetes gerenciado. |
| **Fargate** | Compute serverless para containers (ECS/EKS). |
| **ECR** | Elastic Container Registry — registry de imagens Docker. |
| **Elastic Beanstalk** | PaaS — envie o código, AWS provisiona infra. |
| **Lightsail** | VPS simplificado com preço fixo. |
| **AWS Batch** | Processamento em lote em larga escala. |

## Armazenamento

| Termo | Definição |
|-------|-----------|
| **S3** | Simple Storage Service — object storage. |
| **Bucket** | Container de objetos no S3 (nome globalmente único). |
| **Durabilidade** | Probabilidade de **não perder** o dado (11 9's no S3). |
| **Disponibilidade** | Probabilidade de **acessar agora** (99,99% no S3 Standard). |
| **S3 Standard** | Classe padrão, acesso frequente, imediato. |
| **S3 Intelligent-Tiering** | AWS move automaticamente entre tiers conforme acesso. |
| **S3 Standard-IA** | Pouco frequente, recuperação imediata. |
| **S3 One Zone-IA** | Pouco frequente em **única AZ** — risco se a AZ cair. |
| **Glacier Instant Retrieval** | Arquivo com recuperação em ms. |
| **Glacier Flexible Retrieval** | Arquivo com recuperação em min/horas. |
| **Glacier Deep Archive** | Arquivo mais barato; recuperação 12-48h; mínimo 180 dias. |
| **Versionamento S3** | Mantém versões antigas; uma vez ativado só pode ser **suspenso**. |
| **Lifecycle Policy** | Regras automáticas para mover/expirar objetos. |
| **CRR / SRR** | Cross-Region / Same-Region Replication. |
| **EBS** | Elastic Block Store — disco para EC2; AZ-específico. |
| **Tipos EBS** | gp2/gp3 (SSD geral), io1/io2 (alto IOPS), st1 (HDD throughput), sc1 (HDD frio). |
| **Snapshot** | Backup incremental de EBS armazenado no S3. |
| **EFS** | Elastic File System — NFS multi-AZ Linux. |
| **FSx** | Sistemas de arquivos para Windows (SMB), Lustre (HPC), NetApp ONTAP, OpenZFS. |
| **Storage Gateway** | Híbrido on-prem ↔ AWS: File Gateway, Volume Gateway, Tape Gateway. |
| **Snowcone / Snowball Edge / Snowmobile** | Migração offline: 8 TB / 80-210 TB / 100 PB. |
| **DataSync** | Transferência **online** incremental on-prem ↔ AWS. |
| **AWS Backup** | Backup centralizado de EC2, EBS, RDS, DynamoDB, EFS, FSx. |

## Bancos de Dados

| Termo | Definição |
|-------|-----------|
| **OLTP** | Online Transaction Processing — transações rápidas, row-oriented (RDS, Aurora, DynamoDB). |
| **OLAP** | Online Analytical Processing — análise, colunar (Redshift, Athena). |
| **SQL** | Relacional, schema rígido, ACID, escala vertical. |
| **NoSQL** | Não-relacional, schema flexível, escala horizontal. |
| **ACID** | Atomicity, Consistency, Isolation, Durability. |
| **RDS** | Relacional gerenciado — MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Db2, Aurora. |
| **Multi-AZ** | Standby síncrono em outra AZ — **HA + failover automático**. |
| **Read Replica** | Réplica assíncrona para escalar **leitura**. |
| **Aurora** | Banco relacional AWS — 5x MySQL / 3x PostgreSQL; 6 cópias em 3 AZs; até 128 TB. |
| **Aurora Serverless** | Aurora com auto-scale e cobrança por uso. |
| **Aurora Global Database** | Replicação multi-região com lag <1s. |
| **Backtrack** | "Volta no tempo" no Aurora sem restore. |
| **DynamoDB** | NoSQL key-value serverless; <10 ms; milhões de req/s. |
| **Global Tables** | DynamoDB multi-região ativo-ativo. |
| **DAX** | DynamoDB Accelerator — cache em microssegundos. |
| **Redshift** | Data warehouse OLAP colunar (PB-scale); Serverless disponível. |
| **DocumentDB** | NoSQL documento (compatível com MongoDB). |
| **Neptune** | Banco de grafos. |
| **Timestream** | Séries temporais (IoT, métricas). |
| **QLDB** | Quantum Ledger Database — ledger imutável. |
| **Keyspaces** | Wide-column compatível com Cassandra. |
| **MemoryDB for Redis** | In-memory com durabilidade. |
| **ElastiCache** | Cache gerenciado (Redis ou Memcached). |
| **DMS** | Database Migration Service. |
| **SCT** | Schema Conversion Tool — converte schemas entre engines. |

## Rede

| Termo | Definição |
|-------|-----------|
| **VPC** | Virtual Private Cloud — rede privada isolada. |
| **Subnet** | Subdivisão da VPC; pública ou privada. |
| **CIDR** | Notação de faixa de IPs (VPC=/16, subnet=/24). |
| **IGW** | Internet Gateway — entrada e saída para internet. |
| **NAT Gateway** | Permite que subnet privada acesse internet (só saída). |
| **Route Table** | Define para onde o tráfego é roteado. |
| **VPC Peering** | Conexão entre 2 VPCs; não transitivo. |
| **Transit Gateway** | Hub central para muitas VPCs/VPNs. |
| **VPC Endpoint** | Acesso a serviços AWS sem internet — Gateway (S3/DynamoDB, grátis) ou Interface (pago). |
| **Route 53** | DNS gerenciado + registro de domínios + roteamento. |
| **Políticas Route 53** | Simple, Weighted, Latency, Failover, Geolocation, Multi-value. |
| **CloudFront** | CDN global HTTP/HTTPS com cache. |
| **CDN** | Content Delivery Network. |
| **Lambda@Edge** | Código rodando em Edge Locations do CloudFront. |
| **Global Accelerator** | Aceleração TCP/UDP global com 2 IPs anycast (sem cache). |
| **Site-to-Site VPN** | Túnel IPsec pela internet (setup em minutos). |
| **Client VPN** | VPN para usuários finais (laptop). |
| **Direct Connect** | Fibra dedicada AWS ↔ on-prem (semanas para provisionar). |
| **API Gateway** | Cria APIs REST, HTTP e WebSocket; integra Lambda; auth, throttling, cache. |

## Monitoramento e Gestão

| Termo | Definição |
|-------|-----------|
| **CloudWatch Agent** | Coleta métricas internas (memória, disco) da EC2. |
| **CloudWatch Logs Insights** | Linguagem de query para logs. |
| **CloudWatch Synthetics** | Canários que testam URLs continuamente. |
| **Composite Alarm** | Combina vários alarmes (E/OU). |
| **Service Health Dashboard** | Status público de todos os serviços AWS. |
| **Personal Health Dashboard** | Eventos que afetam sua conta especificamente. |
| **IaC** | Infrastructure as Code. |
| **CloudFormation** | IaC nativa em JSON/YAML; gratuita. |
| **Stack** | Conjunto de recursos criados por um template. |
| **Change Set** | Preview de mudanças antes de aplicar. |
| **Stack Set** | Stack replicada em múltiplas contas/regiões. |
| **Drift Detection** | Detecta mudanças manuais fora do template. |
| **CDK** | Cloud Development Kit — IaC em código (TS/Python/Java) → gera CloudFormation. |
| **Systems Manager (SSM)** | Suíte para operar EC2 e on-prem em escala. |
| **Session Manager** | Shell em EC2 sem SSH/RDP. |
| **Run Command** | Executa comando em massa nas instâncias. |
| **Patch Manager** | Aplica patches em massa. |
| **State Manager** | Mantém configuração desejada (auto-corrige drift). |
| **OpsWorks** | Chef/Puppet gerenciado (em desuso). |
| **Service Catalog** | Catálogo de produtos pré-aprovados para self-service. |
| **License Manager** | Gerencia licenças (Oracle, SQL Server, SAP). |
| **Compute Optimizer** | Recomenda redimensionamento (gratuito). |

## Integração e Mensageria

| Termo | Definição |
|-------|-----------|
| **Síncrono** | Producer espera a resposta do consumer. |
| **Assíncrono** | Producer entrega mensagem e segue; consumer processa depois. |
| **SNS** | Simple Notification Service — pub/sub **push**. |
| **SQS** | Simple Queue Service — fila **pull**. |
| **SQS Standard** | Throughput ilimitado, ordem não garantida, at-least-once. |
| **SQS FIFO** | 300 msg/s (3k com batch), ordem, exactly-once. |
| **Visibility Timeout** | Tempo que mensagem fica invisível após ser lida (padrão 30s). |
| **DLQ** | Dead Letter Queue — fila para mensagens que falharam N vezes. |
| **Long Polling** | Consumer espera até mensagem chegar (mais barato). |
| **Fan-Out** | SNS publica em múltiplas filas SQS para consumers paralelos. |
| **EventBridge** | Event bus serverless com pattern matching + integração SaaS. |
| **EventBridge Pipes** | Source → enrichment → target sem código. |
| **EventBridge Scheduler** | Cron na nuvem (sucessor de CloudWatch Events Rules). |
| **Step Functions** | Orquestrador de workflows; Standard (1 ano) × Express (5 min). |
| **Amazon MQ** | ActiveMQ/RabbitMQ gerenciado (AMQP, MQTT, STOMP). |
| **AppFlow** | ETL sem código entre SaaS e AWS. |

## Ferramentas de Desenvolvedor

| Termo | Definição |
|-------|-----------|
| **CI** | Continuous Integration — build + testes automáticos. |
| **CD** | Continuous Delivery/Deployment — artefato pronto ou deploy automático. |
| **CodePipeline** | Orquestra pipeline CI/CD. |
| **CodeBuild** | Build e testes serverless. |
| **CodeDeploy** | Implanta em EC2, ECS, Lambda. |
| **CodeArtifact** | Repositório privado de pacotes (npm, Maven, PyPI). |
| **CodeCommit** | Git privado (descontinuado para novos clientes). |
| **CodeGuru Reviewer / Profiler / Security** | Revisão de código / performance / vulnerabilidades. |
| **Blue/Green** | Deploy paralelo com troca de tráfego. |
| **Canary** | Libera para % pequena antes do restante. |
| **Linear** | Incrementos iguais no rollout. |
| **SAM** | Serverless Application Model — CloudFormation simplificado para serverless. |
| **SAM CLI** | Testa Lambda localmente. |
| **X-Ray** | Tracing distribuído com mapa de serviços. |
| **AppConfig** | Feature flags sem redeploy. |
| **CodeWhisperer** | Autocomplete de código com IA (em transição para Q Developer). |
| **CloudShell** | Terminal AWS pré-autenticado no navegador (grátis, 1 GB persistente). |
| **AWS SDK** | Bibliotecas para chamar AWS no código (boto3 em Python). |
| **AWS CLI** | Comandos no terminal. |

## Analytics, IA e ML

| Termo | Definição |
|-------|-----------|
| **Data Lake** | Repositório de dados brutos (S3). |
| **Data Warehouse** | Banco analítico estruturado (Redshift). |
| **ETL** | Extract-Transform-Load. |
| **Athena** | SQL serverless sobre dados no S3. |
| **Glue** | ETL serverless + Data Catalog. |
| **Glue Crawler** | Descobre schema dos dados e popula o catálogo. |
| **Glue DataBrew** | ETL sem código para analistas. |
| **EMR** | Elastic MapReduce — Hadoop, Spark, Hive, Presto gerenciados. |
| **Kinesis Data Streams** | Ingestão de stream em tempo real. |
| **Kinesis Data Firehose** | Entrega gerenciada de stream para S3/Redshift/OpenSearch. |
| **Kinesis Data Analytics** | SQL sobre streams (Apache Flink). |
| **Kinesis Video Streams** | Streaming de vídeo ao vivo. |
| **MSK** | Managed Streaming for Apache Kafka. |
| **QuickSight** | BI com dashboards; SPICE = engine in-memory. |
| **QuickSight Q** | Pergunta em linguagem natural sobre dashboards. |
| **OpenSearch** | Busca e analytics (fork do Elasticsearch). |
| **AWS Data Exchange** | Marketplace de datasets de terceiros. |
| **Rekognition** | Visão computacional em imagens/vídeos. |
| **Polly** | Texto → fala (TTS). |
| **Transcribe** | Fala → texto (STT). |
| **Translate** | Tradução de idiomas. |
| **Comprehend** | NLP (sentimento, entidades, idioma). |
| **Comprehend Medical** | NLP médico (HIPAA). |
| **Lex** | Chatbots (motor do Alexa). |
| **Textract** | Extrai texto, **tabelas e formulários** de PDFs/imagens. |
| **Personalize** | Sistema de recomendação. |
| **Forecast** | Previsão de séries temporais. |
| **Kendra** | Busca empresarial inteligente em docs internos. |
| **Fraud Detector** | Detecção de fraude. |
| **SageMaker** | Plataforma ML end-to-end (build, train, deploy). |
| **SageMaker Studio** | IDE Jupyter gerenciada para ML. |
| **SageMaker Canvas / Autopilot** | AutoML sem código. |
| **JumpStart** | Marketplace de modelos pré-treinados. |
| **Bedrock** | API gerenciada de **foundation models** (Claude, Llama, Titan, Jurassic, Cohere, Stability). |
| **Knowledge Bases (Bedrock)** | RAG gerenciado — busca em docs próprios. |
| **Agents (Bedrock)** | Agentes que executam ações. |
| **Amazon Q Developer** | Autocomplete + chat de código (sucessor do CodeWhisperer). |
| **Amazon Q Business** | Q&A em docs/sistemas internos da empresa. |
| **RAG** | Retrieval-Augmented Generation — combina LLM com busca em base própria. |
| **Foundation Model** | Modelo generalista pré-treinado (LLM, imagem, etc.). |

---

[← Voltar ao módulo](./README.md)
