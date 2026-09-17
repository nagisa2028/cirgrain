# AGENTS.md

Instructions for coding agents working in this repository. Minimal for now; it will
grow with the design.

## Read first

[CONTRIBUTING.md](CONTRIBUTING.md) is the process every change follows: flow from
design to pull request, language, what needs the maintainer, branches, pull requests,
review and merge. It is the only place those rules are written; this file does not
repeat them.

## Rules specific to agents

- **Never add the `maintainer-approved` label**, and never resolve a review thread on a
  pull request you authored.
- **Never change repository settings or rulesets**, push to `main`, force-push a
  shared branch, or delete a branch you did not create. Repository settings are the
  maintainer's.
- **Stop on a decision that changes what the design promises** (see "Questions the
  design does not answer" in CONTRIBUTING.md). Label it `needs-decision` and ask the
  maintainer in Japanese; the question on GitHub stays in English.
- Talk to the maintainer in Japanese. Everything written to the repository or to
  GitHub follows the Language section of CONTRIBUTING.md.

## Review guidelines

For reviewers, including automated review:

- Check the change against the design documents it links. An implementation that
  departs from a design document it leaves unchanged is a defect, even if it works.
- Check each acceptance criterion against the verification the pull request reports.
