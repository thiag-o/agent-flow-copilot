# Requirements Document: [PROJECT/FEATURE NAME]

**Workflow**: [workflow-name]  
**Created**: [DATE]  
**Status**: Draft  
**Analyzed By**: speckit.requirements agent  
**Source Prompt**: "[USER_PROMPT]"

---

## Executive Summary

<!--
  Provide a brief 2-3 paragraph summary of:
  - What is being built and why
  - Who are the primary stakeholders/users
  - What are the main goals and expected outcomes
  - High-level scope (what's included, what's not)
-->

[Brief description of the project/feature, the problem it solves, and the expected value it delivers]

### Key Objectives

1. [Primary objective]
2. [Secondary objective]
3. [Tertiary objective]

### Success Metrics

- [Metric 1]: [Target value]
- [Metric 2]: [Target value]
- [Metric 3]: [Target value]

---

## Stakeholders

### Primary Users
- [User type 1]: [Description and needs]
- [User type 2]: [Description and needs]

### Secondary Stakeholders
- [Stakeholder 1]: [Role and interest]
- [Stakeholder 2]: [Role and interest]

---

## Functional Requirements

<!--
  MANDATORY: List all functional requirements (what the system DOES)
  Format: FR[id] - [Priority] - [Requirement description]
  
  Priority levels:
  - P1 (Critical): Must-have for MVP, blocking
  - P2 (Important): Should-have, adds significant value
  - P3 (Nice-to-have): Could-have, enhances experience
  - P4 (Future): Won't-have in first release
-->

### FR1 - [Priority: P1] - [Requirement Title]

**Description**: [Clear, concise description of what the system must do]

**Rationale**: [Why is this requirement needed? What problem does it solve?]

**Acceptance Criteria**:
1. Given [initial state], When [action], Then [expected outcome]
2. Given [initial state], When [action], Then [expected outcome]

**Source**: [Reference to user prompt or stakeholder input]

**Dependencies**: [List any other requirements this depends on, e.g., FR3, NFR2]

**Assumptions**: [Any assumptions made about this requirement]

---

### FR2 - [Priority: P1] - [Requirement Title]

**Description**: [Clear, concise description]

**Rationale**: [Why is this needed?]

**Acceptance Criteria**:
1. Given [initial state], When [action], Then [expected outcome]
2. Given [initial state], When [action], Then [expected outcome]

**Source**: [Reference to user prompt]

**Dependencies**: [Dependencies]

**Assumptions**: [Assumptions]

---

### FR3 - [Priority: P2] - [Requirement Title]

**Description**: [Clear, concise description]

**Rationale**: [Why is this needed?]

**Acceptance Criteria**:
1. Given [initial state], When [action], Then [expected outcome]

**Source**: [Reference to user prompt]

**Dependencies**: [Dependencies]

**Assumptions**: [Assumptions]

---

<!-- Add more functional requirements as needed -->

---

## Non-Functional Requirements

<!--
  MANDATORY: List all non-functional requirements (HOW the system performs)
  Categories: Performance, Scalability, Security, Usability, Reliability, Maintainability, Compatibility
-->

### Performance

#### NFR1 - [Priority: P1] - [Performance Requirement]

**Description**: [Specific performance requirement with measurable criteria]

**Rationale**: [Why this performance level is needed]

**Measurement**: [How this will be measured and validated]

**Target**: [Specific numeric target, e.g., "< 200ms response time", "1000 requests/second"]

**Dependencies**: [Related requirements]

---

### Scalability

#### NFR2 - [Priority: P1] - [Scalability Requirement]

**Description**: [Specific scalability requirement]

**Rationale**: [Why this scale is needed]

**Measurement**: [How this will be measured]

**Target**: [Specific numeric target, e.g., "Support 10,000 concurrent users"]

**Dependencies**: [Related requirements]

---

### Security

#### NFR3 - [Priority: P1] - [Security Requirement]

**Description**: [Specific security requirement]

**Rationale**: [Why this security measure is needed]

**Standards**: [Any security standards to comply with, e.g., OWASP, GDPR, HIPAA]

**Validation**: [How security will be validated]

**Dependencies**: [Related requirements]

---

### Usability

#### NFR4 - [Priority: P2] - [Usability Requirement]

