# Flashcards — Módulo 3

---

**1. Qual a diferença entre Região, AZ e Edge Location?**
<details><summary>Ver resposta</summary>
- **Região** = localização geográfica (sa-east-1).
- **AZ** = data center isolado dentro da região (mínimo 3).
- **Edge Location** = PoP para CloudFront/Route 53 (400+ no mundo).
</details>

---

**2. EC2 Spot oferece até quanto de desconto e qual a contrapartida?**
<details><summary>Ver resposta</summary>
Até **90%** off. A instância pode ser interrompida com **aviso de 2 minutos** — só serve para workloads tolerantes a falha (batch, CI/CD, ML training).
</details>

---

**3. Qual a diferença entre Reserved Instances e Savings Plans?**
<details><summary>Ver resposta</summary>
- **RI**: compromisso por tipo de instância específica (1-3 anos, até 72% off).
- **Savings Plans**: compromisso de **$/h flexível** — cobre EC2, **Fargate e Lambda**.
</details>

---

**4. Quais os limites do Lambda?**
<details><summary>Ver resposta</summary>
- **15 min** de timeout
- 128 MB a 10 GB de memória (CPU proporcional)
- Pacote zip 50 MB / container 10 GB
- Free tier **para sempre**: 1M requisições + 400k GB-s/mês
</details>

---

**5. Diferença entre ECS, EKS e Fargate?**
<details><summary>Ver resposta</summary>
- **ECS**: orquestrador AWS nativo
- **EKS**: Kubernetes gerenciado
- **Fargate**: motor **serverless** para ECS/EKS (sem gerenciar servidor)
</details>

---

**6. S3 — durabilidade vs disponibilidade?**
<details><summary>Ver resposta</summary>
- **Durabilidade = 11 9's** (99,999999999%) — não perde o dado.
- **Disponibilidade = 99,99%** (Standard) — consegue acessar agora.
</details>

---

**7. Quando usar Glacier Deep Archive?**
<details><summary>Ver resposta</summary>
Arquivamento **legal/compliance 7+ anos**: armazenamento mais barato, recuperação em **12-48h**, mínimo **180 dias**.
</details>

---

**8. Qual o risco do S3 One Zone-IA?**
<details><summary>Ver resposta</summary>
Dados em **única AZ** — se a AZ for destruída fisicamente, **dado é perdido**. Use só para dados **recriáveis**. Disponibilidade 99,5%.
</details>

---

**9. Diferença entre EBS, EFS e FSx?**
<details><summary>Ver resposta</summary>
- **EBS**: bloco, **1 EC2**, **AZ-específico** (snapshots no S3).
- **EFS**: NFS, várias EC2 **Linux**, multi-AZ.
- **FSx**: Windows (SMB), Lustre (HPC), ONTAP, OpenZFS.
</details>

---

**10. Para migrar 100 PB para a AWS, qual serviço?**
<details><summary>Ver resposta</summary>
**Snowmobile** (caminhão). Snowcone = 8 TB, Snowball Edge = 80-210 TB.
</details>

---

**11. DataSync vs Snow Family?**
<details><summary>Ver resposta</summary>
- **DataSync** = transferência **online** contínua/incremental.
- **Snow** = transferência **offline** (caminhão/dispositivo físico).
</details>

---

**12. O que é AWS Backup?**
<details><summary>Ver resposta</summary>
Backup **centralizado** de EC2, EBS, RDS, DynamoDB, EFS, FSx em um único serviço.
</details>

---

**13. RDS Multi-AZ vs Read Replica?**
<details><summary>Ver resposta</summary>
- **Multi-AZ**: standby **síncrono** para **HA / failover** (não serve leitura).
- **Read Replica**: réplicas **assíncronas** para escalar **leitura**.
</details>

---

**14. Por que Aurora é mais rápido e quantas cópias mantém?**
<details><summary>Ver resposta</summary>
**5x MySQL / 3x PostgreSQL** com **6 cópias em 3 AZs** (auto-healing), até 128 TB, failover <30s. Storage distribuído + commit por quórum + réplicas leem o mesmo storage.
</details>

---

**15. DynamoDB: latência, tipo e cache?**
<details><summary>Ver resposta</summary>
NoSQL key-value **serverless**, latência **single-digit ms** (<10 ms), milhões de req/s, Global Tables multi-região, **DAX** = cache em microssegundos.
</details>

---

**16. OLTP vs OLAP — qual serviço?**
<details><summary>Ver resposta</summary>
- **OLTP** (transação, row, GB) → **RDS, Aurora, DynamoDB**
- **OLAP** (análise, colunar, TB/PB) → **Redshift, Athena**
</details>

