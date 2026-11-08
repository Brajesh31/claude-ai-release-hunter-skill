# AI Release Digest Quality Checklist

Use this checklist before saving state or sending an email digest.

## Coverage and time window
- [ ] The reporting window and timezone are explicit.
- [ ] Each configured source was checked or marked failed/skipped.
- [ ] GitHub organization/repository scans distinguish releases from commits.
- [ ] Current changelog/page snapshots were compared with prior snapshots.
- [ ] Hacker News results satisfy the configured date, points, and relevance filters.
- [ ] The digest states when any source could not be checked.

## Accuracy and relevance
- [ ] Every item links to its primary release, commit, changelog entry, or discussion.
- [ ] Dates are taken from the source, not inferred.
- [ ] The change is meaningful to the configured audience.
- [ ] Duplicate announcements and already-reported items are removed.
- [ ] A release is not described as shipped when the source only announces a preview or roadmap.
- [ ] Google items are described without adding a Claude/Anthropic comparison angle.
- [ ] No unsupported claims or invented impact estimates appear.

## Email safety
- [ ] Recipient matches RECIPIENT_EMAIL.
- [ ] Subject and language match configuration.
- [ ] The output body is saved to the durable output directory.
- [ ] The delivery command is approved and does not expose credentials.
- [ ] A dry run is reviewed before the first scheduled send.

## State integrity
- [ ] State is read before filtering previously seen items.
- [ ] New IDs/tags/SHAs are written only after successful delivery.
- [ ] A failed send leaves items eligible for retry.
- [ ] Run summary records checked sources, reported items, and failures.
- [ ] State and snapshots contain no credentials or message secrets.
