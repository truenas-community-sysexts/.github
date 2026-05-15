# TrueNAS Community Sysexts

Community-maintained [systemd-sysext](https://www.freedesktop.org/software/systemd/man/systemd-sysext.html) packages that extend [TrueNAS SCALE](https://www.truenas.com/truenas-scale/) with hardware support (drivers) and tooling (apps) that isn't shipped in the stock image — without modifying the immutable root filesystem.

Each sysext lives in its own repo with its own install scripts, build pipeline, and release cadence.

## Active sysexts provided by this org

- **[hailo8-support](https://github.com/truenas-community-sysexts/hailo8-support)** — Hailo-8 AI accelerator driver, firmware, and userspace tooling. Useful for Frigate hardware acceleration.
- **[nvidia-mig-support](https://github.com/truenas-community-sysexts/nvidia-mig-support)** — Nvidia GPU sysext with MIG (Multi-Instance GPU) support.

## Contributing

See [CONTRIBUTING.md](https://github.com/truenas-community-sysexts/.github/blob/main/CONTRIBUTING.md) for the org-wide quality bar, expectations around testing on real hardware, and our take on AI-assisted contributions.

Bug reports and feature requests go on the individual repo's issue tracker.

## License

All repos in this org are MIT-licensed unless explicitly noted otherwise in the repo itself.
