# 🔧 Installation Guide: Sage Attention + Triton for ComfyUI


## ✅ 1. Install CUDA Toolkit and GPU Drivers

- Download the latest NVIDIA CUDA Toolkit:  
  [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads)

- After installation, verify CUDA version with:

```bash
nvcc --version
```

> Recommended: `>= cuda_12.8.0_571.96`

- Restart your PC after installation.

---

## ✅ 2. Install Required Python Packages

Open `cmd` inside `ComfyUI_windows_portable\update` and run these 5 commands one at a time:

```bash
..\python_embeded\python.exe -s -m pip install "accelerate >= 1.1.1"
..\python_embeded\python.exe -s -m pip install "diffusers >= 0.31.0"
..\python_embeded\python.exe -s -m pip install "transformers >= 4.39.3"
..\python_embeded\python.exe -s -m pip install ninja
..\python_embeded\python.exe -s -m pip install buildtools
```

---

## ✅ 3. Install PyTorch Nightly with CUDA

From `ComfyUI_windows_portable` folder:

```bash
.\python_embeded\python.exe -m pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu129 --upgrade
```

---

## ✅ 4. Install Triton

```bash
.\python_embeded\python.exe -m pip install triton-windows
```

### 🧩 Add required includes and libs:

Download the zip below based on your Python version and extract:

- [Python 3.11.x](https://github.com/woct0rdho/triton-windows/releases/download/v3.0.0-windows.post1/python_3.11.9_include_libs.zip)
- [Python 3.12.x](https://github.com/woct0rdho/triton-windows/releases/download/v3.0.0-windows.post1/python_3.12.7_include_libs.zip)

Put the extracted "include" and "libs" folders inside:

```
ComfyUI_windows_portable\python_embeded
```

---

## ✅ 5. Install Visual Studio Build Tools 2022

Install the **Desktop development with C++** workload.

Link: [https://visualstudio.microsoft.com/visual-cpp-build-tools/](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

> Full installation is optional, but recommended.

---

## ✅ 6. Clone and Install SageAttention

From the `ComfyUI_windows_portable` folder:

```bash
git clone https://github.com/thu-ml/SageAttention
```

Then from `ComfyUI_windows_portable\SageAttention`:

```bash
..\python_embeded\python.exe -m pip install .