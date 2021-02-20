# 笔记

## 3.2 程序编码

`mstore.c`

```c++
long mult2(long ,long);

void multstore(long x,long y, long *dest) {
    long t = mult2(x,y);
    *dest = t;
}
```

```shell
gcc -Og -S mstore.c 
```

```assembly
	pushq	%rbx
	movq	%rdx, %rbx
	call	mult2@PLT
	movq	%rax, (%rbx)
	popq	%rbx
	ret

```

# 练习题答案

## 3.1

| 操作数             | 值    | 解释                                                       |
| ------------------ | ----- | ---------------------------------------------------------- |
| %rax               | 0x100 |                                                            |
| 0x104              | 0xAB  |                                                            |
| $0x108             | 0x108 |                                                            |
| (%rax)             | 0xff  | 间接寻址                                                   |
| 4(%rax)            | 0xAB  | Imm(r) = M[Imm+r]                                          |
| 9(%rax, $rdx)      | 0x11  | Imm(rb,ri) = M[Imm+R[rb], R[ri]] = M[9+0x100+3]            |
| 260(%rcx, %rdx)    | 0x13  | Imm(rb,ri) = M[Imm+R[rb], R[ri]] = M[260+0x1+0x3]=M[0x108] |
| 0xFC(, %rcx, %rdx) | 0xFF  | Imm(,r,s) = M[Imm + r \*s] = M[0x100]                      |
| (%rax, %rdx, 4)    | 0x11  | (rb,ri,s) = M[R[rb] + R[ri] \*s] = M[0x100+0x3 \*4]        |













