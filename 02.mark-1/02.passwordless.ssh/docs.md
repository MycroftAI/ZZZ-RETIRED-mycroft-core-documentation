---
title: Setup Passwordless SSH access
taxonomy:
    category:
        - docs
---

This information is basically from the
[Offical Raspberry Pi Documentation - Passwordless SSH Acess](https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md)

It is possible to configure your Pi to allow your computer to access it without providing a password each time you try to connect. To do this you need to generate an SSH key:

## Check for existing SSH keys

First, check whether there are already keys on the computer you are using to connect to the Mark 1:

```
ls ~/.ssh
```

If you see files named `id_rsa.pub` or `id_dsa.pub` you have keys set up already, so you can skip the generating keys step (or delete these files with `rm id*` and make new keys).

## Generate new SSH keys

To generate new SSH keys enter the following command, you can change this to whatever name of your mark 1 device, this is the default name out of the box:

```
ssh-keygen -t rsa -C pi@mark_1
```
Upon entering this command, you'll be asked where to save the key. We suggest you save it in the default location (`/home/pi/.ssh/id_rsa`) by just hitting `Enter`.

You'll also be asked to enter a passphrase. This is extra security which will make the key unusable without your passphrase, so if someone else copied your key, they could not impersonate you to gain access. If you choose to use a passphrase, type it here and press `Enter`, then type it again when prompted. Leave the field empty for no passphrase.  Each time you ssh to this mark 1 you will be asked for this passphrase if you choose one.

Now you should see the files `id_rsa` and `id_rsa.pub` in your `.ssh` directory in your home folder:

```
ls ~/.ssh
```

```
authorized_keys  id_rsa  id_rsa.pub  known_hosts
```

The `id_rsa` file is your private key. Keep this on your mark 1 device.

The `id_rsa.pub` file is your public key. This is what you put on machines you want to connect to. When the machine you try to connect to matches up your public and private key, it will allow you to connect.

Take a look at your public key to see what it looks like:

```
cat ~/.ssh/id_rsa.pub
```

It should be in the form:

```
ssh-rsa <REALLY LONG STRING OF RANDOM CHARACTERS> pi@mark_1
```

## Copy your public key to your Mark 1

If your Mark 1 does not have an .ssh directory you will need to set one up so that you can copy the key from your computer.

```
cd ~
install -d -m 700 ~/.ssh
```

To copy your public key to your Mark 1, use the following command to append the public key to your `authorized_keys` file on the Mark 1, sending it over SSH:

```
cat ~/.ssh/id_rsa.pub | ssh pi@<IP-ADDRESS-Mark1> 'cat >> .ssh/authorized_keys'
```

Note that this time you will have to authenticate with your password.

Now try `ssh pi@<IP-ADDRESS-Mark1>` and you should connect without a password prompt.

If you see a message "Agent admitted failure to sign using the key" then add your RSA or DSA identities to the authentication agent `ssh-agent` then execute the following command:  
```
ssh-add
```

If this did not work, delete your keys with `rm ~/.ssh/id*` and follow the instructions again.

If you are on windows you could always just use [WinSCP](https://winscp.net/eng/download.php) to copy these files over.
