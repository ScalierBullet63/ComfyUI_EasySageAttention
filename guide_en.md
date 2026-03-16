# 🔧 Installation Guide: SageAttention + Triton for ComfyUI

## 📚 Summary

- [1. Install GPU drivers and NVIDIA CUDA Toolkit](#-1-install-gpu-drivers-and-nvidia-cuda-toolkit)
- [2. Install Visual Studio Build Tools 2026](#-2-install-visual-studio-build-tools-2026)
- [3. Install the required Python packages](#-3-install-the-required-python-packages)
- [4. Install PyTorch with CUDA support](#-4-install-pytorch-with-cuda-support)
- [5. Install Triton](#-5-install-triton)
- [6. Clone and install SageAttention](#-6-clone-and-install-sageattention)
- [7. Installation completed!](#-installation-completed)

# ✅ 1. Install GPU drivers and NVIDIA CUDA Toolkit

- Download the latest version of the NVIDIA drivers via the [NVIDIA App](https://www.nvidia.com/it-it/software/nvidia-app/) or from the [NVIDIA website](https://www.nvidia.com/it-it/drivers/).

- If you don’t want to compile SageAttention in order to save time and install less software on your system, skip to [step 3](#3-install-the-required-python-packages); otherwise continue below.

  > ⚠️ Note: NVIDIA CUDA Toolkit version 13.0 was recently released but does not currently appear to be compatible with PyTorch and SageAttention. Therefore, it is recommended to install NVIDIA CUDA Toolkit 12.9 from the following link:

  [https://developer.nvidia.com/cuda-12-9-0-download-archive](https://developer.nvidia.com/cuda-12-9-0-download-archive)

- After installation, verify CUDA version with:

  ```bash
  nvcc --version
  ```

  > Recommended: `>= cuda_12.9.0_571.96`

- Restart your PC after installation.

---

## ✅ 2. Install Visual Studio Build Tools 2026

Install the **Desktop development with C++** workload.

Link: https://visualstudio.microsoft.com/visual-cpp-build-tools/

> The full installation is only required for compilation.

⚠️ To install Visual Studio Build Tools 2026, you must have at least Windows 10 version 20H1 or Windows 11 starting from version 21H2.

---

## ✅ 3. Install the required Python packages

Open `CMD` inside `ComfyUI_windows_portable` and run these 5 commands one at a time:

```bash
.\python_embeded\python.exe -s -m pip install "accelerate >= 1.1.1"
```

```bash
.\python_embeded\python.exe -s -m pip install "diffusers >= 0.31.0"
```

```bash
.\python_embeded\python.exe -s -m pip install "transformers >= 4.39.3"
```

```bash
.\python_embeded\python.exe -s -m pip install ninja
```
  
```bash
.\python_embeded\python.exe -s -m pip install buildtools
```

---

## ✅ 4. Install PyTorch Nightly with CUDA

From `ComfyUI_windows_portable` folder:

```bash
.\python_embeded\python.exe -m pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu129 --upgrade
```

> ⚠️ Note: you can also install the nightly version of PyTorch using the following command, which includes the latest features and updates. However, this version may cause compilation issues with SageAttention, so use it at your own risk:

```bash
.\python_embeded\python.exe -m pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu129 --upgrade
```

---

## ✅ 5. Install Triton

From the `ComfyUI_windows_portable` folder, run:

```bash
.\python_embeded\python.exe -m pip install triton-windows
```

### 🧩 Add required includes and libs:

Download the correct ZIP based on the Python version you have in `.\python_embeded` and extract it:

- [Python 3.11.x](https://github.com/woct0rdho/triton-windows/releases/download/v3.0.0-windows.post1/python_3.11.9_include_libs.zip)
- [Python 3.12.x](https://github.com/woct0rdho/triton-windows/releases/download/v3.0.0-windows.post1/python_3.12.7_include_libs.zip)
- [Python 3.13.x](https://github.com/woct0rdho/triton-windows/releases/download/v3.0.0-windows.post1/python_3.13.2_include_libs.zip)

Put the extracted "include" and "libs" folders inside:

```
ComfyUI_windows_portable\python_embeded
```

---

## ✅ 6. Clone and Install SageAttention

- If you want to compile SageAttention for maximum compatibility

  From the `ComfyUI_windows_portable` folder:

  ```bash
  git clone https://github.com/thu-ml/SageAttention
  ```

  Then from `ComfyUI_windows_portable\SageAttention` run:

  ```bash
  ..\python_embeded\python.exe -m pip install .
  ```

- IF you prefer to avoid compiling SageAttention

  Look among [these wheels](https://github.com/woct0rdho/SageAttention/releases) for the one that matches the PyTorch version installed in `.\python_embeded`, which you can see when ComfyUI starts in the terminal (CMD).

  > ⚠️ Note: if you can’t find a wheel with the same CUDA version as the PyTorch installed in ComfyUI, you can try ignoring the CUDA version and install the wheel anyway. If it doesn’t work, you can change the PyTorch version in ComfyUI or compile SageAttention for your specific version.

  Copy the link of the wheel compatible with your configuration. Then, from the `ComfyUI_windows_portable` folder, run:
  
  ```bash
  .\python_embeded\python.exe -m pip install [copied-url]
  ```
  
  > ⚠️ Note: if you already have SageAttention installed and want to update it to a newer version, add `--upgrade` to the previous command.

  Example:

  ```bash
  .\python_embeded\python.exe -m pip install https://github.com/woct0rdho/SageAttention/releases/download/v2.2.0-windows.post2/sageattention-2.2.0+cu128torch2.8.0.post2-cp39-abi3-win_amd64.whl
  ```

## 🎉🎊 Installation completed!

To use SageAttention, add the `--use-sage-attention` flag to the startup `.bat` file or add the [Patch Sage Attention KJ](https://github.com/kijai/ComfyUI-KJNodes) node inside your workflow!

> If you encounter issues, check that the PyTorch and CUDA versions are compatible with the wheel, or recompile SageAttention as described in step 6.
