# picoCTF 2022

> Arvind Shima | March 18,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Cryptography |
| Challenge Name | Substitution 1 |
| Points | 100 |

## Description

A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again.

#### message.txt

```
IECj (jqfue cfu ixzelus eqs coxa) xus x emzs fc ifrzlesu jsiludem ifrzsededfy. Ifyesjexyej xus zusjsyesk hdeq x jse fc iqxoosyasj hqdiq esje eqsdu iusxedgdem, esiqydixo (xyk affaodya) jpdooj, xyk zuftosr-jfogdya xtdodem. Iqxoosyasj ljlxoom ifgsu x ylrtsu fc ixesafudsj, xyk hqsy jfogsk, sxiq mdsokj x jeudya (ixoosk x coxa) hqdiq dj jltrdeesk ef xy fyodys jifudya jsugdis. IECj xus x ausxe hxm ef osxuy x hdks xuuxm fc ifrzlesu jsiludem jpdooj dy x jxcs, osaxo sygdufyrsye, xyk xus qfjesk xyk zoxmsk tm rxym jsiludem auflzj xuflyk eqs hfuok cfu cly xyk zuxiedis. Cfu eqdj zuftosr, eqs coxa dj: zdifIEC{CU3NL3YIM_4774IP5_4U3_I001_4871S6CT}
```

#### Hints

- Try a frequency attack. An online tool might help.
- Do the punctuation and the individual words help you make any substitutions?

## Approach

Same technique used before in substitution0 challenge like a frequency attack. There is no keys provided. Using [Boxentriq](https://www.boxentriq.com/code-breaking/keyed-caesar-cipher) to automate the process and Got some vaild key to decode.

```
CTFs (short for capture the flag) are a type of computer security competition. Contestants are presented with a set of challenges which test their creativity, technical (and googling) skills, and problem-solving ability. Challenges usually cover a number of categories, and when solved, each yields a string (called a flag) which is submitted to an online scoring service. CTFs are a great way to learn a wide array of computer security skills in a safe, legal environment, and are hosted and played by many security groups around the world for fun and practice. For this problem, the flag is: picoCTF{FR3XU3NCY_4774CK5_4R3_C001_4871E6FB}
```

## Flag

```
picoCTF{FR3XU3NCY_4774CK5_4R3_C001_4871E6FB}
```
