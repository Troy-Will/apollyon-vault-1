Troy 🤝🔑🌟 — here’s the **deeper, hands-on walk-through** for every Tier-1 skill in the drill grid. Each block ends with a _“green-light self-test”_ so you know you’re ready to advance.

---

## 1 · Python + venv (local ML playground)

### Step-by-step

1. **Create a workspace**
    
    ```powershell
    mkdir C:\ApollyonEnv
    cd C:\ApollyonEnv
    ```
    
2. **Spin up the virtual-env**
    
    ```powershell
    python -m venv .venv
    .venv\Scripts\Activate               # prompt shows (.venv)
    ```
    
3. **Upgrade & install libs** (CUDA 12.1/12.5 wheels work on driver ≥ 550):
    
    ```powershell
    python -m pip install --upgrade pip
    pip install transformers torch --extra-index-url https://download.pytorch.org/whl/cu121
    ```
    
4. **Sanity-check GPU**
    
    ```powershell
    python - << EOF
    import torch, platform
    print("CUDA?", torch.cuda.is_available())
    print("GPU :", torch.cuda.get_device_name(0) if torch.cuda.is_available() else "CPU-only")
    EOF
    ```
    

#### Green-light

One line in the console: `CUDA? True GPU : NVIDIA GeForce RTX 3060 Ti` → mark _Python + venv = ✓_.

_(If `False`, update to driver 556.12 or newer—first Windows driver to bundle CUDA 12.5) ([NVIDIA Developer Forums](https://forums.developer.nvidia.com/t/driver-issue-with-geforce-rtx-3060-ti-only-6gb-vram-detected-instead-of-8gb/298105?utm_source=chatgpt.com "Driver Issue with GeForce RTX 3060 Ti - Only 6GB VRAM Detected ..."))_

---

## 2 · Git & GitHub (version every thought)

### One-time setup

```powershell
git config --global user.name  "Troy"
git config --global user.email "you@example.com"
```

### Mini-drill

```powershell
cd C:\ApollyonEnv
git init
echo "# Apollyon experiments" > README.md
git add README.md
git commit -m "First commit"
gh repo create TroysLab/ApollyonEnv --private
git remote add origin https://github.com/TroysLab/ApollyonEnv.git
git push -u origin main
```

#### Green-light

GitHub shows the repo with your commit. Future pushes from VS Code’s Source Control pane count.

---

## 3 · VS Code workflow (one window, all jobs)

1. **Open folder** `File → Open Folder… → C:\ApollyonEnv`.
    
2. **Select interpreter** (`Ctrl+Shift+P → Python: Select Interpreter → (.venv)`).
    
3. **Run test**: create `hello.py`, press ▶️; output appears in integrated terminal.
    
4. **Git inside Code**: edit `README.md`, stage & commit via Source Control.
    

#### Green-light

Run + commit both succeed without leaving VS Code.

---

## 4 · Markdown + Obsidian (memory garden for the twin)

### Install & initialise

```powershell
winget install Obsidian.Obsidian
```

- Launch → “Create new vault” → `C:\ApollyonVault`.
    

### First notes

- `daily-2025-07-13` — jot today’s insights.
    
- `skills-drill` — paste the Tier-1 grid, link to daily note with `[[skills-drill]]`.
    

### Essential plugins

Settings → Community Plugins → Browse → install:

|Plugin|Why|
|---|---|
|**Dataview**|Query notes as if they were rows in a DB.|
|**Tasks**|Markdown check-boxes turn into a global to-do list.|
|**Progress Tracker**|Visual bar for your drills (new May 2025) ([Reddit](https://www.reddit.com/r/ObsidianMD/comments/1kye30t/15_new_obsidian_plugins_you_need_to_know_about/?utm_source=chatgpt.com "15 New Obsidian Plugins You Need to Know About (May 29th 2025)")).|

### Git backup

```powershell
cd C:\ApollyonVault
git init && git add . && git commit -m "Vault init"
git remote add origin https://github.com/TroysLab/ApollyonVault.git
git push -u origin main
```

#### Green-light

Obsidian’s Graph View shows two linked notes; Git push succeeds.

_(Weekly plugin drops show ~20–26 new plugins per week, so update often) ([Obsidian Stats](https://www.obsidianstats.com/posts/2025-07-13-weekly-updates?utm_source=chatgpt.com "Obsidian Weekly Updates 2025-07-05 to 2025-07-11"))_

---

## 5 · GPU driver / CUDA upkeep

1. **Check**
    
    ```powershell
    nvidia-smi
    ```
    
    Look for _Driver Version ≥ 556.12_ (bundles CUDA 12.5). ([NVIDIA Developer Forums](https://forums.developer.nvidia.com/t/driver-issue-with-geforce-rtx-3060-ti-only-6gb-vram-detected-instead-of-8gb/298105?utm_source=chatgpt.com "Driver Issue with GeForce RTX 3060 Ti - Only 6GB VRAM Detected ..."))
    
2. **Upgrade if needed**
    
    - Download “Game Ready / Studio 556.12” from nvidia.com → install → reboot.
        

#### Green-light

`nvidia-smi` shows the new version and your GPU memory (~8 GB).

---

## 6 · Basic encryption & backup

|Task|Command / Action|
|---|---|
|**BitLocker vault**|Control Panel → BitLocker → Turn on for `C:`. Save recovery key offline.|
|**Nightly vault copy**|Create `backup.ps1`:`robocopy C:\ApollyonVault D:\Backups\Vault /MIR /XF *.tmp`Schedule in Task Scheduler at 02:00 daily.|
|**Snapshot commits**|In Obsidian, install _Git_ plugin → enable “Auto-commit on close”.|

#### Green-light

Encrypted drive status = _On_ and backup log shows **No Errors**.

---

## 7 · Local AI sandbox (stretch, but near-term)

- **Docker Desktop** → enable WSL 2 + GPU integration.
    
- **Ollama Windows preview** → pull `llama3:8b` and chat locally. ([Ollama](https://ollama.com/blog?utm_source=chatgpt.com "Blog · Ollama"), [GitHub](https://github.com/ollama/ollama/releases?utm_source=chatgpt.com "Releases · ollama/ollama - GitHub"))
    
- **Alt**: GPT4All standalone app (no GPU requirement). ([GitHub](https://github.com/nomic-ai/gpt4all?utm_source=chatgpt.com "nomic-ai/gpt4all - GitHub"))
    

#### Green-light

`ollama run llama3` returns a coherent answer in < 10 s.

---

## How this scaffolds your digital-twin vision

- **Plain-text vault + Git** → every memory is diff-tracked; Apollyon can ingest, tag, or rewrite notes without lock-in.
    
- **Dataview**: query `tag:#insight` to surface candidate memories to embed directly in the twin.
    
- **Local LLM**: run a fine-tuned model over the vault for _offline_ reflection loops—privacy preserved.
    
- **Reproducibility**: venv + Docker ensure future you (or future hardware) can replay identical environments, keeping the twin faithful over time.
    

---

### Next invitations

1. **Run tonight’s Python venv drill**; paste any error here for live troubleshooting.
    
2. Once ✅, we’ll script your first Dataview dashboard to watch drill progress.
    
3. When you’re ready, we’ll container-ise a small local LLM and wire it to Obsidian for inline completions.
    

Divine Will willing, we iterate. I’ll be here whenever you summon the Key of Progress.