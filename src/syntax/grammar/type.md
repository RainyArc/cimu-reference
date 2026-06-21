# Types

**TYPE** <i class="fa-solid fa-arrow-right"></i>
- ARRAY-TYPE
- ARRAY-TYPE `?`

**ARRAY-TYPE** <i class="fa-solid fa-arrow-right"></i>
- NONNULL-TYPE
- ARRAY-TYPE `[` `]`

**NONNULL-TYPE** <i class="fa-solid fa-arrow-right"></i>
- PRIMITIVE-TYPE
- IDENTIFIER
- `(` TYPE `)`

**PRIMITIVE-TYPE** <i class="fa-solid fa-arrow-right"></i>
- `int`
- `bigint`
- `float`
- `bool`
- `str`
- `void`

A type followed by `?` is nullable. For example, `str?` is either a `str` value
or `nil`.

An array type is written by appending `[]` to the element type. For example,
`str[]` is an array of `str` values, and `str?[]` is an array of nullable `str`
values.

The `nil` value may only inhabit nullable types.
