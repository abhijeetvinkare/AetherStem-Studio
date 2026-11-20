# AetherStem Studio — AI Audio & Stem Workstation

**AetherStem Studio** is a fast, local-first AI audio separation and YouTube extraction workstation built with Python, FastAPI, `audio-separator` (UVR MDX-Net & Meta Demucs), and `yt-dlp`. It runs completely offline after initial model download and launches in a clean, borderless desktop window.

---

## Features

- **3 Tailored Extraction Modes:**
  - **Karaoke & Singing (Fastest):** Separates clean **Vocals** and full **Karaoke Instrumental** (`UVR-MDX-NET-Inst_HQ_3`).
  - **Drums, Bass & Band:** Isolates **Drums**, **Bass**, **Vocals**, and **Other**, plus auto-generates a ready-to-play **Drums + Bass** rhythm backing track (`htdemucs`).
  - **Guitar, Piano & Full Band:** Extracts **Piano/Keys**, **Guitar**, **Drums**, **Bass**, and **Vocals**, plus auto-generates a **No-Keys** backing track (`htdemucs_6s`).
- **Batch Local & YouTube Queue:** Drag and drop multiple local files (`MP3`, `WAV`, `FLAC`, `M4A`, `MP4`) or paste YouTube URLs directly into the processing queue.
- **In-Browser Audio Preview & ZIP Export:** Audition individual stems right inside the workspace or download all separated stems in a single ZIP archive.
- **Native Desktop Experience:** Launches via `Start_AetherStem.bat` into borderless Chrome/Edge App Mode with automatic port checking.

---

## Prerequisites

1. **Windows 10 / 11**
2. **Python 3.10 or 3.11** (Make sure **"Add Python to PATH"** is checked during installation) — [Download Python](https://www.python.org/downloads/)
3. **Google Chrome** or **Microsoft Edge** (used for borderless App Mode window)
4. **FFmpeg** (automatically installed by `setup.bat` via `winget`, or manually via `winget install Gyan.FFmpeg`)

---

## Quick Setup & Launch

### Step 1: Clone or Download the Repository
```bash
git clone https://github.com/abhijeetvinkare/AetherStem-Studio.git
cd AetherStem-Studio
```
*(Or click **Code → Download ZIP** on GitHub and extract the folder.)*

### Step 2: Run One-Time Setup (`setup.bat`)
Double-click **`setup.bat`**.  
This automatically:
1. Creates a clean local Python virtual environment (`venv`).
2. Installs FastAPI, Uvicorn, `yt-dlp`, and `audio-separator` from `requirements.txt`.
3. Checks if FFmpeg is installed and installs it via `winget` if missing.

### Step 3: Launch AetherStem Studio (`Start_AetherStem.bat`)
Double-click **`Start_AetherStem.bat`**.  
- The backend engine starts minimized in the background on `http://127.0.0.1:8000`.
- Within 2–3 seconds, the **AetherStem Studio** desktop window opens automatically.

> **First-Run Note:** The very first time you run a separation in each mode, the corresponding AI model (~65 MB – 200 MB) downloads automatically into the local `models/` folder. All future runs work 100% offline.

---

## Optional: Create a Desktop Shortcut with Custom Icon

1. Right-click **`Start_AetherStem.bat`** → **Send to → Desktop (create shortcut)**.
2. Right-click the new Desktop shortcut → **Properties → Change Icon... → Browse...**
3. Select **`app.ico`** inside your `AetherStem-Studio` folder and click **OK → Apply**.
4. Rename the shortcut to **AetherStem Studio** (and optionally right-click → **Pin to taskbar**).

---

## Optional: NVIDIA GPU Acceleration (CUDA)

By default, `requirements.txt` installs the CPU version of ONNX Runtime, which works on any PC. If you have an NVIDIA GPU and CUDA installed, you can speed up separation significantly by activating `venv` and running:

```bash
venv\Scripts\activate
pip uninstall -y onnxruntime
pip install onnxruntime-gpu
```

---

## Project Structure

```text
AetherStem-Studio/
├── setup.bat             # One-time environment, dependency & FFmpeg installer
├── Start_AetherStem.bat  # One-click desktop App Mode launcher
├── server.py             # FastAPI backend, YouTube downloader & AI stem engine
├── index.html            # Single-page studio UI
├── tailwind.js           # Offline Tailwind CSS bundle
├── requirements.txt      # Python package dependencies
├── app.ico               # Custom multi-resolution application icon
└── .gitignore            # Excludes local models, venv, and temporary cache
```

---

## Troubleshooting

- **Browser window doesn't open:** Ensure Chrome or Edge is installed, or manually open `http://127.0.0.1:8000` in any browser while the minimized `AetherStem Engine` terminal is running.
- **FFmpeg error during audio conversion:** Open PowerShell/Command Prompt and run `winget install Gyan.FFmpeg`, then restart your terminal/app.
- **YouTube download fails:** Update `yt-dlp` inside your virtual environment by running `venv\Scripts\pip install -U yt-dlp`.
