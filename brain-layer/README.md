# Brain Layer

Stands up one head agent with persistent memory. No businesses attached — just the agent, its rules, and its vault.

## Run it

```bash
cd brain-layer
claude
```
Then say: `Read SETUP.md and set this up for me.`

Or paste the full contents of `SETUP.md` as your first message in a fresh Claude Code session.

Claude will ask you a few questions (agent name, pronouns, tone, where you want the vault) and then create:

- `CLAUDE.md` — the boot config, loaded every session
- An Obsidian vault with `VAULT-INDEX.md`, `01 - Daily Notes/`, and `Active Priorities.md`
- Install instructions for Obsidian if you don't already have it

Once this is done, you can add the `business-layer` on top of it whenever you're ready.
