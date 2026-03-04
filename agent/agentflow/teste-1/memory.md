# Agent Flow Memory: teste-1

**Created**: 2026-03-04
**Entry Point Agent**: requirements (Agent Flow Agent)
**Purpose**: Track agent flow activities from requirements analysis through implementation

---

## Agent Flow State

**Status**: ready
**Current Step**: Not started - awaiting user input
**Last Updated**: 2026-03-04

---

## Context

This agent flow is designed to take a user prompt and transform it into actionable development artifacts:

1. **Requirements Analysis** (requirements) - Extract and document requirements
2. **Technical Planning** (speckit.plan) - Create implementation plan
3. **Feature Specification** (speckit.specify) - Detail feature specifications
4. **Task Breakdown** (speckit.tasks) - Generate actionable tasks
5. **Implementation** (speckit.implement) - Execute development

### Agent Flow Configuration

- **Entry Point**: requirements agent (agent flow agent)
- **Trigger**: User invokes requirements agent with prompt
- **Output Directory**: `agent/agentflow/teste-1/`

---

## Agents

### Flow-Specific Agents

- `requirements.agent.md` - Entry point agent for requirements analysis

### Integration with System Agents

This agent flow can hand off to SpecKit system agents:
- `speckit.plan` - For technical planning
- `speckit.specify` - For feature specification
- `speckit.tasks` - For task breakdown
- `speckit.implement` - For implementation

---

## Artifacts

### Generated Files

- `memory.md` - This agent flow memory file (Current)
- `requirements.agent.md` - Requirements analysis agent
- `templates/requirements-template.md` - Requirements document template
- `requirements.md` - Requirements document (Not yet generated)
- _(Additional artifacts will be listed as they are created)_

### Expected Artifacts

- [x] `requirements.agent.md` - Requirements agent
- [x] `templates/requirements-template.md` - Requirements template
- [ ] `requirements.md` - Requirements document
- [ ] `plan.md` - Technical implementation plan
- [ ] `spec.md` - Feature specification
- [ ] `tasks.md` - Task breakdown
- [ ] `implementation-notes.md` - Implementation progress notes

---

## Notes

### Agent Flow Design

This agent flow follows a structured approach:

1. **Start with clarity**: Requirements agent ensures we understand what needs to be built before planning
2. **Plan before coding**: Technical plan provides architectural decisions and approach
3. **Specify thoroughly**: Feature spec details user stories and acceptance criteria
4. **Break down work**: Tasks make implementation manageable and trackable
5. **Execute systematically**: Implementation follows the plan and tracks progress

### Key Principles

- **User-centric**: Start with user needs and problems
- **Incremental**: Build and validate in small steps
- **Traceable**: Every implementation traces back to requirements
- **Flexible**: Agent flow can adapt based on project needs
- **Flow-specific**: Agents in this flow are specific to teste-1 context

---

## History

- **2026-03-04** - Agent flow created
- **2026-03-04** - Entry point set to requirements agent (agent flow agent)
- **2026-03-04** - Memory file initialized
- **2026-03-04** - Restructured from workflow to agent flow structure

---

## Next Steps

1. **User Action**: Invoke the requirements agent with your project description
2. **Agent Action**: Requirements agent will analyze prompt and generate requirements.md
3. **Follow-up**: After requirements, choose to either:
   - Create technical plan with `speckit.plan`
   - Create feature specification with `speckit.specify`

---

## Metadata

**Agent Flow ID**: teste-1
**Type**: Agent Flow (flow-specific agents in `agent/agentflow/teste-1/`)
**Version**: 2.0
**Last Modified**: 2026-03-04
**Modified By**: System restructure to agent flow format
