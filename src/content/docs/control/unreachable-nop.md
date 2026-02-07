---
title: "unreachable & nop"
description: Trap immediately, or do nothing.
---


- `unreachable` traps when executed. Helpful for asserting impossible states.
- `nop` does nothing; occasionally useful as a placeholder.

```wat
(module
  (func (param $x i32)
    local.get $x
    i32.const 0
    i32.lt_s
    if
      ;; negative not allowed
      unreachable
    else
      nop
    end
  )
)
```

Further reading:

- [Control Flow Instructions](/instructions/control) - Complete reference for `unreachable`, `nop`, etc.
- Spec: [Parametric and control instructions](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: insert guards in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


