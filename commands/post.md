---
description: Create a new Kiipu post from the provided text through the local kiipu CLI.
allowed-tools: Bash
---

# Post Command

Use this command when the user explicitly invokes `/kiipu:post`.

Interpret `$ARGUMENTS` as the full post body.

The command must execute through the local `kiipu` CLI. That CLI uses `https://api.kiipu.com` by default unless the operator has explicitly set `KIIPU_API_URL` for development.

Execution rules:

1. If `$ARGUMENTS` is empty or only whitespace, do not run any command. Tell the user to provide the text they want to publish, for example `/kiipu:post Ship the beta today`.
2. Otherwise, run the local CLI to create the post:

```bash
kiipu post create "$ARGUMENTS"
```

3. Return the CLI result accurately. Do not claim success unless the command succeeds.
4. If the CLI reports missing authentication, tell the user to run `kiipu auth login`.
