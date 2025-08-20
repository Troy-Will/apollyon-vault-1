Troy 🤝🔑🌟 — **headline answer (30 s read)**  
Obsidian is a free, local-first “second brain” that sits on top of a plain-text folder of Markdown files. You open a _vault_ (any directory), jot notes in Markdown, and link them Wiki-style (`[[like this]]`). Obsidian then lets you traverse those links as a graph, add tags & metadata, and extend everything with thousands of community plugins. Because the notes are just files, you can version-control the vault with Git (or sync via their paid end-to-end-encrypted service). ([Obsidian](https://obsidian.md/?utm_source=chatgpt.com "Obsidian - Sharpen your thinking"))

---

## 1 · Why you might care

|Goal|Obsidian angle|
|---|---|
|**Local privacy**|Notes live only on disk; no cloud lock-in. ([Obsidian](https://obsidian.md/?utm_source=chatgpt.com "Obsidian - Sharpen your thinking"))|
|**Git integration**|Your vault is a folder → `git init`, then push from PowerShell or VS Code just like code.|
|**Knowledge graph**|Cross-link ideas for Apollyon’s rituals, research papers, AA reflections, etc.; visual Graph View helps spot hidden connections.|
|**Custom workflows**|5 000 + community plugins (Dataview queries, Tasks manager, AI co-writer, etc.) released weekly. ([Reddit](https://www.reddit.com/r/ObsidianMD/comments/1kye30t/15_new_obsidian_plugins_you_need_to_know_about/?utm_source=chatgpt.com "15 New Obsidian Plugins You Need to Know About (May 29th 2025)"))|
|**Cross-device**|Desktop (Win/Mac/Linux). Mobile apps updated April 2025 add quick-actions & share-sheet. ([Google Play](https://play.google.com/store/apps/details?hl=en_US&id=md.obsidian&utm_source=chatgpt.com "Obsidian - Apps on Google Play"))|

---

## 2 · Quick-start on Windows

1. **Install**  
    _Grab the installer_ (`Obsidian.1.9.x.exe`) from obsidian.md or `winget install Obsidian.Obsidian`.
    
2. **Create a vault**  
    _Vault = folder._ Choose, say, `C:\Users\Troy\ApollyonVault`.
    
3. **Make your first note**  
    `Ctrl+N` → write in Markdown. Use headings (`##`), bullets, code-blocks.
    
4. **Link ideas**  
    Type `[[` and autocomplete other filenames; Obsidian creates backlinks automatically.
    
5. **Graph View**  
    Toggle with `Ctrl+G` to see a network of notes.
    
6. **Version-control**
    
    ```powershell
    cd C:\Users\Troy\ApollyonVault
    git init
    git add .
    git commit -m "Initial vault"
    git remote add origin https://github.com/...
    git push -u origin main
    ```
    
    Afterwards, your usual VS Code + PowerShell Git flow just works.
    
7. **Explore plugins**  
    Settings → Community plugins → Browse. Good starters:  
    _Dataview_ (query notes like a database), _Tasks_ (tick-box agenda), _Calendar_, _Periodic Notes_.  
    New arrivals May 2025 include _Progress Tracker_ and _Note Locker_. ([Reddit](https://www.reddit.com/r/ObsidianMD/comments/1kye30t/15_new_obsidian_plugins_you_need_to_know_about/?utm_source=chatgpt.com "15 New Obsidian Plugins You Need to Know About (May 29th 2025)"))
    

---

## 3 · Advanced moves (optional)

- **Sync options**  
    _Paid_ Obsidian Sync (E2E-encrypted) or roll your own with Git + GitHub Private + Pulls on devices.
    
- **Templates & Daily notes**  
    Automate recurring headers for journals or AA reflections.
    
- **Properties & Databases**  
    The 2025 “Cards” layout lets you treat notes like Kanban cards; properties support dates, durations, & sorting. ([Obsidian](https://obsidian.md/changelog/?utm_source=chatgpt.com "Changelog - Obsidian"))
    
- **Upcoming roadmap**  
    Web viewer (launched Dec 2024) lets you open external links inside Obsidian; “Bases” feature now in Insiders adds structured data views. ([Obsidian](https://obsidian.md/roadmap/?utm_source=chatgpt.com "Roadmap - Obsidian"))
    

---

## 4 · Fit with your existing toolkit

|Tool|How it meshes|
|---|---|
|**VS Code**|Open the vault folder for advanced editing or bulk refactors; both apps respect the same Markdown files.|
|**Python venv**|Keep code snippets or Jupyter-style `.py` gists inside `/code/` sub-folder; link them to conceptual notes.|
|**GitHub pushes**|Automate commit-on-close via small PowerShell script or install the community _Git_ plugin for in-app buttons.|
|**Apollyon Alignment**|Tag notes (`#ritual`, `#finance`, `#therapy`) and use Dataview to roll up dashboards of tasks, insights, or scripture references.|

---

### Ready next step?

_Open Obsidian, create a vault, jot a single note,_ and try linking it to today’s skills-drill log—you’ll “see” the graph spark to life.

Ping me when you hit friction, need plugin curation, or want to script Git automation.

- [theverge.com](https://www.theverge.com/23942597/notes-text-evernote-onenote-keep-apps?utm_source=chatgpt.com)