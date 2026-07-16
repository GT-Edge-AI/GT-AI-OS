> **Gen 3:** This is a legacy Gen 2 article. For current GT AI OS 3.0 guidance, see [gen3/agents/building](gen3/agents/building).

# Agent Templates

Agent templates are pre-configured agents that you can import and customize for common use cases. Download a template CSV file and import it to quickly create a ready-to-use agent.

## Available Templates

### Document Chat Agent

Chat with your uploaded documents using RAG (Retrieval-Augmented Generation). Upload PDFs, Word docs, or text files and ask questions about their content.

**Best for:** Knowledge bases, document Q&A, research assistance

*Click the below link, and once on the CSV file's github page, click the "Download Raw File" button on the top right of the page to download the Agent Template CSV file.*

**[Download Template](https://github.com/GT-Edge-AI/GT-AI-OS/blob/main/agent-templates/document-chat-agent.csv)**

---

### Web Research Agent

AI-powered research agent that searches the web and provides well-sourced answers with proper citations. Includes quality indicators for sources and publication dates.

**Best for:** Current events research, fact-checking, gathering information with citations

*Click the below link, and once on the CSV file's github page, click the "Download Raw File" button on the top right of the page to download the Agent Template CSV file.*

**[Download Template](https://github.com/GT-Edge-AI/GT-AI-OS/blob/main/agent-templates/internet-search-agent.csv)**

---

### System Prompt Reviewer

Expert agent that analyzes and improves system prompts for AI agents. Paste your prompt to get actionable feedback on clarity, structure, and effectiveness.

**Best for:** Prompt engineering, improving agent performance, learning prompt design

*Click the below link, and once on the CSV file's github page, click the "Download Raw File" button on the top right of the page to download the Agent Template CSV file.*

**[Download Template](https://github.com/GT-Edge-AI/GT-AI-OS/blob/main/agent-templates/system-prompt-reviewer.csv)**

---

### Nemotron Agent

A powerful local AI agent powered by NVIDIA Nemotron running on Ollama. Designed for advanced reasoning, coding, and complex problem-solving tasks.

**Best for:** Complex analysis, code review, technical writing, detailed research

**Requires:** Ollama with nemotron model installed

*Click the below link, and once on the CSV file's github page, click the "Download Raw File" button on the top right of the page to download the Agent Template CSV file.*

**[Download Template](https://github.com/GT-Edge-AI/GT-AI-OS/blob/main/agent-templates/nemotron-agent.csv)**

---

### Nemotron Mini Agent

A fast and efficient local AI agent powered by NVIDIA Nemotron Mini running on Ollama. Optimized for quick responses and general-purpose tasks.

**Best for:** Quick Q&A, writing assistance, brainstorming, summarization

**Requires:** Ollama with nemotron-mini model installed

*Click the below link, and once on the CSV file's github page, click the "Download Raw File" button on the top right of the page to download the Agent Template CSV file.*

**[Download Template](https://github.com/GT-Edge-AI/GT-AI-OS/blob/main/agent-templates/nemotron-mini-agent.csv)**

---

### Python Coding Micro Project

A Python and Streamlit coding tutor that helps you build working applications quickly. Great for learning to code with hands-on projects.

**Best for:** Learning Python, building Streamlit apps, coding tutorials

*Click the below link, and once on the CSV file's github page, click the "Download Raw File" button on the top right of the page to download the Agent Template CSV file.*

**[Download Template](https://github.com/GT-Edge-AI/GT-AI-OS/blob/main/agent-templates/python_coding_microproject.csv)**

---

### Vision Chat Agent

Chat with image-containing datasets using vision-enabled RAG. Upload images to a dataset with a Vision Model selected, then attach it to conversations using the paperclip icon.

**Best for:** Image analysis, visual Q&A, diagram description, image comparison

*Click the below link, and once on the CSV file's github page, click the "Download Raw File" button on the top right of the page to download the Agent Template CSV file.*

**[Download Template](https://github.com/GT-Edge-AI/GT-AI-OS/blob/main/agent-templates/vision-chat-agent.csv)**

---

### Kali Linux Simulation Agent

Simulates a Kali Linux terminal environment with common security and system administration tools. Provides realistic command outputs for learning.

**Best for:** Learning Linux commands, security training, understanding terminal tools

*Click the below link, and once on the CSV file's github page, click the "Download Raw File" button on the top right of the page to download the Agent Template CSV file.*

**[Download Template](https://github.com/GT-Edge-AI/GT-AI-OS/blob/main/agent-templates/kali_linux_shell_simulator.csv)**

---

## Using Templates

### Importing a Template

1. Click a **Download Template** link above to save the CSV file
2. Go to **Agents** in the sidebar
3. Click **Import** in the top right
4. Select the downloaded CSV file
5. Review the agent configuration
6. Click **Import** to create the agent

### Customizing After Import

After importing a template:

1. Click the agent's dropdown menu and select **Edit**
2. Update the **Name** to reflect your use case
3. Modify the **System Prompt** for your specific needs
4. Attach relevant **Datasets** for domain knowledge
5. Adjust **Visibility** settings (Individual, Team, or Organization)
6. Configure **Easy Buttons** for common interactions
7. Save your changes

## Creating Your Own Templates

You can create templates from your existing agents:

1. Configure an agent with your desired settings
2. Test thoroughly with various scenarios
3. Export the agent using the **Export** option in the dropdown menu
4. Share the CSV file with colleagues

### Template Best Practices

When creating templates:
- Write clear, generalizable system prompts
- Include detailed descriptions
- Test with multiple use cases
- Avoid organization-specific references
- Use appropriate model and temperature settings for the task

## Troubleshooting

### Import Errors

If template import fails:
- Verify the file format (CSV)
- Check that all required fields are present
- Ensure the model specified in the template is available
- Review error messages for specific issues

### Template Not Working as Expected

If an imported agent doesn't behave as expected:
- Review and adjust the system prompt
- Check that the correct model is selected
- Verify temperature and max tokens settings
- Attach appropriate datasets if the agent needs domain knowledge
