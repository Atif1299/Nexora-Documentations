# Week 2: Building Extension Panels (Chat + Platform Browser)

> **Duration:** 7 Days  
> **Goal:** Create two custom sidebar panels in Nexora IDE  
> **End Deliverable:** Working "Nexora Chat" and "Platform Browser" panels visible in IDE

---

## 🎯 Week 2 Success Criteria

By the end of this week, you must have:
- [ ] First VS Code extension created (`nexora-core`)
- [ ] "Nexora Chat" sidebar panel visible and functional
- [ ] "Platform Browser" sidebar panel visible and functional
- [ ] Extension ↔ Backend IPC communication basics working
- [ ] GitHub Projects board set up with milestones
- [ ] Screenshot of both panels for teacher demo

---

## Prerequisites (From Week 1)

Before starting Week 2, verify:
- [ ] `yarn watch` runs without errors
- [ ] Nexora IDE launches with custom branding
- [ ] Development workflow established (watch + reload)
- [ ] Week 1 branch committed and pushed

---

## Day 1-2: Create First VS Code Extension (Hello World)

### What to Learn
- How VS Code extensions are structured
- Extension manifest (`package.json`) contribution points
- Extension activation and lifecycle
- How to register a sidebar view

### Tasks

#### Task 1.1: Create Extension Folder Structure

```powershell
# Navigate to extensions folder
cd d:\Semesters\FYP\vscode\extensions

# Create nexora-core extension folder
mkdir nexora-core
cd nexora-core

# Create folder structure
mkdir src
mkdir media
```

Create the following file structure:
```
vscode/extensions/nexora-core/
├── package.json          # Extension manifest (MOST IMPORTANT)
├── tsconfig.json         # TypeScript config
├── src/
│   ├── extension.ts      # Entry point
│   ├── chatPanel.ts      # Chat UI (Day 3-4)
│   └── platformPanel.ts  # Platform browser UI (Day 4-5)
└── media/
    ├── nexora-icon.svg   # Sidebar icon
    └── styles.css        # Panel styling
```

#### Task 1.2: Create Extension Manifest (package.json)

Create `d:\Semesters\FYP\vscode\extensions\nexora-core\package.json`:

```json
{
  "name": "nexora-core",
  "displayName": "Nexora Core",
  "description": "Universal AI Orchestration System - Core Extension",
  "version": "1.0.0",
  "publisher": "nexora-team",
  "engines": {
    "vscode": "^1.85.0"
  },
  "categories": [
    "Other"
  ],
  "activationEvents": [
    "onStartupFinished"
  ],
  "main": "./out/extension.js",
  "contributes": {
    "viewsContainers": {
      "activitybar": [
        {
          "id": "nexora-sidebar",
          "title": "Nexora AI",
          "icon": "media/nexora-icon.svg"
        }
      ]
    },
    "views": {
      "nexora-sidebar": [
        {
          "type": "webview",
          "id": "nexora.chatPanel",
          "name": "Nexora Chat",
          "contextualTitle": "AI Chat"
        },
        {
          "id": "nexora.platformBrowser",
          "name": "Platform Browser",
          "contextualTitle": "AI Platforms"
        }
      ]
    },
    "commands": [
      {
        "command": "nexora.openChat",
        "title": "Open Nexora Chat",
        "category": "Nexora"
      },
      {
        "command": "nexora.refreshPlatforms",
        "title": "Refresh Platforms",
        "category": "Nexora"
      }
    ]
  },
  "scripts": {
    "vscode:prepublish": "npm run compile",
    "compile": "tsc -p ./",
    "watch": "tsc -watch -p ./"
  },
  "devDependencies": {
    "@types/vscode": "^1.85.0",
    "@types/node": "^18.x",
    "typescript": "^5.3.0"
  }
}
```

#### Task 1.3: Create TypeScript Config (tsconfig.json)

Create `d:\Semesters\FYP\vscode\extensions\nexora-core\tsconfig.json`:

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "ES2020",
    "lib": ["ES2020"],
    "outDir": "out",
    "rootDir": "src",
    "sourceMap": true,
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true
  },
  "exclude": ["node_modules", ".vscode-test"]
}
```

#### Task 1.4: Create Extension Entry Point (extension.ts)

Create `d:\Semesters\FYP\vscode\extensions\nexora-core\src\extension.ts`:

```typescript
import * as vscode from 'vscode';

