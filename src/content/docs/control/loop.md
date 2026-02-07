---
title: loop
description: Repeat a block; branches target the top to continue.
---


`loop` behaves like a labeled loop. Branching to its label jumps to the top (continue).

```wat
(module
  (func (param $n i32) (result i32)
    (local $acc i32)
    i32.const 0
    local.set $acc
    (loop $again
      local.get $n
      i32.eqz
      br_if $done

      local.get $acc
      i32.const 1
      i32.add
      local.set $acc

      local.get $n
      i32.const 1
      i32.sub
      local.set $n

      br $again
    )
    (block $done)
    local.get $acc)
)
```

Tips:

- Use `br_if` to conditionally continue or exit.
- Combine with an outer `block` label for a clean break target.

Further reading:

- [Control Flow Instructions](/instructions/control) - Complete reference for `block`, `loop`, `if`, `br`, `br_if`, etc.
- Spec: [Control instructions](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: related repetitions in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


