# CS224_BombLab

## Introduction
The nefarious Dr. Evil has planted a slew of “binary bombs” on our class machines. A binary bomb is a
program that consists of a sequence of phases. Each phase expects you to type a particular string on stdin.
If you type the correct string, then the phase is defused and the bomb proceeds to the next phase. Otherwise,
the bomb explodes by printing "BOOM!!!" and then terminating. The bomb is defused when every phase
has been defused.
There are too many bombs for us to deal with, so we are giving each participant a bomb to defuse. Your
mission, which you have no choice but to accept, is to defuse that bomb before the due date. Good luck, and
welcome to the bomb squad!

## ___Phase 1___

```sh
cd bomb*
ls
strings bomb
```
`strings bomb` retrieves all the strings in the executable. _Look for a string that sticks out._
```sh
gdb bomb
(gdb) r
Welcome to my fiendish little bomb. You have 6 phases with which yo blow yourself up. Have a nice day!
<PASTE WEIRD STRING HERE>
Phase 1 defused how about the nexst one?
kill
```
## ____Phase  2 ____
