# picoCTF 2022

> Arvind Shima | March 18,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Forensics |
| Challenge Name | Sleuthkit Apprentice |
| Points | 200 |

## Description

Download this disk image and find the flag.
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.

## Approach

Download the `disk.flag.img` file. Mount the disk on `/tmp`.

```bash
mkdir -p /tmp/tmpdisk/

sudo mount -o offset=$((360448*512)) sleuthkit_apprentice/disk.flag.img /tmp/tmpdisk/

cat root/my_folder/flag.uni.txt
```

## Flag

```
picoCTF{by73_5urf3r_3497ae6b}
```
