# :material-linux: Linux Kernel Development

> Practical, original notes for engineers who want to understand and contribute to the Linux kernel.

This site collects original, practical notes for engineers who want to understand and contribute to the Linux kernel. It is organized as a progression: environment setup, kernel architecture, the build system, the upstream contribution process, and debugging tools.

The material assumes basic familiarity with C and the command line, but no prior kernel experience. Each section favors hands-on explanation over theory, with pointers to the authoritative in-tree documentation (`Documentation/` in the kernel source tree) for deeper dives.

!!! info "Who this is for"
    Engineers comfortable with C and git who want a guided path into kernel-level work, not just application development.

## :material-map: Site Map

<div class="grid cards" markdown>

- :material-rocket-launch: **[Getting Started](getting-started.md)**
  Set up a kernel development environment.
- :material-sitemap: **[Kernel Architecture](kernel-architecture.md)**
  Learn how the source tree and subsystems fit together.
- :material-hammer-wrench: **[Building the Kernel](building-the-kernel.md)**
  Configure, compile, and boot a custom kernel.
- :material-source-pull: **[Contributing Upstream](contributing-upstream.md)**
  Send patches the way the kernel community expects.
- :material-bug-check: **[Debugging Tools](debugging-tools.md)**
  Diagnose kernel bugs with printk, ftrace, and kgdb.
- :material-graph-outline: **[Memory Map](memory-map.md)**
  A one-page mindmap tying every topic together.
- :material-cards: **[Flashcards](flashcards.md)**
  Active-recall drill for key terms.

</div>

## What you will learn

By the end of this site you should understand how the kernel source tree is organized and how subsystems interact, how to configure, cross-compile, and boot a custom kernel, how kernel development workflow differs from typical application development (mailing lists, patches, maintainers), and how to use core debugging facilities such as printk, ftrace, and kgdb.

## How to use this site

Work through the pages in order if you are new to kernel development. If you already have experience, jump directly to the topic you need using the navigation menu.

!!! success "Study tip"
    Read a page, then immediately quiz yourself with the matching cards on the [Flashcards](flashcards.md) page. Active recall beats re-reading.

## :material-check-circle: Key Takeaways

- The kernel source tree follows consistent conventions: `arch/`, `drivers/`, `fs/`, `kernel/`, `mm/`, `net/`.
- Kernel development is patch- and mailing-list driven, not pull-request driven.
- A correct `.config` plus `make -j$(nproc)` is most of what building a kernel requires.
- printk, ftrace, and kgdb cover the large majority of day-to-day debugging needs.
- Use the [Memory Map](memory-map.md) and [Flashcards](flashcards.md) pages to reinforce what you read.
