# Mayke De Freitas Santos

I work on inference efficiency and scientific imaging infrastructure,
running on a Threadripper 7970X / RTX PRO 6000 96GB workstation I built
for this purpose.

## Current work

**[Forge-Edge](https://github.com/maykef/forge_edge)** — Surprisal-gated
dual-vocabulary inference. A Shannon-grounded router that resolves 95% of
token predictions from 13.9% of the vocabulary. On Llama 3.1 8B: 73% MAD
reduction at the LM head, 16.6% measured energy savings, 15.8% throughput
gain, trained in 81 seconds. Zero observed quality degradation.

**[entropy2vec](https://github.com/maykef/entropy2vec)** — The theoretical
foundation for Forge-Edge. Are entropy-aware token embeddings real signal,
independent of frequency? Five experiments across GPT-2 and Qwen3-14B.
Short answer: yes (Cohen's d = 1.16, model-agnostic to three decimal
places). Can you exploit it in frozen models? No. Here's exactly why.

## Scientific imaging

**[czi_processing](https://github.com/maykef/czi_processing)** — High-
performance pipeline for 200GB+ Zeiss confocal datasets. CZI → OME-Zarr
with parallel stitching (48 workers), PCIe 5.0 NVMe-optimised Zarr writing,
correct 3D physical scaling from microscope metadata. 211GB in 15 minutes.

**[celltron](https://github.com/maykef/celltron)** — GPU-accelerated 3D
anisotropy analysis. Structure tensor computation in 26 directions,
FA/CL/CS/CP measures, Apple MPS backend, CPU-parallelised
eigen-decomposition.

**[microscopy_indexing](https://github.com/maykef/microscopy_indexing_yolo-qwen2-72b)**
— OCR-free extraction of scientific PDFs using DocLayout-YOLO + Qwen2-VL-72B.
Handles multi-column layouts, LaTeX equations, figure captions. 95%+ accuracy
on scientific text.

## Background

Cambridge, UK. Masters in Conservation Leadership (Cambridge). I've spent
several years procuring the exact instruments that generate the data above —
confocal microscopes, imaging systems, lab infrastructure — which turns out
to be an unusual way to understand both the hardware and what researchers
actually need from it.

→ [maykef.info](https://maykef.info)
