# picoCTF 2022

> Arvind Shima | March 16,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Reverse Engineering |
| Challenge Name | Lookey here |
| Points | 100 |

## Description

Attackers have hidden information in a very large mass of data in the past, maybe they are still doing it.

#### Hint

- Download the file and search for the flag based on the known prefix.

## Approach

```bash
egrep ^*{*}$ anthem.flag.txt
```

## Flag

```
picoCTF{gr3p_15_@w3s0m3_4c479940}
```
