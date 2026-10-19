# Personal Agent Toolkit

Shared configuration for managing my global skills, plugins and tool integrations across **GitHub Copilot, Claude Code and Codex** using [APM](https://github.com/microsoft/apm).

Dependencies and target agents are defined in [`apm.yml`](./apm.yml).

## Packages

| Package | Purpose |
|---------|---------|
| [Ponytail](https://github.com/DietrichGebert/ponytail) | Agent workflows, skills and hooks |
| [Superpowers](https://github.com/obra/superpowers) | Development workflow skills: brainstorming, planning, TDD, debugging and code review |
| [Skill Creator](https://github.com/thomast1906/github-copilot-agent-skills/tree/main/.github/skills/skill-creator) | Create, update and validate agent skills (`SKILL.md`) |

Support varies by agent and installation scope. APM reports compatibility limitations during installation.

## Prerequisites

Install Git, your chosen agent tools and APM.

On macOS:

```bash
brew install apm
```

For other platforms, see the [APM installation guide](https://microsoft.github.io/apm/getting-started/installation/).

## Install globally

From this folder, copy the manifest into APM’s user configuration directory:

```bash
mkdir -p ~/.apm
cp -i ./apm.yml ~/.apm/apm.yml
apm install --global
```

If a global manifest already exists, merge any dependencies you want to keep before replacing it.

Global installation makes supported components available across projects. Running `apm install` without `--global` configures only the current project.

After changing this repository’s `apm.yml`, synchronise and install:

```bash
cp -i ./apm.yml ~/.apm/apm.yml
apm install --global
```

## Update

To update all dependencies in your global APM setup:

```bash
apm update --global
```

This checks every repo listed in `~/.apm/apm.yml`, shows the changes and updates the installed components across your configured agents.

Upgrade the APM CLI separately:

```bash
brew update
brew upgrade apm
```

APM records resolved dependency revisions in `~/.apm/apm.lock.yaml`. Review upstream changes before updating, particularly packages containing executable hooks.

## Known issue: Azure Skills

[Azure Skills](https://github.com/microsoft/azure-skills) is not currently included in `apm.yml` because Azure integration can fail with:

```text
Object of type mappingproxy is not JSON serializable
```

This is tracked in [APM issue #3167](https://github.com/microsoft/apm/issues/3167).

Until the APM issue is resolved, use Azure’s native plugin installation. If you add `microsoft/azure-skills` to the manifest and hit this error, remove it and rerun `apm install --global`.

If APM reports that no transaction changes were committed, the installation did not complete—even if earlier messages say components were integrated.
