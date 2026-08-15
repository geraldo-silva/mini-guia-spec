# Miniguia de Estudo: Desenvolvimento Orientado a Especificações (Spec-Driven Development) com IA

Este documento reúne o consolidado de estudos baseado na mentoria sobre **Spec-Driven Development (SDD)**, **Seed Specs**, **Guardrails** e **Governança de Custos/Contexto em Agentes de IA**.

---

## 1. Resumos Estruturados do Assunto

### 1.1 O Conceito de Spec-Driven Development (SDD)
- **O que é:** Uma metodologia de desenvolvimento em que uma especificação (Spec) detalhada é criada antes do código. No contexto de Inteligência Artificial, a Spec serve como um "cercadinho" (boundary/guardrail) que delimita rigorosamente a atuação do agente.
- **Por que utilizar:** 
  - Evita o desenvolvimento baseado puramente em "vibes" (*Vibe Coding* sem planejamento).
  - Garante padronização arquitetural, previsibilidade de código e alta manutenibilidade.
  - Reduz drasticamente o acúmulo de pacotes/dependências mortas e código redundante.
  - Elimina o risco de falhas em cascata causadas pela perda de contexto a cada novo prompt.

### 1.2 Anatomia de uma Seed Spec (A Semente do Projeto)
A **Seed Spec** é o documento de especificação raiz do projeto (geralmente mantido em Markdown, ex.: `specs/00-seed-spec.md`). Ela atua como a planta arquitetural e o solo fértil do sistema.

#### Componentes Principais:
1. **App Context (Contexto da Aplicação):** Define o propósito fundamental, o domínio de negócio e o escopo funcional (ex.: API REST backend para cadastro e organização de dados da Copa/FIFA).
2. **Stack Definitions (Tech Stack):** Lista explícita do ecossistema, frameworks, ORMs e bibliotecas autorizadas (ex.: Node.js, Fastify, Zod, Drizzle ORM).
3. **Guidelines & Standards (Padrões de Código):**
   - Convenções de Nomenclatura de Arquivos: `kebab-case` (ex.: `user-controller.ts`).
   - Declarações de Constantes: `SCREAMING_SNAKE_CASE` (proibição de *magic numbers*).
   - Separação em Camadas Limpas: Isolamento entre *Routes*, *Controllers*, *Services*, *DTOs* e *Models*.
   - Padronização de API: Endpoints no plural e versionados (ex.: `/v1/players`).
4. **Guardrails (Limites de Funcionamento):**
   - Mapeamento fixo de portas e variáveis de ambiente.
   - Proibição de inclusão de novas *features* que divirjam do objetivo central sem atualização prévia da Spec.
   - Proibição de senhas e dados sensíveis fixos em código (*hardcoded credentials*).

### 1.3 Gestão de Contexto e Otimização de Custos (Tokens)
- **Gerenciamento da Janela de Contexto:** Deixar o chat acumular histórico ilimitado desperdiça tokens e degrada a coerência do agente (*context drift*).
- **Health Check de Spec:** Antes de instruir a IA a gerar código, submeta a Spec a um exame de saúde automático/manual para identificar lacunas, contradições e inconsistências.
- **Hierarquia Estruturada de Specs:**
  - **Seed Spec (Foco na Fundação):** Contém a estrutura global e os pilares arquiteturais.
  - **Feature Specs (Specs Menores):** Specs incrementais e direcionadas (ex.: `01-spec-login.md`), mantendo sessões de contexto curtas, baratas e precisas.

---

## 2. Glossário de Conceitos Aprendidos

| Termo | Definição |
| :--- | :--- |
| **Spec-Driven Development (SDD)** | Metodologia onde documentos de especificação orientam rigorosamente a geração e manutenção de código por agentes de IA. |
| **Seed Spec** | O documento base e inicial que estabelece a arquitetura, o contexto do domínio e as restrições globais de um software. |
| **Guardrails** | Regras de contenção e limites operacionais que impedem a IA de violar os padrões arquiteturais ou criar soluções indesejadas. |
| **Vibe Coding** | Prática informal de programar gerando prompts diretos sem planejamento arquitetural prévio, resultando em alto débito técnico. |
| **Health Check (de Spec)** | Processo de auditoria em um documento de especificação para detectar brechas de requisitos, ambiguidades ou conflitos técnicos antes da codificação. |
| **Magic Numbers** | Valores numéricos soltos no código sem nome descritivo ou contexto claro, violando princípios de Clean Code. |
| **Context Window (Janela de Contexto)** | A quantidade máxima de informação/tokens que um modelo de linguagem consegue processar simultaneamente em uma instrução. |
| **Kebab-case** | Padronização de escrita de texto em letras minúsculas separadas por hífens (ex.: `http-server.ts`), ideal para nomenclatura de arquivos. |

---

## 3. Conjunto de Prompts Reutilizáveis

### Prompt 1: Criação de Seed Spec Inicial
```text
Atue como um Arquiteto de Software Especialista. Preciso criar a Seed Spec em Markdown para o projeto [NOME DO PROJETO].
A aplicação consiste em: [DESCREVER O OBJETIVO E DOMÍNIO DA APLICAÇÃO].

Gere uma Seed Spec contendo obrigatoriamente:
1. App Context: Visão geral e escopo funcional do sistema.
2. Tech Stack: [LISTAR TECNOLOGIAS, EX: Node.js, Fastify, Zod, Drizzle ORM].
3. Guidelines & Code Patterns: Nomenclatura em kebab-case, eliminação de magic numbers, separação em camadas (Routes, Controllers, Services, DTOs).
4. Guardrails: Proibição de credenciais hardcoded, padrões de segurança e porta padrão [EX: 3333].