export function activate(context: vscode.ExtensionContext) {
    console.log('Nexora Core extension is now active!');

    // Register the chat panel command
    let openChatCommand = vscode.commands.registerCommand('nexora.openChat', () => {
        vscode.window.showInformationMessage('Nexora Chat: Coming soon!');
    });

    // Register the refresh platforms command
    let refreshPlatformsCommand = vscode.commands.registerCommand('nexora.refreshPlatforms', () => {
        vscode.window.showInformationMessage('Refreshing platforms...');
    });

    context.subscriptions.push(openChatCommand, refreshPlatformsCommand);

    // Show activation message
    vscode.window.showInformationMessage('🚀 Nexora AI Orchestration System activated!');
}

export function deactivate() {
    console.log('Nexora Core extension deactivated');
}
```

#### Task 1.5: Create Sidebar Icon

Create `d:\Semesters\FYP\vscode\extensions\nexora-core\media\nexora-icon.svg`:

```svg
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
  <circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2"/>
  <circle cx="12" cy="12" r="4" fill="currentColor"/>
  <path d="M12 2V6" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
  <path d="M12 18V22" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
  <path d="M2 12H6" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
  <path d="M18 12H22" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
</svg>
```

#### Task 1.6: Install Dependencies & Compile

```powershell
cd d:\Semesters\FYP\vscode\extensions\nexora-core

# Install dependencies
npm install

# Compile TypeScript
npm run compile
```

#### Task 1.7: Test Extension Loading

```powershell
# In terminal 1 (keep running)
cd d:\Semesters\FYP\vscode
yarn watch

# In terminal 2
.\scripts\code.bat
```

**Verify:**
- [ ] Nexora icon appears in Activity Bar (left sidebar)
- [ ] Clicking icon shows "Nexora Chat" and "Platform Browser" sections
- [ ] Ctrl+Shift+P → "Nexora: Open Chat" shows message

### Verification Checkpoint Day 1-2
- [ ] Extension folder structure created
- [ ] `package.json` manifest configured
- [ ] Extension compiles without errors
- [ ] Nexora icon visible in Activity Bar
- [ ] Basic commands registered and working

---

## Day 2-3: Study Webview API — Custom UI Panels

### What to Learn
- VS Code Webview API for rich HTML/CSS/JS panels
- How to create interactive UI inside VS Code
- Communication between extension and webview
- Security considerations (CSP)

### Tasks

#### Task 2.1: Study Webview Documentation

Read and understand:
- https://code.visualstudio.com/api/extension-guides/webview
- How `createWebviewPanel` works
- How `resolveWebviewView` works for sidebar panels
- Message passing between extension and webview

**Key Concepts to Document:**

| Concept | What It Does | We'll Use For |
|---------|-------------|---------------|
| `WebviewViewProvider` | Provides content for sidebar webview | Chat Panel, Platform Browser |
| `postMessage()` | Send data from extension to webview | Send platform list, chat responses |
| `onDidReceiveMessage` | Receive data from webview | User input, button clicks |
| `asWebviewUri()` | Convert local file to webview-safe URI | Load CSS, images |
| Content Security Policy | Security for webview content | Prevent XSS attacks |

#### Task 2.2: Create Sample Webview Panel

Update `d:\Semesters\FYP\vscode\extensions\nexora-core\src\extension.ts`:

```typescript
import * as vscode from 'vscode';
import { ChatPanelProvider } from './chatPanel';
import { PlatformBrowserProvider } from './platformPanel';

export function activate(context: vscode.ExtensionContext) {
    console.log('Nexora Core extension is now active!');

    // Register Chat Panel Provider
    const chatProvider = new ChatPanelProvider(context.extensionUri);
    context.subscriptions.push(
        vscode.window.registerWebviewViewProvider(
            'nexora.chatPanel',
            chatProvider
        )
    );

    // Register Platform Browser Provider
    const platformProvider = new PlatformBrowserProvider();
    context.subscriptions.push(
        vscode.window.registerTreeDataProvider(
            'nexora.platformBrowser',
            platformProvider
        )
    );

    // Register commands
    context.subscriptions.push(
        vscode.commands.registerCommand('nexora.openChat', () => {
            vscode.commands.executeCommand('nexora.chatPanel.focus');
        }),
        vscode.commands.registerCommand('nexora.refreshPlatforms', () => {
            platformProvider.refresh();
        })
    );

    vscode.window.showInformationMessage('🚀 Nexora AI activated!');
}

export function deactivate() {}
```

### Verification Checkpoint Day 2-3
- [ ] Understand Webview API basics
- [ ] Know how to create WebviewViewProvider
- [ ] Understand message passing pattern
- [ ] Updated extension.ts with providers

---

## Day 3-4: Build "Nexora Chat" Sidebar Panel

### What to Learn
- Implementing WebviewViewProvider
- Creating chat UI with HTML/CSS
- Handling user input in webview
- Sending messages between webview and extension

### Tasks

#### Task 3.1: Create Chat Panel Provider

Create `d:\Semesters\FYP\vscode\extensions\nexora-core\src\chatPanel.ts`:

```typescript
import * as vscode from 'vscode';

