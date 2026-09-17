# AI Ops Starter

A two-layer template for standing up a persistent AI operations setup with Claude Code:

1. **`brain-layer/`** — one head agent with a persistent memory (an Obsidian vault). This is your operations partner: an identity, a set of standing rules, and a memory system that survives across sessions. No businesses, no clients, nothing specific — just the core agent.
2. **`business-layer/`** — a generic, repeatable pattern for adding one or more businesses, each with its own dedicated agent that takes instructions and runs that business day to day. You name the businesses and the agents; the structure repeats for however many you need.

You can run either layer on its own, or run the brain layer first and then the business layer on top of it (the business layer will cross-link into the brain layer's vault if one exists).

## How to use this

Each layer folder contains a single `SETUP.md`. That file is written as a set of instructions *for Claude Code to follow*, not for you to read line by line. Two ways to run it:

**Option A — clone the repo**
```bash
git clone <this-repo-url>
cd ai-ops-starter/brain-layer
claude
```
Then tell Claude: `Read SETUP.md and set this up for me.`

**Option B — copy/paste, no clone**
Open `brain-layer/SETUP.md` on GitHub, copy the whole file, and paste it as your first message in a fresh Claude Code session started in an empty folder. Claude will ask you a handful of setup questions and scaffold everything from there.

Do the same for `business-layer/SETUP.md` when you're ready to add businesses (run it from inside, or pointed at, the vault folder the brain layer created, if you want them linked).

## What you end up with

- A boot config (`CLAUDE.md`) that loads every session and defines your agent's identity and non-negotiable rules.
- An Obsidian vault as long-term memory — daily notes, an index, active priorities.
- One folder per business, each with its own scope note and its own named agent, all indexed so the head agent (if present) knows they exist.

Nothing in here is business-specific or identity-specific until you answer the setup questions — that's the point. It's the same pattern, made generic and reusable.
