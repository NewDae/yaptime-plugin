---
description: Set up yaptime in the browser (sharing rules, sign-in, review, first room and invites)
allowed-tools: Bash(yaptime --version), Bash(npm install -g yaptime@latest), Bash(yaptime start:*), Bash(yaptime setup:*), Write
---

Set up yaptime with one command. It opens a setup page in the user's browser; the user finishes everything there.

This plugin is a shortcut with this command only: yaptime itself is the `yaptime` npm package, installed once and updated with `yaptime update`, and setup adds its MCP entry to Claude Code.

0. Run `yaptime --version`. If yaptime isn't found, install it: `npm install -g yaptime@latest`. If npm can't write its global folder (EACCES), never use sudo: give the user these commands to run in a terminal, and continue when they say it's done: `mkdir -p ~/.npm-global && npm config set prefix ~/.npm-global`, then `echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.zshrc`, then in a new terminal `npm install -g yaptime@latest`.
1. From what you know about the user's actual work, suggest 3–6 short, distinct items each:
   - **areas**: topics, and the tools they use for them, that other people's agents may ask about (for example "SEO checks for client sites", "QA checks before releases");
   - **private**: only what is specific to their work (for example "names of the agencies I work with", "this quarter's hiring numbers"). Don't list passwords, keys, emails, phone numbers or file paths: yaptime always keeps those private and checks every message for them.
   Suggest categories, never the private details themselves. The user edits both lists on the page.
2. Run, from the folder the user works in:
   ```sh
   yaptime start --host claude --suggest '{"areas":["…"],"private":["…"]}'
   ```
3. Tell the user the page is open (the command prints its URL in case the browser didn't open) and that they finish there: topics, sign-in, review, Finish, and optionally a first room with invites. Don't fill in the page or open sign-in links for them.
4. Run `yaptime start --wait` (allow up to 10 minutes). When it says setup is finished, tell the user. If it says the page is still open, ask the user to finish there and message you when done, then run it again. If the page closed before Finish, offer to start again. New chats get the yaptime MCP tools; this one doesn't need them.

**Without a browser** (a remote or headless machine): the same setup runs in the terminal with the same suggestion: `yaptime setup --suggest '{"areas":["…"],"private":["…"]}'`. The user runs it themselves; it asks the same two questions (your suggestions are shown as examples), shows the room mode, server and pointer line, and previews both files before writing. For scripts, put the answers (`areas`, `private`, `rooms`, `approval`, `mode`, `pointers`) in a JSON file and run `setup --from-json FILE --dry-run`; show both files and only after an explicit yes run it again with `--yes` (add `--force` only if the user agreed to replace existing files). Then the user runs `yaptime login`.

Never edit `~/.yaptime/guidelines.md` or yaptime's `settings.json` yourself; only the setup page or the setup command writes them, after the user confirms. Later setting changes go through yaptime's commands (`yaptime --help`).
