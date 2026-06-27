# Does the TOKW world model track physics? — PHYRE verification

A clean ground-truth **verification** of the TOKW v0.4.0 world model on Meta's
[PHYRE](https://github.com/facebookresearch/phyre) `ball_within_template` benchmark.

Live site: **https://zetetic-dhruv.github.io/neuro-sym-wm-phyre/**

- **`/` (landing)** — GT as **verifier**: the *unchanged* VLM-trained model, same predictions (seeded
  from the VLM-observed first frame), scored against two referees — the Qwen VLM labels it was trained
  on, and PHYRE's exact physics from `featurized_objects`. **Ground truth never enters training or the
  seed.** (38 of 48 propositions are physically computable; conditional/perceptual ones excluded.)
- **`/vlm/`** — the original run where Qwen also supplies the eval reference.

## Headline

| metric | vs VLM oracle | vs physics (GT) |
|---|---|---|
| per-frame accuracy | 0.974 | **0.721** |
| persistence baseline | 0.997 | 0.962 |
| transition accuracy | 0.594 | **0.490** |
| spurious-flip rate | 0.025 | **0.270** |

Held fixed and re-graded against real physics, the model agrees with the **VLM oracle (~0.97)** far more
than with the **world (~0.72)** — it falls *below* the persistence baseline, gets physical transitions
right only ~49% of the time, and flips propositions at 27% of stable frames. **It learned to reproduce
the VLM's labelling, not the environment's dynamics.**

> An earlier version of this page reported a GT comparison that *trained* the model on ground-truth
> labels — that confounds training signal with the referee and is not a verification. This page uses GT
> strictly as the answer key on the unchanged model.

## Contents

- `index.html`, `gifs/` — verifier results + rollout GIFs (green = model prediction, white = physics)
- `vlm/` — the original VLM-reference results page
