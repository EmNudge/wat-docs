---
title: 'Exception Handling'
description: 'Try/catch/throw for native exception support in Wasm.'
---

Exception handling introduces `try`, `catch`, `throw`, and related constructs for structured error handling.

```wat
(module
  (tag $e (param i32))  ;; exception tag carrying an i32

  (func (export "mayThrow") (param $x i32) (result i32)
    (try (result i32)
      (do
        local.get $x
        i32.eqz
        if
          i32.const 1
          throw $e
        end
        i32.const 0
      )
      (catch $e
        ;; handle and return a value
        i32.const -1
      )
    )
  )
)
```

References:

- [Exception Instructions](/instructions/exceptions) - Complete reference for `throw`, `throw_ref`, `rethrow`, `tag`, `try_table`, `catch`, `catch_all`, etc.
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: error control in https://github.com/EmNudge/watlings
