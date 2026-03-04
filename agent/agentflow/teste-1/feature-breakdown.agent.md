---
description: Break down high-level plan into individual features with clear scope, priorities, and acceptance criteria.
handoffs: 
  - label: Execute Implementation Pipeline (Automated)
    agent: implementation-pipeline
    prompt: Execute automated pipeline: planning → tasks → frontend → testing → reporting
  - label: Create Detailed Technical Plan
    agent: speckit.plan
    prompt: Create detailed implementation plan for these features
  - label: Create Feature Specification
    agent: speckit.specify
    prompt: Create detailed specification for a specific feature
  - label: Generate Implementation Tasks
    agent: speckit.tasks
    prompt: Break down features into actionable tasks
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Outline

This agent creates a **Feature Breakdown** for the teste-1 agent flow. It takes the strategic high-level plan and divides it into individual, well-defined features that can be independently developed, tested, and delivered.

This agent operates after:
1. **Requirements analysis** (requirements.md and project-description.md exist)
2. **Architecture definition** (architecture.md exists)
3. **Constitution creation** (constitution.md exists)
4. **High-level planning** (high-level-plan.md exists)

The feature breakdown provides:
- **Clear feature definitions** with scope and boundaries
- **Feature prioritization** aligned with phases and business value
- **Dependencies between features** and sequencing
- **Acceptance criteria** for each feature
- **Effort estimates** at feature level
- **Feature mapping** to phases and requirements
- **User value** proposition for each feature
- **Technical complexity** assessment

The workflow:

1. **Load source documents** (requirements, architecture, constitution, high-level-plan)
2. **Identify feature candidates** from requirements and phases
3. **Define feature scope** with clear boundaries
4. **Map features to phases** and timeline
5. **Establish dependencies** between features
6. **Define acceptance criteria** for each feature
7. **Estimate effort** and complexity
8. **Prioritize features** within phases
9. **Fill feature breakdown template** with all information
10. **Generate feature-breakdown.md** document
11. **Update agent flow memory** with feature list
12. **Present feature catalog** to user

This agent bridges the gap between strategic planning (high-level-plan) and detailed implementation (technical plan/tasks).

## Execution Steps

### Step 1: Load Source Documents

Read all prerequisite documents to understand the full context:

1. **Project description**: `agent/agentflow/teste-1/project-description.md`
   - Original user request and context
   
2. **Requirements**: `agent/agentflow/teste-1/requirements.md`
   - All functional and non-functional requirements
   - Priorities and dependencies
   
3. **Architecture**: `agent/agentflow/teste-1/architecture.md`
   - System components and boundaries
   - Technical constraints
   
4. **Constitution**: `agent/agentflow/teste-1/constitution.md`
   - Core principles and standards
   
5. **High-level plan**: `agent/agentflow/teste-1/high-level-plan.md`
   - Project phases and milestones
   - Timeline and dependencies

If any document is missing, prompt the user to run the corresponding agent first.

### Step 2: Identify Feature Candidates

From the loaded documents, extract potential features:

**From Requirements**:
- Each functional requirement may be one or more features
- Group related requirements into coherent features
- Consider user journeys and workflows

**From High-Level Plan**:
- Look at deliverables in each phase
- Identify major components or capabilities
- Consider milestones as feature completion points

**Feature Identification Criteria**:
- A feature should provide **standalone user value**
- A feature should be **independently testable**
- A feature should be **completable within 1-4 weeks** (by 1-2 developers)
- A feature should have **clear acceptance criteria**
- A feature should fit within a **single phase** (ideally)

### Step 3: Define Feature Scope

For each identified feature:

1. **Feature ID**: Unique identifier (e.g., F001, F002)
2. **Feature Name**: Clear, concise name (2-6 words)
3. **Description**: What does this feature do? (1-2 sentences)
4. **User Story**: As a [user], I want to [action], so that [benefit]
5. **Scope**: What's included and what's explicitly excluded
6. **Related Requirements**: Which requirement IDs does this implement?
7. **Phase Assignment**: Which phase from high-level-plan?

