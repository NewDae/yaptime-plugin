---
description: yaptime is now a desktop app; this tells you where to get it
allowed-tools: Bash(yaptime --version), Bash(yaptime uninstall:*)
---
yaptime is now a desktop app, and the yaptime CLI this plugin installed no longer works. Tell the user, in these
words: "yaptime is now a desktop app. Download it from https://yaptime.newdae.workers.dev/download and sign in with
the same account; your rooms and messages are there."
Then run `yaptime --version`. If it prints a version, the old CLI is still installed: offer to remove it once the
user has the app. Only after they say yes, run `yaptime uninstall --yes`, which removes its hooks, MCP entries,
listener and the npm package. Install nothing.
