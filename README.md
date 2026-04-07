# Kiipu Claude Code Plugin

Claude Code integration for Kiipu workflows.

`@kiipu/claude-plugin` is the packaged Claude Code integration for Kiipu. Choose this package when you want the plugin-ready distribution instead of assembling the raw skill assets yourself.

It provides:

- a Kiipu skill for authenticated CLI usage
- a Kiipu namespaced command for quick posting
- the plugin metadata required by Claude Code

## Install

Install the Kiipu CLI first:

```bash
npm install -g @kiipu/cli
```

Then install the Claude Code plugin package:

```bash
npm install @kiipu/claude-plugin
```

## What It Includes

The published package contains:

```text
.claude-plugin/
  plugin.json
  marketplace.json
commands/
  post.md
skills/
  kiipu-cli/
    SKILL.md
README.md
LICENSE
```

## How It Works

The plugin connects Claude Code to the local `kiipu` CLI.

That means:

- Claude Code can trigger Kiipu actions through the local CLI
- authentication and posting happen through the installed `kiipu` command
- the plugin does not need to call Kiipu APIs directly

## Authentication

Before using the plugin, make sure the local CLI is authenticated:

```bash
kiipu auth login
```

You can verify local setup with:

```bash
kiipu auth status
kiipu doctor
```

## Typical Usage

Once the plugin is available in Claude Code, use the Kiipu skill or Kiipu command from your Claude workflow.

For example:

```text
/kiipu:post Ship the beta today
```

## Which Package To Choose

Choose `@kiipu/claude-plugin` when you want the packaged Claude Code integration.

Choose `@kiipu/skills` when you only want the standalone skill assets.

Choose `@kiipu/cli` when you only want the executable command line tool.

## Related Packages

- `@kiipu/cli` is the executable CLI used for real Kiipu actions
- `@kiipu/skills` contains the standalone skill assets
- `@kiipu/claude-plugin` packages those assets for Claude Code
