---
type: Programming Note
programming language:
related:
completed: false
created: 2026-07-05T16:29
updated: 2026-07-05T16:31
---

### 1. Installation & Initial Update

- **App Install:** Downloaded and installed Termux via F-Droid/GitHub (bypassing Google Play due to Huawei Mobile Services and deprecation).
- **Storage Access:** Granted local file permissions:
	- `termux-setup-storage`
- **System Update:** Synchronized repositories and upgraded core packages:
	- `pkg update && pkg upgrade`

### 2. SSH Server Configuration

- **Installation:** Installed the OpenSSH package:
    
    > `pkg install openssh`
    
- **Security:** Set up a secure login password:
    
    > `passwd`
    
- **Service Management:** Started the SSH daemon (runs on non-root port `8022`):
    
    > `sshd`
    
- **Remote Connection:** Checked credentials (`whoami` and `ifconfig`) to connect from a computer using:
    
    > `ssh <username>@<phone_ip> -p 8022`
    

### 3. Shell Customization (Fish)

- **Installation:** Installed the Friendly Interactive Shell:
    
    > `pkg install fish`
    
- **Default Shell Change:** Set Fish to automatically open on every new session:
    
    > `chsh -s fish`
    

### 4. Terminal Environment Fix (`clear` command error)

Fixed the `"terminals database is inaccessible"` error across both shells by forcing the terminal type and defining the correct terminfo path.

#### Fixed for Fish Shell:

Added variables to `~/.config/fish/config.fish`:

> `set -gx TERM xterm-256color` `set -gx TERMINFO /data/data/com.termux/files/usr/share/terminfo`

#### Fixed for Bash Shell:

Added variables to `~/.bashrc`:

> `export TERM=xterm-256color` `export TERMINFO=/data/data/com.termux/files/usr/share/terminfo`

### 5. Off-Site Access via Tailscale (Remote SSH)

Set up a private mesh network to access the Termux SSH server over the internet.

1. **Install:** Download **Tailscale** from F-Droid (or directly from the Tailscale website).
    
2. **Authenticate:** Open the app, log in to your Tailscale account, and toggle the VPN connection to **Active**.
    
3. **Get Remote IP:** Copy the `100.x.x.x` IP address assigned to your phone in the app.
    
4. **Connect Remotely:** From your computer (which must also be running Tailscale and logged into the same account), open a terminal and run:
    

> `ssh <username>@<tailscale_100.x.x.x_ip> -p 8022`

### Quick Commands Cheat Sheet

- **Start SSH Server:** `sshd`
    
- **Stop SSH Server:** `pkill sshd`
    
- **Switch to Fish (Temporary):** `fish`
    
- **Switch to Bash (Temporary):** `bash`
    
- **Change Default Shell Back to Bash:** `chsh -s bash`
    
- **Change Default Shell Back to Fish:** `chsh -s fish`