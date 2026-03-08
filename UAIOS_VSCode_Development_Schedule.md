# UAIOS — VS Code Fork Development Schedule

> **Project:** Universal AI Orchestration System (UAIOS)  
> **Team:** Muhammad Atif (SP23-BAI-031) & Talha Asif (SP23-BAI-042)  
> **Duration:** 6 Months (20 Weeks Active + Breaks)  
> **Goal:** Build an Agentic IDE that competes with Cursor, Antigravity, TRAE, Zed  
> **Evaluation:** Weekly progress demos for teacher

---

## 📋 Schedule Overview

| Semester | Weeks | Focus Area | Outcome |
|----------|-------|------------|---------|
| **Semester 1** | 1-10 | Foundation + Core Engine | Working demo with 3 platform connectors |
| **Vacation** | - | Light tasks + Documentation | Mid-project report |
| **Semester 2** | 11-20 | Advanced Features + Polish | Final defense-ready system |

---

## 🎯 Weekly Evaluation Criteria

Each week ends with:
- ✅ **Demoable deliverable** (something to show teacher)
- 📝 **Git commits** proving work done
- 📊 **Progress update** in GitHub Projects board

---

# SEMESTER 1: Foundation + Core Engine

---

## TOPIC 1: VS Code Fork Setup & Understanding
### Week 1 (Feb 21 - Feb 27)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Clone VS Code repo, understand folder structure | Both | Document: `vscode-structure-notes.md` |
| 2-3 | Study `src/vs/workbench/` — where UI lives | Atif | Identify extension points |
| 3-4 | Study `extensions/` folder — how built-in extensions work | Talha | List of extension APIs |
| 4-5 | Run VS Code from source (`yarn && yarn watch`) | Both | Screenshot of running fork |
| 5-6 | Update branding (product.json, icons, splash) | Atif | "UAIOS" appears in window title |
| 6-7 | Set up development workflow (hot reload, debugging) | Both | Working dev environment |

**🎯 Week 1 Demo:** Running UAIOS fork with custom branding

**📚 Study Materials:**
- VS Code Extension API: https://code.visualstudio.com/api
- VS Code Architecture: `src/vs/` folder walkthrough
- How Cursor modified VS Code (reverse engineer from public info)

---

### Week 2 (Feb 28 - Mar 6)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Create first VS Code extension (Hello World in sidebar) | Atif | Extension loads in UAIOS |
| 2-3 | Study Webview API — custom UI panels in VS Code | Talha | Sample webview panel |
| 3-4 | Build skeleton sidebar panel: "UAIOS Chat" | Atif | Empty chat panel visible |
| 4-5 | Build skeleton sidebar panel: "Platform Browser" | Talha | Empty platform list visible |
| 5-6 | Connect extension to external process (IPC basics) | Both | Extension ↔ Backend communication |
| 6-7 | Set up GitHub Projects board + Milestones | Both | Sprint board ready |

**🎯 Week 2 Demo:** Two custom sidebar panels visible in UAIOS IDE

**📂 Files to Create:**
```
vscode/extensions/uaios-core/
├── package.json          # Extension manifest
├── src/
│   ├── extension.ts      # Entry point
│   ├── chatPanel.ts      # Chat UI
│   └── platformPanel.ts  # Platform browser UI
└── media/
    └── styles.css        # Panel styling
```

---

## TOPIC 2: Backend Foundation
### Week 3 (Mar 7 - Mar 13)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Set up FastAPI backend skeleton | Atif | `/api/health` endpoint |
| 2-3 | Set up PostgreSQL + Redis (Docker Compose) | Atif | `docker-compose.yml` working |
| 3-4 | Design Platform Registry database schema | Talha | Schema diagram + migrations |
| 4-5 | Create `platforms.json` with 50 platforms (metadata) | Talha | Initial seed data |
| 5-6 | Build `/api/platforms` endpoints (CRUD) | Atif | List/search platforms API |
| 6-7 | Connect VS Code extension to backend (fetch platforms) | Both | Platform list shows in IDE |

