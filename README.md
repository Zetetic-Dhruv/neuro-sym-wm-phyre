# Does the TOKW world model track physics? — PHYRE verification + ablations

A clean ground-truth **verification** + **A–F ablation panel** for the TOKW v0.4.0 world model on
Meta's [PHYRE](https://github.com/facebookresearch/phyre) `ball_within_template` benchmark.

Live site: **https://zetetic-dhruv.github.io/neuro-sym-wm-phyre/**

- **`/` (landing)** — GT as verifier (unchanged VLM-trained model, scored against physics) + the A–F
  panel showing what each component contributes.
- **`/vlm/`** — the original run where Qwen also supplies the eval reference.

## Headlines

**Verifier:** the model agrees with the **VLM oracle (~0.97)** far more than with the **world
(~0.72)** — it inherits the labeller's ~28% physical error and at-chance transitions exactly,
adding none of its own.

**Ablation panel (vs physics, 38 mappable APs):**

| config | per-frame | transition |
|---|---|---|
| A — VLM-direct (no model) | 0.719 | 0.489 |
| B — Persistence of v₀ | 0.722 | 0.494 |
| C — Truth-only (z=0) | 0.718 | 0.489 |
| D — Truth-only (z=0, a=0) | 0.719 | 0.488 |
| **F — Full model** | **0.721** | **0.490** |
| E — Kripke Markov chain | 0.685 | 0.494 |
| All-zeros null | 0.723 | — |

A, B, C, D, F lie inside a 0.004 band on per-frame and 0.006 on transition accuracy: **persistence
of v₀ matches the full model**. The latent z, the action channel, and the truth-dynamics
transformer add no measurable physical fidelity. E (Kripke) is strictly worse — discretising to
states actively destroys information. Every variant sits **at or below the all-zeros null (0.723)**,
which is just the mean per-AP zero rate in the schema. The 0.72 number is label sparsity, not a
model signal.

## Caveats

- An earlier `frame_change_f1` column was dropped (degenerate metric: 2p/(1+p) at the physics
  frame-change rate, independent of the ablation).
- C and D retrain logs were silent; their numbers are *consistent with* the headline rather than
  *independent confirmation of* it pending a relogged rerun.

> An earlier version of this page reported a GT comparison that *trained* the model on ground-truth
> labels — that confounds training signal with the referee and is not a verification. This page uses
> GT strictly as the answer key on the unchanged model.

## Contents

- `index.html`, `gifs/` — verifier + ablation panel + rollout GIFs
- `vlm/` — the original VLM-reference results page
