# Neuro-symbolic world model on PHYRE — results

A scrolling results page for the **TOKW v0.4.0** temporal-observable Kripke world model,
benchmarked **unmodified** on Meta's [PHYRE](https://github.com/facebookresearch/phyre)
`ball_within_template` physics benchmark.

Live site: **https://zetetic-dhruv.github.io/neuro-sym-wm-phyre/**

## What this is

- A VLM (Qwen2.5-VL-7B) proposes the atomic-proposition vocabulary, labels event clips, and
  provides the held-out reference. Only two small heads are trained: a latent-dynamics GRU and a
  truth-dynamics transformer over a frozen DINOv2 encoder.
- A PHYRE→TOKW dataset adapter was the only code added; the model code was run as-is.

## How to read the numbers

Raw next-frame accuracy (~0.98) is inflated by **label persistence** — only ~0.2% of frames change,
so copying the previous label already scores ~0.998. The meaningful signal is **transition accuracy**
(~0.59), measured only at the frames where the truth actually flips, where persistence scores 0 by
construction. The page leads with this decomposition.

## Contents

- `index.html` — the results page (open locally or via the live site)
- `gifs/` — per-task held-out rollouts with predicted vs reference atomic propositions overlaid
