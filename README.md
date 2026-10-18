# PR Review

A multi-agent skill for GitHub pull request reviews with verified, low-noise findings.

Four independent bug hunters review the code alongside architecture and security reviewers. Bug findings need agreement from at least two passes. A fact-checker verifies candidates against the source, then a judge filters by severity. Existing discussion is checked to avoid duplicate comments or reopening settled concerns.

**This skill submits reviews directly to GitHub:** approvals, requests for changes, or comments. Line-specific findings become inline comments; architecture findings without a specific line go in the review body.

## Requirements

- A coding agent that can load `SKILL.md`, read local files, run shell commands, and spawn independent agents.
- Git and the GitHub CLI (`gh`), authenticated with access to the target repository and permission to submit reviews.
- A local checkout of the PR's code accessible to every review agent.

Agents run in parallel when supported, or sequentially in isolated sessions. Without independent-agent support, the skill stops rather than performing a single-agent review.

## Installation

Clone this repository into your agent's skills directory, replacing `/path/to/skills` with the directory your agent uses:

```bash
git clone https://github.com/h4ni0/pr-review.git /path/to/skills/pr-review
```

Keep `SKILL.md` and `references/` together. Follow your agent's instructions for discovering or reloading skills. This is a Markdown skill, not a standalone CLI or GitHub Action.

## Usage

With the target PR checked out, ask your agent:

```text
Use the pr-review skill to review https://github.com/OWNER/REPO/pull/123.
The checkout is at /path/to/repository.
```

The skill reviews the code, verifies findings, checks prior discussion, and submits one review outcome. Filtering counts are reported locally, not included in the GitHub review. No PR summary is required.

## Files

- [SKILL.md](SKILL.md) — review workflow and submission rules.
- [references/reviewer-prompts.md](references/reviewer-prompts.md) — complete prompts for the five agent roles.
- [LICENSE](LICENSE) — MIT license.

## Limitations

Agent support varies by host; no host-specific compatibility has been validated. Multi-agent reviews consume more time and tokens than a single pass. Consensus and verification can still miss defects or retain false positives; this does not replace tests or human judgment.

GitHub permissions and review restrictions still apply, including restrictions on reviewing your own PR.

## License

[MIT](LICENSE) © 2026 Hani (@h4ni0).
