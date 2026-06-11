# Knowledge Archaeologist

**AI-powered organizational intelligence platform for Slack.**

Knowledge Archaeologist helps teams uncover buried knowledge across GitHub, Notion, and Slack, reconstruct decisions, understand repositories, and safely execute actions through specialized AI agents.

Built for the Slack Agent Builder Challenge.

---

## What It Does

Knowledge Archaeologist understands:

* GitHub repositories
* Slack discussions
* Notion documentation

It builds:

* Repository Intelligence
* Decision Timelines
* Evidence Chains
* Organizational Knowledge Maps

It creates:

* Specialized AI Agents

It performs:

* Safe Human-Approved Actions

---

## Example 1 — Repository Archaeology

A user pastes:

https://github.com/pallets/flask

Knowledge Archaeologist automatically:

* Reads the repository
* Analyzes README and structure
* Identifies technologies
* Finds key files
* Explains architecture
* Suggests a reading order
* Stores the analysis for follow-up questions

Example:

```text
Repository Archaeology — pallets/flask

Summary:
Flask is a lightweight WSGI web framework for Python.

Tech Stack:
Python · Werkzeug · Jinja · Pytest

Key Files:
src/flask/__init__.py
tests/conftest.py
docs/index.rst

Suggested Reading Order:
README.md
→ docs/index.rst
→ src/flask/__init__.py
```

---

## Example 2 — Organizational Intelligence

Ask:

```text
@Knowledge Archaeologist
Why was the payment migration delayed?
```

Knowledge Archaeologist:

* Searches GitHub
* Searches Slack
* Searches Notion
* Correlates evidence
* Reconstructs the decision

Example:

```text
The migration was delayed because Stripe webhook load tests failed.

Evidence:

💬 Slack:
#backend discussion
May 12–14

📦 GitHub:
PR #84
Webhook redesign

📄 Notion:
Q2 Infrastructure Plan

Decision Owner:
@sarah_eng
```

---

## Example 3 — Specialized Agents

Create agents from templates:

* Repository Analyst
* Documentation Fixer
* Incident Investigator
* Technical Writer
* Knowledge Curator
* Architecture Reviewer
* Security Reviewer
* Release Manager
* Project Historian
* Onboarding Assistant

Or create agents using plain English:

```text
Create an agent that reviews onboarding docs
and flags missing setup instructions.
```

---

## Safe Approval Framework

Agents never perform write actions automatically.

Every write request follows:

```text
Agent
↓
Proposal
↓
Human Approval
↓
Execution
↓
Audit Log
```

This creates a transparent and enterprise-friendly workflow.

---

## Operations Center

Knowledge Archaeologist includes a live Operations Center dashboard.

Features:

* Source Health
* Agent Registry
* Activity Feed
* Repository Analyses
* Approval Queue
* Agent History
* Live Execution Tracking

Every significant action is recorded and visible in real time.

---

## Architecture

```text
Slack User
      ↓
Knowledge Archaeologist
      ↓
MCP Search Layer
 ├─ GitHub
 ├─ Slack
 └─ Notion
      ↓
Groq LLM
      ↓
Evidence Synthesis
      ↓
Agent Framework
      ↓
Human Approval Gate
      ↓
Slack Response + Dashboard
```

---

## Tech Stack

| Layer           | Technology                 |
| --------------- | -------------------------- |
| Agent Platform  | Slack Agent Builder        |
| Backend         | FastAPI                    |
| LLM             | Groq (Llama 3.1)           |
| Integrations    | GitHub, Slack, Notion      |
| Agent Framework | Custom                     |
| Storage         | Supabase                   |
| Dashboard       | Operations Center          |
| Deployment      | Render / Cloudflare Tunnel |

---

## Core Features

### Repository Archaeology

Paste any public GitHub repository and receive:

* Architecture Summary
* Technology Stack
* Key Files
* Reading Order
* Repository Intelligence

### Incident Investigation

Reconstruct incidents using:

* Slack discussions
* GitHub activity
* Notion documentation

### Evidence Chains

Every answer includes evidence and source attribution.

### Agent Platform

Create specialized agents and safely execute actions.

### Operations Center

Real-time visibility into agents, approvals, analyses, and activity.

---

## Current Status

### Implemented

* Repository Archaeology
* Incident Investigator
* Evidence Chains
* Agent Templates
* Natural Language Agent Creation
* Safe Approval Framework
* GitHub Integration
* Slack Integration
* Notion Integration
* Operations Center Dashboard

### In Progress

* Notion Archaeology
* Slack Decision Intelligence
* Evidence Explorer
* Decision Timeline
* Enhanced Repository Intelligence

```
```


## Setup

### Prerequisites
- Python 3.10+
- Slack workspace
- API keys: Slack, GitHub, Notion, Gemini

### Installation

```bash
git clone https://github.com/BRGOVIND/knowledge-archaeologist.git
cd knowledge-archaeologist

python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

pip install -r requirements.txt
cp .env.example .env
# Edit .env with your API keys

python test_setup.py  # verify everything works
python -m uvicorn app.main:app --host 0.0.0.0 --port 3000
```

### Environment Variables

```env
SLACK_BOT_TOKEN=xoxb-...
SLACK_SIGNING_SECRET=...
GEMINI_API_KEY=AIza...
GITHUB_TOKEN=ghp_...
GITHUB_REPO=owner/repo
NOTION_API_KEY=secret_...
SUPABASE_URL=https://...supabase.co
SUPABASE_SERVICE_ROLE_KEY=eyJ...
```

---

## Project Structure

```
knowledge-archaeologist/
├── app/
│   ├── main.py              # FastAPI + Slack Agent
│   ├── mcp_server.py        # MCP server architecture
│   ├── reasoning.py         # LLM synthesis layer
│   ├── cache.py             # Two-tier caching + rate limiting
│   ├── formatting.py        # Slack Block Kit responses
│   ├── config.py            # Central configuration
│   └── integrations/
│       ├── github.py        # GitHub search
│       ├── notion.py        # Notion search
│       └── slack.py         # Slack history search
├── static/
│   └── dashboard.html       # Live status dashboard
├── test_setup.py            # Pre-flight checks
├── render.yaml              # One-click Render deployment
└── requirements.txt
```

---

## Security

- Prompt injection protection (untrusted content delimiters)
- Per-user rate limiting (6 req/min)
- Input validation and length caps
- Secrets managed via environment variables
- Read-only API scopes for all integrations
