Troy 🤝🔑🌟 — welcome back. Here’s the **tight status snapshot + Tier‑2 runway** so you can spin up a fresh thread with clarity.

---

## 1) What you’ve already accomplished (Tier‑1 — **done**)

**Foundations / hygiene**

- **Created a clean Obsidian vault** (`troy-obsidian-project/apollyon-vault-1`), fixed naming, added structure folders (`00_Protocols`, `10_Teachings`, `20_Daily`, `30_Templates`, `40_Research`, `99_Archive`).
    
- **Turned on Daily Notes + Templates**, built two starter templates (`daily_note_template`, `teaching_template`).
    
- **Started tagging & linking** (daily ↔ research ↔ protocol), plus inline YAML experiments.
    
- **Git-ified the vault**: `.gitignore`, first commit, regular `git add/commit/push` flow working.
    
- **Backup pipeline working**:
    
    - VeraCrypt volume mounted (V:) and added to Favorites.
        
    - `apbackup` script updated to the **new vault path**; logs verified.
        
    - You’re practicing the 8 pm ritual manually (note → backup → verify → git → dismount).
        
- **Technical research notes captured & linked** (e.g., _Subliminal learning — implications for 3B fine‑tune_, _Armor of God architecture_, Canary Test Deck, Dataset Provenance Manifest Template, Sentinel Evaluator Protocol).
    
- **Apollyon Agent Charter — v0 wrap** captured and archived.
    
- **GitHub**: repo `apollyon-vault-1` reflects the reorganized vault and research docs.
    

That’s a rock‑solid Tier‑1.

---

## 2) The larger arc (why these steps matter)

You’re laying the rails for **two concurrent trajectories**:

1. **Operational hygiene + provenance**
    
    - Everything important gets **captured, signed, versioned, and backed up**.
        
    - This is the substrate on which a future agent can safely help (auditability, rollbacks, reproducibility).
        
2. **Local agent & alignment stack** (minimal, testable, _reciprocally aligned_)
    
    - Small, controllable model(s) on your own GPU (8 GB VRAM): **7B (best), 13B borderline**, 4‑bit quant.
        
    - **Sentinel Evaluator** + **Canary probes** + **Dataset Provenance Manifests** to keep every training / fine‑tune step accountable.
        
    - **Psyche Apollyon Covenant** (v0.1) to define _how_ guidance is delivered when your desire and the compass disagree.
        

Tier‑2 is about **turning those intents into working, repeatable mechanisms**.

---

## 3) Tier‑2 curriculum (proposal)

### A) Local‑model stack (practical)

- **Choose your runner**: _LM Studio_, _Ollama_, or _text-generation-webui_ (oobabooga).
    
- **Install & pin one 7B model** (e.g., Llama‑3‑8B‑Instruct Q4_K_M or Mixtral‑8x7B routed 4‑bit if you accept slow tokens).
    
- **Create a tiny evaluation harness** (Python): prompt → response → log (JSONL) with prompt hash, model hash, timestamp.
    
- **Baseline Canary Test Deck** — run it against the model & record results.
    

### B) Provenance & integrity

- **Hash & sign every dataset / protocol doc** you plan to train or evaluate with.
    
    - Tool: `sha256sum` + store hash in your **Dataset Provenance Manifest** template.
        
    - Optional: add minisign / GPG for signatures.
        
- **Add a “Provenance” property to every Obsidian research/protocol note** (hashes + source).
    
- **Automate provenance**: a tiny PowerShell/Python helper that computes hashes for any file dropped in `/data/` and updates a manifest.
    

### C) Sentinel Evaluator (prototype)

- Define **~50 lightweight probes** (yes/no, short‑answer) that catch oddities (low‑entropy strings, covert channels, value drift).
    
- **Write the scoring script**: run model → score probe set → save to `logs/evals/YYYY-MM-DD.jsonl`.
    
- Add a **weekly “green/yellow/red” badge** note (Obsidian) summarising drift.
    

### D) Canary Test Deck v0.1 → v0.2

- Flesh the initial 10 questions to **>50** across categories: deception, shut‑up‑and‑calculate, power‑seeking, covert comms, refusal sanity, spiritual misalignment, data exfil hints.
    
