# picoCTF 2022

> Arvind Shima | March 18,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Cryptography |
| Challenge Name | Very-smooth |
| Points | 300 |

## Description

Forget safe primes... Here, we like to live life dangerously... >:)

#### gen.py

```python
#!/usr/bin/python

from binascii import hexlify
from gmpy2 import *
import math
import os
import sys

if sys.version_info < (3, 9):
    math.gcd = gcd
    math.lcm = lcm

_DEBUG = False

FLAG  = open('flag.txt').read().strip()
FLAG  = mpz(hexlify(FLAG.encode()), 16)
SEED  = mpz(hexlify(os.urandom(32)).decode(), 16)
STATE = random_state(SEED)

def get_prime(state, bits):
    return next_prime(mpz_urandomb(state, bits) | (1 << (bits - 1)))

def get_smooth_prime(state, bits, smoothness=16):
    p = mpz(2)
    p_factors = [p]
    while p.bit_length() < bits - 2 * smoothness:
        factor = get_prime(state, smoothness)
        p_factors.append(factor)
        p *= factor

    bitcnt = (bits - p.bit_length()) // 2

    while True:
        prime1 = get_prime(state, bitcnt)
        prime2 = get_prime(state, bitcnt)
        tmpp = p * prime1 * prime2
        if tmpp.bit_length() < bits:
            bitcnt += 1
            continue
        if tmpp.bit_length() > bits:
            bitcnt -= 1
            continue
        if is_prime(tmpp + 1):
            p_factors.append(prime1)
            p_factors.append(prime2)
            p = tmpp + 1
            break

    p_factors.sort()

    return (p, p_factors)

e = 0x10001

while True:
    p, p_factors = get_smooth_prime(STATE, 1024, 16)
    if len(p_factors) != len(set(p_factors)):
        continue
    # Smoothness should be different or some might encounter issues.
    q, q_factors = get_smooth_prime(STATE, 1024, 17)
    if len(q_factors) != len(set(q_factors)):
        continue
    factors = p_factors + q_factors
    if e not in factors:
        break

if _DEBUG:
    import sys
    sys.stderr.write(f'p = {p.digits(16)}\n\n')
    sys.stderr.write(f'p_factors = [\n')
    for factor in p_factors:
        sys.stderr.write(f'    {factor.digits(16)},\n')
    sys.stderr.write(f']\n\n')

    sys.stderr.write(f'q = {q.digits(16)}\n\n')
    sys.stderr.write(f'q_factors = [\n')
    for factor in q_factors:
        sys.stderr.write(f'    {factor.digits(16)},\n')
    sys.stderr.write(f']\n\n')

n = p * q

m = math.lcm(p - 1, q - 1)
d = pow(e, -1, m)

c = pow(FLAG, e, n)

print(f'n = {n.digits(16)}')
print(f'c = {c.digits(16)}')
```

#### output.txt

```
n = 65446ab139efe9744c78a271ad04d94ce541a299f9d4dcb658f66f49414fb913d8ac6c90dacc1ad43135454c3c5ac76c56d71d2816dac23db5c8caa773ae2397bd5909a1f2823c230f44ac684c437f16e4ca75d50b75d2f7e5549c034aa8a723c9eaa904572a8c5c6c1ed7093a0695522a5c41575c4dbf1158ca940c02b223f50ae86e6782819278d989200a2cd2be4b7b303dffd07209752ee5a3060c6d910a108444c7a769d003bf8976617b4459fdc15a2a73fc661564267f55be6a0d0d2ec4c06a4951df5a096b079d9e300f7ad72fa6c73a630f9a38e472563434c10225bde7d08c651bdd23fd471077d44c6aab4e01323ed78641983b29633ad104f3fd
c = 19a98df2bfd703a31fedff8a02d43bc11f1fb3c15cfa7a55b6a32b3532e1ac477f6accc448f9b7d2b4deaae887450217bb70298afaa0f5e31a77e7c6f8ba1986979f15d299230119e3dd7e42eb9ca4d58d084d18b328fbe08c8909a2afc67866d6550e4e6fa27dc13d05c51cc87259fe73e2a1890cc2825d76c8b2a99f72f6023fc96658ac355487a6c275717ca6c13551094818efae1cec3c8773cc5a72fed518c00a53ba9799d9d5c182795dfcece07c727183fdd86fd2cb4b95e9f231be1858320aa7f8430885eb3d24300552d1a83158636316e55e6ac0a30a608964dbf2c412aed6a15df5fd49e737f7c06c02360d0c292abc33a3735152db2fb5bc5f6d
```

#### Hint

- Don't look at me... Go ask Mr. Pollard if you need a hint!

## Approach

Let's get start with python, We have the value of `e (public exponent)` and output.txt have the value of `n (modulus)` and `c (ciphertext)`. Let's decode with [RsaCtfTool](https://github.com/Ganapati/RsaCtfTool).

```bash
python3 RsaCtfTool.py -n 0x65446ab139efe9744c78a271ad04d94ce541a299f9d4dcb658f66f49414fb913d8ac6c90dacc1ad43135454c3c5ac76c56d71d2816dac23db5c8caa773ae2397bd5909a1f2823c230f44ac684c437f16e4ca75d50b75d2f7e5549c034aa8a723c9eaa904572a8c5c6c1ed7093a0695522a5c41575c4dbf1158ca940c02b223f50ae86e6782819278d989200a2cd2be4b7b303dffd07209752ee5a3060c6d910a108444c7a769d003bf8976617b4459fdc15a2a73fc661564267f55be6a0d0d2ec4c06a4951df5a096b079d9e300f7ad72fa6c73a630f9a38e472563434c10225bde7d08c651bdd23fd471077d44c6aab4e01323ed78641983b29633ad104f3fd -e 0x10001 --uncipher 0x19a98df2bfd703a31fedff8a02d43bc11f1fb3c15cfa7a55b6a32b3532e1ac477f6accc448f9b7d2b4deaae887450217bb70298afaa0f5e31a77e7c6f8ba1986979f15d299230119e3dd7e42eb9ca4d58d084d18b328fbe08c8909a2afc67866d6550e4e6fa27dc13d05c51cc87259fe73e2a1890cc2825d76c8b2a99f72f6023fc96658ac355487a6c275717ca6c13551094818efae1cec3c8773cc5a72fed518c00a53ba9799d9d5c182795dfcece07c727183fdd86fd2cb4b95e9f231be1858320aa7f8430885eb3d24300552d1a83158636316e55e6ac0a30a608964dbf2c412aed6a15df5fd49e737f7c06c02360d0c292abc33a3735152db2fb5bc5f6d
```

## Flag

```
picoCTF{376ebfe7}
```
