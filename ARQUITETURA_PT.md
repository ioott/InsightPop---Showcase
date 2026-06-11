# InsightPop - Arquitetura Técnica e Engenharia

Este documento detalha as decisões arquiteturais e os padrões de engenharia que sustentam o **InsightPop**. O sistema foi projetado para alta disponibilidade, escalabilidade e manutenibilidade, seguindo princípios modernos de engenharia de software.

## 🏗️ Arquitetura Backend: Limpa e Desacoplada

O backend é construído com **Python (FastAPI)** e segue uma abordagem de **Monolito Modular em Camadas**, fortemente inspirada em **Clean Architecture** e princípios **SOLID**.

### Camadas Principais:
1.  **Camada de API (Controllers):** Focada e leve. Lida com questões HTTP, validação (Pydantic) e delega a lógica de negócio para os Services.
2.  **Camada de Serviço (Lógica de Negócio):** Orquestra fluxos complexos, como processamento de IA, onboarding de usuários e consolidação de dados. É completamente desacoplada do banco de dados e do framework HTTP.
3.  **Camada de Repositório (Acesso a Dados):** Implementa o **Repository Pattern**. Abstrai consultas ao banco de dados (MongoDB/Motor), permitindo futuras trocas de banco sem tocar na lógica de negócio.
4.  **Motor de Templates:** Os prompts de IA são armazenados como templates externos, permitindo iteração rápida e versionamento do comportamento da IA sem alterações no código.

### Estratégia de Resiliência: IA "Zero Downtime"
Para garantir que o app permaneça funcional apesar de cotas de API ou falhas de modelo, o IP implementa:
*   **Rodízio de Múltiplas Chaves:** Failover automático entre várias chaves de API.
*   **Fallback de Modelo:** Pontuação e ranqueamento dinâmico de modelos LLM disponíveis. Se um falhar, o sistema degrada automaticamente para o próximo melhor modelo em milissegundos.

---

## 📱 Arquitetura Mobile: Estabilidade e Tipagem

Construído com **React Native (TypeScript)**, o cliente mobile foca em performance e estado previsível.

### Padrões de Engenharia:
*   **Gestão de Estado (Zustand):** Um sistema leve e centralizado que evita o "prop-drilling" e garante alta performance.
*   **Custom Hooks para SRP:** A lógica de negócio é extraída dos componentes de UI para hooks especializados (ex: `useAuthSession`, `usePushNotifications`), aderindo ao **Princípio da Responsabilidade Única**.
*   **Design System:** Uma paleta de cores semântica e sistema de tipografia centralizado (`colors.ts`) garantem consistência visual e zero CSS inline.
*   **Segurança de Tipos:** Tipagem de ponta a ponta, das respostas da API aos componentes de UI, reduzindo erros em tempo de execução.

---

## 🧪 Testes e Garantia de Qualidade

*   **Backend:** Suíte de testes abrangente usando **Pytest**, cobrindo fluxos críticos como extração de IA e consolidação de dados.
*   **Frontend:** Validação de UI e lógica usando **Jest** e **Testing Library**.
*   **Qualidade de Código:** Adesão estrita à **PEP 8**, linting automatizado e um protocolo de "código limpo" (sem linhas > 79 caracteres, modularização de imports).

---

> **Nota:** Para uma demonstração privada do código-fonte, incluindo detalhes da implementação do motor de IA e camadas de segurança, entre em contato com a autora.
