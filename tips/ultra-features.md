# Claude Code's "ultra" features, compared

Four different features share the "ultra" name or a close cousin of it. Here's what each one actually does.

| Feature | What it does | How to invoke | Requirements |
|---|---|---|---|
| `/code-review ultra` (`/ultrareview`) | Sends a branch diff or GitHub PR to a fleet of reviewer agents in a remote sandbox; every finding is independently reproduced before being reported | `/code-review ultra`, or `/ultrareview` where the alias is available | claude.ai sign-in; not available on Bedrock, Google Cloud Agent Platform, Microsoft Foundry, or Zero Data Retention orgs (falls back to local `/code-review`). Pro/Max get 3 free lifetime runs, then usage credits; Team/Enterprise go straight to usage credits |
| `/effort ultracode` | A session setting, not a model effort level: sends `xhigh` reasoning effort to the model **and** turns on automatic dynamic workflow orchestration for planning and executing tasks | `/effort ultracode`, `--effort ultracode`, `"ultracode": true` in settings, or `effortLevel: "ultracode"` in the Agent SDK | Model must support `xhigh` (Fable 5.1, Fable 5, Opus 5, Sonnet 5, Opus 4.8, Opus 4.7 — Opus 4.6 and Sonnet 4.6 top out at `max`); workflows must be enabled |
| `ultrathink` | Deeper reasoning for one turn only, no session setting changed | Include `ultrathink` anywhere in a prompt | None |
| `/ultraplan` | Retired. The command, its keyword trigger, and the plan-approval dialog option that launched it were all removed | Not available | Use Plan Mode or Claude Code on the web instead |

A few things worth calling out:

- **Ultracode isn't an inline keyword.** The persisted effort setting and the `CLAUDE_CODE_EFFORT_LEVEL` env var explicitly don't accept `ultracode` as a value you type into a prompt. If you want a one-turn boost without changing your session settings, that's `ultrathink`, not `ultracode`.
- **Ultrareview is a research preview**, so its name, pricing, and availability can change.
- **Don't confuse `/ultrareview` with Anthropic's separate "Code Review" GitHub App**, which auto-reviews PRs on push or open and posts inline comments. It's a distinct, Team/Enterprise-only product that happens to share review infrastructure and similar branding with `/ultrareview`.
- **`/ultraplan` is gone for good**, not renamed. There's no direct 1:1 replacement — Anthropic points people to Plan Mode for local planning or Claude Code on the web for cloud sessions.

References:
- [Ultrareview](https://code.claude.com/docs/en/ultrareview)
- [Code Review (GitHub App)](https://code.claude.com/docs/en/code-review)
- [Model configuration](https://code.claude.com/docs/en/model-config)
- [Ultraplan (removed)](https://code.claude.com/docs/en/ultraplan)
