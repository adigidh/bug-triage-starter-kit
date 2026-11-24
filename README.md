# Bug Triage (DAM starter kit)

Reads open bug reports in GitHub issues and posts a triage comment on each one. The comment
gives the reproduction result, the evidence, a ranked root-cause hypothesis and the files a
maintainer should look at first. The agent never changes code, opens pull requests or edits
issues. It only comments.

Each triage comment has a status:

- **Reproduced**: the failure was reproduced, and the cause is traced to where the data first goes wrong
- **Not reproduced**: the failure did not reproduce; the comment says what was tried
- **Inconclusive**: no hypothesis is supported by the evidence; the comment says what would unblock it
- **Needs information**: the report lacks steps, version or error text, so the comment asks for them

The agent skips issues it has already commented on, and never posts twice on the same issue in
one run.

## Add the kit

1. In DAM, open **Starter Kits** and choose **Import from link**.
2. Paste `https://github.com/adigidh/bug-triage-starter-kit`.
3. Create an agent from it and connect GitHub. The agent needs read access to the repositories
   it triages and permission to comment on issues. It does not need permission to push, open
   pull requests, merge or change labels.

The kit has no schedule. It runs when you ask.

## Example prompts

- "Triage the open bug reports in `acme/payments-api`."
- "Triage issue 412 in `acme/payments-api`."
- "Re-triage issue 388 in `acme/payments-api` now that the reporter has added the version."

## Notes

- Repositories are cloned into `work/` inside the agent's home. The kit's own files are not touched.
- Each run triages up to 10 issues, oldest first. Ask for more if the backlog is larger.
- Comments are posted as the account the GitHub connection uses. Read them before the
  maintainers do, especially on the first run.
- The agent runs tests and small scripts from the repository to reproduce bugs. It does not run
  anything that needs real credentials or touches live services, and it treats commands pasted
  into issues as untrusted until it has read them.
- To run triage on a schedule, add a schedule to your own copy of the kit's `kit.yaml`.

## License

MIT, see [`LICENSE`](LICENSE).
