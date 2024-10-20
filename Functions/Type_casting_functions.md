# 类型转换函数

类型转换主要包括三种操作：转换、重新解释和提升。
- **转换（Conversion）**。指将一个值的数据类型更改为另一种数据类型。这需要额外的计算，仅由 `TO_STRING()` 函数执行。
- **重新解释（Reinterpretation）**。指将表示一个值的二进制数据按不同的数据类型进行解释，而不实际更改底层数据。这由 `SINT()` 处理，不涉及额外计算；它只是重新解释现有数据。
- **提升（Promotion）**。指将一个值转换为“更大”或更精确的数据类型。它不需要额外计算，只是要求参数提供不同类型的值。仅 JSON 字段和一些其他函数可以将其值提升为整数。如果参数无法生成不同类型的值，则提升将失败。例如，`TIMEDIFF()` 函数通常返回字符串，但也可以返回数字。因此，`BIGINT(TIMEDIFF(1,2))` 可以成功执行，强制 `TIMEDIFF()` 提供一个整数值。相反，`DATE_FORMAT()` 仅返回字符串，无法生成数字，因此 `BIGINT(DATE_FORMAT(...))` 将失败。

### BIGINT()

此函数将整数参数提升为 64 位类型，而浮点参数保持不变。它的设计目的是确保在 64 位模式下评估某些表达式（如 `a*b`），即使所有参数都是 32 位的。

### DOUBLE()

`DOUBLE()` 函数将其参数提升为浮点类型。这有助于强制评估数值 JSON 字段。

### INTEGER()

`INTEGER()` 函数将其参数提升为 64 位有符号类型。它的设计目的是强制评估数值 JSON 字段。

### TO_STRING()

此函数强制将其参数转换为字符串类型。

### UINT()

`UINT()` 函数将其参数提升为 32 位无符号整数类型。

### UINT64()

`UINT64()` 函数将其参数提升为 64 位无符号整数类型。

### SINT()

`SINT()` 函数强制将其 32 位无符号整数参数重新解释为有符号类型，并将其扩展为 64 位类型（因为 32 位类型是无符号的）。例如，1-2 通常计算结果为 4294967295，但 `SINT(1-2)` 计算结果为 -1。
<!-- proofread -->
