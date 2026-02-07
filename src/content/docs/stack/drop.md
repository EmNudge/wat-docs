---
title: drop
description: Discard the top-of-stack value.
---


`drop` removes the top value from the stack. It’s handy when an intermediate result is not needed.

```wat
(module
  (func (result i32)
    i32.const 10
    i32.const 20
    drop           ;; drops 20
    ;; stack: [10]
  )
)
```

Tips:

- Keep an eye on stack discipline. `drop` is the simplest way to balance unwanted values.
- Combine with `block (result ...)` to ensure correct outputs from structured constructs.

References:

- [Parametric Instructions](/instructions/parametric) - Complete reference for `drop`, `select`
- Spec: [Parametric instructions — drop](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: stack exercises in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


