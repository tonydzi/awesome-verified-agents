# Contributing

## The bar

One question decides every entry: **what artifact does this leave behind that a human can inspect
later?**

A signed record. A pass/fail. A score. A blocked call in a log. A diff between two runs. A trace.

Out of scope, however good: tools whose whole mechanism is steering generation — prompt libraries,
instruction packs, system-prompt collections, "safer" model wrappers with nothing to inspect
afterwards. There are excellent lists for those; this is not one of them.

Also out of scope: closed products with no public docs describing the artifact. If a reader cannot
tell what evidence comes out without a sales call, it does not belong here.

## What a PR should contain

- **One project.** Batches are harder to judge and harder to reverse.
- **The row**, in the format of the section you are adding to: project link, what evidence it
  produces, license, stars, last-commit date. Read the stars and date from the GitHub API on the
  day you submit; do not copy them from another list.
- **One sentence on what it does not do.** Every tool here has a boundary. Naming it is not a
  weakness in the PR, it is the reason the entry is trustworthy.
- **Section choice, with a reason.** If it plausibly fits two, say so and pick one.
- **Duplicate check.** Search the README for the project name and the repo URL, and say you did.

## What we will not do

- We will not accept an entry because it has a lot of stars. Stars are a column, not a criterion.
- We will not restate a project's performance claims as if this list had verified them. If you want
  numbers in your entry, link to the run that produced them.
- We will not quietly drop a project that goes cold. It keeps its row and its last-commit date, and
  the reader decides.

## Self-submissions

Submit your own project. Say that it is yours in the PR — that is all we ask. Maintainer-affiliated
entries in this list are marked with † and follow exactly the same bar, and this list's own
maintainers hold themselves to it in public.

## Your rights

Your copyright stays yours. There is no CLA here and there will not be one. Contributions go in
under the same MIT license as the rest of the repo, and we will not relicense your work into
something closed without asking you by name.

## What you get back

An answer within 48 hours — a merge, a specific objection, or a clear no. If a PR here sits silent
for longer than that, ping it; the silence is our bug, not your fault.
