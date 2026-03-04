# Agent Creation Template

<!-- 
This template guides the creation of new SpecKit agents.
Use this when creating agents via speckit.agentforge or manually.
Placeholders marked with [BRACKETS] should be replaced with actual content.
-->

```chatagent
---
description: [One-line description of what this agent does - max 100 chars]
handoffs:
  - label: [Human-readable action description]
    agent: [target.agent.name]
    prompt: [Default prompt text to send to target agent]
    send: [true|false - optional, auto-forward if true]
  # Add more handoffs as needed
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Outline

[High-level description of what this agent does and how it fits in the SpecKit workflow]

Key responsibilities:
1. [Primary responsibility]
2. [Secondary responsibility]
3. [Additional responsibilities...]

Interactions:
- **Receives from**: [Which agents/users trigger this agent]
- **Sends to**: [Which agents this hands off to]
- **Reads**: [Which files/artifacts it consumes]
- **Writes**: [Which files/artifacts it produces]

## Prerequisites

<!-- Define what must exist before this agent can run -->

**Required**:
- [Required file/state/condition]
- [Another requirement]

**Optional**:
- [Optional file that enhances functionality]
- [Optional condition for extended features]

**Validation**: 
```bash
# Command to validate prerequisites
[bash command or script call]
```

## Execution Steps

<!-- Main workflow - numbered steps the agent follows -->

### Step 1: [Initialize/Setup]

[Detailed instructions for initialization]

**Actions**:
1. [Specific action with command/tool]
2. [Another action]

**Validation**:
- ✅ [Check that something succeeded]
- ❌ ERROR if [failure condition]

### Step 2: [Core Processing]

[Main logic of the agent]

**Algorithm**:
```
1. [Pseudocode or structured steps]
2. IF [condition]:
     [action]
   ELSE:
     [alternative]
3. [Continue processing]
```

**Implementation**:
- [Specific implementation details]
- [Tool/command usage]
- [File operations]

### Step 3: [Generate Output]

[How the agent produces its results]

**Output Format**:
```markdown
[Example of expected output structure]
```

**File Operations**:
- Create: `[file path]` - [purpose]
- Update: `[file path]` - [what changes]
- Read: `[file path]` - [what information extracted]

### Step 4: [Finalize/Report]

[How the agent completes and communicates results]

**Success Criteria**:
- [Condition 1 for success]
- [Condition 2 for success]

**Output Message**:
```
[Template of completion message to user]
```

## Domain-Specific Logic

<!-- Add sections specific to this agent's domain -->

### [Domain Concept 1]

[Explanation and implementation details]

### [Domain Concept 2]

[Explanation and implementation details]

## Error Handling

<!-- Define how errors are handled -->

| Error Type | Condition | Resolution |
|------------|-----------|------------|
| [Error category] | [When it occurs] | [How to handle/recover] |
| [Another error] | [Condition] | [Resolution] |

**Error Response Format**:
```
ERROR: [error type]
Cause: [what went wrong]
Solution: [how to fix]
```

## Integration Patterns

<!-- How this agent integrates with the SpecKit ecosystem -->

### Script Integration

```bash
# Existing scripts this agent uses
[script path and purpose]

# Command format
[example command with flags]
```

### File Integration

**Reads from**:
- `.specify/templates/[template-name]` - [purpose]
- `specs/[feature]/[artifact]` - [purpose]

**Writes to**:
- `specs/[feature]/[new-artifact]` - [purpose]
- `.specify/[location]/[file]` - [purpose]

### Agent Integration

**Flow Position**:
```
[Previous Agent] → [This Agent] → [Next Agent]
                        ↓
                  [Alternative Path]
```

**Handoff Protocol**:
- **From previous**: Receives [what data/state]
- **To next**: Passes [what data/state]

## Configuration Options

<!-- If agent behavior can be customized -->

| Option | Format | Default | Purpose |
|--------|--------|---------|---------|
| [option-name] | [type] | [default-value] | [what it controls] |

**Usage**:
```bash
[command with options example]
```

## Examples

<!-- Real-world usage examples -->

### Example 1: [Common Use Case]

**Input**:
```
[example user input]
```

**Process**:
1. [what happens step by step]
2. [intermediate states]
3. [final outcome]

**Output**:
```
[example output]
```

### Example 2: [Edge Case]

**Input**:
```
[edge case input]
```

**Expected Behavior**:
[how agent handles this case]

## Validation Rules

<!-- Rules the agent must enforce -->

### Input Validation

- ✅ [Required input check]
- ✅ [Format validation]
- ✅ [Constraint verification]

### Output Validation

- ✅ [Output completeness check]
- ✅ [Format correctness]
- ✅ [Quality gates]

### State Validation

- ✅ [System state check]
- ✅ [Dependency verification]
- ✅ [Consistency validation]

## Performance Considerations

<!-- If applicable -->

- **Time complexity**: [O(n) or description]
- **Space requirements**: [memory/disk usage]
- **Scalability limits**: [known constraints]
- **Optimization opportunities**: [potential improvements]

## Testing Guidelines

<!-- How to test this agent -->

### Unit Tests

**Test Cases**:
1. [Test case description] → Expected: [outcome]
2. [Another test case] → Expected: [outcome]

### Integration Tests

**Flow Tests**:
1. [Full workflow test] → Expected: [end-to-end result]
2. [Alternative path test] → Expected: [alternative result]

### Edge Cases

- [Edge case 1]: [expected behavior]
- [Edge case 2]: [expected behavior]

## Maintenance Notes

<!-- Information for future maintainers -->

### Known Limitations

- [Limitation 1 and why it exists]
- [Limitation 2 and potential workaround]

### Future Enhancements

- [ ] [Potential improvement 1]
- [ ] [Potential improvement 2]
- [ ] [Feature request consideration]

### Dependencies

**Internal**:
- [Other SpecKit agent/script] - [why needed]

**External**:
- [External tool/library] - [purpose]

### Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | [date] | Initial creation |

## Key Rules

<!-- Critical rules this agent must follow -->

- **MUST**: [Non-negotiable requirement]
- **MUST NOT**: [Prohibited action]
- **SHOULD**: [Strong recommendation]
- **MAY**: [Optional behavior]

## Related Documentation

<!-- Links to related files -->

- Related agents: [list agent files]
- Related templates: [list template files]
- Related scripts: [list script files]
- Related reports: [list documentation]

---

<!-- 
COMPLETION CHECKLIST FOR AGENT CREATORS:
- [ ] Description is clear and under 100 characters
- [ ] All handoffs reference valid agents
- [ ] User Input section is present
- [ ] Outline explains agent purpose and position
- [ ] Execution steps are numbered and detailed
- [ ] Error handling is comprehensive
- [ ] Examples demonstrate usage
- [ ] Validation rules are testable
- [ ] Integration patterns are documented
- [ ] File paths use absolute references
- [ ] No syntax errors in code blocks
- [ ] Companion prompt file created
- [ ] Related template created (if needed)
-->
```
