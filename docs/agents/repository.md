# Repository details

## Purpose and architecture

This is Steve Shickles's GitHub profile repository, `sshickles/sshickles`.
GitHub displays the root README.md on the owner's profile. There is no
application, package manager, server or database. The scripts and agent docs
implement the canonical repository standard; the profile content is independent.

## Commands and tool versions

Linux is the only supported development platform. Git, Python 3.11+ and mise
are host prerequisites. mise.toml pins actionlint 1.7.12, the only additional
tool used by validation. Bash supplies shell syntax checking.

- `./scripts/setup` installs the pinned tool and selects `.githooks`.
- `./scripts/setup --doctor` verifies local setup.
- `./scripts/check` validates policy integrity, runs test, actionlint and shell syntax checks.
- `./scripts/test` validates repository structure and canonical provenance.
- `./scripts/review` runs the configured CodeRabbit review against origin/main.

CI runs `./scripts/check` in the `checks` job. The policy audit workflow
reports canonical updates without applying them.

## Configuration ownership

Steve owns profile content and GitHub repository configuration. There are no
service environments, application secrets or pulled environment files.
`.repo-standard.json` defines repository validation and integrations;
`.repo-standard-source.json` records canonical provenance. Live rulesets and
reviewer dashboard settings are managed separately in GitHub and Greptile.

## Local runtime setup

Use the assigned Linux host and the existing T3-managed task worktree. Run
`./scripts/setup` followed by `./scripts/setup --doctor`. The custom dependency adapter uses exact pins in mise.toml as its lockfile
and links the installed actionlint binary into ignored `.tools/actionlint`.
There are no application dependencies or development servers to start.
The default branch is main and the remote is origin.

## Verification

This README-only repository has no application test suite. The test entry point
honestly runs policy and structure validation; check adds workflow lint and
shell syntax validation. Review profile edits for Markdown rendering and
accurate links. Follow [review checklist](review-checklist.md).

There were no existing setup scripts, hooks, tests or CI workflows to migrate.
The shared pre-push hook rejects main destinations and runs `check --pre-push`.
The custom structure validator has no supported affected-test mapping, so hook
mode keeps the full test command. CI and plain `check` also retain full validation.
No additional
repository checks are needed under `.githooks/pre-push.d/`. PR review requires
current-head Greptile 5/5 and a clean local CodeRabbit review.

## Deployment and recovery

GitHub renders README.md directly; there is no deployment command or hosted
application to roll back. Recover content through a reviewed revert PR.
Preserve unpublished work and use T3's worktree manager for cleanup. Canonical
updates use the external generator as described in [setup](../setup.md).

## Approved exceptions

None.
