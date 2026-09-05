# LlamaManager — llama.cpp Model Manager

[English](README.md) | [简体中文](README.zh-CN.md)

A **single-file Windows desktop tool** to manage your local GGUF models and launch them with [llama.cpp](https://github.com/ggml-org/llama.cpp)'s `llama-server` — no command line needed.

> Current version: **v1.28.0** (download from the **Releases** section)

---

## Features

- **Manage a local GGUF model library**: add / swap / duplicate / delete / open folder; reorder the list by dragging rows, using the ↑/↓ buttons or the context menu (order is auto-saved).
- **Multiple "launch profiles" per model**: port, context length, GPU layers, sampling, reasoning, cache and dozens of other parameters in any combination, switchable with one click. The profile name doubles as the llama-server alias (`-a`).
- **Visual config, official defaults by default**: every parameter is a unified dropdown — the default value is shown inline and is *not* written to the command line; custom values are highlighted. Each row's label shows the exact argument/value that will actually be sent.
- **Built-in official parameter reference** translated to match your UI language (Simplified Chinese / English).
- **One-click start + live logs**: per-argument command preview (copyable); run **multiple servers concurrently** (different models/profiles, each with its own log panel).
- **OpenAI-compatible API out of the box**: copy the API base URL / alias / API key, open it in a browser, or test it with the built-in chat dialog.
- Light / dark themes. **On first launch the UI language follows your OS language**; you can pin Simplified Chinese or English in Settings later.

## Requirements

- Windows 10 / 11 (x64)
- You need **llama-server** (from llama.cpp) yourself:
  - Official download: [ggml-org/llama.cpp Releases](https://github.com/ggml-org/llama.cpp/releases) — pick a `-bin-win-` archive (`-cuda-` for NVIDIA, `-vulkan-` for AMD/Intel)
  - Or use "Settings → Auto-detect" inside the app
- A local model file in `.gguf` format

## Quick start

1. Download `LlamaManager-1.28.0-win64.exe` from the Releases section (optionally verify it against the `.sha256` file in the same release).
2. Run it — a single file, no installation.
3. The UI language follows your system on first launch; set the `llama-server.exe` path in **Settings**.
4. Click **Add model** and pick your `.gguf` file (quantization / architecture / size are read automatically).
5. Configure a profile on the right, then press the orange **Start** button and wait until the status turns to "Running".
6. Copy the API base URL (e.g. `http://127.0.0.1:8080`) and connect any OpenAI-compatible client.

## Where is my data stored?

Everything you configure is saved to the **user data directory** (not next to the exe):

```
%APPDATA%\LlamaManager\
├─ profiles.json   models + all launch profiles (the important one)
└─ settings.json   global settings (server path / language / theme…)
```

To move to another machine, just copy the whole `%APPDATA%\LlamaManager\` folder. Individual profiles can also be exported/imported from the UI.

## Verify the download (optional)

```powershell
# Windows PowerShell
Get-FileHash .\LlamaManager-1.28.0-win64.exe -Algorithm SHA256
# The result should match the value in LlamaManager-1.28.0-win64.exe.sha256
```

## FAQ

- **Server exits right after start / "port in use"**: check the server log and pick another free port.
- **GPU not used**: download the CUDA/Vulkan build of `llama-server` and set a value > 0 for "GPU layers".
- **Antivirus false positive**: single-file executables built with PyInstaller are occasionally flagged; add an exclusion.

## Source code

Only the compiled program is published for now. **The source code will be open-sourced when ready** — watch this repository.

---

Powered by [llama.cpp](https://github.com/ggml-org/llama.cpp) — local LLM management & launcher.
