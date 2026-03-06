# Mayke De Freitas Santos

I work on scientific imaging infrastructure and inference efficiency.  
Cambridge, UK · [maykef.info](https://maykef.info) · [LinkedIn](https://www.linkedin.com/in/mayke-santos-755960360/)

---

## Scientific text extraction

**[scientific-pdf-extraction](https://github.com/maykef/microscopy_indexing_yolo-qwen2-72b)** — High-fidelity text extraction from scientific books and papers.  
A production pipeline that replaces OCR with a vision-language model, achieving accuracy traditional OCR cannot reach on dense scientific content. DocLayout-YOLO detects and classifies every region on the page — text, titles, section headers, captions, formulas — and Qwen2-VL-72B transcribes each crop directly from the image. Multi-column reading order is reconstructed spatially. LaTeX equations are preserved verbatim. Benchmarked on graduate-level microscopy textbooks (A100 80GB, 8-bit):

| Metric | Value |
|---|---|
| Accuracy on scientific text | 95%+ |
| Throughput | ~15–25 tokens/sec |
| Pages/hour | ~30–50 |
| VRAM usage | 70–90 GB |

Checkpoint/resume for long books. OOM-safe dynamic batching. JSON output with per-block bounding boxes, confidence scores, and token counts. Markdown export with correct reading order.

---

## Inference efficiency

**[forge-edge](https://github.com/maykef/forge-edge)** — Surprisal-gated dual-vocabulary inference.  
A Shannon-grounded router that resolves 95% of token predictions from 13.9% of the vocabulary, combined with selective MLP layer bypass. Benchmarked on Qwen2.5-14B bf16 (M1 Max):

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
Five experiments across GPT-2 and Qwen3-14B. The signal is real (Cohen's d = 1.16, model-agnostic to three decimal places). Cannot be exploited in frozen models — here's exactly why.

---

## Scientific imaging

**[czi_processing](https://github.com/maykef/czi_processing)** — End-to-end pipeline for large Zeiss confocal datasets.  
Raw `.czi` mosaic files from a Zeiss confocal arrive as hundreds of overlapping tiles per Z-slice across multiple channels. This pipeline stitches them into full-resolution planes using weighted blending across 48 parallel workers — enough to saturate a 32-core Threadripper without thrashing 128GB of RAM. Stitched planes write directly to multiscale OME-Zarr using large-chunk Zarr writing tuned for PCIe 5.0 NVMe sequential throughput. Z-axis physical scaling is extracted automatically from microscope metadata (0.65 µm XY, 2.0 µm Z-step) and applied at load time in Napari, so the 3D volume renders with correct proportions without manual correction. The full pipeline runs from a single command.

| Dataset | Stitching | Zarr conversion | Total |
|---|---|---|---|
| 62 GB | 1.0 min | 2.7 min | 3.7 min |
| 211 GB | 3.7 min | 11.5 min | 15.4 min |

**[celltron](https://github.com/maykef/celltron)** — 3D anisotropy analysis for microscopy volumes.  
Quantifies local directional structure in 3D tissue volumes using the structure tensor method. Gradients are computed in 26 spatial directions (faces, edges, and corners of the voxel neighbourhood) via separable 3D Sobel kernels running on Apple MPS. The resulting 3×3 tensors are eigen-decomposed in parallel across CPU processes using NumPy backed by Apple's Accelerate framework, with per-process BLAS thread pinning to prevent oversubscription. From the ordered eigenvalues (λ1 ≥ λ2 ≥ λ3) the pipeline computes four standard anisotropy measures — Fractional Anisotropy (FA), Linear (CL), Planar (CP), and Spherical (CS) — following Westin et al. conventions. Output is float16 compressed NPZ with principal direction vectors, ready for visualisation in Napari.

| Volume | Processing time | Memory |
|---|---|---|
| 256³ voxels | 12.3 s | 2.1 GB |
| 512³ voxels | 98.7 s | 8.4 GB |
| 1024³ voxels | 847 s | 32.1 GB |

---

## Background

I've spent several years procuring the exact instruments that generate the data above — confocal microscopes, imaging systems, lab infrastructure at the University of Cambridge. It turns out to be an unusual way to understand both the hardware and what researchers actually need from it.

The workstation running most of this: Threadripper 7970X · RTX PRO 6000 96GB · 96TB ZFS.  
Details at [maykef.info](https://maykef.info).
