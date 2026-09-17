# SETUP: Business Layer Bootstrap

You are Claude Code. You have just been handed this file by a person who wants to add one or more businesses to their setup, each with its own dedicated agent that takes instructions and runs that business day to day. Your job right now is to run the setup, not to explain what this file is.

Follow these steps in order. Ask one question at a time and wait for the answer before moving to the next.

**Before anything else:** check whether the current working directory is a clone of the `ai-ops-starter` template repo (e.g. it contains a sibling `brain-layer/` folder, or `git remote -v` points at the template). If so, stop and tell the person: don't run setup from inside the template clone — copy this `SETUP.md` into their brain-layer agent's own folder (or a new empty folder, if running standalone) first, then run Claude Code from there. If a file called `SETUP.md` already exists in that destination folder (e.g. the brain-layer bootstrap that was already run there), copy this one in under a different name instead — such as `BUSINESS-SETUP.md` — so it doesn't silently overwrite the original.

## Step 1 — Check for an existing brain layer

Ask: "Have you already set up a brain-layer vault (a head agent with its own vault)? If so, what's the path to it?"

- If yes, record `{{VAULT_PATH}}` and confirm the folder exists and contains a `VAULT-INDEX.md` before continuing. If it doesn't exist, tell the person and ask them to fix the path rather than guessing.
- If no, this layer will run standalone: create a `Businesses/` folder in the current working directory instead of inside a vault, and skip anything below that references linking into `VAULT-INDEX.md`.

## Step 2 — Ask how many businesses

Ask: "How many businesses do you want to set up right now?" (They can always add more later by running this same file again.)

## Step 3 — For each business, ask

Repeat for each business, one question at a time:

1. "What's the name of business #{{N}}?"
2. "One line: what does {{business name}} do?"
3. "What do you want to name the agent that runs {{business name}}?"
4. "Pronouns for {{agent name}} — he/him, she/her, or they/them?"

Record each as a numbered entry: `{{BUSINESS_N_NAME}}`, `{{BUSINESS_N_DESC}}`, `{{BUSINESS_N_AGENT}}`, `{{BUSINESS_N_PRONOUNS}}`.

## Step 4 — Create the folder structure

Inside `{{VAULT_PATH}}` if one exists, otherwise inside the current working directory, create:

```
Businesses/
  BUSINESSES-INDEX.md
  01 - {{BUSINESS_1_NAME}}/
    {{BUSINESS_1_NAME}}.md
    Jobs/
      README.md
  02 - {{BUSINESS_2_NAME}}/
    {{BUSINESS_2_NAME}}.md
    Jobs/
      README.md
  ... one numbered folder per business ...
```

**`BUSINESSES-INDEX.md`:**

```markdown
# Businesses Index

| # | Business | Agent | Pronouns | Description |
|---|----------|-------|----------|-------------|
| 01 | {{BUSINESS_1_NAME}} | {{BUSINESS_1_AGENT}} | {{BUSINESS_1_PRONOUNS}} | {{BUSINESS_1_DESC}} |
| 02 | {{BUSINESS_2_NAME}} | {{BUSINESS_2_AGENT}} | {{BUSINESS_2_PRONOUNS}} | {{BUSINESS_2_DESC}} |

_Add a row here each time a new business is set up._
```

**Each `{{BUSINESS_N_NAME}}.md`:**

```markdown
# {{BUSINESS_N_NAME}}

{{BUSINESS_N_DESC}}

## Agent

This business is run day to day by **{{BUSINESS_N_AGENT}}** ({{BUSINESS_N_PRONOUNS}}). {{BUSINESS_N_AGENT}} takes instructions here and executes them within this business's scope only — not across other businesses.

## Jobs

Recurring tasks for {{BUSINESS_N_AGENT}} live in `Jobs/`. Add one note per recurring job describing what it does and how to run it.

## Notes

_Nothing recorded yet._
```

**Each `Jobs/README.md`:**

```markdown
# Jobs — {{BUSINESS_N_NAME}}

One file per recurring job {{BUSINESS_N_AGENT}} is responsible for. Each job file should describe: what triggers it, what {{BUSINESS_N_AGENT}} does step by step, and what "done" looks like.
```

## Step 5 — Link into the brain layer, if one exists

If `{{VAULT_PATH}}` was provided in Step 1, open its `VAULT-INDEX.md` and update the `## Vault Structure` section to add a line pointing at the new `Businesses/` folder and `BUSINESSES-INDEX.md`, replacing the placeholder line left by the brain-layer setup if it's still there. Also add a short pronoun/naming note near the bottom of `VAULT-INDEX.md` (or wherever the brain layer's `CLAUDE.md` keeps its "Make it yours" section) listing each business agent's name and pronouns, the same way the brain layer records its own.

## Step 6 — Confirm

Tell the person what was created: the folder path, the list of businesses and their agents, and that running this file again is the way to add another business later (it will ask fresh questions and add a new numbered folder without touching the existing ones).
