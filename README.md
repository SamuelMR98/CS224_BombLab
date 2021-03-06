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
phase 3 needs a char before the secong number the char is the ASCII value of the %rax register
__Phase 3__ 5 o739

## __Phase 4__
1. Open bomb.s
```ssh
vi bomb.s
```

```assembly
0000000000401158 <phase_4>:
  401158:       48 83 ec 18             sub    $0x18,%rsp
  40115c:       64 48 8b 04 25 28 00    mov    %fs:0x28,%rax
  401163:       00 00 
  401165:       48 89 44 24 08          mov    %rax,0x8(%rsp)
  40116a:       31 c0                   xor    %eax,%eax
  40116c:       48 8d 4c 24 04          lea    0x4(%rsp),%rcx
  401171:       48 89 e2                mov    %rsp,%rdx
  401174:       be 35 2a 40 00          mov    $0x402a35,%esi
  401179:       e8 c2 fa ff ff          callq  400c40 <__isoc99_sscanf@plt>
  40117e:       83 f8 02                cmp    $0x2,%eax
  401181:       75 06                   jne    401189 <phase_4+0x31>
  401183:       83 3c 24 0e             cmpl   $0xe,(%rsp)
  401187:       76 05                   jbe    40118e <phase_4+0x36>
  401189:       e8 cf 05 00 00          callq  40175d <explode_bomb>
  40118e:       ba 0e 00 00 00          mov    $0xe,%edx
  401193:       be 00 00 00 00          mov    $0x0,%esi
  401198:       8b 3c 24                mov    (%rsp),%edi
  40119b:       e8 7a ff ff ff          callq  40111a <func4>
  4011a0:       83 f8 03                cmp    $0x3,%eax
  4011a3:       75 07                   jne    4011ac <phase_4+0x54>
  4011a5:       83 7c 24 04 03          cmpl   $0x3,0x4(%rsp)
  4011aa:       74 05                   je     4011b1 <phase_4+0x59>
  4011ac:       e8 ac 05 00 00          callq  40175d <explode_bomb>
  4011b1:       48 8b 44 24 08          mov    0x8(%rsp),%rax
  4011b6:       64 48 33 04 25 28 00    xor    %fs:0x28,%rax
  4011bd:       00 00 
  4011bf:       74 05                   je     4011c6 <phase_4+0x6e>
  4011c1:       e8 ca f9 ff ff          callq  400b90 <__stack_chk_fail@plt>
  4011c6:       48 83 c4 18             add    $0x18,%rsp
  4011ca:       c3                      retq

```
3. Phase 4 class for __func4__
```assembly
000000000040111a <func4>:
  40111a:       48 83 ec 08             sub    $0x8,%rsp
  40111e:       89 d0                   mov    %edx,%eax
  401120:       29 f0                   sub    %esi,%eax
  401122:       89 c1                   mov    %eax,%ecx
  401124:       c1 e9 1f                shr    $0x1f,%ecx
  401127:       01 c8                   add    %ecx,%eax
  401129:       d1 f8                   sar    %eax
  40112b:       8d 0c 30                lea    (%rax,%rsi,1),%ecx
  40112e:       39 f9                   cmp    %edi,%ecx
  401130:       7e 0c                   jle    40113e <func4+0x24>
  401132:       8d 51 ff                lea    -0x1(%rcx),%edx
  401135:       e8 e0 ff ff ff          callq  40111a <func4>
  40113a:       01 c0                   add    %eax,%eax
  40113c:       eb 15                   jmp    401153 <func4+0x39>
  40113e:       b8 00 00 00 00          mov    $0x0,%eax
  401143:       39 f9                   cmp    %edi,%ecx
  401145:       7d 0c                   jge    401153 <func4+0x39>
  401147:       8d 71 01                lea    0x1(%rcx),%esi
  40114a:       e8 cb ff ff ff          callq  40111a <func4>
  40114f:       8d 44 00 01             lea    0x1(%rax,%rax,1),%eax
  401153:       48 83 c4 08             add    $0x8,%rsp
  401157:       c3                      retq
```
4. Decode Fun4
```c
int fun4(int p, int q, int r){
    int a = r - q;
    int b = a >> 31;
    a = a + b;
    a = a >> 1;
    b = a + q;
    if (b <= p){
        if (b >= p){
            return 0;
            
        }else{
            return 2 * fun4(p, b + 1, r) + 1;
            
        }
    }else{
        return 2 * fun4(p, q, b - 1);
    }
}
```
The variables *q* and *r* are known from the code and are 0 and 14 respectively.
5. Analize these lines
```assembly
   0x00000000004011a0 <+72>:	cmp    $0x3,%eax
   0x00000000004011a3 <+75>:	jne    0x4011ac <phase_4+84>
   0x00000000004011a5 <+77>:	cmpl   $0x3,0x4(%rsp)
   0x00000000004011aa <+82>:	je     0x4011b1 <phase_4+89>
```
For the first input we need a number so that the *__func4__* returns 3 and the second must be equal to __3__
__Phase_4__ 12 3

