# Expressions

**EXPRESSION** <i class="fa-solid fa-arrow-right"></i>
- ASSIGNMENT-EXPRESSION

**PRIMARY-EXPRESSION** <i class="fa-solid fa-arrow-right"></i> 
- IDENTIFIER
- LITERAL
- `nil`
- `true`
- `false`
- `(` EXPRESSION `)`
- IF-EXPRESSION
- SWITCH-EXPRESSION
- MACRO-INVOCATION

**POSTFIX-EXPRESSION** <i class="fa-solid fa-arrow-right"></i> 
- PRIMARY-EXPRESSION
- POSTFIX-EXPRESSION `[` EXPRESSION `]`
- POSTFIX-EXPRESSION `.` IDENTIFIER
- POSTFIX-EXPRESSION `(` ARGUMENT-EXPRESSION-LIST `)`

**ARGUMENT-EXPRESSION-LIST** <i class="fa-solid fa-arrow-right"></i>
- EXPRESSION
- ARGUMENT-EXPRESSION-LIST `,` EXPRESSION

**UNARY-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i> 
- POSTFIX-EXPRESSION
- UNARY-OPERATOR UNARY-EXPRESSION

**UNARY-OPERATOR**  <i class="fa-solid fa-arrow-right"></i> 
- `+`
- `-`
- `!`
- `~`

**CAST-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i>
- UNARY-EXPRESSION
- CAST-EXPRESSION `as` TYPE

**MULTIPLICATIVE-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i> 
- CAST-EXPRESSION
- MULTIPLICATIVE-EXPRESSION `*` CAST-EXPRESSION
- MULTIPLICATIVE-EXPRESSION `/` CAST-EXPRESSION
- MULTIPLICATIVE-EXPRESSION `%` CAST-EXPRESSION


**ADDITIVE-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i> 
- MULTIPLICATIVE-EXPRESSION
- ADDITIVE-EXPRESSION `+` MULTIPLICATIVE-EXPRESSION
- ADDITIVE-EXPRESSION `-` MULTIPLICATIVE-EXPRESSION

**SHIFT-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i> 
- ADDITIVE-EXPRESSION
- SHIFT-EXPRESSION `>>` ADDITIVE-EXPRESSION
- SHIFT-EXPRESSION `<<` ADDITIVE-EXPRESSION

**BITWISE-AND-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i>
- SHIFT-EXPRESSION
- BITWISE-AND-EXPRESSION `&` SHIFT-EXPRESSION

**BITWISE-XOR-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i>
- BITWISE-AND-EXPRESSION
- BITWISE-XOR-EXPRESSION `^` BITWISE-AND-EXPRESSION

**BITWISE-OR-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i>
- BITWISE-XOR-EXPRESSION
- BITWISE-OR-EXPRESSION `|` BITWISE-XOR-EXPRESSION

**RELATIONAL-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i> 
- BITWISE-OR-EXPRESSION
- RELATIONAL-EXPRESSION `>=` BITWISE-OR-EXPRESSION
- RELATIONAL-EXPRESSION `<=` BITWISE-OR-EXPRESSION
- RELATIONAL-EXPRESSION `>` BITWISE-OR-EXPRESSION
- RELATIONAL-EXPRESSION `<` BITWISE-OR-EXPRESSION

**EQUALITY-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i> 
- RELATIONAL-EXPRESSION
- EQUALITY-EXPRESSION `==` RELATIONAL-EXPRESSION
- EQUALITY-EXPRESSION `!=` RELATIONAL-EXPRESSION

**LOGICAL-AND-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i>
- EQUALITY-EXPRESSION
- LOGICAL-AND-EXPRESSION `&&` EQUALITY-EXPRESSION

**LOGICAL-OR-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i>
- LOGICAL-AND-EXPRESSION
- LOGICAL-OR-EXPRESSION `||` LOGICAL-AND-EXPRESSION

**NIL-COALESCING-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i>
- LOGICAL-OR-EXPRESSION
- NIL-COALESCING-EXPRESSION `??` LOGICAL-OR-EXPRESSION

The `??` operator evaluates to the value carried by `Some`, or evaluates to the
expression on its right-hand side when the left-hand side is the `None` case.

**ASSIGNMENT-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i>
- NIL-COALESCING-EXPRESSION
- UNARY-EXPRESSION ASSIGNMENT-OPERATOR ASSIGNMENT-EXPRESSION

**ASSIGNMENT-OPERATOR**  <i class="fa-solid fa-arrow-right"></i>
- `=`
- `+=`
- `-=`
- `*=`
- `/=`

**IF-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i>
- `if` EXPRESSION BLOCK-EXPRESSION
- `if` EXPRESSION BLOCK-EXPRESSION `else` BLOCK-EXPRESSION
- `if` EXPRESSION BLOCK-EXPRESSION `else` IF-EXPRESSION

An `if` expression evaluates to the value of the selected branch.

**SWITCH-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i>
- `switch` EXPRESSION `{` SWITCH-ARM-LIST? `}`

**SWITCH-ARM-LIST**  <i class="fa-solid fa-arrow-right"></i>
- SWITCH-ARM
- SWITCH-ARM-LIST `,` SWITCH-ARM

**SWITCH-ARM**  <i class="fa-solid fa-arrow-right"></i>
- SWITCH-PATTERN `=>` EXPRESSION
- SWITCH-PATTERN `=>` BLOCK-EXPRESSION

**SWITCH-PATTERN**  <i class="fa-solid fa-arrow-right"></i>
- LITERAL
- `nil`
- `true`
- `false`
- `_`
- `default`
- IDENTIFIER
- IDENTIFIER `(` PATTERN `)`

**PATTERN**  <i class="fa-solid fa-arrow-right"></i>
- IDENTIFIER
- LITERAL
- `nil`
- `true`
- `false`
- `_`

When switching over an enum, an identifier pattern matches an enum variant.
When switching over a tagged union, an identifier pattern matches a case without
a payload, and `IDENTIFIER ( PATTERN )` matches a case with a payload and
destructures that payload.

**BLOCK-EXPRESSION**  <i class="fa-solid fa-arrow-right"></i>
- `{` STATEMENT-LIST? EXPRESSION? `}`

Examples:

```cimu
flags & mask
flags | enabled
flags ^ toggled

name ?? "Unknown"

var display = switch name {
    Some(value) => value,
    None => "Unknown",
};

var title = if unlocked {
    "Extra"
} else {
    "Locked"
};

var line = switch mood {
    Happy => "Welcome back.",
    Sad => "Are you alright?",
    default => "Hello.",
};

var message = switch result {
    Ok(value) => value,
    Err(error) => error.message,
};
```

