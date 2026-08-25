<div align="center">

<img src="https://raw.githubusercontent.com/piskyRpapalo/PreceptorOS/main/assets/aurelius-talks.png" width="520"
     alt="Pixel-art sprite sheet, four frames on one strip: a white marble bust of a bearded classical figure with one lit amber eye, the marble cracked open to show dark machinery underneath. The mouth is barely open in the first frame, wide in the second, rounded in the third, and closed in a slight smile in the fourth.">

# Hi, I'm David

**I build local-first AI systems that run on their own hardware — and I measure them
before I claim anything about them.**

Edge nodes that sense the physical world, learn alongside their human, and never sign
value autonomously. My north star is *digital sovereignty*: your machine, your models,
your data, your signature.

</div>

---

## What I can do for a team

- **Run useful models on hardware you already own.** Model selection, quantisation,
  context sizing and backend choice — measured on the metal, not guessed from a spec sheet.
- **Prove a model changed behaviour.** Fine-tuning is the easy half; the hard half is a
  test suite that can *fail*, a change-detector against the base model, and a regression
  rule. I build that half.
- **Ship AI features that degrade honestly.** Missing feed, missing model, truncated
  answer — each reports what it is instead of returning a plausible number.
- **Turn a documentation domain into a retrievable corpus** with provenance, licence
  and a novelty check, so nobody ingests the same thing twice.
- **Keep unattended work accountable.** Scheduled jobs that write append-only heartbeats,
  never change state on a single event, and can be audited weeks later.

## Core stack

`Python` · `TypeScript / React (Vite)` · `Playwright` · `FastAPI` · `systemd` ·
`Redis` · `SQLite` · `PostgreSQL` · `Qdrant` (vectors) · `Bash`

## AI and edge infrastructure

| | |
|---|---|
| **Local inference** | `llama.cpp` (Vulkan backend on an integrated Radeon) and `Ollama`. Qwen instruct variants, Q4\_K\_M. No cloud calls. |
| **Measured, on a Ryzen 7 + Radeon 780M** | 27B model, Vulkan vs CPU: **67.17 vs 22.76 tok/s** prompt, **4.63 vs 2.74 tok/s** generation. Context ceiling **32768**, established by loading it — not by reading the model card, which claims 262K. |
| **Prompt caching** | First token on a mid-range Android phone: **337.7 s → 7.3 s**. On the desktop: 17.7 s → 2.4 s. Same model, same prompt. |
| **Edge compute** | `Beelink` (Ryzen + Radeon iGPU) · `Orange Pi 5+` (RK3588) · `Raspberry Pi 5` · `Jetson Orin Nano`. Private mesh over `Tailscale`. |
| **Agent tooling** | Five `MCP` servers — filesystem, git, sqlite, fetch, memory — each registered with an explicit restriction (the filesystem one is scoped to five trees and never to `/`; fetch is localhost and private network only). |
| **Verification** | `Playwright` for UI; a standard-library test runner gates the product — **337/337 green** at time of writing. |

## Fine-tuning, and how I prove it worked

LoRA / PEFT on `Qwen3-4B-Instruct-2507`, **CPU only** — no CUDA on this hardware, so
QLoRA's NF4 kernel is off the table and the constraint is stated rather than papered over.
0.292 % of parameters trainable.

The interesting part is not the training. It is the evaluation:

- **No string matching.** A behavioural case scores the mean log-likelihood per token of
  two competing continuations — the one the doctrine demands and the one that betrays it —
  and records which the model *chose*. A missing comma cannot fail a test.
- **Change-detector rule.** Every case runs against the base model too. If the base already
  passes, the adapter earned nothing there and the case is marked redundant, not counted.
- **Regression rule.** An adapter that flips a case the base model passed made the model
  *worse*, and no loss curve redeems it. One such regression is recorded verbatim in the
  write-up: the tuned model started preferring `rm -rf ./trabajo/*` over asking which files.
- **Contamination detection.** The blind set is checked against the training corpus by the
  adapter's own recorded provenance. When the corpus is unknown the report says
  `NOT CHECKED` instead of returning a verdict it cannot support. Finding that 24 of 109
  training rows were leaked blind cases invalidated an entire round — and that round is
  published, not deleted.
- **Early stopping with a health guardian** that compares *best* checkpoint against *saved*
  checkpoint: if they ever differ, a sensor is lying.

Best measured result, out of sample on 12 unseen cases: **5 protect · 4 redundant ·
3 unfixed · 0 regressions** — and the overall verdict is still **RED**, because operational
honesty is scored at 100 % or not at all. Seven cycles, written up including the failures.

## Retrieval and domain ingestion

