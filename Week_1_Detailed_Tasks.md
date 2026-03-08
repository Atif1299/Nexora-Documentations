# Week 1: VS Code Fork Setup & Understanding

> **Duration:** 7 Days  
> **Goal:** Get UAIOS fork running with custom branding  
> **End Deliverable:** Running IDE with "UAIOS" title, ready for development

---

## 🎯 Week 1 Success Criteria

By the end of this week, you must have:
- [ ] VS Code fork cloned and running from source
- [ ] Understanding of VS Code's folder structure documented
- [ ] Custom branding (UAIOS name, icons) applied
- [ ] Hot reload development workflow working
- [ ] Screenshot of running UAIOS ready for teacher demo

---

## Day 1-2: Clone & Understand VS Code Structure

### What to Learn
- How VS Code is organized as a project
- The difference between `src/vs/` (core) and `extensions/` (plugins)
- How the workbench UI is structured

### Tasks

#### Task 1.1: Clone the VS Code Fork
```powershell
# Navigate to your FYP folder
cd d:\Semesters\FYP

# The vscode folder should already exist (forked)
cd vscode

# Verify you're in the right place
ls
# Should see: src/, extensions/, package.json, product.json, etc.
```

#### Task 1.2: Install Dependencies
```powershell
# Install Node.js 18+ if not already installed
# Check version
node --version   # Should be 18.x or higher
npm --version

# Install yarn globally if needed
npm install -g yarn

# Install VS Code dependencies (this takes 10-15 minutes)
yarn
```

#### Task 1.3: Study the Folder Structure

Create a document `vscode-structure-notes.md` with your findings:

```
d:\Semesters\FYP\vscode\
│
├── src/                          # CORE SOURCE CODE
│   └── vs/                       # Main VS Code source
│       ├── base/                 # Base utilities, UI components
│       ├── platform/             # Platform services (file, storage, etc.)
│       ├── editor/               # Monaco editor (the text editor)
│       ├── workbench/            # ⭐ THE MAIN UI - WHERE YOU'LL WORK
│       │   ├── browser/          # Browser-specific workbench
│       │   ├── contrib/          # ⭐ Built-in features (terminal, debug, etc.)
│       │   ├── services/         # Workbench services
│       │   └── api/              # Extension API implementation
│       └── code/                 # Electron main process
│
├── extensions/                   # ⭐ BUILT-IN EXTENSIONS
│   ├── git/                      # Git integration
│   ├── typescript-language-features/
│   ├── markdown-language-features/
│   └── ...                       # Study these as examples
│
├── product.json                  # ⭐ BRANDING - name, icons, etc.
├── package.json                  # Dependencies
├── build/                        # Build scripts
└── resources/                    # Icons, images
```

### Key Files to Study

| File | What It Does | Why Important |
|------|-------------|---------------|
| `product.json` | Defines product name, icons, URLs | You'll edit this for UAIOS branding |
| `src/vs/workbench/browser/workbench.ts` | Main workbench entry | Understand how UI initializes |
| `src/vs/workbench/contrib/` | Built-in features | Examples of adding features |
| `extensions/git/package.json` | Extension manifest | Template for your extension |

### Verification Checkpoint
- [ ] Can list all folders in `src/vs/`
- [ ] Understand what `workbench` is (the main IDE UI)
- [ ] Know where extensions live
- [ ] Created `vscode-structure-notes.md`

---

## Day 2-3: Study the Workbench UI

### What to Learn
- How VS Code renders the sidebar, editor area, panel
- What "contributions" are (how features register themselves)
- How the Activity Bar (left icons) works

### Tasks

#### Task 2.1: Study Workbench Layout

Open and study these files:

```
src/vs/workbench/browser/
├── layout.ts              # How the layout is structured
├── parts/
│   ├── activitybar/       # ⭐ Left sidebar icons
│   ├── sidebar/           # ⭐ Sidebar panels (Explorer, Search, etc.)
│   ├── editor/            # Editor area
│   ├── panel/             # Bottom panel (Terminal, Problems, etc.)
│   └── statusbar/         # Bottom status bar
```