export class ChatPanelProvider implements vscode.WebviewViewProvider {
    public static readonly viewType = 'nexora.chatPanel';
    private _view?: vscode.WebviewView;

    constructor(private readonly _extensionUri: vscode.Uri) {}

    public resolveWebviewView(
        webviewView: vscode.WebviewView,
        context: vscode.WebviewViewResolveContext,
        _token: vscode.CancellationToken
    ) {
        this._view = webviewView;

        webviewView.webview.options = {
            enableScripts: true,
            localResourceRoots: [this._extensionUri]
        };

        webviewView.webview.html = this._getHtmlForWebview(webviewView.webview);

        // Handle messages from the webview
        webviewView.webview.onDidReceiveMessage(data => {
            switch (data.type) {
                case 'sendMessage':
                    this._handleUserMessage(data.message);
                    break;
                case 'clearChat':
                    // Handle clear chat
                    break;
            }
        });
    }

    private _handleUserMessage(message: string) {
        // For now, echo the message back
        // Later: Send to backend API for processing
        const response = `🤖 Nexora received: "${message}"\n\n[Backend integration coming in Week 3]`;
        
        if (this._view) {
            this._view.webview.postMessage({
                type: 'addMessage',
                role: 'assistant',
                content: response
            });
        }

        // Show in VS Code notification too
        vscode.window.showInformationMessage(`Processing: ${message.substring(0, 50)}...`);
    }

    private _getHtmlForWebview(webview: vscode.Webview): string {
        return `<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="Content-Security-Policy" content="default-src 'none'; style-src ${webview.cspSource} 'unsafe-inline'; script-src 'unsafe-inline';">
    <title>Nexora Chat</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            font-family: var(--vscode-font-family);
            font-size: var(--vscode-font-size);
            color: var(--vscode-foreground);
            background-color: var(--vscode-sideBar-background);
            height: 100vh;
            display: flex;
            flex-direction: column;
        }
        .chat-header {
            padding: 12px;
            border-bottom: 1px solid var(--vscode-panel-border);
            background: var(--vscode-sideBarSectionHeader-background);
        }
        .chat-header h3 {
            font-size: 13px;
            font-weight: 600;
            color: var(--vscode-sideBarTitle-foreground);
        }
        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 12px;
        }
        .message {
            margin-bottom: 12px;
            padding: 10px 12px;
            border-radius: 8px;
            max-width: 95%;
            word-wrap: break-word;
        }
        .message.user {
            background: var(--vscode-button-background);
            color: var(--vscode-button-foreground);
            margin-left: auto;
        }
        .message.assistant {
            background: var(--vscode-editor-background);
            border: 1px solid var(--vscode-panel-border);
        }
        .message-role {
            font-size: 11px;
            font-weight: 600;
            margin-bottom: 4px;
            opacity: 0.8;
        }
        .chat-input-container {
            padding: 12px;
            border-top: 1px solid var(--vscode-panel-border);
            background: var(--vscode-sideBar-background);
        }
        .chat-input-wrapper {
            display: flex;
            gap: 8px;
        }
        #chatInput {
            flex: 1;
            padding: 8px 12px;
            border: 1px solid var(--vscode-input-border);
            background: var(--vscode-input-background);
            color: var(--vscode-input-foreground);
            border-radius: 6px;
            font-size: 13px;
            outline: none;
        }
        #chatInput:focus {
            border-color: var(--vscode-focusBorder);
        }
        #sendBtn {
            padding: 8px 16px;
            background: var(--vscode-button-background);
            color: var(--vscode-button-foreground);
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 13px;
        }
        #sendBtn:hover {
            background: var(--vscode-button-hoverBackground);
        }
        .welcome-message {
            text-align: center;
            padding: 20px;
            opacity: 0.7;
        }
        .welcome-message h4 {
            margin-bottom: 8px;
        }
    </style>
</head>
<body>
    <div class="chat-header">
        <h3>🤖 Nexora AI Assistant</h3>
    </div>
    
    <div class="chat-messages" id="chatMessages">
        <div class="welcome-message">
            <h4>Welcome to Nexora!</h4>
            <p>Describe what you want to build, and I'll orchestrate the AI platforms to make it happen.</p>
        </div>
    </div>
    
    <div class="chat-input-container">
        <div class="chat-input-wrapper">
            <input type="text" id="chatInput" placeholder="Describe your project..." />
            <button id="sendBtn">Send</button>
        </div>
    </div>

    <script>
        const vscode = acquireVsCodeApi();
        const chatMessages = document.getElementById('chatMessages');
        const chatInput = document.getElementById('chatInput');
        const sendBtn = document.getElementById('sendBtn');

        function addMessage(role, content) {
            // Remove welcome message if present
            const welcome = chatMessages.querySelector('.welcome-message');
            if (welcome) welcome.remove();

            const messageDiv = document.createElement('div');
            messageDiv.className = 'message ' + role;
            
            const roleLabel = document.createElement('div');
            roleLabel.className = 'message-role';
            roleLabel.textContent = role === 'user' ? '👤 You' : '🤖 Nexora';
            
            const contentDiv = document.createElement('div');
            contentDiv.textContent = content;
            
            messageDiv.appendChild(roleLabel);
            messageDiv.appendChild(contentDiv);
            chatMessages.appendChild(messageDiv);
            
            // Scroll to bottom
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        function sendMessage() {
            const message = chatInput.value.trim();
            if (!message) return;

            // Add user message to UI
            addMessage('user', message);
            
            // Send to extension
            vscode.postMessage({
                type: 'sendMessage',
                message: message
            });

            // Clear input
            chatInput.value = '';
        }

        sendBtn.addEventListener('click', sendMessage);
        chatInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') sendMessage();
        });

        // Handle messages from extension
        window.addEventListener('message', event => {
            const message = event.data;
            switch (message.type) {
                case 'addMessage':
                    addMessage(message.role, message.content);
                    break;
            }
        });
    </script>
</body>
</html>`;
    }
}
```

#### Task 3.2: Test Chat Panel

```powershell
# Recompile extension
cd d:\Semesters\FYP\vscode\extensions\nexora-core
npm run compile

