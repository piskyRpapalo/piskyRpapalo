<div align="center">

<img src="https://raw.githubusercontent.com/piskyRpapalo/aurelius/main/assets/aurelius-talks.png" width="520"
     alt="Pixel-art sprite sheet, four frames on one strip: a white marble bust of a bearded classical figure with one lit amber eye, the marble cracked open to show dark machinery underneath. The mouth is barely open in the first frame, wide in the second, rounded in the third, and closed in a slight smile in the fourth.">

# Hi, I'm David

**I build local-first AI systems that run on their own hardware.**

Sun-fed edge nodes that sense the physical world, learn alongside their human,
and never sign value autonomously. My north star is *digital sovereignty*: your
machine, your models, your data, your signature.

</div>

---

## Core stack

`Python` · `TypeScript / React (Vite)` · `Playwright` · `FastAPI` · `systemd` ·
`Redis` · `SQLite / TimescaleDB` · `Bash`

## AI and edge infrastructure

| | |
|---|---|
| **Local inference** | `Qwen` (instruct variants) served with `Ollama` — no cloud calls. |
| **Edge compute** | `Beelink` (Ryzen + Radeon iGPU) · `Orange Pi` · `Raspberry Pi`. |
| **Sensing** | `RTL-SDR` software-defined radio (ADS-B & AIS) · `ESP32` environmental telemetry. |
| **Verification** | `Playwright` end-to-end suites gate every UI change before it ships. |

## Safe Prompt Doctrine

Working with local LLMs on real hardware, a few non-negotiables shape everything I ship:

- **Prompt-injection resistance** — untrusted input is treated as data, never as
  instructions; system context is isolated from user content.
- **Execution isolation** — model-proposed actions run sandboxed against an
  explicit allow-list; nothing touches value or irreversible state autonomously.
- **Deterministic output validation** — structured outputs are schema-checked and
  every operation reports a deterministic exit code; a failure is loud, never silent.

## Architecture and philosophy

Each principle maps to something actually running:

- **Digital sovereignty** → local inference on edge hardware; nothing leaves the node.
- **Human-in-the-loop signing** → the machine proposes; the human signs every value operation.
- **Honest sensors** → a feed with no data shows `NO DATA` with cause and last-seen — never a fabricated number.
- **Evolve under law** → operational configs self-edit only with telemetry + rollback; doctrine is human-signed.

## Current focus

- Optimizing **local inference on edge hardware** (context sizing, model orchestration by cost).
- **Real-time RF data ingestion** (ADS-B / AIS) on distributed edge nodes, rendered on a live map.
- **Local agent orchestration** — a panel of small local models that propose, never decide.

<details>
<summary>How the pieces fit (deeper)</summary>

<br>

- A local API gateway (FastAPI) fans data from radio, environmental and chain-read
  sources into a single dashboard; slow or missing feeds degrade independently and
  honestly, never freezing the surface.
- Radio capture (dump1090 / AIS-catcher) runs on the edge nodes and is wired to the
  gateway by environment variable — moving a sensor between nodes is a config change,
  not a code change.
- The web surface is a React/Vite multi-page app; a Playwright suite runs across
  mobile-to-desktop viewports as the merge gate.

</details>

## Featured work

### [Aurelius](https://github.com/piskyRpapalo/aurelius) — the learning companion that teaches technical sovereignty

<img src="https://img.shields.io/badge/Python-3.10%2B-2F6B4F?style=flat" alt="Python 3.10 or newer">
<img src="https://img.shields.io/badge/dependencies-standard%20library%20only-A9762B?style=flat" alt="Dependencies: standard library only">
<img src="https://img.shields.io/badge/code-MIT-57534E?style=flat" alt="Code licence: MIT">
<img src="https://img.shields.io/badge/prose-CC%20BY--SA%204.0-57534E?style=flat" alt="Prose licence: CC BY-SA 4.0">

A memory that starts empty and says so. Bilingual, offline, and stored in one
file you can carry. It is the doctrine above, made small enough to run on a
laptop and read end to end.

### Hexelion / P0X — the sovereign micro-state

The rack itself: sensors, attestation, and the dashboard that reads them. The
repository is **private**, so there is no link here to open — a link that
returns 404 for everyone who clicks it is exactly the dishonest sensor the
doctrine above rules out.

## Contact

**[Open an issue on Aurelius](https://github.com/piskyRpapalo/aurelius/issues)** —
that is the working channel today, and the one that gets an answer.

A direct channel to the author's own hardware is planned. It is not live.
