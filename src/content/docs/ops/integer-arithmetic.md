---
title: Integer Arithmetic
description: i32/i64 add, sub, mul, div, rem and typical usage.
---


Instructions wrap on overflow (two’s complement). Division by zero traps.

## add, sub, mul

```wat
(module
  (func (export "ops") (param $x i32) (param $y i32) (result i32)
    local.get $x
    local.get $y
    i32.add)                 ;; i32.sub, i32.mul
)
```

## div and rem

Signed vs unsigned matter for negatives:

```wat
(module
  (func (export "divrem") (param $x i32) (param $y i32) (result i32)
    local.get $x
    local.get $y
    i32.div_s)               ;; i32.div_u for unsigned
)
```

Remainder:

```wat
(module
  (func (export "rem") (param $x i32) (param $y i32) (result i32)
    local.get $x
    local.get $y
    i32.rem_s)               ;; i32.rem_u
)
```

Also available for `i64.*`.

Reference:
- [i32 Instructions](/instructions/i32) - Complete i32 instruction reference
- [i64 Instructions](/instructions/i64) - Complete i64 instruction reference
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: integers in https://github.com/EmNudge/watlings


