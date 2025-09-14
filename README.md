# 📧 Agende de Classificação de Emails

## 📌 Objetivo

O **Jornada_Agente_Email** é um agente inteligente desenvolvido em
**n8n** para **automatizar o processamento de e-mails recebidos**.\
Ele classifica mensagens com IA, organiza no Gmail com rótulos
apropriados, armazena dados estruturados em planilhas, gera propostas
automaticamente e envia respostas personalizadas ou alertas de urgência.

------------------------------------------------------------------------
<img width="891" height="666" alt="image" src="https://github.com/user-attachments/assets/8cbf1c94-d728-45fd-99c1-c9d9018dd5c9" />
------------------------------------------------------------------------

## 🔄 Fluxo Geral

1.  **Captura** de novos e-mails não lidos.
2.  **Classificação automática** do conteúdo com IA (Google Gemini +
    Classificador de Texto).
3.  **Ação personalizada** para cada categoria:
    -   **Potencial Cliente** → Proposta inicial + registro em CRM.
    -   **Aluno da Jornada** → Resposta automática de suporte.
    -   **Spam** → Exclusão imediata.
    -   **Interno ou Importante** → Alerta via WhatsApp.
4.  **Execução adicional**:
    -   Rótulos no Gmail.
    -   Registro no Google Sheets.
    -   Geração de documentos no Google Docs.
    -   Envio de mensagens automáticas ou rascunhos.

------------------------------------------------------------------------

## 🧩 Principais Componentes

### 1. Gmail Trigger

-   Captura novos e-mails **não lidos** a cada minuto.
-   Extrai: **assunto, remetente, data, corpo**.

### 2. Classificação de Texto (IA)

-   Categorias:
    -   **Potencial Cliente** → orçamento, proposta, parceria, serviço.
    -   **Aluno da Jornada** → curso, acesso, pagamento, certificado.
    -   **Spam ou Irrelevante** → oferta, promoção, sorteio,
        unsubscribe.
    -   **Interno ou Importante** → urgente, falha, erro, sistema,
        alerta.
-   Modelo utilizado: **Google Gemini 2.5 Pro**.

### 3. Ações por Categoria

#### 📂 Potencial Cliente

-   Rótulo no Gmail + marcar como lido.\
-   Passa para **AI Agent**, que gera JSON estruturado com:
    -   Resumo técnico
    -   Escopo
    -   Estimativa de esforço
    -   Stack sugerida
    -   Perguntas para reunião
-   Registro no **Google Sheets (CRM)**.
-   Criação de **documento no Google Docs**.
-   Criação de **rascunho de e-mail de resposta automática**.

#### 🎓 Aluno da Jornada

-   Rótulo + marcar como lido.\
-   **AI Agent** gera resposta automática.\
-   Envio de **mensagem personalizada** pelo Gmail.

#### 🚫 Spam ou Irrelevante

-   Rótulo + marcar como lido.\
-   **Exclusão automática** do e-mail.

#### ⚠️ Interno ou Importante

-   Rótulo + marcar como lido.\
-   **AI Agent** analisa urgência.
-   Se urgente → resumo curto enviado via **WhatsApp API**.

------------------------------------------------------------------------

## 📊 Estrutura do JSON (AI Agent)

``` json
{
  "resumo": "Cliente deseja automatizar relatórios de vendas diários integrados ao ERP.",
  "escopo": "Coleta de dados via API, transformação com dbt e visualização no Looker Studio.",
  "estimativa_de_esforco": "Coleta: 5 dias, Transformação: 3 dias, Visualização: 2 dias.",
  "stack_sugerida": "Airbyte, dbt, BigQuery, Looker Studio",
  "nome": "João da Silva",
  "email": "joao@empresa.com",
  "data_de_recebimento": "2025-07-03T14:00:00Z",
  "motivo_do_contato": "Automação de relatórios de vendas",
  "escopo_resumido": "Pipeline automatizado com dashboard integrado.",
  "estimativa_resumida": "3 semanas",
  "riscos_resumidos": "Instabilidade da API, falta de documentação.",
  "perguntas_para_reuniao": "1. O ERP possui API documentada? 2. Há regras de limpeza dos dados? 3. Qual a ferramenta de visualização preferida?",
  "subject": "Sobre sua solicitação – Projeto de Dados",
  "mensagem_email": "Olá João da Silva, recebemos sua solicitação e já estamos avaliando..."
}
```

------------------------------------------------------------------------

## ⚙️ Integrações

-   **Gmail** → captura, rótulos, exclusões, respostas e rascunhos.\
-   **Google Sheets** → registro estruturado para CRM.\
-   **Google Docs** → criação de propostas automáticas.\
-   **WhatsApp API** → alertas imediatos para mensagens críticas.

------------------------------------------------------------------------

## ✅ Benefícios

-   **Automatização ponta a ponta** do ciclo de atendimento.\
-   **Respostas rápidas e personalizadas** para clientes e alunos.\
-   **Classificação inteligente** de e-mails com IA.\
-   **Integração direta com CRM e documentos**.\
-   **Alertas instantâneos** para casos críticos.
