# Relatório: Fluxo de Agentes SpecKit

## Visão Geral

O **SpecKit** é um sistema de desenvolvimento orientado a especificações que separa claramente o **QUE** construir (requisitos de negócio) do **COMO** construir (decisões técnicas). O sistema organiza features em user stories com prioridades (P1, P2, P3) para permitir entregas incrementais de MVPs.

## Agentes do Sistema (9 Total)

### 1. speckit.constitution
**Propósito**: Cria e mantém a constituição do projeto  
**Arquivo**: [.specify/memory/constitution.md](.specify/memory/constitution.md)  
**Função**: Define princípios não-negociáveis do projeto (Library-First, Test-First, etc.), gerencia versionamento e propaga mudanças para templates dependentes.

### 2. speckit.specify
**Propósito**: Cria especificação de feature a partir de linguagem natural  
**Saída**: Branch `###-short-name` + arquivo `specs/###-feature/spec.md`  
**Função**: Define **O QUE** construir - requisitos, user stories, critérios de sucesso. Tecnologia-agnóstico e focado em negócio. Valida qualidade da especificação.

### 3. speckit.clarify
**Propósito**: Resolve ambiguidades na especificação (opcional)  
**Função**: Q&A interativo (máximo 5 perguntas), atualiza spec.md com clarificações, reduz retrabalho em fases posteriores. Executar antes do `plan`.

### 4. speckit.plan
**Propósito**: Cria plano técnico de implementação  
**Saída**: `plan.md`, `research.md`, `data-model.md`, `contracts/`, `quickstart.md`  
**Função**: Define **COMO** construir - tech stack, decisões arquiteturais, estrutura de projeto. Valida contra princípios da constituição. Atualiza contextos de agentes AI.

### 5. speckit.tasks
**Propósito**: Gera breakdown de tarefas dos documentos de design  
**Saída**: `tasks.md` organizado por user story  
**Função**: Cria tarefas ordenadas por dependência, organizadas por prioridade (P1→P2→P3). Cada story = incremento MVP independentemente testável. Formato: `[ID] [P?] [Story] Descrição`.

### 6. speckit.analyze
**Propósito**: Análise de consistência cross-artifact (somente leitura)  
**Função**: Verifica alinhamento entre spec.md ↔ plan.md ↔ tasks.md. Detecta duplicações, ambiguidades, gaps e violações da constituição. **NÃO** corrige automaticamente, apenas reporta.

### 7. speckit.implement
**Propósito**: Executa implementação a partir das tarefas  
**Função**: Valida checklists antes de iniciar, cria ignore files, processa tarefas fase-por-fase respeitando dependências e marcadores paralelos [P]. Marca tarefas completas como [X].

### 8. speckit.checklist
**Propósito**: Gera checklists de validação de qualidade  
**Função**: "Testes unitários para requisitos" - valida qualidade dos requisitos (completos/claros/consistentes), **NÃO** implementação. Domain-specific (ux.md, security.md, api.md). Pode ser executado em qualquer ponto.

### 9. speckit.taskstoissues
**Propósito**: Converte tarefas em issues do GitHub  
**Requisito**: GitHub MCP server  
**Função**: Cria issues a partir de tasks.md. Funciona apenas com remotes GitHub.

## Fluxo de Trabalho

```
┌─────────────────────────────────────────────────────────────┐
│ FASE 0: Setup do Projeto (Opcional, executar uma vez)      │
└─────────────────────────────────────────────────────────────┘
   speckit.constitution → .specify/memory/constitution.md

┌─────────────────────────────────────────────────────────────┐
│ FASE 1: Especificação da Feature (O QUE construir)         │
└─────────────────────────────────────────────────────────────┘
   speckit.specify       → Cria branch, specs/###-name/spec.md
          ↓
   speckit.clarify*      → Atualiza spec.md com clarificações
          ↓                 (*Opcional, mas recomendado)
   speckit.checklist*    → Cria checklist requirements.md
          ↓                 (*Opcional)

┌─────────────────────────────────────────────────────────────┐
│ FASE 2: Planejamento Técnico (COMO construir)              │
└─────────────────────────────────────────────────────────────┘
   speckit.plan          → plan.md, research.md, data-model.md,
          ↓                 contracts/, quickstart.md
          ↓                 Atualiza arquivos de contexto
   speckit.checklist*    → Cria checklists de design
          ↓                 (*Opcional)

┌─────────────────────────────────────────────────────────────┐
│ FASE 3: Breakdown de Tarefas                               │
└─────────────────────────────────────────────────────────────┘
   speckit.tasks         → tasks.md (organizado por story)
          ↓
   speckit.analyze*      → Relatório de consistência (read-only)
          ↓                 (*Opcional, mas recomendado)
   speckit.checklist*    → Cria checklists de implementação
          ↓                 (*Opcional)

┌─────────────────────────────────────────────────────────────┐
│ FASE 4: Implementação                                       │
└─────────────────────────────────────────────────────────────┘
   speckit.implement     → Executa tarefas, valida checklists
          ∥                 Fase 1: Setup
          ∥                 Fase 2: Foundational (bloqueia stories)
          ∥                 Fase 3+: User Stories (P1→P2→P3)
          ∥                 Final: Polish
          ↓
   speckit.taskstoissues*→ Criar issues no GitHub
                           (*Opcional)
```

