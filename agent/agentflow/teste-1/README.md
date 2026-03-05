# Agent Flow: teste-1 🎨 Frontend Development

**Type**: Agent Flow (workflow-specific agents)
**Created**: 2026-03-04
**Status**: Active
**Focus**: **Frontend Development** - Specialized for UI/UX projects

## Overview

This is an agent flow directory specifically designed for **front-end development projects**. It contains workflow-specific agents that guide you from initial requirements through to fully implemented and tested frontend code.

**🎨 Frontend-Focused Features**:
- Component-based architecture planning
- State management strategies
- Responsive design considerations
- Performance optimization
- Accessibility compliance (WCAG 2.1)
- E2E testing with Cypress
- Modern frontend frameworks (React, Vue, Angular, etc.)

Agent flows are different from system agents - they are bound to specific workflows and operate within a dedicated context with specialized templates and memory.

## Directory Structure

```
agent/agentflow/teste-1/
├── README.md                          # This file
├── memory/
│   └── constitution.md                # Agent flow state and history tracking
├── requirements.agent.md              # Requirements analysis agent (entry point)
├── architecture.agent.md              # Frontend architecture definition agent
├── constitution.agent.md              # Frontend development governance agent
├── high-level-plan.agent.md           # Strategic frontend planning agent
├── feature-breakdown.agent.md         # Frontend feature breakdown agent
├── implementation-pipeline.agent.md   # Automated frontend implementation orchestrator
├── frontend.agent.md                  # Senior frontend implementation specialist
├── tester.agent.md                    # E2E testing agent (Cypress)
├── reporter.agent.md                  # Comprehensive report generator
└── templates/
    ├── requirements-template.md       # Requirements document template
    ├── architecture-template.md       # Frontend architecture template
    ├── constitution-template.md       # Constitution template
    ├── high-level-plan-template.md    # Strategic plan template
    └── feature-breakdown-template.md  # Feature breakdown template
```

## Agents

### 1. requirements.agent.md (Entry Point)

**Type**: Entry Point Agent (User-invokable)
**Purpose**: Analyze user prompts and extract structured frontend requirements  
**Tools**: ['search', 'web/fetch', 'search/codebase', 'read'] (read-only)
**User Input Required**: YES - Provide project description
**Outputs**: `requirements.md`, `project-description.md`
**Handoffs**: architecture, speckit.plan, speckit.specify

Transforms natural language descriptions into structured frontend requirements including UI/UX needs, component requirements, interactions, and accessibility needs.

### 2. architecture.agent.md

**Type**: Frontend Architecture Agent (User-invokable)
**Purpose**: Define frontend architecture, patterns, and technology stack
**Tools**: ['search', 'web/fetch', 'search/codebase', 'read'] (read-only)
**User Input Required**: YES - Architecture preferences, framework choice, styling approach
**Outputs**: `architecture.md`
**Handoffs**: constitution, speckit.plan, speckit.specify

Establishes frontend architecture including component patterns, state management strategy, styling methodology, and build configuration.

### 3. constitution.agent.md

**Type**: Governance Agent (User-invokable)
**Purpose**: Codify frontend development principles and standards
**Tools**: ['search', 'web/fetch', 'search/codebase', 'read'] (read-only)
**Outputs**: `constitution.md`
**Handoffs**: high-level-plan, speckit.plan, speckit.specify, speckit.tasks

Creates governance document for UI/UX consistency, component design rules, and frontend quality standards.

### 4. high-level-plan.agent.md

**Type**: Strategic Planning Agent (User-invokable)
**Purpose**: Create strategic roadmap with frontend-focused phases and milestones
**Tools**: ['search', 'web/fetch', 'search/codebase', 'read'] (read-only)
**User Validation Required**: YES - User must approve plan before proceeding
**Outputs**: `high-level-plan.md`
**Handoffs**: feature-breakdown, speckit.plan, speckit.tasks, speckit.specify

Generates strategic plan with frontend-specific phases (Design System → Components → Pages → Polish), milestones (responsive design, accessibility, performance), and timeline estimates.

### 5. feature-breakdown.agent.md

**Type**: Feature Analysis Agent (User-invokable)
**Purpose**: Break down plan into frontend features (components, pages, interactions)
**Tools**: ['search', 'web/fetch', 'search/codebase', 'read'] (read-only)
**User Validation Required**: YES - User must approve features before implementation
**Outputs**: `feature-breakdown.md`
**Handoffs**: implementation-pipeline, speckit.plan, speckit.specify, speckit.tasks

Divides strategic plan into deliverable UI features with component hierarchies, acceptance criteria, and frontend-specific effort estimates.

### 6. implementation-pipeline.agent.md

**Type**: Orchestrator Agent (User-invokable)
**Purpose**: Automated frontend implementation pipeline orchestrator
**Tools**: ['agent', 'read', 'search', 'search/codebase', 'web/fetch']
**Orchestrates**: planning → tasks → frontend implementation → E2E testing → reporting
**Handoffs**: speckit.implement

Executes automated pipeline: technical plan → task breakdown → frontend implementation → Cypress testing → comprehensive report.

### 7. frontend.agent.md

**Type**: Implementation Agent (Pipeline-only)
**Purpose**: Senior frontend specialist implementing with best practices
**Tools**: ['read', 'search', 'search/codebase', 'search/usages', 'edit/editFiles', 'web/fetch', 'web/githubRepo', 'execute']
**Auto-handoff**: tester agent

