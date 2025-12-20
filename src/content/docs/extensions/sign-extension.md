---
title: "Sign-extension Operators"
description: "Extend smaller integer widths to larger ones with sign preservation."
---

These operators widen integers while preserving the sign of the smaller type.

```wat
(module
  (func (export "ext8") (param $x i32) (result i32)
    local.get $x
    i32.extend8_s)      ;; sign-extend low 8 bits to 32-bit

  (func (export "ext16") (param $x i32) (result i32)
    local.get $x
    i32.extend16_s)

  (func (export "ext32") (param $x i64) (result i64)
    local.get $x
    i64.extend32_s)
)
```

References:

- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: integer ops in https://github.com/EmNudge/watlings


