# Agent Flow: teste-1

**Type**: Agent Flow (workflow-specific agents)
**Created**: 2026-03-04
**Status**: Active

## Overview

This is an agent flow directory that contains workflow-specific agents for the `teste-1` process. Agent flows are different from system agents - they are bound to specific workflows and operate within a dedicated context.

## Directory Structure

```
agent/agentflow/teste-1/
├── README.md                          # This file
├── memory/
│   └── constitution.md                # Agent flow state and history tracking
├── requirements.agent.md              # Requirements analysis agent (entry point)
└── templates/
    └── requirements-template.md       # Template for requirements documents
```

## Agents

### requirements.agent.md

**Type**: Entry Point Agent  
**Purpose**: Analyze user prompts and extract structured requirements  
**Outputs**: `requirements.md` (requirements document)  
**Handoffs**: Can hand off to `speckit.plan` or `speckit.specify`

This agent receives natural language descriptions from users and transforms them into structured requirements documents with:
- Functional requirements
- Non-functional requirements
- Technical constraints
- Business requirements
- Dependencies and risks
- Priorities and acceptance criteria

## How to Use

### Invoke the Requirements Agent

The requirements agent is the entry point for this flow. Invoke it with your project description:

```
Tell the requirements agent: "Build a real-time chat system for customer support"
```

The agent will:
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