**🎯 Week 3 Demo:** Platform Browser in IDE shows list from backend API

**📂 Backend Structure:**
```
backend/
├── app/
│   ├── main.py           # FastAPI entry
│   ├── api/
│   │   ├── platforms.py  # Platform registry endpoints
│   │   └── health.py     # Health check
│   ├── models/
│   │   └── platform.py   # SQLAlchemy models
│   └── core/
│       └── database.py   # DB connection
├── data/
│   └── platforms.json    # Seed data (50+ platforms)
├── requirements.txt
└── docker-compose.yml    # PostgreSQL + Redis
```

**📊 Platform Registry Schema:**
```python
class Platform:
    id: str                    # "cursor", "v0-dev", etc.
    name: str                  # "Cursor"
    category: str              # "Programming Assistant"
    description: str           # What it does
    capabilities: List[str]    # ["code_generation", "chat"]
    api_type: str              # "MCP" | "REST" | "SDK"
    auth_type: str             # "OAuth" | "API_Key" | "None"
    base_url: str              # API endpoint
    autonomy_level: int        # 1-5 scale
    has_active_connector: bool # True if we built integration
    created_at: datetime
```

---

### Week 4 (Mar 14 - Mar 20)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Set up ChromaDB for vector embeddings | Talha | ChromaDB running in Docker |
| 2-3 | Generate embeddings for platform capabilities | Talha | All 50 platforms embedded |
| 3-4 | Build `/api/platforms/search` — semantic search | Talha | "I need to deploy" → [Vercel, Railway] |
| 4-5 | Integrate search into Platform Browser panel | Atif | Search box in IDE works |
| 5-6 | Add platform detail view (click → see full info) | Atif | Platform cards expand |
| 6-7 | Documentation + code cleanup | Both | Clean codebase |

**🎯 Week 4 Demo:** Semantic search in IDE — type "generate UI" → shows v0, Lovable, Figma AI

---

## TOPIC 3: Cognitive Layer (The Brain)
### Week 5 (Mar 21 - Mar 27)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Study LLM function calling (Claude/OpenAI) | Talha | Working examples |
| 2-3 | Set up LiteLLM for unified LLM access | Talha | Can call Claude/GPT/Gemini |
| 3-4 | **Set up OpenRouter AI** for model routing + fallback | Talha | Auto-fallback if model fails |
| 4-5 | Build Intent Classifier prompt | Talha | User input → intent JSON |
| 5-6 | Build `/api/cognitive/classify` endpoint | Atif | API returns structured intent |
| 6-7 | Connect Chat Panel → Intent Classifier + test 10 prompts | Both | Accuracy validation |

**🎯 Week 5 Demo:** Type "Build a landing page" → System shows: `{intent: "SOFTWARE_BUILD", components: ["UI", "Deploy"]}`

**📝 Intent Classification Output:**
```json
{
  "intent": "SOFTWARE_BUILD",
  "confidence": 0.95,
  "sub_intents": ["UI_GENERATION", "DEPLOYMENT"],
  "entities": {
    "project_type": "landing_page",
    "tech_hints": []
  },
  "complexity": "MEDIUM"
}
```

---

### Week 6 (Mar 28 - Apr 3)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Build Requirement Decomposer prompt | Talha | Single request → sub-tasks |
| 2-3 | Build `/api/cognitive/decompose` endpoint | Atif | API returns task list |
| 3-4 | Build DAG Generator (task dependencies) | Talha | Which tasks can run parallel |
| 4-5 | Visualize DAG in IDE (simple tree view) | Atif | User sees task breakdown |
| 5-6 | Connect decomposer → platform registry | Both | Each task gets platforms |
| 6-7 | End-to-end test: prompt → decompose → platforms | Both | Full flow working |

**🎯 Week 6 Demo:** "Build a blog with auth" → Shows DAG: UI (v0) → Auth (Supabase) → Deploy (Vercel)

