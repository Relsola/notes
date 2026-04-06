# 位运算

## 位运算符和运算规则

| 符号 | 描述 | 运算规则                                    |
| ---- | ---- | ------------------------------------------- |
| `&`  | 与   | 两个位都为1时，结果才为1                    |
| `\|` | 或   | 两个位都为0时，结果才为0                    |
| `^`  | 异或 | 两个位相同为0，相异为1                      |
| `~`  | 取反 | 0变1，1变0                                  |
| `<<` | 左移 | 各二进位全部左移若干位，高位丢弃，低位补0   |
| `>>` | 右移 | 各二进位全部右移若干位，高位补0或符号位补齐 |

复合运算符如 `a &= b` 解释为 `a = a & b`


## 位运算应用

### 表示组合

这里以C语言类型组合语法解析为例

关键字顺序无关

```c
long int
int long
```

有效组合是有限集合

```c
bool

char
signed char

short
short int
short short
short short int

// ...

long
long int
long long
long long int
signed long
signed long int
signed long long
signed long long int
```

用`位计数器`表示类型组合,每种类型关键字占`2 bit` ,可以表示出现次数，如 `long long`

```c
enum {
  VOID     = 1 << 0,
  BOOL     = 1 << 2,
  CHAR     = 1 << 4,
  SHORT    = 1 << 6,
  INT      = 1 << 8,
  LONG     = 1 << 10,
  FLOAT    = 1 << 12,
  DOUBLE   = 1 << 14,
  OTHER    = 1 << 16,
  SIGNED   = 1 << 17,
  UNSIGNED = 1 << 18,
};
```

`+=` 计算出现次数，`|=` 记录是否出现

```c
int counter = 0;

if (equal(tok, "void")) 
	counter += VOID;
else if (equal(tok, "_Bool")) 
	counter += BOOL;
else if (equal(tok, "char")) 
	counter += CHAR;
// ...
else if (equal(tok, "signed"))
	counter |= SIGNED;
else if (equal(tok, "unsigned"))
	counter |= UNSIGNED;
```

用 `switch` 做合法组合归约

```c
switch (counter) {
  case VOID:
    break;
  case BOOL:
    break;
  case CHAR:
  case SIGNED + CHAR:
    break;
  case UNSIGNED + CHAR:
    break;

    // ...

  case LONG:
  case LONG + INT:
  case LONG + LONG:
  case LONG + LONG + INT:
  case SIGNED + LONG:
  case SIGNED + LONG + INT:
  case SIGNED + LONG + LONG:
  case SIGNED + LONG + LONG + INT:
    break;
  case UNSIGNED + LONG:
  case UNSIGNED + LONG + INT:
  case UNSIGNED + LONG + LONG:
  case UNSIGNED + LONG + LONG + INT:
    break;
  default:
}
```
