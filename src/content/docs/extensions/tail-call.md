---
title: "Tail Calls"
description: "return_call and return_call_indirect for optimized recursion."
---

Tail calls allow a function to transfer control to another function as its final action without growing the stack.

```wat
(module
  (func $f (param $n i32) (result i32)
    local.get $n
    i32.eqz
    if (result i32)
      i32.const 0
    else
      local.get $n
      i32.const 1
      i32.sub
      return_call $f
    end)
)
```

References:

- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: recursion fundamentals in https://github.com/EmNudge/watlings


