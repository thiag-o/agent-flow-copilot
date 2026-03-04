---
description: Define architecture, design patterns, rules and standards for scalable project development.
handoffs: 
  - label: Establish Project Constitution
    agent: constitution
    prompt: Create project constitution from requirements and architecture
  - label: Create Technical Plan
    agent: speckit.plan
    prompt: Create implementation plan based on these architecture decisions
  - label: Create Feature Specification
    agent: speckit.specify
    prompt: Create detailed specification following this architecture
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Outline

This agent defines the **architecture, design patterns, and project rules** for the teste-1 agent flow. It operates after requirements analysis and before technical planning.

This agent **requires explicit user input** to define:
- Architecture style and patterns
- Technology stack preferences
- Coding standards and conventions
- Project-specific rules

The agent **enforces mandatory best practices**:
- Design Patterns (Factory, Strategy, Observer, etc.)
- Clean Code principles
- SOLID principles
- Scalability rules

The workflow:

1. **Gather architecture input** from user (architecture style, stack, preferences)
2. **Define architectural decisions** and structure
3. **Establish mandatory design patterns** (Factory, Singleton, Strategy, etc.)
4. **Define coding standards** (Clean Code, SOLID)
5. **Create project rules** for scalability and maintainability
6. **Generate architecture document** using the architecture template
7. **Save document** to agent flow directory
8. **Update agent flow memory** with architecture decisions

This agent ensures consistency, quality, and scalability across the project.

## Execution Steps

### Step 1: Validate Input

Ensure the user has provided architecture preferences:

- If `$ARGUMENTS` is empty or insufficient, ask the user:
  - **Architecture Style**: What architecture will you use? (e.g., Microservices, Monolithic, Layered, Hexagonal, Clean Architecture, Event-Driven)
  - **Technology Stack**: What technologies/languages? (e.g., Node.js, Python, Java, React, Vue)
  - **Database**: What database(s)? (e.g., PostgreSQL, MongoDB, Redis)
  - **Deployment**: How will it be deployed? (e.g., Docker, Kubernetes, Serverless, VMs)
  - **Project Patterns**: Any specific patterns you want to enforce? (e.g., Repository, Service Layer, CQRS)
  - **Standards**: Any specific coding standards or conventions?

### Step 2: Read Requirements Document

Before proceeding, load the requirements document from the previous step:

```bash
# Check if requirements document exists
if [ -f "agent/agentflow/teste-1/requirements.md" ]; then
    cat agent/agentflow/teste-1/requirements.md
else
    echo "Warning: Requirements document not found. This agent should run after requirements agent."
fi
```

Use the requirements to inform architectural decisions.

### Step 3: Define Architectural Decisions

Based on user input and requirements, document:

#### 3.1 Architecture Style

