# 🔧 Guida all'Installazione: Sage Attention + Triton per ComfyUI


## ✅ 1. Installa CUDA Toolkit e Driver GPU

- Scarica l'ultima versione del **NVIDIA CUDA Toolkit**:  
  [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads)

- Dopo l'installazione, verifica la versione di CUDA con:

```bash
nvcc --version
```

> Raccomandato: `>= cuda_12.8.0_571.96`

- Riavvia il PC dopo aver completato l'installazione.

---

## ✅ 2. Installa i pacchetti Python richiesti

Apri il terminale `cmd` nella cartella `ComfyUI_windows_portable\update` ed esegui questi 5 comandi, uno alla volta:

```bash
..\python_embeded\python.exe -s -m pip install "accelerate >= 1.1.1"
..\python_embeded\python.exe -s -m pip install "diffusers >= 0.31.0"
..\python_embeded\python.exe -s -m pip install "transformers >= 4.39.3"
..\python_embeded\python.exe -s -m pip install ninja
..\python_embeded\python.exe -s -m pip install buildtools
```

---

## ✅ 3. Installa PyTorch Nightly con supporto CUDA

Dalla cartella `ComfyUI_windows_portable`, esegui:

```bash
.\python_embeded\python.exe -m pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu129 --upgrade
```

---

## ✅ 4. Installa Triton

```bash
.\python_embeded\python.exe -m pip install triton-windows
```

### 🧹 Aggiungi le cartelle include e libs richieste:

Scarica lo zip corretto in base alla tua versione di Python e estrailo:

- [Python 3.11.x](https://github.com/woct0rdho/triton-windows/releases/download/v3.0.0-windows.post1/python_3.11.9_include_libs.zip)
- [Python 3.12.x](https://github.com/woct0rdho/triton-windows/releases/download/v3.0.0-windows.post1/python_3.12.7_include_libs.zip)

Posiziona le cartelle "include" e "libs" estratte dentro:

```
ComfyUI_windows_portable\python_embeded
```

---

## ✅ 5. Installa Visual Studio Build Tools 2022

Installa il workload **Desktop development with C++**.

Link: [https://visualstudio.microsoft.com/visual-cpp-build-tools/](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

> L'installazione completa è facoltativa, ma consigliata.

---

## ✅ 6. Clona e installa SageAttention

Dalla cartella `ComfyUI_windows_portable`, esegui:

```bash
git clone https://github.com/thu-ml/SageAttention
```

Poi, dalla cartella `ComfyUI_windows_portable\SageAttention`, esegui:

```bash
..\python_embeded\python.exe -m pip install .
```