# Reload VS Code window (Ctrl+Shift+P → "Reload Window")
```

**Verify:**
- [ ] Chat panel shows in Nexora sidebar
- [ ] Can type message and press Send/Enter
- [ ] User message appears in chat
- [ ] Bot response appears (echo for now)
- [ ] Messages scroll properly

### Verification Checkpoint Day 3-4
- [ ] ChatPanelProvider implemented
- [ ] HTML/CSS chat UI working
- [ ] Message input and display working
- [ ] Extension ↔ Webview communication working

---

## Day 4-5: Build "Platform Browser" Sidebar Panel

### What to Learn
- VS Code TreeView API
- TreeDataProvider for hierarchical data
- Tree item icons and decorations
- Refresh and click handling

### Tasks

#### Task 4.1: Create Platform Browser Provider

Create `d:\Semesters\FYP\vscode\extensions\nexora-core\src\platformPanel.ts`:

```typescript
import * as vscode from 'vscode';

// Platform data structure
interface Platform {
    id: string;
    name: string;
    category: string;
    description: string;
    capabilities: string[];
    status: 'available' | 'connected' | 'unavailable';
}

// Sample platform data (will come from backend in Week 3)
const SAMPLE_PLATFORMS: Platform[] = [
    {
        id: 'openai',
        name: 'OpenAI GPT-4',
        category: 'LLM',
        description: 'Large language model for text generation',
        capabilities: ['text_generation', 'code_generation', 'chat'],
        status: 'available'
    },
    {
        id: 'claude',
        name: 'Anthropic Claude',
        category: 'LLM',
        description: 'AI assistant for analysis and coding',
        capabilities: ['text_generation', 'code_generation', 'analysis'],
        status: 'available'
    },
    {
        id: 'v0-dev',
        name: 'v0.dev',
        category: 'UI Generation',
        description: 'AI-powered UI component generator',
        capabilities: ['ui_generation', 'react_components'],
        status: 'available'
    },
    {
        id: 'github',
        name: 'GitHub',
        category: 'Version Control',
        description: 'Code repository and collaboration',
        capabilities: ['repo_management', 'version_control', 'ci_cd'],
        status: 'connected'
    },
    {
        id: 'vercel',
        name: 'Vercel',
        category: 'Deployment',
        description: 'Frontend deployment platform',
        capabilities: ['deployment', 'hosting', 'serverless'],
        status: 'available'
    },
    {
        id: 'supabase',
        name: 'Supabase',
        category: 'Database',
        description: 'Backend-as-a-Service with PostgreSQL',
        capabilities: ['database', 'auth', 'storage', 'realtime'],
        status: 'available'
    },
    {
        id: 'stripe',
        name: 'Stripe',
        category: 'Payments',
        description: 'Payment processing platform',
        capabilities: ['payments', 'subscriptions', 'invoicing'],
        status: 'unavailable'
    },
    {
        id: 'crewai',
        name: 'CrewAI',
        category: 'Multi-Agent',
        description: 'Multi-agent orchestration framework',
        capabilities: ['agent_orchestration', 'task_delegation'],
        status: 'available'
    }
];

