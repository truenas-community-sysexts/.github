<!--
Thanks for contributing. A few quick checks before you submit.

If this is a typo fix or one-line obvious cleanup, you can delete most of this template.

Otherwise, please fill in the sections below. They map directly to the contributor guide in this org's .github repo (CONTRIBUTING.md).
-->

## Summary

<!-- One or two sentences. What changed and why. -->

## Linked issue or discussion

<!-- For non-trivial changes, link the issue or discussion you opened first. Trivial PRs can write "n/a". -->

Closes #

## Test plan

<!--
Describe what you actually ran. For installer / kernel-module / runtime changes, "CI passes" is not a test plan on its own.

Examples of useful entries:
- Dispatched build.yml for TrueNAS 25.10.3.1 / HailoRT 4.21.0; installed the resulting sysext on a Frigate host; verified `hailortcli fw-control identify` returns the expected firmware.
- Ran install.sh --dry-run on a multi-pool host and confirmed it errored cleanly rather than picking a pool silently.
- Uninstalled with Frigate stopped, then with Frigate running — second case now fails fast as intended.

If you couldn't test something on real hardware, say so explicitly below.
-->

- [ ] CI is green (lint / actionlint / shellcheck)
- [ ] Built the sysext locally or via `workflow_dispatch` (link the run if applicable):
- [ ] Exercised the affected install / uninstall / runtime path on real hardware
- [ ] If any of the above is "no", I've explained why below:

## Scope check

- [ ] The diff is limited to the change described in the summary — no drive-by reformatting, untouched-code refactors, or new abstractions that aren't load-bearing for this PR.

## AI assistance (optional)

<!--
Mentioning AI involvement is helpful but not required. It tells reviewers what to scrutinize.

Examples:
- "Claude wrote the initial draft; I rewrote the install-path logic and tested on hardware."
- "Cursor autocomplete only."
- "All hand-written."

This is informational — not a gate.
-->
