# agents-and-skills

Robert's personal Claude Code marketplace — a collection of skills and agents.

This repo is a **Claude Code plugin marketplace**. It ships one plugin,
`my-skills`, containing the skills listed below. To use these skills inside
Claude Code, you first add this repo as a marketplace, then install the plugin.

## Installation

### 1. Add the marketplace

In Claude Code, run:

```
/plugin marketplace add RobertGleison/agents-and-skills
```

You can also point at a local clone or a full Git URL:

```
/plugin marketplace add ~/Desktop/codebase/agents-and-skills
/plugin marketplace add https://github.com/RobertGleison/agents-and-skills.git
```

### 2. Install the plugin

```
/plugin install my-skills@agents-and-skills
```

Or browse interactively and install from the menu:

```
/plugin
```

### 3. Restart / reload

Restart Claude Code (or reload the window) so the new skills are registered.
After that, the skills become available to the `Skill` tool and are auto-invoked
when their description matches your task.

## Verifying the install

```
/plugin marketplace list   # should list "agents-and-skills"
/plugin                    # my-skills should show as installed
```

The skills then appear in the available-skills list as `my-skills:<skill-name>`.

## Updating

When this repo changes, refresh the marketplace and reinstall:

```
/plugin marketplace update agents-and-skills
```

## Included skills (`my-skills` plugin)

| Skill | Purpose |
|-------|---------|
| `commit_writter` | Create commits following project conventions. Triggers on any commit / git commit / save-changes task. |
| `refactor-module` | Transform monolithic Terraform configurations into reusable, maintainable modules following HashiCorp's module design principles. |
| `terraform-search-import` | Discover existing cloud resources via Terraform Search and bulk-import them into Terraform management. |
| `terraform-style-guide` | Generate Terraform HCL following HashiCorp's official style conventions and best practices. |

## Repo structure

```
.claude-plugin/
  marketplace.json          # marketplace definition (name, plugins)
plugins/
  my-skills/
    skills/
      commit_writter/
      refactor-terraform-module/
      terraform-search/
      terraform-style-guide/
```

## Manual install (without the marketplace)

To try a single skill without registering the marketplace, copy its folder into
your user skills directory and restart Claude Code:

```bash
cp -r plugins/my-skills/skills/terraform-style-guide ~/.claude/skills/
```