Implements frontend features following SOLID principles, clean code, performance optimization, accessibility compliance, and responsive design.

### 8. tester.agent.md

**Type**: Testing Agent (Pipeline-only)
**Purpose**: E2E testing with Cypress and automatic retry logic
**Tools**: ['read', 'search', 'search/codebase', 'agent', 'execute', 'web/fetch']
**Retry Logic**: Up to 3 attempts, sends errors back to planner
**Auto-handoff**: reporter agent

Runs comprehensive Cypress E2E tests, validates user flows and interactions, retries on failure.

### 9. reporter.agent.md

**Type**: Reporting Agent (Pipeline-only)
**Purpose**: Generate comprehensive implementation report
**Tools**: ['read', 'search', 'search/codebase', 'web/fetch']
**Handoffs**: speckit.implement

Consolidates all artifacts, documents successes and failures, provides quality assessment and recommendations.

## How to Use

### Step 1: Start with Requirements Agent

The requirements agent is the entry point for this frontend-focused flow. Invoke it with your frontend project description:

**Example Prompts**:
```
"Build a responsive dashboard for analytics with charts and real-time data"
"Create a component library for an e-commerce platform with cart and checkout"
"Develop a mobile-first landing page with animations and form validation"
```

The agent will:
1. Save your original prompt to `project-description.md`
2. Extract frontend-specific requirements (UI components, interactions, responsive needs, accessibility)
3. Generate structured `requirements.md`
4. Present handoff options to continue

### Step 2: Define Frontend Architecture

Use the architecture agent to define your frontend stack:

**You'll be asked about**:
- Framework choice (React, Vue, Angular, Svelte, etc.)
- State management (Redux, Context API, Zustand, Pinia, etc.)
- Styling approach (CSS Modules, Styled Components, Tailwind, SASS)
- Build tools (Vite, Webpack, Turbopack)
- Deployment strategy

### Step 3: Strategic Planning with Validation

The high-level-plan agent creates frontend-focused phases:
- Phase 1: Design System & Foundation
- Phase 2: Core Components & Pages
- Phase 3: Feature Components
- Phase 4: Polish & Optimization

**⚠️ User validation required** - Review and approve before proceeding.

### Step 4: Feature Breakdown with Validation

The feature-breakdown agent divides the plan into:
- UI Components (buttons, forms, cards, navigation)
- Pages/Views (homepage, dashboard, profile)
- Interactions (modals, dropdowns, animations)
- State Management features
- Performance optimizations

**⚠️ User validation required** - Review features and priorities before implementation.

### Step 5: Automated Implementation Pipeline

After feature approval, the implementation-pipeline executes:
1. **Planning** (speckit.plan) - Technical frontend implementation plan
2. **Tasks** (speckit.tasks) - Actionable task breakdown
3. **Frontend** (frontend agent) - Senior frontend specialist implements with best practices
4. **Testing** (tester agent) - Cypress E2E tests (retry up to 3x on failure)
5. **Reporting** (reporter agent) - Comprehensive report with results and unresolved issues

This runs autonomously with automatic handoffs between specialized agents.
1. Analyze your prompt
2. Extract all requirements
3. Categorize and prioritize them
4. Generate `requirements.md`
5. Update `memory.md` with progress

### Check Flow State

View the agent flow memory to see current state:

```bash
cat agent/agentflow/teste-1/memory/constitution.md
```

### View Generated Requirements

After the agent runs, check the requirements document:

```bash
cat agent/agentflow/teste-1/requirements.md
```

## Files Generated

The agents in this flow will create:

- `requirements.md` - Structured requirements document
- Additional artifacts as the flow progresses

All outputs are saved in this directory (`agent/agentflow/teste-1/`).

## Integration with System Agents

This agent flow integrates with SpecKit system agents:

- **speckit.plan** - For technical planning based on requirements
- **speckit.specify** - For detailed feature specifications
- **speckit.tasks** - For task breakdown
- **speckit.implement** - For implementation execution

## Memory Tracking

The `memory/constitution.md` file tracks:
- Current flow state
- Artifacts generated
- Agent execution history
- Next steps and recommendations

Update this file as the flow progresses to maintain continuity across sessions.

## Key Differences from System Agents

| Aspect | System Agents | Agent Flow Agents (this) |
|--------|--------------|-------------------------|
| Location | `.github/agents/` | `agent/agentflow/teste-1/` |
| Naming | `speckit.[name].agent.md` | `[name].agent.md` |
| Scope | Cross-project, reusable | This flow only |
| Memory | Stateless | `memory/constitution.md` tracks state |
| Templates | `.specify/templates/` | `templates/` (flow-specific) |

## Extending This Flow

To add more agents to this flow:

1. Create new agent file: `agent/agentflow/teste-1/[name].agent.md`
2. Update handoffs in existing agents
3. Add agent to `memory/constitution.md` artifacts list
4. Create flow-specific templates if needed in `templates/`

## Version History

- **3.0** (2026-03-04) - Memory structure updated to memory/constitution.md
- **2.0** (2026-03-04) - Restructured to agent flow format
- **1.0** (2026-03-04) - Initial creation

---

For questions about agent flows vs system agents, see [.github/agents/speckit.agentforge.agent.md](.github/agents/speckit.agentforge.agent.md).
