# Creating Agents

This guide walks you through creating custom agents in GT AI OS step by step.

## Prerequisites

- You need appropriate permissions to create agents
- Understand what task the agent should accomplish
- Have a clear idea of the agent's personality and behavior

## Creating a New Agent

### Step 1: Open the Creation Form

1. Go to **Agents** in the sidebar
2. Click the toggle to switch to **Agent Configuration** view (if in Favorites view)
3. Click **Create Agent**
4. The agent creation form opens

### Step 2: Basic Information

Fill in the required fields:

| Field | Required | Description | Example |
|-------|----------|-------------|---------|
| **Name** | Yes | Clear, descriptive name | "Customer Support - Technical" |
| **Description** | Yes | What this agent does | "Helps users troubleshoot technical issues" |
| **Category** | Yes | Select or create a category | "Technical", "General", "Creative" |
| **Tags** | No | Keywords for filtering | "support", "technical", "help" |

**Note**: Categories are customizable - you can create new ones or use existing categories your organization has set up.

### Step 3: System Prompt

The system prompt is the most important part - it defines your agent's behavior.

**Structure your prompt like this:**

```
# Role
You are a helpful customer service agent for [Company].

# Responsibilities
- Answer questions about products and services
- Help resolve common technical issues
- Escalate complex problems to human support

# Communication Style
- Be professional and empathetic
- Use clear, simple language
- Provide step-by-step instructions when helpful

# Boundaries
- Don't make up information you don't know
- Don't discuss competitors negatively
- Redirect off-topic questions politely
```

**Best practices for system prompts:**
- Be specific about the agent's role and expertise
- Define the tone (formal, friendly, technical)
- List clear responsibilities
- Set boundaries on what the agent should and shouldn't do
- Include examples if helpful

### Step 4: Model Configuration

Configure how the AI generates responses:

| Setting | Range | Description |
|---------|-------|-------------|
| **Temperature** | 0.0-2.0 | Controls creativity vs. consistency |

**Temperature guide:**
- **0.0-0.3**: Consistent, factual responses (technical support, Q&A)
- **0.4-0.7**: Balanced (general use, default is 0.7)
- **0.8-2.0**: Creative, varied responses (brainstorming, writing)

### Step 5: Attach Datasets

Give your agent specialized knowledge:

1. In the **Datasets** section, use the search box to find datasets
2. Check the boxes next to datasets you want to attach
3. Use **Select All** or **Clear All** for bulk selection
4. Selected datasets appear as badges above the list

**Tips:**
- More datasets isn't always better - keep it focused
- Update dataset attachments when your documents change
- Test retrieval quality after attaching

### Step 6: Easy Buttons (Optional)

Add quick-access conversation starters that appear as buttons in the chat:

1. Find the **Easy Buttons** section
2. Click **Add Easy Button** to create a new button
3. Enter the prompt text that will be sent when clicked
4. Add up to 10 easy buttons

**Examples:**
- "Summarize this document"
- "Explain this in simple terms"
- "Help me draft an email about..."

### Step 7: Visibility Settings

Control who can access your agent:

| Visibility | Who Can Access | Best For |
|------------|----------------|----------|
| **Individual** | Only you | Personal agents, development |
| **Team** | Selected team members | Team-specific workflows |
| **Organization** | All users in your organization | Company-wide tools |

**Note**: Only Tenant Admins can set Organization visibility. Once set, all users can access the agent. See [Sharing Agents](Agents-Sharing) for details.

When selecting **Team** visibility:
1. Choose which teams should have access
2. Each team's members will see the agent

### Step 8: Save and Test

1. Review all your settings
2. Click **Create Agent**
3. The agent is created and available immediately
4. Click on the agent to start a test conversation
5. Iterate based on results

## Testing Your Agent

### Initial Testing

After creating:
1. Try the main use cases you designed for
2. Test edge cases and unexpected inputs
3. Verify the tone matches your intentions
4. Check that datasets are being used correctly

### Iteration Cycle

1. Note any issues in responses
2. Edit the agent to adjust
3. Test again
4. Repeat until satisfied

## Tips for Better Agents

### Write Clear Instructions

Be explicit about:
- What the agent should do
- How it should communicate
- What it should avoid
- How to handle edge cases

### Start Simple

- Begin with basic functionality
- Test thoroughly before adding complexity
- Iterate based on actual usage

### Use Datasets Wisely

- Attach only relevant datasets
- Keep dataset content focused
- Update datasets when information changes

### Test Edge Cases

- Try unexpected inputs
- Test boundary conditions
- Verify error handling

## Common Mistakes to Avoid

| Mistake | Problem | Solution |
|---------|---------|----------|
| Vague system prompt | Inconsistent responses | Be specific about role and behavior |
| Too many datasets | Slow, unfocused retrieval | Only attach what's needed |
| Wrong temperature | Responses too rigid or chaotic | Match setting to use case |
| No testing | Sharing broken agents | Always test before sharing |
| No boundaries | Off-topic responses | Define what agent shouldn't do |

## Next Steps

After creating your agent:
- [Configure advanced settings](configuring)
- [Share with your team](sharing)
- Monitor usage and gather feedback
