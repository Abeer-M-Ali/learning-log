# Day 1: Week 0, Kickoff

**Date:** 21 October 2026
**Goal:** Tools ready, GitHub set up, first commit pushed.

## What I did

- Set up my development environment inside **WSL (Ubuntu 24.04 LTS)**.
- Installed **Node.js v24.22.0 (LTS)** and **npm 11.19.1** using **nvm**.
- Confirmed **Git 2.43.0** and **VS Code** (opened from WSL with `code`).
- Created an **SSH key** and connected it to GitHub.
- Created the **learning-log** repo and pushed my **first commit**.

## What I learned

### The terminal and WSL

- To check a tool's version: `git --version`, `node -v`, `npm -v`. "Command not found" means it isn't installed.
- `which <tool>` shows where a command lives. A path starting with `/mnt/c/` means WSL is using the Windows copy, and a path in `/usr/bin` or `~/.nvm` means it's the Linux copy, which is the one I want.
- When `sudo` asks for a password, **nothing shows while I type**. That's normal. It's my Ubuntu password, not my Windows one.
- I don't need `do-release-upgrade`. Ubuntu 24.04 is an LTS release, so it's supported for years. Routine updates are `sudo apt update` and `sudo apt upgrade`.

### Node with nvm

- I didn't use `apt install nodejs`, because it gives an old version and no way to switch.
- **nvm** (Node Version Manager) lets me install several Node versions and switch between them.
- `command -v nvm` checks that it's installed. `which nvm` doesn't work, because nvm is a shell function and not a program.
- Useful commands: `nvm install --lts`, `nvm ls`, `nvm use <version>`, `nvm uninstall <version>`, `nvm alias default 'lts/*'`.

### SSH keys

- `ssh-keygen -t ed25519` creates a **key pair**: a private key (never share it) and a public key (the `.pub` file, safe to share).
- I added the **public** key to GitHub (Settings → SSH and GPG keys).
- `ssh -T git@github.com` tests the connection. "Hi <username>! You've successfully authenticated, but GitHub does not provide shell access" means it worked.

### Git basics

- Git has four places my work can live: **working folder → staging area → local repository → GitHub**.
- `git config --global` sets my name, email and default branch once for the whole computer.
- Commands I ran, in order: `git init`, `git add`, `git commit -m "..."`, `git remote add origin <address>`, `git push -u origin main`.
- `git status` shows what changed. `git log --oneline` shows my commit history.
- `origin` is just the nickname for the GitHub copy of the repo. `-u` links my local `main` to it, so later `git push` is enough.
- I created the GitHub repo **empty** so my first push wouldn't clash with a README GitHub made on its own.

### My first real error: GH007

- **Error:** `GH007: Your push would publish a private email address.`
- **Cause:** Git stamps every commit with the email from my config, and I had used my real one. GitHub blocked the push to protect my email privacy.
- **Fix:**
  1. Copy my `noreply` address from github.com/settings/emails.
  2. `git config --global user.email "<noreply address>"`
  3. `git commit --amend --reset-author --no-edit` (rewrites the commit that wasn't pushed yet).
  4. `git push -u origin main`
- Lesson: changing my config doesn't change commits that already exist, and I can safely amend a commit **only before I push it**.

## Result

- Repo: `learning-log`, public, 1 commit, README rendering on GitHub.

## Still to do in Week 0

- [ ] Publish my GitHub profile README (the `Abeer-M-Ali/Abeer-M-Ali` repo)
- [ ] Pin repos and archive or delete empty old ones
- [ ] Baseline tests: EF SET (English) and a JavaScript self-quiz
- [ ] Skim roadmap.sh/frontend

## Questions I still have

- (write any command that still feels like magic here)