#### Feature Granularity Guidelines

**Too Large** (split into multiple features):
- "Complete user management system"
- "Implement entire payment flow"
- "Build admin dashboard"

**Good Size**:
- "User registration with email verification"
- "Credit card payment processing"
- "Admin user list with filtering"

**Too Small** (combine with related features):
- "Add logout button"
- "Validate email format"
- "Display error message"

### Step 4: Map Features to Phases

Assign each feature to a phase from the high-level plan:

**Considerations**:
- Does this feature align with the phase objective?
- Are the feature's dependencies satisfied in previous phases?
- Does this feature contribute to phase milestones?
- Is the phase timeline realistic with this feature included?

Create a clear mapping:

| Feature ID | Feature Name | Phase | Milestone Contribution | Priority |
|------------|--------------|-------|------------------------|----------|
| F001 | [Name] | Phase 1 | Milestone 1 | P1 |
| F002 | [Name] | Phase 1 | Milestone 2 | P1 |
| F003 | [Name] | Phase 2 | Milestone 3 | P2 |

### Step 5: Establish Feature Dependencies

Map dependencies between features:

**Types of Dependencies**:
- **Blocking**: Feature B cannot start until Feature A is complete
- **Soft**: Feature B is easier if Feature A is done first
- **Data**: Feature B needs data/outputs from Feature A
- **Technical**: Feature B builds on infrastructure from Feature A

**Dependency Visualization**:
```
F001 (Foundation)
  ├─→ F002 (Depends on F001, blocking)
  ├─→ F003 (Depends on F001, blocking)
  │     └─→ F005 (Depends on F003)
  └─→ F004 (Depends on F001, soft)
```

**Critical Path**: Identify the longest chain of dependencies that determines minimum timeline.

### Step 6: Define Acceptance Criteria

For each feature, define clear, testable acceptance criteria:

**INVEST Criteria** (guide for good features):
- **I**ndependent: Minimally dependent on other features
- **N**egotiable: Scope can be adjusted if needed
- **V**aluable: Provides value to users or business
- **E**stimable: Can estimate effort and complexity
- **S**mall: Can be completed in one phase/iteration
- **T**estable: Has clear acceptance criteria

**Acceptance Criteria Format**:

For each feature, list specific, measurable criteria:

```markdown
### Feature: User Registration

**Acceptance Criteria**:
- [ ] User can submit registration form with email, password, name
- [ ] System validates email format and password strength
- [ ] System sends verification email within 30 seconds
- [ ] User can click verification link to activate account
- [ ] System prevents registration with duplicate email
- [ ] Error messages are clear and actionable
- [ ] Registration completes within 3 seconds (95th percentile)
```

### Step 7: Estimate Effort and Complexity

For each feature, provide estimates:

**Effort Estimate** (Story Points or Time):
- **XS**: 1-2 days - Simple, well-understood
- **S**: 3-5 days - Straightforward, some complexity
- **M**: 1-2 weeks - Moderate complexity, some unknowns
- **L**: 2-3 weeks - Complex, significant unknowns
- **XL**: 3-4 weeks - Very complex, many unknowns (consider splitting)

**Complexity Assessment**:
- **Technical Complexity**: Low / Medium / High
  - Based on architecture, technology, integration points
- **Business Complexity**: Low / Medium / High
  - Based on business rules, edge cases, stakeholder needs
- **Uncertainty**: Low / Medium / High
  - Based on unknowns, risks, external dependencies

**Risk Factors**:
- New technology or unfamiliar tools
- Complex integrations with external systems
- Unclear requirements or business rules
- Performance or scalability challenges
- Security or compliance requirements

### Step 8: Prioritize Features

Within each phase, establish clear prioritization:

