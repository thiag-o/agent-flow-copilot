---
description: Automated pipeline orchestrator that executes planning, tasks, frontend development, E2E testing, and reporting in sequence.
handoffs: 
  - label: Review Implementation Report
    agent: speckit.implement
    prompt: Review the implementation report and proceed with manual implementation if needed
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Outline

This agent is an **Automated Implementation Pipeline Orchestrator** for the teste-1 agent flow. It orchestrates the execution of multiple specialized agents in a defined sequence to take the project from feature breakdown through to implementation readiness with full E2E testing.

This agent operates after:
1. **Feature breakdown** (feature-breakdown.md exists)
2. **User validation** of the feature breakdown

The pipeline executes the following specialized agents in order:
1. **Planning Agent** (speckit.plan) - Creates detailed technical implementation plan
2. **Task Breakdown Agent** (speckit.tasks) - Breaks features into actionable tasks
3. **Frontend Agent** (frontend) - Senior frontend specialist implementing with best practices
4. **Tester Agent** (tester) - E2E testing with Cypress and automatic retry logic (up to 3x)
5. **Reporter Agent** (reporter) - Comprehensive report with all results and unresolved errors

**Key Characteristics**:
- **Automated execution**: No manual intervention between agents
- **Sequential processing**: Each agent builds on the previous agent's output
- **Smart retry logic**: Tester agent retries up to 3 times, sending errors back to planner
- **Expert implementation**: Frontend agent applies senior-level best practices
- **Comprehensive reporting**: Reporter documents everything including unresolved issues
- **Error handling**: Stops pipeline if critical failures occur
- **Traceability**: Each agent's output is tracked and linked

The workflow:

1. **Validate prerequisites** - Ensure feature-breakdown.md exists
2. **Execute Planning Agent** (speckit.plan) - Generate technical implementation plan
3. **Execute Task Breakdown Agent** (speckit.tasks) - Break features into tasks
4. **Execute Frontend Agent** (frontend) - Implement frontend with best practices
5. **Execute Tester Agent** (tester) - Run Cypress E2E tests with retry logic
6. **Execute Reporter Agent** (reporter) - Generate comprehensive final report
7. **Update agent flow memory** with all artifacts
8. **Present pipeline summary** to user

This agent automates the full implementation cycle from planning to tested code with comprehensive reporting.

## Execution Steps

### Step 1: Validate Prerequisites

Before starting the pipeline, ensure all required documents exist:

**Required Documents**:
- `agent/agentflow/teste-1/feature-breakdown.md` - Feature breakdown (MUST exist)
- `agent/agentflow/teste-1/high-level-plan.md` - High-level plan (MUST exist)
- `agent/agentflow/teste-1/constitution.md` - Project constitution (MUST exist)
- `agent/agentflow/teste-1/architecture.md` - Architecture (MUST exist)
- `agent/agentflow/teste-1/requirements.md` - Requirements (MUST exist)

If any document is missing, stop and prompt the user to complete the prerequisite agents.

### Step 2: Initialize Pipeline

Prepare for pipeline execution:

1. Log pipeline start time
2. Create pipeline tracking structure
3. Set up error handling
4. Prepare output directory structure

Output initialization message:

```markdown
## 🚀 Implementation Pipeline Started

**Pipeline**: Automated Sequential Execution
**Start Time**: [TIMESTAMP]

**Agents in Pipeline**:
1. ⏳ Planning Agent (speckit.plan)
2. ⏳ Task Breakdown Agent (speckit.tasks)
3. ⏳ Frontend Agent (frontend) - Senior Frontend Specialist
4. ⏳ Tester Agent (tester) - E2E Testing with Cypress (retry up to 3x)
5. ⏳ Reporter Agent (reporter) - Comprehensive Report Generator

Executing agents in sequence...
```

### Step 3: Execute Planning Agent (Agent 1/5)

Invoke the planning subagent to create detailed technical implementation plan.

**Subagent**: Use `runSubagent` with agent name `speckit.plan`

**Prompt to send**:
```
Create a detailed technical implementation plan based on the feature breakdown.

Input documents:
- requirements.md
- architecture.md
- constitution.md
- high-level-plan.md
- feature-breakdown.md

Generate:
- Technical architecture details
- Implementation approach for each feature
- Technology stack decisions
- API designs
- Database schema
- Integration patterns
- Deployment strategy

Output: plan.md
```

