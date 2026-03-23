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
Spaces in filename — wrap in quotes or use backslash
cat "my file name"
cat my\ file\ name
Filename starting with dash — use ./ or --
cat ./-
cat -- -
Tab autocomplete handles weird filenames automatically
Start typing the name and press Tab — Linux fills the rest
-- means end of flags, everything after is treated as a filename

## find command
find . -type f              # all files in current folder


## What is sudo?

`sudo` = "superuser do" — runs a command as the administrator (root).
Root is the most powerful user in Linux. Root can do ANYTHING.
sudo gives you that power temporarily for one command.

```
Normal user → limited powers
Root user   → unlimited powers
sudo        → borrow root powers for one command
```

---

## sudo basics

| Command | What it does |
|---------|-------------|
| `sudo command` | Run a command as root |
| `sudo su` | Switch to root user permanently |
| `sudo su -` | Switch to root with root's environment |
| `exit` | Leave root and go back to normal user |
| `whoami` | Check who you are currently logged in as |

### Example
```bash
whoami              # shows your username
sudo whoami         # shows "root"
sudo apt update     # update packages as root
```

---

## Why sudo matters for hacking

When you compromise a system, you start with a low privilege user.
The goal is always to get root — called "privilege escalation."
Understanding how sudo works helps you:
- Find misconfigured sudo permissions on target systems
- Exploit sudo vulnerabilities
- Escalate your privileges from normal user to root

```bash
sudo -l    # list what sudo commands current user can run
           # this is one of the first things pentesters check!
```

---

## User management

| Command | What it does |
|---------|-------------|
| `whoami` | Show current username |
| `id` | Show user ID, group ID and groups |
| `cat /etc/passwd` | List all users on the system |
| `cat /etc/shadow` | List password hashes (root only) |
| `sudo adduser username` | Create a new user |
| `sudo deluser username` | Delete a user |
| `su username` | Switch to another user |
| `sudo passwd username` | Change a user's password |

### Example
```bash
id                      # uid=1000(kali) gid=1000(kali)
cat /etc/passwd         # see all users
sudo adduser hacker     # create user called hacker
su hacker               # switch to hacker user
```

---

## Groups

Groups control what users can and can't do.
Adding a user to a group gives them extra permissions.

| Command | What it does |
|---------|-------------|
| `groups` | Show groups current user belongs to |
| `groups username` | Show groups a specific user belongs to |
| `sudo usermod -aG groupname username` | Add user to a group |
| `cat /etc/group` | List all groups on the system |

### Important groups
| Group | What it allows |
|-------|---------------|
| `sudo` | Run sudo commands |
| `root` | Full system access |
| `www-data` | Web server access |
| `shadow` | Read password hashes |

### Example
```bash
# Add user to sudo group (gives them sudo power)
sudo usermod -aG sudo username
```

---

## /etc/passwd explained

This file lists every user on the system. Format:
```
username:x:UID:GID:comment:home:shell
root:x:0:0:root:/root:/bin/bash
kali:x:1000:1000:Kali:/home/kali:/bin/bash
```
- UID 0 = root (most powerful)
- UID 1000+ = regular users
- Shell `/bin/bash` = can log in
- Shell `/bin/false` = cannot log in (service accounts)

---

## /etc/shadow explained

Stores password hashes — only root can read this.
```
username:$hash:lastchange:min:max:warn:inactive:expire
```
 if you can read `/etc/shadow`, you can crack the hashes offline using tools like `hashcat` or `john`.

```bash
cat /etc/shadow          # needs root
sudo cat /etc/shadow     # works if you have sudo
```

---

## Hacking relevance — privilege escalation

```bash
# Step 1 — check who you are
whoami

# Step 2 — check your sudo permissions
sudo -l

# Step 3 — check what groups you're in
id

# Step 4 — look for users on the system
cat /etc/passwd

# Step 5 — if you have root, grab shadow hashes
sudo cat /etc/shadow
```

This exact sequence is what pentesters run after getting initial access to a system.

---

## Quick reference

| Command | Pentesting use |
|---------|---------------|
| `sudo -l` | Check for privilege escalation opportunities |
| `cat /etc/passwd` | Enumerate users on target system |
| `cat /etc/shadow` | Grab password hashes if root access |
| `id` | Check current privileges |
| `su username` | Lateral movement between users |


find . -name "filename"     # find by name

find . -size 1033c          # find by size in bytes

find . -readable            # human readable files only

find . -type f -size 1033c -readable  # combine conditions


## 2>/dev/null — hiding errors

Redirects error messages to the trash bin
Use it to clean up messy output

# Without it — wall of "Permission denied" errors
# With it — only clean results show

find / -user bandit7 -group bandit6 -size 33c 2>/dev/null


## grep — searching inside files

Find lines containing a specific word

grep "word" filename            # basic search
cat file | grep "word"          # pipe into grep
grep -i "word" file             # ignore uppercase/lowercase
grep -n "word" file             # show line numbers too
grep -r "word" .                # search all files in folder


## Pipe |

Connects two commands together
Takes output of first command and feeds into second

cat file | grep "word"   # read file then search it
