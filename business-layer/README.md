# Business Layer

Adds one or more generic businesses, each with its own dedicated agent that takes instructions and runs that business. Repeatable — run it once for however many businesses you have, and run it again later to add more.

## Run it

If you already ran the `brain-layer` setup, run this from inside that agent's own folder (not from inside the cloned template repo) so it can find and link into the existing vault. If running standalone, copy `SETUP.md` into a fresh, empty folder of your own first.

**Copy it under a different name if a `SETUP.md` already exists there** (e.g. from the brain-layer setup) — otherwise the copy silently overwrites it:

```bash
cp SETUP.md ~/my-agent/BUSINESS-SETUP.md   # or wherever your brain-layer folder is
cd ~/my-agent
claude
```
Then say: `Read BUSINESS-SETUP.md and set this up for me.`

Or skip cloning entirely: paste the full contents of `SETUP.md` as your first message in a fresh Claude Code session.

Claude will ask how many businesses you want to set up, then for each one: its name, what it does, and the name and pronouns of the agent that runs it. If you've already run the `brain-layer` setup, point it at that vault and it will cross-link the businesses into it; otherwise it creates a small standalone index.

You end up with one folder per business, each with an overview note and a `Jobs/` folder for that business's recurring tasks.
