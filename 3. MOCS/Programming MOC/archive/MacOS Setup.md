---
type: Programming Note
programming language:
related:
completed: false
created: 2025-12-12T15:27
updated: 2026-02-14T10:26
---
## Apps

`brew install --cask bitwarden ente-auth zen discord obsidian onlyoffice raycast karabiner-elements`

`brew install --cask github visual-studio-code ghostty`

>[!note] Notes
>- [Install Battery-Toolkit (aldente alternative)](https://github.com/mhaeuser/Battery-Toolkit)
>- Discord Themes: [Vencord Installer](https://vencord.dev/download/) - [Theme](https://github.com/catppuccin/discord?tab=readme-ov-file)
>- Remember to add [NextDNS](https://nextdns.io/)

## Terminal

`brew install stow fish starship zoxide atuin eza bat gitui bob container`

>[!note] Configs
>
>1. clone https://github.com/rimaout/.dotfiles
>2. use `stow` for linking the configs 

>[!note] Notes
>- *Install Cascadia Cove Font:* `brew install --cask font-caskaydia-cove-nerd-font`
>- *add bob path to fish:* `fish_add_path ~/.local/share/bob/nvim-bin`

On mac os when you open a new terminal window a message like this is printed: `Last login: Sat Jan 31 13:51:18 on ttys004`, to disable this just do `touch ~/.hushlogin`.

## Cluster Sapienza

Install open vpn connect to access Sapienza network: `brew install openvpn-connect`
...

Use `ssh surname_studentId@192.168.0.102` to connect, but this will ask for you user password.

I like to create a ssh key for the login, so I don't have to type the password each time:
1. create the ssh key: `ssh-keygen -t ed25519 -f ~/.ssh/sapienza_cluster`
2. save the public key to the server: `ssh-copy-id -i ~/.ssh/sapienza_cluster.pub surname_studentId@192.168.0.102`
3. I like also to add ...

Here is the consolidated guide, rewritten to be clear, copy-pasteable, and easy for other students to follow.

I have organized it logically: **Connection** $\to$ **Security (No Password)** $\to$ **Convenience (Short Alias)**.

---

# Sapienza Cluster Access Guide

### 1. Prerequisites (VPN)

You must be connected to the Sapienza network to access the cluster.

- **Install OpenVPN Connect:**
    
    Bash
    
    ```
    brew install openvpn-connect
    ```
    
- _Make sure your VPN is active before proceeding._
    

---

### 2. Create an SSH Key

_Why? So you don't have to type your password every time you log in._

Run the following command to generate a specific key for this cluster (using the modern `ed25519` algorithm):

Bash

```
ssh-keygen -t ed25519 -f ~/.ssh/sapienza_cluster
```

_(Press Enter to accept defaults. You can leave the passphrase empty if you want fully automatic login)._

Next, copy this key to the server. Replace `surname_studentId` with your actual username:

Bash

```
ssh-copy-id -i ~/.ssh/sapienza_cluster.pub surname_studentId@192.168.0.102
```

_(You will be asked to enter your cluster password one last time)._

---

### 3. Create an SSH Short Alias

_Why? So you can type `ssh sapienza` instead of the long command._

1. Open your SSH config file:
    
    Bash
    
    ```
    nano ~/.ssh/config
    ```
    
2. Paste the following block into the file. **Make sure to replace `surname_studentId` with your specific username:**
    
    Plaintext
    
    ```
    Host sapienza
        HostName 192.168.0.102
        User surname_studentId
        IdentityFile ~/.ssh/sapienza_cluster
    ```
    
3. Save and exit (`Ctrl + O`, `Enter`, `Ctrl + X`).
    

---

### 4. How to Connect

Now that everything is set up, you can simply run:

Bash

```
ssh sapienza
```

---

**Would you like me to generate a "Troubleshooting" section for your guide in case students run into permission errors?**
 






