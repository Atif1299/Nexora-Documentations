

## Project Management Tools — My Top 3 Picks

| Tool | Why It's Best for Your FYP | Free? |
|------|---------------------------|-------|
| **1. Linear** | Built for software teams. Clean sprints, roadmaps, GitHub integration. Your teacher will love the visual progress. | Free for 2 members |
| **2. GitHub Projects** | Already where your code lives. Kanban boards + issues + milestones. Zero extra setup. | Free |
| **3. Notion** | Best for combining docs + tasks + wiki. Great for FYP documentation alongside task tracking. | Free for education |

**My recommendation: GitHub Projects (for tasks/sprints) + Notion (for documentation/research notes).** This combo is what real startups use and will impress your supervisor.

---

## The Realistic Timeline — 6 Months Breakdown

You have **2 people × 6 months**. Let me be brutally honest about scope and give you a plan that **actually ships**.

---

### SEMESTER 1: Foundation + Core Engine (10 Weeks)

---

#### Sprint 1 — Week 1-2 (Feb 21 → Mar 6): Project Setup & Research

| Task | Owner | Deliverable |
|------|-------|-------------|
| Fork VS Code / OpenVSCode Server | Atif | Running forked IDE |
| Set up monorepo (backend + frontend + extension) | Atif | GitHub repo with CI |
| Deep-dive MCP Protocol docs + build hello-world MCP server | Talha | Working MCP client/server |
| Deep-dive LangGraph + LangChain docs | Talha | Sample agent workflow |
| Set up FastAPI backend skeleton | Atif | `/api/health` endpoint live |
| Set up PostgreSQL + Redis locally | Atif | Docker compose file |
| Create project board in GitHub Projects | Both | Sprint board ready |

**Milestone: Dev environment running, team understands MCP + LangGraph**

---

#### Sprint 2 — Week 3-4 (Mar 7 → Mar 20): Platform Registry

| Task | Owner | Deliverable |
|------|-------|-------------|
| Design Platform Registry schema (name, category, capabilities, API type, auth type, cost) | Talha | DB schema + seed data |
| Populate registry with 50+ platforms (from your massive list) as JSON/DB entries | Both | `platforms.json` with metadata |
| Set up ChromaDB for semantic search over platform capabilities | Talha | "Find me a code generator" → returns Cursor, Claude Code, etc. |
| Build `/api/platforms/search` endpoint | Atif | REST API that takes natural language → returns ranked platforms |
| Build `/api/platforms/{id}` detail endpoint | Atif | Platform detail with capabilities |

**Milestone: You can search "I need to deploy a website" and get back [Vercel, Railway, Netlify] ranked**

---

#### Sprint 3 — Week 5-6 (Mar 21 → Apr 3): Cognitive Layer (The Brain)

| Task | Owner | Deliverable |
|------|-------|-------------|
| Build Intent Classifier using Claude/GPT function calling | Talha | User input → structured intent JSON |
| Build Requirement Decomposer (single task → sub-task DAG) | Talha | "Build a blog" → [Research, Design, Code, Deploy] |
| Build Task Dependency Graph (DAG) generator | Atif | Determines which tasks can run in parallel vs sequential |
| Connect decomposer → platform registry (auto-select platforms per sub-task) | Atif | Each sub-task gets matched to best platform |
| Build `/api/orchestrate/plan` endpoint | Both | User requirement → full execution plan with platforms |

**Milestone: User says "Build a landing page" → system returns a plan: v0 for UI → Claude for code → Vercel for deploy**

---

#### Sprint 4 — Week 7-8 (Apr 4 → Apr 17): First 3 Platform Connectors

| Task | Owner | Deliverable |
|------|-------|-------------|
| Build MCP Client adapter (generic) | Talha | Can call any MCP-compatible server |
| Build REST API adapter (generic) | Atif | Can call any REST API with auth |
| Connector #1: OpenAI/Claude API (LLM brain) | Talha | Generate text/code on demand |
| Connector #2: GitHub API (repo creation, commits, PRs) | Atif | Auto-create repos, push code |
| Connector #3: Vercel API (deploy from GitHub) | Atif | Auto-deploy a project |
| Integration test: Generate code → Push to GitHub → Deploy to Vercel | Both | End-to-end test passing |

**Milestone: System can autonomously generate a file, push to GitHub, and deploy it to Vercel**

---

#### Sprint 5 — Week 9-10 (Apr 18 → May 1): Orchestration Engine + VS Code Integration

