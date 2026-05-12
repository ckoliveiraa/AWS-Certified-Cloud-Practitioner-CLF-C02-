# Simulado — Módulo 1 (Conceitos de Nuvem)

> **20 questões** no estilo CLF-C02. Respostas e justificativas ao final.

---

### 1. Qual benefício da nuvem AWS permite trocar investimento inicial por custo sob demanda?
- A) Economias de escala
- B) Troca de despesa de capital por despesa variável
- C) Agilidade
- D) Globalização em minutos

### 2. Qual pilar do Well-Architected Framework foi adicionado mais recentemente?
- A) Segurança
- B) Confiabilidade
- C) Sustentabilidade
- D) Excelência Operacional

### 3. Uma empresa quer migrar um aplicativo legado sem modificá-lo. Qual estratégia usar?
- A) Refactor
- B) Repurchase
- C) Rehost
- D) Retire

### 4. O Amazon EC2 é um exemplo de qual modelo?
- A) SaaS
- B) PaaS
- C) IaaS
- D) FaaS

### 5. Qual característica descreve elasticidade?
- A) Pagar antecipadamente por 3 anos
- B) Escalar recursos para cima e para baixo automaticamente
- C) Replicar dados em várias regiões
- D) Criptografar dados em repouso

### 6. Qual perspectiva do CAF foca em habilidades e cultura?
- A) Plataforma
- B) Pessoas
- C) Governança
- D) Operações

### 7. Qual estratégia dos 6 Rs envolve substituir por uma solução SaaS?
- A) Replatform
- B) Refactor
- C) Repurchase
- D) Retain

### 8. Qual NÃO é um benefício da nuvem AWS segundo a própria AWS?
- A) Parar de adivinhar capacidade
- B) Eliminar completamente a responsabilidade de segurança
- C) Tornar-se global em minutos
- D) Economias de escala

### 9. Nuvem híbrida combina:
- A) Duas regiões AWS
- B) AWS + Azure
- C) Nuvem pública + infraestrutura on-premises
- D) Múltiplas contas AWS

### 10. Elastic Beanstalk é classificado como:
- A) IaaS
- B) PaaS
- C) SaaS
- D) DBaaS

### 11. Quantos pilares tem o Well-Architected Framework atualmente?
- A) 4
- B) 5
- C) 6
- D) 7

### 12. Uma empresa quer manter um sistema crítico em seu data center por restrição regulatória. Qual estratégia?
- A) Rehost
- B) Retire
- C) Retain
- D) Refactor

### 13. Qual serviço da AWS leva hardware AWS para o data center do cliente?
- A) Direct Connect
- B) Storage Gateway
- C) Outposts
- D) Snowball

### 14. Qual perspectiva do CAF é **técnica**?
- A) Pessoas
- B) Governança
- C) Negócio
- D) Plataforma

### 15. Qual pilar do WAF trata de minimizar impacto ambiental?
- A) Otimização de Custos
- B) Eficiência de Performance
- C) Sustentabilidade
- D) Excelência Operacional

### 16. Amazon WorkMail é exemplo de:
- A) IaaS
- B) PaaS
- C) SaaS
- D) FaaS

### 17. Qual serviço da AWS apoia migração automatizada de servidores (rehost)?
- A) AWS Migration Hub
- B) AWS Application Migration Service (MGN)
- C) AWS DataSync
- D) AWS Snowmobile

### 18. Qual a diferença entre Rehost e Replatform?
- A) Rehost é mais caro
- B) Replatform é lift-and-shift puro
- C) Rehost move sem alterações; Replatform aplica pequenas otimizações
- D) Não há diferença

### 19. Qual ferramenta da AWS avalia gratuitamente seus workloads contra os 6 pilares?
- A) Trusted Advisor
- B) Well-Architected Tool
- C) Cost Explorer
- D) Compute Optimizer

### 20. O que melhor descreve o modelo pay-as-you-go?
- A) Pagar antecipadamente por 3 anos com desconto
- B) Pagar uma assinatura mensal fixa
- C) Pagar apenas pelos recursos efetivamente consumidos
- D) Pagar somente quando exceder a cota gratuita

---

## Gabarito

| # | Resposta | Justificativa |
|---|----------|---------------|
| 1 | **B** | CapEx → OpEx é o primeiro benefício oficial da AWS. |
| 2 | **C** | Sustentabilidade foi adicionada em 2021 como 6º pilar. |
| 3 | **C** | Rehost = lift-and-shift, sem alterações. |
| 4 | **C** | EC2 fornece infraestrutura (VMs) = IaaS. |
| 5 | **B** | Elasticidade = escalar nas duas direções automaticamente. |
| 6 | **B** | Pessoas trata de cultura e habilidades (perspectiva de negócio). |
| 7 | **C** | Repurchase = drop-and-shop = trocar por SaaS. |
| 8 | **B** | Segurança é **responsabilidade compartilhada**, não eliminada. |
| 9 | **C** | Híbrida combina nuvem pública + on-premises/privada. |
| 10 | **B** | Beanstalk = PaaS (você só envia o código). |
| 11 | **C** | 6 pilares (Sustentabilidade adicionada em 2021). |
| 12 | **C** | Retain = manter on-prem por restrição. |
| 13 | **C** | Outposts leva hardware AWS para o DC do cliente. |
| 14 | **D** | Plataforma é perspectiva técnica (junto com Security e Operations). |
| 15 | **C** | Sustentabilidade foca em impacto ambiental. |
| 16 | **C** | WorkMail é SaaS (email gerenciado, consumo direto). |
| 17 | **B** | MGN automatiza rehost (sucessor do CloudEndure). |
| 18 | **C** | Rehost = sem alterações; Replatform = pequenas otimizações. |
| 19 | **B** | Well-Architected Tool é gratuita no console. |
| 20 | **C** | Pay-as-you-go = pagamento por consumo efetivo. |

---

[← Voltar ao módulo](./README.md)
