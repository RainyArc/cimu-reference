# Declarations

**ITEM** <i class="fa-solid fa-arrow-right"></i>
- FUNCTION-ITEM
- SCENE-ITEM
- STRUCT-ITEM
- ENUM-ITEM
- UNION-ITEM
- INTERFACE-ITEM
- IMPORT-ITEM

**PARAMETER-LIST** <i class="fa-solid fa-arrow-right"></i>
- PARAMETER
- PARAMETER-LIST `,` PARAMETER

**PARAMETER** <i class="fa-solid fa-arrow-right"></i>
- IDENTIFIER `:` TYPE

**FUNCTION-ITEM** <i class="fa-solid fa-arrow-right"></i>
- `fn` IDENTIFIER `(` PARAMETER-LIST? `)` RETURN-TYPE? BLOCK-EXPRESSION
- `async` `fn` IDENTIFIER `(` PARAMETER-LIST? `)` RETURN-TYPE? BLOCK-EXPRESSION

**RETURN-TYPE** <i class="fa-solid fa-arrow-right"></i>
- `:` TYPE

**SCENE-ITEM** <i class="fa-solid fa-arrow-right"></i>
- `scene` IDENTIFIER `(` PARAMETER-LIST? `)` SCENE-BLOCK

**STRUCT-ITEM** <i class="fa-solid fa-arrow-right"></i>
- `struct` IDENTIFIER `{` FIELD-LIST? `}`

**FIELD-LIST** <i class="fa-solid fa-arrow-right"></i>
- FIELD
- FIELD-LIST `,` FIELD

**FIELD** <i class="fa-solid fa-arrow-right"></i>
- IDENTIFIER `:` TYPE

**ENUM-ITEM** <i class="fa-solid fa-arrow-right"></i>
- `enum` IDENTIFIER `{` ENUM-VARIANT-LIST? `}`

**ENUM-VARIANT-LIST** <i class="fa-solid fa-arrow-right"></i>
- ENUM-VARIANT
- ENUM-VARIANT-LIST `,` ENUM-VARIANT

**ENUM-VARIANT** <i class="fa-solid fa-arrow-right"></i>
- IDENTIFIER

**UNION-ITEM** <i class="fa-solid fa-arrow-right"></i>
- `union` IDENTIFIER `(` TYPE `)` `{` UNION-CASE-LIST? `}`

**UNION-CASE-LIST** <i class="fa-solid fa-arrow-right"></i>
- UNION-CASE
- UNION-CASE-LIST `,` UNION-CASE

**UNION-CASE** <i class="fa-solid fa-arrow-right"></i>
- IDENTIFIER
- IDENTIFIER `:` TYPE

The type in parentheses is the tag enum of the union. Each union case name
should match a variant of the tag enum. A union case may omit its payload type.

Example:

```cimu
enum ResultTag {
    Ok,
    Err,
}

union Result(ResultTag) {
    Ok: str,
    Err: Error,
}
```

**INTERFACE-ITEM** <i class="fa-solid fa-arrow-right"></i>
- `interface` IDENTIFIER `{` INTERFACE-MEMBER-LIST? `}`

**INTERFACE-MEMBER-LIST** <i class="fa-solid fa-arrow-right"></i>
- INTERFACE-MEMBER
- INTERFACE-MEMBER-LIST INTERFACE-MEMBER

**INTERFACE-MEMBER** <i class="fa-solid fa-arrow-right"></i>
- `fn` IDENTIFIER `(` PARAMETER-LIST? `)` RETURN-TYPE? `;`

**IMPORT-ITEM** <i class="fa-solid fa-arrow-right"></i>
- `import` IMPORT-TREE `;`

**IMPORT-TREE** <i class="fa-solid fa-arrow-right"></i>
- IMPORT-PATH IMPORT-ALIAS?
- IMPORT-PATH `.` `{` IMPORT-SPECIFIER-LIST? `}`

**IMPORT-PATH** <i class="fa-solid fa-arrow-right"></i>
- IDENTIFIER
- IMPORT-PATH `.` IDENTIFIER

**IMPORT-SPECIFIER-LIST** <i class="fa-solid fa-arrow-right"></i>
- IMPORT-SPECIFIER
- IMPORT-SPECIFIER-LIST `,` IMPORT-SPECIFIER

**IMPORT-SPECIFIER** <i class="fa-solid fa-arrow-right"></i>
- IDENTIFIER IMPORT-ALIAS?

**IMPORT-ALIAS** <i class="fa-solid fa-arrow-right"></i>
- `as` IDENTIFIER

Examples:

```cimu
import std.dialog;
import std.dialog as dialog;
import std.{scene, audio};
import std.{scene as sc, audio};
```

**VARIABLE-DECLARATION** <i class="fa-solid fa-arrow-right"></i>
- `var` IDENTIFIER TYPE-ANNOTATION? `=` EXPRESSION
- `const` IDENTIFIER TYPE-ANNOTATION? `=` EXPRESSION

**TYPE-ANNOTATION** <i class="fa-solid fa-arrow-right"></i>
- `:` TYPE
