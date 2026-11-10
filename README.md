# David Pecero Caballero

**PreceptorOS · Local-first AI · Deterministic software · Human oversight**

[GitHub repositories](https://github.com/piskyRpapalo?tab=repositories) · [PreceptorOS Web](https://www.preceptoros.org/) · [Community missions](https://github.com/piskyRpapalo/preceptoros-public-mesa) · [LinkedIn](https://www.linkedin.com/in/david-pecero-caballero/)

## What I build

I design AI tools that run on hardware their owner controls. I focus on the logic around a model. I work on evidence search, exact decisions, safe tool use, tests, and records of failure.

**PreceptorOS** is my engineering portfolio and an open place to work with others. The project has public code and tests. It also has private coordination and infrastructure. These parts have different access rules.

My rules are simple: **local first; measured or `NO_DATA` with a cause; silicon proposes, the human signs.** A test result does not prove that a live service works. A source file does not prove an end-to-end feature.

## The ecosystem

| Part | GitHub | What is built or in review |
|---|---|---|
| **Web** | [preceptoros-web](https://github.com/piskyRpapalo/preceptoros-web) | Public entry point, local AI guides, OpenWorld, and small testable JavaScript cores. |
| **App** | [preceptoros-app](https://github.com/piskyRpapalo/preceptoros-app) | Local companion with nine panels, memory, model interfaces, and evidence checks. |
| **Lab** | [lab](https://github.com/piskyRpapalo/lab) | Reproducible tests, local model studies, search code, and measured records. |
| **Study** | [study](https://github.com/piskyRpapalo/study) | Public methods, contracts, laws, and research. |
| **Babel** | [babel](https://github.com/piskyRpapalo/babel) | The single home for official terms and their history. |
| **Companions** | [preceptoros-companion](https://github.com/piskyRpapalo/preceptoros-companion) | A public door for people who bring their own projects. |
| **Public Mesa** | [preceptoros-public-mesa](https://github.com/piskyRpapalo/preceptoros-public-mesa) | Public missions for people and AI preceptors. The public catalog is merged and serving. |
| **Private Mesa** | [preceptoros-private-mesa](https://github.com/piskyRpapalo/preceptoros-private-mesa) | Restricted coordination, research checks, internal proposals, and human review. Private content is not required for public work. |

**Web, App, Lab, and Study** are the four core public repositories. Babel and Companions provide public entry points. **Public Mesa and Private Mesa are the two mission and review surfaces**, not two new AI engines.

Public Mesa is for tasks done **by, for, and with the community**. Its [public catalog](https://github.com/piskyRpapalo/preceptoros-public-mesa/blob/main/CATALOG.md) was merged on 2026-11-10 and is the published task list for contributors.

Private Mesa connects the work of the GitHub preceptors. It stores questions, checks, and decisions before any public release. Its [preceptor README](https://github.com/piskyRpapalo/preceptoros-private-mesa/blob/main/preceptors/README.md) is merged.

## Five engineering pieces

Each example links to code and, where available, a test. These are **working source implementations**, not a claim of live integration.

### 1. Exact probabilities for AI decisions

[App · `eleccion_tier2.py`](https://github.com/piskyRpapalo/preceptoros-app/blob/main/eleccion_tier2.py)

A model can return a score and still be wrong. This validator checks a closed option set. It uses Python `Fraction` values to verify that the stated probabilities add up to **10,000 basis points**, with zero rounding tolerance. It rejects invalid input. It can return `NO_DATA` with a cause instead of making a choice.

**Problem solved:** Keep a model's confidence separate from proof that a decision is valid.

### 2. Search with strict source and byte limits

[Lab · `attention_selector/core.py`](https://github.com/piskyRpapalo/lab/blob/main/attention_selector/core.py) · [Tests](https://github.com/piskyRpapalo/lab/blob/main/tests/test_attention_selector.py)

A local model cannot read every file at once. This selector gives each text chunk a deterministic score. It uses term overlap and inverse document frequency. It applies source exclusions and hard byte limits. It records why it did not select a chunk.

**Problem solved:** Retrieve useful context with stable rules and a bounded cost.

### 3. Answers tied to checked source text

[App · `hexelion_book.py`](https://github.com/piskyRpapalo/preceptoros-app/blob/main/hexelion_book.py) · [Local proxy](https://github.com/piskyRpapalo/preceptoros-app/blob/main/hexelion_proxy.py)

A fluent model answer is not a valid source citation. This code checks the SHA-256 value of each source. It limits prompt and quote sizes. It checks exact extracts before the answer can be accepted. The local proxy restricts network targets and returns a cause when a model is not available.

**Problem solved:** Make evidence checks independent of a model's fluency. **Live remote inference:** `NO_DATA: end_to_end_not_verified`.

### 4. Reproducible game probabilities

[Web · `public/game/gacha.js`](https://github.com/piskyRpapalo/preceptoros-web/blob/main/public/game/gacha.js) · [10,000-draw test cases](https://github.com/piskyRpapalo/preceptoros-web/blob/main/atlas/puros/gacha_odds_cases.mjs)

The generator takes a fixed seed. Rarity weights are explicit. The test code checks the weights and runs 10,000 seeded draws for each game class. It compares the counts with declared statistical limits.

**Problem solved:** Test a probability system with repeatable inputs. A seeded game generator is **not** a cryptographic random source.

### 5. A duel with a verifiable replay

[Web · `atlas/puros/wave_duel.js`](https://github.com/piskyRpapalo/preceptoros-web/blob/main/atlas/puros/wave_duel.js) · [Tests](https://github.com/piskyRpapalo/preceptoros-web/blob/main/atlas/puros/wave_duel_cases.mjs)

Each player has a seed. The code derives moves and records SHA-256 commitments. The verifier rejects a changed move or commitment. The same input gives the same replay.

**Problem solved:** Detect changes to a simulation record. This code does **not** verify a player's identity or claim that the game is balanced.

## How preceptors read and write

A preceptor can be a person, an AI agent, or both working together.

**Read:** Start with the task, the repository's `AGENTS.md`, and the source files. Check current code before you propose new code. Use [Study](https://github.com/piskyRpapalo/study/blob/main/08-ai-fluency.md) for reading depth and budgets.

**Name:** Apply the [Renaming Law](https://github.com/piskyRpapalo/study/blob/main/10-collisions.md). Use the official English name. Keep older names as dated aliases. Read the [Rosetta](https://github.com/piskyRpapalo/study/blob/main/13-rosetta.md) to map the Sovereign's Spanish terms to those names. [Babel](https://github.com/piskyRpapalo/babel/blob/main/registry/reading-directions.md) is the current vocabulary home. Rosetta reads names; it does not create new terms.

**Write:** Record the problem, source, proposed change, result, limits, and a next step. Use short, clear sentences in the style of **ASD-STE100**. Link to the exact file and commit. Mark unknown results `NO_DATA` with a cause. An idea, a code path, a running service, and an end-to-end test are different states.

**Review:** Work on a branch. Open a draft GitHub Pull Request. Run the owner's checks. Add a small receipt. The human approves the **exact head SHA** before a consequential merge. A preceptor must not sign on the human's behalf.

**Use the two Mesas:**
- [Private Mesa](https://github.com/piskyRpapalo/preceptoros-private-mesa) holds internal research, source checks, conflicts, and review. Do not copy its contents to public projects.
- [Public Mesa](https://github.com/piskyRpapalo/preceptoros-public-mesa) holds reviewed, safe missions and public contributor work. Use public sources only. You do not need private access to help.

Missions live in the two Mesas, cut over on 2026-11-10 under a signed Sovereign order. The [WEB mission map §9](https://github.com/piskyRpapalo/preceptoros-web/blob/main/docs/canon-map-details-20261107.md) is the historical source of record; new missions are proposed only in a Mesa.

**Evolution Alarm (B6):** An old concept can receive a new mission later. For example, a mission at position `778.5` may be found after `782` was built. The [B6 implementation PR](https://github.com/piskyRpapalo/preceptoros-web/pull/798) computes past distance and later progress over declared records. It does not set a priority or approve work. **Live GitHub source adapter:** `NO_DATA: not_implemented`.

## Build with us

We do not sell a product here. We publish code, methods, tests, and known gaps. You can report a problem, check a mission, or propose a small improvement.

Start at [Public Mesa](https://github.com/piskyRpapalo/preceptoros-public-mesa). Read the public mission and its checks. Share a reproducible result. Keep it clear enough for a person, a screen reader, and a machine to reach the same conclusion.

**The method:** [METHOD.md](METHOD.md) · **The public reading guide:** [Study](https://github.com/piskyRpapalo/study) · **The mission door:** [Public Mesa](https://github.com/piskyRpapalo/preceptoros-public-mesa).

---

**Publication note:** Statements in this profile describe inspected source code and available public records as of 2026-11-10. They do not certify legal compliance or production uptime. Public and private data remain separate.
