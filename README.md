# Claude Code Tips

Collection of my favorite Claude Code tips as I explore it.

![](images/img.png)

## Table of Contents

### General
- [Tip 1: Name and resume sessions like git branches](#tip-1-name-and-resume-sessions-like-git-branches)
- [Tip 2: Match your effort level to the task](#tip-2-match-your-effort-level-to-the-task)
- [Tip 3: Skip local file discovery for scripted runs](#tip-3-skip-local-file-discovery-for-scripted-runs)
- [Tip 4: Turn on Explanatory or Learning mode to study a codebase](#tip-4-turn-on-explanatory-or-learning-mode-to-study-a-codebase)
- [Tip 5: Move sessions between your laptop, phone, and the cloud](#tip-5-move-sessions-between-your-laptop-phone-and-the-cloud)
- [Tip 6: Turn a recurring task into a loop or a scheduled job](#tip-6-turn-a-recurring-task-into-a-loop-or-a-scheduled-job)
- [Tip 7: Understand what auto mode is actually deciding for you](#tip-7-understand-what-auto-mode-is-actually-deciding-for-you)

### Command
- [Tip 1: Give Claude a standing goal for the whole session](#tip-1-give-claude-a-standing-goal-for-the-whole-session)
- [Tip 2: Let /batch run a migration across hundreds of files](#tip-2-let-batch-run-a-migration-across-hundreds-of-files)
- [Tip 3: Run parallel sessions in isolated worktrees](#tip-3-run-parallel-sessions-in-isolated-worktrees)
- [Tip 4: Pre-approve the commands you already trust](#tip-4-pre-approve-the-commands-you-already-trust)
- [Tip 5: Sandbox risky commands instead of prompting for each one](#tip-5-sandbox-risky-commands-instead-of-prompting-for-each-one)
- [Tip 6: Script Claude into CI and pre-commit hooks](#tip-6-script-claude-into-ci-and-pre-commit-hooks)

### Agent
- [Tip 1: Define reusable subagents instead of re-explaining a role every time](#tip-1-define-reusable-subagents-instead-of-re-explaining-a-role-every-time)
- [Tip 2: Delegate research to a subagent so it doesn't eat your context](#tip-2-delegate-research-to-a-subagent-so-it-doesnt-eat-your-context)
- [Tip 3: Have a fresh subagent grade the work before you call it done](#tip-3-have-a-fresh-subagent-grade-the-work-before-you-call-it-done)
- [Tip 4: Batch large changes across worktree-isolated agents](#tip-4-batch-large-changes-across-worktree-isolated-agents)
- [Tip 5: Reach for agent teams when work needs teammates, not just workers](#tip-5-reach-for-agent-teams-when-work-needs-teammates-not-just-workers)

### Skill
- [Tip 1: Ship skills your team can invoke but Claude won't guess at](#tip-1-ship-skills-your-team-can-invoke-but-claude-wont-guess-at)
- [Tip 2: Reach for another CLI when WebFetch hits a wall](#tip-2-reach-for-another-cli-when-webfetch-hits-a-wall)
- [Tip 3: Let a plugin enforce TDD and root-cause debugging discipline](#tip-3-let-a-plugin-enforce-tdd-and-root-cause-debugging-discipline)
- [Tip 4: Give Claude a real browser for pages WebFetch can't handle](#tip-4-give-claude-a-real-browser-for-pages-webfetch-cant-handle)
- [Tip 5: Browse skills.sh before writing one from scratch](#tip-5-browse-skillssh-before-writing-one-from-scratch)

### Mcp
- [Tip 1: Bundle MCP servers, skills, and hooks together as a plugin](#tip-1-bundle-mcp-servers-skills-and-hooks-together-as-a-plugin)
- [Tip 2: Tune how aggressively Claude loads your MCP tool definitions](#tip-2-tune-how-aggressively-claude-loads-your-mcp-tool-definitions)
- [Tip 3: Keep raw tool output out of your context with a sandboxed MCP server](#tip-3-keep-raw-tool-output-out-of-your-context-with-a-sandboxed-mcp-server)
- [Tip 4: Give Claude persistent memory across sessions with claude-mem](#tip-4-give-claude-persistent-memory-across-sessions-with-claude-mem)

### Prompt
- [Tip 1: Have Claude interview you before building something big](#tip-1-have-claude-interview-you-before-building-something-big)
- [Tip 2: Write the code in one session, review it in another](#tip-2-write-the-code-in-one-session-review-it-in-another)
- [Tip 3: Put your planning effort into plan mode, not into micromanaging](#tip-3-put-your-planning-effort-into-plan-mode-not-into-micromanaging)

### Hooks
- [Tip 1: Hook into specific moments in Claude's lifecycle](#tip-1-hook-into-specific-moments-in-claudes-lifecycle)
- [Tip 2: Auto-format on every edit with a PostToolUse hook](#tip-2-auto-format-on-every-edit-with-a-posttooluse-hook)
- [Tip 3: Use a Stop hook as a deterministic gate for unattended runs](#tip-3-use-a-stop-hook-as-a-deterministic-gate-for-unattended-runs)
- [Tip 4: Get worktree isolation on non-git version control](#tip-4-get-worktree-isolation-on-non-git-version-control)

### Workflow
- [Tip 1: Treat CLAUDE.md as a file that gets smarter, not a README](#tip-1-treat-claudemd-as-a-file-that-gets-smarter-not-a-readme)
- [Tip 2: Reserve "IMPORTANT" for the one rule Claude keeps missing](#tip-2-reserve-important-for-the-one-rule-claude-keeps-missing)
- [Tip 3: Let /doctor prune your CLAUDE.md for you](#tip-3-let-doctor-prune-your-claudemd-for-you)
- [Tip 4: Give Claude a way to check its own work](#tip-4-give-claude-a-way-to-check-its-own-work)
- [Tip 5: Run risky, unsupervised work in a container](#tip-5-run-risky-unsupervised-work-in-a-container)

## General

### Tip 1: Name and resume sessions like git branches

Claude Code saves every conversation locally, so a task that spans multiple sittings doesn't need re-explaining from scratch. Run `/rename` to give a session a descriptive name, the same way you'd name a branch. Use `claude --continue` to pick up your most recent session, or `claude --resume` to choose from a list of past ones. Treat each workstream as its own persistent context: one session per feature, not one giant thread for everything you touch this week. Descriptive names pay off weeks later, when you're trying to remember which session already has the context you need.

Example:
```
claude --resume
```
Then pick "oauth-migration" from the list to jump back into that work with full context intact.

Reference: [Manage sessions](https://code.claude.com/docs/en/sessions)

### Tip 2: Match your effort level to the task

Run `/effort` to control how hard Claude thinks before responding. Levels range from low (fewer tokens, faster) through medium, high, xhigh, max, and auto, where Claude picks per request. The default is high on Team, Enterprise, and direct API access, and medium everywhere else. Reach for xhigh on complex coding or agentic work when you want deeper reasoning without paying the full cost of max. Save max for the genuinely hard cases: a gnarly debugging session or an architecture decision where you want Claude to think for as long as it needs. Max burns through usage limits faster, so turn it on for the session that needs it rather than leaving it as your default.

Example:
```
/effort xhigh
Refactor the auth module to support multi-tenant sessions without breaking existing token validation.
```

Reference: [Power user tips](https://support.claude.com/en/articles/14554000-claude-code-power-user-tips)

### Tip 3: Skip local file discovery for scripted runs

By default, `claude -p` and the SDKs search your filesystem for CLAUDE.md files, settings, and MCP configs before every run. That's the right behavior interactively, but for scripted or CI usage you already know exactly what should load. Add `--bare` and pass `--system-prompt`, `--mcp-config`, and `--settings` explicitly instead, and startup gets roughly 10x faster. This local search was a default set early on, and the Claude Code team plans to flip it in a future version, so `--bare` is the flag worth reaching for today whenever you're calling Claude from a script.

Example:
```
claude -p "summarize this codebase" \
  --output-format=stream-json \
  --verbose \
  --bare
```

Reference: [Power user tips](https://support.claude.com/en/articles/14554000-claude-code-power-user-tips)

### Tip 4: Turn on Explanatory or Learning mode to study a codebase

Output styles change how Claude talks, not just what it does. Set one in `/config`. Explanatory mode has Claude narrate the frameworks and patterns behind its own changes as it works, which is useful when you're onboarding onto code you didn't write. Learning mode goes a step further and coaches you through the change instead of just making it for you. Combine either one with a direct ask: have Claude generate an HTML walkthrough of a tricky module, draw an ASCII diagram of a protocol, or quiz you on a file until your explanation lines up with its own.

Example:
```
/config
```
Set output style to Explanatory, then:
```
Walk me through how the request middleware pipeline works in @src/server/middleware, explaining the pattern as you go.
```

Reference: [Power user tips](https://support.claude.com/en/articles/14554000-claude-code-power-user-tips)

### Tip 5: Move sessions between your laptop, phone, and the cloud

A session doesn't have to stay on one machine. Run `/teleport` (or `claude --teleport`) to pull a cloud session down and keep working from your terminal. Run `/remote-control` to flip that around and drive a local session from your phone or a browser instead. The Claude mobile app has a dedicated Code tab for this, and an iMessage plugin lets you fire off tasks from any Apple device without opening the app at all. If you want this available everywhere by default, turn on "Enable Remote Control for all sessions" in `/config` instead of switching it on per session.

Reference: [Power user tips](https://support.claude.com/en/articles/14554000-claude-code-power-user-tips)

### Tip 6: Turn a recurring task into a loop or a scheduled job

`/loop` repeats a task locally on an interval for up to three days, which covers things like babysitting open PRs or closing out stale ones without you kicking it off by hand each time. `/schedule` does the same job but runs in the cloud, so it keeps going after you close your laptop. The strongest version of this pattern pairs a schedule with a skill: write the workflow once as a skill, then schedule it to run on its own.

Example:
```
/loop 5m /babysit
/loop 1h /pr-pruner
```
```
/schedule a daily job that looks at all PRs shipped since yesterday and updates our docs based on the changes. Use the Slack MCP to message #docs-update with the changes
```

Reference: [Power user tips](https://support.claude.com/en/articles/14554000-claude-code-power-user-tips)

### Tip 7: Understand what auto mode is actually deciding for you

On Pro, Max, and Team plans, auto mode is the default permission mode for interactive terminal and VS Code sessions. A separate classifier model reviews each action before it runs and approves the routine ones on its own, only stopping you for things like scope escalation, unfamiliar infrastructure, or an action that looks driven by hostile content Claude just read. You can switch modes at any point in a session with Shift+Tab if you'd rather approve everything by hand for a while. For scripted runs, pass the mode explicitly instead of relying on the interactive default, and know that a non-interactive run doesn't stop just because the classifier blocks a few actions in a row.

Example:
```
claude --permission-mode auto -p "fix all lint errors"
```

Reference: [Permission modes](https://code.claude.com/docs/en/permission-modes)

## Command

### Tip 1: Give Claude a standing goal for the whole session

`/goal` sets a condition that gets re-checked after every turn, not just once at the start. A separate evaluator watches for it, and Claude keeps working across turns until the condition actually resolves, instead of treating "done" as something it only claims once. If Claude genuinely can't get there, Claude Code eventually stops the run rather than looping forever, but the goal stays set so you can pick it back up later. This is the difference between asking Claude to fix something once and asking it to keep trying until the thing is actually fixed.

Example:
```
/goal all tests in the payments/ directory pass and `npm run typecheck` is clean
```

Reference: [/goal](https://code.claude.com/docs/en/goal)

### Tip 2: Let /batch run a migration across hundreds of files

`/batch` interviews you about a migration up front, then fans the work out across as many worktree agents as it needs, dozens or hundreds if the change calls for it. Each agent works in its own isolated worktree, tests its own changes, and opens its own PR. You answer a handful of questions once instead of babysitting a change that touches your whole codebase file by file.

Example:
```
/batch migrate src/ from JavaScript to TypeScript
```

Reference: [Power user tips](https://support.claude.com/en/articles/14554000-claude-code-power-user-tips)

### Tip 3: Run parallel sessions in isolated worktrees

The single biggest change most engineers can make to their workflow is running 3-5 Claude sessions at once, each in its own git worktree, so they can't step on each other's file edits. `claude --worktree` (or `claude --worktree my-feature`) starts a session in a fresh worktree, and adding `--tmux` gives it its own detachable terminal session too. If your version control isn't git (Mercurial, Perforce, SVN), define `WorktreeCreate` and `WorktreeRemove` hooks in settings.json to get the same isolation. Name your worktrees and set up shell aliases to jump between them, or you'll quickly lose track of which terminal is doing what.

Example:
```
claude --worktree auth-refactor --tmux
```

Reference: [Hooks](https://code.claude.com/docs/en/hooks)

### Tip 4: Pre-approve the commands you already trust

Instead of choosing between approving every single action or skipping permissions entirely, run `/permissions` to allowlist the commands you already trust, then check that list into `.claude/settings.json` for your whole team. It supports real wildcard syntax, so a rule like `"Bash(bun run *)"` or `"Edit(/docs/**)"` covers a whole category of actions at once. Everything you add is additive to the small set of safe commands Claude Code pre-approves out of the box, and the result is an auditable allowlist instead of a black box.

Example: `.claude/settings.json`
```json
{
  "permissions": {
    "allow": ["Bash(bun run *)", "Edit(/docs/**)"]
  }
}
```

Reference: [Power user tips](https://support.claude.com/en/articles/14554000-claude-code-power-user-tips)

### Tip 5: Sandbox risky commands instead of prompting for each one

`/sandbox` opts you into Claude Code's open source sandbox runtime, which isolates both the filesystem and the network on your own machine. You get three modes: sandboxed with auto-allow, sandboxed with regular permission prompts still on, or no sandbox at all. This cuts the number of prompts you see while actually improving safety, since a sandboxed command that goes wrong can't reach outside its box in the first place. It's worth turning on before you turn on auto mode, not instead of it, since the two solve different problems.

Reference: [Power user tips](https://support.claude.com/en/articles/14554000-claude-code-power-user-tips)

### Tip 6: Script Claude into CI and pre-commit hooks

`claude -p "prompt"` runs Claude non-interactively and still creates a resumable session unless you pass `--no-session-persistence`. Pick your output format based on what's downstream: plain text for a one-off query, `--output-format json` for a single object you can parse, or `--output-format stream-json` for one JSON event per line when you want to process output as it arrives. This is what turns Claude Code into something you wire into a pipeline rather than something you only run by hand.

Example:
```
claude -p "list all API endpoints" --output-format json
```

Reference: [Headless mode](https://code.claude.com/docs/en/headless)

## Agent

### Tip 1: Define reusable subagents instead of re-explaining a role every time

Drop a markdown file into `.claude/agents/` with a `name`, `description`, and optionally a restricted `tools` list, and you have a reusable subagent you can invoke with `claude --agent=<name>` or let Claude reach for on its own. A read-only agent scoped to just the Read tool is a common one to keep around for safe exploration of unfamiliar code. Boris Cherny keeps a small library of these for jobs he runs often, a code simplifier, a build checker, a test runner, each one starting from a clean context and returning just a result.

Example: `.claude/agents/ReadOnly.md`
```
---
name: ReadOnly
description: Read-only agent restricted to the Read tool only
tools: Read
---
You are a read-only agent that cannot edit files or run bash.
```

Reference: [Subagents](https://code.claude.com/docs/en/sub-agents)

### Tip 2: Delegate research to a subagent so it doesn't eat your context

Context is the real constraint in a long session, and exploration is usually the biggest cost against it. Tell Claude to use a subagent to investigate something, and that research happens in a separate context entirely, leaving your main conversation focused on implementation. This matters most on an unfamiliar codebase, where the alternative is burning through half your context window finding the right files before you've written a line of code.

Example:
```
Use a subagent to investigate how our existing rate limiter is implemented and where it's used, then summarize the findings before we touch anything.
```

Reference: [Subagents](https://code.claude.com/docs/en/sub-agents)

### Tip 3: Have a fresh subagent grade the work before you call it done

The longer a run goes unattended, the more it matters that something other than the agent that did the work checks it. Before treating a task as finished, have a subagent review the diff in a fresh context with only the diff and your criteria, not the reasoning that produced the change, so it isn't grading its own homework. Claude Code ships a `/code-review` skill that does exactly this: it reviews the current diff in a fresh subagent and reports findings back to your session.

Example:
```
/code-review
```
or write your own criteria:
```
Spin up a subagent with only the current diff and this checklist: no unhandled errors, no new dependencies, tests cover the new branch. Report gaps, don't fix them.
```

Reference: [Subagents](https://code.claude.com/docs/en/sub-agents)

### Tip 4: Batch large changes across worktree-isolated agents

Add `isolation: worktree` to a subagent's frontmatter and Claude Code runs that agent in its own git worktree automatically, which matters once you're launching many agents against the same repo at the same time. This is what makes a prompt like "migrate all sync IO to async, launch 10 parallel agents" safe to run: each agent tests its own change end to end and opens its own PR, without ten agents fighting over the same working directory.

Example: `.claude/agents/worktree-worker.md`
```
---
name: worktree-worker
model: haiku
isolation: worktree
---
```
Then prompt:
```
Migrate all sync IO to async. Batch the changes and launch 10 parallel agents with worktree isolation. Each agent should test its changes end to end, then put up a PR.
```

Reference: [Power user tips](https://support.claude.com/en/articles/14554000-claude-code-power-user-tips)

### Tip 5: Reach for agent teams when work needs teammates, not just workers

A subagent hands back one result and disappears. An agent team keeps every teammate alive as its own full Claude Code session, one that can message any other teammate directly and pull work off a task list the whole team shares. One session takes the lead, spawning teammates and handing out tasks, but you can talk to any teammate directly and redirect it yourself without going through the lead. That gives you real coordination a subagent can't: teammates compare notes, challenge each other's findings, or split ownership across a feature's frontend, backend, and tests. Reach for it when you're debugging with competing hypotheses, running a review that needs several angles at once, or splitting a feature cleanly enough to give each teammate their own slice. It's still experimental, gated behind `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`, and burns tokens fast since every teammate holds its own full context window, so start with 3-5 teammates and save it for work where the parallelism actually pays off. For anything sequential or single-file, delegating to a plain subagent (Tip 2) stays cheaper and simpler.

Example: `.claude/settings.json`
```json
{ "env": { "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1" } }
```
Then:
```
Spawn a team of 3 to review the auth module: one on token handling,
one on session management, one on input validation. Have them share
findings with each other before reporting back to me.
```

Reference: [Agent teams](https://code.claude.com/docs/en/agent-teams)

## Skill

### Tip 1: Ship skills your team can invoke but Claude won't guess at

A skill is a `SKILL.md` file under `.claude/skills/<name>/` with a `name` and `description`, and Claude applies it automatically when it looks relevant, or you can call it directly with `/skill-name`. Some skills shouldn't be auto-invoked, like an issue-fixer that takes an argument and touches multiple files on your say-so alone. Set `disable-model-invocation: true` in the frontmatter for those, and the skill only runs when someone explicitly asks for it by name.

Example: `.claude/skills/fix-issue/SKILL.md`
```
---
name: fix-issue
description: Fix a GitHub issue
disable-model-invocation: true
---
Analyze and fix the GitHub issue: $ARGUMENTS.
1. Use `gh issue view` to get the issue details
2. Search the codebase for relevant files
3. Implement the fix and write a test for it
```

Example:
```
/fix-issue 482
```

Reference: [Skills](https://code.claude.com/docs/en/skills)

### Tip 2: Reach for another CLI when WebFetch hits a wall

WebFetch can't reach every site, Reddit is a common example. Rather than giving up, write a skill that shells out to a different CLI with its own web access through a tmux session: start it, send the query, capture the output, parse the result. Package this as a skill instead of pasting the same instructions into CLAUDE.md, since a skill only loads into context when Claude actually needs it, while anything in CLAUDE.md loads into every single conversation whether that conversation needs it or not.

Example:
```
Check how Claude Code skills are being discussed on Reddit and summarize the sentiment.
```

Reference: [Skills](https://code.claude.com/docs/en/skills)

### Tip 3: Let a plugin enforce TDD and root-cause debugging discipline

Left alone, Claude tends to jump straight to code. The [Superpowers](https://claude.com/plugins/superpowers) plugin is a skill pack that pushes back on that: it forces red-green-refactor TDD, so a test has to fail before any implementation gets written, and it runs a four-phase debugging process that investigates the root cause instead of guessing at a fix. It also ships a brainstorming skill that questions your requirements before any code gets touched, and a review skill that hands the diff to a separate subagent instead of grading its own homework. These skills activate on their own once installed, so you don't have to invoke them by name, and every session inherits the same discipline instead of you re-explaining "write the test first" in every prompt.

Example:
```
/plugin install superpowers@claude-plugins-official
```
```
Add rate limiting to the public API.
```

Reference: [Discover and install plugins](https://code.claude.com/docs/en/discover-plugins)

### Tip 4: Give Claude a real browser for pages WebFetch can't handle

WebFetch reads static HTML, so it misses anything a page only renders after JavaScript runs, and it can't click a button, fill in a form, or step through a login. [agent-browser](https://github.com/vercel-labs/agent-browser) installs as a skill (`npx skills add vercel-labs/agent-browser`) and drives a real Chrome instance instead. Claude reads the page's accessibility tree and gets back stable references like `@e2` for each interactive element, then clicks, types, or screenshots against that reference instead of guessing a CSS selector that breaks the moment the layout shifts. Reach for this when you're testing your own app end to end, reading a page that only renders after JavaScript runs, or walking through a flow that needs a login. Keep WebFetch for the simple case: pulling text off a page that doesn't need any interaction.

Example:
```
npx skills add vercel-labs/agent-browser
```
```
Open our staging checkout page, fill in the test card details, complete the purchase, and screenshot the confirmation screen.
```

Reference: [agent-browser](https://github.com/vercel-labs/agent-browser)

### Tip 5: Browse skills.sh before writing one from scratch

[skills.sh](https://www.skills.sh) is Vercel's directory of open-source agent skills, searchable by name or by what they do. Before writing a new skill from scratch, check whether someone already published one for the same job. The `npx skills` CLI handles the whole lifecycle: `npx skills add <owner/repo>` installs a skill from the registry, `npx skills list` shows what's installed, and `npx skills update` pulls the latest version of everything you've added instead of you tracking each source repo by hand. It's the same CLI Tip 4's agent-browser example uses to install, just applied as your everyday way of managing every skill you pull in, not a one-off install command.

Example:
```
npx skills add vercel-labs/agent-browser
npx skills list
npx skills update
```

Reference: [skills.sh](https://www.skills.sh)

## Mcp

### Tip 1: Bundle MCP servers, skills, and hooks together as a plugin

Once you're managing more than one or two MCP connections, a plugin is the better unit to work in. A single plugin can bundle language servers, MCP connections, skills, agents, and hooks into one install. Run `/plugin` to install from Anthropic's official marketplace, or stand up an internal one for your org and check the marketplace reference into `settings.json` so every new developer gets it automatically on setup.

Example:
```
/plugin
```
or add a server directly:
```
claude mcp add sentry --url https://mcp.sentry.dev
```

Reference: [MCP](https://code.claude.com/docs/en/mcp)

### Tip 2: Tune how aggressively Claude loads your MCP tool definitions

Every MCP tool's schema counts against your context window before Claude has used it even once, and fifty tools can burn 10-20k tokens before you've typed a word. Tool search is on by default in current versions of Claude Code: instead of loading every schema upfront, Claude searches your tool catalog and pulls in only what the current task needs, up to five tools at a time. Set `ENABLE_TOOL_SEARCH=auto:5` if you want it to kick in earlier, once definitions cross 5% of the context window instead of the default threshold, or set it to `false` if you run a small, stable toolset and would rather load everything upfront and skip the extra round trip.

Reference: [Scale to many tools with tool search](https://code.claude.com/docs/en/agent-sdk/tool-search)

### Tip 3: Keep raw tool output out of your context with a sandboxed MCP server

Every byte a tool call returns lands in your context window, whether you needed all of it or not. [context-mode](https://github.com/mksglu/context-mode) is an MCP server that works around this: it runs commands and file reads in a subprocess, indexes the full output with SQLite, and hands back only what you explicitly print. A repo-wide grep or a log scan that would normally dump thousands of lines into the conversation instead returns a short, derived answer, and the rest stays searchable if you need it later. It also snapshots the conversation right before a compaction and reindexes it, so a compacted session can pull back a specific decision or file instead of losing it for good. This is worth reaching for whenever the output size is unpredictable and you plan to filter it down anyway, not for a command whose short output you'd read in full regardless.

Example:
```
Count the exported functions in every .ts file under src/, then report only the top 10 by count.
```
With context-mode installed, Claude runs this in the sandbox and returns a 10-line summary instead of reading all the files into context.

Reference: [context-mode](https://github.com/mksglu/context-mode)

### Tip 4: Give Claude persistent memory across sessions with claude-mem

Session resume with `--continue` or `--resume` replays a transcript, and CLAUDE.md only holds what you type into it yourself. Neither one remembers what Claude actually found out while working. [claude-mem](https://github.com/thedotmack/claude-mem) fills that gap: a plugin that hooks into five points in Claude's lifecycle and captures decisions, bug fixes, and other observations into a local SQLite and vector store as you go. A `SessionStart` hook then feeds the relevant slice of that history back in automatically at the start of your next session, no manual note-taking required. Install it from the plugin marketplace and restart Claude Code and it starts capturing immediately, no slash command needed to turn it on. Once enough history has built up, the bundled `mem-search` skill lets you ask about your own project's past in plain language. Wrap anything sensitive in `<private>` tags to keep it out of storage. Everything runs locally by default, and signing in only adds an optional hosted memory tier on top.

Example:
```
/plugin marketplace add thedotmack/claude-mem
/plugin install claude-mem
```
Then, in a later session:
```
What did we decide about the retry policy in the payments service?
```

Reference: [claude-mem](https://github.com/thedotmack/claude-mem)

## Prompt

### Tip 1: Have Claude interview you before building something big

For a feature with real design decisions in it, don't start by writing a spec yourself. Start with a one-line prompt and let Claude interview you using the `AskUserQuestion` tool instead. It surfaces edge cases, tradeoffs, and UX questions you haven't considered yet, then writes the result to `SPEC.md`. Start a brand new session to actually build the feature: that session gets a clean context focused entirely on implementation, with a written spec to work from instead of a long back-and-forth it would otherwise have to re-derive.

Example:
```
I want to build a rate limiter for our public API. Interview me in detail using the AskUserQuestion tool.

Ask about technical implementation, UI/UX, edge cases, concerns, and tradeoffs. Don't ask obvious questions, dig into the hard parts I might not have considered.

Keep interviewing until we've covered everything, then write a complete spec to SPEC.md.
```

Reference: [Best practices](https://code.claude.com/docs/en/best-practices)

### Tip 2: Write the code in one session, review it in another

A session that just wrote a piece of code is biased toward believing it's correct. Open a second session with a fresh context, hand it just the file or the diff, and ask it to review, and it will catch things the first session glossed over. The same split works for tests: have one session write tests first, then a different session write the code that has to pass them.

Example:
Session A: `Implement a rate limiter for our API endpoints`
Session B: `Review the rate limiter implementation in @src/middleware/rateLimiter.ts. Look for edge cases, race conditions, and consistency with our existing middleware. Don't fix anything, just report what you find.`

Reference: [Best practices](https://code.claude.com/docs/en/best-practices)

### Tip 3: Put your planning effort into plan mode, not into micromanaging

Shift+Tab cycles into plan mode. The idea is to pour your attention into getting the plan right so Claude can implement it in one pass, rather than course-correcting it turn by turn during implementation. A pattern worth stealing: have one Claude write the plan, then start a second Claude to review it the way a staff engineer would before you approve it. If something goes sideways mid-implementation, go back to plan mode and re-plan instead of trying to patch your way out live.

Example:
```
Plan a migration of our session storage from Redis to Postgres. Don't write any code yet.
```

Reference: [Power user tips](https://support.claude.com/en/articles/14554000-claude-code-power-user-tips)

## Hooks

### Tip 1: Hook into specific moments in Claude's lifecycle

Hooks run your own logic deterministically at fixed points in a session: `SessionStart` when a session begins, `PreToolUse` and `PostToolUse` around every tool call, `PermissionRequest` when Claude is about to ask you for approval, `Stop` when a turn is about to end, and `PostCompact` right after context gets compressed. You don't need to write these by hand from scratch. Ask Claude directly and it will generate one for you, matcher and all.

Example:
```
Write a hook that runs eslint after every file edit
```

Reference: [Hooks](https://code.claude.com/docs/en/hooks)

### Tip 2: Auto-format on every edit with a PostToolUse hook

`PostToolUse` is the hook worth setting up first, since it catches formatting issues right after Claude writes or edits a file, before they ever reach CI. Match on the `Write` and `Edit` tools and run your formatter as a command. A failing formatter shouldn't block the edit itself, so a trailing `|| true` keeps the session moving even if formatting fails.

Example: `.claude/settings.json`
```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [{ "type": "command", "command": "bun run format || true" }]
      }
    ]
  }
}
```

Reference: [Hooks](https://code.claude.com/docs/en/hooks)

### Tip 3: Use a Stop hook as a deterministic gate for unattended runs

For a long run you want to walk away from, a `Stop` hook is more reliable than asking Claude nicely to verify itself before finishing. It runs your check as a script and refuses to let the turn end until that check passes. Claude Code caps this at 8 consecutive blocks and then ends the turn anyway, so a broken check can't trap a session forever. This is the difference between "please run the tests before you finish" as a suggestion and a turn that mechanically cannot end while the tests are red.

Reference: [Hooks](https://code.claude.com/docs/en/hooks)

### Tip 4: Get worktree isolation on non-git version control

`--worktree` only works with git, but the isolation it buys you doesn't have to be git-specific. Define `WorktreeCreate` and `WorktreeRemove` hooks in `settings.json`, and Claude Code calls them to set up and tear down an isolated workspace on Mercurial, Perforce, or SVN the same way it would with a native git worktree. This is the only way to get parallel, non-interfering sessions if your team isn't on git, and it's a small amount of hook code for a real workflow unlock.

Reference: [Hooks](https://code.claude.com/docs/en/hooks)

## Workflow

### Tip 1: Treat CLAUDE.md as a file that gets smarter, not a README

CLAUDE.md isn't documentation, it's instructions: naming rules, test commands, style preferences, and mistakes Claude has made before. When Claude gets something wrong, fix the immediate problem, then ask it to update CLAUDE.md so the same mistake doesn't happen again. Boris Cherny calls this "Compounding Engineering": every caught mistake becomes prevention for every future session, and because the file is checked into git, one engineer's fix helps the whole team. If you've installed the GitHub Action, you can even trigger this straight from a PR comment.

Example:
```
@claude nit: use a string literal, not a ts enum. Add to CLAUDE.md to never use enums, always prefer literal unions.
```

Reference: [CLAUDE.md files](https://code.claude.com/docs/en/memory)

### Tip 2: Reserve "IMPORTANT" for the one rule Claude keeps missing

If Claude keeps skipping a specific instruction in CLAUDE.md, adding emphasis like "IMPORTANT" to that single line pulls it back into focus. The catch is that this only works if you use it sparingly: emphasize five lines and none of them stand out anymore. Save it for the rule that's actually getting ignored, not as your default way of writing every line in CLAUDE.md.

Example:
```
IMPORTANT: never commit directly to main, always open a PR.
```

Reference: [Best practices](https://code.claude.com/docs/en/best-practices)

### Tip 3: Let /doctor prune your CLAUDE.md for you

A CLAUDE.md file grows over time, and a bloated one is exactly what causes Claude to miss instructions buried in the noise. Run `/doctor` on a checked-in CLAUDE.md and Claude proposes cuts for anything it can already derive by reading the codebase, like standard language conventions or self-evident practices you didn't need to spell out. Treat the file like code: review it when something goes wrong, prune it on a schedule, and confirm a change actually shifted Claude's behavior instead of assuming it will.

Reference: [Best practices](https://code.claude.com/docs/en/best-practices)

### Tip 4: Give Claude a way to check its own work

This is the single most valuable habit on this whole list. Without a feedback loop, Claude assumes its output is correct and stops there. With one, it iterates until the output actually is correct. What that loop looks like depends on the domain: a screenshot compared against a spec for web work, a simulator run for mobile, a test suite for a backend. Boris Cherny estimates this alone is worth a 2-3x improvement in output quality. Before starting anything nontrivial, ask what "done and correct" looks like, and make sure Claude has a way to check it, not just a way to claim it.

Example:
```
Implement the checkout flow, then take a screenshot of the final state and compare it against @designs/checkout.png before telling me it's done.
```

Reference: [Best practices](https://code.claude.com/docs/en/best-practices)

### Tip 5: Run risky, unsupervised work in a container

A session running with `--dangerously-skip-permissions` shouldn't run on your host machine, because if something goes wrong there's nothing containing the damage. Move that session into a container instead, and a bad outcome stays inside the container. This is the right setup for long research tasks, or for something like patching a minified CLI bundle after an upgrade: Claude can explore, apply a patch, notice it didn't work, and iterate, all without you approving each step, because the blast radius is contained by the environment rather than by your attention.

Reference: [Permission modes](https://code.claude.com/docs/en/permission-modes)
