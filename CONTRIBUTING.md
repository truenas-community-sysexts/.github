# Contributing to TrueNAS Community Sysexts

Thanks for taking the time to contribute. These repos build systemd-sysext packages that run on real TrueNAS hosts in real homelabs, and bugs in install scripts, kernel modules, or sysext layouts can leave someone's NAS in a state they have to recover from manually. That shapes most of the guidance below.

These rules are the same for every repo in the org. This file is the single contributing guide: repos do not carry their own `CONTRIBUTING.md` (on GitHub a repo-level file would replace this one, not add to it). Repo-specific build and test details live in each repo's `docs/`.

## How changes flow: your fork > our `dev` > our `main`

Every change reaches a release the same way:

```
your fork (feature branch)  --PR-->  dev  --maintainer sync PR-->  main  -->  builds and releases
```

1. **Fork the repo** and create a branch in your fork from our **`dev`** branch, not `main`.
2. **Open your PR against `dev`.** GitHub pre-selects `main` as the base for PRs from forks, so change the base to `dev` before you submit. A PR from a fork that targets `main` is closed automatically with a note asking you to open it against `dev` instead (it is not retargeted for you, since a fork branch cut from an older `main` could otherwise pull in unrelated history).
3. **CI runs on your PR** (lint, shellcheck, actionlint and the repo's unit tests, depending on the files touched). For a first-time contributor, a maintainer has to approve the workflow run before it starts.
4. **A maintainer reviews and merges it into `dev`.**
5. **Maintainers sync `dev` into `main`** with a pull request, merged as a merge commit so both branches keep a shared history. Contributors never open PRs into `main`.
6. **`main` is what ships.** The scheduled checks and builds run from `main`, and the install one-liners serve the Latest release, which is built from `main` and only promoted after a hardware-test sign-off (see Hardware testing below).

Automated commits (version tracking, the supported-versions tables, the NVIDIA driver catalog) are made by our CI app directly on `main`; maintainers sync `main` back into `dev` to keep them level.

## Before opening a PR

For anything beyond a typo fix or one-line obvious cleanup, **open an issue or discussion first**. A two-line "I want to do X, here's my plan" message saves everyone time and avoids you sinking effort into a PR that gets closed on direction grounds. PRs that arrive with no context, lots of churn, or no evidence of testing will get closed with a pointer back to this document.

We'd rather have a 10-line conversation than a 500-line cleanup.

## Quality bar for every PR

- **You've read what you're submitting, every line.** If a reviewer asks "why is this here?", "couldn't you do this without the loop?", or "what happens if X is missing?", you can answer.
- **You've tested it.** For non-trivial changes, run a build (`workflow_dispatch` on the relevant build workflow makes this easy) and exercise the affected install / uninstall / runtime path on real hardware. If you genuinely can't test something, say so explicitly in the PR description, don't hide it.
- **The diff is scoped to what the PR claims to change.** No drive-by reformatting, no "while I was in there" refactors of untouched code, no new abstractions that don't carry their weight for this specific change.
- **Comments explain *why*, not *what*.** Self-explanatory code shouldn't be narrated. `# Loop through items` above `for item in items:` should be deleted, not committed.
- **No speculative abstractions.** Helper functions used once, parameters added "for future use," base classes with one subclass: strip them.

## AI-assisted contributions

We use AI tools heavily ourselves. A substantial share of the maintainers' commits across these repos are AI-assisted. So contributions written with help from Claude, Copilot, Cursor, ChatGPT, or anything else are welcome on the same terms as any other contribution.

**The bar isn't whether AI wrote it. The bar is whether you can stand behind it.**

You don't have to disclose AI use, but mentioning it in the PR description is helpful: it tells reviewers what kind of review to give. The PR template has an optional slot for this.

What we push back on, regardless of source:

- PRs where the author can't explain why each change is there.
- AI-generated cleanup sweeps that touch unrelated code ("while we're here, let's modernize this loop").
- AI-suggested abstractions, helper functions, or comments that exist only because the model added them.
- Untested changes to install scripts, kernel modules, or anything that runs at boot.

If a reviewer says "this looks AI-generated and you don't seem to know why X is in here", take the feedback seriously. It's not a personal accusation; it's a signal that the PR isn't ready and needs another pass from you, not the model.

## Hardware testing

Most of these repos build sysexts that load kernel drivers or modify boot-time state. "Builds locally" and "CI passes" are necessary but not sufficient for changes that affect the install path, the kernel module, or runtime behavior: those need to be exercised on hardware.

If you don't have access to a repo's target hardware, that's fine, you can still contribute documentation fixes, CI improvements, and discussion. For driver/install changes, either find a way to test or be very explicit in the PR that you couldn't, and what specifically wasn't exercised. Maintainers may hold those PRs until someone can verify on hardware.

The auto-build workflows generally tag a release as un-promoted ("not Latest") and open a hardware-test issue when a daily check dispatches a build. That same flow is available manually via `workflow_dispatch` for testing your branch end-to-end without touching `Latest`.

Test reports are contributions too: if you own target hardware, commenting on a repo's open `hardware-test` issues with your results is one of the most useful things you can do here, no code required.

## Review process

- All changes go through a PR. `main` and `dev` are protected in every repo: no direct pushes, no force-pushes, no deletion. That applies to maintainers too.
- Only the org owner can override that protection, and only by hand when merging a PR.
- Maintainers may merge their own PRs into `dev` once CI is green and the change is straightforward.
- PRs from non-maintainers will get at least one maintainer review before merge.
- Reviewers may ask you to force-push *your own branch* to clean up history (squash fixup commits, drop drive-by changes) before merging.

## Reporting bugs and requesting features

Use the issue tracker on the repo the bug is in. Include:

- What you ran and what happened.
- What you expected to happen instead.
- TrueNAS version, hardware, and (if relevant) the sysext release tag you have installed.
- Any relevant log output (`dmesg`, `journalctl -u <unit>`, install-script stdout).

For security-sensitive issues, follow whatever `SECURITY.md` says in that repo, or contact a maintainer privately rather than filing a public issue.

## License

By contributing, you agree your contribution is licensed under the same terms as the repo you're contributing to (MIT for all current repos in this org).
