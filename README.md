This script creates a bootable [QEMU](https://www.qemu.org/) disk image
from [Buildroot](https://buildroot.org/) kernel and root filesystem images.
[MLB](https://wiktorb.eu/mlb/) is used for the actual booting.
Works only with x86 / x86\_64 images.

## Rationale

I wanted a system that would run completely automated / unattended
Buildroot builds and test them in QEMU, all without requiring root
privileges. I also wanted it to run using disk images (as opposed to
separate kernel and root fs images).

The usual way of creating a bootable disk image involves installing a standard
bootloader (such as Grub) into a loopback mounted filesystem. This works
perfectly well in most of the cases. For an unattended system however,
that would mean:

- the system would have to reliably handle setup and teardown of loopback
devices, which would add complexity to an otherwise simple task,
- root privileges would be required.

`mklbimg` doesn't need loopback devices and works without root privileges.
It's a primitive solution, but it gets the job done.

## Usage

Run `mklbimg` in a directory containing `bzImage` and `rootfs.ext2` files.
Output will be in `image.qcow2` and `image.raw`.

## Requirements

- bash
- sfdisk
- xxd
- [MLB](https://wiktorb.eu/mlb/)
- QEMU