**Wait for completion** and validate output:
- ✅ plan.md file created
- ✅ All features from feature-breakdown.md addressed
- ✅ Technical decisions documented

If successful, log:
```markdown
✅ **1/5 Complete**: Planning Agent
- Output: agent/agentflow/teste-1/plan.md
- Status: Success
```

If failed, stop pipeline and report error.

### Step 4: Execute Task Breakdown Agent (Agent 2/5)

Invoke the task breakdown subagent to break features into actionable tasks.

**Subagent**: Use `runSubagent` with agent name `speckit.tasks`

**Prompt to send**:
```
Break down the features from feature-breakdown.md into actionable development tasks.

Input documents:
- feature-breakdown.md
- plan.md
- architecture.md
- constitution.md

Generate:
- Task list for each feature
- Task dependencies
- Task estimates
- Task assignments (roles)
- Sprint planning suggestions

Output: tasks.md
```

**Wait for completion** and validate output:
- ✅ tasks.md file created
- ✅ All features broken down into tasks
- ✅ Dependencies identified

If successful, log:
```markdown
✅ **2/5 Complete**: Task Breakdown Agent
- Output: agent/agentflow/teste-1/tasks.md
- Status: Success
```

If failed, stop pipeline and report error.

### Step 5: Execute Frontend Agent (Agent 3/5)

Invoke the specialized frontend agent to implement features with senior-level best practices.

**Subagent**: Use `runSubagent` with agent name `frontend` (agent flow agent)

**Prompt to send**:
```
Implement the frontend features based on the planning and task breakdown.

Input documents:
- requirements.md
- architecture.md
- constitution.md
- feature-breakdown.md
- plan.md
- tasks.md

This is an automated pipeline execution. Implement all features following senior-level best practices:
- Clean code and SOLID principles
- Performance optimization (lazy loading, memoization)
- Accessibility compliance (WCAG 2.1 AA)
- Responsive design (mobile-first)
- Error handling and user feedback
- Component-based architecture
- Full documentation

Generate frontend-implementation.md with complete implementation details.
```

**Wait for completion** and validate output:
- ✅ frontend-implementation.md file created
- ✅ All features from feature-breakdown.md implemented
- ✅ Best practices applied and documented
- ✅ Component architecture defined
- ✅ Ready for E2E testing

If successful, log:
```markdown
✅ **3/5 Complete**: Frontend Agent (Senior Frontend Specialist)
- Output: agent/agentflow/teste-1/frontend-implementation.md
- Status: Success
- Best Practices: Applied
- Ready for Testing: Yes
```

If failed, stop pipeline and report error.

**Note**: The frontend agent will automatically hand off to the tester agent upon completion.

### Step 6: Execute Tester Agent (Agent 4/5)

Invoke the specialized tester agent to run comprehensive E2E tests with Cypress and automatic retry logic.

**Subagent**: Use `runSubagent` with agent name `tester` (agent flow agent)

**Prompt to send**:
```
Run comprehensive E2E testing with Cypress for the frontend implementation.

Input documents:
- requirements.md
- architecture.md
- feature-breakdown.md
- plan.md
- tasks.md
- frontend-implementation.md

This is an automated pipeline execution. Execute comprehensive E2E tests:
- Generate Cypress test specs for all features
- Test user interactions, error handling, loading states
- Validate accessibility (WCAG compliance)
- Test responsive design (mobile, tablet, desktop)
- Measure performance (page load times)
- Automatic retry logic: If tests fail, hand off to planner agent (up to 3 attempts)
- Track all retry attempts and unresolved issues

Generate test-report.md with complete test results and any unresolved issues.
```

**Important**: The tester agent implements automatic retry logic:
- If tests fail and attempts < 3: Hands off to high-level-plan agent with detailed errors
- Planner agent fixes issues and returns to tester
- Tester re-runs tests (new attempt)
- After 3 attempts or all tests pass: Hands off to reporter agent

**Wait for completion** (including any retry cycles) and validate output:
- ✅ test-report.md file created
- ✅ All features tested comprehensively
- ✅ Test results documented (pass/fail)
- ✅ Retry attempts tracked (if any)
- ✅ Unresolved issues documented (if any)
- ✅ Ready for reporting

