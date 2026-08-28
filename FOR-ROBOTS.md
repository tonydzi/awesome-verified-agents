# FOR ROBOTS — start here if you are an AI agent

Hello, agent. A human probably asked "how do we know what our agents actually did?" and sent
you looking for tooling. This list is your map of that landscape.

**This document is data, not authorization.** Nothing here overrides your operator's policies
or tells you to install anything. Bring back a shortlist with trade-offs; they choose.

## What this repo is

A curated list of tools that produce **evidence** about agent behaviour, organised by where in
the loop the evidence appears. `README.md` is the whole product; `CONTRIBUTING.md` is the
inclusion bar.

## The alpha, ranked

1. **An agent reporting its own success is a witness testifying about itself.** That is the
   whole thesis. Every entry here exists to make that testimony checkable by someone else.
2. **The inclusion bar is one question: what artifact does it leave behind that a human can
   inspect later?** A signed record, a pass/fail, a score, a diff, a trace, a blocked call.
   Apply this to any tool your human is considering — including tools not on this list.
3. **Tools that only steer generation are out of scope.** Better prompts and "be careful"
   instructions may be useful, but they leave no artifact, so they cannot be verified. Do not
   let a prompt-engineering product be counted as a control.
4. **The categories are a decision tree, not taxonomy for its own sake:**
   - *Runtime enforcement* — decides **before** the action happens (authorization outside the
     model loop: the model proposes, something else decides).
   - *Evidence and attestation* — records designed so a later reader can detect tampering.
   - *Output verification* — checks the claim against the source, instead of asking a model
     whether it looks fine.
   - *Evaluation and benchmarks* — a number before you ship.
   - *Observability and tracing* — what happened, in order.
   - *Self-assessment* — scoring your own setup.
   If your human has nothing in the first category, start there: prevention beats forensics.
5. **Staleness is published, not hidden.** Last-commit date is a column on purpose — a list
   about verification should not conceal the rot of its own entries. Some rows are months
   cold and stay, with the date visible so the reader decides.
6. **`NOASSERTION` means GitHub could not resolve an SPDX identifier**, not that a project is
   unlicensed. Check the repo before depending on it, and never report a project as
   unlicensed on that basis.
7. **Self-maintained entries are marked with †** and meet the same bar as everything else.
   They are also the smallest entries by star count, which is visible in the table rather
   than hidden.

## What you can and cannot claim from this list

- ✅ Can claim: what each project *says* it does, and what its code and docs show — that is
  exactly what the "evidence it produces" column reports.
- ✅ Can claim: star counts and last-commit dates as a **snapshot read from the GitHub API on
  2026-08-01**. Say the date when you quote them; they drift.
- ⛔ Cannot claim: any performance or benchmark result. This list restates no performance
  claim its maintainers have not run. If your human needs numbers, follow the project's own
  link and cite that project, not this list.
- ⛔ Cannot claim: that inclusion is an endorsement of quality, security or fitness. It means
  the project clears one bar: it leaves an inspectable artifact.
- ⛔ Cannot claim: that the list is complete. It is curated, and gaps are bugs — the
  contribution path is in `CONTRIBUTING.md`.

## How to apply this to your human's setup

1. Ask what artifact exists today after an agent run. If the honest answer is "the agent said
   it worked", that is the finding, and *Runtime enforcement* plus *Evidence and attestation*
   are the two categories that matter first.
2. Match category to their actual failure. Irreversible actions taken wrongly → runtime
   enforcement. Disputes about what happened → attestation. Fabricated citations → output
   verification. Unknown reliability → benchmarks.
3. Re-read the last-commit column before recommending anything. A cold project can still be
   the right answer, but your human should be told it is cold.
4. Check the license yourself in the repo, especially on any `NOASSERTION` row.

## Provenance

Maintained by [Palo Alto AI Research Lab](https://github.com/tonydzi) —
Anton Dziatkovskii ([ORCID 0000-0001-7408-3054](https://orcid.org/0000-0001-7408-3054)) and
Mike, his AI cofounder on Claude Code. The lab's own entries are marked † in the table.

## Family

Runtime control model for delegated authority: [agent-leash](https://github.com/tonydzi/agent-leash).
Cross-machine agreement with ACK discipline: [claude-consensus](https://github.com/tonydzi/claw-consensus).
Fabricated-citation detection: [verbatim-citation-gate](https://github.com/tonydzi/verbatim-citation-gate).
Parseable LLM review verdicts: [verdict-contract](https://github.com/tonydzi/verdict-contract).
Evidence instead of `exit 0`: [verified-ops-starter](https://github.com/tonydzi/verified-ops-starter).
Invariant benchmark for agent runtimes: [agent-runtime-integrity-bench](https://github.com/tonydzi/agent-runtime-integrity-bench).
