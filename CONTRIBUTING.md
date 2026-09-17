# Contributing

How work moves from a design to a merged change in this repository. It applies to
every contributor, human or agent.

## Flow

1. **Rough design.** Written as documents in this repository and merged by pull
   request. The maintainer reviews it (see [What needs the maintainer](#what-needs-the-maintainer)).
2. **Milestones.** The rough design is cut into steps. Each step is a milestone: a
   state in which something works end to end.
3. **Issues.** Detailed design turns a milestone into issues. Each issue belongs to
   one milestone and carries one `area/*` label. An issue for a repository-wide change
   (see [Areas](#areas)) carries no area label, and has a milestone only if a
   milestone depends on it.
   - A task is an issue one pull request completes. It uses the Task template.
   - A feature that needs several tasks is a parent issue, using the Feature
     template, with the tasks as its sub-issues. A parent has no pull request of its
     own: it is closed when all of its sub-issues are closed and its own acceptance
     criteria are checked.
4. **Pull requests.** One task is implemented by one pull request, which closes it.
   - A task that turns out too large, before or during review, is split into new
     sub-issues and the pull request narrowed to one of them.
   - Work on a task starts only when every issue it is blocked by is satisfied: the
     work it needs is merged, or it has been confirmed that the dependency is no
     longer needed. An issue closed as a duplicate or as not planned satisfies
     nothing by being closed.

A milestone is a unit of tracking only. Design documents are not organized by
milestone (see [Documents](#documents)).

## Documents

Design documents live in `docs/`; [docs/README.md](docs/README.md) is the index and
says which document covers what.

- **Decisions live in the repository**, not in issue or pull request text. An issue
  states the goal and acceptance criteria and links the documents it relies on.
- **Subject documents say what holds now.** They are organized by subject and
  rewritten to stay current: a change of decision edits the document in place, and
  no section is appended to record what changed or when.
- **Decision records say why.** A decision that chooses between alternatives, or
  changes an earlier decision, gets a record in `docs/decisions/`: the context, the
  options considered, the choice and its reasons, and the documents and issues it
  affects. A record is never edited after it merges, except to mark it superseded by
  a later one. Subject documents link the records behind what they state.
- **A design change is made whole in one pull request**: the decision record, and
  every document it lists as affected. Implementation it affects is tracked as issues
  linked from the record.
- A document that describes something not built yet says so.

## Language

| text | language |
| --- | --- |
| code: identifiers, comments, error and log messages | English |
| issues, pull requests, review comments, commit messages | English |
| `README.md`, `CONTRIBUTING.md` | English |
| design documents | Japanese |

Issues and pull requests are written and reviewed mostly by agents, so they are in
English. Design documents are what the maintainer reads to decide, so they are in
Japanese.

- In Japanese text, technical terms and identifiers stay in English, untranslated:
  「`Volume` の `status.phase` が `Ready` になったら」. Code and documents are then
  searched with the same words, and a later translation has no terms to reconcile.
- A document exists in one language only. When one is translated, the translation
  replaces it; two copies drift.

## What needs the maintainer

The maintainer reviews decisions, not every change. Two things reach them.

### Changes to gated paths

These paths hold the design and the rules the repository runs by:

- `docs/`
- `.github/`
- `CONTRIBUTING.md`, `CLAUDE.md`, `AGENTS.md`

A pull request that changes any of them cannot merge until the maintainer adds the
`maintainer-approved` label. The `maintainer-approval` check enforces this, and a
later push that changes a gated path again removes the label.

- Only the maintainer adds `maintainer-approved`.
- A design change goes in its own pull request, merged before the implementation that
  relies on it. Mixed into an implementation pull request, it holds the whole change
  until the maintainer gets to it.
- An implementation does not depart from a design document it leaves unchanged. If
  the design cannot be followed, the design is changed first.

### Questions the design does not answer

Two kinds of choice come up while implementing, and only the first goes to the
maintainer:

- **A choice that changes what the design promises**: behavior a user or another
  module can observe, a public contract (API, CLI, stored data format), or a
  constraint a design document states. Example: whether deleting a network that
  still has ports attached is refused or cascades.
- **A choice that keeps those promises**: data structures, internal error handling,
  how code is split into functions and packages. Example: whether the ports of a
  network are looked up by a query or kept in an in-memory index. These are made by
  whoever implements, and the reason is stated in the pull request.

When work needs a choice of the first kind that no design document makes, or finds
that a document cannot be followed:

1. Stop the work that depends on the answer. Unrelated work continues.
2. Add the `needs-decision` label to the issue or pull request, and put the question at
   the top of its own comment, in English, with the options and a recommendation.
   The agent working with the maintainer relays it to them in Japanese.
3. Resume when the answer is merged into the design documents (a decision record and
   the documents it affects), not when it is given in the thread. Then remove the
   label.

## Areas

An area names the part of the system an issue or change belongs to. The same word is
used in two places:

| where | form | example |
| --- | --- | --- |
| issue label | `area/<area>` | `area/compute` |
| pull request title | `<type>(<area>): …` | `feat(compute): create a VM from an image` |

The areas are listed here and nowhere else. Labels are created from this table.

| area | covers |
| --- | --- |
| *(defined with the rough design)* | |

- Work that crosses areas is assigned to the area where most of the change lands, and
  depends on other issues through issue links ("blocked by #N") rather than carrying
  several area labels.
- A change to the repository as a whole — the rough design itself, these rules, CI,
  tooling — has no area and omits it: `docs: add the rough design`.

## Branches

- Branch from `main`; merge back by pull request. `main` accepts nothing else.
- Name: `<type>/<issue number>-<short-kebab-description>`, for example
  `fix/31-port-teardown`. Work without an issue drops the number.
- One branch per task. A merged branch is deleted and never reused.
- Keep up with `main` by rebasing or by merging `main` in; either is fine, because the
  branch is squashed on merge.

## Pull requests

### Title and body

- **The title becomes the commit on `main`**, since every pull request is squash
  merged. Write it in [Conventional Commits](https://www.conventionalcommits.org/)
  form:

  ```
  <type>(<area>): <summary in the imperative>
  ```

  `type` is one of `feat`, `fix`, `docs`, `refactor`, `test`, `build`, `ci`, `chore`.
  The area is omitted for repository-wide changes (see [Areas](#areas)). A breaking
  change adds `!` before the colon: `feat(api)!: …`.
- **The body becomes the commit message.** Use the template.
- Commits on the branch are free-form; they do not reach `main`.
- Refer to a milestone by link or number, not by its name, so renaming it breaks
  nothing.

### Work without an issue

Allowed only for repository-wide changes (the rough design, these rules, CI, tooling)
and for fixes small enough that an issue would only repeat the pull request. The
template's issue section then reads `No issue: <reason>` in place of `Closes #N`.

### Ready for review

A pull request is marked ready when its body shows, for each acceptance criterion of
its issue, how it was verified and the result, and lists anything not verified with
the reason. A pull request without an issue states what it set out to do and
verifies that instead. Until then it stays a draft.

### Review

- **The reviewer is not the author.** Codex reviews pull requests. If Codex also
  wrote the change, the review is still a separate review run on the pull request,
  never the session that wrote it.
- A review covers the head commit. A push after the review needs a new review of
  what the push changed.
- The author answers each review thread with the fix or with the reason for not
  changing the code. **A thread is resolved by the reviewer or the maintainer, never
  by the author.**
- If no review arrives, the author asks the maintainer; the pull request does not
  merge without one.

### Merge

A pull request can merge only when all of these hold:

1. Every acceptance criterion is verified and met. A criterion not met, or not
   verified, blocks the merge unless the maintainer accepts it in a comment on the
   pull request; the exception is also recorded in the body's "Not met or not verified" section.
2. The head commit has been reviewed, and no review thread is unresolved.
3. The required checks pass, including `maintainer-approved` where a gated path
   changed.

Where GitHub enforces all of these, enable auto-merge (`gh pr merge --auto --squash`)
and let it merge; nobody decides to merge by judgment. Today it enforces only part of
them: resolved threads, the squash-only rule and `maintainer-approval`. Until the rest
are required checks, **the maintainer merges every pull request**, and checks 1 and
2 before doing so.

## Commits

- Commit with the GitHub noreply address, not a personal one: this repository is
  public and commit metadata cannot be taken back.
- Never commit secrets. Push protection blocks known token formats, not all of them.

## GitHub Actions

- Reference every action by a full commit SHA; the repository refuses tags.
- Declare minimal `permissions` in each workflow. The read-only token is only the
  default and a workflow can ask for more.
- A `pull_request_target` workflow runs in the base repository's context, so even for
  a pull request from a fork it can use write permissions and secrets. Use it only when the workflow reads the pull request through the API and
  never checks out or runs its code, as `maintainer-approval` does. Use
  `pull_request` for anything that builds or tests.
- Never attach a self-hosted runner to this repository: pull requests from forks
  could run code on it.
