# Getting Started

Before touching kernel code, set up a reliable development environment. This page covers the tools and habits that make kernel work manageable.

## Prerequisites

You will need a Linux host (native or a VM) with at least 20 GB free disk space, familiarity with C, Makefiles, and git, and the following packages: build-essential, libncurses-dev, bison, flex, libssl-dev, libelf-dev, and bc.

## Getting the source

The canonical source lives in Linus Torvalds' tree, mirrored on kernel.org. For learning, clone a stable branch rather than master/mainline so the tree stays quiet while you experiment. For example: `git clone --branch linux-6.6.y https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git` followed by `cd linux`.

## Picking a starting configuration

Use an existing config as a baseline instead of starting from nothing. Running `make defconfig` gives a sane architecture default. Alternatively, reuse your running system's config with `zcat /proc/config.gz > .config` followed by `make olddefconfig` to fill in any new options with defaults.

## Editor setup

Most kernel developers use ctags or cscope, or an LSP such as clangd generated from compile_commands.json (via the scripts/clang-tools/gen_compile_commands.py helper), to navigate the tree efficiently. Investing in cross-reference tooling pays off quickly given the size of the codebase.

The next page looks at how the source tree is organized so this tooling has structure to navigate.


!!! tip "Save time"
    Clone with `--depth 1` if you only need the latest commit on a stable branch; it downloads much faster than a full history clone.