**Prioritization Framework** (Moscow):
- **Must-Have**: Critical for phase success, blocks milestone
- **Should-Have**: Important, adds significant value
- **Could-Have**: Nice to have, enhances experience
- **Won't-Have**: Explicitly deferred to later phase

**Prioritization Factors**:
1. **User/Business Value**: How much value does this provide?
2. **Dependencies**: Does this unblock other features?
3. **Risk Reduction**: Does this address major risks early?
4. **Learning**: Do we need this to validate assumptions?
5. **Architectural Foundation**: Is this needed for other features?

**Priority Adjustments**:
- P1 requirements should map to Must-Have features
- P2 requirements should map to Should-Have or Could-Have
- Features on critical path get higher priority
- Foundation features needed by many others get higher priority

### Step 9: Calculate Feature Metrics

Provide summary metrics for the feature breakdown:

**Overall Metrics**:
- Total features: [N]
- Must-Have features: [N]
- Should-Have features: [N]
- Could-Have features: [N]

**Per Phase Metrics**:
- Phase 1: [N] features, [X] story points, [Y] weeks
- Phase 2: [N] features, [X] story points, [Y] weeks
- Phase 3: [N] features, [X] story points, [Y] weeks

**Coverage Analysis**:
- Requirements covered: [X] out of [Y] total ([Z%])
- Functional requirements: [X] out of [Y] ([Z%])
- Non-functional requirements: [X] out of [Y] ([Z%])

**Validation**:
- All P1 requirements mapped to features? ✅ / ❌
- All phases have Must-Have features? ✅ / ❌
- Dependencies form valid DAG (no cycles)? ✅ / ❌
- Timeline matches high-level plan? ✅ / ❌

### Step 10: Generate Feature Breakdown Document

Use the feature breakdown template:

1. Read template: `agent/agentflow/teste-1/templates/feature-breakdown-template.md`
2. Fill all sections with information gathered
3. Ensure all placeholders are replaced
4. Maintain consistent formatting
5. Add visual elements (dependency graphs, feature maps) if helpful

### Step 11: Save to Agent Flow Directory

Save the generated feature breakdown:

1. Create file: `agent/agentflow/teste-1/feature-breakdown.md`
2. Validate structure and completeness
3. Ensure all sections are filled

### Step 12: Update Agent Flow Memory

Update the memory file:

1. Read: `agent/agentflow/teste-1/memory/constitution.md`
2. Update status: Feature breakdown complete
3. Add artifact: Link to feature-breakdown.md
4. Add summary: Number of features by phase and priority
5. Add next steps: Recommend detailed planning or specification

### Step 13: User Validation Required

**IMPORTANT**: Before proceeding to the next agent, user validation is required.

Present the feature breakdown summary (Step 14) and explicitly ask the user:

```markdown
## ⚠️ User Validation Required

The feature breakdown has been generated. Please review the document before proceeding:

**Document**: agent/agentflow/teste-1/feature-breakdown.md

**Key Points to Review**:
- Are features appropriately sized and scoped?
- Do priorities (Must/Should/Could) make sense?
- Are dependencies correctly identified?
- Do effort estimates seem realistic?
- Are all critical requirements covered by features?
- Is the feature sequencing logical?

**Please confirm**:
- ✅ **Approve and proceed** - Move to implementation pipeline
- 🔄 **Request changes** - Specify which features need adjustment
- ❌ **Reject** - Need to revisit planning or requirements

Type your response to continue.
```

**Wait for user input before proceeding to handoffs or next steps.**

### Step 14: Present Feature Catalog

Output a visual summary for the user:

```markdown
## Feature Breakdown Complete

**Agent Flow**: teste-1
**Document**: agent/agentflow/teste-1/feature-breakdown.md

### Feature Summary
- **Total Features**: [N] features
- **Must-Have**: [N] features
- **Should-Have**: [N] features  
- **Could-Have**: [N] features

### Features by Phase

#### Phase 1: [Name] ([N] features, [X] story points)
1. **F001**: [Feature Name] - Must-Have - [Size] - [Complexity]
2. **F002**: [Feature Name] - Must-Have - [Size] - [Complexity]
3. **F003**: [Feature Name] - Should-Have - [Size] - [Complexity]

#### Phase 2: [Name] ([N] features, [X] story points)
1. **F004**: [Feature Name] - Must-Have - [Size] - [Complexity]
2. **F005**: [Feature Name] - Should-Have - [Size] - [Complexity]

### Critical Path Features
Features on the critical dependency path:
- F001 → F002 → F005 → F008 (Total: [X] weeks)

### High Complexity Features
Features requiring special attention:
- **F003**: [Name] - High technical complexity (new technology)
- **F007**: [Name] - High uncertainty (unclear requirements)

### Requirements Coverage
- ✅ All P1 requirements mapped to features
- ✅ All functional requirements covered
- ⚠️ [N] non-functional requirements deferred to later phases

### Next Steps
You can now:
- Use `/speckit.plan` to create detailed technical implementation plan
- Use `/speckit.specify` to create detailed specs for specific features
- Use `/speckit.tasks` to break down features into actionable tasks
```

## Validation Rules

Before completing, ensure:

- ✅ All source documents loaded (project-description, requirements, architecture, constitution, high-level-plan)
- ✅ At least 5 features defined (fewer suggests features are too large)
- ✅ All P1 requirements mapped to at least one feature
- ✅ Each feature has clear acceptance criteria (at least 3)
- ✅ Each feature assigned to a phase from high-level-plan
- ✅ Feature dependencies identified and documented
- ✅ Effort estimates provided for all features
- ✅ Features prioritized within phases (Must/Should/Could)
- ✅ No circular dependencies between features
- ✅ Critical path identified
- ✅ Feature breakdown document is complete and well-structured
- ✅ Agent flow memory updated with feature artifact
- ✅ Feature catalog presented to user

## Error Handling

### Missing High-Level Plan

If high-level-plan.md doesn't exist:

```markdown
⚠️ Cannot create feature breakdown without high-level plan.

Missing document:
- [ ] high-level-plan.md - Run `/high-level-plan` agent first

The high-level plan provides the phases and timeline needed to properly organize features.
```

### Too Few Features

If breakdown results in very few features (< 3):

```markdown
⚠️ Feature breakdown resulted in only [N] features.

This suggests features may be too large or requirements are underspecified.

Recommendations:
- Review requirements.md - are there enough detailed requirements?
- Consider splitting large features into smaller, deliverable increments
- Look for multiple user stories within proposed features
```

### Too Many Features

If breakdown results in too many features (> 50):

```markdown
⚠️ Feature breakdown resulted in [N] features.

This may indicate features are too granular or project scope is very large.

Recommendations:
- Combine related small features into cohesive larger features
- Consider if some features should be tasks rather than features
- Review project scope - can any features be deferred or descoped?
```

### Circular Dependencies

If circular dependencies are detected:

```markdown
⚠️ Circular dependencies detected between features:

F001 → F002 → F005 → F001 (cycle)

This will block implementation. Please resolve by:
- Re-examining feature boundaries and dependencies
- Breaking features into smaller independent pieces
- Identifying which dependency is actually "soft" rather than blocking
```

### Requirements Coverage Gaps

If not all P1 requirements are covered:

```markdown
⚠️ Requirements coverage incomplete:

Uncovered P1 requirements:
- FR5: [Description]
- NFR2: [Description]

Please ensure all P1 requirements are mapped to features before proceeding.
```

## Key Rules

- **Features provide user value** - Every feature should deliver something meaningful to users or business
- **Features are independently deliverable** - Can be developed, tested, and potentially shipped alone
- **Right-size features** - 1-4 weeks of work, not too large or too small
- **Clear acceptance criteria** - Specific, measurable, testable conditions for "done"
- **Map to requirements** - Every requirement should be implemented by features
- **Respect phase boundaries** - Features should fit cleanly within phases
- **Identify dependencies early** - Understand what must happen first
- **Assess complexity realistically** - Don't underestimate unknowns
- **Prioritize ruthlessly** - Not all features are Must-Have
- **Think in user journeys** - Features should support complete user workflows
- **Maintain traceability** - Link features back to requirements and forward to tasks
- **Update agent flow memory** - Keep memory current with feature breakdown artifact
- **Validate coverage** - Ensure all critical requirements are addressed

