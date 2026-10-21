# IW3 Colab: 2D to 3D Stereoscopic Video & Image Converter

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TakisAlPastor/IW3-Colab/blob/main/iw3_colab.ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

An optimized, headless Google Colab workflow for converting standard 2D videos and image collections into immersive 3D stereoscopic formats (Side-by-Side, Top-Bottom, VR180) using [`nagadomi/nunif`](https://github.com/nagadomi/nunif)'s **`iw3`** module.

---

## 🚀 Quick Start

1. Click the **Open in Colab** badge above.
2. Ensure you are connected to a GPU runtime (**Runtime** → **Change runtime type** → **T4 GPU**).
3. Execute the notebook cells sequentially:
   - **Cell 1:** Verify GPU allocation and CUDA availability.
   - **Cell 2:** Mount Google Drive to persist media and outputs.
   - **Cell 3:** Set up the `nunif` environment and dependencies.
   - **Cell 4:** Configure conversion parameters using interactive Colab Form controls and execute.
   - **Cell 5:** Verify elementary stream geometry and container integrity.

---

## 🥽 VR Headset Compatibility & Recommended Settings

| Headset / Player | Recommended Format | Divergence | Convergence | Method | Video Codec |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Meta Quest 3 / Quest Pro** (Skybox VR, 4XVR) | `full-sbs` | `2.0` | `0.5` | `forward` | `h264_nvenc` |
| **Meta Quest 2** (Legacy / Bandwidth-Constrained) | `half-sbs` | `1.8` | `0.5` | `row` | `h264_nvenc` |
| **Apple Vision Pro** | `full-sbs` | `2.2` | `0.5` | `forward` | `hevc_nvenc` |
| **Standard 3D TV / Monitor** | `half-sbs` or `tb` | `1.8` | `0.5` | `forward` | `libx264` |
| **Anaglyph (Red/Cyan Glasses)** | `anaglyph` | `1.5` | `0.5` | `forward` | `libx264` |

---

## ⚙️ Model Selection & VRAM Optimization

The notebook supports multiple depth estimation backends:

| Model Identifier | Architecture | VRAM Usage (at 384p) | Relative Speed | Recommended Use Case |
| :--- | :--- | :--- | :--- | :--- |
| `Any_V2_L` | Depth Anything V2 (Large) | ~10–12 GB | 1x (Baseline) | **Recommended for T4 GPU.** Maximum depth detail and temporal stability. |
| `Any_V2_B` | Depth Anything V2 (Base) | ~5–7 GB | ~2.2x faster | Faster renders with minimal detail loss. |
| `Any_V2_S` | Depth Anything V2 (Small) | ~3–4 GB | ~4x faster | Quick previews and rapid iteration. |
| `ZoeD_Any_N` | ZoeDepth Metric Hybrid | ~8–10 GB | ~1.3x faster | Scenes requiring absolute metric distance estimations. |

> [!TIP]
> **Preventing CUDA Out of Memory (OOM):**
> On standard Colab T4 instances (16 GB VRAM), default parameters are already tuned with `--zoed-height 384` and `--batch-size 1`. If processing 4K sources encounters an OOM error, reduce `zoed_height` to `320` or switch `depth_model` to `Any_V2_B`.

---

## 🧪 Verification & Integrity Pipeline

Cell 5 implements automated verification:
* **`ffprobe` Inspection:** Validates horizontal and vertical pixel geometry (e.g. verifying 32:9 ratio for Full-SBS).
* **Null-Mux Decode:** Executes `ffmpeg -v error -i <file> -f null -` to verify packet timestamps (PTS/DTS) and detect macroblock decode errors.
* **Inline Preview:** Extracts a sample stereo frame and renders it directly within the notebook.

---

## 📄 License & Credits

* Core stereoscopic conversion engine powered by [`nagadomi/nunif`](https://github.com/nagadomi/nunif) (IW3 module).
* Notebook and workflow harness maintained under the MIT License.
