# 🔧 Guida all'Installazione: SageAttention + Triton per ComfyUI

## ✅ 1. Installa CUDA Toolkit e Driver GPU

- Scarica l'ultima versione del **NVIDIA CUDA Toolkit**:

  > ⚠️ Nota: è stata da poco rilasciata la versione 13.0 di NVIDIA CUDA Toolkit che non sembra al momento essere compatibile con PyTorch e SageAttention. Il consiglio è dunque quello di installare NVIDIA CUDA Toolkit 12.9 al seguente link:

  [https://developer.nvidia.com/cuda-12-9-0-download-archive](https://developer.nvidia.com/cuda-12-9-0-download-archive)

- Dopo l'installazione, verifica la versione di CUDA con:

```bash
nvcc --version
```

> Raccomandato: `>= cuda_12.9.0_571.96`

- Riavvia il PC dopo aver completato l'installazione.

---

## ✅ 2. Installa i pacchetti Python richiesti

Apri il terminale `cmd` nella cartella `ComfyUI_windows_portable` ed esegui questi 5 comandi, uno alla volta:

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

## ✅ 3. Installa PyTorch con supporto CUDA

Dalla cartella `ComfyUI_windows_portable`, esegui:

```bash
.\python_embeded\python.exe -m pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu129 --upgrade
```

> ⚠️ Nota: puoi installare anche la versione nightly di PyTorch con il comando seguente, che include le ultime funzionalità e aggiornamenti. Tuttavia, questa versione potrebbe causare problemi di compilazione con SageAttention, quindi usala a tuo rischio e pericolo:

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

> Si consiglia di fare un'installazione completa dal momento che Triton e SageAttention richiedono degli eseguibili compresi nei Visual Studio Build Tools 2022.

 ⚠️ Per installare Visual Studio Build Tools 2022 è necessario avere almeno Windows 10 versione 1909 oppure Windows 11 a partire dalla 21H2.

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

- SE preferisci evitare di compilare SageAttention puoi scaricare il file whl nelle release e inserirlo direttamente all'interno della cartella ComfyUI_windows_portable. Apri il terminale all'interno di quella cartella e utilizza questo comando per installare il file

  .\python_embeded\python.exe -m pip install "nome del file whl"

  Esempio:

  ```bash
  .\python_embeded\python.exe -m pip install sageattention-2.2.0-cp312-cp312-win_amd64.whl
  ```

## 🎉🎊 Installazione completata!

Per utilizzare il sage attention aggiungi il flag --use-sage-attention al file .bat di avvio o aggiungi il nodo Patch Sage Attention KJ all'interno del tuo workflow!
