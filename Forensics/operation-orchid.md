# picoCTF 2022

> Arvind Shima | March 17,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Forensics |
| Challenge Name | Operation Orchid |
| Points | 400 |

## Description

Download this disk image and find the flag.
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.

## Approach

Download the `disk.img` file. Mount the disk on `/tmp`.

```bash
mkdir -p /tmp/tmpdisk/

fdisk -l disk.flag.img 

sudo mount -o offset=$((411648*512)) disk.flag.img /tmp/tmpdisk/
```
This challenge, We have the flag on root directory as an encrypted data. In linux whatever command we put on terminal will saved as a history file. So, Let's Check out the `.ash_history`.

```bash
cat .ash_history 

touch flag.txt
nano flag.txt 
apk get nano
apk --help
apk add nano
nano flag.txt 
openssl
openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567
shred -u flag.txt
ls -al
halt
```

See, They used AES Encryption. Let's decrypt the `flag.txt.enc` with openssl.

```bash
openssl enc -d -aes-256-cbc -in flag.txt.enc -out flag.txt -k unbreakablepassword1234567
```

## Flag

```
picoCTF{h4un71ng_p457_0a710765}
```
