---
title: 'Exception Handling'
description: 'Try/catch/throw for native exception support in Wasm.'
---

Exception handling introduces `try`, `catch`, `throw`, and related constructs for structured error handling.

```wat
(module
  (tag $e (param i32))

  (func (export "mayThrow") (param $x i32) (result i32)
    (try (result i32)
      (do
        (if (i32.eqz (local.get $x))
          (then (throw $e (i32.const 1))))
        (i32.const 0))
      (catch $e
        (drop)
        (i32.const -1))))
)
```

## Instruction Reference

- [Exception Instructions](/instructions/exceptions) — `throw`, `throw_ref`, `rethrow`, `tag`, `try_table`, `catch`, `catch_all`
