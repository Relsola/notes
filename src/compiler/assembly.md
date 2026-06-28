# 汇编语言

## x86 汇编基础

### 语法风格

Intel 语法：

```asm
mov rax, rbx
```

AT&T 语法：

```asm
movq %rbx, %rax
```

本文以 intel 语法为主

### 寄存器

#### 通用寄存器

| 64 位 | 32 位 | 16 位 | 8 位  |
| ----- | ----- | ----- | ----- |
| `rdi` | `edi` | `di`  | `dil` |
| `rsi` | `esi` | `si`  | `sil` |
| `rdx` | `edx` | `dx`  | `dl`  |
| `rcx` | `ecx` | `cx`  | `cl`  |
| `r8`  | `r8d` | `r8w` | `r8b` |
| `r9`  | `r9d` | `r9w` | `r9b` |

#### 栈相关寄存器

栈空间：后进先出，从高地址往低地址增长

`rsp` (stack pointer) : 当前栈顶指针

`rbp` (base/frame pointer) : 当前函数栈帧的基准指针

```asm
push rbp      # 保存上一个函数栈基指针
mov rbp, rsp  # 设置当前栈基指针

mov rsp, rbp
pop rbp
ret
```

#### Flags 标志寄存器

cmp、test、add、sub 等指令都会修改 EFLAGS。

常用标志：

ZF：结果为 0

CF：产生进位

SF：结果为负

OF：有符号溢出

### 常用指令

#### mov

移动，目标和源位宽必须一致。

```asm
mov al,  bl

mov ax,  bx

mov eax, ebx

mov rax, rbx
```

如果需要扩展

```asm
movzx  eax, al    # 零扩展，高位填充零

movsx  eax, al    # 符号扩展，高位填充低位符号位的值

movsxd rax, eax  # 将 32 位有符号扩展到 64 位
```

内存寻址

```asm
mov rax, [0x1000]        # 直接寻址

mov rax, [rbx]           # 基址寻址

mov rax, [rbx + 8]       # 偏移寻址

mov rax, [rbx + rcx * 8] # 数组寻址
```

x86 大多数指令最多只能有一个内存操作数。

```asm
mov [rax], [rbx]        # 不允许
```

内存大小

| 类型  | 大小    |
| ----- | ------- |
| byte  | 1 Byte  |
| word  | 2 Byte  |
| dword | 4 Byte  |
| qword | 8 Byte  |
| oword | 16 Byte |

```asm
mov al,  byte ptr  [rax]

mov ax,  word ptr  [rax]

mov eax, dword ptr [rax]

mov rax, qword ptr [rax]
```

#### 算术

加减法

```asm
add rax, rbx  # rax = rax + rbx

sub rax, rbx  # rax = rax - rbx
```

乘法

```asm
imul rax, rbx  # 有符号乘法 rax = rax * rbx

mul eax, ecx   # 无符号乘法 eax = eax * ecx

mul rbx        # 一操作数  rax = rax * rbx
```

除法

```asm
idiv rbx       # 有符号除法
```

`div rcx` 实际操作为 `rax / rcx`，其中商放在 `rax` 中，余数放在 `rdx` 中

```asm

inc rax           # 自增

dec rax           # 自减

neg rax           # 取负
```

#### 比较


```asm
cmp rax, rbx      # 比较两个操作数

test rax, rax     # 按位与，仅修改标志位
```

`cmp` 本质执行减法，仅影响 EFLAGS，不保存结果。

`test` 本质执行按位与，常用于判断是否为 0。


#### 跳转

```asm
jmp label         # 无条件跳转

je label          # 相等

jne label         # 不相等

jg label          # 大于（有符号）

jge label         # 大于等于

jl label          # 小于

jle label         # 小于等于

ja label          # 大于（无符号）

jb label          # 小于（无符号）
```

#### 函数调用

```asm
call func     # 调用函数

ret           # 返回
```

`call` 会将下一条指令地址压栈，然后跳转。

`ret` 从栈中弹出返回地址继续执行。

#### 栈操作

```asm
push rax  # 入栈 rsp -= 8

pop rax   # 出栈 rsp += 8
```

#### lea 指令

`lea` 计算地址，不访问内存。

```asm
mov rax, [rbx]      # 读取内存

lea rax, [rbx]      # # 获取地址

lea rax, [rbx + 8]

lea rax, [rbx + rcx * 4]
```

### 其他

```asm
nop
```

不执行任何操作，占用一个指令周期，常用于代码对齐、热补丁、调试。