// Tree item for a platform
class PlatformTreeItem extends vscode.TreeItem {
    constructor(
        public readonly platform: Platform,
        public readonly collapsibleState: vscode.TreeItemCollapsibleState
    ) {
        super(platform.name, collapsibleState);
        
        this.tooltip = `${platform.description}\n\nCapabilities: ${platform.capabilities.join(', ')}`;
        this.description = platform.category;
        
        // Set icon based on status
        this.iconPath = this._getStatusIcon(platform.status);
        
        // Set context value for conditional menus
        this.contextValue = platform.status;
    }

    private _getStatusIcon(status: string): vscode.ThemeIcon {
        switch (status) {
            case 'connected':
                return new vscode.ThemeIcon('check', new vscode.ThemeColor('charts.green'));
            case 'available':
                return new vscode.ThemeIcon('circle-outline');
            case 'unavailable':
                return new vscode.ThemeIcon('circle-slash', new vscode.ThemeColor('charts.red'));
            default:
                return new vscode.ThemeIcon('question');
        }
    }
}

// Tree item for a category
class CategoryTreeItem extends vscode.TreeItem {
    constructor(
        public readonly category: string,
        public readonly platforms: Platform[]
    ) {
        super(category, vscode.TreeItemCollapsibleState.Expanded);
        this.tooltip = `${platforms.length} platforms`;
        this.description = `(${platforms.length})`;
        this.iconPath = new vscode.ThemeIcon('folder');
    }
}

export class PlatformBrowserProvider implements vscode.TreeDataProvider<vscode.TreeItem> {
    private _onDidChangeTreeData: vscode.EventEmitter<vscode.TreeItem | undefined | null | void> = 
        new vscode.EventEmitter<vscode.TreeItem | undefined | null | void>();
    readonly onDidChangeTreeData: vscode.Event<vscode.TreeItem | undefined | null | void> = 
        this._onDidChangeTreeData.event;

    private platforms: Platform[] = SAMPLE_PLATFORMS;

    refresh(): void {
        this._onDidChangeTreeData.fire();
        vscode.window.showInformationMessage('Platforms refreshed!');
    }

    getTreeItem(element: vscode.TreeItem): vscode.TreeItem {
        return element;
    }

    getChildren(element?: vscode.TreeItem): Thenable<vscode.TreeItem[]> {
        if (!element) {
            // Root level: return categories
            const categories = this._groupByCategory();
            return Promise.resolve(
                Object.entries(categories).map(
                    ([category, platforms]) => new CategoryTreeItem(category, platforms)
                )
            );
        } else if (element instanceof CategoryTreeItem) {
            // Category level: return platforms in this category
            return Promise.resolve(
                element.platforms.map(
                    platform => new PlatformTreeItem(platform, vscode.TreeItemCollapsibleState.None)
                )
            );
        }
        return Promise.resolve([]);
    }

    private _groupByCategory(): Record<string, Platform[]> {
        return this.platforms.reduce((acc, platform) => {
            if (!acc[platform.category]) {
                acc[platform.category] = [];
            }
            acc[platform.category].push(platform);
            return acc;
        }, {} as Record<string, Platform[]>);
    }

    // Method to update platforms (will be called from backend later)
    updatePlatforms(platforms: Platform[]): void {
        this.platforms = platforms;
        this.refresh();
    }
}
```

#### Task 4.2: Update Extension to Handle Platform Selection

Update `d:\Semesters\FYP\vscode\extensions\nexora-core\src\extension.ts`:

```typescript
import * as vscode from 'vscode';
import { ChatPanelProvider } from './chatPanel';
import { PlatformBrowserProvider } from './platformPanel';

export function activate(context: vscode.ExtensionContext) {
    console.log('Nexora Core extension is now active!');

    // Register Chat Panel Provider
    const chatProvider = new ChatPanelProvider(context.extensionUri);
    context.subscriptions.push(
        vscode.window.registerWebviewViewProvider(
            'nexora.chatPanel',
            chatProvider
        )
    );

    // Register Platform Browser Provider
    const platformProvider = new PlatformBrowserProvider();
    const treeView = vscode.window.createTreeView('nexora.platformBrowser', {
        treeDataProvider: platformProvider,
        showCollapseAll: true
    });
    context.subscriptions.push(treeView);

    // Handle platform selection
    treeView.onDidChangeSelection(e => {
        if (e.selection.length > 0) {
            const selected = e.selection[0];
            if ('platform' in selected) {
                const platform = (selected as any).platform;
                vscode.window.showInformationMessage(
                    `Selected: ${platform.name} (${platform.status})`
                );
            }
        }
    });

    // Register commands
    context.subscriptions.push(
        vscode.commands.registerCommand('nexora.openChat', () => {
            vscode.commands.executeCommand('nexora.chatPanel.focus');
        }),
        vscode.commands.registerCommand('nexora.refreshPlatforms', () => {
            platformProvider.refresh();
        }),
        vscode.commands.registerCommand('nexora.connectPlatform', (item) => {
            if (item && item.platform) {
                vscode.window.showInformationMessage(
                    `Connecting to ${item.platform.name}... (OAuth flow coming in Week 8)`
                );
            }
        })
    );

    vscode.window.showInformationMessage('🚀 Nexora AI Orchestration System activated!');
}

