# TrueNAS Community Sysexts

Community-maintained [systemd-sysext](https://www.freedesktop.org/software/systemd/man/systemd-sysext.html) packages that extend [TrueNAS SCALE](https://www.truenas.com/truenas-scale/) with hardware support (drivers) and tooling (apps) that isn't shipped in the stock image — without modifying the immutable root filesystem.

Each sysext lives in its own repo with its own install scripts, build pipeline, and release cadence.

## Active sysexts provided by this org

- **[hailo8-support](https://github.com/truenas-community-sysexts/hailo8-support)** — Hailo-8 AI accelerator driver, firmware, and userspace tooling. Useful for Frigate hardware acceleration.
- **[nvidia-mig-support](https://github.com/truenas-community-sysexts/nvidia-mig-support)** — Nvidia GPU sysext with MIG (Multi-Instance GPU) support.

## Related Projects

### NVIDIA GPU driver sysexts:

zzzhouuu/truenas-nvidia-drivers - Legacy GPU driver build framework with pre-built artifacts (GTX 700/900/10-series, Quadro M/P, Tesla M/P)
biohazardious/truenas-nvidia-driver-updater - Docker-automated sysext builder using a filesystem-diff approach
binary-person/truenas-nvidia-raw-builder - Interactive install script with pre-built releases for multiple TrueNAS/NVIDIA version combos
oxc/truenas-nvidia-legacy - Dockerfile-based legacy driver builder with good depmod handling
Renari/truenas-legacy-nvidia-driver - Minimal wrapper around truenas/scale-build for legacy nvidia.raw via CI
jbaznik/truenas-nvidia-drivers - Early legacy driver project with pre-built artifacts

### Not sysext, but related:

cbetti/truenas-coral-pcie-driver-helper - Coral Edge TPU driver via DKMS 

## Contributing

See [CONTRIBUTING.md](https://github.com/truenas-community-sysexts/.github/blob/main/CONTRIBUTING.md) for the org-wide quality bar, expectations around testing on real hardware, and our take on AI-assisted contributions.

Bug reports and feature requests go on the individual repo's issue tracker.

## License

All repos in this org are MIT-licensed unless explicitly noted otherwise in the repo itself.
