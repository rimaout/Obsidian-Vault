---
created: 2025-07-19T15:42
updated: 2025-09-23T14:12
---
## Installation

Download the Debian ISO and create a bootable drive, I used ventoy.

Follow the Debian graphical installation, in particular in the software section select only `SSH server` and `standard system utilities` and do not install a desktop environment.

## SSH

Login as root, so write `root` and press `enter`, the write your root password. 

Now we can use the `ip addr` command to print the network informations, now note down the address of the network interface used, it can be found after the *inet* flag.

Is my case is `192.168.178.20`, and if you want it to not change remember to see how to set up a static ip address for you server in your router settings.

Now that we have the local ip address of the server, go on you machine (in my case my mac), open the terminal and write `ssh username@server_ip_address`, where `username` is the name of your non root user, and `server_ip_address` is the ip address that we just noted down.

Now when asked write the password of you non root user and press `enter`. Tatann you are now logged in via ssh.

## Install and setup sudo

Elevate your self to a root shell doing `su root` + `enter`, and then write you root password.

Now we will install `sudo` and a terminal text editor (in my case it's `vim`): write `apt install sudo vim`.

now write ``/usr/sbin/visudo`` in the shell it will open a file with nano, be sure that the line `%sudo   ALL=(ALL:ALL) ALL` it's uncommented, just like this:

```
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
```

This means that the users in the sudo group, are going to be allowed to use sudo along side their password to elevate their privileges to the root user.

Now we are going to add our non root user to the sudo group, write `/usr/sbin/usermod -aG sudo <username>` and replace `<username>` with the name of your non root user.

So now the user is in the sudo group, this means that we can logout from the root user and just use the non root user and sudo.

Now before continuing logout form the ssh connection to apply the changes, `exit` two times, the first to log out from the root user the second to log out from the ssh connection.

## SSH Hardening

Currently our `SSH` configuration is not really secure, do to the fact that is still possible to log as the root user, and that we use a simple password for the ssh login, so we are going to:
- disable root login via ssh
- use public key authentication instead of password authentication
- change the port of the ssh server (22 is the default so it can be easily targeted)

In your machine (not the server) generate a public ssh key:
1. go in your ssh directory `cd ~/.ssh`
2. generate a key writing `ssh-keygen`, an then:
	- respond to *Enter file in which to save the key* with something like `DebianServerSSHKey`
	- respond to *Enter passphrase for "DebianServerSSHKey" (empty for no passphrase)* with a password, but since my drive is encrypted i leave it empty.
3. Now the key is generated, but you need to copy the public key you just generated because we will need to use it later:
4. Use `cat ~/.ssh/DebianServerSSHKey.pub` to print your public key on the terminal
5. Copy the key (is something similar to `ssh-ed25519 AAAAC3NzaC1lZDI1NTEKGHJI9+fTJLsifkS1TwwFf9z0dstadWiXOQi4DhpuxEPtYW username@hostname`)

Now we can harden SSH configuration on the server.

First of all log via ssh to the server with your non root user (same way as the last time `ssh username@server_ip_address`).

Open `/etc/ssh/sshd_config` file with your favorite text editor in my case `sudo vim /etc/ssh/sshd_config`.

To **change the port** of the ssh server, uncomment `#port 22` line and replace `22` with another port number, for example `port 3819`.

To **disable root login** via ssh, uncomment `#PermitRootLogin prohibit-password` and replace `prohibit-password` with `no`.

Also be sure that the line `PubkeyAuthentication` is set to `yes` and **disable password authentication** uncommenting `#PasswordAuthentication yes` and replacing `yes` with `no` like this `PasswordAuthentication no`.

Now we just need to add the public key by editing ``vim ~/.ssh/authorized_keys`` and pasting the previously generated key in the fist available empty line (if the `.ssh` directory doesn’t exist, create it with `mkdir ~/.ssh).

Now we just need to restart the ssh demon, write `sudo systemctl restart sshd`.

Now if you want to log in via ssh you have to use `ssh username@server_ip_address -p 1234 -i ~/.ssh/key_name`, where:
- `username@server_ip_address` is the same as before
- `-p 1234` is the port you selected in the step before (replace 1234 with the port select, in the example is 3819)
- `~/.ssh/pubkey_name` is the path to the ssh key generated in the previous steps, so replace `pubkey_name` with the name you gave to the key (in the example is DebianServerSSHKey)

## ZFS Mirror

Since the ZFS file system has a conflicting licenze in not shipped in the linux kernel by default, so we have to install the kernel module separately.

>**I just followed this guide:** https://openzfs.github.io/openzfs-docs/Getting%20Started/Debian/index.html

First of all we have to add repositories to download non-free resources to `apt` with `sudo vim /etc/apt/sources.list.d/bookworm-backports.list` and add:

```
deb http://deb.debian.org/debian bookworm-backports main contrib
deb-src http://deb.debian.org/debian bookworm-backports main contrib
```

Then edit `sudo vim /etc/apt/preferences.d/90_zfs` and add:

```
Package: src:zfs-linux
Pin: release n=bookworm-backports
Pin-Priority: 990
```

>[!note]- Whats this means?
>
>The pin file tells APT to prefer the ZFS source package from the Bookworm backports repository. It targets the source package (`src:zfs-linux`) and sets a high priority for the `bookworm-backports` release so apt will select the newer backports source by default (instead of the older main archive). This makes it easier to install a ZFS kernel module compatible with newer kernels without always using `-t bookworm-backports`. You can omit the pin and install explicitly with `apt -t bookworm-backports ...` if you prefer.

Now we can install the needed packages:

```
sudo apt update
sudo apt install dpkg-dev linux-headers-generic linux-image-generic 
sudo apt install zfs-dkms zfsutils-linux
```

Now there are many different options of pools, but since I had only two drives I used a mirror setup, here is how I did it: [[How I setup a ZFS mirror pool]].

## Docker

**Initialization:**
- Installing Docker: `sudo apt install docker.io docker-compose docker-doc`
- Start at boot (and now): `sudo systemctl enable --now docker`

**Adding the user to the docker group:**
- `sudo /sbin/usermod -aG docker rima`
- logout using `exit`
- re-login (in my case `ssh rima@192.168.178.20 -p 2348 -i ~/.ssh/debianServerSHHKey`)

