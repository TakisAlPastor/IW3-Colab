# IW3 Colab: 2D to 3D Stereoscopic Video & Image Converter

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TakisAlPastor/IW3-Colab/blob/main/iw3_colab.ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

A Google Colab workflow for converting standard 2D videos and images into immersive 3D stereoscopic formats (Side-by-Side, Top-Bottom, VR180) using [`nagadomi/nunif`](https://github.com/nagadomi/nunif)'s **`iw3`** module.

## Quick Start

1. Click the **Open in Colab** badge above.
2. Ensure you are connected to a GPU runtime (**Runtime** → **Change runtime type** → **T4 GPU** or higher).
3. Execute the notebook cells sequentially:
   - **Cell 1:** Inspect CUDA device allocation and verify FFmpeg/FFprobe binaries.
   - **Cell 2:** Mount Google Drive to persist video inputs and outputs.
   - **Cell 3:** Clone `nagadomi/nunif`, install dependencies, and download base checkpoints.
   - **Cell 4:** Configure conversion parameters.
   - **Cell 5:** Validate elementary stream geometry, packet integrity, and inspect an inline stereoscopic preview.

## 📄 License & Credits

* Core stereoscopic conversion engine powered by [`nagadomi/nunif`](https://github.com/nagadomi/nunif) (IW3 module).
* Notebook and workflow harness maintained under the MIT License.
