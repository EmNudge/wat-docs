---
title: br_table
description: Multi-way branch (switch) over an index with a default.
---

`br_table` pops an `i32` index and branches to one of several labels; out-of-range falls back to a default label. Useful for `switch`-like dispatch.

```wat
(module
  (func (param $tag i32) (result i32)
    (block $default (result i32)
      (block $case2 (result i32)
        (block $case1 (result i32)
          (block $case0 (result i32)
            local.get $tag
            br_table $case0 $case1 $case2 $default
          )
          i32.const 10
          br 3
        )
        i32.const 20
        br 2
      )
      i32.const 30
      br 1
    )
    ;; default
    i32.const -1
  )
)
```

Tips:

- Order of labels matches indices 0..n-1, then a final default.
- Each target must produce the block’s result type(s).

Further reading:

- [Control Flow Instructions](/instructions/control) - Complete reference for `block`, `loop`, `if`, `br`, `br_if`, `br_table`, etc.
- Spec: [br_table](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: create small switch exercises in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)
