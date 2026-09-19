# How releases work: which build your system gets

Every sysext in this org installs with the same one-liner shape:

```bash
curl -fsSL https://raw.githubusercontent.com/truenas-community-sysexts/<repo>/main/get.sh | sudo bash
```

`get.sh` works out which build suits your system, checks it, and runs that build's own installer. This page explains how it chooses, why it sometimes refuses, and how you can help.

## The short version

- A build is only installed after somebody has run it on real hardware and said it worked.
- "Worked" is recorded per TrueNAS train, so a pass on TrueNAS 26 does not put that build on 25.10 systems.
- If nothing has been signed off for your system yet, the installer stops and tells you what it is waiting for. It does not install something untested.

## Trains

A "train" is a TrueNAS release line:

- **25.10**, **25.04**: the version's first two parts.
- **26**: from TrueNAS 26 onward the major version alone is the train, so every 26.x release, betas included, is train 26.

Trains matter because TrueNAS changes between them in ways that affect these packages: different kernels, different system libraries, and different internal APIs that the install scripts use.

## What get.sh does

1. Reads your TrueNAS version and works out your train.
2. For driver sysexts (coral, hailo, memryx), also reads your running kernel (`uname -r`). A kernel module only loads on the exact kernel it was built for, so this is the first filter.
3. Finds published releases approved for your train, and takes the newest.
4. Downloads that release's image, checks it against the release's checksum, and runs **that release's own installer**, not the newest code in the repo. So the installer you run is the one that was tested.
5. Sets up persistence, so the sysext survives reboots and TrueNAS updates.

To install one exact build instead, pin it. This skips the approval check and is how a tester installs a build under test:

```bash
curl -fsSL .../main/get.sh | sudo bash -s -- --release=TAG
```

## What "approved" means

Every new build is published as a **pre-release** and opens a hardware-test issue. Closing that issue as completed is the sign-off, and it records approval for that build's train in the release notes, as a line like:

```
<!-- verified-train: 26 -->
```

So:

- A sign-off on TrueNAS 26 makes that build available to 26 systems. 25.10 systems keep whatever was last approved for 25.10.
- Builds that were promoted before this scheme started count for every train. Nothing that used to install stopped installing.
- A build rejected during testing (its issue closed as "not planned") is never installed by anyone.

## When nothing is approved yet

You will see a message naming your train and the builds that are waiting, with links to their test issues. Nothing is installed. This normally means a build exists but nobody with your hardware has tested it yet.

Your options:

- Wait for someone to sign it off.
- Test it yourself and sign it off (see below).
- Pin the untested build deliberately with `--release=TAG`, accepting the risk.

## Helping: testing takes about ten minutes

This is the most useful thing a user can do here, and it needs no coding.

Each waiting build has an issue whose title says what to test, on what hardware, and on which TrueNAS version, for example:

```
Hardware test: Coral TPU driver Gasket 1.0-18.4 | TrueNAS 25.10.7 (kernel 6.12.105) | k6.12.105-gasket1.0-18.4-r14
```

The issue body is a step-by-step procedure: pre-checks, install, verify, reboot and re-verify, each with the exact commands and the output to expect. Run it, comment with what you saw, and close the issue as completed if it worked. That single act is what releases the build to everyone else on your train.

If it did not work, comment with the details and close it as "not planned" instead. That is just as useful: it keeps a broken build away from other people's systems.

## Uninstalling

```bash
curl -fsSL .../main/get.sh | sudo bash -s -- --uninstall
```

This uses the same approved release's uninstall scripts, so the removal matches the install.

## For maintainers and contributors

See [CONTRIBUTING.md](../CONTRIBUTING.md) for the contribution flow and the sign-off rules from the maintainer side.