**Description**: [Specific usability requirement]

**Rationale**: [Why this matters for users]

**Measurement**: [How usability will be measured, e.g., user testing, surveys]

**Target**: [Specific target, e.g., "95% task completion rate"]

**Dependencies**: [Related requirements]

---

### Reliability

#### NFR5 - [Priority: P1] - [Reliability Requirement]

**Description**: [Specific reliability requirement]

**Rationale**: [Why this reliability level is needed]

**Measurement**: [How reliability will be measured]

**Target**: [Specific target, e.g., "99.9% uptime", "< 0.1% error rate"]

**Dependencies**: [Related requirements]

---

### Maintainability

#### NFR6 - [Priority: P2] - [Maintainability Requirement]

**Description**: [Specific maintainability requirement]

**Rationale**: [Why this matters for long-term success]

**Practices**: [Specific practices to follow, e.g., code reviews, documentation standards]

**Dependencies**: [Related requirements]

---

### Compatibility

#### NFR7 - [Priority: P2] - [Compatibility Requirement]

**Description**: [Specific compatibility requirement]

**Rationale**: [Why this compatibility is needed]

**Supported**: [List of supported platforms, browsers, devices, etc.]

**Dependencies**: [Related requirements]

---

<!-- Add more non-functional requirements as needed -->

---

## Technical Constraints

<!--
  Document any technical limitations, technology choices, or constraints
-->

### TC1 - [Priority: P1] - [Technical Constraint Title]

**Description**: [What is the constraint?]

**Rationale**: [Why does this constraint exist?]

**Impact**: [How does this affect the implementation?]

**Alternatives Considered**: [What other options were considered and why were they rejected?]

---

### TC2 - [Priority: P1] - [Technical Constraint Title]

**Description**: [What is the constraint?]

**Rationale**: [Why does this constraint exist?]

**Impact**: [How does this affect the implementation?]

**Alternatives Considered**: [Alternatives]

---

<!-- Add more technical constraints as needed -->

---

## Business Requirements

<!--
  Document business rules, constraints, and requirements
-->

### BR1 - [Priority: P1] - [Business Requirement Title]

**Description**: [What is the business requirement?]

**Rationale**: [Why is this important for the business?]

**Success Criteria**: [How will success be measured?]

**ROI/Value**: [Expected return or business value]

---

### BR2 - [Priority: P2] - [Business Requirement Title]

**Description**: [What is the business requirement?]

**Rationale**: [Why is this important?]

**Success Criteria**: [Success metrics]

**ROI/Value**: [Expected value]

---

<!-- Add more business requirements as needed -->

---

## Dependencies

<!--
  Map out dependencies between requirements and external systems
-->

### Internal Dependencies

| Requirement | Depends On | Type | Notes |
|-------------|------------|------|-------|
| FR3 | FR1, FR2 | Requires | FR3 cannot be implemented without FR1 and FR2 |
| NFR2 | NFR1 | Supports | Scalability builds on performance foundation |
| [Req ID] | [Req ID] | [Type] | [Notes] |

### External Dependencies

| Description | Provider | Status | Risk Level | Mitigation |
|-------------|----------|--------|------------|------------|
| [External system/API] | [Provider name] | [Available/Pending/Unknown] | [Low/Medium/High] | [Mitigation plan] |
| [Third-party service] | [Provider name] | [Status] | [Risk level] | [Mitigation] |

---

## Assumptions

<!--
  Document all assumptions made during requirements analysis
  These should be validated with stakeholders
-->

