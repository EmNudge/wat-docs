---
title: block
description: Structured block with optional result type and label targets.
---

`block` creates a new label and scope. It can optionally produce results.

```wat
(module
  (func (param $n i32) (result i32)
    (block $out (result i32)
      local.get $n
      i32.const 0
      i32.eq
      br_if $out           ;; early-exit with the top-of-stack value (0/1)
      i32.const 42         ;; normal path value
    )
  )
)
```

Notes:

- Label names are optional; you can target blocks by relative depth as well.
- A block with a `(result ...)` must leave that value on the stack on all exits.

Further reading:

- Spec: [Blocks and result types](https://webassembly.github.io/spec/core/syntax/index.html)
- Practice: browse exercises in [watlings](https://github.com/EmNudge/watlings/tree/main/exercises)


