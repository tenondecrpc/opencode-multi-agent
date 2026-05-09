# opencode-config

Personal configuration for [OpenCode](https://opencode.ai) CLI — a multi-agent setup for full-stack and AWS engineering work.

## Overview

`opencode.json` defines a primary orchestration agent backed by eleven specialist subagents. The primary agent classifies each task by domain and delegates to the appropriate specialist before implementing anything.

## Agent Roster

| Agent | Role | Model |
|---|---|---|
| **build** (primary) | Orchestrates full-stack and AWS tasks | qwen3.6-plus |
| **plan** (primary) | Decomposition, risk analysis, pre-implementation review | qwen3.6-plus |
| **general** | Summaries, synthesis, medium-complexity side tasks | qwen3.6-plus |
| **explore** | Read-only repo search, dependency tracing, convention lookup | qwen3.6-plus |
| **vision** | Screenshot analysis, visual QA, UI inspection | kimi-k2.6 |
| **frontend** | React, Next.js, CSS, accessibility, components | kimi-k2.6 |
| **backend** | APIs, services, data models, auth flows, business logic | deepseek-v4-pro |
| **cloud** | AWS, CDK, Terraform, Docker, CI/CD, networking | glm-5.1 |
| **security** | Secrets, IAM, auth, encryption, dependency risk | glm-5.1 |
| **architect** | Module boundaries, data flow, layering, tradeoffs | glm-5.1 |
| **qa** | Regression analysis, edge cases, test strategy, release risk | minimax-m2.7 |
| **refiner** | Small refactors, naming, formatting, cleanup | minimax-m2.7 |
| **documenter** | Setup notes, API refs, runbooks, changelogs | mimo-v2.5-pro |

## Design Principles

- **Specialist-first delegation** — the primary agent must use a domain specialist when one exists; falling back to `general` for a covered domain is not allowed.
- **Read before write** — `plan`, `explore`, `architect`, `qa`, and `security` agents are read-only by default.
- **Conservative cloud changes** — destructive cloud commands (`cdk deploy`, `terraform apply/destroy`, `cdk destroy`) are denied; mutations require confirmation.
- **Minimal changes** — all agents prefer targeted edits over speculative rewrites.

## Usage

Place `opencode.json` at the root of a project (or your home config directory) and run OpenCode normally. The build agent picks up the configuration automatically.

```sh
opencode
```

To use only planning mode:

```sh
opencode --agent plan
```

## File

```
opencode.json   # Full agent configuration with models, prompts, and permissions
```