---

**17. ElastiCache: Redis vs Memcached?**
<details><summary>Ver resposta</summary>
- **Redis**: persistência, multi-AZ, replicação, estruturas (listas, sets, hashes)
- **Memcached**: simples, só strings, sem persistência nem multi-AZ
</details>

---

**18. CloudFront vs Global Accelerator?**
<details><summary>Ver resposta</summary>
- **CloudFront**: HTTP/HTTPS com **cache**, CDN (sites, vídeo, API).
- **Global Accelerator**: **TCP/UDP**, sem cache, 2 IPs anycast (gaming, VoIP, IoT).
</details>

---

**19. VPC Endpoint Gateway vs Interface?**
<details><summary>Ver resposta</summary>
- **Gateway**: só **S3 e DynamoDB**, **grátis**.
- **Interface**: outros serviços, **pago** (por hora + GB).
</details>

---

**20. VPN vs Direct Connect?**
<details><summary>Ver resposta</summary>
- **VPN**: túnel IPsec pela internet, **setup em minutos**, barato.
- **Direct Connect**: fibra **dedicada**, **semanas** para provisionar, latência previsível.
</details>

---

**21. ALB vs NLB?**
<details><summary>Ver resposta</summary>
- **ALB** = camada **7** (HTTP/HTTPS), roteamento por URL/header.
- **NLB** = camada **4** (TCP/UDP), **IP estático**, performance extrema.
</details>

---

**22. Por que CloudWatch não mostra memória de EC2 por padrão?**
<details><summary>Ver resposta</summary>
Memória e disco vivem **dentro do SO** — é preciso instalar o **CloudWatch Agent** na instância.
</details>

---

**23. CloudFormation Drift Detection serve para quê?**
<details><summary>Ver resposta</summary>
Detectar **mudanças manuais** feitas no console que divergem do template (drift).
</details>

---

**24. Como replicar uma stack em várias contas/regiões?**
<details><summary>Ver resposta</summary>
**CloudFormation Stack Sets** (ideal com Organizations).
</details>

---

**25. CloudFormation vs CDK?**
<details><summary>Ver resposta</summary>
- **CloudFormation**: YAML/JSON, nativo, gratuito.
- **CDK**: código (TS/Python/Java) com loops/condicionais → **gera CloudFormation** por baixo.
</details>

---

**26. Como acessar EC2 sem abrir porta 22 nem ter chave SSH?**
<details><summary>Ver resposta</summary>
**Systems Manager Session Manager** — shell via console/CLI, sem SSH, com auditoria no CloudTrail.
</details>

---

**27. Qual serviço gratuito recomenda redimensionar EC2/EBS/Lambda?**
<details><summary>Ver resposta</summary>
**AWS Compute Optimizer** — usa ML para detectar over-provisioning.
</details>

---

**28. Service Health Dashboard vs Personal Health Dashboard?**
<details><summary>Ver resposta</summary>
- **Service Health**: status público de todos os serviços AWS.
- **Personal Health**: eventos que afetam **sua conta** especificamente (integra EventBridge).
</details>

---

**29. SNS vs SQS?**
<details><summary>Ver resposta</summary>
- **SNS**: **push** pub/sub — uma mensagem vai para vários subscribers ao mesmo tempo.
- **SQS**: **pull** (fila) — consumer busca quando quiser.
</details>

---

**30. SQS Standard vs FIFO?**
<details><summary>Ver resposta</summary>
- **Standard**: throughput quase ilimitado, **pode duplicar**, ordem não garantida.
- **FIFO**: 300 msg/s (3.000 com batch), **ordem garantida**, **exactly-once**.
</details>

---

**31. O que é DLQ?**
<details><summary>Ver resposta</summary>
**Dead Letter Queue** — fila secundária que armazena mensagens que falharam N vezes para investigação posterior.
</details>

---

**32. Qual a retenção máxima do SQS?**
<details><summary>Ver resposta</summary>
**14 dias** (padrão 4 dias). Mensagem até **256 KB**.
</details>

---

**33. Step Functions Standard vs Express?**
<details><summary>Ver resposta</summary>
- **Standard**: até **1 ano**, auditável (aprovações, contratos).
- **Express**: até **5 min**, alta frequência (IoT, streaming).
</details>

---

**34. Quando usar Amazon MQ em vez de SNS+SQS?**
<details><summary>Ver resposta</summary>
Quando há **sistema legado** com protocolos padrão (**AMQP, MQTT, STOMP, OpenWire**). App nova → SNS+SQS.
</details>

---

