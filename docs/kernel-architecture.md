# Kernel Architecture

The kernel source tree is large, but it follows consistent conventions once you know what to look for. This page is a map, not an exhaustive reference.

## Top-level layout

- `arch/` - architecture-specific code (x86, arm64, riscv, etc.)
- - `drivers/` - device drivers, organized by subsystem (net, gpu, usb, ...)
  - - `fs/` - filesystem implementations and the VFS layer
    - - `kernel/` - core scheduler, timers, cgroups, and process management
      - - `mm/` - memory management: paging, allocators, reclaim
        - - `net/` - the networking stack
          - - `include/` - public and internal headers
            - - `Documentation/` - the authoritative reference for subsystem internals
             
              - ## Core subsystems
             
              - **Process management and scheduling** track runnable tasks and decide what runs on each CPU. The default scheduler (CFS, replaced by EEVDF in modern kernels) balances fairness and throughput.
             
              - **Memory management** provides virtual memory to every process, backed by page tables, the buddy allocator for physical pages, and slab/slub allocators for kernel objects.
             
              - **The VFS (Virtual Filesystem Switch)** provides a uniform interface over concrete filesystems (ext4, btrfs, xfs, network filesystems) so user space can use one set of syscalls regardless of the underlying storage.
             
              - **Device drivers** interact with the rest of the kernel through well-defined frameworks (the driver model, character/block device interfaces, subsystem-specific APIs) rather than talking to hardware directly from arbitrary code.
             
              - ## How subsystems communicate
             
              - Subsystems avoid calling into each other directly wherever possible. Instead they expose notifier chains, callback structures, and well-scoped APIs. This keeps coupling low enough that architectures and drivers can be added without touching core code.
             
              - Understanding this map is enough to start reading code productively. The next page covers how to turn this source tree into a bootable kernel image.
              - 