#### Task 2.2: Understand Contributions

Look at how existing features register:

```typescript
// Example from src/vs/workbench/contrib/terminal/browser/terminal.contribution.ts
// This file registers the Terminal feature

// Key patterns to note:
// 1. Registry.as() - registers viewlets, panels, commands
// 2. registerSingleton() - registers services
// 3. MenuRegistry - adds menu items
```

#### Task 2.3: Study Extension Points (Atif Focus)

In `src/vs/workbench/contrib/`, study:
- `files/` - File explorer implementation
- `search/` - Search panel implementation
- `scm/` - Source control panel

Note the pattern:
1. `*.contribution.ts` - Registers the feature
2. `*View.ts` or `*Viewlet.ts` - The UI component
3. `*Service.ts` - Business logic

### Deliverable
Document in `vscode-structure-notes.md`:
- [ ] How to add a new icon to Activity Bar
- [ ] How to add a new sidebar panel
- [ ] Where to register your custom UI

---

## Day 3-4: Study Extensions Folder (Talha Focus)

### What to Learn
- How built-in extensions are structured
- The Extension API (what's available to extensions)
- Difference between built-in extensions and user extensions

### Tasks

#### Task 3.1: Study a Simple Extension

Look at `extensions/markdown-basics/`:
```
extensions/markdown-basics/
├── package.json           # Extension manifest (most important!)
├── language-configuration.json
└── syntaxes/              # TextMate grammars
```

Study `package.json`:
```json
{
  "name": "markdown-basics",
  "contributes": {
    "languages": [...],      // Language registration
    "grammars": [...],       // Syntax highlighting
    "snippets": [...],       // Code snippets
    "commands": [...],       // Commands (Cmd+Shift+P)
    "views": [...],          // Custom views/panels
    "viewsContainers": [...] // Custom sidebar sections
  }
}
```

#### Task 3.2: Study a Complex Extension

Look at `extensions/git/`:
```
extensions/git/
├── package.json           # Complex manifest with many contributions
├── src/
│   ├── main.ts           # Extension entry point
│   ├── git.ts            # Git operations
│   ├── repository.ts     # Repository management
│   └── commands/         # Command implementations
```

Key things to note:
- `activationEvents` - When extension loads
- `contributes.views` - Custom sidebar panels
- `contributes.commands` - Registered commands

#### Task 3.3: List Available Extension APIs

Create a list of APIs we'll use for UAIOS:

| API | What It Does | We'll Use For |
|-----|-------------|---------------|
| `vscode.window` | Windows, editors, panels | Creating Chat Panel |
| `vscode.workspace` | Files, folders, settings | Reading project files |
| `vscode.commands` | Register/execute commands | UAIOS commands |
| `vscode.webview` | Custom HTML/JS panels | Rich UI for workflows |
| `vscode.TreeView` | Tree-based views | Platform Browser |

### Deliverable
- [ ] List of 10+ Extension APIs with descriptions
- [ ] Understanding of `package.json` contribution points
- [ ] Notes on how Git extension structures its code

---

## Day 4-5: Run VS Code from Source

### What to Learn
- How to compile and run VS Code
- Hot reload workflow
- Debugging the extension host

### Tasks

#### Task 4.1: Compile VS Code

```powershell
cd d:\Semesters\FYP\vscode

# Compile the source (first time takes 5-10 minutes)
yarn compile

# OR use watch mode for development (recommended)
yarn watch
```

#### Task 4.2: Run VS Code

```powershell
# In a NEW terminal (keep yarn watch running)
# Run the compiled VS Code
.\scripts\code.bat

# OR on Windows, you can also use:
yarn start
```

**Expected Result:** VS Code opens, but it's YOUR compiled version!

#### Task 4.3: Verify It's Your Fork

1. Open VS Code that just launched
2. Go to Help → About
3. It should show version info from YOUR build
4. The title bar might still say "Code - OSS" (we'll change this)

#### Task 4.4: Test Hot Reload

1. Keep `yarn watch` running
2. Make a small change in a TypeScript file
3. Wait for recompile (watch the terminal)
4. Reload VS Code window (Ctrl+Shift+P → "Reload Window")
5. See your change!

### Troubleshooting

| Problem | Solution |
|---------|----------|
| `yarn` fails | Make sure Node.js 18+ is installed |
| Compile errors | Run `yarn` again to reinstall deps |
| VS Code won't start | Check terminal for errors, try `yarn compile` first |
| Changes not showing | Make sure `yarn watch` is running, then reload window |

### Verification Checkpoint
- [ ] `yarn watch` runs without errors
- [ ] VS Code launches from source
- [ ] Can make a change and see it after reload
- [ ] Screenshot taken of running VS Code

---

## Day 5-6: Update Branding to UAIOS

### What to Learn
- How VS Code branding is configured
- Which files control the name, icons, splash screen

### Tasks

#### Task 5.1: Edit product.json

**This is the main branding file.** It should already have UAIOS changes from before, but verify:

```powershell
# Open product.json
code d:\Semesters\FYP\vscode\product.json
```

Key fields to verify/update:

```json
{
  "nameShort": "UAIOS",
  "nameLong": "UAIOS - Universal AI Orchestration System",
  "applicationName": "uaios",
  "dataFolderName": ".uaios",
  "win32MutexName": "uaios",
  "urlProtocol": "uaios",
  "win32DirName": "UAIOS",
  "win32NameVersion": "UAIOS",
  "win32ShellNameShort": "UAIOS",
  "serverApplicationName": "uaios-server",
  "serverDataFolderName": ".uaios-server",
  "tunnelApplicationName": "uaios-tunnel",
  "linuxIconName": "uaios",
  "licenseFileName": "LICENSE.txt"
}
```

#### Task 5.2: Verify Branding Changes

After editing `product.json`:

```powershell
# Recompile
yarn compile

# Run
.\scripts\code.bat
```

**Check:**
- [ ] Window title says "UAIOS" (not "Code - OSS")
- [ ] About dialog shows "UAIOS"
- [ ] Application name in taskbar is correct

#### Task 5.3: Update Icons (Optional but Recommended)

Icons are in the `resources/` folder:

```
resources/
├── win32/
│   ├── code.ico           # Windows icon - replace with UAIOS icon
│   └── code_70x70.png     # Taskbar icon
├── linux/
│   └── code.png           # Linux icon
└── darwin/
    └── code.icns          # macOS icon
```

To create UAIOS icons:
1. Design a simple logo (can use AI tools)
2. Create in sizes: 16x16, 32x32, 64x64, 128x128, 256x256, 512x512
3. Convert to .ico (Windows), .icns (macOS), .png (Linux)
4. Replace the files in `resources/`

**Note:** Icon changes require rebuild: `yarn compile`

#### Task 5.4: Update Package.json Metadata

Edit `package.json` in root:

```json
{
  "name": "uaios",
  "version": "1.0.0",
  "author": {
    "name": "UAIOS Team - Muhammad Atif & Talha Asif"
  },
  "description": "Universal AI Orchestration System - Agentic IDE"
}
```

### Verification Checkpoint
- [ ] Window title shows "UAIOS"
- [ ] About dialog shows correct name
- [ ] Product.json has all UAIOS values
- [ ] Screenshot taken showing branding

---

## Day 6-7: Set Up Development Workflow

### What to Learn
- Efficient development cycle
- Debugging extensions
- Using VS Code to develop VS Code

### Tasks

#### Task 6.1: Set Up Two-Terminal Workflow

**Terminal 1 (Watch):**
```powershell
cd d:\Semesters\FYP\vscode
yarn watch
# Keep this running - it recompiles on changes
```

**Terminal 2 (Run):**
```powershell
cd d:\Semesters\FYP\vscode
.\scripts\code.bat
# Launches VS Code
# When you make changes, just Ctrl+Shift+P → "Reload Window"
```

#### Task 6.2: Debug Configuration

Create/verify `.vscode/launch.json` in the vscode folder:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Launch VS Code",
      "type": "node",
      "request": "launch",
      "runtimeExecutable": "${workspaceFolder}/scripts/code.bat",
      "args": ["--extensionDevelopmentPath=${workspaceFolder}/extensions/uaios-core"],
      "outFiles": ["${workspaceFolder}/out/**/*.js"],
      "presentation": {
        "hidden": false,
        "group": "",
        "order": 1
      }
    },
    {
      "name": "Attach to Extension Host",
      "type": "node",
      "request": "attach",
      "port": 5870,
      "outFiles": ["${workspaceFolder}/out/**/*.js"]
    }
  ]
}
```

#### Task 6.3: Git Workflow Setup

```powershell
# Create a new branch for Week 1 work
git checkout -b week-1-setup

