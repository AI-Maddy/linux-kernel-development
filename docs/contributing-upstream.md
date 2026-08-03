# :material-source-pull: Contributing Upstream

Kernel development is patch-based and mailing-list driven — one commit at a time, reviewed in public, not merged through pull requests.

Kernel development is patch-based and mailing-list driven rather than pull-request driven, even though many subsystems now also mirror trees on GitHub/GitLab for browsing.

## :material-format-list-numbered: The basic loop

!!! info "Start small"
    Pick a small, well-scoped change, such as a typo fix, a warning fix, or a small driver improvement. Make the change against a recent -next or maintainer tree rather than an old release.

!!! info "Explain why, not just what"
    Write a commit message that explains the motivation and impact of the change, not merely a restatement of the diff.

!!! success "Check style before sending"
    Run checkpatch.pl against your patch to catch style issues before anyone else sees it, then generate the patch and send it with git send-email to the relevant subsystem list and maintainer(s).

!!! success "Iterate on review"
    Respond to review feedback, send a v2/v3 if needed, and wait for the change to be picked up into a maintainer tree.

## :material-account-search: Finding maintainers and lists

The get_maintainer.pl script maps a changed file to the people and mailing lists responsible for it:

```bash
./scripts/get_maintainer.pl --file drivers/net/ethernet/example.c
```

Always CC the listed maintainers and lists directly — relying on a list archive alone is easy to miss.

## :material-message-text: Commit message conventions

The first line should be a short summary, prefixed with the affected subsystem, for example `net: fix off-by-one in ...`. The body should explain motivation and impact, wrapped at roughly 72 columns. A `Signed-off-by:` line, added automatically with `git commit -s`, certifies you have the right to submit the change under the Developer's Certificate of Origin.

## :material-account-group: Etiquette

Review feedback on kernel lists can be blunt and technical. Treat it as a discussion about the code, not a personal judgment, and keep patch series small so reviewers can reason about them quickly.

## :material-alert: Pitfalls

!!! warning "Basing a patch on an old release"
    Working against an old release tree instead of a current -next or maintainer tree often produces a patch that no longer applies cleanly, or duplicates work already done upstream.

!!! warning "Skipping get_maintainer.pl"
    Sending a patch to a generic list without CCing the maintainers found by get_maintainer.pl is one of the most common reasons a patch is ignored.

## :material-help-circle: Self-Test

=== "Question 1"
    What does `checkpatch.pl` catch, and when should you run it?

=== "Answer 1"
    Style issues in a patch — run it before sending, so reviewers see a clean patch instead of catching style problems for you.

=== "Question 2"
    What does a `Signed-off-by:` line certify, and how is it added?

=== "Answer 2"
    It certifies you have the right to submit the change under the Developer's Certificate of Origin; it's added automatically with `git commit -s`.

## :material-check-circle: Summary

- Kernel contributions are patches sent by email, reviewed on mailing lists — not pull requests.
- Start with a small, well-scoped change against a recent -next or maintainer tree.
- Use `get_maintainer.pl` to find who to CC, and `checkpatch.pl` to catch style issues first.
- Commit messages need a subsystem-prefixed summary line and a `Signed-off-by:` trailer.
- Expect blunt technical feedback — it's about the code, not you — and keep patch series small.

With a change accepted upstream, the last piece is knowing how to debug problems when things do not go as planned — covered next.
