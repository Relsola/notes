# C/C++ 编程

我喜欢C的简洁性，但也会使用一些 C++特性提升开发效率。 : )

## 内存管理

如何管理内存，使 CPU 尽可能多的命中缓存是程序快速运行的关键

## C 程序运行

C 程序从源代码到运行大致经过以下主要阶段：

1. 预处理（Preprocessing）

   - 处理 `#include`、`#define` 与条件编译，生成翻译单元。

2. 编译与汇编（Compilation & Assembly）

   - 编译器将翻译单元翻译为汇编代码，汇编器生成目标文件（`.o` / `.obj`）。

3. 链接（Linking）

   - 链接器合并目标文件与库（静态或动态），解析符号并执行重定位，生成可执行文件或共享库（例如 ELF、PE、`.so`、`.dll`）。

4. 加载与执行（Loading & Execution）
   - 操作系统加载器把可执行文件载入内存；动态链接器在运行时按需加载共享库并完成符号解析；运行时环境（如 CRT）初始化后，程序从入口点开始执行。

附注 — 常用命令示例：

```bash
gcc -c foo.c      # 生成目标文件 foo.o
gcc foo.o -o foo  # 链接生成可执行文件
```

## C 程序编译

1. 编译器选择 Clang GCC ...

2. 编译参数 （Clang 示例）

| 参数示例                 | 含义                                                                                   |
| ------------------------ | -------------------------------------------------------------------------------------- |
| `-std=gnu++20`           | 指定 GNU 风格 C++20 标准                                                               |
| `-g`                     | 调试模式                                                                               |
| `-c`                     | 只编译不链接                                                                           |
| `-O0`                    | 不进行优化                                                                             |
| `-o`                     | 输出到流或文件                                                                         |
| `-luser32 -lgdi32`       | -l 链接 user32 gdi32 ，Windows 编程链接库                                              |
| `-Wl,/SUBSYSTEM:WINDOWS` | -Wl, 将后面的参数传递给链接器 /SUBSYSTEM:WINDOWS 是 MSVC 链接器的参数，指定为 GUI 程序 |

## C 程序 Debugger

1. 断点调试

2. 反汇编查看

## C/C++ 编程

C 语言会尝试将你的输入进行跨平台处理，如将 \n 处理为换行，unix 使用 \n 换行，但 Windows 使用 \r\n 换行，如果不想你的流被处理，使用二进制模式

结构体对齐，栈变量对齐，CPU 访问 32 位边界比非边界快得多

数组和结构体都是 C 语言中内存布局的一种描述，但数组指针有一些特别。

二进制，位运算，运算符优先级

变量、运算、流程控制、作用域

链接导入库：静态链接 动态链接（优雅降级） 打包链接库（DLL 等）

浮点数 + 0.5f 截断是一个不错的四舍五入技巧

## x86_64 asm

C 代码：

```C
int a = 10;
a = a + 1;
```

翻译的 x86 汇编表示：

```asm
    mov  dword ptr [a],0Ah
    mov  eax,dword ptr [a]
    add  eax,1
    mov  dword ptr [a],eax
```

## 构建

## 栈分配和堆分配

## C 与 C++ 互操作

z.h

```c
typedef struct {
  int x;
  double y;
} vector;

#ifdef __cplusplus
extern "C" {
#endif

void add(vector a, vector b, vector *res);

#ifdef __cplusplus
}
#endif
```

z1.c

```c
#include "z.h"
#include <stdio.h>
#include <stdlib.h>

static vector a = {1, 3.5};
static vector b = {3, .5};

int main() {
  vector *res = (vector *)malloc(sizeof(vector));
  add(a, b, res);
  printf("  c -> vector { x: %d, y: %.2f }\n", res->x, res->y);
  return 0;
}
```

z2.cc

```cpp
#include "z.h"
#include <format>
#include <iostream>

template <typename T>
constexpr T _add(T a, T b) noexcept { return a + b; }

vector inline operator+(vector &a, vector &b) { return vector{_add(a.x, b.x), _add(a.y, b.y)}; }

extern "C" void add(vector a, vector b, vector *res) {
  *res = _add(a, b);
  std::cout << std::format("cpp -> vector {{ x: {}, y: {:.2f} }}", res->x, res->y) << '\n';
}
```

output

```bash
$ clang -std=gnu17 -c -o z1.o z1.c
$ clang -std=gnu++20 -c -o z2.o z2.cc
$ clang -std=gnu17 -o main z1.o z2.o
$ ./main

# output
# cpp -> vector { x: 4, y: 4.00 }
#   c -> vector { x: 4, y: 4.00 }
```

## 性能与编译优化

指针别名会干扰编译器优化

不需要过早优化，注重核心热点代码的优化（直接查看编译的汇编）

## 编程风格

1. 函数顶部前置声明变量
2. 使用断言进行边界检查
3. `if` 判错提前退出避免作用域嵌套
