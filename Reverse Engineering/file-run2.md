# picoCTF 2022

> Arvind Shima | March 17,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Reverse Engineering |
| Challenge Name | file-run2 |
| Points | 100 |

## Description

Another program, but this time, it seems to want some input. What happens if you try to run it on the command line with input "Hello!"?

#### Hint

- Try running it and add the phrase "Hello!" with a space in front (i.e. "./run Hello!")

## Approach

```bash
chmod +x run && ./run Hello!
```

## Flag

```
picoCTF{F1r57_4rgum3n7_be0714da}
```
