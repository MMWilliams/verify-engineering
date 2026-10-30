# verify-engineering

A Claude Code skill that makes the agent prove its work: before changing behavior it writes a verification matrix (each requirement or risk mapped to a source, a runnable check and a pass criterion set independently of the code), runs those checks on the final state, and closes with Verified, Partially verified or Failed verification.

## Install

```sh
git clone https://github.com/MMWilliams/verify-engineering ~/.claude/skills/verify-engineering
```

Claude Code picks it up automatically; invoke with `/verify-engineering` or let it trigger on implementation, fix, refactor and readiness-review tasks.
