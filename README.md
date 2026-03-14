# RHyDOS v1.0 // #RAICANDISH

> **Personal GGUF depot terminal.**  
> Drop a GGUF in the folder. Add one line to manifest.json. Push. Done.  
> Built by [Rai Candish](https://www.candish.me) — [isukirirai-hub.github.io/rhydos](https://isukirirai-hub.github.io/rhydos)

---

## The Family

| Terminal | Target | URL |
|---|---|---|
| **RAiDOS** | Metal / WebGPU | [isukirirai-hub.github.io/raidos](https://isukirirai-hub.github.io/raidos) |
| **RyDOS** | CPU / no-GPU | [isukirirai-hub.github.io/rydos](https://isukirirai-hub.github.io/rydos) |
| **RiDOS** | RAM-first / multi-agent | [isukirirai-hub.github.io/ridos](https://isukirirai-hub.github.io/ridos) |
| **RHyDOS** | Personal GGUF depot | [isukirirai-hub.github.io/rhydos](https://isukirirai-hub.github.io/rhydos) |

All hosted at [www.candish.me](https://www.candish.me) — #RAICANDISH

---

## What is RHyDOS?

RHyDOS is your personal GGUF depot. You curate the models. You control what runs.

On boot it reads `models/manifest.json`, displays every model you have committed to the repo, and waits for you to pick one. The selected GGUF loads directly into browser RAM via **wllama** — a lightweight WASM wrapper for llama.cpp that reads `.gguf` files natively, no conversion needed.

Add a model: drop the file in `models/`, add one entry to `manifest.json`, push to GitHub. It appears in the picker on next load.

---

## Current Depot

| Model | File | Size | Params |
|---|---|---|---|
| SmolLM2 114M | `smollm2-135m-instruct-q4_k_m.gguf` | 114.8 MB | 114M |
| TinyLlama 1.1B | `tinyllama-1.1b-chat-v1.0.Q4_K_M.gguf` | 783 MB | 1.1B |

---

## Adding a Model

**1. Drop the `.gguf` into `models/`**

```
models/
├── manifest.json
├── smollm2-135m-instruct-q4_k_m.gguf
├── tinyllama-1.1b-chat-v1.0.Q4_K_M.gguf
└── your-new-model.gguf          ← add here
```

**2. Add one entry to `manifest.json`**

```json
{
  "id":      "your-model-id",
  "file":    "your-new-model.gguf",
  "name":    "Your Model Name",
  "params":  "7B",
  "size_mb": 4200,
  "quant":   "Q4_K_M",
  "arch":    "LLaMA",
  "desc":    "A short description.",
  "context": 4096
}
```

**3. Commit and push**

```bash
git add models/
git commit -m "add your-model-name to depot"
git push
```

The model appears in the picker on next load. That's it.

---

## File Structure

```
rhydos/
├── index.html          — entire application
├── sw.js               — service worker (COOP/COEP headers)
├── _headers            — Netlify/Cloudflare Pages headers
├── README.md
└── models/
    ├── manifest.json   — depot index (edit this to add models)
    ├── smollm2-135m-instruct-q4_k_m.gguf
    └── tinyllama-1.1b-chat-v1.0.Q4_K_M.gguf
```

---

## Runtime

**wllama** — a lightweight WASM build of llama.cpp that runs `.gguf` files directly in the browser.

- No GPU, no Metal, no WebGPU
- Pure CPU via WASM threads
- Works on old Macs, old PCs, phones
- First load fetches the selected GGUF over HTTP — subsequent loads use the browser cache
- Falls back to demo mode if wllama fails to initialise

---

## Commands

| Command | Action |
|---|---|
| `/models` | List all models in the depot |
| `/load [id]` | Switch to a different model |
| `/model` | Show active model info |
| `/depot` | Open depot panel |
| `/look` | Re-describe current location |
| `/go [place]` | Move somewhere |
| `/inv` | Inventory |
| `/lore` | World lore |
| `/visited` | Locations visited |
| `/take [item]` | Pick up item |
| `/drop [item]` | Drop item |
| `/new` | Start new world |
| `/source` | View source code |
| `/debug` | Debug report |
| `/export` | Download index.html |
| `/help` | All commands |

---

## Notes on GitHub Pages + GGUFs

GitHub Pages serves files over HTTPS as static assets. The browser fetches GGUFs the same way it fetches images — via HTTP GET. wllama streams the file into browser RAM as it downloads.

**File size limits:** GitHub has a 100 MB soft limit per file and a 2 GB repo limit. Files over 50 MB should use [Git LFS](https://git-lfs.github.com/). For large GGUFs (500 MB+) Git LFS is recommended.

**Git LFS setup:**
```bash
git lfs install
git lfs track "*.gguf"
git add .gitattributes
git add models/your-large-model.gguf
git commit -m "add large model via LFS"
git push
```

GitHub Free includes 1 GB LFS storage and 1 GB/month bandwidth. GitHub Pro includes more.

---

## Built by

**Rai Candish** — [www.candish.me](https://www.candish.me)

```
#RAICANDISH   #RYCANDISH    #RYANCANDISH
#RAiBios      #RAiOS        #RAiDOS
#RAiBOOT      #RAi          #MKALTRAi
#RAiHISTORY   #MKRAINAME    #METAþORR
#MKCTRLALTDEL #MKALTRAiþeπαραβολή
#RyIsukiri
```

---

## Licence

Do what you want with it.  
The depot is yours.
