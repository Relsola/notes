# 代码生成


## 函数调用约定

### 一些概念

非易失寄存器 `callee-saved` : 

易失寄存器 `caller-saved` :  

### Windows x64 Microsoft ABI

整数/指针参数寄存器: `RCX`, `RDX`, `R8`, `R9` 共 4 个

浮点参数寄存器: `XMM0` - `XMM3` 共 4 个

更多参数走栈

调用者必须预留 32 字节 `shadow space`

返回值寄存器： `RAX`

易失寄存器: `R10`

### Linux x86-64 System V ABI

整数/指针参数寄存器: `RDI`, `RSI`, `RDX`, `RCX`, `R8`, `R9` 共 6 个

浮点参数寄存器: `XMM0` - `XMM7` 共 8 个

更多参数走栈

有 `red zone` : 栈指针下方 128 字节可临时用

返回值寄存器： `RAX`

易失寄存器: `RDI`
