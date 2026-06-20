# Macros

This section describes macro invocations. Macro definitions are specified
separately.

**MACRO-INVOCATION** <i class="fa-solid fa-arrow-right"></i>
- `@` IDENTIFIER
- `@` IDENTIFIER `(` ARGUMENT-EXPRESSION-LIST? `)`
- `@` IDENTIFIER MACRO-TOKEN-BLOCK
- `@` IDENTIFIER `(` ARGUMENT-EXPRESSION-LIST? `)` MACRO-TOKEN-BLOCK

**MACRO-TOKEN-BLOCK** <i class="fa-solid fa-arrow-right"></i>
- `{` TOKEN-TREE* `}`

**TOKEN-TREE** <i class="fa-solid fa-arrow-right"></i>
- TOKEN
- `(` TOKEN-TREE* `)`
- `[` TOKEN-TREE* `]`
- `{` TOKEN-TREE* `}`

The argument list and token block of a macro invocation may be omitted.

The contents of a macro token block are not parsed as regular expressions or
statements. They may contain any token sequence accepted by the lexer, with
balanced delimiters.

Examples:

```cimu
@trace
@trace(value)
@trace {
    any token sequence here
}
@trace(value) {
    if value => #text
}
```
