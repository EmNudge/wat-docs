---
title: Constants
description: i32.const, i64.const, f32.const, f64.const and using immediates.
---

Push literal values onto the stack.

```wat
(module
  (func (export "consts") (result i32)
    i32.const 42)             ;; i64.const, f32.const, f64.const
)
```

Hex and floats:

```wat
(module
  (func
    i32.const 0xFF
    f64.const 3.14159)
)
```

Reference:

- [i32 Instructions](/instructions/i32#i32const) - `i32.const` reference
- [i64 Instructions](/instructions/i64#i64const) - `i64.const` reference
- [f32 Instructions](/instructions/f32#f32const) - `f32.const` reference
- [f64 Instructions](/instructions/f64#f64const) - `f64.const` reference
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: constants in https://github.com/EmNudge/watlings
