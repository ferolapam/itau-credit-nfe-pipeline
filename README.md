<div align="center">

# 🟠 itau-credit-nfe-pipeline  
### Pipeline Serverless para Processamento de NFe, Crédito e Adiantamento  
Arquitetura AWS • Java • Python • DevOps • Datadog • FinOps

<br>

<!-- Tecnologias -->
![Java](https://img.shields.io/badge/Java-17-red?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge)
![AWS](https://img.shields.io/badge/AWS-Serverless-orange?style=for-the-badge)
![Terraform](https://img.shields.io/badge/Terraform-IaC-623CE4?style=for-the-badge)
![GitHubActions](https://img.shields.io/badge/GitHub-Actions-black?style=for-the-badge)

<br>

<!-- Arquitetura AWS -->
![Lambda](https://img.shields.io/badge/AWS-Lambda-FD8A00?style=for-the-badge)
![APIGateway](https://img.shields.io/badge/AWS-API%20Gateway-CC33FF?style=for-the-badge)
![DynamoDB](https://img.shields.io/badge/AWS-DynamoDB-4053D6?style=for-the-badge)
![RDS](https://img.shields.io/badge/AWS-RDS-527FFF?style=for-the-badge)
![SQS](https://img.shields.io/badge/AWS-SQS-FF9900?style=for-the-badge)
![CloudWatch](https://img.shields.io/badge/AWS-CloudWatch-232F3E?style=for-the-badge)

<br>

<!-- Domínio -->
![NFe](https://img.shields.io/badge/Domain-NFe-blueviolet?style=for-the-badge)
![Credito](https://img.shields.io/badge/Credito-Avaliacao%20e%20Limites-green?style=for-the-badge)
![Adiantamento](https://img.shields.io/badge/Financeiro-Adiantamento-important?style=for-the-badge)
![Custodia](https://img.shields.io/badge/Custodia-Servicos-lightgrey?style=for-the-badge)
![U2](https://img.shields.io/badge/Squad-U2-blue?style=for-the-badge)
![VH6](https://img.shields.io/badge/Squad-VH6-orange?style=for-the-badge)
![SN](https://img.shields.io/badge/Squad-SN-purple?style=for-the-badge)

<br>

<!-- Qualidade -->
![CleanCode](https://img.shields.io/badge/Clean%20Code-SOLID-critical?style=for-the-badge)
![DDD](https://img.shields.io/badge/DDD-Domain%20Driven%20Design-blueviolet?style=for-the-badge)
![Tests](https://img.shields.io/badge/Tests-PyTest%20%2F%20JUnit-lightblue?style=for-the-badge)

<br>

<!-- Observabilidade -->
![Datadog](https://img.shields.io/badge/Monitoring-Datadog-purple?style=for-the-badge)
![Logs](https://img.shields.io/badge/Logs-Estruturados-blue?style=for-the-badge)
![Tracing](https://img.shields.io/badge/Tracing-Distributed-orange?style=for-the-badge)
![Metrics](https://img.shields.io/badge/Metrics-Latency%20%7C%20Errors%20%7C%20Cost-yellowgreen?style=for-the-badge)

<br>

<!-- DevOps e FinOps -->
![CI/CD](https://img.shields.io/badge/DevOps-CI%2FCD-black?style=for-the-badge)
![IaC](https://img.shields.io/badge/IaC-Terraform-5F43E9?style=for-the-badge)
![FinOps](https://img.shields.io/badge/FinOps-Cost%20Optimization-brightgreen?style=for-the-badge)
![PayPerUse](https://img.shields.io/badge/Modelo-Pay%20Per%20Use-blue?style=for-the-badge)

<br>

<!-- Status -->
![Build](https://img.shields.io/badge/Build-Passing-brightgreen?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-red?style=for-the-badge)

<br><br>

</div>


# 🧩Sobre o Projeto

Este repositório apresenta um pipeline financeiro serverless baseado em AWS para validar Notas Fiscais Eletrônicas (NFe), executar regras de crédito e liberar adiantamento financeiro.

Desenhado seguindo práticas corporativas encontradas em squads como **U2, VH6 e SN** no Itaú — domínios de crédito, custódia e serviços — com alto foco em:

- Arquitetura escalável  
- Baixa latência  
- Observabilidade real-time (Datadog)  
- DevOps e automatização  
- Clean Code, SOLID e DDD  
- FinOps (custo por uso, rightsizing, métricas de custo x performance)

---

# ⚙️ 1. Arquitetura Serverless (AWS)

Fluxo técnico completo:

Fornecedor → API Gateway → Lambda 01 (Validação NF)  
→ DynamoDB (Persistência de status da NF)  
→ Lambda 02 (Regras de Crédito)  
→ RDS (Cadastro, limites e histórico)  
→ Lambda 03 (Adiantamento)  
→ SQS (Eventos assíncronos)  
→ Datadog (Logs, Métricas, Tracing)


### 🧱 Componentes

| Componente | Função |
|-----------|--------|
| **API Gateway** | Entrada dos eventos financeiros |
| **Lambdas** | Validação, crédito, adiantamento |
| **DynamoDB** | Persistência NoSQL e baixa latência |
| **RDS** | Dados relacionais e limites |
| **SQS** | Backpressure e comunicação assíncrona |
| **Datadog** | Observabilidade completa |
| **Terraform** | Infraestrutura como código |
| **GitHub Actions** | CI/CD |

---

# 🏦 2. Fluxo de Negócio — Crédito

### **2.1 Recebimento de Nota Fiscal**
- Recebe chave da NFe  
- Avalia emissor, valores e parcelas  
- Aciona Lambda de validação

---

### **2.2 Validação da NFe (Lambda 01)**
- Consulta SEFAZ  
- Verifica status (ativa / cancelada)  
- Registra logs estruturados  
- Salva no DynamoDB  

---

### **2.3 Regras de Crédito (Lambda 02)**
Avaliação baseada em:

- limite disponível  
- comportamento histórico  
- risco  
- valor total  
- parcelas  
- pagamentos futuros

---

### **2.4 Adiantamento (Lambda 03)**
- liberação parcial ou total  
- gravação em RDS  
- envio de evento para SQS  
- tracing + logs + métricas  

---

### **2.5 Observabilidade (Datadog)**
Dashboards incluem:

- latência das lambdas  
- erros  
- backlog da SQS  
- custo estimado  
- tracing ponta-a-ponta  

---

# 🔌 3. Endpoints

| Método | Rota | Descrição |
|--------|-------|-----------|
| **POST** | `/nfe/event` | Processa evento NF-e |
| **GET** | `/nfe/{chave}/status` | Consulta status da NFe |
| **POST** | `/credit/evaluate` | Avalia crédito |
| **POST** | `/credit/advance` | Solicita adiantamento |

---

# 📦 4. Exemplos de Payload

### 📘 4.1 Evento de Faturamento
```json
{
  "nfeKey": "35240512345678000123550010001234567890123456",
  "issuer": "Fornecedor X",
  "value": 55000.00,
  "installments": 3,
  "emissionDate": "2025-05-01",
  "paymentTerms": "parcelado"
}

### 📙 **4.2 Consulta de Status**
{
  "nfeKey": "35240512345678000123550010001234567890123456"
}

## 📗 **4.3 Avaliação de Crédito**
```json
{
  "customerId": "U2-001",
  "nfeKey": "35240512345678000123550010001234567890123456",
  "value": 55000.00,
  "installments": 3,
  "paymentDate": "2025-05-10"
}

## 📕 **4.4 Avaliação de Adiantamento**
```json
{
  "customerId": "U2-001",
  "nfeKey": "35240512345678000123550010001234567890123456",
  "requestedAmount": 30000.00,
  "advanceType": "parcial",
  "requestDate": "2025-05-02T10:21:00Z"
}

## 📙 **4.5 Resposta de Liberação (Output)**
```json
{
  "status": "approved",
  "approvedAmount": 30000.00,
  "limitRemaining": 25000.00,
  "operationId": "ADV-20250502-987654",
  "processedAt": "2025-05-02T10:21:03Z"
}

---

## 🟧 **5. Observabilidade e DevOps**

## 🟧 **5.1 Métricas (Datadog)**

- lambda.validation.latency

- lambda.credit.error_rate

- sqs.backlog

- rds.connection_pool_usage


## 🟧 **5.2 Logs Estruturados**

- trace_id

- etapa

- nfeKey

- customerId

- resultado das validações


## 🟧 **5.3 Tracing**

Acompanhamento completo:

API Gateway → Lambda 01 → DynamoDB → Lambda 02 → RDS → Lambda 03 → SQS.

## 🟧 **5.4 Alertas**

- Erro 500

- Latência alta

- Falhas na SEFAZ

- Fila SQS represada

- Falhas consecutivas no adiantamento

---

## 🟧 **6. Práticas de FinOps**

- Lambda sob demanda (pay-per-request)

- DynamoDB on-demand

- RDS com autoscaling

- Rightsizing periódico

- Métrica “custo por NFe processada”

- Otimização baseada em logs + métricas

- Menor latência possível = menor custo

---

## 🟧 **7. Práticas DevOps**

- Infraestrutura como código (Terraform)

- Pipelines GitHub Actions

- Testes unitários (PyTest/JUnit)

- Testes integrados

- Mock AWS

- Versionamento semântico

- Clean Code

- SOLID

- DDD

- 12-Factors

---

## 🟧 **8. Estrutura do Projeto**
backend/
  java/
  python/
  tests/

infra/
  terraform/
  lambdas/
  api-gateway/

docs/
  architecture/
    bpmn/
  runbook/
  specs/

---

## 🟧 **9. Roadmap**

 Arquitetura AWS (Draw.io)

 Sequence Diagram (Draw.io)

 Lambda 01 (Python)

 Lambda 02 (Java)

 Lambda 03 (Adiantamento)

 CI/CD com GitHub Actions

 Dashboards Datadog

 Runbook

 RFC (Tech Spec)

---

<div align="center">

## 🟧 **10. Autor**

### **Pamella Ferola – Engenharia de Software**  
Cloud • AWS • DevOps • Serverless • Crédito

São Paulo – Brasil  

</div>