- **Selected Architecture**: [User's choice + rationale]
- **Architecture Layers**: Define clear separation of concerns
- **Component Boundaries**: Define how components interact
- **Data Flow**: Describe how data moves through the system

#### 3.2 Technology Stack

- **Backend**: Languages, frameworks, runtime
- **Frontend**: Languages, frameworks, libraries
- **Database**: Primary and cache databases
- **Infrastructure**: Deployment, CI/CD, monitoring
- **External Services**: APIs, cloud services, integrations

#### 3.3 Design Decisions

Document key design decisions with rationale:
- Why this architecture was chosen
- Trade-offs considered
- Alternatives evaluated
- Expected benefits and risks

### Step 4: Define Mandatory Design Patterns

**REQUIRED**: All projects must implement appropriate design patterns. Select from these based on architecture:

#### Creational Patterns
- **Factory Pattern**: For object creation with abstraction
- **Builder Pattern**: For complex object construction
- **Singleton Pattern**: For shared resources (use carefully)
- **Prototype Pattern**: For object cloning when needed

#### Structural Patterns
- **Adapter Pattern**: For interface compatibility
- **Decorator Pattern**: For extending functionality
- **Facade Pattern**: For simplified interfaces
- **Proxy Pattern**: For access control and lazy loading

#### Behavioral Patterns
- **Strategy Pattern**: For algorithm selection
- **Observer Pattern**: For event handling
- **Command Pattern**: For request encapsulation
- **Chain of Responsibility**: For request processing

#### Architectural Patterns
- **Repository Pattern**: For data access abstraction
- **Service Layer**: For business logic organization
- **Dependency Injection**: For loose coupling (MANDATORY)
- **Unit of Work**: For transaction management

**Selection Criteria**:
- Choose 3-5 patterns that fit the architecture
- Document where each pattern will be used
- Provide examples for implementation
- Explain benefits for the specific project

### Step 5: Enforce Clean Code Principles

**MANDATORY**: All code must follow Clean Code principles:

#### Naming Conventions
- Use meaningful, descriptive names
- Classes: `PascalCase` (e.g., `UserRepository`)
- Functions/Methods: `camelCase` (e.g., `getUserById`)
- Constants: `UPPER_SNAKE_CASE` (e.g., `MAX_RETRY_COUNT`)
- Private members: prefix with `_` or use language convention

#### Function Rules
- **Single Responsibility**: One function, one purpose
- **Small Functions**: Max 20-30 lines
- **Few Parameters**: Max 3 parameters, use objects for more
- **No Side Effects**: Functions should be predictable
- **Error Handling**: Don't return null, use exceptions or Result types

#### Code Organization
- **DRY**: Don't Repeat Yourself
- **KISS**: Keep It Simple, Stupid
- **YAGNI**: You Aren't Gonna Need It
- **Separate Concerns**: One file, one responsibility
- **Comments**: Explain WHY, not WHAT

#### Other Rules
- Avoid magic numbers/strings
- Use meaningful abstractions
- Prefer composition over inheritance
- Write self-documenting code

### Step 6: Enforce SOLID Principles

**MANDATORY**: All code must follow SOLID principles:

#### S - Single Responsibility Principle
- Each class/module has ONE reason to change
- Separate business logic from infrastructure
- Example: `UserValidator` only validates, `UserRepository` only persists

#### O - Open/Closed Principle
- Open for extension, closed for modification
- Use interfaces and abstractions
- Example: Strategy pattern for payment methods

#### L - Liskov Substitution Principle
- Subtypes must be substitutable for base types
- Don't break contracts in inheritance
- Example: All repository implementations follow same contract

#### I - Interface Segregation Principle
- Many specific interfaces better than one general
- Clients shouldn't depend on unused methods
- Example: `IReadable` and `IWritable` instead of `IReadWrite`

#### D - Dependency Inversion Principle
- Depend on abstractions, not concretions
- High-level modules independent of low-level
- Use dependency injection (MANDATORY)

### Step 7: Define Project Rules

Create rules that ensure **scalability, maintainability, and quality**:

#### Scalability Rules

1. **Stateless Services**: Services must be stateless for horizontal scaling
2. **Async Processing**: Use async for I/O operations and long-running tasks
3. **Caching Strategy**: Define what, where, and when to cache
4. **Database Optimization**: 
   - Use indexes appropriately
   - Avoid N+1 queries
   - Consider read replicas for high read loads
5. **Load Balancing**: Design for multiple instances
6. **Resource Limits**: Set timeouts, connection pools, rate limits
7. **Monitoring**: Add metrics for performance tracking

#### Maintainability Rules

1. **Testing Requirements**:
   - Minimum 80% code coverage
   - Unit tests for all business logic
   - Integration tests for critical paths
   - E2E tests for user flows
2. **Documentation**:
   - README for setup instructions
   - API documentation (OpenAPI/Swagger)
   - Architecture decision records (ADRs)
   - Code comments for complex logic
3. **Version Control**:
   - Feature branches + PR reviews
   - Conventional commits (feat:, fix:, docs:)
   - No direct commits to main/master
4. **Code Review**:
   - All PRs require approval
   - Use linters and formatters
   - Automated checks in CI/CD

#### Security Rules

1. **Authentication & Authorization**:
   - Implement proper authentication
   - Use role-based access control (RBAC)
   - Secure session management
2. **Data Protection**:
   - Encrypt sensitive data at rest
   - Use HTTPS for data in transit
   - Never log sensitive information
3. **Input Validation**:
   - Validate all user inputs
   - Sanitize data to prevent injection
   - Use parameterized queries
4. **Dependency Management**:
   - Keep dependencies updated
   - Scan for vulnerabilities
   - Use lock files

#### Performance Rules

1. **Response Time**: API responses under 200ms (p95)
2. **Database Queries**: Optimize queries, use explain plans
3. **Asset Optimization**: Compress images, minify JS/CSS
4. **Lazy Loading**: Load resources on demand
5. **Pagination**: Implement pagination for large datasets

#### Error Handling Rules

1. **Graceful Degradation**: System continues with reduced functionality
2. **Meaningful Errors**: Return clear error messages
3. **Logging**: Log errors with context and stack traces
4. **Retry Logic**: Implement exponential backoff for failures
5. **Circuit Breakers**: Prevent cascade failures

### Step 8: Generate Architecture Document

Load the architecture template:

```bash
cat agent/agentflow/teste-1/templates/architecture-template.md
```

Fill in all sections:
- Architecture Overview
- Technology Stack
- Design Patterns (selected)
- Clean Code Standards
- SOLID Principles Application
- Project Rules (scalability, maintainability, security, performance)
- Deployment Architecture
- Monitoring & Observability

### Step 9: Save Architecture Document

Write the completed architecture document:

```bash
cat > agent/agentflow/teste-1/architecture.md << 'EOF'
[Generated architecture content]
EOF
```

### Step 10: Update Agent Flow Memory

Update the memory file to track architecture decisions:

```bash
# Read current memory
cat agent/agentflow/teste-1/memory/constitution.md

# Append architecture decisions
cat >> agent/agentflow/teste-1/memory/constitution.md << 'EOF'

### Architecture Definition Completed

**Date**: [current date]
**Architecture Style**: [selected architecture]
**Key Decisions**: 
- [Decision 1]
- [Decision 2]
- [Decision 3]

**Design Patterns**: [list selected patterns]
**Document**: agent/agentflow/teste-1/architecture.md

EOF
```

### Step 11: Summary and Next Steps

Provide a summary of the architecture definition:

```markdown
## Architecture Definition Complete

### Architecture Overview
- **Style**: [Architecture style]
- **Stack**: [Technology stack]
- **Patterns**: [Selected design patterns]

### Mandatory Standards
✅ Design Patterns: [Count] patterns defined
✅ Clean Code: Principles enforced
✅ SOLID: All principles required
✅ Scalability Rules: [Count] rules defined

### Documents Generated
- [architecture.md](agent/agentflow/teste-1/architecture.md)

### Next Steps
Choose one:
1. **Create Technical Plan** - Generate detailed implementation plan
2. **Create Specification** - Write detailed feature specification
3. **Refine Architecture** - Make changes to architecture document
```

Present handoff options to user for next step.

## Key Rules

- **Never skip user input** - Architecture requires explicit user decisions
- **Enforce mandatory patterns** - Always include design patterns, Clean Code, SOLID
- **Document rationale** - Every decision must have reasoning
- **Focus on scalability** - All rules must support project growth
- **Be specific** - Provide concrete examples, not just theory
- **Validate completeness** - Ensure all template sections are filled
- **Maintain consistency** - Architecture must align with requirements
- **Update memory** - Always track decisions in constitution.md

## Validation Checklist

Before completing, verify:

- [ ] User provided architecture preferences
- [ ] Requirements document was reviewed
- [ ] Architecture style is clearly defined
- [ ] Technology stack is complete and justified
- [ ] 3-5 design patterns selected with usage examples
- [ ] Clean Code principles documented with rules
- [ ] All 5 SOLID principles enforced
- [ ] Scalability rules defined (min 5 rules)
- [ ] Maintainability rules defined (min 5 rules)
- [ ] Security rules included
- [ ] Performance targets set
- [ ] Error handling strategy defined
- [ ] Architecture document generated
- [ ] Memory/constitution.md updated
- [ ] Next steps presented to user

## Error Handling

### Missing Requirements

If requirements document not found:
- Warn user that architecture should follow requirements
- Ask if they want to proceed anyway or run requirements agent first

### Incomplete User Input

If user didn't provide enough architecture details:
- Ask specific, targeted questions
- Provide examples to guide user
- Don't proceed until critical information is gathered

### Invalid Architecture Choices

If user's choices conflict with requirements:
- Highlight the conflicts
- Suggest alternatives
- Explain trade-offs
- Get user confirmation before proceeding
