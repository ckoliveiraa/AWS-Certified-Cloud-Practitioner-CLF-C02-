# Checklist de Revisão — Módulo 3

## 3.1 Infraestrutura Global
- [ ] Região × AZ × Edge Location (mínimo 3 AZs por região, 400+ Edges)
- [ ] Critérios de escolha de região: latência, conformidade, custo, serviços
- [ ] **Globais**: IAM, Route 53, CloudFront, WAF, Organizations
- [ ] **Regionais**: EC2, S3 (dados), RDS, Lambda
- [ ] Bucket S3 tem nome **globalmente único** mesmo sendo regional
- [ ] **Outposts** (AWS no DC do cliente), **Local Zones** (perto de cidades), **Wavelength** (5G)

## 3.2 Computação
- [ ] Famílias EC2: T/M (geral), C (compute), R/X (memória), I/D (storage), P/G (GPU)
- [ ] **Modelos de preço**: On-Demand, Reserved (até 72% off, 1-3 anos), **Savings Plans** (EC2+Fargate+Lambda), **Spot** (até 90% off, aviso 2 min), Capacity Reservation, Dedicated Host (BYOL), Dedicated Instance
- [ ] Spot **NÃO** para BD/web crítico; serve para batch/CI/ML training
- [ ] Auto Scaling: Launch Template, ASG, políticas (Target Tracking, Step, Scheduled)
- [ ] **Lambda**: timeout **15 min**, mem 128 MB-10 GB, zip 50 MB / container 10 GB
- [ ] Cold start → **Provisioned Concurrency**
- [ ] Free tier Lambda: 1M req + 400.000 GB-s/mês **para sempre**
- [ ] **ECS** (AWS nativo), **EKS** (Kubernetes), **Fargate** (sem servidor), **ECR** (registry)
- [ ] **Beanstalk** = PaaS gratuito (paga só recursos)
- [ ] **Lightsail** = VPS preço fixo; **Batch** = lote em larga escala

## 3.3 Armazenamento
- [ ] S3: **11 9's durabilidade**, **4 9's disponibilidade** (Standard)
- [ ] **Durabilidade ≠ Disponibilidade**
- [ ] Classes: Standard, Intelligent-Tiering (30d), Standard-IA (30d), One Zone-IA (1 AZ, 99,5%), Glacier Instant (90d), Glacier Flexible (90d, min-h), **Glacier Deep Archive (180d, 12-48h)**
- [ ] **One Zone-IA**: se a AZ cair, dado some — só recriável
- [ ] Versionamento: **só pode ser suspenso, nunca desativado**
- [ ] Lifecycle policies, CRR (cross-region), SRR (same-region)
- [ ] **EBS**: bloco, AZ-específico, 1 EC2; snapshots ficam no **S3**
- [ ] Tipos EBS: gp2/gp3 (SSD geral), io1/io2 (alto IOPS), st1 (HDD throughput), sc1 (HDD frio)
- [ ] **EFS**: NFS multi-AZ Linux; **FSx**: Windows/Lustre/ONTAP/OpenZFS
- [ ] Storage Gateway: **File** (NFS/SMB→S3), **Volume** (iSCSI), **Tape** (VTL→Glacier)
- [ ] Snow Family: **Snowcone 8 TB**, **Snowball Edge 80-210 TB**, **Snowmobile 100 PB**
- [ ] **DataSync = online** · **Snow = offline**
- [ ] **AWS Backup** = centraliza backup de EC2/EBS/RDS/DynamoDB/EFS/FSx

## 3.4 Bancos de Dados
- [ ] **OLTP × OLAP**: transação × análise; row × colunar
- [ ] **SQL × NoSQL**: schema rígido+ACID × flexível+escala horizontal
- [ ] RDS engines: MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Db2, Aurora
- [ ] **Multi-AZ = HA** (standby síncrono) × **Read Replica = performance leitura** (assíncrono)
- [ ] **Aurora**: 5x MySQL / 3x PostgreSQL, 6 cópias em 3 AZs, até 128 TB, 15 réplicas, failover <30s
- [ ] Aurora Serverless, Global Database, Backtrack
- [ ] **DynamoDB**: NoSQL serverless, latência <10ms, Global Tables, **DAX** (cache μs)
- [ ] **Redshift**: data warehouse OLAP colunar (PB), serverless disponível
- [ ] Outros NoSQL: **DocumentDB** (MongoDB), **Neptune** (grafo), **Timestream** (séries), **QLDB** (ledger), **Keyspaces** (Cassandra), **MemoryDB** (Redis durável)
- [ ] **ElastiCache**: Redis (persistência, multi-AZ, estruturas) × Memcached (simples)
- [ ] **DMS** + **SCT** (Schema Conversion Tool) para migração

## 3.5 Rede
- [ ] **VPC** (rede privada) + **Subnets** (pública/privada)
- [ ] **IGW** (entrada+saída) × **NAT Gateway** (só saída de subnet privada)
- [ ] CIDR: VPC = **/16** (~65k IPs) · Subnet = **/24** (~256)
- [ ] **VPC Peering** (2 VPCs, não transitivo) × **Transit Gateway** (hub) × **VPC Endpoints**
- [ ] Endpoints: **Gateway** (S3, DynamoDB, **grátis**) × **Interface** (outros, pago)
- [ ] **Route 53**: DNS + registrar + roteamento
- [ ] Políticas R53: Simple, Weighted, Latency, Failover, Geolocation, Multi-value
- [ ] **CloudFront** (HTTP/HTTPS, cache, 400+ Edges) × **Global Accelerator** (TCP/UDP, sem cache, 2 IPs anycast)
- [ ] **VPN** (internet, IPsec, minutos) × **Direct Connect** (fibra dedicada, semanas)
- [ ] ELB: **ALB** (L7 HTTP), **NLB** (L4 TCP/UDP, IP estático), **GLB** (L3 appliances)
- [ ] **API Gateway**: REST, HTTP, WebSocket; integra Lambda; throttling, cache, auth

