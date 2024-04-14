# pallet-standard
The standard configuration of Forklift package deployments for PlanktoScopes

## Introduction

pallet-standard is a [Forklift](https://github.com/PlanktoScope/forklift) pallet specifying the
standard configuration of Forklift package deployments for the PlanktoScope software distribution.

## Usage

### Deployment

This Github repository has three release channels, each corresponding to a Git branch: `stable`,
`beta`, and `edge`, as well as Git tags for each released version. You should probably use either
the `stable` branch (recommended so that you will automatically be notified for new stable versions)
or a specific Git tag.

You can clone and stage this Forklift pallet to be applied to your PlanktoScope using the
[`forklift`](https://github.com/PlanktoScope/forklift) tool. For example, you can run any
of the following `forklift` CLI commands, depending on which release of this pallet you want:
```
// to clone the latest development (unstable) version of the edge branch:
forklift plt switch github.com/PlanktoScope/pallet-standard@edge
// to clone the latest beta or stable (pre-)release of the edge branch:
forklift plt switch github.com/PlanktoScope/pallet-standard@beta
// to clone the latest stable release of the edge branch:
forklift plt switch github.com/PlanktoScope/pallet-standard@stable
// to clone the v2023.9.0 release:
forklift plt switch github.com/PlanktoScope/pallet-standard@v2023.9.0
```

Afterwards, your pallet will be staged to be applied the next time your PlanktoScope boots up. To
apply your changes, you just need to reboot your PlanktoScope. Warning: when you reboot your
Planktoscope, Forklift will replace all Docker containers on your Docker host according to the
package deployments specified by this pallet and delete any Docker containers not specified by this
pallet's package deployments. Forklift will also update your OS's configuration files according to
the package deployments specified by this pallet - though if you've manually made changes to any
OS configuration files which overlap with files provided by this pallet, your manually-changed
versions of those files will completely override this pallet's versions of those files (see TBD for
more information).

### Layering

TBD

### Development

You should clone this Github repository to your local file system (on either your PlanktoScope's
embedded computer or another computer). For example, you can clone the latest unstable version (on
the `edge` branch) of this pallet using the command:

```
git clone https://github.com/PlanktoScope/pallet-standard
```

Then you will need to download/install `forklift` in order to run its commands for development. For
more details and usage information, refer to the
[readme for Forklift](https://github.com/PlanktoScope/forklift#readme), especially the
["Work on a development pallet"](https://github.com/PlanktoScope/forklift#work-on-a-development-pallet)
section of that readme's usage instructions. If you are performing development tasks on your
PlanktoScope, `forklift` is already installed for you.

The most common routine maintenance task will be to upgrade the version of the
[`github.com/PlanktoScope/device-pkgs`](https://github.com/PlanktoScope/device-pkgs) repository used
by this pallet. You can do that using a command like the following:

```
forklift dev --cwd {path to your local copy of the pallet for development} plt add-repo github.com/PlanktoScope/device-pkgs@{version to upgrade to}
```

If you are your PlanktoScope's embedded computer to perform development tasks and you want to
immediately test changes to the Docker apps provided by the your local development copy of this
pallet, you can run:

```
forklift dev --cwd {path to your local copy of the pallet for development} plt apply
```

Note: any changes made to your OS's configuration files in `/etc` and `/var` will only take effect
the next time you boot up your PlanktoScope - to test those changes, reboot your PlanktoScope.

## Licensing

Forklift packages deployed by this pallet have their own software licenses, as specified in the
Forklift repositories where those packages are published. Any source code provided with this
Forklift pallet is covered by the following information, except where otherwise indicated:

Copyright Ethan Li and PlanktoScope project contributors

SPDX-License-Identifier: Apache-2.0 OR BlueOak-1.0.0

You can use the source code provided here either under the
[Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0)
or under the [Blue Oak Model License 1.0.0](https://blueoakcouncil.org/license/1.0.0);
you get to decide. We are making the software available under the Apache license because it's
[OSI-approved](https://writing.kemitchell.com/2019/05/05/Rely-on-OSI.html),
but we like the Blue Oak Model License more because it's easier to read and understand.
