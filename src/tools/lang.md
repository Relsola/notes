# Lang

## C/C++

当前我使用的版本为 GNU++14，主要使用 C 语法，并使用少量 C++ 特性进行改善。

### 枚举

1. C 枚举

枚举值会暴露到外层作用域

可以隐式转换为 `int` 类型

```c
enum { Red, Green, Blue };
```

```c
typedef enum { Red, Green, Blue } Color;
```

2. C++ 枚举

作用域枚举

显式指定底层类型

```cpp
enum struct Color : unsigned int { Red, Green, Blue };
```
