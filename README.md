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
PHASE 1 __Crikey! I have lost my mojo!__
## ___Phase  2___
1. Create a file with the WEIRD STRING codes.txt
2.Bomb Disasemble
```ssh
objdump -d bomb > bomb.s
```
Save to a file and open it with your favorite text editor
```ssh
vi bomb.s
```
Look for the phase_2 assembly code
```assembly
0000000000400f49 <phase_2>:
  400f49:       55                      push   %rbp
  400f4a:       53                      push   %rbx
  400f4b:       48 83 ec 28             sub    $0x28,%rsp
  400f4f:       64 48 8b 04 25 28 00    mov    %fs:0x28,%rax
  400f56:       00 00 
  400f58:       48 89 44 24 18          mov    %rax,0x18(%rsp)
  400f5d:       31 c0                   xor    %eax,%eax
  400f5f:       48 89 e6                mov    %rsp,%rsi
  400f62:       e8 2c 08 00 00          callq  401793 <read_six_numbers>
  400f67:       83 3c 24 01             cmpl   $0x1,(%rsp)
  400f6b:       74 05                   je     400f72 <phase_2+0x29>
  400f6d:       e8 eb 07 00 00          callq  40175d <explode_bomb>
  400f72:       48 89 e3                mov    %rsp,%rbx
  400f75:       48 8d 6c 24 14          lea    0x14(%rsp),%rbp
  400f7a:       8b 03                   mov    (%rbx),%eax
  400f7c:       01 c0                   add    %eax,%eax
  400f7e:       39 43 04                cmp    %eax,0x4(%rbx)
  400f81:       74 05                   je     400f88 <phase_2+0x3f>
  400f83:       e8 d5 07 00 00          callq  40175d <explode_bomb>
  400f88:       48 83 c3 04             add    $0x4,%rbx
  400f8c:       48 39 eb                cmp    %rbp,%rbx
  400f8f:       75 e9                   jne    400f7a <phase_2+0x31>
  400f91:       48 8b 44 24 18          mov    0x18(%rsp),%rax
  400f96:       64 48 33 04 25 28 00    xor    %fs:0x28,%rax
  400f9d:       00 00 
  400f9f:       74 05                   je     400fa6 <phase_2+0x5d>
  400fa1:       e8 ea fb ff ff          callq  400b90 <__stack_chk_fail@plt>
  400fa6:       48 83 c4 28             add    $0x28,%rsp
  400faa:       5b                      pop    %rbx
  400fab:       5d                      pop    %rbp
  400fac:       c3                      retq
```