**📝 Decomposition Output:**
```json
{
  "original_request": "Build a blog with auth",
  "tasks": [
    {
      "id": "T1",
      "name": "Generate UI Components",
      "type": "UI_GENERATION",
      "depends_on": [],
      "platforms": ["v0.dev", "Lovable", "Figma AI"],
      "selected_platform": "v0.dev"
    },
    {
      "id": "T2", 
      "name": "Set up Authentication",
      "type": "AUTH_SETUP",
      "depends_on": ["T1"],
      "platforms": ["Supabase", "Firebase", "Clerk"],
      "selected_platform": "Supabase"
    },
    {
      "id": "T3",
      "name": "Deploy Application",
      "type": "DEPLOYMENT",
      "depends_on": ["T1", "T2"],
      "platforms": ["Vercel", "Railway", "Netlify"],
      "selected_platform": "Vercel"
    }
  ],
  "dag": {
    "T1": [],
    "T2": ["T1"],
    "T3": ["T1", "T2"]
  },
  "estimated_time": "15 minutes",
  "estimated_cost": "$0.00"
}
```

---

## TOPIC 4: First Platform Connectors
### Week 7 (Apr 4 - Apr 10)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Study MCP Protocol specification | Talha | Understanding document |
| 2-3 | Install mcp-python-sdk, build hello-world MCP client | Talha | Connect to MCP server |
| 3-4 | Build generic MCP Client adapter class | Talha | Reusable for any MCP server |
| 4-5 | Build generic REST Client adapter class | Atif | Reusable for any REST API |
| 5-6 | Connector #1: OpenAI/Claude API (LLM calls) | Both | Can generate text/code |
| 6-7 | Test LLM connector end-to-end | Both | Working integration |

**🎯 Week 7 Demo:** System calls Claude API to generate code, displays in IDE

**📂 Connector Architecture:**
```
backend/app/connectors/
├── base.py               # Abstract connector class
├── mcp_client.py         # Generic MCP client
├── rest_client.py        # Generic REST client
├── llm/
│   ├── openai.py         # OpenAI connector
│   └── anthropic.py      # Claude connector
└── ...
```

---

### Week 8 (Apr 11 - Apr 17)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Connector #2: GitHub API (create repo, push code) | Atif | Create repo via UAIOS |
| 2-3 | GitHub OAuth flow implementation | Atif | User connects GitHub |
| 3-4 | Connector #3: Vercel API (deploy from repo) | Atif | Deploy project via UAIOS |
| 4-5 | Vercel OAuth flow implementation | Atif | User connects Vercel |
| 5-6 | Store OAuth tokens securely (encrypted) | Talha | Secure credential storage |
| 6-7 | Integration test: Generate → Push → Deploy | Both | End-to-end working |

**🎯 Week 8 Demo:** Generate a file → Push to GitHub → Deploy to Vercel — all from IDE

---

## TOPIC 5: Orchestration Engine
### Week 9 (Apr 18 - Apr 24)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Study LangGraph for stateful workflows | Talha | Sample workflow running |
| 2-3 | Build DAG Executor class | Talha | Executes tasks in order |
| 3-4 | Implement parallel task execution | Talha | Run independent tasks together |
| 4-5 | Build State Machine (pending → running → done/failed) | Atif | Task lifecycle tracking |
| 5-6 | WebSocket setup for real-time updates | Atif | IDE gets live status |
| 6-7 | Display execution progress in IDE | Atif | Progress bar + status |

**🎯 Week 9 Demo:** Start workflow → See tasks executing in real-time with status updates

**📝 Execution State Machine:**
```
PENDING → QUEUED → RUNNING → SUCCESS
                      ↓
                   FAILED → RETRY (3x) → FALLBACK → ESCALATE
```

---

### Week 10 (Apr 25 - May 1)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Error handling: retry logic (3 attempts) | Talha | Auto-retry on failure |
| 2-3 | Fallback logic: switch to alternative platform | Talha | If v0 fails → use Lovable |
| 3-4 | User escalation: pause and ask user | Atif | "Platform failed. Retry?" prompt |
| 4-5 | Execution history storage (DB) | Atif | Store all past workflows |
| 5-6 | Execution history panel in IDE | Atif | View past workflows |
| 6-7 | **SEMESTER 1 DEMO PREPARATION** | Both | Polish everything |

