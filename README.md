# Claude AI Release Hunter Skill

A Claude skill that monitors public AI engineering activity and prepares a deduplicated daily release digest. It tracks selected GitHub organizations and repositories, Claude-related product updates, technical blog posts, Vercel Labs experiments, and Hacker News.

The digest is designed to highlight meaningful releases and changes rather than produce an unfiltered stream of links.

## What It Monitors

The skill's configured watch list covers:

- **Anthropic:** Claude Code, SDKs, cookbooks, courses, Claude-related changelogs, and the claude.dev technical blog.
- **Meta:** Selected repositories from the `meta-llama` and `facebookresearch` organizations.
- **Vercel Labs:** Agent tooling, developer experiments, skills, and changes to the Vercel Labs experiment catalogue.
- **OpenAI:** Codex, agent frameworks, guardrails, MCP-related tooling, and other selected developer repositories.
- **Google:** Gemini and agent-development repositories.
- **Hacker News:** Relevant discussions and launches.

The exact repository and page watch lists are defined in `SKILL.md` and can be adjusted as monitoring needs change.

## Key Features

- Checks configured sources for new releases, commits, posts, and experiments.
- Filters updates for relevance to AI, agents, developer tools, and related engineering work.
- Deduplicates previously reported items using a persistent JSON state file.
- Produces a structured daily digest with links and concise explanations of why each item matters.
- Supports scheduled execution through cron, a Claude Code routine, or `/loop`.
- Records snapshots and run outputs for operational review.

## Repository Structure

```text
.
├── SKILL.md
├── .gitignore
└── resources/
    ├── daily-digest-template.md
    ├── digest-quality-checklist.md
    ├── monitoring-schedule-runbook.md
    ├── platform-coverage-register.csv
    └── seen-state-example.json
```

- `SKILL.md` defines the monitoring workflow, sources, configuration, and digest behavior.
- `resources/daily-digest-template.md` provides the report structure.
- `resources/digest-quality-checklist.md` helps validate relevance and completeness.
- `resources/monitoring-schedule-runbook.md` describes recurring execution and recovery.
- `resources/platform-coverage-register.csv` tracks monitored platform coverage.
- `resources/seen-state-example.json` illustrates the deduplication state format.

## Installation

Clone the repository into your Claude skills directory:

```bash
git clone https://github.com/Brajesh31/claude-ai-release-hunter-skill.git ~/.claude/skills/ai-release-hunter
```

To update an existing installation:

```bash
cd ~/.claude/skills/ai-release-hunter
git pull
```

## Configuration

Review the Configuration section in `SKILL.md` before the first run. The workflow uses these settings:

| Setting | Purpose |
|---|---|
| `RECIPIENT_EMAIL` | Destination for the digest |
| `SEND_COMMAND` | Command or configured delivery integration used to send the email |
| `STATE_DIR` | Persistent deduplication state |
| `SNAPSHOT_DIR` | Stored page snapshots |
| `OUTPUT_DIR` | Generated email bodies and run logs |
| `EMAIL_LANGUAGE` | Language used for the digest |
| `EMAIL_SUBJECT` | Email subject |
| `AUDIENCE` | Context for the digest's relevance explanations |
| `GITHUB_TOKEN` | Recommended token for GitHub API rate limits |

The skill's documented defaults and required values are defined in `SKILL.md`. Configure a reliable email delivery command before expecting automated delivery.

## Running the Skill

Ask Claude to prepare a digest:

```text
Use the ai-release-hunter skill to scan the configured sources
and prepare today's AI release digest.
```

For recurring delivery, schedule the workflow using cron, a Claude Code routine, or another scheduler supported by your environment. The runbook in `resources/monitoring-schedule-runbook.md` covers scheduling, persistent state, delivery, and recovery.

## Operational Guidance

- Keep `.release-hunter/` and other runtime state out of version control.
- Persist the deduplication state between runs.
- Use a GitHub token to reduce the chance of API rate-limit failures.
- Do not mark items as delivered when email delivery fails.
- Make the digest identify sources that could not be checked.
- Review the quality checklist before sending a report.
- Keep credentials in environment variables or a secret manager.

## License

This repository is licensed under the MIT License. See [LICENSE](LICENSE).
