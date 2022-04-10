# picoCTF 2022

> Arvind Shima | March 16,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Forensics |
| Challenge Name | File types |
| Points | 100 |

## Description

This file was found among some files marked confidential but my pdf reader cannot read it, maybe yours can.

#### Hint

Remember that some file types can contain and nest other files

## Approach

```bash
┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file Flag.pdf 
Flag.pdf: shell archive text

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $mv Flag.pdf Flag.sh

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $chmod +x Flag.sh

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $./Flag.sh 
x - created lock directory _sh00046.
x - extracting flag (text)
x - removed lock directory _sh00046.

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file flag 
flag: current ar archive

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $ar x flag

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file flag 
flag: cpio archive

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $mv flag Flag

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $cpio -i < Flag
2 blocks

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file flag 
flag: bzip2 compressed data, block size = 900k

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $mv flag flag.bz2

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $bzip2 -dv flag.bz2 
  flag.bz2: done

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file flag 
flag: gzip compressed data, was "flag", last modified: Tue Mar 15 06:50:36 2022, from Unix, original size modulo 2^32 329

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $mv flag flag.gz

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $gunzip flag.gz

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file flag 
flag: lzip compressed data, version: 1

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $mv flag flag.lz

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $lzip -d flag.lz

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file flag
flag.lz4: LZ4 compressed data (v1.4+)

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $mv flag flag.lz4

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $lz4 -dv flag.lz4 
*** LZ4 command line interface 64-bits v1.9.3, by Yann Collet ***
Decoding file flag 
flag.lz4             : decoded 283 bytes

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file flag
flag.lz4: LZ4 compressed data (v1.4+)

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $mv flag flag.lz4

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $lz4 -dv flag.lz4 
*** LZ4 command line interface 64-bits v1.9.3, by Yann Collet ***
Decoding file flag 
flag.lz4             : decoded 266 bytes

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file flag
flag: LZMA compressed data, non-streamed, size 255

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $mv flag flag.lzma

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $lzma -d flag.lzma

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file flag 
flag: lzop compressed data - version 1.040, LZO1X-1, os: Unix

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $mv flag flag.lzo

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $lzop -d flag.lzo

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file flag
flag: lzip compressed data, version: 1

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $mv flag flag.lzip

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $lzip -d flag.lzip

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file flag.lzip.out

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $mv flag.lzip.out flag.xz

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $xz -d flag.xz

┌─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $file flag 
flag: ASCII text

┌─[✗]─[whoami@parrot]─[~/Workspace/picoctf/picoctf2022/forensics/file-types]
└──╼ $cat flag | xxd -r -p

```

## Flag

```
picoCTF{f1len@m3_m@n1pul@t10n_f0r_0b2cur17y_347eae65}
```