## __Phase_5__
1. Open bomb.s and look for the phase_5 section
```ssh
vi bomb.s
```
2. phase_5 assembly
```assembly
00000000004011cb <phase_5>:
  4011cb:       48 83 ec 18             sub    $0x18,%rsp
  4011cf:       64 48 8b 04 25 28 00    mov    %fs:0x28,%rax
  4011d6:       00 00 
  4011d8:       48 89 44 24 08          mov    %rax,0x8(%rsp)
  4011dd:       31 c0                   xor    %eax,%eax
  4011df:       48 8d 4c 24 04          lea    0x4(%rsp),%rcx
  4011e4:       48 89 e2                mov    %rsp,%rdx
  4011e7:       be 35 2a 40 00          mov    $0x402a35,%esi
  4011ec:       e8 4f fa ff ff          callq  400c40 <__isoc99_sscanf@plt>
  4011f1:       83 f8 01                cmp    $0x1,%eax
  4011f4:       7f 05                   jg     4011fb <phase_5+0x30>
  4011f6:       e8 62 05 00 00          callq  40175d <explode_bomb>
  4011fb:       8b 04 24                mov    (%rsp),%eax
  4011fe:       83 e0 0f                and    $0xf,%eax
  401201:       89 04 24                mov    %eax,(%rsp)
  401204:       83 f8 0f                cmp    $0xf,%eax
  401207:       74 2f                   je     401238 <phase_5+0x6d>
  401209:       b9 00 00 00 00          mov    $0x0,%ecx
  40120e:       ba 00 00 00 00          mov    $0x0,%edx
  401213:       83 c2 01                add    $0x1,%edx
  401216:       48 98                   cltq
  401218:       8b 04 85 80 27 40 00    mov    0x402780(,%rax,4),%eax
  40121f:       01 c1                   add    %eax,%ecx
  401221:       83 f8 0f                cmp    $0xf,%eax
  401224:       75 ed                   jne    401213 <phase_5+0x48>
  401226:       c7 04 24 0f 00 00 00    movl   $0xf,(%rsp)
  40122d:       83 fa 0f                cmp    $0xf,%edx
  401230:       75 06                   jne    401238 <phase_5+0x6d>
  401232:       3b 4c 24 04             cmp    0x4(%rsp),%ecx
  401236:       74 05                   je     40123d <phase_5+0x72>
  401238:       e8 20 05 00 00          callq  40175d <explode_bomb>
  40123d:       48 8b 44 24 08          mov    0x8(%rsp),%rax
  401242:       64 48 33 04 25 28 00    xor    %fs:0x28,%rax
  401249:       00 00 
  40124b:       74 05                   je     401252 <phase_5+0x87>
  40124d:       e8 3e f9 ff ff          callq  400b90 <__stack_chk_fail@plt>
  401252:       48 83 c4 18             add    $0x18,%rsp
  401256:       c3                      retq
  ```

