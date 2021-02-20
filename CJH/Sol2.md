# 笔记

## 2.1 信息存储

### show_bytes

```c
#include <stdio.h>
typedef unsigned char * byte_pointer;

void show_bytes(byte_pointer start, size_t len) {
    size_t i;
    for(i = 0; i<len; i++)
        printf(" %.2x", start[i]);
    printf("\n");
}

void show_int(int x) {
    show_bytes((byte_pointer)&x, sizeof(int));
}

void show_float(float x) {
    show_bytes((byte_pointer)&x, sizeof(float));
}

void show_pointer(void *x) {
    show_bytes((byte_pointer)&x, sizeof(void));
}

```



## 2.3 整数运算

### 负数移位

```c
#include <stdio.h>

int main() {
    int a = (-17)>>4; // FFFFFFEF FFFFFFFE -2
    printf("%08X %08X %d\n",-17,a,a);
    
    a = (-17)/16; // FFFFFFEF FFFFFFFF -1
    printf("%08X %08X %d\n",-17,a,a);

    a = 17/16; // 00000011 00000001 1
    printf("%08X %08X %d\n",17,a,a);
}
```

​	

# 习题答案

## 16

| x                | x<<3             | x>>3 逻辑        | x>>2 算术        |
| ---------------- | ---------------- | ---------------- | ---------------- |
| 0b11000011, 0xC3 | 0b00011000, 0x18 | 0x00011000, 0x18 | 0x11111000, 0xF8 |
| 0b01110101, 0x75 | 0b10101000, 0xA8 | 0x00001110, 0x0E | 0b00011101, 0x1D |
| 0b10000111, 0x87 | 0b00111000, 0x38 | 0b00010000, 0x10 | 0b11100001, 0xE1 |
| 0b01100110, 0x66 | 0b00110000, 0x30 | 0b00001100, 0x0A | 0b00001100, 0x0A |

## 22

这是（2.3）
$$
B2T_{w}(\vec{x}) \doteq -x_{w-1} 2^{w+1} + \sum_{i=0}^{w-2} x_i 2^i
$$
A [1011]
$$
B2T_{w}([1011]) = -2^3 + 2^1 + 2^0 \\
= -8 + 2 + 1 \\
= -5
$$


B[11011]
$$
B2T_{w}([11011]) = -2^4 + 2^3 + 2^1 + 2^0 \\
= - 2^3 + 2^1 + 2^0 \\
= -8 + 2 + 1 \\
= -5
$$


C[111011]
$$
B2T([111011]) = -2^5 + 2^4 + 2^3 + 2^1 + 2^0 \\
= -2^4 + 2^3 + 2^1 + 2^0 \\
= - 2^3 + 2^1 + 2^0 \\
= -8 + 2 + 1 \\
= -5
$$





## 23

```cpp
#include <stdio.h>

int fun1(unsigned word) {
    return (int)( (word<<24) >> 24) ;
}

int fun2(unsigned word) {
    return ((int)word<<24) >> 24 ;
}

int main() {
    unsigned w;
    w = 0x00000076; printf("%08X %08X\n", fun1(w) , fun2(w) );
    w = 0x87654321; printf("%08X %08X\n", fun1(w) , fun2(w) );
    w = 0x000000c9; printf("%08X %08X\n", fun1(w) , fun2(w) );
    w = 0xEDCBA987; printf("%08X %08X\n", fun1(w) , fun2(w) );
    return 0;
}
```



## 25

对于unsigned，-1 = UMAX

要改成

```
i<length
```

## 26

A. s比t短的时候

B. 左边是unsigned

C. `strlen(s) > strlen(t)`

## 27

```cpp
/* Determine whether arguments can be added without overflow */
int uadd_ok(unsigned x, unsigned y) {
    return x+y<x;
}
```

## 28

| 0    | 0    | 0    |
| ---- | ---- | ---- |
| 5    | 11   | B    |
| 8    | 8    | 8    |
| 13   | 3    | 3    |
| 15   | 1    | 1    |

## 31

因为它永真。

## 38

| k    | b    | 倍数 |
| ---- | ---- | ---- |
| 0    | 0    | 0    |
| 1    | a    | 2    |
| 2    | 0    | 4    |
| 3    | a    | 8    |
| 0    | 0    | 1    |
| 1    | a    | 3    |
| 2    | 0    | 5    |
| 3    | a    | 9    |

## 39

$$
-(x\ll m)
$$

## 40

|      |      |      |                             |
| ---- | ---- | ---- | --------------------------- |
|      |      |      | $(x\ll 2) + (x \ll 1)$      |
|      |      |      | $(x\ll 5) -x$               |
|      |      |      | $(x \ll 1) - (x \ll 3)$     |
|      |      |      | $(x \ll 6) - (x \ll 3) - x$ |

## 41

只有个1时选择第一种，否则选择第二种

## 47

| 位      | $e$  | $E$  | $2^E$       | $f$          | $M$          | $2^E \times M$ | $V$          | 十进制 |
| ------- | ---- | ---- | ----------- | ------------ | ------------ | -------------- | ------------ | ------ |
| 0 00 00 | 0    | -1   | $1 \over 2$ | $0 \over 4$  | $4 \over 4$  | $1 \over 2$    | $1 \over 2$  | 0.5    |
| 0 00 01 | 0    | -1   | $1 \over 2$ | $ 1 \over 4$ | $5 \over 4$  | $ 5 \over 8$   | $ 5 \over 8$ | 0.625  |
| 0 00 10 | 0    | -1   | $1 \over 2$ | $2 \over 4$  | $6 \over 4$  | $ 6 \over 8$   | $3 \over 4$  | 0.75   |
| 0 00 11 | 0    | -1   | $1 \over 2$ | $3 \over 4$  | $ 7 \over 4$ | $ 7 \over 8$   | $ 7 \over 8$ | 0.875  |
| 0 01 00 | 1    | 0    | 1           | $0 \over 4$  | $4 \over 4$  | $4 \over 4$    | 1            | 1.0    |
| 0 01 01 | 1    | 0    | 1           | $ 1 \over 4$ | $5 \over 4$  | $5 \over 4$    | $5 \over 4$  | 1.25   |
|         |      |      |             |              |              |                |              |        |
|         |      |      |             |              |              |                |              |        |
|         |      |      |             |              |              |                |              |        |
|         |      |      |             |              |              |                |              |        |
|         |      |      |             |              |              |                |              |        |
|         |      |      |             |              |              |                |              |        |
| 0 11 00 | -    | -    | -           | -            | -            | -              |              | -      |
| 0 11 01 | -    | -    | -           | -            | -            | -              |              | -      |
| 0 11 10 | -    | -    | -           | -            | -            | -              |              | -      |
| 0 11 11 | -    | -    | -           | -            | -            | -              |              | -      |



## 48

$$
0x00359141 = \\
(0000 \ 0000 \ 0011 \ 0101 \ 1001 \ 0001 \ 0100 \ 0001)_2 \\
= 1.1  0101  1001  0001  0100  0001 \times 2^{21} \\
$$

用IEEE单精度表示。

21要加上偏置量127 等于148；长度21后面要加两个0。
$$
0b 0 \ 10010100 \ 1  0101  1001  0001  0100  000100 \\
= 0b 0100 \ 1010 \ 0101 \ 0110 \ 0100 \ 0101 \ 0000 \ 0100 \\
= 0x 4A 564504
$$





















