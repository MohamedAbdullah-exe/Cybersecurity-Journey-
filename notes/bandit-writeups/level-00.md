# Bandit Level 0

## Goal
Connect to the OverTheWire Bandit server using SSH for the first time.

## What I learned
- What SSH is — a way to remotely control another computer through a terminal
- How to use the `ssh` command with a username, hostname, and port number

## The Command

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Breaking it down:
- `ssh` — the command to start a secure shell connection
- `bandit0` — the username I'm logging in as
- `@bandit.labs.overthewire.org` — the server I'm connecting to
- `-p 2220` — the port number (default SSH is 22, this server uses 2220)

## What happened
- It asked "are you sure you want to continue connecting?" — typed `yes`
- It asked for a password — typed `bandit0`
- Password didn't show on screen while typing — that's normal for security
- Got in and saw the Bandit welcome message
---

*Completed: March 2026*
