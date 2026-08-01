# Getting Started

Before touching kernel code, set up a reliable development environment. This page covers the tools and habits that make kernel work manageable.

## Prerequisites

- A Linux host (native or a VM) with at least 20 GB free disk space
- - Familiarity with C, Makefiles, and git
  - - Packages: `build-essential`, `libncurses-dev`, `bison`, `flex`, `libssl-dev`, `libelf-dev`, `bc`
   
    - ## Getting the source
   
    - The canonical source lives in Linus Torvalds' tree, mirrored on kernel.org. For learning, clone a stable branch rather than `master`/`mainline` so the tree stays quiet while you experiment:
   
    - ```bash
      git clone --branch linux-6.6.y https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git
      cd linux
      ```

      ## Picking a starting configuration

      Use an existing config as a baseline instead of starting from nothing:

      ```bash
      make defconfig
      # or, to reuse your running system's config
      zcat /proc/config.gz > .config
      make olddefconfig
      ```

      ## Editor setup

      Most kernel developers use `ctags`/`cscope` or an LSP (`clangd`) generated from `compile_commands.json` (via the `scripts/clang-tools/gen_compile_commands.py` helper) to navigate the tree efficiently. Investing in cross-reference tooling pays off quickly given the size of the codebase.

      The next page looks at how the source tree is organized so this tooling has structure to navigate.
      