# Make your changes...

# Stage and commit
git add .
git commit -m "Week 1: UAIOS branding and setup"

# Push to YOUR fork (not Microsoft's)
git push origin week-1-setup
```

#### Task 6.4: Verify Remote URLs

```powershell
# Check remotes
git remote -v

# Should show:
# origin    https://github.com/YOUR_USERNAME/vscode.git (fetch)
# origin    https://github.com/YOUR_USERNAME/vscode.git (push)
# upstream  https://github.com/microsoft/vscode.git (fetch)  [optional]
```

If origin points to Microsoft, fix it:
```powershell
git remote set-url origin https://github.com/YOUR_USERNAME/vscode.git
```

### Verification Checkpoint
- [ ] `yarn watch` runs in one terminal
- [ ] VS Code launches from source in another
- [ ] Changes reflect after window reload
- [ ] Git branch created for Week 1
- [ ] Remote points to YOUR fork

---

## 📋 Week 1 Checklist Summary

### Documentation Deliverables
- [ ] `vscode-structure-notes.md` — Folder structure documentation
- [ ] List of Extension APIs with descriptions
- [ ] Understanding of contribution points documented

### Technical Deliverables
- [ ] VS Code compiles without errors
- [ ] VS Code runs from source
- [ ] Branding shows "UAIOS" in title bar
- [ ] `product.json` updated with UAIOS values
- [ ] Development workflow established (watch + run)

### Git Deliverables
- [ ] Branch `week-1-setup` created
- [ ] All changes committed
- [ ] Pushed to YOUR GitHub fork

### Demo Deliverables
- [ ] Screenshot of running UAIOS with custom title
- [ ] Can open VS Code and show it's your build
- [ ] Can explain folder structure to teacher

---

## 🚨 Common Issues & Solutions

| Issue | Solution |
|-------|----------|
| `yarn` command not found | `npm install -g yarn` |
| Node version error | Install Node.js 18+ from nodejs.org |
| Compile fails with memory error | Close other apps, or increase Node memory: `set NODE_OPTIONS=--max-old-space-size=8192` |
| VS Code won't launch | Run `yarn compile` first, then try again |
| Changes not appearing | Make sure `yarn watch` is running, then reload window (not restart) |
| Git push rejected | Check remote URL points to your fork, not Microsoft |
| Icons don't update | Full rebuild required: stop watch, `yarn compile`, restart |

---

## 📎 Resources

- **VS Code Extension API Docs:** https://code.visualstudio.com/api
- **VS Code Source Architecture:** https://github.com/microsoft/vscode/wiki/Source-Code-Organization  
- **How to Debug VS Code:** https://github.com/microsoft/vscode/wiki/How-to-Contribute
- **Electron Basics:** https://www.electronjs.org/docs/latest/

---

## ✅ End of Week 1

When you complete all checkpoints:
1. Push all changes to your fork
2. Take screenshots for teacher demo
3. Prepare to show running UAIOS
4. Move to Week 2: Building Extension Panels

**Next Week Preview:** Create UAIOS Chat Panel and Platform Browser sidebar panels.