## 3.6 Monitoramento e Gestão
- [ ] **CloudWatch Agent** necessário para **memória/disco** de EC2
- [ ] CloudWatch Logs Insights, Synthetics (canários), Container/Lambda Insights, Composite Alarms
- [ ] **Service Health Dashboard** (público) × **Personal Health Dashboard** (sua conta + EventBridge)
- [ ] **CloudFormation**: IaC JSON/YAML, gratuito, Stack, Change Set, **Stack Sets** (multi-conta/região), **Drift Detection**, rollback automático
- [ ] **CDK**: IaC em código (TS/Python/Java) → gera CloudFormation
- [ ] **Systems Manager**: Session Manager (sem SSH), Run Command, Patch Manager, Parameter Store, State Manager, Inventory
- [ ] **Compute Optimizer** (gratuito): identifica EC2/EBS/Lambda super-dimensionados
- [ ] **Service Catalog** (governança), **License Manager** (Oracle/SQL Server), **OpsWorks** (Chef/Puppet)
- [ ] Trusted Advisor full = **Business/Enterprise Support** (ver 2.6)

## 3.7 Integração e Mensageria
- [ ] Síncrono × Assíncrono (acoplamento forte × fraco)
- [ ] **SNS = push (pub/sub)** × **SQS = pull (fila)**
- [ ] SNS subscribers: SQS, Lambda, HTTP, Email, SMS, mobile push, Firehose; até 256 KB
- [ ] SQS **Standard** (alto throughput, at-least-once) × **FIFO** (300 msg/s, ordem, exactly-once)
- [ ] SQS: Visibility Timeout (30s default), **DLQ**, Long Polling, retenção 4d (máx **14d**), msg 256 KB
- [ ] **SNS + SQS Fan-Out** = 1 evento → várias filas
- [ ] **EventBridge** = event bus + pattern matching + integração SaaS + Schema Registry
- [ ] **Step Functions**: Standard (até 1 ano) × Express (até 5 min); estados Task/Choice/Parallel/Map/Wait
- [ ] **Amazon MQ** = ActiveMQ/RabbitMQ (legado AMQP/MQTT/STOMP)
- [ ] **AppFlow** = ETL sem código SaaS↔AWS

## 3.8 Ferramentas para Desenvolvedores
- [ ] CI × CD (Delivery) × CD (Deployment)
- [ ] **CodePipeline** orquestra · **CodeBuild** (serverless, paga/min) · **CodeDeploy** · **CodeArtifact** (npm/Maven/PyPI)
- [ ] CodeCommit/Cloud9/CodeStar **descontinuados**
- [ ] CodeDeploy estratégias: In-place, **Blue/Green** (rollback fácil), **Canary** (% pequena), **Linear** (incremental), All-at-once
- [ ] Configs prontas: LambdaCanary10Percent5/30Minutes, LambdaLinear10PercentEvery1/10Min, AllAtOnce/HalfAtATime/OneAtATime
- [ ] **CodeGuru** = 3 produtos: Reviewer (código), Profiler (performance), Security (vulns)
- [ ] **SAM**: CloudFormation simplificado serverless; **SAM CLI** teste Lambda local
- [ ] **X-Ray** = tracing distribuído (mapa de serviços, latência por etapa)
- [ ] **AppConfig** = feature flags sem redeploy
- [ ] **Q Developer** (substitui CodeWhisperer), **Q Business**, **Q in QuickSight/Connect**
- [ ] **CloudShell**: terminal grátis no navegador, 1 GB persistente, pré-autenticado
- [ ] **SDK** (boto3) × **CLI** (scripts)

## 3.9 Analytics & IA/ML
- [ ] Pipeline: Fontes → Kinesis/MSK → S3 (lake) → Glue/EMR → Redshift → Athena/QuickSight
- [ ] **Athena** = SQL serverless no S3 (paga TB escaneado)
- [ ] **Glue** = ETL serverless + Catalog (Crawler, Studio, **DataBrew** sem código)
- [ ] **EMR** = Hadoop/Spark/Hive/Presto/HBase gerenciado
- [ ] Kinesis 4 sabores: **Data Streams** (real-time), **Firehose** (entrega gerenciada), **Data Analytics** (SQL no stream), **Video Streams**
- [ ] **MSK** = Kafka gerenciado (empresa que já usa Kafka)
- [ ] **QuickSight** (BI, SPICE, Q natural language), **OpenSearch** (busca/logs), **Data Exchange** (marketplace)
- [ ] IA pronta: **Rekognition** (imagem), **Polly** (TTS), **Transcribe** (STT), **Translate**, **Comprehend** (sentimento), **Lex** (chatbot), **Textract** (PDFs/tabelas), **Personalize** (recomendação), **Forecast** (séries), **Kendra** (busca empresarial), **Fraud Detector**
- [ ] **SageMaker** = plataforma ML (Studio, Training, Endpoints, Canvas, JumpStart)
- [ ] **Bedrock** = IA generativa (Claude, Llama, Titan, Jurassic, Cohere, Stability)
- [ ] Bedrock features: Knowledge Bases (RAG), Agents, fine-tuning, privacidade

## Prática
- [ ] Simulado ≥ 80%
- [ ] Flashcards revisados
- [ ] Glossário dominado
- [ ] Laboratórios/homework concluídos

---

[← Voltar ao módulo](./README.md)
