# Debate Skill

Debate is an agent skill for comparing competing approaches to a decision. Two subagents make opposing cases, challenge each other's assumptions, and explain what would make them change their minds. A third, independent subagent reviews the evidence and recommends an option.

Use it when two or more plausible approaches have meaningful trade-offs, such as choosing between architectures or deciding how to run a rollout. A quick factual lookup or a straightforward implementation can usually skip the debate.

## Install

Use an agent that can load a `SKILL.md` file and delegate to subagents with separate contexts. Copy [`SKILL.md`](SKILL.md) into a folder named `debate` under your agent’s skills directory. If that folder already contains a skill, review the existing file before replacing it.

| Host | Personal skill file | Invocation |
| --- | --- | --- |
| [Claude Code](https://code.claude.com/docs/en/skills) | `~/.claude/skills/debate/SKILL.md` | `/debate` |
| [Codex](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills) | `~/.agents/skills/debate/SKILL.md` | `$debate` |

For another host, use its documented skill directory and invocation method. If your host has no skill loader, ask it to follow `SKILL.md` directly. The full workflow still requires delegation.

## Use

Invoke the skill with a decision and the constraints that matter. For example:

> Use the debate skill. Should our nightly import keep running as one scheduled job, or should we move to a worker queue? Compare recovery from partial failures, operating cost, and the work needed to roll back. Inspect the current code and recommend an approach.

The coordinating agent prepares a neutral brief, then delegates six turns across three phases:

1. **Construct.** Each participant presents a distinct approach and its strongest evidence.
2. **Cross-examine.** Participants answer each other's questions and identify how their own approach could fail.
3. **Crystallize.** Participants weigh the decisive trade-offs and state what would overturn their recommendations.

The judge receives anonymized options and a summary of the evidence and disagreements. The resulting recommendation explains the decisive trade-offs, remaining uncertainties, and a practical test that could change the verdict. You can ask for the full six-turn transcript.

The standard workflow requires actual delegated subagents. If delegation is unavailable, the coordinating agent reports that limitation. The debate produces a recommendation and leaves implementation to a separately authorized task.

## Skill file

[`SKILL.md`](SKILL.md) contains the orchestration instructions, participant roles, and judge rubric. It is self-contained.