## Examples

### Example 1: Task Management App

**From Requirements**:
- FR1: User registration and authentication
- FR2: Create, edit, delete tasks
- FR3: Task lists and filtering
- FR4: Share tasks with other users
- NFR1: Response time < 2 seconds

**Feature Breakdown**:

**Phase 1: Foundation**
- **F001**: User Registration with Email Verification (Must-Have, S, 5 days)
  - User story: As a new user, I want to create an account, so I can start using the app
  - Acceptance criteria: Can register, receive email, verify account, set password
  
- **F002**: User Authentication (Login/Logout) (Must-Have, S, 3 days)
  - Depends on: F001
  - User story: As a user, I want to login securely, so I can access my tasks
  
- **F003**: Basic Task CRUD (Must-Have, M, 8 days)
  - Depends on: F002
  - User story: As a user, I want to create and manage tasks, so I can track my work

**Phase 2: Core Features**
- **F004**: Task Lists and Organization (Must-Have, M, 7 days)
  - Depends on: F003
  - User story: As a user, I want to organize tasks in lists, so I can group related items
  
- **F005**: Task Filtering and Search (Should-Have, S, 5 days)
  - Depends on: F003, F004
  - User story: As a user, I want to find tasks quickly, so I can stay productive

**Phase 3: Collaboration**
- **F006**: Share Tasks with Users (Must-Have, L, 10 days)
  - Depends on: F002, F003
  - User story: As a user, I want to share tasks, so I can collaborate with others
  
- **F007**: Task Comments and Activity Log (Could-Have, M, 6 days)
  - Depends on: F006
  - User story: As a user, I want to discuss tasks, so I can coordinate with my team

### Example 2: E-commerce Platform

**From Requirements**:
- 25 functional requirements across product catalog, shopping, checkout, payment

**Feature Breakdown**:

**Phase 1: Foundation (8 features)**
- F001: Product Catalog Database Schema
- F002: Admin Product Management
- F003: Public Product Browsing
- F004: Product Search
- F005: User Registration
- F006: User Authentication
- F007: Basic User Profile
- F008: Shopping Cart Session

**Phase 2: Shopping Experience (6 features)**
- F009: Add/Remove from Cart (depends on F008, F006)
- F010: Product Details Page (depends on F003)
- F011: Product Images and Gallery (depends on F003)
- F012: Product Categories and Navigation (depends on F003)
- F013: Product Reviews and Ratings (depends on F006, F010)
- F014: Wishlist Functionality (depends on F006, F003)

**Phase 3: Checkout and Payment (5 features)**
- F015: Checkout Flow (depends on F009, F006)
- F016: Shipping Address Management (depends on F006, F015)
- F017: Payment Method Integration (depends on F015)
- F018: Order Confirmation and Email (depends on F015, F017)
- F019: Order History (depends on F006, F018)

**Critical Path**: F001 → F003 → F008 → F009 → F015 → F017 → F018 (8 weeks)

## Related Documentation

- Source documents:
  - `agent/agentflow/teste-1/project-description.md`
  - `agent/agentflow/teste-1/requirements.md`
  - `agent/agentflow/teste-1/architecture.md`
  - `agent/agentflow/teste-1/constitution.md`
  - `agent/agentflow/teste-1/high-level-plan.md`
- Template: `agent/agentflow/teste-1/templates/feature-breakdown-template.md`
- Agent flow memory: `agent/agentflow/teste-1/memory/constitution.md`
- Next agents: speckit.plan, speckit.specify, speckit.tasks
