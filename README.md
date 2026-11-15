# Debate Skill for Codex

`$debate` helps Codex compare competing approaches to a decision. Two subagents make opposing cases, challenge each other's assumptions, and explain what would make them change their minds. A third, independent subagent reviews the evidence and recommends an option.

Use it when two or more plausible approaches have meaningful trade-offs, such as choosing between architectures or deciding how to run a rollout. A quick factual lookup or a straightforward implementation can usually skip the debate.

## Install

You need a Codex environment with subagent delegation enabled and Git for the commands below. If you already have a `debate` skill, review it before replacing it.

To install the skill for your user account:

```sh
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/kangzheng97/codex-debate-skill.git "$HOME/.agents/skills/debate"
```

To share it with a project, copy [`SKILL.md`](SKILL.md) to `.agents/skills/debate/SKILL.md` in that project and commit it. See the [Codex skill discovery documentation](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills) for supported locations.

## Use

Start a Codex chat and invoke `$debate` with a decision and the constraints that matter. For example:

> $debate Should our nightly import keep running as one scheduled job, or should we move to a worker queue? Compare recovery from partial failures, operating cost, and the work needed to roll back. Inspect the current code and recommend an approach.

Codex prepares a neutral brief, then delegates six turns across three phases:

1. **Construct.** Each participant presents a distinct approach and its strongest evidence.
2. **Cross-examine.** Participants answer each other's questions and identify how their own approach could fail.
3. **Crystallize.** Participants weigh the decisive trade-offs and state what would overturn their recommendations.

The judge receives anonymized options and a summary of the evidence and disagreements. The resulting recommendation explains the decisive trade-offs, remaining uncertainties, and a practical test that could change the verdict. You can ask for the full six-turn transcript.

The standard workflow requires actual delegated subagents. If delegation is unavailable, Codex reports that limitation. The debate produces a recommendation and leaves implementation to a separately authorized task.

## Skill file

[`SKILL.md`](SKILL.md) contains the orchestration instructions, participant roles, and judge rubric. It is self-contained.