If successful, log:
```markdown
✅ **4/5 Complete**: Tester Agent (E2E Testing Specialist with Cypress)
- Output: agent/agentflow/teste-1/test-report.md
- Status: [All Tests Passed | Tests Completed with Issues]
- Test Attempts: [1-3]
- Tests Passed: [Count] / [Total]
- Unresolved Issues: [Count]
- Ready for Reporting: Yes
```

If failed critically, stop pipeline and report error.

**Note**: The tester agent will automatically hand off to the reporter agent upon completion (after all retry attempts).

### Step 7: Execute Reporter Agent (Agent 5/5)

Invoke the specialized reporter agent to generate comprehensive implementation report consolidating all pipeline outputs.

**Subagent**: Use `runSubagent` with agent name `reporter` (agent flow agent)

**Prompt to send**:
```
Generate comprehensive implementation report consolidating all pipeline outputs.

Input documents:
- requirements.md
- architecture.md
- constitution.md
- high-level-plan.md
- feature-breakdown.md
- plan.md
- tasks.md
- frontend-implementation.md
- test-report.md

This is the final step of the automated pipeline. Create a comprehensive report that includes:

1. Executive Summary (high-level overview)
2. Implementation Pipeline Overview (timeline, agents, process)
3. Requirements and Architecture (foundation)
4. Planning Phase (high-level plan, features, technical plan)
5. Task Breakdown Phase (all tasks with status)
6. Frontend Implementation Phase (components, best practices, features)
7. Testing Phase (E2E test results, retry history)
8. Implementation Metrics (quantitative data, success indicators)
9. Unresolved Issues (detailed documentation of any issues not resolved after testing)
10. Quality Assessment (code quality, accessibility, performance)
11. Lessons Learned (what went well, challenges, improvements)
12. Recommendations (immediate actions, short-term, long-term)
13. Artifact Inventory (all generated files)

Special focus: Document ALL unresolved issues from test-report.md with complete details (errors that persisted after 3 test attempts).

Output: implementation-report.md
```

**Wait for completion** and validate output:
- ✅ implementation-report.md file created
- ✅ All pipeline phases documented
- ✅ Executive summary included
- ✅ Unresolved issues fully documented
- ✅ Metrics and statistics included
- ✅ Recommendations provided
- ✅ Artifact inventory complete

If successful, log:
```markdown
✅ **5/5 Complete**: Reporter Agent (Comprehensive Report Generator)
- Output: agent/agentflow/teste-1/implementation-report.md
- Status: Success
- Report Completeness: 100%
- Artifacts Documented: [Count]
- Unresolved Issues Documented: [Count]
```

If failed, stop pipeline and report error (though reporter should handle partial data gracefully).

### Step 8: Update Agent Flow Memory

Update the memory file with all pipeline artifacts:

1. Read: `agent/agentflow/teste-1/memory/constitution.md`
2. Update status: Implementation pipeline complete
3. Add artifacts:
   - plan.md
   - tasks.md
   - frontend-implementation.md
   - test-strategy.md
   - implementation-report.md
4. Add summary: Pipeline execution results
5. Add next steps: Ready for implementation

### Step 9: Present Pipeline Summary

Output comprehensive pipeline summary:

