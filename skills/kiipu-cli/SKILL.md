---
name: kiipu-cli
description: Use when the user wants to manage Kiipu posts, authentication, local setup, or command help through the Kiipu CLI.
---

# Kiipu CLI

Use this skill when the user wants to manage Kiipu posts or CLI setup from Claude Code through the local `kiipu` CLI.

Primary cases:

- create, list, search, show, update, star, pin, delete, restore, or purge posts
- authenticate through browser login, no-browser login, a device name override, or an API key
- check auth status or log out
- run `kiipu doctor` to verify local setup and API reachability
- run `kiipu skills` to point the user to the separate Claude Code plugin package
- run `kiipu help`, `kiipu help post`, `kiipu help auth`, `kiipu help doctor`, or `kiipu help skills`
- explain the exact `kiipu` CLI command to use when the user asks for manual usage
- route explicit slash-command posting requests to `/kiipu:post` when the user wants the command form

Do not use this skill for:

- chat-context actions like deleting "the current post" without an explicit id
- website automation or API calls when the local CLI already covers the task

## Installation

```bash
npm install -g @kiipu/cli
```

## Required execution path

Execute the local Kiipu CLI instead of simulating results.

Post commands:

```bash
kiipu post list [--tag <tag>] [--sort <updatedAt|createdAt|title>] [--starred] [--deleted]
kiipu post search <query>
kiipu post search --query "<query>"
kiipu post show --id <postId>
kiipu post update --id <postId> --content "<text>" [--title "<title>"] [--visibility public|private] [--tags <a,b,c>]
kiipu post star --id <postId>
kiipu post pin --id <postId>
kiipu post create --content "<text>"
kiipu post create "<text>"
kiipu post delete --id "<postId>"
kiipu post restore --id "<postId>"
kiipu post purge --id "<postId>"
```

Authentication:

```bash
kiipu auth login
kiipu auth login --device-name "<name>"
kiipu auth login --no-browser
kiipu auth login --api-key <cpk_...>
kiipu auth status
kiipu auth logout
```

Diagnostics and discovery:

```bash
kiipu doctor
kiipu skills
```

Help:

```bash
kiipu help
kiipu help post
kiipu help auth
kiipu help doctor
kiipu help skills
```

## Execution rules

1. Run the CLI before claiming success.
2. Return the CLI result accurately instead of inventing status.
3. If the user wants command usage rather than execution, provide the exact command form or the most relevant `kiipu help ...` command.
4. If the user wants to create or update a post, pass their full requested post body through `--content` or the positional create argument.
5. If the user wants show, update, star, pin, delete, restore, or purge but did not provide an id, ask for the explicit post id.
6. If the user wants search but did not provide a query, ask for the explicit search text.
7. If authentication is missing, tell the user to run `kiipu auth login`.
8. Prefer `kiipu skills` when the user is asking where the Claude Code plugin or skill package lives.
9. Prefer the local CLI over direct HTTP calls so auth, logging, and environment selection stay consistent.
10. Keep host-specific runtime guidance out of Claude Code unless the user is explicitly working with that host.
11. If the user explicitly wants to use a slash command for posting, suggest `/kiipu:post <text>`.

## Examples

```bash
kiipu post list --sort updatedAt
kiipu post search "roadmap"
kiipu post show --id post_123
kiipu post update --id post_123 --content "Revised note" --visibility private --tags work,planning
kiipu post star --id post_123
kiipu post pin --id post_123
kiipu post create --content "Ship the beta today"
kiipu post create "Ship the beta today"
kiipu post delete --id post_123
kiipu post restore --id post_123
kiipu post purge --id post_123
kiipu auth login
kiipu auth login --device-name "MacBook Pro"
kiipu auth login --no-browser
kiipu auth login --api-key cpk_example
kiipu auth status
kiipu auth logout
kiipu doctor
kiipu skills
kiipu help
kiipu help post
```
