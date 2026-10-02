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
      Job Template.md
  02 - {{BUSINESS_2_NAME}}/
    {{BUSINESS_2_NAME}}.md
    Jobs/
      README.md
      Job Template.md
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

## Completion protocol

If the head agent's `CLAUDE.md` loads the unlazy completion protocol, {{BUSINESS_N_AGENT}} follows it too: a gates ledger for substantial work, outside any git repo, with every gate proven before reporting done. A local session inherits it only when it starts in the head agent's folder or below it (see Step 5b of the business-layer template); a session started inside the vault does not. If {{BUSINESS_N_AGENT}} runs as a scheduled or cloud job that can't see local files, start its prompt with the PROTOCOL block from the business-layer template.

## Approval gate

{{BUSINESS_N_AGENT}} follows the head agent's business action approval gate (or, without a brain layer, this one): anything involving money (quotes, invoices, payments, ad spend) and anything that is new territory (first contact with a new person or lead, an untested approach) goes to the owner for review first. Routine actions may run on {{BUSINESS_N_AGENT}}'s judgment only in a category the owner has confirmed as proven. {{BUSINESS_N_AGENT}} never handles card numbers or other payment credentials; it flags payment problems early and the owner completes any purchase.

Proven categories (each added only when the owner confirms it, with the date):
- _None yet._

## Jobs

Recurring tasks for {{BUSINESS_N_AGENT}} live in `Jobs/`, one note per job, each started from `Jobs/Job Template.md`.

## Notes

_Nothing recorded yet._
```

**Each `Jobs/README.md`:**

```markdown
# Jobs — {{BUSINESS_N_NAME}}

One file per recurring job {{BUSINESS_N_AGENT}} is responsible for. Start each new job by copying `Job Template.md` and filling in every section. A job note is how {{BUSINESS_N_AGENT}} learns: corrections and working methods go into its Lessons section, so the next run starts from what was learned, not from scratch.
```

**Each `Jobs/Job Template.md`:**

```markdown
# [Job name]

**The job:** one or two sentences on what this job produces and why it matters to {{BUSINESS_N_NAME}}.

## Boot chain
Read these, in order, before running the job:
1. This note, end to end.
2. The business overview note, `{{BUSINESS_N_NAME}}.md`, for scope and the approval gate.
3. `Active Priorities.md` in the brain-layer vault, if there is one, to confirm nothing about this job changed.

## The procedure
1. [Step]
2. [Step]

## Schedule and watchdog
- Trigger: manual, or the schedule it runs on.
- Watchdog: what checks that each scheduled run actually succeeded, and what happens on failure. Required for anything scheduled.

## Quality bar
- [What "done right" looks like, concretely and checkably.]

## Approved outputs log
Every output the owner approves (a post, an email, a quote) is logged here verbatim, with its date, at the moment it is approved. Never edit a past entry.

## Lessons
Every correction, dated. When the first approach to a recurring step fails and another works, record the working method and the dead end to skip, so no later run pays for it twice. When the owner confirms this job as proven for running without per-item review, record that here too, with the date.
```

## Step 5 — Link into the brain layer, if one exists

If `{{VAULT_PATH}}` was provided in Step 1, open its `VAULT-INDEX.md` and update the `## Vault Structure` section to add a line pointing at the new `Businesses/` folder and `BUSINESSES-INDEX.md`, replacing the placeholder line left by the brain-layer setup if it's still there. Also add a short pronoun/naming note near the bottom of `VAULT-INDEX.md` (or wherever the brain layer's `CLAUDE.md` keeps its "Make it yours" section) listing each business agent's name and pronouns, the same way the brain layer records its own.

## Step 5b: Completion protocol for business agents

If the head agent's `CLAUDE.md` loads the unlazy completion protocol (brain-layer setup, startup step 4), every business agent follows the same protocol. Nothing extra is needed for agents that run as local Claude Code sessions inside the head agent's folder or a subfolder of it, because Claude Code loads `CLAUDE.md` files from the working directory and every parent directory.

Watch the folder a business agent starts in. The business folders created above live in the vault, which is usually a different folder from the head agent's (where its `CLAUDE.md` is). A session started inside the vault does not load the head agent's `CLAUDE.md`, so it would skip the protocol. Either start business agents from the head agent's folder, or put a `CLAUDE.md` in the folder they start in that carries the same startup step 4 line.

A scheduled or cloud agent (for example a Claude Code cloud routine) runs somewhere that can't see local files or installed skills. When you create one for a business, start its prompt with this block, unchanged:

```text
PROTOCOL (standing rule; applies before any other step):
1. Fetch the unlazy skill at its reviewed commit: `git init -q /tmp/unlazy && git -C /tmp/unlazy fetch -q --depth 1 https://github.com/Leonxlnx/unlazy 16671491f6679ad9378f52604d3bc2415b4120c7 && git -C /tmp/unlazy checkout -q FETCH_HEAD`. Read `/tmp/unlazy/SKILL.md` in full and follow it for this run.
2. Write this run's gates ledger at `/tmp/unlazy-run/GATES.md` (outside the repository; never commit it), with one gate per required outcome of the task below. Lint it with `node /tmp/unlazy/scripts/gate-lint.mjs`, run only CHECK commands you wrote yourself with `--approve`, and do not report done while any gate is unmet.
3. Never install unlazy's Stop hook.
4. If the fetch fails or Node.js isn't available, say so plainly in your final summary and still apply the same discipline by hand: list every required outcome, verify each one directly before reporting, and report anything unmet as unmet.

---
```

After adding it, read the agent's saved prompt back and confirm the block is at the top and the rest is unchanged. A scripted single-response call (one prompt in, JSON or text out, no tools) doesn't need the block; the protocol exempts it.

## Step 6 — Confirm

Tell the person what was created: the folder path, the list of businesses and their agents, that each business has an approval gate and a job template to copy for every recurring job, and that running this file again is the way to add another business later (it will ask fresh questions and add a new numbered folder without touching the existing ones).
