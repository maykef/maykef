# Mayke De Freitas Santos

I work on inference efficiency and scientific imaging infrastructure.  
Cambridge, UK · [maykef.info](https://maykef.info)

---

## Inference efficiency

**[forge-edge](https://github.com/maykef/forge-edge)** — Surprisal-gated dual-vocabulary inference.  
A Shannon-grounded router that resolves 95% of token predictions from 13.9% of the vocabulary,
combined with selective MLP layer bypass. Benchmarked on Qwen2.5-14B bf16 (M1 Max):

| Configuration | tok/s | Speedup |
|---|---|---|
| Baseline | 10.27 ± 0.26 | 1.00× |
| Stage 1 (vocab routing) | 10.63 ± 0.26 | 1.03× |
| Stage 2A (MLP bypass) | 11.04 ± 0.24 | 1.07× |
| **Stacked** | **12.09 ± 0.04** | **1.18×** |

Router trains in ~80 seconds. Zero observed quality degradation.  
Previously validated on Llama 3.1 8B: 73% MAD reduction, 16.6% measured energy savings.

**[entropy2vec](https://github.com/maykef/entropy2vec)** — The theoretical foundation.  
Are entropy-aware token embeddings real signal, independent of frequency?  
Five experiments across GPT-2 and Qwen3-14B. The signal is real (Cohen's d = 1.16,
model-agnostic to three decimal places). Cannot be exploited in frozen models — here's exactly why.

---

## Scientific imaging

**[czi_processing](https://github.com/maykef/czi_processing)** — 200GB+ Zeiss confocal pipeline.  
CZI → OME-Zarr with 48-worker parallel stitching, PCIe 5.0 NVMe-optimised Zarr writing,
correct 3D physical scaling from microscope metadata. 211GB processed in 15 minutes.

**[celltron](https://github.com/maykef/celltron)** — 3D anisotropy analysis.  
GPU-accelerated structure tensor computation (26 directions), FA/CL/CS/CP measures,
Apple MPS backend, CPU-parallelised eigen-decomposition.

**[microscopy_indexing](https://github.com/maykef/microscopy_indexing_yolo-qwen2-72b)** — OCR-free scientific PDF extraction.  
DocLayout-YOLO + Qwen2-VL-72B. Handles multi-column layouts, LaTeX equations, figure captions.
95%+ accuracy on scientific text.

---

## Background

I've spent several years procuring the exact instruments that generate the data above —
confocal microscopes, imaging systems, lab infrastructure at the University of Cambridge.
It turns out to be an unusual way to understand both the hardware and what researchers
actually need from it.

The workstation running most of this: Threadripper 7970X · RTX PRO 6000 96GB · 96TB ZFS.  
Details at [maykef.info](https://maykef.info).
