---
title: return
description: Exit the current function, optionally pushing results.
---

`return` exits the current function immediately. Any required result values must already be on the stack.

```wat
(module
  (func (param $x i32) (result i32)
    local.get $x
    i32.eqz
    if
      i32.const 0
      return
    end
    i32.const 1
  )
)
```

Multi-value:

```wat
(func (param $a i32) (param $b i64) (result i32 i64)
  local.get $a
  local.get $b
  return)
```

Further reading:

- Spec: [Function results and return](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: early-exit tasks in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


