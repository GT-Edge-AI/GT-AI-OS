# Mock Assessments Workflow

## Start Here

1. Identify the assessment rubric or scenario your tenant uses (check with your tenant manager for the published **evaluation** or mock-assessment agent configuration).
2. Create or select a dataset with the source material the assessment should reference (policies, prior reports, scenario injects).
3. Open [GT Chat](gen3/chat) and select an agent configured for assessment or evaluation prompts.
4. Attach the dataset with the **paperclip** when the scenario requires document context.
5. Run the assessment prompt sequence (scenario setup, timed responses, grading questions) and save the conversation for review in [Conversations](gen3/conversations).

![Paperclip control in GT Chat for attaching assessment datasets](gen3/images/chat-paperclip.png)

## Why this matters

Mock assessments train operators and validate agent behavior before live events. GT3 keeps assessment traffic inside normal chat, datasets, and observability boundaries so tenant managers can review usage and outcomes without a separate product silo.

## Details

### Preparation

- Align with [Tenant Administration](gen3/tenant-admin) on which agents are approved for assessment use.
- Pre-stage datasets so participants are not blocked by upload processing during timed drills.
- Use [Observability](gen3/observability) (tenant manager scope) to review conversation volume and outcomes after exercises.

### Running the exercise

- Start a **new conversation** per participant or per scenario inject when you need clean scoring boundaries.
- Keep prompts explicit about role, constraints, and deliverable format.
- Use assistant message **Report** actions in chat when an answer must be escalated to support or leadership.

### After action review

- Export or reopen threads from [Conversations](gen3/conversations).
- Update agent instructions in [Building Agents](gen3/agents/building) when rubric gaps appear repeatedly.
- Share improved agents or datasets through [Groups](gen3/groups) for team-wide drills.

### Related workflows

- [Document Review](gen3/workflows/document-review)
- [Diagram Review](gen3/workflows/diagram-review)
- [GT Helper](gen3/agents/helper-agent) — ask how to configure assessment agents in your tenant
