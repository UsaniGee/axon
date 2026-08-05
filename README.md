# AXON

**Spec-driven development for high-performance software teams.**

AXON is an open-source plugin for AI coding agents and IDE assistants. It gives
an agent a disciplined lifecycle for turning product context into specs,
execution plans, implementation, inspection, and recovery.

AXON stands for **Atop eXecution Orchestration Network**. The name reflects the
core idea: software work should move like a well-routed signal through a living
engineering system, from intent to verified code.

AXON is maintained by **Atop Web Technologies**.

## Philosophy

Most coding-agent sessions lose context unless the user keeps restating it.
AXON treats context as a managed project artifact. The project keeps its own
product definition, technical stack, workflow rules, style guides, and active
work pathways under version control.

The lifecycle is:

```text
Context -> Spec -> Plan -> Immerse -> Inspect -> Recover
```

## Commands

AXON exposes namespace-grouped slash commands:

| Command | Purpose | Primary artifacts |
| --- | --- | --- |
| `/axon:axon-initialize` | Initialize project context and workflow standards. | `axon/product.md`, `axon/tech-stack.md`, `axon/workflow.md` |
| `/axon:axon-craft` | Craft a new pathway from a feature, bug, chore, or MVP idea. | `axon/pathways/<id>/spec.md`, `axon/pathways/<id>/plan.md` |
| `/axon:axon-immerse` | Enter an approved pathway and implement the plan. | Updates pathway status and plan tasks |
| `/axon:axon-investigate` | Investigate project progress across pathways. | Reads `axon/pathways.md` and pathway plans |
| `/axon:axon-inspect` | Review completed work against the spec, plan, and standards. | Reads specs, plans, code style guides, and git changes |
| `/axon:axon-revert` | Revert a pathway, phase, or task using git-aware recovery. | Reverts commits and synchronizes pathway state |

## Generated Project Artifacts

When initialized in a target project, AXON creates:

```text
axon/
  index.md
  product.md
  product-guidelines.md
  tech-stack.md
  workflow.md
  code_styleguides/
  pathways.md
  pathways/
    <pathway_id>/
      index.md
      spec.md
      plan.md
      metadata.json
```

## Installation

### Antigravity / Gemini-compatible agents

Install from GitHub:

```bash
agy plugins install https://github.com/atopwebtechnologies/axon
```

For local development, clone and link the plugin:

```bash
git clone https://github.com/atopwebtechnologies/axon.git
cd axon
mkdir -p ~/.gemini/config/plugins/
ln -sfn "$(pwd)" ~/.gemini/config/plugins/axon
```

For workspace-level isolation:

```bash
mkdir -p .agents/plugins/
ln -sfn /absolute/path/to/axon .agents/plugins/axon
```

### Claude Code

After this repository is available as a plugin marketplace source:

```bash
/plugin marketplace add atopwebtechnologies/axon
/plugin install axon
```

### Codex-compatible local plugin development

This repository includes `.codex-plugin/plugin.json` so it can be used as a
Codex-style local plugin package during development.

## Natural Language Triggers

You do not have to memorize commands. Agents can map natural language intent to
the relevant AXON protocol:

- "Initialize AXON for this project."
- "Craft a pathway for adding team invitations."
- "Immerse in the active pathway."
- "Investigate our AXON progress."
- "Inspect the completed pathway."
- "Revert the last completed task."

## Repository Structure

```text
skills/
  axon-initialize/
  axon-craft/
  axon-immerse/
  axon-investigate/
  axon-inspect/
  axon-revert/
rules/
  axon_antigravity.md
.claude-plugin/
.codex-plugin/
```

## Upstream

AXON is derived from the Apache-2.0 licensed
[`gemini-cli-extensions/conductor`](https://github.com/gemini-cli-extensions/conductor)
project. The AXON fork is deeply rebranded and will evolve independently under
Atop Web Technologies.

## License

Apache-2.0. See [LICENSE](LICENSE) and [NOTICE](NOTICE).
