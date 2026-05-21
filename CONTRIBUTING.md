# Contributing to the Synth Community

This repo is the community hub — not the SDK source. Contributions here are discussions, issues, and feedback rather than code.

---

## Filing a bug report

Use the [bug report template](../../issues/new?template=bug_report.md).

Good bug reports include:
- Your Synth version: `pip show synth-agent-sdk`
- Python version: `python --version`
- Provider (Anthropic, OpenAI, Bedrock, etc.)
- A minimal reproduction — the smallest code that triggers the issue
- What you expected vs what actually happened
- Full error output including the traceback

If you're not sure it's a bug, start a [Q&A discussion](../../discussions/new?category=q-a) first.

---

## Requesting a feature

Use the [feature request template](../../issues/new?template=feature_request.md).

The most useful feature requests describe the **problem** first, not just the solution. "I want X" is less useful than "When I do Y, I can't Z, which means I have to work around it by...". That context helps us understand whether your proposed solution is the right one or whether there's a better approach.

Check the [roadmap](ROADMAP.md) and existing issues before filing — your request may already be tracked.

---

## Asking a question

Use [GitHub Discussions → Q&A](../../discussions/new?category=q-a).

Include:
- What you're trying to build
- What you've already tried
- Relevant code snippets (use code blocks)

---

## Sharing what you built

Use [GitHub Discussions → Show and tell](../../discussions/new?category=show-and-tell).

No minimum bar — a 20-line script that does something interesting is as welcome as a full production deployment. Include what problem it solves and any interesting patterns you used.

---

## Roadmap feedback

Use [GitHub Discussions → Roadmap Feedback](../../discussions/new?category=roadmap-feedback) or comment on the pinned roadmap discussion.

The most useful roadmap feedback includes:
- The specific use case you're blocked on
- How often you hit it
- What you're doing as a workaround today

---

## What this repo is NOT for

- SDK source code contributions (that happens in the SDK repo)
- Security vulnerability reports — email directly rather than filing a public issue
- Spam or self-promotion without substance
