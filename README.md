# Beithar

(formerly "Heimdall")

## Description

This is the feed containing research packages created by and for researchers at Drexel University and University of California Riverside.  For example, the feed contains the package "syscall-sensors," a which includes a program that tracks and records a log of system calls made by processes running on OpenWrt routers.

As more programs are developed for router security (sensors, detectors, mitigators), they will be added to this feed in order to build a robust suite security software for routers.

As of 1/21/2016, the project supports OpenWrt routers running on ARM processor architecture.  With proper usage (see the OpenWrt documentation), the packages should cross compile to other architectures using OpenWrt's buildroot system, but everything in this feed should be considered to be at an alpha level of development at best; it is intended for private research and no support will be given.

## Usage

This repository is intended to provide additional, custom packages to the OpenWrt kernel.

To install OpenWrt's buildroot, follow the instructions here:

[OpenWrt Buildroot - Installation](http://wiki.openwrt.org/doc/howto/buildroot.exigence)

Once installed, navigate to your trunk directory (the root directory for your clone of the OpenWrt buildroot repository).

To enable this feed, open feeds.conf.default and add the following line (with the quotes removed):

'src-git beithar https://github.com/ronin-zero/beithar.git

Then execute the following commands (without quotes):

'./scripts/feeds update beithar'
'./scripts/feeds install beithar'

After confirming that this was successful, run menuconfig:

'make menuconfig'

Navigate to the packages you wish to enable through menuconfig and select to build them as modules or as a part of the kernel as your needs require.

## License

Other than members of this research project at Drexel University or University of California Riverside, use or duplication of this package or linked, original source code is not authorized and expressly not supported.
