# Brain Layer

Stands up one head agent with persistent memory. No businesses attached — just the agent, its rules, and its vault.

## Run it

Copy `SETUP.md` into a fresh, empty folder of your own first — don't run this from inside the cloned template repo, since setup will create your personal `CLAUDE.md` and vault in the current working directory.

```bash
mkdir ~/my-agent && cp SETUP.md ~/my-agent/
cd ~/my-agent
claude
```
Then say: `Read SETUP.md and set this up for me.`

Or skip cloning entirely: paste the full contents of `SETUP.md` as your first message in a fresh Claude Code session started in an empty folder.

Claude will ask you a few questions (agent name, pronouns, tone, where you want the vault) and then create:

- `CLAUDE.md` — the boot config, loaded every session
- An Obsidian vault with `VAULT-INDEX.md`, `01 - Daily Notes/`, and `Active Priorities.md`
- Install instructions for Obsidian if you don't already have it

Once this is done, you can add the `business-layer` on top of it whenever you're ready.
