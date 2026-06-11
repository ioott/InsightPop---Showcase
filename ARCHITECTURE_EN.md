# InsightPop - Technical Architecture & Engineering

This document outlines the architectural decisions and engineering standards that power **InsightPop**. The system is designed for high availability, scalability, and maintainability, following modern software engineering principles.

## 🏗️ Backend Architecture: Clean & Decoupled

The backend is built with **Python (FastAPI)** and follows a **Layered Modular Monolith** approach, heavily inspired by **Clean Architecture** and **SOLID** principles.

### Key Layers:
1.  **API Layer (Controllers):** Thin and focused. It handles HTTP concerns, validation (Pydantic), and delegates business logic to Services.
2.  **Service Layer (Business Logic):** Orchestrates complex flows, such as AI processing, user onboarding, and data consolidation. It is completely decoupled from the database and the HTTP framework.
3.  **Repository Layer (Data Access):** Implements the **Repository Pattern**. It abstracts database queries (MongoDB/Motor), allowing for future database swaps without touching business logic.
4.  **Template Engine:** AI prompts are stored as external templates, allowing for rapid iteration and versioning of AI behavior without code changes.

### Resilience Strategy: "Zero Downtime" AI
To ensure the app remains functional despite API quotas or model failures, IP implements:
*   **Multi-Key Rotation:** Automatic failover across multiple API keys.
*   **Model Fallback:** Dynamic scoring and ranking of available LLM models. If one fails, the system automatically degrades to the next best available model in milliseconds.

---

## 📱 Mobile Architecture: Stability & Type Safety

Built with **React Native (TypeScript)**, the mobile client focuses on performance and a predictable state.

### Engineering Standards:
*   **State Management (Zustand):** A lightweight, centralized state management system that avoids "prop-drilling" and ensures high performance.
*   **Custom Hooks for SRP:** Business logic is extracted from UI components into specialized hooks (e.g., `useAuthSession`, `usePushNotifications`), adhering to the **Single Responsibility Principle**.
*   **Design System:** A semantic color palette and centralized typography system (`colors.ts`) ensure UI consistency and zero inline CSS.
*   **Type Safety:** End-to-end typing from API responses to UI components, reducing runtime errors.

---

## 🧪 Testing & Quality Assurance

*   **Backend:** Comprehensive test suite using **Pytest**, covering critical flows like AI extraction and data consolidation.
*   **Frontend:** UI and logic validation using **Jest** and **Testing Library**.
*   **Code Quality:** Strict adherence to **PEP 8**, automated linting, and a "clean code" protocol (no lines > 79 chars, no inline CSS, modular imports).

---

> **Note:** For a private walkthrough of the codebase, including the implementation details of the AI engine and security layers, please contact the author.