1. **[Assumption 1]**: [Description of what we're assuming]
   - **Impact if wrong**: [What happens if this assumption is incorrect]
   - **Validation needed**: [How to validate this assumption]

2. **[Assumption 2]**: [Description]
   - **Impact if wrong**: [Impact]
   - **Validation needed**: [Validation method]

3. **[Assumption 3]**: [Description]
   - **Impact if wrong**: [Impact]
   - **Validation needed**: [Validation method]

---

## Risks

<!--
  Identify potential risks that could affect requirements or implementation
-->

### Risk 1: [Risk Title]

**Description**: [What is the risk?]

**Probability**: [Low/Medium/High]

**Impact**: [Low/Medium/High]

**Mitigation Strategy**: [How will we mitigate or manage this risk?]

**Owner**: [Who is responsible for managing this risk?]

---

### Risk 2: [Risk Title]

**Description**: [What is the risk?]

**Probability**: [Low/Medium/High]

**Impact**: [Low/Medium/High]

**Mitigation Strategy**: [Mitigation approach]

**Owner**: [Responsible party]

---

<!-- Add more risks as needed -->

---

## Open Questions

<!--
  List questions that need to be answered before requirements are finalized
  Update this section as questions are answered
-->

### High Priority Questions

1. **[Question 1]**
   - **Affects**: [Which requirements or decisions this impacts]
   - **Asked to**: [Who should answer this]
   - **By when**: [Deadline for answer]
   - **Status**: [Open/Answered/Deferred]

2. **[Question 2]**
   - **Affects**: [Impact]
   - **Asked to**: [Stakeholder]
   - **By when**: [Deadline]
   - **Status**: [Status]

### Medium Priority Questions

1. **[Question 3]**
   - **Affects**: [Impact]
   - **Asked to**: [Stakeholder]
   - **By when**: [Deadline]
   - **Status**: [Status]

---

## Out of Scope

<!--
  Explicitly document what is NOT included in this project/feature
  This is important to manage expectations and prevent scope creep
-->

The following items are explicitly **out of scope** for this project:

1. [Out of scope item 1] - [Why it's out of scope]
2. [Out of scope item 2] - [Reason]
3. [Out of scope item 3] - [Reason]

---

## Requirements Summary

<!--
  This section is auto-generated or manually updated for quick reference
-->

### By Priority

| Priority | Functional | Non-Functional | Technical | Business | Total |
|----------|-----------|----------------|-----------|----------|-------|
| P1 | [count] | [count] | [count] | [count] | [total] |
| P2 | [count] | [count] | [count] | [count] | [total] |
| P3 | [count] | [count] | [count] | [count] | [total] |
| P4 | [count] | [count] | [count] | [count] | [total] |
| **Total** | [total] | [total] | [total] | [total] | [grand total] |

### By Category

- **Functional Requirements**: [count] ([P1 count] critical)
- **Non-Functional Requirements**: [count] ([P1 count] critical)
- **Technical Constraints**: [count] ([P1 count] critical)
- **Business Requirements**: [count] ([P1 count] critical)

---

## Traceability Matrix

<!--
  Map requirements to user stories, test cases, and implementation tasks
  This section can be updated as the project progresses
-->

| Req ID | Requirement | User Story | Test Cases | Implementation Tasks | Status |
|--------|-------------|------------|------------|---------------------|---------|
| FR1 | [Brief description] | US-001 | TC-001, TC-002 | TASK-001 | [Not Started/In Progress/Done] |
| FR2 | [Brief description] | US-001 | TC-003 | TASK-002 | [Status] |
| NFR1 | [Brief description] | - | TC-004 | TASK-003 | [Status] |

---

## Approval

<!--
  Track who has reviewed and approved these requirements
-->

| Stakeholder | Role | Review Date | Status | Comments |
|-------------|------|-------------|--------|----------|
| [Name] | [Role] | [Date] | [Approved/Rejected/Pending] | [Comments] |
| [Name] | [Role] | [Date] | [Status] | [Comments] |

---

## Change Log

<!--
  Track changes to requirements over time
-->

| Date | Version | Changed By | Changes | Reason |
|------|---------|------------|---------|--------|
| [Date] | 1.0 | [Agent/Person] | Initial draft | Requirements analysis from user prompt |
| [Date] | [Version] | [Who] | [What changed] | [Why] |

---

## Next Steps

<!--
  Recommended actions after requirements are finalized
-->

1. **Validate Assumptions**: Review and validate all assumptions with stakeholders
2. **Answer Open Questions**: Get answers to all high-priority questions
3. **Stakeholder Review**: Get approval from all key stakeholders
4. **Create Technical Plan**: Use `/speckit.plan` to create implementation plan
5. **Create Specification**: Use `/speckit.specify` to create detailed feature specification
6. **Generate Tasks**: Break down requirements into actionable tasks

---

## Notes

<!--
  Any additional notes, observations, or context that doesn't fit elsewhere
-->

[Add any additional notes here]
