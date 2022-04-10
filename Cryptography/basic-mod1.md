# picoCTF 2022

> Arvind Shima | March 15,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Cryptography |
| Challenge Name | Basic-mod1 |
| Points | 100 |

## Description

We found this weird message being passed around on the servers, we think we have a working decrpytion scheme.
Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore.
Wrap your decrypted message in the picoCTF flag format (i.e. picoCTF{decrypted_message})

#### Hints

- Do you know what mod 37 means?
- mod 37 means modulo 37. It gives the remainder of a number after being divided by 37.

## Approach

```python
import math

f = [ 54,396,131,198,225,258,87,258,128,211,57,235,114,258,144,220,39,175,330,338,297,288 ]

for i in f: print(int(math.fmod(i, 37)),end=" ")

"""
Output: 17 26 20 13 3 36 13 36 17 26 20 13 3 36 33 35 2 27 34 5 1 29
"""
```

## Flag

```
picoCTF{R0UND_N_R0UND_79C18FB3}
```