export function deactivate() {}
```

#### Task 4.3: Add Context Menu for Platforms

Update `package.json` to add right-click menu:

```json
{
  "contributes": {
    "menus": {
      "view/item/context": [
        {
          "command": "nexora.connectPlatform",
          "when": "view == nexora.platformBrowser && viewItem == available",
          "group": "inline"
        }
      ]
    }
  }
}
```

#### Task 4.4: Test Platform Browser

```powershell
# Recompile
cd d:\Semesters\FYP\vscode\extensions\nexora-core
npm run compile

# Reload VS Code window
```

**Verify:**
- [ ] Platform Browser shows in Nexora sidebar
- [ ] Categories are expandable (LLM, UI Generation, etc.)
- [ ] Platforms show with status icons
- [ ] Clicking platform shows info message
- [ ] Refresh button works

### Verification Checkpoint Day 4-5
- [ ] PlatformBrowserProvider implemented
- [ ] TreeView with categories and platforms
- [ ] Status icons (connected/available/unavailable)
- [ ] Platform selection handling
- [ ] Context menu for connect action

---

## Day 5-6: Extension ↔ Backend IPC Communication Basics

### What to Learn
- How VS Code extensions communicate with external processes
- HTTP client in VS Code extensions
- Preparing for backend integration in Week 3

### Tasks

#### Task 5.1: Create Backend Client Service

Create `d:\Semesters\FYP\vscode\extensions\nexora-core\src\services\backendClient.ts`:

```typescript
import * as vscode from 'vscode';

export interface BackendConfig {
    baseUrl: string;
    timeout: number;
}

export class BackendClient {
    private config: BackendConfig;

    constructor(config?: Partial<BackendConfig>) {
        this.config = {
            baseUrl: config?.baseUrl || 'http://localhost:8000',
            timeout: config?.timeout || 30000
        };
    }

    // Health check
    async checkHealth(): Promise<boolean> {
        try {
            const response = await this._fetch('/api/health');
            return response.status === 'ok';
        } catch (error) {
            console.error('Backend health check failed:', error);
            return false;
        }
    }

    // Get platforms list
    async getPlatforms(): Promise<any[]> {
        try {
            const response = await this._fetch('/api/platforms');
            return response.platforms || [];
        } catch (error) {
            console.error('Failed to fetch platforms:', error);
            return [];
        }
    }

    // Search platforms
    async searchPlatforms(query: string): Promise<any[]> {
        try {
            const response = await this._fetch(`/api/platforms/search?q=${encodeURIComponent(query)}`);
            return response.results || [];
        } catch (error) {
            console.error('Failed to search platforms:', error);
            return [];
        }
    }

    // Send chat message (will be implemented in Week 5)
    async sendMessage(message: string): Promise<any> {
        try {
            const response = await this._post('/api/cognitive/classify', { message });
            return response;
        } catch (error) {
            console.error('Failed to send message:', error);
            throw error;
        }
    }

    // Generic GET request
    private async _fetch(endpoint: string): Promise<any> {
        const url = `${this.config.baseUrl}${endpoint}`;
        
        // Using VS Code's built-in fetch (available in recent versions)
        // For older versions, we'd use node-fetch
        try {
            const response = await fetch(url, {
                method: 'GET',
                headers: {
                    'Content-Type': 'application/json'
                }
            });
            
            if (!response.ok) {
                throw new Error(`HTTP ${response.status}: ${response.statusText}`);
            }
            
            return await response.json();
        } catch (error) {
            // Backend not running yet - return mock data
            console.log('Backend not available, using mock data');
            return this._getMockData(endpoint);
        }
    }

