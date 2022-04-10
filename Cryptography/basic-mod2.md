# picoCTF 2022

> Arvind Shima | March 25,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Cryptography |
| Challenge Name | Basic-mod2 |
| Points | 100 |

## Description

A new modular challenge!
Take each number mod 41 and find the modular inverse for the result. Then map to the following character set: 1-26 are the alphabet, 27-36 are the decimal digits, and 37 is an underscore.
Wrap your decrypted message in the picoCTF flag format (i.e. picoCTF{decrypted_message})

#### Hints

- Do you know what the modular inverse is?
- The inverse modulo z of x is the number, y that when multiplied by x is 1 modulo z
- It's recommended to use a tool to find the modular inverses

## Approach

```python
def find_mod_inv(a,m):

    for x in range(1,m):
        if((a%m)*(x%m) % m==1):
            return x
    raise Exception('The modular inverse does not exist.')

a = [ 268,413,110,190,426,419,108,229,310,379,323,373,385,236,92,96,169,321,284,185,154,137,186 ]
m = 41

try:
	for i in a:
		res=find_mod_inv(i,m)
		print(str(res),end=" ")

except:
    print('The modular inverse does not exist.')

"""
Output: 28 14 22 30 18 32 30 12 25 37 8 31 18 4 37 3 33 35 27 2 4 3 28
"""
```

## Flag

```
picoCTF{1NV3R53LY_H4RD_C680BDC1}
```
