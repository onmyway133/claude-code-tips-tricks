# Contributing

This repo is a curated list of Claude Code tips. Contributions are welcome, but every tip goes through a quick review to keep the collection tight and non-redundant.

## Before you start

Open an issue or a draft PR describing the tip idea before writing it up. This avoids duplicate or overlapping tips — check the table of contents in `README.md` first to see if something similar already exists.

## Where a tip goes

Tips are grouped into sections in `README.md`: General, Command, Agent, Skill, Mcp, Prompt, Hooks, Workflow. Add a new section only if a tip doesn't fit any existing one.

Within a section, tips are numbered sequentially starting at 1. Add your tip to the end of its section so existing tip numbers don't shift.

Add a matching entry to the table of contents at the top of `README.md`, linking to the tip's heading anchor.

## Writing a tip

- Heading format: `### Tip N: Title`
- Title is plain and descriptive — no catchy phrasing, no buzzwords.
- Body is 5-10 sentences of original prose. Don't pad it — be concise.
- Break up long paragraphs into shorter ones.
- Include a short code snippet or prompt example if it helps illustrate the tip. Prompt examples are encouraged for most tips.
- If a tip needs a reference link, link only to official documentation (GitHub, Anthropic/Claude Code docs) — no blog posts or third-party sources.
- If a tip needs more than that (e.g. a diagram or a longer walkthrough), put the extra detail in a new file under `tips/` and link to it from the tip in `README.md`. Keep code snippets there short too.

## Style

Writing must be simple, concise, and in your own words — don't lift phrasing from source material or existing docs.

## Submitting

Open a PR with the tip. Mention any source material or research that informed it so it can be reviewed for accuracy.
