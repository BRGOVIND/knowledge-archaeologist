# 🔍 Knowledge Archaeologist

> **AI-powered Slack agent that uncovers buried organizational knowledge across GitHub, Notion, and Slack — then explains it with sources and context.**

Built for the Slack Hackathon on DevPost.

---

## The Problem

Someone asks in Slack:
> *"Why was the payment migration delayed?"*
> *"Who approved the Kubernetes migration?"*
> *"How does our deployment process work?"*

The answer exists. But it's buried across Slack threads, GitHub PRs, and Notion docs. People waste hours searching.

## The Solution

Knowledge Archaeologist acts like an AI investigator. Ask it anything — it searches everything, synthesizes the answer, and shows you exactly where it found the information.

```
@Knowledge Archaeologist Why was the payment migration postponed?

→ The Stripe webhook system failed load testing at 5,000 req/sec.

   📦 GitHub: PR #12 "Payment Migration" — webhook failure noted
   📄 Notion: "Q2 Infrastructure Projects" — marked as delayed  
   💬 Slack: #backend discussion (May 12-14)

   Decision owner: @sarah_eng
   Next steps: Redesign webhook batching system
   
   Answered in 3.2s ⚡
```

---

## Demo

![Knowledge Archaeologist Demo](https://img.shields.io/badge/Status-Live-brightgreen)

**Live demo:** Ask the bot anything in the Slack workspace.

---

## Architecture

```
Slack Message (@Knowledge Archaeologist)
              ↓
        FastAPI Backend
              ↓
     MCP Servers (parallel)
     ├── GitHub MCP     → PRs, Issues
     ├── Notion MCP     → Pages, Docs  
     └── Slack MCP      → Message History
              ↓
      Supabase Cache (TTL)
              ↓
    qwen3 / Gemini LLM
    (Synthesize + Reason)
              ↓
    Slack Block Response
    (Answer + Sources + Citations)
```

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| **Agent Platform** | Slack Agent Builder |
| **Backend** | FastAPI + Python |
| **MCP Servers** | Custom (GitHub, Notion, Slack) |
| **LLM** | qwen3:8b (local) / Gemini 2.0 Flash |
| **Cache** | Supabase + In-memory TTL |
| **Deployment** | Render |

---

## Features

- **Multi-source search** — GitHub, Notion, and Slack searched simultaneously
- **AI synthesis** — LLM reconstructs decisions with reasoning
- **Source citations** — every answer shows exactly where it came from
- **Caching** — repeated queries answer in <1 second (`⚡ cached`)
- **Rate limiting** — protects against API abuse
- **MCP architecture** — modular, extensible knowledge sources
- **Live dashboard** — real-time query monitoring at `/`

---

## Judging Criteria Alignment

| Criterion | How We Address It |
|-----------|------------------|
| **Slack AI capabilities** | Full Slack Agent Builder integration with `app_mention` events |
| **MCP integration** | Real MCP servers for GitHub, Notion, Slack — in the request path |
| **Real-time search** | 3 sources searched in parallel on every query |
| **Design** | Progressive UX — instant "Digging..." → edited answer |
| **Impact** | Every company with Slack has this problem |
| **Innovation** | Multi-source synthesis with citations, not just another chatbot |

---

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