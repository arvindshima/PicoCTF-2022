# picoCTF 2022

> Arvind Shima | March 17,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Cryptography |
| Challenge Name | Rail-fence |
| Points | 100 |

## Description

A type of transposition cipher is the rail fence cipher, which is described [here](https://en.wikipedia.org/wiki/Rail_fence_cipher). Here is one such cipher encrypted using the rail fence with 4 rails. Can you decrypt it?

#### message.txt

```
Ta _7N6D49hlg:W3D_H3C31N__A97ef sHR053F38N43D7B i33___N6
```

#### Hint

Once you've understood how the cipher works, it's best to draw it out yourself on paper

## Approach

As they mentioned in description, We know the cipher and how many rails used in this cipher. Let's decode by [Boxentriq](https://www.boxentriq.com/code-breaking/rail-fence-cipher).

## Flag

```
picoCTF{WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_4A76B997}
```