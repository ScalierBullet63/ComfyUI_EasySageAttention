# 🔧 Installation Guide: SageAttention + Triton for ComfyUI

## ✅ 1. Install CUDA Toolkit and GPU Drivers

- Download the latest NVIDIA CUDA Toolkit:

  > ⚠️ Note: NVIDIA CUDA Toolkit version 13.0 was recently released but does not currently appear to be compatible with PyTorch and SageAttention. Therefore, it is recommended to install NVIDIA CUDA Toolkit 12.9 from the following link:

  [https://developer.nvidia.com/cuda-12-9-0-download-archive](https://developer.nvidia.com/cuda-12-9-0-download-archive)

- After installation, verify CUDA version with:

```bash
nvcc --version
```

> Recommended: `>= cuda_12.9.0_571.96`

- Restart your PC after installation.

---

## ✅ 2. Install Required Python Packages

Open `cmd` inside `ComfyUI_windows_portable` and run these 5 commands one at a time:

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

## ✅ 3. Install PyTorch Nightly with CUDA

From `ComfyUI_windows_portable` folder:

```bash
.\python_embeded\python.exe -m pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu129 --upgrade
```

> ⚠️ Note: you can also install the nightly version of PyTorch using the following command, which includes the latest features and updates. However, this version may cause compilation issues with SageAttention, so use it at your own risk:

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

⚠️ If you are unable to install Visual Studio Build Tools 2022 (for example, due to incompatibility with older versions of Windows), you can download the pre-compiled whl file included in the release.

---

## ✅ 6. Clone and Install SageAttention

- IF you have installed Visual Studio Build Tools 2022

  From the `ComfyUI_windows_portable` folder:

  ```bash
  git clone https://github.com/thu-ml/SageAttention
  ```

  Then from `ComfyUI_windows_portable\SageAttention` run:

  ```bash
  ..\python_embeded\python.exe -m pip install .
  ```

- IF you downloaded the whl file in step 5, you can place it directly inside the ComfyUI_windows_portable folder. Open the terminal inside that folder and use this command to install the file

  .\python_embeded\python.exe -m pip install “name of whl file”

  Example:

  ```bash
  .\python_embeded\python.exe -m pip install sageattention-2.2.0-cp312-cp312-win_amd64.whl
  ```

## 🎉🎊 Installation completed!

To use Sage Attention, add the --use-sage-attention flag to the startup .bat file or add the Patch Sage Attention KJ node to your workflow!
