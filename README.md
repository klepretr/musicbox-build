## MusicBox builder repository ##
This repository is used to build the yocto Linux distribution for MusicBox.
MusicBox is a Spotify server running on a Raspberry Pi Zero W

## Pre-requisites ##

This documentation supports Ubuntu 22.04 LTS version.
However command listed below should work with any recent debian-like Linux
distribution.

### git ###

From https://git-scm.com/:
Git is a free and open source distributed version control system designed to
 handle everything from small to very large projects with speed and efficiency.

To install git:

```bash
  $ sudo apt install git
```

For more informations: https://git-scm.com/

### Docker  ###

From https://docs.docker.com/get-started/overview/:
Docker is an open platform for developing, shipping, and running applications.

To install docker:

```bash
  $ sudo apt install docker.io
```

For more informations: https://www.docker.com/

### cqfd ###

From https://github.com/savoirfairelinux/cqfd:
cqfd provides a quick and convenient way to run commands in the current
directory, but within a Docker container defined in a per-project config file.

To install cqfd:

```bash
  $ git clone git@github.com:savoirfairelinux/cqfd.git
  $ cd cqfd/
  $ sudo make install
```

For more information: https://github.com/savoirfairelinux/cqfd

## Get the project ##

```bash
  $ git clone git@github.com:klepretr/musicbox-build.git
```

## Build cqfd docker image ##

This has to be done only once unless the Dockerfile is modified:

```bash
  $ cqfd init
```

## Configure the build ##

### Wifi setup ###
Create a file called `env.yml` based on `env.yml.template`

```bash
  $ cp env.yml.template env.yml
```

In the file `env.yml` set the two variables `WIFI_SSID` and `WIFI_PASSWORD` with your own configuration.

## Build project ##

To build MusicBox project:

```bash
  $ cqfd
```

## Advanced build setup ##

### Launch kas shell cqfd container ###

To help developing a shell kas with all bitbake environment can be start:

```bash
  $ cqfd run kas shell project.yml
```

## Flash project on target ##

The generated image is named 'musicbox-image-musicbox.wic.bz2'
It is generated in build directory:
```bash
  musicbox-build/build/tmp/deploy/images/musicbox/musicbox-image-musicbox.wic.bz2
```
You can flash the board using a dd command or using graphical tool as Balena Etcher (https://www.balena.io/etcher/)