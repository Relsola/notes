# config

**记录自己常用工具的一些配置文件和配置工具**

## .editorconfig

```ini
# 全局配置 适用于所有文件
[*]

# 文件编码 UTF-8
charset = utf-8

# 使用 Tab 字符进行缩进
indent_style = tab

# 每个缩进级别相当于 2 个空格的宽度
indent_size = 2

# 行尾使用 LF
end_of_line = lf

# 文件末尾自动插入换行符
insert_final_newline = true

# 自动删除行尾的多余空格
trim_trailing_whitespace = true

# 覆盖全局设置 仅对 Markdown 文件生效
[*.md]

# 不删除行尾空格
trim_trailing_whitespace = false
```

## .clang-format

```yaml
---
# LLVM 风格
BasedOnStyle: LLVM

# 行宽限制0 不限制代码行长度
ColumnLimit: 0

#  没有 else 分支时允许短 if 语句放在一行
AllowShortIfStatementsOnASingleLine: WithoutElse

# 头文件不自动排序
SortIncludes: Never
```
