---
created: 2025-07-19T15:42
updated: 2025-09-29T23:27
---
## Installation

Download the Debian ISO and create a bootable drive, I used ventoy.

Follow the Ubuntu graphical installation, in particular when asked install the ssh server, install it same thing for Nvidia proprietary graphics drivers.

>[!tip] Give your machine a cool name
>
>Also I decided that from now my machines will be named after the plates of *other wilds*, in this case I will call this server `timber-hearth`. So when asked during the installation I'm going to call it like this.

## SSH

Login to you user, now we can use the `ip addr` command to print the network informations, now note down the address of the network interface used, it can be found after the *inet* flag.

>[!warning] Static IP
>
>Is my case is `192.168.178.20`, and if you want it to not change remember to see how to set up a static ip address for you server in your router settings.

Now that we have the local ip address of the server, go on you machine (in my case my mac), open the terminal and write `ssh username@server_ip_address`, where `username` is the name of your non root user, and `server_ip_address` is the ip address that we just noted down.

Now when asked write the password of you non root user and press `enter`. Tatann you are now logged in via ssh.

### SSH Hardening

Currently our `SSH` configuration is not really secure, do to the fact that is still possible to log as the root user, and that we use a simple password for the ssh login, so we are going to:
- generating a ssh login key
- disable root login via ssh
- use public key authentication instead of password authentication
- change the port of the ssh server (22 is the default so it can be easily targeted)

>[!note] Generating the SSH Key
>In your machine (not the server) generate a public ssh key:
>1. go in your ssh directory `cd ~/.ssh`
>2. generate a key writing `ssh-keygen -t ed25519 -C "My ubuntu server"`, an then:
>	- respond to *Enter file in which to save the key* with something like `NameOfYourServer_SSHKey`
>	- respond to *Enter passphrase for "NameOfYourServer_SSHKey"* (empty for no passphrase) with a password, but since my drive is encrypted I leave it empty.
>3. Now the key is generated, but you need to copy the public key you just generated because we will need to use it later:
>4. Use `cat ~/.ssh/NameOfYourServer_SSHKey.pub` to print your public key on the terminal
>5. Copy the key (is something similar to `ssh-ed25519 AAAAC3NzaC1lZDI1NTEKGHJI9+fTJLsifkS1TwwFf9z0dstadWiXOQi4DhpuxEPtYW username@server_ip_address`)

>[!note] Adding the public SSH key to the server
>
>Use this command `ssh-copy-id -i ~/.ssh/NameOfYourServer_SSHKey.pub user@server_ip` to save the public ssh key in the server, obviously replace `NameOfYourServer_SSHKey.pub` and `user@server_ip` with you values.

>[!note] Hardening SSH configuration
>
>First of all log via ssh to the server with your non root user (same way as the last time `ssh username@server_ip_address`).
>
>Open `/etc/ssh/sshd_config` file with your favorite text editor in my case `sudo vim /etc/ssh/sshd_config`.
>
>To **change the port** of the ssh server, uncomment `#port 22` line and replace `22` with another port number, for example `port 3819`.
>
>To **disable root login** via ssh, uncomment `#PermitRootLogin prohibit-password` and replace `prohibit-password` with `no`.
>
>Also be sure that the line `PubkeyAuthentication` is set to `yes` and **disable password authentication** uncommenting `#PasswordAuthentication yes` and replacing `yes` with `no` like this `PasswordAuthentication no`.
>
>Disable `kbdInteractiveAuthentication` setting it to `yes` since is only used for password authentication.
>
>Disable `UsePAM` setting it to `no` since is only used for password authentication.
>
>Disable `X11Forwarding` setting it to `no`, this is used if you want to display a remote graphical user interface via ssh but since i will not use this can be disabled.
>
>Add to the end:
>```
>AuthenticationMethods publickey
>AllowUser youUserName
>```
>
>**Restart ssh service:** `sudo systemctl restart ssh`


Now if you want to log in via ssh you have to use `ssh username@server_ip_address -p 1234 -i ~/.ssh/key_name`, where:
- `username@server_ip_address` is the same as before
- `-p 1234` is the port you selected in the step before (replace 1234 with the port select, in the example is 3819)
- `~/.ssh/pubkey_name` is the path to the ssh key generated in the previous steps, so replace `pubkey_name` with the name you gave to the key (in the example is DebianServerSSHKey)

## ZFS Mirror

First we need to install OpenZFS:

```
sudo apt update
sudo apt install zfsutils-linux
```

After that, we can check if ZFS was installed correctly by running `whereis zfs`, you should see output similar to the following:

```
user@host:~$ whereis zfs
zfs: /usr/bin/zfs /usr/sbin/zfs /etc/zfs /usr/share/zfs /usr/share/man/man8/zfs.8.gz /usr/share/man/man4/zfs.4.gz
```

Now there are many different options of pools, but since I had only two drives I used a mirror setup, here is how I did it: [[How I setup a ZFS mirror pool]].

## Docker

**Initialization:**
- Installing Docker: `sudo apt install docker.io docker-compose -y`
- Start at boot (and now): `sudo systemctl enable --now docker`

**Adding the user to the docker group:**
- `sudo /sbin/usermod -aG docker rima`
- logout using `exit`
- re-login

Inside `/home/rima/data` (the mount point for the mirrored pool) create a *docker* a *media* directories: `mkdir docker` and `mkdir media`.

In the docjer compose file we will often need the **PUID** and **PGID** are the user ID and group ID of the linux user (*rima*), who we want to run the home server apps as. Both of these can be obtained using the `id` command as shown below:
```
	  rima@timber-hearth:~/data/docker$ id 
	  uid=1000(rima) gid=1000(rima) groups=1000(rima),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),101(lxd),111(docker)
```

>[!note] NVIDIA Contain Toolkit
>
>Some of the container I'll install (jellyfin and immich) can take advantage of my nvidia GPU, first of all I have already installed the proprietary NVIDA drivers during the installation of ubuntu, now i just need to install NVIDIA Contain Toolkit following this guide: https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/index.html

## Jellyfin

 Now we are going use docker compose to run a jellyfin container.

First of I'm going to create a directory to contain the `docker-compose.yaml` file for Jellyfin.

Run `cd /` to go in the root directory, here is mounted the zfs pool that we have previously created (tank), so `cd tank` and then `sudo mkdir docker/jellyfin`.

Now we can create the file `vim docker-compose.yaml` and paste inside:

```yaml
services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
    user: uid:gid
    network_mode: 'host'
	nv_file:
      - ../common.env
    volumes:
      - /path/to/config:/config
      - /path/to/cache:/cache
      - type: bind
        source: /path/to/media
        target: /media
      - type: bind
        source: /path/to/media2
        target: /media2
        read_only: true
      # Optional - extra fonts to be used during transcoding with subtitle burn-in
      - type: bind
        source: /path/to/fonts
        target: /usr/local/share/fonts/custom
        read_only: true
    restart: 'unless-stopped'
    # Optional - alternative address used for autodiscovery
    environment:
      - JELLYFIN_PublishedServerUrl=http://example.com
    # Optional - may be necessary for docker healthcheck to pass if running in host network mode
    extra_hosts:
      - 'host.docker.internal:host-gateway' 
```
