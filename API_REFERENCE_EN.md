# InsightPop API Reference (v1)

This document provides a public overview of the InsightPop API endpoints. The API is designed for speed, resilience, and ease of integration.

## 🔐 Authentication
Most endpoints require **JWT Authentication**. Include the header `Authorization: Bearer <your_token>`.

## 🧠 AI Processing (`/process`)
The core engine of InsightPop. It receives unstructured data and returns structured JSON.
*   **POST /process**: Supports `.txt`, `.zip` (WhatsApp), `.pdf`, and Images (`.png`, `.jpg`).
*   **Output Example:**
    ```json
    {
      "context": "Professional",
      "title": "Project Budget",
      "relevant_facts": [{"key": "Client", "value": "John Doe"}],
      "action_triggers": [{"description": "Send Proposal", "date": "2026-06-15"}]
    }
    ```

## 📚 Memory Management (`/insights`)
*   **GET /insights**: List memories with global search and workspace filtering.
*   **POST /confirm-insights**: Advanced endpoint for saving, editing, or merging memories. Includes **Smart Collision Detection** to prevent duplicate entries.
*   **DELETE /insights/{id}**: Cascading deletion of memories and associated triggers.

## ⚙️ User Rules (`/rules`)
Users can "train" the AI by providing custom rules.
*   **GET /rules**: List custom extraction rules.
*   **POST /rules**: Create new guidelines for the AI engine.

## 💬 Conversational Onboarding (`/onboarding`)
An AI-driven interview process that builds the user profile dynamically.
*   **GET /onboarding/start**: Initiates the AI chat.
*   **POST /onboarding/message**: Processes the chat history to extract user persona and suggest initial rules.

---

> For full technical specifications, including error schemas and rate-limiting details, please request access to the private documentation.
