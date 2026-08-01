# Contributing Upstream

Kernel development is patch-based and mailing-list driven rather than pull-request driven, even though many subsystems now also mirror trees on GitHub/GitLab for browsing.

## The basic loop

Start by picking a small, well-scoped change, such as a typo fix, a warning fix, or a small driver improvement. Make the change against a recent `-next` or maintainer tree rather than an old release, and write a commit message that explains *why*, not just *what*. Run `checkpatch.pl` against your patch to catch style issues before anyone else sees it, then generate the patch and send it with `git send-email` to the relevant subsystem list and maintainer(s). Finally, respond to review feedback, send a v2/v3 if needed, and wait for it to be picked up into a maintainer tree.

## Finding maintainers and lists

The `get_maintainer.pl` script maps a changed file to the people and mailing lists responsible for it:

```bash
./scripts/get_maintainer.pl --file drivers/net/ethernet/example.c
```

Always CC the listed maintainers and lists directly - relying on a list archive alone is easy to miss.

## Commit message conventions

The first line should be a short summary, prefixed with the affected subsystem, for example `net: fix off-by-one in ...`. The body should explain motivation and impact, wrapped at roughly 72 columns. A `Signed-off-by:` line, added automatically with `git commit -s`, certifies you have the right to submit the change under the Developer's Certificate of Origin.

## Etiquette

Review feedback on kernel lists can be blunt and technical. Treat it as a discussion about the code, not a personal judgment, and keep patch series small so reviewers can reason about them quickly.

With a change accepted upstream, the last piece is knowing how to debug problems when things do not go as planned - covered next.
