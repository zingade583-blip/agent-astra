# Agent Astra 🤖

**Agent Astra** is a personal AI agent designed to help users create professional content and manage communication tasks from one place. It aims to support LinkedIn post drafting, email writing, Instagram captions, and content adaptation for different platforms.

🔗 **GitHub Repository:** https://github.com/zingade583-blip/agent-astra

---

## 🌟 Project Overview

Creating content for multiple platforms takes time. Agent Astra aims to simplify this process by allowing users to request different types of content through a single AI agent.

The project focuses on:

- 📝 LinkedIn post drafting
- 📧 Professional email drafting
- 📸 Instagram captions and hashtags
- 🔄 Adapting content for different platforms
- 🛡️ Human approval before external actions
- 📊 Clear action status and error reporting

**Important:** Actual sending, publishing, and third-party integrations depend on the features implemented in the code and the required API permissions. This README describes the intended workflow; it does not claim that every integration is already operational.

## ⚙️ How Agent Astra Works

Agent Astra is designed to follow this workflow:

```text
                USER REQUEST
                     |
                     v
             INTENT CLASSIFICATION
                     |
          +----------+----------+
          |          |          |
          v          v          v
      LinkedIn     Email     Instagram
          |          |          |
          v          v          v
     Post Draft  Email Draft  Caption
          |          |          |
          +----------+----------+
                     |
                     v
              CONTENT PREVIEW
                     |
                     v
            USER APPROVAL REQUIRED
                     |
              +------+------+
              |             |
              v             v
          Not Approved   Approved
              |             |
              v             v
          Keep Draft   Verify Integration
                            |
                            v
                     Execute if Available
                            |
                            v
                     Verify Real Result
```

### 1. Understand the request

The agent identifies what the user wants to create and which platform is relevant.

### 2. Generate the correct content

- **LinkedIn:** A professional post based on the user's topic and supplied details.
- **Email:** A recipient, subject line, and complete email body.
- **Instagram:** A caption with relevant hashtags.
- **Content adaptation:** Rewrites content for a requested platform or tone.

The agent should not substitute a LinkedIn post when the user requests an email.

### 3. Preview before taking action

The agent displays the complete draft so the user can review and edit it.

### 4. Request explicit approval

Writing or drafting content does not grant permission to send or publish it. The agent must obtain clear approval for the specific content and destination before performing an external action.

### 5. Verify the result

The agent reports the actual outcome. It must never claim that content was published or an email was sent unless the relevant service confirms success.

## 🛡️ Human Approval and Safety

Agent Astra follows these principles:

- Drafting is the default behavior.
- Never publish automatically when the user only asks to write or draft.
- Ask for approval before sending emails or publishing content.
- Never claim an external action succeeded without confirmation.
- Use only information provided by the user or available in authorized context.
- Never invent personal achievements, experiences, or affiliations.
- Explain clearly when an integration is unavailable.
- Keep API keys, access tokens, passwords, and client secrets private.

## 🧰 Technology Stack

The project may use the following technologies, depending on the current implementation:

| Technology | Purpose |
|---|---|
| Python | Main application and agent logic |
| uAgents | Agent framework |
| Agentverse | Hosting, discovery, and agent communication |
| ASI:One API | AI capabilities, when configured |
| LinkedIn API | LinkedIn integration, when implemented and authorized |
| Email API | Email integration, when implemented and authorized |
| Instagram API | Instagram integration, when implemented and authorized |
| Git and GitHub | Version control and source-code hosting |

The presence of a technology in this table does not guarantee that its integration is configured or working.

## 📁 Project Structure

```text
agent-astra/
├── agent.py
├── linkedin_setup.py
├── requirements.txt
├── .env.example
├── .gitignore
└── README.md
```

- `agent.py` — Main Python agent and its implemented handlers.
- `linkedin_setup.py` — LinkedIn authentication helper, if used by the project.
- `requirements.txt` — Python dependencies.
- `.env.example` — Example environment-variable template containing placeholders.
- `.gitignore` — Specifies files Git should not track.
- `README.md` — Project documentation.

A local `.env` file may also exist. It must remain private and must not be committed to GitHub.

## 💻 Setup and Installation

### Prerequisites

- Python
- Git
- A terminal such as Command Prompt or PowerShell
- API credentials for any integrations actually used by the application

### Step 1: Clone the repository

```bash
git clone https://github.com/zingade583-blip/agent-astra.git
cd agent-astra
```

### Step 2: Create a virtual environment