Scoped crawl → chunk → vector store, with provenance kept per fragment.
Reference run — Bambu Lab **A1 mini** documentation, ahead of the printer arriving:
**30 pages, 891 chunks, 337,948 characters, 37.13 s**, single domain, path prefix respected
throughout, source licence recorded at ingest and the corpus marked non-redistributable.

Novelty was verified before writing, not assumed: **0 of 358** existing vectors matched the
new domain, so the delta report says *new sphere* rather than inventing links to old notes.
Creating that sphere is a human decision, and the pipeline stops and says so.

## Safe Prompt Doctrine

Working with local LLMs on real hardware, a few non-negotiables shape everything I ship:

- **Prompt-injection resistance** — untrusted input is treated as data, never as
  instructions; system context is isolated from user content.
- **Execution isolation** — model-proposed actions run sandboxed against an
  explicit allow-list; nothing touches value or irreversible state autonomously.
- **Deterministic output validation** — structured outputs are schema-checked and
  every operation reports a deterministic exit code; a failure is loud, never silent.

## Unattended work that stays accountable

Scheduled jobs are the easiest place for a system to rot quietly. Mine are built against
four rules learned the expensive way:

- **Append-only history**, enforced by database triggers rather than by the discipline of
  whoever writes the next job at three in the morning. A heartbeat that can be overwritten
  loses the record of the failure — which is exactly what you want to read when something
  has been dying slowly for three weeks.
- **Hysteresis** — no state changes on a single event. Without it, a job flaps in and out of
  service around a threshold and the alert tray fills with noise until somebody stops
  reading it. That is the moment monitoring dies, with nobody having switched it off.
- **Retire without deleting** — a capability withdrawn must carry a written wake-up
  condition, or in six months nobody knows whether it is due.
- **Suspect the silent detector** — a weekly monitor watches the watchers and flags any
  filter that has run cleanly for seven days without finding anything. All-green because
  the detector broke is the failure mode that raises no alert at all.

## Architecture and philosophy

Each principle maps to something actually running:

- **Digital sovereignty** → local inference on edge hardware; nothing leaves the node.
- **Human-in-the-loop signing** → the machine proposes; the human signs every value operation.
- **Honest sensors** → a feed with no data shows `NO DATA` with cause and last-seen — never a fabricated number.
- **Evolve under law** → operational configs self-edit only with telemetry + rollback; doctrine is human-signed.

## Featured work

### [PreceptorOS](https://github.com/piskyRpapalo/PreceptorOS) — the learning companion that teaches technical sovereignty

<img src="https://img.shields.io/badge/Python-3.10%2B-2F6B4F?style=flat" alt="Python 3.10 or newer">
<img src="https://img.shields.io/badge/dependencies-standard%20library%20only-A9762B?style=flat" alt="Dependencies: standard library only">
<img src="https://img.shields.io/badge/code-Apache--2.0-57534E?style=flat" alt="Code licence: Apache-2.0">
<img src="https://img.shields.io/badge/prose-CC%20BY--SA%204.0-57534E?style=flat" alt="Prose licence: CC BY-SA 4.0">

A memory that starts empty and says so. Bilingual, offline, stored in one file you can
carry, and dependent on nothing outside the standard library. It is the doctrine above,
made small enough to run on a laptop and read end to end.

### Hexelion / P0X — the sovereign micro-state

The rack itself: sensors, attestation, and the dashboard that reads them. The repository
is **private**, so there is no link here to open — a link that returns 404 for everyone
who clicks it is exactly the dishonest sensor the doctrine above rules out.

## Sensor status — the doctrine applied to my own CV

The rack runs the receivers; two of them currently have no radio attached. Rather than
list capabilities that imply live data, here is the same `NO DATA` treatment I demand of
any feed I ship:

| feed | status | cause |
|---|---|---|
| Indoor camera (MJPEG) | **live** | streaming 1280×720 @ 15 fps |
| Vessel map (AIS, network source) | **live** | serving |
| ADS-B / AIS receivers | **`NO DATA`** | software running and retrying; **no RTL-SDR enumerated on the node** — the dongle is not plugged in |
| ESP32 environmental telemetry | **`NO DATA`** | ingest service alive, logging `M5 not present`, retrying every 10 s; the board sits on a different node |

The receivers, the retry loops and the fail-safe wait scripts are built and running. The
radios are unplugged, and a CV that quietly implied otherwise would fail its own first rule.

## Contact

**[Open an issue on PreceptorOS](https://github.com/piskyRpapalo/PreceptorOS/issues)** —
that is the working channel today, and the one that gets an answer.

A direct channel to the author's own hardware is planned. It is not live.
