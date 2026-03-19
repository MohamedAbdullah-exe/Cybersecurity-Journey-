# Linux Notes

Personal notes from my day-to-day learning.

---

## Navigation

| Command | What it does |
|---------|-------------|
| `pwd` | Shows where you are (print working directory) |
| `ls` | Lists files in current folder |
| `ls -la` | Lists ALL files including hidden ones |
| `cd foldername` | Move into a folder |
| `cd ..` | Go back one folder |
| `cd ~` | Go straight to home directory |

---

## Files & Folders

| Command | What it does |
|---------|-------------|
| `cat filename` | Read a file |
| `cat ./filename` | Read a file with special characters in the name |
| `mkdir foldername` | Create a new folder |
| `rm filename` | Delete a file |
| `rm -r foldername` | Delete a folder and everything inside |
| `cp file destination` | Copy a file |
| `mv file destination` | Move or rename a file |
| `touch filename` | Create an empty file |
| `find / -name filename` | Search for a file |

---

## Reading Files

| Command | What it does |
|---------|-------------|
| `cat file` | Print whole file to screen |
---
## SSH

```bash
# Connect to a remote server
ssh username@hostname -p portnumber

# Example — OverTheWire Bandit
ssh bandit0@bandit.labs.overthewire.org -p 2220

# Exit SSH session
exit
```

---

## Useful Tips

- Highlight text in terminal to copy it (no Ctrl+C — that cancels commands)
- Paste in terminal with `Shift + Ctrl + V`
- Press `Tab` to autocomplete file and folder names
- Press `Up arrow` to cycle through previous commands
- `Ctrl + C` cancels a running command
- `clear` clears the terminal screen

---
## Tricky Filenames
# Spaces in filename — wrap in quotes or use backslash
cat "my file name"
cat my\ file\ name
# Filename starting with dash — use ./ or --
cat ./-
cat -- -
# Tab autocomplete handles weird filenames automatically
# Start typing the name and press Tab — Linux fills the rest
# -- means end of flags, everything after is treated as a filename
