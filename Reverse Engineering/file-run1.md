# picoCTF 2022

> Arvind Shima | March 17,2022

## Overview

| Tables | Description |
| ------ | ----------- |
| Category | Reverse Engineering |
| Challenge Name | file-run1 |
| Points | 100 |

## Description

A program has been provided to you, what happens if you try to run it on the command line?

#### Hints

- To run the program at all, you must make it executable (i.e. $ chmod +x run)
- Try running it by adding a '.' in front of the path to the file (i.e. $ ./run)

## Approach

```bash
chmod +x run && ./run
```

## Flag

```
picoCTF{U51N6_Y0Ur_F1r57_F113_9bc52b6b}
```
