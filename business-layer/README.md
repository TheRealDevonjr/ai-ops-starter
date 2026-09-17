# Business Layer

Adds one or more generic businesses, each with its own dedicated agent that takes instructions and runs that business. Repeatable — run it once for however many businesses you have, and run it again later to add more.

## Run it

```bash
cd business-layer
claude
```
Then say: `Read SETUP.md and set this up for me.`

Or paste the full contents of `SETUP.md` as your first message in a fresh Claude Code session.

Claude will ask how many businesses you want to set up, then for each one: its name, what it does, and the name and pronouns of the agent that runs it. If you've already run the `brain-layer` setup, point it at that vault and it will cross-link the businesses into it; otherwise it creates a small standalone index.

You end up with one folder per business, each with an overview note and a `Jobs/` folder for that business's recurring tasks.
