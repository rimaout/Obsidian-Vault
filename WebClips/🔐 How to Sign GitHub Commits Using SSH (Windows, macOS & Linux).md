---
created: 2025-10-25T12:57
updated: 2025-10-25T13:00
---
WebClip form: https://dev.to/udara_dananjaya/how-to-sign-github-commits-using-ssh-windows-macos-linux-24mi

---

If you’ve ever admired that shiny green **“Verified”** badge next to a commit on GitHub, you’re looking at a **digitally signed commit**. Traditionally, that meant diving into the somewhat messy world of **GPG keys**. But now, GitHub supports **SSH-signed commits** — and it's far simpler, faster, and works beautifully across **Windows**, **macOS**, and **Linux**.

In this article, I’ll show you how to set up **SSH commit signing** on any operating system so your GitHub commits are secure and proudly Verified. Let’s roll. 🔐🚀

## Why Sign Your GitHub Commits?

Signed commits:

- Prove **you actually made them** (authenticity)
- Prevent impersonation and spoofing
- Show the **✅ Verified** badge on GitHub
- Add trust, especially in open source or team environments

## Prerequisites

Before you start, make sure you have:

- **Git 2.34 or newer** (check with `git --version`)
- A GitHub account
- Git set up on your machine
- SSH access (or willingness to generate an SSH key)

## Step 1: Generate an SSH Key (If You Don’t Have One)

SSH keys are a pair: a **private key** (kept secret) and a **public key** (shared with GitHub).

Run the following in your terminal:  

```
ssh-keygen -t ed25519 -C "your-email@example.com"
```

- Hit **Enter** to accept the default file location:
    
    - macOS/Linux: `~/.ssh/id_ed25519`
    - Windows: `C:\Users\YourName\.ssh\id_ed25519`
- Set a **passphrase** if you want (recommended for security)
    

If you're asked whether to overwrite an existing key — be careful! It may already be in use for GitHub or another service.

## Step 2: Add Your Public Key to GitHub

Now we give GitHub your **public key** so it can verify your commits.

how your public key:

- **macOS/Linux:**  
    
    ```
    cat ~/.ssh/id_ed25519.pub
    ```
    
- **Windows (PowerShell):**  
    
    ```
    type $env:USERPROFILE\.ssh\id_ed25519.pub
    ```


Copy the entire key that starts with `ssh-ed25519`.

### Add the key to GitHub:

1. Go to: [https://github.com/settings/ssh](https://github.com/settings/ssh)
2. Click **New SSH key**
3. Fill in:
    
    - **Title**: Something like `GitHub Signing Key`
    - **Key type**: Signing Key
    - **Key**: Paste the key you copied
4. Click **Add SSH key**

## Step 3: Configure Git to Sign Commits with SSH

Now, configure Git to use SSH as the signing backend and point it to your **private key**.

### Run the following:

```
git config --global gpg.format ssh
git config --global user.signingkey ~/.ssh/id_ed25519
git config --global commit.gpgsign true
```

