# AXON

**Atop eXecution Orchestration Network**

AXON is an open-source plugin for AI coding agents and IDE assistants. It helps
teams plan and build predictable software applications by turning product
intent into durable project context, specs, execution plans, implementation
workflows, inspection, and recovery.

Architecture, design, build, test, and deploy workflows have changed
drastically. AI agents can now move fast enough to create real product surface
area in a single session, but speed without structure creates drift. AXON gives
that speed a protocol: context first, specification second, implementation
third, verification always.

AXON is maintained by **Atop Web Technologies**.

## Why AXON Exists

Prompt-only development is hard to repeat. The agent may understand the current
request, but forget the product direction, design constraints, stack decisions,
test expectations, or deployment workflow on the next task.

AXON stores those decisions inside the project:

- product definition
- product and UX guidelines
- technology stack
- workflow rules
- code style guides
- active work pathways
- specs and plans for each pathway

The result is a more predictable way to plan and build software applications:

```text
Context -> Craft -> Immerse -> Investigate -> Inspect -> Revert
```

## Commands

AXON exposes slash commands through supported coding agents and IDEs.

| Command | Purpose | Example |
| --- | --- | --- |
| `/axon:axon-initialize` | Initialize project context and workflow standards. | `/axon:axon-initialize` |
| `/axon:axon-craft` | Craft a new pathway from a feature, bug, chore, or MVP idea. | `/axon:axon-craft "Add team invitations with email links."` |
| `/axon:axon-immerse` | Enter an approved pathway and implement the plan. | `/axon:axon-immerse` |
| `/axon:axon-investigate` | Investigate project progress across pathways. | `/axon:axon-investigate` |
| `/axon:axon-inspect` | Inspect completed work against the spec, plan, and standards. | `/axon:axon-inspect` |
| `/axon:axon-revert` | Revert a pathway, phase, or task using git-aware recovery. | `/axon:axon-revert pathway team-invites` |

Generated artifacts live in the target project:

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

### Codex

AXON includes a Codex-compatible plugin manifest at
`.codex-plugin/plugin.json`.

Install AXON from GitHub as a Codex plugin marketplace:

```bash
codex plugin marketplace add atopwebtechnologies/axon --ref main
codex plugin add axon@axon
```

For local development, clone the repo and add the local checkout as a
marketplace:

```bash
git clone https://github.com/atopwebtechnologies/axon.git
cd axon
codex plugin marketplace add "$(pwd)"
codex plugin add axon@axon
```

Once AXON is active, start in the target project with:

```text
/axon:axon-initialize
```

### Quick Local Link

For workspace-level testing in compatible agents:

```bash
mkdir -p .agents/plugins/
ln -sfn /absolute/path/to/axon .agents/plugins/axon
```

## Tutorial: Greenfield Build

This example creates a small web application from scratch: a picker wheel that
spins and selects a random option.

### 1. Create the Project

```bash
mkdir picker-wheel
cd picker-wheel
```

Start your coding agent or IDE from this directory. If asked whether you trust
the folder, choose to trust it.

### 2. Initialize AXON

```text
/axon:axon-initialize
```

Follow the prompts. A simple set of answers might be:

```text
Product goal: A web app with a configurable spinning wheel.
Audience: General public.
Interaction: Click or tap to spin.
Customization: Basic editable options.
Platform: Desktop-first, responsive enough for mobile.
Product guidelines: Autogenerate.
Language: TypeScript.
Frontend: Vue.
Backend: None for the first version.
Database: None.
Workflow: Standard.
```

AXON creates the project context in `axon/`.

### 3. Craft the First Pathway

```text
/axon:axon-craft "Build the initial picker wheel application."
```

AXON will create:

```text
axon/pathways/<pathway_id>/index.md
axon/pathways/<pathway_id>/spec.md
axon/pathways/<pathway_id>/plan.md
axon/pathways/<pathway_id>/metadata.json
```

Read the generated `spec.md` and `plan.md`. Approve the plan when it matches
the application you want.

### 4. Immerse and Build

```text
/axon:axon-immerse
```

AXON works through the plan, updates task status, runs the project checks, and
asks for manual verification when needed. For a frontend app, that may include
starting the dev server, opening the local URL, spinning the wheel, editing the
options, and confirming the winner display.

### 5. Investigate or Inspect

Check progress:

```text
/axon:axon-investigate
```

Inspect completed work:

```text
/axon:axon-inspect
```

## Tutorial: Brownfield Iteration

This example improves an existing picker wheel so signed-in users can save and
restore their wheel configurations.

Start from an existing app, then open a new coding-agent session from the app
root.

### 1. Initialize or Reuse AXON Context

If the project has never used AXON:

```text
/axon:axon-initialize
```

For a brownfield project, AXON analyzes the existing codebase before drafting
product, stack, and workflow context.

### 2. Craft a Personalization Pathway

```text
/axon:axon-craft "Allow users to log in and save their picker wheel configurations."
```

Example pathway decisions:

```text
Authentication: Firebase Auth.
Saved data: Wheel options and visual settings.
Storage: Firestore.
Login UI: Modal overlay.
Restore behavior: Load the user's most recent saved wheel.
```

AXON writes a new pathway under `axon/pathways/<pathway_id>/`.

### 3. Review the Plan

Before implementation, read:

```text
axon/pathways/<pathway_id>/index.md
axon/pathways/<pathway_id>/spec.md
axon/pathways/<pathway_id>/plan.md
```

The plan should describe the data model, auth flow, UI changes, tests, and
manual verification steps.

### 4. Immerse

```text
/axon:axon-immerse
```

AXON implements the approved pathway and keeps the plan synchronized as work
progresses.

### 5. Verify

Reload the application and confirm:

```text
Users can sign in.
Users can save a wheel configuration.
Users can reload and restore saved options.
Signed-out users still get a usable picker wheel.
```

Tip: if your dev server or test runner enters watch mode, update
`axon/workflow.md` with the exact non-watch command. For example, many projects
need `CI=true npm test` or a test command with watch mode disabled.

## Natural Language Triggers

You do not have to memorize commands. Agents can map natural language intent to
the relevant AXON protocol:

- "Initialize AXON for this project."
- "Craft a pathway for adding team invitations."
- "Immerse in the active pathway."
- "Investigate AXON progress."
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

## Other Agent Setups

### Antigravity / Gemini-compatible agents

```bash
agy plugins install https://github.com/atopwebtechnologies/axon
```

For local development:

```bash
git clone https://github.com/atopwebtechnologies/axon.git
cd axon
mkdir -p ~/.gemini/config/plugins/
ln -sfn "$(pwd)" ~/.gemini/config/plugins/axon
```

### Claude Code

```text
/plugin marketplace add atopwebtechnologies/axon
/plugin install axon
```

## Acknowledgements

AXON began with inspiration from the Apache-2.0 licensed
[`gemini-cli-extensions/conductor`](https://github.com/gemini-cli-extensions/conductor)
project. We are grateful for that groundwork. AXON is now an Atop Web
Technologies project with its own language, roadmap, and direction.

## License

Apache-2.0. See [LICENSE](LICENSE) and [NOTICE](NOTICE).
