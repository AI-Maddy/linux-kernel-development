# Contributing Upstream

Kernel development is patch-based and mailing-list driven rather than pull-request driven, even though many subsystems now also mirror trees on GitHub/GitLab for browsing.

## The basic loop

1. Pick a small, well-scoped change (a typo fix, a warning fix, a small driver improvement).
2. 2. Make the change against a recent `-next` or maintainer tree, not an old release.
   3. 3. Write a commit message that explains *why*, not just *what*.
      4. 4. Run `checkpatch.pl` against your patch to catch style issues before anyone else sees it.
         5. 5. Generate the patch and send it with `git send-email` to the relevant subsystem list and maintainer(s).
            6. 6. Respond to review feedback, send a v2/v3 if needed, and wait for it to be picked up into a maintainer tree.
              
               7. ## Finding maintainers and lists
              
               8. The `get_maintainer.pl` script maps a changed file to the people and mailing lists responsible for it:
              
               9. ```bash
                  ./scripts/get_maintainer.pl --file drivers/net/ethernet/example.c
                  ```

                  Always CC the listed maintainers and lists directly - relying on a list archive alone is easy to miss.

                  ## Commit message conventions

                  - First line: short summary, prefixed with the affected subsystem (e.g. `net: fix off-by-one in ...`)
                  - - Body: explain motivation and impact, wrapped at ~72 columns
                    - - `Signed-off-by:` line, added automatically with `git commit -s`, certifying you have the right to submit the change (the Developer's Certificate of Origin)
                     
                      - ## Etiquette
                     
                      - Review feedback on kernel lists can be blunt and technical. Treat it as a discussion about the code, not a personal judgment, and keep patch series small so reviewers can reason about them quickly.
                     
                      - With a change accepted upstream, the last piece is knowing how to debug problems when things do not go as planned - covered next.
                      - 