| Task | Owner | Deliverable |
|------|-------|-------------|
| Build DAG Executor (sequential + parallel task runner) | Talha | Executes plan steps in correct order |
| Build state machine (pending → running → success/failed → retry/fallback) | Talha | Each task has lifecycle |
| Error handling: retry 3x → fallback platform → escalate to user | Atif | Robust execution |
| Build VS Code extension sidebar (chat panel) | Atif | User can type requirements in IDE |
| Connect extension → backend API | Both | Chat in IDE → hits orchestration API |
| **SEMESTER 1 DEMO** | Both | Live demo for supervisor |

**Milestone: Working demo — type in IDE → system plans → executes across 3 platforms → delivers result**

---

### VACATION: Month Off (May 2 → May 31)

Don't burn out. But do these light tasks:

| Task | Owner | Time |
|------|-------|------|
| Add 5 more platform connectors (Supabase, Stripe, ElevenLabs, v0, CrewAI) | Both | ~1 week casual |
| Write mid-project report/documentation | Both | ~3-4 days |
| Research A2A protocol for next semester | Talha | Reading only |
| UI/UX mockups for the IDE interface | Atif | Figma designs |

---

### SEMESTER 2: Advanced Features + Polish (10 Weeks)

---

#### Sprint 6 — Week 1-2: Advanced IDE Interface

| Task | Owner | Deliverable |
|------|-------|-------------|
| Build visual workflow viewer (show DAG execution in real-time) | Atif | User sees tasks executing with status |
| WebSocket streaming (live execution logs to IDE) | Atif | Real-time progress updates |
| Build platform browser panel (browse 500+ platforms in IDE) | Talha | Searchable catalog in sidebar |
| Build execution history panel | Talha | Past workflows with results |

---

#### Sprint 7 — Week 3-4: OAuth + More Connectors

| Task | Owner | Deliverable |
|------|-------|-------------|
| OAuth 2.0 flow for GitHub, Vercel, Stripe | Atif | User connects accounts once |
| Connector #4: Supabase (database setup) | Talha | Auto-create tables, auth |
| Connector #5: Stripe (payment setup) | Atif | Auto-create products, checkout |
| Connector #6: v0.dev or Lovable (UI generation) | Talha | Generate UI components |
| Connector #7: CrewAI (multi-agent sub-workflows) | Talha | Complex tasks delegated to agent crews |

---

#### Sprint 8 — Week 5-6: Adaptive Intelligence

| Task | Owner | Deliverable |
|------|-------|-------------|
| Track platform success/failure rates per task type | Talha | Analytics DB |
| Auto-improve platform selection based on history | Talha | System gets smarter over time |
| User preference learning (remembers preferred platforms) | Atif | Personalized recommendations |
| Cost tracking and optimization | Atif | Shows cost per workflow |

---

#### Sprint 9 — Week 7-8: End-to-End Demo Scenarios

| Task | Owner | Deliverable |
|------|-------|-------------|
| Demo 1: "Build a blog and deploy it" | Both | Full autonomous execution |
| Demo 2: "Create a SaaS with auth + payments" | Both | Multi-platform orchestration |
| Demo 3: "Research a topic and create a report" | Both | Research agent workflow |
| Edge case testing + error handling | Both | Robust system |
| Performance optimization | Both | Fast responses |

---

#### Sprint 10 — Week 9-10: Documentation + Final Defense

| Task | Owner | Deliverable |
|------|-------|-------------|
| Final project report (full thesis) | Both | Complete document |
| Architecture diagrams | Atif | System design docs |
| Video demo recording | Both | 10-min walkthrough |
| Presentation slides | Both | Defense-ready |
| Code cleanup + README | Both | Professional repo |
| **FINAL DEFENSE** | Both | Ship it! |

---

## GitHub Projects Board Structure

Set up these columns:

```
📋 Backlog → 🏃 Sprint (Current) → 🔨 In Progress → 👀 Review → ✅ Done
```

**Labels to create:**
- `cognitive-layer`, `registry`, `orchestration`, `connector`, `ide-ui`, `docs`, `infra`
- `P0-critical`, `P1-important`, `P2-nice-to-have`
- `atif`, `talha`

**Milestones to create:**
1. `Sprint 1-2: Foundation` (Mar 6)
2. `Sprint 3-4: Brain + Registry` (Apr 3)
3. `Sprint 5: Semester 1 Demo` (May 1)
4. `Sprint 6-7: Advanced IDE` (Jul 15)
5. `Sprint 8-9: Intelligence + Demos` (Aug 15)
6. `Sprint 10: Final Defense` (Aug 31)

---

## The Key Rule

> **Every 2-week sprint must end with something DEMOABLE.**

Your teacher doesn't care about 80% done features. They care about **working demos** that show progress. Each sprint above ends with a concrete, showable result.

Want me to set up the initial project structure in your `FYP Working` directory now?