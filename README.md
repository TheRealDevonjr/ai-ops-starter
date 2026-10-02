# AI Ops Starter

A two-layer template for standing up a persistent AI operations setup with Claude Code:

1. **`brain-layer/`** — one head agent with a persistent memory (an Obsidian vault). This is your operations partner: an identity, a set of standing rules, and a memory system that survives across sessions. No businesses, no clients, nothing specific — just the core agent.
2. **`business-layer/`** — a generic, repeatable pattern for adding one or more businesses, each with its own dedicated agent that takes instructions and runs that business day to day. You name the businesses and the agents; the structure repeats for however many you need.

You can run either layer on its own, or run the brain layer first and then the business layer on top of it (the business layer will cross-link into the brain layer's vault if one exists).

## Before you start

You need three things installed. Each command below is the official one; run the version for your system.

1. **Claude Code**, which needs a paid Claude plan (Pro, Max, Team, Enterprise, or a Console account; the free plan doesn't include it).
   - macOS or Linux, in Terminal:
     ```bash
     curl -fsSL https://claude.ai/install.sh | bash
     ```
   - Windows, in PowerShell:
     ```powershell
     irm https://claude.ai/install.ps1 | iex
     ```
   Then open a new terminal window and run `claude --version`; it should print a version number. The first time you run `claude`, it opens your browser to log in. Full details: https://code.claude.com/docs/en/setup
2. **Git**, to clone this repo (and for the optional completion protocol). macOS asks to install it the first time you run `git`; on Windows, install [Git for Windows](https://git-scm.com/downloads/win), which also lets Claude Code use Git Bash.
3. **Obsidian** (free, https://obsidian.md), to read and edit the vault. Optional, but recommended.

## How to use this

Each layer folder contains a single `SETUP.md`. That file is written as a set of instructions *for Claude Code to follow*, not for you to read line by line. Two ways to run it:

**Option A — clone the repo**

macOS or Linux (Terminal):
```bash
git clone <this-repo-url>
mkdir ~/my-agent && cp ai-ops-starter/brain-layer/SETUP.md ~/my-agent/
cd ~/my-agent
claude
```

Windows (PowerShell):
```powershell
git clone <this-repo-url>
New-Item -ItemType Directory -Force "$HOME\my-agent" | Out-Null
Copy-Item "ai-ops-starter\brain-layer\SETUP.md" "$HOME\my-agent\"
Set-Location "$HOME\my-agent"
claude
```
Replace `<this-repo-url>` with the address from the green **Code** button on this repo's GitHub page. Then tell Claude: `Read SETUP.md and set this up for me.`

Copy `SETUP.md` into a fresh folder of your own first — don't run Claude Code directly inside the cloned template repo. Setup creates your personal `CLAUDE.md` and vault in the current working directory, and those shouldn't end up mixed into the shared template repo.

**Option B — copy/paste, no clone**
Open `brain-layer/SETUP.md` on GitHub, copy the whole file, and paste it as your first message in a fresh Claude Code session started in an empty folder. Claude will ask you a handful of setup questions and scaffold everything from there.

Do the same for `business-layer/SETUP.md` when you're ready to add businesses (run it from inside, or pointed at, the vault folder the brain layer created, if you want them linked). If you're copying both layers' files into the same folder, give the second one a different filename (e.g. `BUSINESS-SETUP.md`; the business-layer README shows the command for both systems). Both layers ship a file called `SETUP.md`, and copying the second on top of the first silently overwrites it.

## Daily use

Setup gives you two folders, and each one is opened differently:

- **The agent folder** (`my-agent` in the examples above) holds `CLAUDE.md`, the boot file that makes every session start as your agent. You open it in a **terminal** and start Claude Code there.
- **The vault** (wherever you chose during setup) is the agent's memory. You open it in **Obsidian**. The agent reads and writes it on its own during sessions, so you never need to open the vault in a terminal.

Each time you want to work with your agent:

macOS or Linux:
1. Open Terminal. On a Mac, press `Cmd + Space`, type `Terminal`, and press `Enter`.
2. Go to the agent folder and start Claude Code:
   ```bash
   cd ~/my-agent
   claude
   ```

Windows:
1. Open PowerShell: press the `Windows` key, type `PowerShell`, and press `Enter`.
2. Go to the agent folder and start Claude Code:
   ```powershell
   Set-Location "$HOME\my-agent"
   claude
   ```

To pick up your most recent conversation instead of starting fresh, run `claude --continue` instead of `claude`. To end a session, type `/exit`. If the `~` key is awkward on your keyboard, `cd "$HOME/my-agent"` does the same thing on macOS and Linux.

## What you end up with

- A boot config (`CLAUDE.md`) that loads every session and defines your agent's identity and non-negotiable rules.
- An Obsidian vault as long-term memory — daily notes, an index, active priorities.
- One folder per business, each with its own scope note and its own named agent, all indexed so the head agent (if present) knows they exist.
- Operating rules proven in daily use: an approval gate (money and new territory always go to you first; routine work runs on its own only once you declare it proven; agents never handle payment details), a watchdog for every scheduled job, a full reread of every changed file after each commit, a job-note template whose Lessons section is how each agent improves over time, and a daily note template built for picking up where the last session left off.
- Optional: a completion protocol every agent follows. The brain-layer setup offers to install the open-source [unlazy](https://github.com/Leonxlnx/unlazy) skill (MIT license, by Leon Lin), pinned to a reviewed commit. For substantial work, agents write a checklist of verifiable outcomes first and prove each one before reporting done. Quick edits and simple answers are exempt, and its optional Stop hook is left off by default. The business-layer setup carries the same protocol to each business agent, including a ready-made prompt block for scheduled or cloud agents.

Nothing in here is business-specific or identity-specific until you answer the setup questions — that's the point. It's the same pattern, made generic and reusable.
