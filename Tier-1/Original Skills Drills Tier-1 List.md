**Troy 🤝🔑🌟—core skill checklist (first-pass)**

|Tier|Why it matters to _Apollyon_|1-hour “proof you can do it” test|
|---|---|---|
|**Shell fundamentals** (PowerShell / bash)|Every script, Git command, or model-launch starts here.|Navigate to a project folder, list files, and pipe the output to a text file (`ls \| Out-File files.txt`). ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Command_line?utm_source=chatgpt.com "Command line crash course - Learn web development \| MDN"))|
|**Python + venv**|Lets you run / tweak model-training code without polluting your main system.|Create a virtual-env, install `transformers`, and run `python -c "import transformers, torch; print(torch.cuda.is_available())"`. ([Python Documentation](https://docs.python.org/3/tutorial/venv.html?utm_source=chatgpt.com "12. Virtual Environments and Packages — Python 3.13.5 ..."))|
|**Git & GitHub**|Version-controls your “Memory Garden” notebooks _and_ your twin’s fine-tune scripts.|Clone a repo, commit a change, push to a private GitHub repo. ([git-scm.com](https://git-scm.com/docs/gittutorial?utm_source=chatgpt.com "gittutorial Documentation - Git"))|
|**VS Code workflow**|Single environment for Python, Markdown, and Git; cuts friction.|Open VS Code, attach to your venv, run a `.py` file, stage a commit—all inside the editor. ([Visual Studio Code](https://code.visualstudio.com/docs/introvideos/basics?utm_source=chatgpt.com "Getting started with Visual Studio Code"))|
|**Markdown + Obsidian**|Your long-term knowledge base and twin-training corpus.|Create a new note, use headings, links, and tags; confirm it appears in the graph view. ([Obsidian Help](https://help.obsidian.md/create-note?utm_source=chatgpt.com "Create your first note - Obsidian Help"))|
|**GPU driver / CUDA upkeep**|Keeps local model inference fast and stable.|Verify `nvidia-smi` shows your GPU; install/upgrade CUDA toolkit if a model fails to load.|
|**Basic encryption & backup**|Protects the very data that _is_ you.|Use VeraCrypt or BitLocker to encrypt your Obsidian vault and schedule a nightly copy to an external drive.|

---

### How to use this table

1. **Self-score** each test (✓ / ✗ / “need help”).
    
2. Tell me where the ✗’s are; I’ll drop targeted mini-guides or scripts.
    
3. Once Tier-1 is solid, we can add _next-level_ items: Docker, Hugging Face Hub CLI, cloud GPU rentals, basic REST-API hacking.
    

_Ready when you are to zoom in on any cell._