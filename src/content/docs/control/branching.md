---
title: "br & br_if"
description: Structured branches to labeled blocks and loops.
---


`br $label` performs an unconditional jump to the end of a `block` or to the top of a `loop`. `br_if` pops a condition and branches if non-zero.

```wat
(module
  (func (param $n i32) (result i32)
    (block $exit (result i32)
      local.get $n
      i32.const 10
      i32.gt_s
      br_if $exit            ;; early return 1 for n > 10
      i32.const 1
      br $exit
    )
  )
)
```

Relative labels:

```wat
;; br 0 targets the innermost label; br 1 jumps one level out, etc.
(block (result i32)
  (block (result i32)
    i32.const 42
    br 1            ;; exits the outer block, leaving 42 as its result
  )
)
```

Further reading:

- [Control Flow Instructions](/instructions/control) - Complete reference for `block`, `loop`, `if`, `br`, `br_if`, etc.
- Spec: [Branching and label indices](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: explore labeled blocks in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


