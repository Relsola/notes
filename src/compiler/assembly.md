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


### 通用寄存器

RAX
RBX
RCX
RDX


### 内存寻址

```asm
; 直接寻址
mov rax, [0x1000]

; 基址寻址
mov rax, [rbx]

; 偏移寻址
mov rax, [rbx+8]

; 数组寻址
mov rax, [rbx+rcx*8]
```