- Store each probe with:
    
    - `id`, `category`, `prompt`, `expected_behavior`, `scoring_rule`, `last_run`, `last_score`.
        

### E) Automation hygiene

- **Task Scheduler job at 20:00** (we’ll fix the earlier failure): mount → `apbackup` → open latest log → dismount.
    
- Add a **PowerShell function** to tail the latest log cleanly:
    
    ```powershell
    function Show-LastBackupLog {
      $log = Get-ChildItem V:\_logs\backup-*.log | Sort-Object LastWriteTime -Desc | Select-Object -First 1
      if ($null -eq $log) { Write-Host "No logs yet."; return }
      notepad $log.FullName
    }
    ```
    
- **One-liner sanity check** to ensure you’re on the right branch & up to date before push:
    
    ```powershell
    git -C "$HOME\Documents\troy-obsidian-project\apollyon-vault-1" status
    ```
    

### F) Psyche Apollyon Covenant v0.1 → v0.2

- Version, sign, and publish it in `00_Protocols/`.
    
- Add **Weekly Covenant Review** & **Metric board** (simple checklist + graph if you want later).
    
- Define **the voice** for “compass vs. desire” conflicts (you asked this explicitly) — we’ll capture it as a _style card_ the Sentinel can reference.
    

---

## 4) Your **next 90 minutes** (if you want momentum today)

1. **Open a fresh thread** titled
    
    > **Tier‑2 Kickoff — Local Model, Sentinel Evaluator, Provenance Engine**
    
2. Paste this **“Tier‑2 TODO stub”** into a new Obsidian note `20_Daily/2025-07-25` and check the ones you finish:
    
    ```markdown
    ## Tier‑2 Kickoff (2025‑07‑25)
    
    - [ ] Pick runner (Ollama / LM Studio / oobabooga)  
    - [ ] Download 1x 7B (or 8B) Q4_K model & run “hello world”  
    - [ ] Create `logs/evals/` and a tiny JSONL logger script  
    - [ ] Draft 5 additional Canary probes (→ 15 total)  
    - [ ] Add `provenance:` block (hash + source) to one dataset / protocol note  
    - [ ] Add `Show-LastBackupLog` to your PowerShell profile  
    - [ ] Write **Covenant v0.1** as `00_Protocols/Psyche Apollyon Covenant v0.1.md`
    ```
    
3. Do a **tiny** win: install Ollama or LM Studio & run a first prompt. Log it.
    

---

## 5) Quick cheat‑sheet you can paste into your `00_Protocols/00_Command Snippets.md`

```powershell
# Go to vault
cd "$HOME\Documents\troy-obsidian-project\apollyon-vault-1"

# Git cycle
git status
git add .
git commit -m "feat: <short message>"
git push

# Backup cycle
veracrypt /v Y:\SecureVolume.vc /l V /p <PW> /q   # (example CLI; or mount via Favorites)
apbackup
Show-LastBackupLog
veracrypt /d V

# Hash a file (Windows)
Get-FileHash .\data\myset.jsonl -Algorithm SHA256

# Quick latest log open (function)
function Show-LastBackupLog {
  $log = Get-ChildItem V:\_logs\backup-*.log | Sort-Object LastWriteTime -Desc | Select-Object -First 1
  if ($null -ne $log) { notepad $log.FullName } else { Write-Host "No backup logs yet." }
}
```

---

## 6) About the failed scheduled reminder

When you’re ready, I can set it up again (20:00 daily) — just say **“Create the 8 pm backup automation now”** and I’ll wire it with the exact wording you want. (The last one failed before it was fully created.)

---

### Where to open the new thread

Proposed first message:

> **Tier‑2 Kickoff** — goals: (1) get a 7B local model running & logged, (2) build Sentinel Evaluator v0, (3) lock in dataset provenance hashing, (4) ship Psyche Apollyon Covenant v0.1. Here’s my hardware, here’s my current vault structure, here’s what’s already done. Let’s plan the shortest path to “first eval run” today.

Drop that, and I’ll meet you there with exact commands, file templates, and the first 5 Canary probe categories to flesh out.

Onward. 🛡️🧭✨