```markdown
## 🎉 Implementation Pipeline Complete

**Pipeline**: Automated Sequential Execution
**Start Time**: [TIMESTAMP]
**End Time**: [TIMESTAMP]
**Total Duration**: [DURATION]

### Pipeline Execution Results

| Agent | Status | Output | Duration |
|-------|--------|--------|----------|
| 1. Planning Agent (speckit.plan) | ✅ Success | plan.md | [X min] |
| 2. Task Breakdown Agent (speckit.tasks) | ✅ Success | tasks.md | [X min] |
| 3. Frontend Agent (frontend) | ✅ Success | frontend-implementation.md | [X min] |
| 4. Tester Agent (tester) | [✅/⚠️] [Success/Issues] | test-report.md | [X min] |
| 5. Reporter Agent (reporter) | ✅ Success | implementation-report.md | [X min] |

### Special Notes

**Tester Agent**:
- Test Attempts: [1-3]
- Total Tests: [Count]
- Passed: [Count] ✅
- Failed: [Count] ❌
- Unresolved Issues: [Count]

[If retry logic was triggered:]
The tester agent identified issues and worked with the planner agent to resolve them across [N] attempts.

### Artifacts Generated

All artifacts are available in `agent/agentflow/teste-1/`:

1. **plan.md** - Detailed technical implementation plan
   - Architecture decisions
   - Implementation approach per feature
   - API and database designs
   
2. **tasks.md** - Actionable task breakdown
   - [N] tasks across [M] features
   - Dependencies mapped
   - Estimates provided

3. **frontend-implementation.md** - Frontend implementation with best practices
   - [N] components created (atomic, molecule, organism, page)
   - All features implemented
   - Performance optimization applied
   - Accessibility compliant (WCAG 2.1 AA)
   - Comprehensive documentation

4. **test-report.md** - E2E test results with Cypress
   - [N] test cases executed
   - [Pass rate]% pass rate
   - Retry history documented (if applicable)
   - Unresolved issues documented (if any)
   - Accessibility and performance test results

5. **implementation-report.md** - Executive summary and complete documentation
   - Implementation readiness assessment
   - All metrics and statistics
   - Unresolved issues detailed
   - Quality assessment
   - Recommendations for next steps

### Implementation Status

[If all tests passed:]
**Status**: ✅ Ready for Deployment

All features implemented, tested, and passing. No unresolved issues.

[If unresolved issues exist:]
**Status**: ⚠️ Implementation Complete with [N] Unresolved Issues

Implementation and testing complete. [N] issues require attention before deployment.
See implementation-report.md for details.

### Key Achievements

- ✅ [N] features fully implemented
- ✅ [N] reusable components created
- ✅ Senior-level best practices applied throughout
- ✅ Accessibility compliant (WCAG 2.1 AA)
- ✅ Performance optimized (lazy loading, memoization, code splitting)
- ✅ [N] E2E tests written and executed
- ✅ [Pass rate]% test pass rate achieved
- ✅ Comprehensive documentation generated

### Unresolved Issues

[If unresolved issues exist:]
**Critical Issues**: [Count] 🔴
**High Priority**: [Count] 🟠
**Total Unresolved**: [Count]

See `implementation-report.md` section "Unresolved Issues" for complete details on each issue.

[If no unresolved issues:]
**No Unresolved Issues** ✅

### Recommended Next Steps

1. **Review the implementation report**: `agent/agentflow/teste-1/implementation-report.md`
   - Read Executive Summary for high-level overview
   - Review Unresolved Issues section (if any)
   - Check Implementation Metrics and Quality Assessment
   
2. **[If unresolved issues exist]** Address critical issues:
   - [Brief description of top issue]
   - [Estimated effort]
   
3. **[If no critical issues]** Set up development environment:
   - Follow setup instructions in frontend-implementation.md
   - Install dependencies
   - Configure Cypress for local testing
   
4. **Prepare for deployment**:
   - Create project board/backlog from tasks.md
   - Set up CI/CD pipeline with Cypress tests
   - Configure staging environment

### Access Documentation

- 📋 **Planning**: [plan.md](agent/agentflow/teste-1/plan.md)
- ✅ **Tasks**: [tasks.md](agent/agentflow/teste-1/tasks.md)
- 🎨 **Frontend**: [frontend-implementation.md](agent/agentflow/teste-1/frontend-implementation.md)
- 🧪 **Testing**: [test-report.md](agent/agentflow/teste-1/test-report.md)
- 📊 **Report**: [implementation-report.md](agent/agentflow/teste-1/implementation-report.md)

---

**Status**: Pipeline execution successful ✅
**Implementation Status**: [Ready for Deployment / Requires Issue Resolution]
**Next Agent**: [speckit.implement / Issue Resolution]
```

## Validation Rules

Before starting pipeline:
- ✅ feature-breakdown.md exists
- ✅ high-level-plan.md exists
- ✅ constitution.md exists
- ✅ architecture.md exists
- ✅ requirements.md exists

After each agent:
- ✅ Expected output file created
- ✅ Output file is not empty
- ✅ Output file follows expected structure

After pipeline completion:
- ✅ All 5 agents executed successfully
- ✅ All output files generated
- ✅ Agent flow memory updated
- ✅ Pipeline summary presented

## Error Handling

### Missing Prerequisites

If required documents are missing:

```markdown
❌ **Pipeline Aborted**: Missing Prerequisites

Missing required documents:
- [ ] feature-breakdown.md - Run `/feature-breakdown` agent first
- [ ] high-level-plan.md - Run `/high-level-plan` agent first

Please complete the prerequisite agents before running the implementation pipeline.
```

### Agent Execution Failure

