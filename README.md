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
Phase 2 __1 2 4 8 16 32__

## __Phase 3__
1.  Go to Vi file
```ssh
vi bomb.s
```
2. Look for the part 3 assembly
```assembly
0000000000400fad <phase_3>:
  400fad:       48 83 ec 28             sub    $0x28,%rsp
  400fb1:       64 48 8b 04 25 28 00    mov    %fs:0x28,%rax
  400fb8:       00 00 
  400fba:       48 89 44 24 18          mov    %rax,0x18(%rsp)
  400fbf:       31 c0                   xor    %eax,%eax
  400fc1:       4c 8d 44 24 14          lea    0x14(%rsp),%r8
  400fc6:       48 8d 4c 24 0f          lea    0xf(%rsp),%rcx
  400fcb:       48 8d 54 24 10          lea    0x10(%rsp),%rdx
  400fd0:       be 29 27 40 00          mov    $0x402729,%esi
  400fd5:       e8 66 fc ff ff          callq  400c40 <__isoc99_sscanf@plt>
  400fda:       83 f8 02                cmp    $0x2,%eax
  400fdd:       7f 05                   jg     400fe4 <phase_3+0x37>
  400fdf:       e8 79 07 00 00          callq  40175d <explode_bomb>
  400fe4:       83 7c 24 10 07          cmpl   $0x7,0x10(%rsp)
  400fe9:       0f 87 fc 00 00 00       ja     4010eb <phase_3+0x13e>
  400fef:       8b 44 24 10             mov    0x10(%rsp),%eax
  400ff3:       ff 24 c5 40 27 40 00    jmpq   *0x402740(,%rax,8)
  400ffa:       b8 76 00 00 00          mov    $0x76,%eax
  400fff:       81 7c 24 14 6b 01 00    cmpl   $0x16b,0x14(%rsp)
  401006:       00 
  401007:       0f 84 e8 00 00 00       je     4010f5 <phase_3+0x148>
  40100d:       e8 4b 07 00 00          callq  40175d <explode_bomb>
  401012:       b8 76 00 00 00          mov    $0x76,%eax
  401017:       e9 d9 00 00 00          jmpq   4010f5 <phase_3+0x148>
  40101c:       b8 76 00 00 00          mov    $0x76,%eax
  401021:       81 7c 24 14 48 02 00    cmpl   $0x248,0x14(%rsp)
  401028:       00 
  401029:       0f 84 c6 00 00 00       je     4010f5 <phase_3+0x148>
  40102f:       e8 29 07 00 00          callq  40175d <explode_bomb>
  401034:       b8 76 00 00 00          mov    $0x76,%eax
  401039:       e9 b7 00 00 00          jmpq   4010f5 <phase_3+0x148>
  40103e:       b8 6f 00 00 00          mov    $0x6f,%eax
  401043:       81 7c 24 14 17 03 00    cmpl   $0x317,0x14(%rsp)
  40104a:       00 
  40104b:       0f 84 a4 00 00 00       je     4010f5 <phase_3+0x148>
  401051:       e8 07 07 00 00          callq  40175d <explode_bomb>
  401056:       b8 6f 00 00 00          mov    $0x6f,%eax
  40105b:       e9 95 00 00 00          jmpq   4010f5 <phase_3+0x148>
  401060:       b8 69 00 00 00          mov    $0x69,%eax
  401065:       81 7c 24 14 92 00 00    cmpl   $0x92,0x14(%rsp)
  40106c:       00 
  40106d:       0f 84 82 00 00 00       je     4010f5 <phase_3+0x148>
  401073:       e8 e5 06 00 00          callq  40175d <explode_bomb>
  401078:       b8 69 00 00 00          mov    $0x69,%eax
  40107d:       eb 76                   jmp    4010f5 <phase_3+0x148>
  40107f:       b8 68 00 00 00          mov    $0x68,%eax
  401084:       81 7c 24 14 45 01 00    cmpl   $0x145,0x14(%rsp)
  40108b:       00 
  40108c:       74 67                   je     4010f5 <phase_3+0x148>
  40108e:       e8 ca 06 00 00          callq  40175d <explode_bomb>
  401093:       b8 68 00 00 00          mov    $0x68,%eax
  401098:       eb 5b                   jmp    4010f5 <phase_3+0x148>
  40109a:       b8 6f 00 00 00          mov    $0x6f,%eax
  40109f:       81 7c 24 14 e3 02 00    cmpl   $0x2e3,0x14(%rsp)
  4010a6:       00 
  4010a7:       74 4c                   je     4010f5 <phase_3+0x148>
  4010a9:       e8 af 06 00 00          callq  40175d <explode_bomb>
  4010ae:       b8 6f 00 00 00          mov    $0x6f,%eax
  4010b3:       eb 40                   jmp    4010f5 <phase_3+0x148>
  4010b5:       b8 6a 00 00 00          mov    $0x6a,%eax
  4010ba:       81 7c 24 14 9b 01 00    cmpl   $0x19b,0x14(%rsp)
  4010c1:       00 
  4010c2:       74 31                   je     4010f5 <phase_3+0x148>
  4010c4:       e8 94 06 00 00          callq  40175d <explode_bomb>
  4010c9:       b8 6a 00 00 00          mov    $0x6a,%eax
  4010ce:       eb 25                   jmp    4010f5 <phase_3+0x148>
  4010d0:       b8 61 00 00 00          mov    $0x61,%eax
  4010d5:       81 7c 24 14 cf 03 00    cmpl   $0x3cf,0x14(%rsp)
  4010dc:       00 
  4010dd:       74 16                   je     4010f5 <phase_3+0x148>
  4010df:       e8 79 06 00 00          callq  40175d <explode_bomb>
  4010e4:       b8 61 00 00 00          mov    $0x61,%eax
  4010e9:       eb 0a                   jmp    4010f5 <phase_3+0x148>
  4010eb:       e8 6d 06 00 00          callq  40175d <explode_bomb>
  4010f0:       b8 6b 00 00 00          mov    $0x6b,%eax
  4010f5:       3a 44 24 0f             cmp    0xf(%rsp),%al
  4010f9:       74 05                   je     401100 <phase_3+0x153>
  4010fb:       e8 5d 06 00 00          callq  40175d <explode_bomb>
  401100:       48 8b 44 24 18          mov    0x18(%rsp),%rax
  401105:       64 48 33 04 25 28 00    xor    %fs:0x28,%rax
  40110c:       00 00 
  40110e:       74 05                   je     401115 <phase_3+0x168>
  401110:       e8 7b fa ff ff          callq  400b90 <__stack_chk_fail@plt>
  401115:       48 83 c4 28             add    $0x28,%rsp
  401119:       c3                      retq
```
```ssh
gdb bomb
```
```ssh
(gdb) break explode_bomb
```
```ssh
(gdb) break phase_3
```
```ssh
(gdb) run
```
3. Enter the input for phase 1 and 2
4. Use random input for phase 3 ti start cracking it
```ssh
(gdb) 0 292
```
5. Use `disas` command to see whats going on
```ssh
disas phase_3
```
```ssh
--Type <RET> for more, q to quit, c to continue without paging--r
```
```ssh
(gdb) ni
```
```ssh 
(gdb) info registers 
````
give int representation
```ssh
(gdb) x/1xd 0x7fffffffe8f0 // rsp address
```
