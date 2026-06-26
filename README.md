# Neuro-symbolic world model on PHYRE — results

Scrolling results for the **TOKW v0.4.0** world model, benchmarked **unmodified** on Meta's
[PHYRE](https://github.com/facebookresearch/phyre) `ball_within_template` benchmark.

Live site: **https://zetetic-dhruv.github.io/neuro-sym-wm-phyre/**

- **`/` (landing)** — the **ground-truth eval**: atomic propositions computed directly from PHYRE's
  exact physics (`featurized_objects`), no VLM in the loop. Includes a VLM-vs-ground-truth comparison.
- **`/vlm/`** — the original run where Qwen2.5-VL supplies the vocabulary, the per-clip labels, *and*
  the held-out reference (same oracle end to end).

## The headline (ground truth vs VLM reference)

Same model, two references. Against PHYRE physics the model is a real-but-modest predictor; the VLM
reference had *undersold* it (it punished real changes the VLM never labelled).

| metric | VLM reference | ground truth |
|---|---|---|
| transition fraction | 0.22% | 4.1% |
| persistence baseline | 0.998 | 0.959 |
| autoregressive rollout | 0.976 | 0.929 |
| **transition accuracy** | 0.594 | **0.600** |
| frame-change precision | 0.067 | **0.417** |
| **frame-change F1** | 0.125 | **0.579** |

Under both references raw accuracy stays below persistence (physics is mostly static); the genuine
signal is concentrated at transitions (~0.60), and is robust to the reference choice.

## Contents

- `index.html`, `gifs/` — ground-truth results page + rollout GIFs (predicted vs physics labels)
- `vlm/index.html`, `vlm/gifs/` — the VLM-reference results page + GIFs
