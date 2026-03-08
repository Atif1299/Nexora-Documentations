# Nexora-Documentations

FYP/
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