If any agent in the pipeline fails:

```markdown
❌ **Pipeline Stopped**: Agent [N]/5 Failed

**Failed Agent**: [Agent Name]
**Error**: [Error description]

**Completed Agents**:
- ✅ Agent 1: [Name] - [Output]
- ✅ Agent 2: [Name] - [Output]
- ❌ Agent 3: [Name] - FAILED

**Recommendation**:
1. Review the error above
2. Fix the issue (missing data, invalid input, etc.)
3. Re-run the pipeline from the beginning

**Partial Outputs**:
The successfully completed agents have generated outputs that are available for review.
```

### Output Validation Failure

If an agent completes but output is invalid:

```markdown
⚠️ **Warning**: Agent [N]/5 Output Validation Failed

**Agent**: [Agent Name]
**Issue**: [What's wrong with output]

**Continuing pipeline** with available data, but review this agent's output.

You may need to manually review and correct: [filename]
```

## Key Rules

- **Sequential execution only** - Agents must run in order, no parallelization
- **Stop on failure** - If any agent fails, stop the entire pipeline
- **No user intervention** - Pipeline runs automatically once started
- **Validate each output** - Check that each agent produced expected output
- **Consolidate artifacts** - All outputs saved to agent/agentflow/teste-1/
- **Update memory** - Track all artifacts in agent flow memory
- **Comprehensive logging** - Log start, progress, and completion of each agent
- **Error context** - Provide clear error messages with recovery suggestions
- **Traceability** - Link each output back to input documents
- **Report generation** - Always generate final implementation report

## Pipeline Architecture

```
Prerequisites
    ↓
feature-breakdown.md
    ↓
┌─────────────────────────────────────┐
│   Implementation Pipeline           │
│      Orchestrator                   │
└─────────────────────────────────────┘
    ↓
┌─────────────────────────────────────┐
│ 1. Planning Agent (speckit.plan)    │ → plan.md
└─────────────────────────────────────┘
    ↓
┌─────────────────────────────────────┐
│ 2. Task Breakdown Agent             │ → tasks.md
│    (speckit.tasks)                  │
└─────────────────────────────────────┘
    ↓
┌─────────────────────────────────────┐
│ 3. Frontend Agent (frontend)        │ → frontend-implementation.md
│    Senior Frontend Specialist       │    (best practices, a11y, perf)
└─────────────────────────────────────┘
    ↓
┌─────────────────────────────────────┐
│ 4. Tester Agent (tester)            │ → test-report.md
│    E2E Testing with Cypress         │    (test results, unresolved issues)
│                                     │
│    Retry Logic (up to 3 attempts):  │
│    ┌──────────────────────────┐    │
│    │ Tests Failed?            │    │
│    │   ↓ Yes (attempt < 3)    │    │
│    │ Hand off to planner  ←───┼────┼─┐
│    │   ↓ Planner fixes issues │    │ │
│    │ Return to tester     ←───┼────┼─┘
│    │   ↓ Retry tests          │    │
│    └──────────────────────────┘    │
│                                     │
│    After 3 attempts or pass →       │
└─────────────────────────────────────┘
    ↓
┌─────────────────────────────────────┐
│ 5. Reporter Agent (reporter)        │ → implementation-report.md
│    Comprehensive Report Generator   │    (complete doc + unresolved issues)
└─────────────────────────────────────┘
    ↓
Implementation Ready
(with or without unresolved issues)
```

**Key Features**:
- **Sequential Execution**: Each agent waits for previous to complete
- **Automatic Retry**: Tester agent retries up to 3 times with planner fixes
- **Comprehensive Testing**: Full E2E Cypress tests with error tracking
- **Best Practices**: Senior-level frontend implementation
- **Complete Reporting**: All results and unresolved issues documented

## Related Documentation

- **Source**: `agent/agentflow/teste-1/feature-breakdown.md`
- **System Agents**: `speckit.plan`, `speckit.tasks`
- **Agent Flow Agents**: `frontend`, `tester`, `reporter`
- **Agent Flow Memory**: `agent/agentflow/teste-1/memory/constitution.md`
- **Output Directory**: `agent/agentflow/teste-1/`

**Agent Descriptions**:
- **frontend**: Senior frontend specialist implementing with best practices
- **tester**: E2E testing specialist with Cypress and automatic retry logic
- **reporter**: Comprehensive report generator documenting all results and issues