**🎯 Week 10 Demo (SEMESTER 1 FINAL):**
Complete flow: User types "Build a landing page" →
1. System decomposes into tasks
2. Selects v0 + GitHub + Vercel
3. Executes in order with live progress
4. Delivers deployed link

---

# VACATION PERIOD (May 2 - May 31)

| Task | Owner | Time |
|------|-------|------|
| Add 2 more platform connectors (Supabase, Stripe) | Both | 1 week |
| Write mid-project documentation/report | Both | 3-4 days |
| Deep-dive A2A protocol docs for Week 14 implementation | Talha | Reading + notes |
| UI/UX mockups for advanced IDE features | Atif | Figma designs |
| Bug fixes from Semester 1 feedback | Both | As needed |

---

# SEMESTER 2: Advanced Features + Polish

---

## TOPIC 6: Advanced IDE Interface
### Week 11 (Jun 1 - Jun 7)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Build visual DAG workflow viewer (React in Webview) | Atif | See task graph visually |
| 2-3 | Add node status colors (pending/running/done) | Atif | Real-time color updates |
| 3-4 | Implement drag-to-reorder tasks (optional) | Atif | User can modify plan |
| 4-5 | Build output viewer (show each task's result) | Talha | Click task → see output |
| 5-6 | Add execution logs panel | Talha | Detailed logs per task |
| 6-7 | Improve chat panel UX (message history, formatting) | Both | Professional chat UI |

**🎯 Week 11 Demo:** Visual workflow DAG with real-time execution animation

---

### Week 12 (Jun 8 - Jun 14)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Build settings panel (API keys, preferences) | Atif | User configures platforms |
| 2-3 | Build platform connection status page | Talha | See which APIs connected |
| 3-4 | Implement keyboard shortcuts | Atif | Cmd+K opens chat, etc. |
| 4-5 | Add notification system (toast messages) | Talha | "Task completed" alerts |
| 5-6 | Dark/light theme consistency | Both | Polished appearance |
| 6-7 | Accessibility improvements (screen reader, contrast) | Both | A11y compliance |

**🎯 Week 12 Demo:** Professional IDE with settings, notifications, keyboard shortcuts

---

## TOPIC 7: More Platform Connectors
### Week 13 (Jun 15 - Jun 21)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Connector #4: Supabase (database + auth setup) | Talha | Auto-create DB schema |
| 2-3 | Connector #5: Stripe (payment setup) | Atif | Create products, checkout |
| 3-4 | Connector #6: v0.dev (UI generation) | Talha | Generate React components |
| 4-5 | Text each connector in isolation | Both | Unit tests pass |
| 5-6 | Integration test: Full SaaS setup flow | Both | End-to-end working |
| 6-7 | Document all connector APIs | Both | Developer docs |

**🎯 Week 13 Demo:** "Build SaaS with auth + payments" → Uses v0 + Supabase + Stripe

---

### Week 14 (Jun 22 - Jun 28)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Connector #7: CrewAI (multi-agent workflows) | Talha | Delegate complex tasks |
| 2-3 | Connector #8: GPT Researcher (research tasks) | Talha | Auto-research topics |
| 3-4 | Connector #9: ElevenLabs (voice/audio) | Atif | Generate voice content |
| 4-5 | **Google A2A Protocol** — Agent Cards + task delegation | Both | A2A client working |
| 5-6 | Build A2A-compatible Agent Card for UAIOS | Talha | Other agents can discover UAIOS |
| 6-7 | Test all 10 connectors + A2A together | Both | Full system test |

**🎯 Week 14 Demo:** All 10 platform connectors + A2A protocol working

**📝 Google A2A Implementation:**
```python
# Agent Card (JSON-LD format)
{
  "@type": "AgentCard",
  "name": "UAIOS",
  "description": "Universal AI Orchestration System",
  "capabilities": ["code_generation", "deployment", "research"],
  "endpoint": "https://uaios.api/a2a",
  "supportedTasks": ["build_app", "deploy", "research"]
}
```

---

## TOPIC 8: Adaptive Intelligence
### Week 15 (Jun 29 - Jul 5)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Track execution success/failure per platform | Talha | Analytics DB schema |
| 2-3 | Build platform performance scoring system | Talha | Score: speed, reliability |
| 3-4 | **Langfuse integration** — LLM observability/tracing | Talha | All LLM calls traced |
| 4-5 | Auto-improve platform selection based on history | Both | System learns preferences |
| 5-6 | User preference storage + Cost tracking | Atif | Remember choices + show cost |
| 6-7 | Build analytics dashboard in IDE | Atif | View usage statistics + traces |

**🎯 Week 15 Demo:** System recommends platforms based on past success rates + full LLM tracing

**📝 Langfuse Integration:**
```python
from langfuse import Langfuse

langfuse = Langfuse()

# Trace every LLM call
@langfuse.trace()
def call_llm(prompt, platform):
    response = litellm.completion(model=platform, messages=[{"role": "user", "content": prompt}])
    return response
```

---

### Week 16 (Jul 6 - Jul 12)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Implement workflow templates (pre-built flows) | Talha | "Landing Page" template |
| 2-3 | Save custom workflows as templates | Talha | User creates templates |
| 3-4 | **Custom MCP server template** — easy to add new platforms | Both | Boilerplate for new connectors |
| 4-5 | Workflow sharing (export/import) | Atif | Share with team |
| 5-6 | Context memory (remember project state) | Atif | Resume previous work |
| 6-7 | Suggested next actions based on context | Both | Smart system demo |

**🎯 Week 16 Demo:** System suggests "Deploy your changes?" + reusable MCP template

---

## TOPIC 9: End-to-End Demo Scenarios
### Week 17 (Jul 13 - Jul 19)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Demo 1: "Build a blog and deploy it" | Both | Full recording |
| 2-3 | Demo 2: "Create SaaS with auth + payments" | Both | Full recording |
| 3-4 | Demo 3: "Research topic and create report" | Both | Full recording |
| 4-5 | Edge case testing (failures, timeouts) | Both | Robust handling |
| 5-6 | Performance optimization | Both | Faster responses |
| 6-7 | Security review (API keys, tokens) | Both | Secure system |

**🎯 Week 17 Demo:** Three polished demo scenarios ready for defense

---

### Week 18 (Jul 20 - Jul 26)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Load testing (multiple concurrent workflows) | Talha | Performance metrics |
| 2-3 | Error recovery testing | Talha | Graceful degradation |
| 3-4 | Cross-platform testing (Windows/Mac/Linux) | Both | Works everywhere |
| 4-5 | User testing with 3-5 people | Both | Feedback collected |
| 5-6 | Bug fixes from user testing | Both | Issues resolved |
| 6-7 | Final feature freeze | Both | No new features |

**🎯 Week 18 Demo:** Stable, tested system ready for documentation

---

## TOPIC 10: Documentation & Defense
### Week 19 (Jul 27 - Aug 2)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Write final project report (Chapter 1-3) | Both | Introduction, Lit Review, Methodology |
| 2-3 | Write final project report (Chapter 4-5) | Both | Implementation, Results |
| 3-4 | Create architecture diagrams | Atif | System design visuals |
| 4-5 | Create user guide documentation | Talha | How to use UAIOS |
| 5-6 | Create developer documentation | Talha | How to extend UAIOS |
| 6-7 | README cleanup + GitHub repo polish | Both | Professional repo |

**🎯 Week 19 Deliverable:** Complete thesis document draft

---

### Week 20 (Aug 3 - Aug 9)

| Day | Task | Owner | Deliverable |
|-----|------|-------|-------------|
| 1-2 | Record 10-minute demo video | Both | Video walkthrough |
| 2-3 | Create presentation slides (20-25 slides) | Both | Defense deck |
| 3-4 | Practice defense presentation | Both | Confident delivery |
| 4-5 | Prepare for Q&A (anticipate questions) | Both | Answer bank |
| 5-6 | Final code cleanup + comments | Both | Clean codebase |
| 6-7 | **FINAL DEFENSE** | Both | 🎓 Ship it! |

**🎯 Week 20 Deliverable:** Successful FYP defense!

---

# 📊 Summary: What You'll Have Built

## System Components

| Component | What It Does | Where |
|-----------|-------------|-------|
| **UAIOS IDE** | VS Code fork with custom UI | `vscode/` |
| **Chat Panel** | Natural language interface | Extension |
| **Platform Browser** | Search 500+ platforms | Extension |
| **Workflow Visualizer** | See DAG execution | Extension |
| **Backend API** | FastAPI orchestration server | `backend/` |
| **Platform Registry** | 500+ platforms indexed | PostgreSQL + ChromaDB |
| **Cognitive Layer** | Intent + Decomposition | LLM prompts |
| **Orchestration Engine** | DAG executor | LangGraph |
| **10 Connectors** | Active platform integrations | MCP + REST |

## Tech Stack Mastered

```
├── TypeScript (VS Code extension)
├── Python (FastAPI backend)
├── PostgreSQL + Redis (Database)
├── ChromaDB (Vector search)
├── LangGraph (Orchestration)
├── MCP Protocol (Tool calling)
├── OAuth 2.0 (Authentication)
├── WebSockets (Real-time updates)
└── Docker (Deployment)
```

## Competitive Features

| Feature | Cursor | Antigravity | UAIOS |
|---------|--------|-------------|-------|
| Code Generation | ✅ | ✅ | ✅ |
| Multi-Platform Orchestration | ❌ | ❌ | ✅ |
| 500+ Platform Registry | ❌ | ❌ | ✅ |
| Visual Workflow Builder | ❌ | ❌ | ✅ |
| Auto-Deploy Pipelines | ❌ | ✅ | ✅ |
| Adaptive Learning | ❌ | ❌ | ✅ |

---

# 📌 Quick Reference: Key Files to Create

```
d:\Semesters\FYP\
├── vscode/                          # Forked VS Code (already exists)
│   └── extensions/
│       └── uaios-core/              # Your main extension
│           ├── package.json
│           ├── src/
│           │   ├── extension.ts
│           │   ├── panels/
│           │   │   ├── chatPanel.ts
│           │   │   ├── platformBrowser.ts
│           │   │   └── workflowViewer.ts
│           │   └── services/
│           │       └── backendClient.ts
│           └── media/
│               └── styles.css
│
├── backend/                         # FastAPI backend
│   ├── app/
│   │   ├── main.py
│   │   ├── api/
│   │   │   ├── platforms.py
│   │   │   ├── cognitive.py
│   │   │   └── orchestrate.py
│   │   ├── core/
│   │   │   ├── cognitive.py
│   │   │   ├── orchestrator.py
│   │   │   └── registry.py
│   │   └── connectors/
│   │       ├── base.py
│   │       ├── mcp_client.py
│   │       ├── github.py
│   │       ├── vercel.py
│   │       └── ...
│   ├── data/
│   │   └── platforms.json
│   ├── requirements.txt
│   └── docker-compose.yml
│
└── documentations/                  # Project docs
    ├── Core_Understanding.md
    ├── Working Schedule Breakdown.md
    └── UAIOS_VSCode_Development_Schedule.md  # This file
```

---

# 🚀 Start Now Checklist

- [ ] Week 1, Day 1: Clone VS Code, run `yarn && yarn watch`
- [ ] Week 1, Day 2: Study `src/vs/workbench/` structure
- [ ] Week 1, Day 3: Update `product.json` with UAIOS branding
- [ ] Week 1, Day 4: Create GitHub Projects board with all milestones
- [ ] Week 1, Day 5: First commit with branding changes
- [ ] Week 1, Day 6: Screenshot of running UAIOS for teacher
- [ ] Week 1, Day 7: Document learnings in `vscode-structure-notes.md`

---

**Remember:** Every week must end with something DEMOABLE. Your teacher wants to see progress, not promises.

Good luck! 🎯
