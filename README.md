# claude-ai-release-hunter-skill

A Claude Code skill for collecting, deduplicating, and delivering a recurring digest of significant AI product and developer-tool releases.

## Overview

This skill organizes a release-monitoring workflow that scans configured public release channels, identifies meaningful changes, removes duplicates, and prepares a digest for delivery.

It is designed for scheduled use, such as a daily run, and keeps local state so previously reported items are not repeatedly included.

## Main Capabilities

- Monitor configured AI product and developer-tool release sources.
- Review repository changes and product updates.
- Collect relevant release announcements and technical changes.
- Deduplicate previously reported items.
- Store run state and snapshots.
- Generate a structured digest.
- Prepare email content for a configured delivery command.
- Keep run logs for troubleshooting.

## Configuration

The skill uses environment and directory settings for delivery and local state. Review the configuration table in `SKILL.md` before the first run.

Typical configuration includes:

- Recipient email address.
- Email delivery command.
- State directory.
- Snapshot directory.
- Output directory.
- Digest language.
- Email subject.

Do not store email credentials or API tokens in the repository. Use environment variables or a secure secret manager.

## Installation

```bash
git clone https://github.com/Brajesh31/claude-ai-release-hunter-skill.git ~/.claude/skills/ai-release-hunter
```

## Usage

Invoke the skill when requesting a release digest or configuring a scheduled monitoring workflow:

```text
/ai-release-hunter
```

Specify the sources to monitor, digest cadence, delivery method, language, and relevance criteria.

## Typical Workflow

1. Load configuration and credentials securely.
2. Read the previous deduplication state.
3. Collect updates from configured sources.
4. Normalize and classify candidate items.
5. Remove duplicates and previously reported changes.
6. Filter for meaningful releases.
7. Generate the digest.
8. Deliver it through the configured email command.
9. Save updated state and logs.
10. Review failures and incomplete source checks.

## Reliability and Operations

- Use bounded request timeouts.
- Handle unavailable sources independently.
- Avoid sending duplicate digests after partial failures.
- Preserve state between scheduled runs.
- Keep snapshots and logs for diagnosis.
- Validate the recipient and delivery command before enabling automation.
- Report which sources failed or were skipped.

## Repository Contents

- `SKILL.md`: Main release monitoring workflow and configuration.
- `README.md`: Setup, scheduled use, and operational guidance.

## Scheduling

The workflow can be run by a scheduler such as cron or another automation system. Choose a cadence that matches the value of the updates and ensure that the execution environment has the required network access, credentials, and delivery command.

## Important Note

This skill summarizes configured release sources. It does not guarantee that every relevant AI release will be detected. Review source coverage and failed checks before treating a digest as comprehensive.

## Supporting Resources

| File | Purpose |
|---|---|
| [Source coverage register](resources/source-coverage-register.csv) | Track configured source groups, check methods, coverage, and failures. |
| [Digest quality checklist](resources/digest-quality-checklist.md) | Validate coverage, relevance, source links, email safety, and state updates. |
| [Seen-state example](resources/seen-state-example.json) | Show the basic shape of deduplication state without credentials or real user data. |

## Important operating notes

The monitored source list and repository names in SKILL.md are a starting configuration, not a guarantee of complete coverage. Confirm source availability, date windows, API limits, and relevant changes on each run. The workflow can make many GitHub API calls, so handle rate limits and partial source failures explicitly. Do not advance deduplication state until delivery succeeds, otherwise an item may be silently lost on retry.
