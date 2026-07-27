# Hi, I'm David 👋

I build **local-first AI systems that run on their own hardware** — sun-fed edge
nodes that sense the physical world, learn alongside their human, and never sign
value autonomously. My north star is *digital sovereignty*: your machine, your
models, your data, your signature.

## ⚙️ Core Stack

`Python` · `TypeScript / React (Vite)` · `Playwright` · `FastAPI` · `systemd` ·
`Redis` · `SQLite / TimescaleDB` · `Bash`

## 🧠 AI & Edge Infrastructure

- **Local inference:** `Qwen` (instruct variants) served with `Ollama` — no cloud calls.
- **Edge compute:** `Beelink` (Ryzen + Radeon iGPU) · `Orange Pi` · `Raspberry Pi`.
- **Sensing:** `RTL-SDR` software-defined radio (ADS-B & AIS) · `ESP32` environmental telemetry.
- **Verification:** `Playwright` end-to-end suites gate every UI change before it ships.

## 🛡️ Safe Prompt Doctrine

Working with local LLMs on real hardware, a few non-negotiables shape everything I ship:

- **Prompt-injection resistance** — untrusted input is treated as data, never as
  instructions; system context is isolated from user content.
- **Execution isolation** — model-proposed actions run sandboxed against an
  explicit allow-list; nothing touches value or irreversible state autonomously.
- **Deterministic output validation** — structured outputs are schema-checked and
  every operation reports a deterministic exit code; a failure is loud, never silent.

## 🏗️ Architecture & Philosophy

Each principle maps to something actually running:

- **Digital sovereignty** → local inference on edge hardware; nothing leaves the node.
- **Human-in-the-loop signing** → the machine proposes; the human signs every value operation.
- **Honest sensors** → a feed with no data shows `NO DATA` with cause and last-seen — never a fabricated number.
- **Evolve under law** → operational configs self-edit only with telemetry + rollback; doctrine is human-signed.

## 🚀 Current Focus

- Optimizing **local inference on edge hardware** (context sizing, model orchestration by cost).
- **Real-time RF data ingestion** (ADS-B / AIS) on distributed edge nodes, rendered on a live map.
- **Local agent orchestration** — a panel of small local models that propose, never decide.

<details>
<summary>How the pieces fit (deeper)</summary>

- A local API gateway (FastAPI) fans data from radio, environmental and chain-read
  sources into a single dashboard; slow or missing feeds degrade independently and
  honestly, never freezing the surface.
- Radio capture (dump1090 / AIS-catcher) runs on the edge nodes and is wired to the
  gateway by environment variable — moving a sensor between nodes is a config change,
  not a code change.
- The web surface is a React/Vite multi-page app; a Playwright suite runs across
  mobile-to-desktop viewports as the merge gate.

</details>

---

*Featured: [Hexelion / P0X](https://github.com/piskyRpapalo/-hexelion-public) — the
sovereign micro-state · [Aurelius](https://github.com/piskyRpapalo/aurelius) — the
learning companion that teaches technical sovereignty.*
