---
title: 'Reference Types (externref)'
description: 'Hold references to host objects and use function references.'
---

This extension lets Wasm store references to host objects (`externref`) and introduces more flexible function references. See the Language page for fundamentals.

- Start here: [/reference-types/](/reference-types/)
- Use with tables and `call_indirect` for dynamic dispatch.

References:

- [Reference Instructions](/instructions/reference) - `ref.null`, `ref.func`, `ref.is_null`, etc.
- [Table Instructions](/instructions/table) - `table.get`, `table.set`, etc.
- [Type Names](/instructions/types) - `funcref`, `externref`, etc.
- Spec: https://webassembly.github.io/spec/core/syntax/index.html
- Practice: function tables in https://github.com/EmNudge/watlings