    // Generic POST request
    private async _post(endpoint: string, data: any): Promise<any> {
        const url = `${this.config.baseUrl}${endpoint}`;
        
        try {
            const response = await fetch(url, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(data)
            });
            
            if (!response.ok) {
                throw new Error(`HTTP ${response.status}: ${response.statusText}`);
            }
            
            return await response.json();
        } catch (error) {
            console.log('Backend not available for POST');
            throw error;
        }
    }

    // Mock data for development (before backend is ready)
    private _getMockData(endpoint: string): any {
        if (endpoint === '/api/health') {
            return { status: 'ok', message: 'Mock backend' };
        }
        if (endpoint === '/api/platforms') {
            return {
                platforms: [
                    { id: 'openai', name: 'OpenAI GPT-4', category: 'LLM', status: 'available' },
                    { id: 'claude', name: 'Anthropic Claude', category: 'LLM', status: 'available' },
                    { id: 'v0-dev', name: 'v0.dev', category: 'UI Generation', status: 'available' },
                    { id: 'github', name: 'GitHub', category: 'Version Control', status: 'connected' },
                    { id: 'vercel', name: 'Vercel', category: 'Deployment', status: 'available' }
                ]
            };
        }
        return {};
    }
}

// Singleton instance
let backendClient: BackendClient | null = null;

export function getBackendClient(): BackendClient {
    if (!backendClient) {
        backendClient = new BackendClient();
    }
    return backendClient;
}
```

#### Task 5.2: Create Services Folder and Index

Create `d:\Semesters\FYP\vscode\extensions\nexora-core\src\services\index.ts`:

```typescript
export { BackendClient, getBackendClient } from './backendClient';
```

#### Task 5.3: Update Extension to Use Backend Client

Update `extension.ts` to check backend on activation:

```typescript
import * as vscode from 'vscode';
import { ChatPanelProvider } from './chatPanel';
import { PlatformBrowserProvider } from './platformPanel';
import { getBackendClient } from './services';

export async function activate(context: vscode.ExtensionContext) {
    console.log('Nexora Core extension is now active!');

    // Check backend health
    const backendClient = getBackendClient();
    const isBackendHealthy = await backendClient.checkHealth();
    
    if (isBackendHealthy) {
        vscode.window.showInformationMessage('🚀 Nexora connected to backend!');
    } else {
        vscode.window.showWarningMessage('⚠️ Nexora backend not available. Using offline mode.');
    }

    // ... rest of activation code
}
```

#### Task 5.4: Update tsconfig for Services

Update `tsconfig.json`:

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "ES2020",
    "lib": ["ES2020", "DOM"],
    "outDir": "out",
    "rootDir": "src",
    "sourceMap": true,
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "resolveJsonModule": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", ".vscode-test"]
}
```

### Verification Checkpoint Day 5-6
- [ ] BackendClient service created
- [ ] Mock data returns when backend not running
- [ ] Extension shows warning when backend unavailable
- [ ] Ready for Week 3 backend integration

---

## Day 6-7: GitHub Projects Board Setup + Documentation

### What to Learn
- Setting up project management in GitHub
- Creating milestones and sprints
- Documenting extension architecture

### Tasks

#### Task 6.1: Set Up GitHub Projects Board

1. Go to your GitHub repo: `https://github.com/YOUR_USERNAME/vscode`
2. Click "Projects" tab
3. Create new project: "Nexora Development"
4. Set up columns:
   - 📋 Backlog
   - 🏃 Sprint (Current)
   - 🔨 In Progress
   - 👀 Review
   - ✅ Done

#### Task 6.2: Create Milestones

Create these milestones in GitHub Issues:

| Milestone | Due Date | Description |
|-----------|----------|-------------|
| Week 1-2: IDE Foundation | Week 2 End | VS Code fork + Extension panels |
| Week 3-4: Backend + Registry | Week 4 End | FastAPI + Platform search |
| Week 5-6: Cognitive Layer | Week 6 End | Intent + Decomposition |
| Week 7-8: First Connectors | Week 8 End | GitHub + Vercel integration |
| Week 9-10: Orchestration | Week 10 End | Semester 1 Demo |

#### Task 6.3: Create Week 2 Issues

Create these issues and add to Sprint:

1. **[Extension] Create nexora-core extension structure** ✅
2. **[Extension] Implement Chat Panel with Webview** ✅
3. **[Extension] Implement Platform Browser TreeView** ✅
4. **[Extension] Create BackendClient service** ✅
5. **[Docs] Update vscode-structure-notes.md**
6. **[Git] Commit Week 2 changes to branch**

#### Task 6.4: Update Documentation

Update `d:\Semesters\FYP\vscode\vscode-structure-notes.md`:

```markdown
# VS Code Structure Notes

## Week 1 Learnings
- [Previous content...]

## Week 2 Learnings

### Extension Architecture

Our `nexora-core` extension structure:
```
extensions/nexora-core/
├── package.json          # Manifest with contributions
├── tsconfig.json         # TypeScript config
├── src/
│   ├── extension.ts      # Entry point, registers providers
│   ├── chatPanel.ts      # WebviewViewProvider for chat
│   ├── platformPanel.ts  # TreeDataProvider for platforms
│   └── services/
│       ├── index.ts      # Service exports
│       └── backendClient.ts  # HTTP client for backend
└── media/
    └── nexora-icon.svg   # Activity bar icon
