# What are community sysexts?

Community-maintained [systemd-sysext](https://www.freedesktop.org/software/systemd/man/systemd-sysext.html) packages extend [TrueNAS](https://www.truenas.com/) with hardware support (drivers) and tooling (apps) that isn't shipped in the stock image, without modifying the immutable root filesystem. This allows us to support drivers and some application types to appear as installed without needing the system to have ever been put in developer mode. Its simple to remove sysexts in an emergency by deleting their symlinks. Though each sysext provided by this org has install and unistall tooling via scripts.

Each sysext lives in its own repo with its own install scripts, build pipeline, and release cadence.

The goal is to have a common tooling and approach so multiple community sysexts can be installed at any time.  We welcome contributions from all. 

This org will not create or distribute artefacts that contain non-open code or binaries.  If a sysext requires proriteray files then the nstall scripts will download neeed files automatically as permitted by the license you have with the vendor or let you provide binaries as per your license agreement with any vendor.

This project is not affilated with, or endorsed by ixsystems/truenas in anyway.

## Active sysexts provided by this org

- **[cli-tools](https://github.com/truenas-community-sysexts/cli-tools)** - Commonly requested CLI tools not included in TrueNas >25.x .
- **[coral-pcie-support](https://github.com/truenas-community-sysexts/coral-pcie-support)** - Google Coral PCIe TPU kernel modules (gasket/apex). Useful for Frigate hardware-accelerated object detection.
- **[hailo8-support](https://github.com/truenas-community-sysexts/hailo8-support)** - Hailo-8 AI accelerator driver and userspace tooling. Useful for Frigate hardware acceleration.
- **[nvidia-driver-support](https://github.com/truenas-community-sysexts/nvidia-driver-support)** - Install of multiple legacy and newer drivers in both open and proprietary flavours.
- **[nvidia-mig-support](https://github.com/truenas-community-sysexts/nvidia-mig-support)** - Enable nvidia MIG (Multi-Instance GPU) support for native TrueNAS Nvidia driver or other supported drivers.
- **[prometheus-exporters](https://github.com/truenas-community-sysexts/prometheus-exporters)** - Prometheus exporters (node, smartctl, nut, blackbox, snmp, ipmi) as systemd services.

## Related Projects

### NVIDIA GPU driver sysexts:

- [zzzhouuu/truenas-nvidia-drivers](https://github.com/zzzhouuu/truenas-nvidia-drivers) - Legacy GPU driver build framework with pre-built artifacts (GTX 700/900/10-series, Quadro M/P, Tesla M/P)
- [biohazardious/truenas-nvidia-driver-updater](https://github.com/biohazardious/truenas-nvidia-driver-updater) - Docker-automated sysext builder using a filesystem-diff approach
- [binary-person/truenas-nvidia-raw-builder](https://github.com/binary-person/truenas-nvidia-raw-builder) - Interactive install script with pre-built releases for multiple TrueNAS/NVIDIA version combos
- [oxc/truenas-nvidia-legacy](https://github.com/oxc/truenas-nvidia-legacy) - Dockerfile-based legacy driver builder with good depmod handling
- [Renari/truenas-legacy-nvidia-driver](https://github.com/Renari/truenas-legacy-nvidia-driver) - Minimal wrapper around truenas/scale-build for legacy nvidia.raw via CI
- [jbaznik/truenas-nvidia-drivers](https://github.com/jbaznik/truenas-nvidia-drivers) - Early legacy driver project with pre-built artifacts

### Not sysext, but related:

- [cbetti/truenas-coral-pcie-driver-helper](https://github.com/cbetti/truenas-coral-pcie-driver-helper) - Coral Edge TPU driver via DKMS

## Community sysext guide

New to building sysexts for TrueNAS? Check out the [community sysext guide](https://github.com/truenas-community-sysexts/.github/blob/main/docs/sysext-guide.md), which covers the TrueNAS-specific quirks of building, installing, and maintaining sysext packages.

## Contributing

See [CONTRIBUTING.md](https://github.com/truenas-community-sysexts/.github/blob/main/CONTRIBUTING.md) for the org-wide quality bar, expectations around testing on real hardware, and our take on AI-assisted contributions.

Bug reports and feature requests go on the individual repo's issue tracker.

## License

All repos in this org are MIT-licensed unless explicitly noted otherwise in the repo itself.
