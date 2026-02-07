---
title: "Bitwise & Shifts"
description: and, or, xor, shifts, and rotates for integers.
---


Bitwise ops are for integers only.

```wat
(module
  (func (export "bits") (param $x i32) (param $y i32) (result i32)
    local.get $x
    local.get $y
    i32.and)                ;; i32.or, i32.xor
)
```

Shifts/rotates:

```wat
(module
  (func (export "shifts") (param $x i32) (param $amt i32) (result i32)
    local.get $x
    local.get $amt
    i32.shl)                ;; i32.shr_s, i32.shr_u, i32.rotl, i32.rotr
)
```

Also available for `i64.*`.

Reference:
- [i32 Instructions](/instructions/i32) - Complete i32 instruction reference
- [i64 Instructions](/instructions/i64) - Complete i64 instruction reference
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: bitwise tasks in https://github.com/EmNudge/watlings