## Interação com Arquivos .specify

### Templates Base ([.specify/templates/](.specify/templates/))
- **spec-template.md**: Estrutura para especificação (user scenarios, requisitos funcionais, critérios de sucesso)
- **plan-template.md**: Estrutura para planejamento técnico (contexto técnico, estrutura do projeto)
- **tasks-template.md**: Estrutura para breakdown de tarefas (fases, dependências)
- **checklist-template.md**: Estrutura para checklists domain-specific
- **constitution-template.md**: Estrutura para constituição do projeto
- **agent-file-template.md**: Estrutura para contextos de AI agents

### Memória do Sistema
- **[.specify/memory/constitution.md](.specify/memory/constitution.md)**: Princípios do projeto validados por `speckit.plan` e `speckit.analyze`

### Scripts de Suporte ([.specify/scripts/bash/](.specify/scripts/bash/))
Os agentes utilizam scripts bash para:
- Criar branches e diretórios de features
- Validar estrutura e requisitos
- Atualizar contextos de AI agents
- Preparar ambiente de planejamento

Ver: [relatorio-scripts.md](relatorio-scripts.md) para detalhes completos.

## Artifacts Gerados

Cada feature cria um diretório `specs/###-feature-name/` contendo:
- **spec.md**: Especificação da feature (O QUE)
- **plan.md**: Plano técnico (COMO)
- **tasks.md**: Tarefas de implementação
- **research.md**: Pesquisa técnica (unknowns resolvidos)
- **data-model.md**: Modelo de dados
- **contracts/**: Contratos de API/interfaces
- **quickstart.md**: Guia rápido de início
- **checklists/**: Validações domain-specific (ux.md, security.md, etc.)

## Pontos de Decisão

### Quando usar speckit.clarify?
- Após `specify` se houver ambiguidades nos requisitos
- Antes de `plan` para evitar retrabalho técnico
- **Sempre recomendado** para features complexas

### Quando usar speckit.analyze?
- Após `tasks` antes de começar implementação
- Para validar consistência entre spec/plan/tasks
- **Sempre recomendado** para detectar gaps antecipadamente

### Quando usar speckit.checklist?
- Em qualquer ponto do workflow
- Para domínios específicos (UX, segurança, API, acessibilidade)
- Múltiplos checklists podem coexistir

## Filosofia do Sistema

### Separação WHAT vs HOW
- **spec.md**: Requisitos de negócio, agnóstico de tecnologia
- **plan.md**: Decisões técnicas, stack escolhido

### User Stories como MVPs
- Cada story (P1, P2, P3) é **independentemente testável**
- Permite entrega incremental: P1 → MVP mínimo, P2 → expansão, P3 → refinamento
- Tasks organizadas por story para suportar entregas parciais

### Constitutional Principles
- Princípios não-negociáveis definidos em constitution.md
- Validados automaticamente durante planning e analysis
- Conflitos = severidade CRÍTICA

### Quality Gates via Checklists
- "Testes unitários para requisitos"
- Validam **qualidade dos requisitos**, não da implementação
- Domain-specific e expansíveis

## Referências Cruzadas

- Definições de agentes: [.github/agents/](.github/agents/)
- Prompts de agentes: [.github/prompts/](.github/prompts/)
- Templates do sistema: [.specify/templates/](.specify/templates/)
- Scripts de suporte: [.specify/scripts/bash/](.specify/scripts/bash/)
- Relatório de scripts: [relatorio-scripts.md](relatorio-scripts.md)
