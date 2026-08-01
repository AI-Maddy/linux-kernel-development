# Building the Kernel

Compiling a kernel is mostly about configuration; the actual `make` invocation is simple once `.config` is correct.

## Configuring

`make menuconfig` (ncurses UI) or `make xconfig` (Qt UI) let you browse and toggle thousands of options interactively. Options are grouped by subsystem and show help text with `?`.

For cross-compiling to an embedded target, set the toolchain prefix and target architecture:

```bash
export ARCH=arm64
export CROSS_COMPILE=aarch64-linux-gnu-
make menuconfig
```

## Building

```bash
make -j$(nproc)
```

This produces `vmlinux` (the uncompressed ELF image, useful for debugging) and an architecture-specific bootable image such as `arch/x86/boot/bzImage` or `arch/arm64/boot/Image`.

## Building modules

Out-of-tree or in-tree modules can be built separately:

```bash
make modules
make modules_install INSTALL_MOD_PATH=/path/to/rootfs
```

## Installing and booting

On a test VM, copy the image and modules, update the bootloader entry (GRUB, extlinux, or U-Boot depending on target), and reboot. Keep the previous working kernel available as a fallback boot entry - a bad `.config` can otherwise leave a device unbootable.

## Iterating quickly

For rapid iteration, `ccache` and `make -j` with a high parallelism count noticeably cut rebuild time. QEMU (`qemu-system-x86_64 -kernel arch/x86/boot/bzImage`) lets you boot-test changes in seconds without touching physical hardware.

With a working build loop in place, the next page covers how changes actually get proposed and merged upstream.
