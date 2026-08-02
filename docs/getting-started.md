# :material-rocket-launch: Getting Started

> Set up a reliable development environment before touching kernel code — most early pain comes from environment problems, not the code itself.

Before touching kernel code, set up a reliable development environment. This page covers the tools and habits that make kernel work manageable.

## :material-format-list-checks: Prerequisites

!!! info "What you need"
    A Linux host (native or a VM) with at least 20 GB free disk space, familiarity with C, Makefiles, and git, and these packages: `build-essential`, `libncurses-dev`, `bison`, `flex`, `libssl-dev`, `libelf-dev`, `bc`.

## :material-source-branch: Getting the source

The canonical source lives in Linus Torvalds' tree, mirrored on kernel.org. For learning, clone a stable branch rather than master/mainline so the tree stays quiet while you experiment.

```bash
git clone --branch linux-6.6.y https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git
cd linux
```

!!! success "Save time"
    Clone with `--depth 1` if you only need the latest commit on a stable branch; it downloads much faster than a full history clone.

## :material-cog: Picking a starting configuration

Use an existing config as a baseline instead of starting from nothing. Running `make defconfig` gives a sane architecture default. Alternatively, reuse your running system's config:

```bash
zcat /proc/config.gz > .config
make olddefconfig
```

## :material-file-code: Editor setup

Most kernel developers use ctags or cscope, or an LSP such as clangd generated from `compile_commands.json` (via the `scripts/clang-tools/gen_compile_commands.py` helper), to navigate the tree efficiently. Investing in cross-reference tooling pays off quickly given the size of the codebase.

## :material-alert: Pitfalls

!!! warning "Don't start from mainline"
    Developing against a moving master/mainline branch means the tree under you keeps changing. Pin a stable `-y` branch while learning.

!!! warning "Skipping olddefconfig"
    Reusing an old `.config` without running `make olddefconfig` first can leave new kernel options unset, causing confusing build or boot failures.

## :material-help-circle: Self-Test

=== "Question 1"
    Why clone a stable branch instead of mainline when learning?

=== "Answer 1"
    Mainline changes constantly; a stable branch stays quiet, so build/boot problems you hit are more likely caused by you, not upstream churn.

=== "Question 2"
    What does `make olddefconfig` do, and why run it after copying an old `.config`?

=== "Answer 2"
    It fills in any kernel options that are new since the old config was generated, using their defaults, so the build doesn't fail or silently omit new features.

## :material-check-circle: Summary

- Use a native or VM Linux host with the standard kernel build packages installed.
- Clone a stable `-y` branch, optionally with `--depth 1`, rather than mainline.
- Start from `make defconfig` or an exported `/proc/config.gz`, then run `make olddefconfig`.
- Set up ctags/cscope or clangd via `compile_commands.json` before diving into the source tree.

The next page looks at how the source tree is organized so this tooling has structure to navigate.
