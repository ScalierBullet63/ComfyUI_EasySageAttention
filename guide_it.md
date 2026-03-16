# 🔧 Guida all'Installazione: SageAttention + Triton per ComfyUI

## 📚 Sommario

- [1. Installa i driver GPU e NVIDIA CUDA Toolkit](#-1-installa-i-driver-gpu-e-nvidia-cuda-toolkit)
- [2. Installa Visual Studio Build Tools 2026](#-2-installa-visual-studio-build-tools-2026)
- [3. Installa i pacchetti Python richiesti](#-3-installa-i-pacchetti-python-richiesti)
- [4. Installa PyTorch con supporto CUDA](#-4-installa-pytorch-con-supporto-cuda)
- [5. Installa Triton](#-5-installa-triton)
- [6. Clona e installa SageAttention](#-6-clona-e-installa-sageattention)
- [7. Installazione completata!](#-installazione-completata)

---

## ✅ 1. Installa i driver GPU e NVIDIA CUDA Toolkit

- Scarica l'ultima versione dei driver NVIDIA tramite [NVIDIA App](https://www.nvidia.com/it-it/software/nvidia-app/) o tramite il [sito NVIDIA](https://www.nvidia.com/it-it/drivers/).

- Se non vuoi compilare SageAttention per risparmiare tempo e installare meno software a sistema salta al [punto 3](#3-installa-i-pacchetti-python-richiesti), altrimenti prosegui qui sotto.

  > ⚠️ Nota: è stata da poco rilasciata la versione 13.0 di NVIDIA CUDA Toolkit che non sembra al momento essere compatibile con PyTorch e SageAttention. Il consiglio è dunque quello di installare NVIDIA CUDA Toolkit 12.9 al seguente link:

  [https://developer.nvidia.com/cuda-12-9-0-download-archive](https://developer.nvidia.com/cuda-12-9-0-download-archive)

- Dopo l'installazione, verifica la versione di CUDA con:

  ```bash
  nvcc --version
  ```

  > Raccomandato: `>= cuda_12.9.0_571.96`

- Riavvia il PC dopo aver completato l'installazione.

---

## ✅ 2. Installa Visual Studio Build Tools 2026

Installa il workload **Desktop development with C++**.

Link: [https://visualstudio.microsoft.com/visual-cpp-build-tools/](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

> L'installazione completa è necessaria solo per la compilazione.

⚠️ Per installare Visual Studio Build Tools 2026 è necessario avere almeno Windows 10 versione 20H1 oppure Windows 11 a partire dalla 21H2.

---

## ✅ 3. Installa i pacchetti Python richiesti

Apri il terminale `CMD` nella cartella `ComfyUI_windows_portable` ed esegui questi 5 comandi, uno alla volta:

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

## ✅ 4. Installa PyTorch con supporto CUDA

Dalla cartella `ComfyUI_windows_portable`, esegui:

```bash
.\python_embeded\python.exe -m pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu129 --upgrade
```

> ⚠️ Nota: puoi installare anche la versione nightly di PyTorch con il comando seguente, che include le ultime funzionalità e aggiornamenti. Tuttavia, questa versione potrebbe causare problemi di compilazione con SageAttention, quindi usala a tuo rischio e pericolo:

```bash
.\python_embeded\python.exe -m pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu129 --upgrade
```

---

## ✅ 5. Installa Triton

Dalla cartella `ComfyUI_windows_portable`, esegui:

```bash
.\python_embeded\python.exe -m pip install triton-windows
```

### 🧹 Aggiungi le cartelle include e libs richieste:

Scarica lo zip corretto in base alla versione di Python che hai in `.\python_embeded` ed estrailo:

- [Python 3.11.x](https://github.com/woct0rdho/triton-windows/releases/download/v3.0.0-windows.post1/python_3.11.9_include_libs.zip)
- [Python 3.12.x](https://github.com/woct0rdho/triton-windows/releases/download/v3.0.0-windows.post1/python_3.12.7_include_libs.zip)
- [Python 3.13.x](https://github.com/woct0rdho/triton-windows/releases/download/v3.0.0-windows.post1/python_3.13.2_include_libs.zip)

Posiziona le cartelle "include" e "libs" estratte dentro:

```
ComfyUI_windows_portable\python_embeded
```

---

## ✅ 6. Clona e installa SageAttention

- SE vuoi compilare SageAttention per avere la massima compatibilità

  Dalla cartella `ComfyUI_windows_portable`, esegui:

  ```bash
  git clone https://github.com/thu-ml/SageAttention
  ```

  Poi dalla cartella `ComfyUI_windows_portable\SageAttention` esegui:

  ```bash
  ..\python_embeded\python.exe -m pip install .
  ```

- SE preferisci evitare di compilare SageAttention

  Cerca tra [questi wheel](https://github.com/woct0rdho/SageAttention/releases) quello adatto alla versione di PyTorch installata in `.\python_embeded` e che vedi all’avvio di ComfyUI nel terminale (CMD).

  > ⚠️ Nota: se non trovi il wheel con la stessa versione di CUDA di PyTorch installato in ComfyUI, potresti provare ad ignorare la versione di CUDA e installare il wheel comunque. Se non ti funziona, puoi cambiare PyTorch in ComfyUI o compilare SageAttention per la tua versione specifica.

  Copia il link del wheel compatibile con la tua configurazione. Poi, dalla cartella `ComfyUI_windows_portable`, esegui:

  ```bash
  .\python_embeded\python.exe -m pip install [url-copiato]
  ```

  > ⚠️ Nota: se hai già SageAttention installato e vuoi aggiornarlo con una versione più recente aggiungi `--upgrade` al comando precedente.

  Esempio:

  ```bash
  .\python_embeded\python.exe -m pip install https://github.com/woct0rdho/SageAttention/releases/download/v2.2.0-windows.post2/sageattention-2.2.0+cu128torch2.8.0.post2-cp39-abi3-win_amd64.whl
  ```

## 🎉🎊 Installazione completata!

Per utilizzare SageAttention aggiungi il flag `--use-sage-attention` al file `.bat` di avvio o aggiungi il nodo [Patch Sage Attention KJ](https://github.com/kijai/ComfyUI-KJNodes) all'interno del tuo workflow!

> Se riscontri problemi, verifica che la versione di PyTorch e CUDA siano compatibili con il wheel o ricompila SageAttention come indicato nel punto 6.
