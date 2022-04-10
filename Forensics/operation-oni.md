# picoCTF 2022

> Arvind Shima | March 17,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Forensics |
| Challenge Name | Operation Oni |
| Points | 300 |

## Description

Download this disk image, find the key and log into the remote machine.
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.

## Approach

Download the `disk.img` file. Mount the disk on `/tmp` and Get the Private key.

```bash
mkdir -p mkdir -p /tmp/tmpdisk/

fdisk -l disk.img

sudo mount -o offset=$((206848*512)) disk.img /tmp/tmpdisk/
```

```bash
cat root/.ssh/id_ed25519

-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACBgrXe4bKNhOzkCLWOmk4zDMimW9RVZngX51Y8h3BmKLAAAAJgxpYKDMaWC
gwAAAAtzc2gtZWQyNTUxOQAAACBgrXe4bKNhOzkCLWOmk4zDMimW9RVZngX51Y8h3BmKLA
AAAECItu0F8DIjWxTp+KeMDvX1lQwYtUvP2SfSVOfMOChxYGCtd7hso2E7OQItY6aTjMMy
KZb1FVmeBfnVjyHcGYosAAAADnJvb3RAbG9jYWxob3N0AQIDBAUGBw==
-----END OPENSSH PRIVATE KEY-----
```

Login to the remote server by using private key.

```bash
chmod 600 id_ed25519

ssh -i id_ed25519 -p 62686 ctf-player@saturn.picoctf.net
```

## Flag

```
picoCTF{k3y_5l3u7h_b5066e83}
```
