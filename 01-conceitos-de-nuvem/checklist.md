# Checklist de Revisão — Módulo 1

## 1.1 O que é Computação em Nuvem
- [ ] Sei definir computação em nuvem com minhas palavras
- [ ] **5 características essenciais**: sob demanda, autoatendimento, elástico, medido, amplo acesso
- [ ] Diferencio nuvem × on-premises (CapEx vs OpEx, semanas vs minutos)
- [ ] Sei que pay-as-you-go é habilitado pela **medição de uso**

## 1.2 Benefícios da Nuvem AWS
- [ ] Memorizei os **6 benefícios** na ordem oficial:
  1. Trocar CapEx por OpEx
  2. Economias de escala
  3. Parar de adivinhar capacidade
  4. Aumentar velocidade e agilidade
  5. Parar de manter data centers
  6. Tornar-se global em minutos
- [ ] Distingo "economias de escala" (#2) de "parar de adivinhar capacidade" (#3)
- [ ] "Global em minutos" se refere a **Regiões AWS** (não só AZs)
- [ ] Sei dar um exemplo prático de cada benefício

## 1.3 Modelos de Serviço
- [ ] Diferencio **IaaS, PaaS, SaaS** (pirâmide de responsabilidade)
- [ ] Classifico: **EC2 = IaaS**, **Beanstalk = PaaS**, **WorkMail = SaaS**, **Lambda = PaaS/FaaS**
- [ ] Quanto mais alto na pirâmide, **menos** responsabilidade operacional

## 1.4 Modelos de Implantação
- [ ] **Pública** (AWS, Azure, GCP) × **Privada** (on-prem dedicada) × **Híbrida** (combinação)
- [ ] Híbrida = pelo menos **pública + privada/on-prem**
- [ ] **Outposts** = resposta clássica para "AWS no meu DC"
- [ ] Sei serviços híbridos: Outposts, Storage Gateway, Direct Connect, VMware Cloud on AWS
- [ ] Pública ≠ inseguro — segurança é **responsabilidade compartilhada**

## 1.5 Well-Architected Framework
- [ ] Listo os **6 pilares**: Excelência Operacional, Segurança, Confiabilidade, Eficiência de Performance, Otimização de Custos, **Sustentabilidade**
- [ ] **Sustentabilidade** foi adicionada em **2021** (é a mais recente)
- [ ] Sei o foco de cada pilar
- [ ] Conheço a **Well-Architected Tool** (gratuita no console)

## 1.6 Estratégias de Migração (6 Rs)
- [ ] **Rehost** = lift-and-shift (mais rápido, sem alterações)
- [ ] **Replatform** = lift-tinker-and-shift (otimizações pequenas, ex.: usar RDS)
- [ ] **Repurchase** = drop-and-shop (substituir por **SaaS**)
- [ ] **Refactor** = re-arquitetar (maior benefício, maior custo)
- [ ] **Retire** = descontinuar
- [ ] **Retain** = manter on-prem (por ora)
- [ ] Conheço serviços de apoio: **Migration Hub, MGN, DMS, SCT, DataSync, Snow Family**

## 1.7 Cloud Adoption Framework (CAF)
- [ ] Listo as **6 perspectivas** (3 negócio + 3 técnicas):
  - Negócio: **Business, People, Governance**
  - Técnicas: **Platform, Security, Operations**
- [ ] **Pessoas** é perspectiva de **negócio** (cultura, habilidades)
- [ ] CAF (Security perspective) ≠ Pilar Segurança do WAF — são conceitos distintos
- [ ] Benefícios do CAF: reduzir risco, ESG, receita, eficiência operacional

## Prática
- [ ] Simulado ≥ 70% de acerto
- [ ] Flashcards revisados
- [ ] Glossário dominado

---

[← Voltar ao módulo](./README.md)
