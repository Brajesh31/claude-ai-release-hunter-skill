# claude-ai-release-hunter-skill

A Claude Code skill for collecting, filtering, and delivering a recurring digest of important AI product and developer-tool updates.

## Capabilities

- Monitor selected public GitHub organizations and repositories.
- Review releases, meaningful commits, product changelogs, and technical discussions.
- Filter routine activity and duplicate announcements.
- Rank updates for a defined audience.
- Prepare a structured daily briefing.
- Preserve run state and page snapshots.
- Deliver an approved digest through a configured email workflow.
- Record incomplete checks and delivery failures.

## Install

~~~bash
git clone https://github.com/Brajesh31/claude-ai-release-hunter-skill.git ~/.claude/skills/ai-release-hunter
~~~

## Use

~~~text
/ai-release-hunter
~~~

Specify the organizations and products to monitor, reporting window, time zone, audience, delivery method, and digest language.

## Run workflow

1. Establish the reporting window.
2. Collect releases and meaningful product changes.
3. Filter noise and remove duplicates.
4. Draft the digest with links and clear dates.
5. Review the message and recipient.
6. Deliver through the approved method.
7. Save deduplication state only after successful delivery.

## Supporting materials

| File | Purpose |
|---|---|
| [Digest quality checklist](resources/digest-quality-checklist.md) | Review relevance, dates, coverage, delivery safety, and state integrity. |
| [Deduplication state example](resources/seen-state-example.json) | Illustrate the persistent state format. |
| [Platform coverage register](resources/platform-coverage-register.csv) | Maintain monitored organizations, pages, methods, and check status. |
| [Daily digest template](resources/daily-digest-template.md) | Prepare a consistent daily briefing. |
| [Monitoring schedule runbook](resources/monitoring-schedule-runbook.md) | Configure recurring execution, delivery, and recovery. |

## Operational requirements

Use a stable time zone, persistent storage, protected credentials, and a reliable delivery command. A failed delivery must not advance deduplication state. The report must identify any platforms that could not be checked.

## License

MIT. See the root [LICENSE](LICENSE).