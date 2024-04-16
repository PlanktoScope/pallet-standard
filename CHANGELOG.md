# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project uses [Calendar Versioning](https://calver.org/) with a `YYYY.minor.patch` scheme.
All dates in this file are given in the [UTC time zone](https://en.wikipedia.org/wiki/Coordinated_Universal_Time).

## Unreleased

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

- (Breaking change) The minimum supported Forklift version for using this repository has been bumped from v0.4.0 to v0.7.0-alpha.3, because some packages provided by this repository now require functionality added by v0.7.0 (namely, file-exporting functionality) in order to work as described/expected.
- (Breaking change) Deployment `host/planktoscope/machine-name` has been renamed to `host/machine-name`.

### Removed

- Deployment `apps/cockpit/deploy.yml` no longer has a resource dependency on a fileset involving `/etc/cockpit/cockpit.conf`.

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
