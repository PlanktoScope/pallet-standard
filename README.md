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

You can clone this Forklift pallet to your PlanktoScope (or any computer acting as a Docker host)
using the [`forklift`](https://github.com/PlanktoScope/forklift) tool. For example, you can run any
one of the `forklift` CLI commands, depending on which release of this pallet you want:
```
// to clone and track the latest release of the edge branch:
forklift plt clone github.com/PlanktoScope/pallet-standard@edge
// to clone the v2023.9.0 release:
forklift plt clone github.com/PlanktoScope/pallet-standard@v2023.9.0
```

Then you can apply the cloned pallet on your PlanktoScope (or the Docker host you're running) using
the following `forklift` CLI command:
```
forklift plt apply
```

Warning: this will replace all Docker containers on your Docker host with the package deployments
specified by this pallet and delete any Docker containers not specified by this pallet's package
deployments.

### Layering

TBD

### Development

You should clone this Github repository to your local file system. For example, you can clone the
latest unstable version (on the `edge` branch) of the
[`github.com/PlanktoScope/pallet-standard`](https://github.com/PlanktoScope/pallet-standard) pallet
using the command:

```
git clone https://github.com/PlanktoScope/pallet-standard
```

Then you will need to download/install `forklift` in order to run its commands for development. For
more details and usage information, refer to the
[readme for Forklift](https://github.com/PlanktoScope/forklift#readme), especially the
["Work on a development pallet"](https://github.com/PlanktoScope/forklift#work-on-a-development-pallet)
section.

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
