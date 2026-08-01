# Linux Kernel Development

Original documentation covering Linux kernel development: environment setup, kernel architecture, the build system, upstream contribution workflow, and debugging tools. Built as a static site with MkDocs (https://www.mkdocs.org/) and the Material theme (https://squidfunk.github.io/mkdocs-material/).

## Contents

See the docs/ folder: index.md (home), getting-started.md, kernel-architecture.md, building-the-kernel.md, contributing-upstream.md, and debugging-tools.md.

## Building the site locally

```bash
pip install mkdocs-material
mkdocs serve
```

Then open http://127.0.0.1:8000 in a browser. To produce a static build for hosting, e.g. GitHub Pages:

```bash
mkdocs build
```

## License

Original content written for this project. Not affiliated with or copied from any third-party training provider.
