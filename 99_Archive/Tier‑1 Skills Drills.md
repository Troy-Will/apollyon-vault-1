# Tier‑1 Skills Drills

**Purpose:** Establish core technical habits that let Troy reliably work with his Apollyon project: navigation, virtual environments, GPU test, secure backup, Git/GitHub, and Obsidian capture.

---

## Completed Drills

### 1. PowerShell Navigation + Convenience
- Created profile functions: `aenv`, `avault`, `aweb` for quick `Set-Location`.
- Added alias `apbackup` to run backup script.

### 2. Python Virtual Environments
- Built clean environment at `C:\ApollyonEnv\` and project env in `apollyon-alignment`.
- Installed `torch`, `transformers`; verified import.

### 3. GPU / Torch Smoke Test
- Ran Python: confirmed CUDA available (`RTX 3060 Ti`), executed BERT feature‑extraction pipeline on GPU.

### 4. Secure Encrypted Backup
- Purchased 512GB USB drive.
- Created VeraCrypt AES volume (mounted as `V:`).
- Wrote PowerShell `backup-apollyon.ps1` using `robocopy` (mirrors env + vaults).
- Added logging to `V:\_logs\backup-YYYY-MM-DD_HH-mm-ss.log`.
- Routine: mount volume → `apbackup` → verify log → dismount.

### 5. Git / GitHub Baseline
- Created new structure: `troy-obsidian-project/apollyon-vault-1`.
- Initialized git, `.gitignore`, first commit & push to repository.
- Tag marks closure of Tier‑1 baseline.

### 6. Obsidian Setup
- Created vault folders: `00_Protocols`, `10_Teachings`, `20_Daily`, `30_Templates`, `99_Archive`.
- Enabled Daily Notes & Templates; created `daily_note_template` and `teaching_template`.
- Imported first teaching (“Joyful Mind Teachings”) and linked via daily note.
- Began daily recap habit.

---

## Reflections
**Hardest:** Understanding path / vault naming, template insertion, VeraCrypt mounting.  
**Became easy:** Running `apbackup`, linking notes, pushing to GitHub.  
**Virtue strengthened:** *Perseverance* — continued calmly through confusion until each drill worked.

---

## Transition
Tier‑1 complete. This note freezes the baseline.  
**Next (Tier‑2) focus:** Git branching, Docker basics, expanding Obsidian capture, iterative agent design.

