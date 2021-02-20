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

| 操作数  | 值    | 解释              |
| ------- | ----- | ----------------- |
| %rax    | 0x100 |                   |
| 0x104   | 0x104 |                   |
| $0x108  | 0x108 |                   |
| (%rax)  | 0xff  | 间接寻址          |
| 4(%rax) | 0xAB  | Imm(r) = M[Imm+r] |
|         |       |                   |
|         |       |                   |
|         |       |                   |













