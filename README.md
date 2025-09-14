# 📧 Agende de Classificação de Emails

## 📌 Objetivo

O **Jornada_Agente_Email** é um agente inteligente construído em **n8n**
para **automatizar a triagem, classificação e resposta de e-mails
recebidos**.\
Ele aplica **IA (Google Gemini)** para categorizar mensagens, direcionar
fluxos diferentes para vendas, suporte e TI, além de criar registros no
CRM, propostas em Google Docs e alertas via WhatsApp.

<img width="974" height="667" alt="image" src="https://github.com/user-attachments/assets/ff9a77a7-30f1-4736-813b-e2da94b0f042" />


------------------------------------------------------------------------

## 🔄 Fluxo Geral

1.  **Captura de e-mails não lidos** no Gmail.\
2.  **Classificação automática** com IA (Text Classifier + Gemini).\
3.  **Encaminhamento para o fluxo correspondente**:
    -   **Pré-vendas (Potencial Cliente)**\
    -   **Suporte (Aluno da Jornada)**\
    -   **Exclusão automática (Spam)**\
    -   **TI/Operações (E-mails Internos ou Urgentes)**\
4.  **Ações adicionais**:
    -   Aplicação de rótulos no Gmail.\
    -   Registro no **Google Sheets** (CRM).\
    -   Criação e atualização de documentos no **Google Docs**.\
    -   Integração com **Trello** (cards no funil de vendas e suporte).\
    -   Envio de notificações via **WhatsApp API**.

------------------------------------------------------------------------

## 🧩 Principais Componentes

### 1. Gmail Trigger

-   Captura novos e-mails **não lidos** a cada minuto.\
-   Extrai: **assunto, remetente, data, corpo**.

### 2. Text Classifier (IA)

Classifica as mensagens em quatro categorias:

-   **Potencial Cliente** → propostas, orçamento, parcerias, serviços.\
-   **Aluno da Jornada** → dúvidas sobre curso, acesso, certificado,
    pagamento.\
-   **Spam ou Irrelevante** → promoções, sorteios, mensagens
    automáticas.\
-   **E-mail Interno ou Importante** → falhas, erros, alertas,
    urgências.

------------------------------------------------------------------------

## 📂 Fluxos por Categoria

### 🔹 Pré-vendas (Time Comercial)

-   Rótulo no Gmail + marcar como lido.\
-   **AI Agent 3** analisa a demanda técnica e gera JSON estruturado
    com:
    -   resumo técnico, escopo, estimativa de esforço, stack sugerida.\
    -   dados do solicitante (nome, e-mail, data).\
    -   perguntas-chave para a reunião.\
-   Registros salvos no **Google Sheets** (CRM).\
-   Criação de **documento no Google Docs** com a proposta.\
-   Anexos e cards no **Trello -- Funil de Vendas**.\
-   Notificação via **WhatsApp API** para equipe comercial.

👉 **Responsável:** **Time de Vendas**

------------------------------------------------------------------------

### 🔹 Alunos da Jornada (Time de Suporte)

-   Rótulo no Gmail + marcar como lido.\
-   **AI Agent 1** gera resposta automática personalizada.\
-   Envio imediato de **resposta ao aluno** via Gmail.\
-   Registro no **Trello -- Suporte de TI** para acompanhamento.

👉 **Responsável:** **Time de Suporte de TI**

------------------------------------------------------------------------

### 🔹 Spam ou Irrelevante

-   Rótulo no Gmail + marcar como lido.\
-   Exclusão automática do e-mail.

👉 **Responsável:** **Fluxo automático (sem intervenção humana)**

------------------------------------------------------------------------

### 🔹 E-mails Internos ou Urgentes

-   Rótulo no Gmail + marcar como lido.\
-   **AI Agent 2** analisa a urgência:
    -   URGENTE → envia resumo curto via **WhatsApp API**.\
    -   NÃO URGENTE → apenas registra e classifica.\
-   Comunicação imediata com equipe técnica.

👉 **Responsável:** **Time de TI/Operações**

------------------------------------------------------------------------

## 📊 Estrutura do JSON (Pré-vendas)

``` json
{
  "resumo": "Cliente deseja automatizar relatórios de vendas diários integrados ao ERP.",
  "escopo": "Coleta via API, transformação com dbt, visualização no Looker Studio.",
  "estimativa_de_esforco": "Coleta: 5 dias, Transformação: 3 dias, Visualização: 2 dias.",
  "stack_sugerida": "Airbyte, dbt, BigQuery, Looker Studio",
  "nome": "João da Silva",
  "email": "joao@empresa.com",
  "data_de_recebimento": "2025-09-14T10:00:00Z",
  "motivo_do_contato": "Automação de relatórios de vendas",
  "escopo_resumido": "Pipeline automatizado com dashboard integrado.",
  "estimativa_resumida": "3 semanas",
  "riscos_resumidos": "Instabilidade da API, falta de documentação.",
  "perguntas_para_reuniao": "1. O ERP possui API documentada? 2. Há regras de limpeza? 3. Qual ferramenta de visualização preferida?",
  "subject": "Sobre sua solicitação – Projeto de Dados",
  "mensagem_email": "Olá João da Silva, recebemos sua solicitação e já estamos avaliando..."
}
```

------------------------------------------------------------------------

## ⚙️ Integrações

-   **Gmail** → captura, rótulos, exclusão, respostas.\
-   **Google Sheets** → CRM de pré-vendas.\
-   **Google Docs** → geração de propostas.\
-   **Trello** → cards em funis de vendas e suporte.\
-   **WhatsApp API** → notificações automáticas.

------------------------------------------------------------------------

## ✅ Benefícios

-   **Automação ponta a ponta** no atendimento a clientes, alunos e
    equipe.\
-   **Resposta rápida e personalizada** para cada perfil de e-mail.\
-   **Organização no CRM e Trello**, reduzindo perdas de informação.\
-   **Alertas imediatos via WhatsApp** em casos críticos.
