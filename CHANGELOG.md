# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project uses [Calendar Versioning](https://calver.org/) with a `YYYY.minor.patch` scheme.
All dates in this file are given in the [UTC time zone](https://en.wikipedia.org/wiki/Coordinated_Universal_Time).

## v2024.0.0-beta.2 - 2024-09-19

### Added

- Added a `host/prepare-custom-image` package to export a script to `/usr/libexec/prepare-custom-image` for resetting the filesystem and shutting down the machine in preparation for cloning the filesystem as an SD card image.
- Added experimental feature flags for other pallets to reference when importing files from this pallet.

### Changed

- Deployment `apps/grafana` now tries to limit Grafana's CPU usage to one core.

## v2024.0.0-beta.1 - 2024-06-24

### Changed

- The Docker container image has been bumped to the latest version for the `apps/ps/device-portal`, to remove a deprecation notice for the `planktoscope.local` hostname (as that hostname is being un-deprecated for v2024.0.0).

## v2024.0.0-beta.0 - 2024-06-07

### Added

- Deployment `host/machine-name` now exports a `machine-name` binary built for the appropriate CPU architecture target.

### Changed

- The Docker container image has been bumped to the latest version for the `apps/ps/device-portal`, to fix some broken links and remove the links to Portainer (whose inclusion in the default PlanktoScope OS images is deprecated for v2024.0.0 of PlanktoScope OS).
- Docker container images have been bumped to the latest version for filebrowser-related package deployments.

## v2024.0.0-alpha.2 - 2024-04-25

### Added

- Deployment `apps/cockpit` now exports a drop-in config file for reverse-proxying (see the notes on additions to `core/host/cockpit`)
- Deployment `apps/ps/node-red-dashboard` now exports more config files needed for the Node-RED dashboard.
- Deployment `host/cockpit` now exports system services to automatically generate a Cockpit config file from drop-in config file fragments, and various drop-in config files for Cockpit.
- Deployment `host/dnsmasq` now exports system services to automatically generate a dnsmasq drop-in config file from drop-in config file templates.
- Added a `host/docker` deployment which exports an override to the default systemd `docker.service`.
- Deployment `host/networking/autohotspot` now exports everything needed for autohotspot functionality.
- Deployment `host/networking/dhcpcd` now exports an override to the default systemd `dhcpcd.service`.
- Deployment `host/networking/dnsmasq` now exports various drop-in config files for dnsmasq.
- Deployment `host/networking/hostapd` now exports a default basic config file for hostapd.
- Deployment `host/networking/hosts` now exports system services to automatically generate a hosts file from drop-in hosts file fragments.
- Deployment `host/networking/interface-forwarding` now exports everything needed for interface-forwarding functionality.
- Deployment `host/planktoscope/gpio-init` now exports everything needed for GPIO-initialization functionality.
- Deployment `host/planktoscope/gpsd` now exports all config files needed to support the GPS module (still no guarantee whether the files are actually correct, though!).
- Deployment `host/planktoscope/machine-name` now exports everything needed for automatically updating machine name-related configurations (machine name, hostname, SSID, Cockpit configuration).
- Deployment `host/sshd` now enables the system-provided `ssh.service` and adds & enables a service which automatically regenerates host keys for the SSH server if no host keys exist at boot.

### Changed

- (Breaking change) Previously, the default behavior of the segmenter deployed by `apps/ps/backend/proc-segmenter` was to subtract consecutive masks to try to mitigate image-processing issues with objects which get stuck to the flowcell during imaging. However, when different objects occupied the same space in consecutive frames, the subtraction behavior would subtract one object's mask from the mask of the other object in the following frame, which would produce clearly incorrect masks. This behavior is no longer enabled by default; in order to re-enable it, you should enable the `pipeline-subtract-consecutive-masks` feature flag in the package deployment.
- (Breaking change) The minimum supported Forklift version for using this repository has been bumped from v0.4.0 to v0.7.0, because some packages provided by this repository now require functionality added by v0.7.0 (namely, file-exporting functionality) in order to work as described/expected.
- (Breaking change) Deployment `host/planktoscope/machine-name` has been renamed to `host/machine-name`.
- Docker container images have been bumped to newer versions for almost all package deployments.
- Deployment `apps/cockpit/deploy.yml` no longer has a resource dependency on a fileset involving `/etc/cockpit/cockpit.conf`.
- Deployment `host/networking/interface-forwarding` has a slightly simpler network configuration, and now all packets for the PlanktoScope's static IP addresses (e.g. 192.168.4.1, 192.168.5.1, 192.168.6.1, etc.) are routed to 127.0.0.1 regardless of whether the packet for that IP address came from the interface corresponding to it.

### Deprecated

- Deployment `apps/portainer` will no longer be enabled by default after v2024.0.0. This is because it requires inclusion of a relatively large Docker container image in the PlanktoScope OS's SD card image (which is constrained to be up to 2 GB in size so that it can be attached as an upload to GitHub Releases), and because it has an annoying first-time user experience (i.e. that a password must be set within a few minutes of boot, or else the Portainer container must be restarted), and because Dozzle already provides all the basic functionalities needed by most users, and because Portainer has never actually been used for troubleshooting within the past year of the project.

### Removed

- Deployment `host/exim` was removed because it was useless and is no longer relevant.

## v2024.0.0-alpha.1 - 2024-03-26

### Added

- Added deployments for a few new packages which only describe assumptions about files provided by the host.

### Changed

- Upgraded packages so that some now require certain files to be provided by the host.

### Fixed

- The container created by deployment `apps/ps/backend/proc-segmenter` now runs as the `root` user, so that it correctly handles root directories created on the host by `apps/ps/backend/controller`.

## v2024.0.0-alpha.0 - 2024-02-06

### Added

- Deployment for Dozzle as a Docker container log viewer.
- Deployments for Prometheus metrics monitoring.
- Deployments for various scripts - and a few config files - to make available for running on the host.

### Changed

- Deployment `apps/ps/backend/proc-segmenter` now deploys the segmenter as a Docker container instead of assuming it's available on the host.

## v2023.9.0 - 2023-12-30

(this release involves no changes from v2023.9.0-beta.2; it's just a promotion of v2023.9.0-beta.2 to a stable release)

## v2023.9.0-beta.2 - 2023-12-02

### Changed

- (Breaking change) Updated files for use with v0.4.0 of the Forklift tool. Previous versions must be used with forklift v0.3.

### Removed

- The hardware setup guides are no longer included by default in the offline docs site, to reduce the size of the PlanktoScope SD card images.

## v2023.9.0-beta.1 - 2023-09-14

### Changed

- Upgraded github.com/PlanktoScope/device-pkgs repository from v2023.9.0-beta.0 to v2023.9.0-beta.1

## v2023.9.0-beta.0 - 2023-09-02

### Added

- Packages for host resources.

### Changed

- (Breaking change) Updated files for use with v0.3.1 of the Forklift tool. Previous versions must be used with forklift v0.1.
- (Breaking change) Reorganized packages with a directory tree structure.
- Upgraded various Docker images.

## v2023.9.0-alpha.0 - 2023-05-30

### Added

- Basic repository and package deployment configuration for the v2023.9.0 release
