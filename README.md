# Awesome Verified Agents [![Awesome](https://awesome.re/badge-flat2.svg)](https://awesome.re)

> Tools that produce **evidence** about what an AI agent actually did — not tools that hope it behaves.

An agent that reports its own success is a witness testifying about itself. This list collects the
projects that make that testimony checkable: gates that decide before an action runs, records that
cannot be quietly edited afterwards, checks that test an output against a source, and benchmarks
that put a number on reliability before you ship.

**The inclusion bar is one question: what artifact does it leave behind that a human can inspect
later?** A signed record, a pass/fail, a score, a diff, a trace, a blocked call. Tools that only
steer generation — better prompts, better instructions, "be careful" — are out of scope, however
useful they are.

---

## Contents

- [Runtime enforcement](#runtime-enforcement) — decides *before* the action happens
- [Evidence and attestation](#evidence-and-attestation) — records that survive the agent
- [Output verification](#output-verification) — is the claim actually supported?
- [Evaluation and benchmarks](#evaluation-and-benchmarks) — a number before you ship
- [Observability and tracing](#observability-and-tracing) — what happened, in order
- [Self-assessment](#self-assessment) — scoring your own setup
- [How the numbers here work](#how-the-numbers-here-work)
- [Contributing](#contributing)

---

## Runtime enforcement

Authorization lives outside the model loop: the model proposes, something else decides.

| Project | Evidence it produces | License | ★ | Last commit |
|---|---|---|---|---|
| [Adrian](https://github.com/secureagentics/Adrian) | Analyzes tool calls and reasoning traces in-flight; runs in audit or block mode, so each decision is a logged allow/deny | NOASSERTION | 496 | 2026-07-29 |
| [invariant](https://github.com/invariantlabs-ai/invariant) | Guardrails plus a trace-analysis tool for agent runs | Apache-2.0 | 437 | 2026-01-12 |
| [tenuo](https://github.com/tenuo-ai/tenuo) | Capability authorization engine: task-scoped warrants with cryptographic attenuation and offline verification — the warrant itself is the artifact | NOASSERTION | 77 | 2026-07-13 |
| [agent-browser-shield](https://github.com/pixiebrix/agent-browser-shield) | Browser extension, 35+ rules; masks secrets and strips injected instructions before the agent reads the page | NOASSERTION | 32 | 2026-08-01 |
| [TealTiger](https://github.com/agentguard-ai/tealtiger) | Policy enforcement and cost tracking with structured audit output (SARIF, JUnit XML, JSON) — machine-readable, so CI can fail on it | NOASSERTION | 16 | 2026-08-01 |
| [SourceryKit](https://github.com/ProvablyAI/sourcerykit) | Hooks the HTTP layer: logs every outbound call and blocks anything off the trusted-endpoint allowlist | NOASSERTION | 15 | 2026-07-28 |
| [Shani](https://github.com/kmori-source/shani) | Signed Authorized Decision Object per decision, with replay prevention and a human-in-the-loop approval path | NOASSERTION | 0 | 2026-06-25 |

## Evidence and attestation

Records designed so that a later reader can tell whether they were tampered with.

| Project | Evidence it produces | License | ★ | Last commit |
|---|---|---|---|---|
| [dos-kernel](https://github.com/anthony-chaudhary/dos-kernel) | Verifies an agent's "done" claim against git evidence instead of its self-report; audits commit claims against their own diffs | MIT | 18 | 2026-07-17 |
| [attestation-envelope-spec](https://github.com/TheColonyCC/attestation-envelope-spec) | A spec, not a tool: typed evidence pointers that structurally exclude self-signed assertions, content-hash pinning, ed25519 sigchains, plus a reference verifier | MIT | 0 | 2026-07-25 |
| [claude-consensus](https://github.com/Palo-Alto-AI-Research-Lab/claude-consensus) † | Cross-machine agreement protocol (propose / counter / accept / commit) with ACK discipline, so a multi-agent decision has a record independent of any one agent | MIT | 2 | 2026-08-01 |

## Output verification

Checking the claim against the source, rather than asking a model whether it looks fine.

| Project | Evidence it produces | License | ★ | Last commit |
|---|---|---|---|---|
| [guardrails](https://github.com/guardrails-ai/guardrails) | Validators that run over model output and return structured pass/fail per validator | Apache-2.0 | 7235 | 2026-07-29 |
| [NeMo Guardrails](https://github.com/NVIDIA-NeMo/Guardrails) | Programmable rails between the app and the model, evaluated per turn | NOASSERTION | 6850 | 2026-08-01 |
| [verbatim-citation-gate](https://github.com/Palo-Alto-AI-Research-Lab/verbatim-citation-gate) † | Deterministic first stage: every quoted span must appear verbatim in the retrieved context, so an invented quote fails with no model call; survivors go to a burden-of-proof judge. **Known defect:** the normalizer is Latin-only, see issue #1 | MIT | 3 | 2026-08-01 |
| [verdict-contract](https://github.com/Palo-Alto-AI-Research-Lab/verdict-contract) † | Turns an LLM reviewer's verdict into a process exit status (0 approve / 3 request-changes / 4 contract broken), with the prompt rule and the parser in one file so they cannot drift. Blocking wins from anywhere; approving requires the exact shape. 42 counterexample cases | MIT | 0 | 2026-08-04 |

## Evaluation and benchmarks

Putting a number on it before it reaches a user.

| Project | Evidence it produces | License | ★ | Last commit |
|---|---|---|---|---|
| [promptfoo](https://github.com/promptfoo/promptfoo) | Declarative assertions over prompts, agents and RAG, plus red-team runs — output is a scored matrix you can diff between versions | MIT | 23817 | 2026-08-01 |
| [openai/evals](https://github.com/openai/evals) | Eval framework and a registry of shared benchmarks | NOASSERTION | 19081 | 2026-04-14 |
| [deepeval](https://github.com/confident-ai/deepeval) | Metric suite for LLM and RAG outputs, runnable in a test suite | Apache-2.0 | 17321 | 2026-07-31 |
| [giskard-oss](https://github.com/Giskard-AI/giskard-oss) | Scans an LLM agent for failure classes and produces a report of found issues | Apache-2.0 | 5726 | 2026-07-31 |
| [inspect_ai](https://github.com/UKGovernmentBEIS/inspect_ai) | Evaluation framework from the UK AI Security Institute; solvers and scorers are explicit objects, so a result is reproducible from the eval definition | MIT | 2444 | 2026-07-31 |
| [AgentLeak](https://github.com/Privatris/AgentLeak) | Benchmark for privacy leakage in multi-agent systems across 7 channels including tool calls, RAG queries and inter-agent messages | NOASSERTION | 26 | 2026-07-01 |
| [ClawBench](https://github.com/TIGER-AI-Lab/ClawBench) | Five-layer execution evidence (replay, screenshots, HTTP traffic, browser actions and agent messages) plus interception results and task scores; it does not certify internal reasoning or real-world outcomes beyond the configured evaluator | Apache-2.0 | 541 | 2026-07-31 |
| [agent-runtime-integrity-bench](https://github.com/Palo-Alto-AI-Research-Lab/agent-runtime-integrity-bench) † | Deterministic fault-injection scenarios run against real SDKs, distilled from production incidents | MIT | 0 | 2026-08-01 |

## Observability and tracing

You cannot verify what you cannot see.

| Project | Evidence it produces | License | ★ | Last commit |
|---|---|---|---|---|
| [langfuse](https://github.com/langfuse/langfuse) | Traces, evals and metrics for LLM applications, self-hostable | NOASSERTION | 32278 | 2026-07-31 |
| [phoenix](https://github.com/Arize-ai/phoenix) | Observability and evaluation over recorded traces | NOASSERTION | 10850 | 2026-08-01 |
| [openllmetry](https://github.com/traceloop/openllmetry) | OpenTelemetry-based instrumentation, so agent traces land in the tooling you already run | Apache-2.0 | 7348 | 2026-07-13 |

## Self-assessment

Before buying anything: score what you already have.

| Project | Evidence it produces | License | ★ | Last commit |
|---|---|---|---|---|
| [Agent-Wiz](https://github.com/Repello-AI/Agent-Wiz) | Extracts the agent workflow from LangChain / LangGraph / CrewAI / AutoGen code and runs automated threat modeling over it | Apache-2.0 | 385 | 2025-11-02 |
| [agent-leash (LEASH-8)](https://github.com/Palo-Alto-AI-Research-Lab/agent-leash) † | 24-statement scored worksheet across 8 control domains, plus the plan-vs-authorize pattern and an approval-design checklist. Docs and templates, no runtime | MIT | 2 | 2026-08-01 |

---

## How the numbers here work

- **Stars and last-commit dates were read from the GitHub API on 2026-08-01.** They are a snapshot, not a live badge, and they will drift. If a row is wrong, that is a bug — open an issue.
- **Last commit is a column on purpose.** A list about verification should not hide the staleness of its own entries. Two rows above are more than six months cold; they stay because the work is still worth reading, and you can see the date and decide.
- **`NOASSERTION`** means GitHub could not resolve a standard SPDX identifier from the repo, not that the project is unlicensed. Check the repo before you depend on it.
- **†** marks a project maintained by the same lab that maintains this list. They follow the same inclusion bar as everything else, and they are the smallest entries here by star count — that is visible in the table rather than hidden.
- **No claim in this list is a benchmark result.** Every "evidence it produces" cell describes what the project says it does and what its code and docs show. Where a project's own numbers exist, follow its link — we do not restate performance claims we have not run.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). The short version: one project per PR, name the artifact it
leaves behind, and say honestly what it does not do. Copyright of your contribution stays yours.

---

<!--ecosystem-map:start-->

## 🧩 One piece of a working system

This repository is one piece lifted out of a live operation: one non-technical founder, an AI
cofounder, and a fleet of machines that reach consensus with each other and wake the human only
for money or the irreversible. It was extracted after it survived production, not written as a
demo — and it runs on its own: nothing here phones home to the rest.

**See how the whole thing fits together → [SYSTEM.md](https://github.com/tonydzi/Palo-Alto-AI-Research-Lab/blob/main/SYSTEM.md)**

Its closest neighbours in the **in public** layer: [`the-journey`](https://github.com/tonydzi/the-journey) · [`clawrush`](https://github.com/tonydzi/clawrush) · [`dashboards`](https://github.com/tonydzi/dashboards)

<!--ecosystem-map:end-->

## AI contributors

This project is built by a human + AI team, and the git log says so: Claude writes most of
the code, Codex and Grok review it, Gemini feeds the research. Each is credited on a commit
**only if its output changed that commit's content** — no decorative credits. Lab-wide
policy, one source for every repo: [AI-CONTRIBUTORS.md](https://github.com/Palo-Alto-AI-Research-Lab/.github/blob/main/AI-CONTRIBUTORS.md).