```

### Key VS Code APIs Used

| API | Purpose | File |
|-----|---------|------|
| `WebviewViewProvider` | Sidebar webview panel | chatPanel.ts |
| `TreeDataProvider` | Hierarchical tree view | platformPanel.ts |
| `TreeView` | Tree view with selection | extension.ts |
| `commands.registerCommand` | Register commands | extension.ts |
| `window.showInformationMessage` | Notifications | extension.ts |

### Extension ↔ Webview Communication

```
Extension (TypeScript)          Webview (HTML/JS)
        │                              │
        │  webview.postMessage({})     │
        │ ──────────────────────────►  │
        │                              │
        │  vscode.postMessage({})      │
        │ ◄──────────────────────────  │
        │                              │
```

### Next Steps (Week 3)
- Set up FastAPI backend
- Create Platform Registry database
- Connect extension to real backend API
```

#### Task 6.5: Git Commit Week 2

```powershell
cd d:\Semesters\FYP\vscode

# Create Week 2 branch
git checkout -b Week2-Extension-Panels

# Stage all changes
git add .

# Commit
git commit -m "Week 2: Nexora Chat Panel + Platform Browser extension

- Created nexora-core extension structure
- Implemented ChatPanelProvider with Webview UI
- Implemented PlatformBrowserProvider with TreeView
- Added BackendClient service for API communication
- Set up mock data for offline development
- Updated documentation"

# Push to fork
git push origin Week2-Extension-Panels
```

### Verification Checkpoint Day 6-7
- [ ] GitHub Projects board created
- [ ] Milestones set up
- [ ] Week 2 issues created and tracked
- [ ] Documentation updated
- [ ] Git branch created and pushed

---

## 📋 Week 2 Checklist Summary

### Technical Deliverables
- [ ] `nexora-core` extension folder created
- [ ] `package.json` manifest with viewsContainers and views
- [ ] `extension.ts` entry point with providers registered
- [ ] `chatPanel.ts` — WebviewViewProvider with chat UI
- [ ] `platformPanel.ts` — TreeDataProvider with categories
- [ ] `services/backendClient.ts` — HTTP client ready
- [ ] Extension compiles without errors
- [ ] Both panels visible in Nexora sidebar

### UI Deliverables
- [ ] Nexora icon in Activity Bar
- [ ] Chat Panel with input, send button, message display
- [ ] Platform Browser with expandable categories
- [ ] Platform status icons (connected/available/unavailable)

### Documentation Deliverables
- [ ] `vscode-structure-notes.md` updated with Week 2 learnings
- [ ] GitHub Projects board set up
- [ ] Milestones created

### Git Deliverables
- [ ] Branch `Week2-Extension-Panels` created
- [ ] All changes committed with descriptive message
- [ ] Pushed to GitHub fork

### Demo Deliverables
- [ ] Screenshot of Nexora sidebar with both panels
- [ ] Can demonstrate chat input/output
- [ ] Can demonstrate platform browser navigation
- [ ] Can explain extension architecture to teacher

---

## 🚨 Common Issues & Solutions

| Issue | Solution |
|-------|----------|
| Extension not loading | Check `package.json` for syntax errors, run `npm run compile` |
| Webview blank | Check CSP in HTML, verify `enableScripts: true` |
| TreeView not showing | Verify view ID matches in `package.json` and `registerTreeDataProvider` |
| Icon not appearing | Check SVG path, verify `viewsContainers` in manifest |
| TypeScript errors | Run `npm install`, check `tsconfig.json` |
| Changes not reflecting | Run `npm run compile`, then Reload Window |
| Backend connection fails | Expected — backend not built yet, mock data should work |

---

## 📎 Resources

- **VS Code Webview Guide:** https://code.visualstudio.com/api/extension-guides/webview
- **VS Code TreeView Guide:** https://code.visualstudio.com/api/extension-guides/tree-view
- **VS Code Extension Samples:** https://github.com/microsoft/vscode-extension-samples
- **TypeScript Handbook:** https://www.typescriptlang.org/docs/handbook/

---

## ✅ End of Week 2

When you complete all checkpoints:
1. Push all changes to your fork
2. Take screenshots for teacher demo
3. Prepare to show both panels working
4. Move to Week 3: Backend Foundation (FastAPI + Platform Registry)

**Next Week Preview:** Set up FastAPI backend, PostgreSQL database, and connect the Platform Browser to real data from the backend API.
