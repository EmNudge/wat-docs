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
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: constants in https://github.com/EmNudge/watlings