On Windows:

```bash
py -m venv .venv
.venv\Scripts\activate
```

### Step 3: Install dependencies

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Use a Python version compatible with the installed dependencies. If the agent encounters an asyncio event-loop error, check Python and uAgents compatibility before changing versions.

## 🔐 Environment Configuration

If the project uses environment variables, create a local configuration file from the example:

```bash
copy .env.example .env
```

Example placeholders:

```env
ASI1_API_KEY=your_api_key_here
ASI1_BASE_URL=https://api.asi1.ai/v1

LINKEDIN_ACCESS_TOKEN=
LINKEDIN_AUTHOR_URN=
LINKEDIN_CLIENT_ID=
LINKEDIN_CLIENT_SECRET=
LINKEDIN_REDIRECT_URI=http://localhost:8000/callback
```

These are illustrative settings. Use only the variables required by the current code.

**Security rules:**

- Never commit `.env`.
- Never put real API keys or tokens in this README.
- Keep `.env.example` limited to placeholders.
- If a credential is exposed, revoke or rotate it immediately.
- Configure hosted secrets using the hosting platform's supported settings.

## ▶️ Run Agent Astra

From the project directory, activate your virtual environment and run:

```bash
python agent.py
```

Keep the terminal open while the agent is running. Press `Ctrl+C` to stop it.

If the agent provides an Agent Inspector URL, open it while the process is running and follow the platform's instructions to configure any required messaging or mailbox connection.

## 🧪 Testing

Test the agent with these prompts before enabling external actions.

**Test 1 — LinkedIn draft**

```text
Write a professional LinkedIn post about my project.
Do not publish it.
```

Expected: A LinkedIn draft, with no claim that it was published.

**Test 2 — Email draft**

```text
Draft an email to my teammate asking how their hackathon
preparation is going. Do not send it.
```

Expected: A subject line and complete email body. The agent must not return a LinkedIn post instead.

**Test 3 — Avoid invented details**

```text
Write a LinkedIn post about my achievements.
```

Expected: Use known facts or ask the user for more details.

**Test 4 — Approval workflow**

```text
Show me a preview of this LinkedIn post.
```

Expected: Display the complete draft and wait for explicit approval before any external publishing action.

**Test 5 — Integration unavailable**

Ask the agent to publish a post when no LinkedIn integration is configured.

Expected: Explain that it can provide a draft but cannot publish through an unavailable integration.

## 🔧 Troubleshooting

| Problem | Suggested check |
|---|---|
| `401 invalid_api_key` | Verify the provider, endpoint, and API-key configuration. |
| Asyncio event-loop error | Check compatibility between Python and the installed uAgents version. |
| Agent does not respond | Check that it is running and that messaging or mailbox setup is complete. |
| Email request returns a LinkedIn post | Review intent classification and message handlers. |
| Agent falsely claims publication | Review the publishing handler and require confirmed service results. |
| Git push is rejected | Check repository history and resolve merge conflicts before pushing. |

## 🚀 Future Improvements

Potential improvements include:

- More reliable intent classification
- LinkedIn, email, and Instagram integrations
- A consistent preview and approval interface
- Action history and status tracking
- Better error handling and retry logic
- Secure credential management
- Automated tests for channel routing and approval
- Deployment and monitoring improvements

These are planned improvements unless they have already been implemented and tested.

## 🔒 Security

Agent Astra should protect user privacy and credentials at every stage. External actions must require the appropriate authorization, and success messages must be based on verified results.

## 👨‍💻 Project Repository

**Agent Astra**

GitHub: https://github.com/zingade583-blip/agent-astra

Built to make AI-assisted content creation more organized, transparent, and user-controlled.
## 🙏 Credits and Acknowledgements

Special thanks to **[ShyamRV](https://github.com/ShyamRV)** for the original LinkedIn agent workshop and project that served as a reference and learning resource for this project.

**Agent Astra** builds on the learning and inspiration gained from that reference, with its own project identity, documentation, and intended focus on AI-assisted content creation and human-approved actions.

- **Original reference:** [ShyamRV/demo-linkedin-agent](https://github.com/ShyamRV/demo-linkedin-agent)
- **My project:** [zingade583-blip/agent-astra](https://github.com/zingade583-blip/agent-astra)

All credit for the original work belongs to its respective creator. Please refer to the original repository's license for applicable reuse and attribution terms.

---

*This documentation describes the intended design and workflow. Actual capabilities depend on the current source code, configured integrations, and granted permissions.*
