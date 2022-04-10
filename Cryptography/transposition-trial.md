# picoCTF 2022

> Arvind Shima | March 18,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Cryptography |
| Challenge Name | Transposition-trial |
| Points | 100 |

## Description

Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message.

#### message.txt

```
heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V6E5926A}4
```

#### Hint

- Split the message up into blocks of 3 and see how the first block is scrambled

## Flag

```
picoCTF{7R4N5P051N6_15_3XP3N51V3_56E6924A}
```
