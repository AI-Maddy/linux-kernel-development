# :material-hammer-wrench: Building the Kernel

Compiling a kernel is mostly about getting `.config` right — the `make` invocation itself is simple.

Compiling a kernel is mostly about configuration; the actual `make` invocation is simple once `.config` is correct.

## :material-cog-outline: Configuring

`make menuconfig` (ncurses UI) or `make xconfig` (Qt UI) let you browse and toggle thousands of options interactively. Options are grouped by subsystem and show help text with `?`.

For cross-compiling to an embedded target, set the toolchain prefix and target architecture:

```bash
export ARCH=arm64
export CROSS_COMPILE=aarch64-linux-gnu-
make menuconfig
```

## :material-play: Building

```bash
make -j$(nproc)
```

This produces `vmlinux` (the uncompressed ELF image, useful for debugging) and an architecture-specific bootable image such as `arch/x86/boot/bzImage` or `arch/arm64/boot/Image`.

## :material-puzzle: Building modules

Out-of-tree or in-tree modules can be built separately:

```bash
make modules
make modules_install INSTALL_MOD_PATH=/path/to/rootfs
```

## :material-power: Installing and booting

!!! warning "Always keep a fallback"
    On a test VM, copy the image and modules, update the bootloader entry (GRUB, extlinux, or U-Boot depending on target), and reboot. Keep the previous working kernel available as a fallback boot entry — a bad `.config` can otherwise leave a device unbootable.

## :material-speedometer: Iterating quickly

!!! success "Faster rebuild loop"
    `ccache` and `make -j` with a high parallelism count noticeably cut rebuild time. QEMU (`qemu-system-x86_64 -kernel arch/x86/boot/bzImage`) lets you boot-test changes in seconds without touching physical hardware.

## :material-alert: Pitfalls

!!! warning "No fallback kernel entry"
    Overwriting the only bootable kernel with an untested build is the single most common way to lock yourself out of a test machine. Always add, never replace, a boot entry.

!!! warning "Wrong CROSS_COMPILE prefix"
    A cross-build silently falling back to the host compiler produces a binary for the wrong architecture. Verify `${CROSS_COMPILE}gcc --version` resolves before running `make`.

## :material-help-circle: Self-Test

=== "Question 1"
    You need a kernel for an arm64 board built on an x86_64 host. Which two environment variables must be set before `make menuconfig`?

=== "Answer 1"
    `ARCH=arm64` and `CROSS_COMPILE=aarch64-linux-gnu-` (or the equivalent toolchain prefix).

=== "Question 2"
    Why boot-test with QEMU before flashing real hardware?

=== "Answer 2"
    QEMU lets you catch a kernel that fails to boot in seconds, without risking bricking physical hardware or losing access to a real device.

## :material-check-circle: Summary

- Configuration (`.config`) is the hard part; `make -j$(nproc)` itself is straightforward.
- Cross-compiling only needs `ARCH` and `CROSS_COMPILE` set correctly.
- `make modules` / `modules_install` build and stage kernel modules separately from the core image.
- Always keep a known-good fallback boot entry.
- QEMU gives a fast, safe boot-test loop before touching real hardware.

With a working build loop in place, the next page covers how changes actually get proposed and merged upstream.
