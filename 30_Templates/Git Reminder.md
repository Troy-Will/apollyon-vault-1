# 1) Go to the vault repo
avault    # or: cd "$HOME\Documents\troy-obsidian-project\apollyon-vault-1"

# (sanity checks)
git rev-parse --is-inside-work-tree
git remote -v
git status

# 2) Stage changes (new & modified files)
git add -A    # (-A stages deletions too)

# 3) Commit (use today’s date in the message)
$d = (Get-Date).ToString('yyyy-MM-dd')
git commit -m "chore(daily): note + backup log link ($d)"

# 4) Push to GitHub
git push      # if upstream not set: git push -u origin main