**35. EventBridge vs SNS?**
<details><summary>Ver resposta</summary>
**EventBridge** é o pub/sub evoluído: event bus com **pattern matching**, integração com **SaaS** (Salesforce, Datadog, Zendesk) e Schema Registry. SNS é pub/sub mais simples e rápido.
</details>

---

**36. Estratégias de deploy do CodeDeploy?**
<details><summary>Ver resposta</summary>
- **In-place**: substitui nas mesmas instâncias (com downtime)
- **Blue/Green**: ambiente novo paralelo, troca tráfego (rollback fácil)
- **Canary**: % pequena primeiro, depois resto
- **Linear**: incrementos iguais
- **All-at-once**: tudo de uma vez
</details>

---

**37. O que faz cada produto do CodeGuru?**
<details><summary>Ver resposta</summary>
- **Reviewer**: revisa código (Python/Java) com IA
- **Profiler**: análise de performance em produção (CPU, memória)
- **Security**: detecta vulnerabilidades no código
</details>

---

**38. Como testar Lambda localmente?**
<details><summary>Ver resposta</summary>
**SAM CLI** (Serverless Application Model) — emula Lambda + API Gateway localmente.
</details>

---

**39. O que é AWS X-Ray?**
<details><summary>Ver resposta</summary>
**Tracing distribuído** — mostra o caminho completo de uma requisição entre microsserviços, com **latência por etapa** e onde ocorreu o erro.
</details>

---

**40. Como ligar/desligar features em produção sem redeployar?**
<details><summary>Ver resposta</summary>
**AWS AppConfig** — feature flags, rollouts graduais, rollback instantâneo.
</details>

---

**41. O que é CloudShell?**
<details><summary>Ver resposta</summary>
Terminal **grátis no navegador**, pré-autenticado, com CLI/git/Python/Node instalados, 1 GB persistente por região.
</details>

---

**42. Athena, Redshift, Glue, EMR — qual a função de cada?**
<details><summary>Ver resposta</summary>
- **Athena**: SQL serverless no S3
- **Redshift**: data warehouse OLAP colunar
- **Glue**: ETL serverless + Data Catalog
- **EMR**: Hadoop/Spark/Hive gerenciado
</details>

---

**43. Os 4 sabores do Kinesis?**
<details><summary>Ver resposta</summary>
- **Data Streams**: ingestão real-time (você processa)
- **Firehose**: entrega gerenciada a S3/Redshift/OpenSearch
- **Data Analytics**: SQL em streams (Apache Flink)
- **Video Streams**: vídeo ao vivo
</details>

---

**44. Quando usar MSK em vez de Kinesis?**
<details><summary>Ver resposta</summary>
Quando a empresa **já usa Apache Kafka** (portabilidade multi-cloud, on-prem). Kinesis é proprietário AWS.
</details>

---

**45. Rekognition × Textract × Comprehend?**
<details><summary>Ver resposta</summary>
- **Rekognition**: imagem/vídeo (rostos, objetos)
- **Textract**: PDFs/imagens → texto + **tabelas + formulários**
- **Comprehend**: NLP (sentimento, entidades, idioma)
</details>

---

**46. Polly × Transcribe × Translate × Lex?**
<details><summary>Ver resposta</summary>
- **Polly**: texto → fala (TTS)
- **Transcribe**: fala → texto (STT)
- **Translate**: tradução
- **Lex**: chatbots (motor do Alexa)
</details>

---

**47. SageMaker vs Bedrock?**
<details><summary>Ver resposta</summary>
- **SageMaker**: plataforma para **treinar modelos próprios** (build, train, deploy).
- **Bedrock**: acesso a **foundation models** (Claude, Llama, Titan) via API, sem treinar.
</details>

---

**48. O que é Knowledge Bases do Bedrock?**
<details><summary>Ver resposta</summary>
**RAG gerenciado** — busca em seus documentos próprios para que o modelo responda com base neles (ex.: chatbot de manuais internos).
</details>

---

**49. Variantes do Amazon Q?**
<details><summary>Ver resposta</summary>
- **Q Developer**: autocomplete de código (substituiu CodeWhisperer)
- **Q Business**: busca em docs internos (Slack, SharePoint)
- **Q in QuickSight**: pergunta natural sobre dashboards
- **Q in Connect**: sugestões para atendentes
</details>

---

**50. SDK vs CLI?**
<details><summary>Ver resposta</summary>
- **SDK** (boto3, AWS SDK for X): chamar AWS **a partir do código**.
- **CLI**: comandos no **terminal** (`aws s3 ls`).
</details>

---

[← Voltar ao módulo](./README.md)
