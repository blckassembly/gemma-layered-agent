# Layered Task System — a thesis-first Gemma 4 coding agent

**Understand the repository and tool limits, plan the fix, then verify
and submit the patch.**

An offline software-engineering agent built on one conviction: most
failed patches are failed *investigations*. The agent therefore spends
its structure on knowing before editing — and its token budget follows
the same rule, which is why the design doubles as a fewest-tokens
architecture.

## The workflow

| Stage | Name | What happens |
|---|---|---|
| 0 | Task Intake | Issue description + frozen repository snapshot |
| 1 | Gemma 4 Agent | Model guided by this bundle's configuration |
| 2 | Investigate | Read files, search code, understand the issue — no edits |
| 2.5 | Repository Thesis | Project/stack, module map, dependencies, tests, evidence and unknowns — grounded in this task's repo |
| 3.1 | Access + Capability Check | GATE: accessible files, harness tools, offline limits confirmed before any edit |
| 3.5 | Pre-Edit Plan | Expected behavior restated, testable hypothesis, target files and checks chosen |
| 3 | Change and Check | Edit → run sandbox checks → inspect → revise, iterating; new evidence updates the thesis |
| 4 | Submit Patch | Code changes submitted as a unified diff |
| 5 | Evaluation | Hidden task tests: PASS / FAIL — a FAIL updates the thesis evidence |

## Bundle layout

```
agent.yaml                  root config: stages, gates, limits
configs/sampling.yaml       deterministic, low-temperature sampling
prompts/system.md           the staged workflow, as the system prompt
prompts/analyzer.md         the Repository Thesis prompt
sub_agents/code_analyzer.yaml   read-only investigator (owns stages 2–2.5)
skills/repo_navigation/     token-efficient navigation procedure
adapters/                   LoRA adapter slots (main_lora, tool_lora)
```

## Why this shape wins tokens
- **Thesis before edits** — wrong edits are the most expensive tokens
  an agent can spend; the thesis is the receipt that prevents them.
- **A read-only analyzer** — investigation can't be contaminated by a
  fix already in progress, so evidence stays honest.
- **Gates, not vibes** — access/capability and the pre-edit plan are
  hard gates in config, not suggestions in prose.
- **Narrow checks first** — the loop runs the tests covering the change
  before anything broad.

## Status
v0.1 scaffold: workflow, prompts, sub-agent, skill, and sampling are
written and internally consistent. The LoRA adapters are placeholders —
post-training is the next build step, followed by scored practice runs
against the public task set. No benchmark numbers are claimed here;
the design states what would falsify it: if thesis-first agents do not
beat edit-first agents on pass rate or tokens-per-pass, the layering
is overhead, not leverage.
