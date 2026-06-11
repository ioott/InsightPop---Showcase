# Referência da API InsightPop (v1)

Este documento fornece uma visão geral pública dos endpoints da API do InsightPop. A API foi projetada para velocidade, resiliência e facilidade de integração.

## 🔐 Autenticação
A maioria dos endpoints requer **Autenticação JWT**. Inclua o cabeçalho `Authorization: Bearer <seu_token>`.

## 🧠 Processamento de IA (`/process`)
O motor principal do InsightPop. Recebe dados desestruturados e retorna JSON estruturado.
*   **POST /process**: Suporta `.txt`, `.zip` (WhatsApp), `.pdf`, e Imagens (`.png`, `.jpg`).
*   **Exemplo de Saída:**
    ```json
    {
      "context": "Professional",
      "title": "Orçamento de Projeto",
      "relevant_facts": [{"key": "Cliente", "value": "João Silva"}],
      "action_triggers": [{"description": "Enviar Proposta", "date": "2026-06-15"}]
    }
    ```

## 📚 Gestão de Memória (`/insights`)
*   **GET /insights**: Lista memórias com busca global e filtragem por workspace.
*   **POST /confirm-insights**: Endpoint avançado para salvar, editar ou fundir memórias. Inclui **Detecção Inteligente de Colisão** para evitar entradas duplicadas.
*   **DELETE /insights/{id}**: Exclusão em cascata de memórias e gatilhos associados.

## ⚙️ Regras do Usuário (`/rules`)
Usuários podem "treinar" a IA fornecendo regras personalizadas.
*   **GET /rules**: Lista regras de extração personalizadas.
*   **POST /rules**: Cria novas diretrizes para o motor de IA.

## 💬 Onboarding Conversacional (`/onboarding`)
Um processo de entrevista guiado por IA que constrói o perfil do usuário dinamicamente.
*   **GET /onboarding/start**: Inicia o chat de IA.
*   **POST /onboarding/message**: Processa o histórico do chat para extrair a persona do usuário e sugerir regras iniciais.

---

> Para especificações técnicas completas, incluindo esquemas de erro e detalhes de rate-limiting, solicite acesso à documentação privada.
