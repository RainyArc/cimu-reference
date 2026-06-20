# Literals

**LITERAL** <i class="fa-solid fa-arrow-right"></i>

- INTEGER-LITERAL
- FLOATING-LITERAL
- STRING-LITERAL

## Integer
**INTEGER-LITERAL** <i class="fa-solid fa-arrow-right"></i>
DECIMAL-LITERAL | OCTAL-LITERAL | HEX-LITERAL

**DECIMAL-LITERAL** <i class="fa-solid fa-arrow-right"></i> 
DIGIT+

**OCTAL-LITERAL** <i class="fa-solid fa-arrow-right"></i> 
{ `0o` | `0O` } OCTAL-DIGIT+

**HEX-LITERAL** <i class="fa-solid fa-arrow-right"></i>
{ `0x` | `0X` } HEX-DIGIT+

## Floating
**FLOATING-LITERAL** <i class="fa-solid fa-arrow-right"></i> 
DECIMAL-FLOATING-LITERAL | HEX-FLOATING-LITERAL

**DECIMAL-FLOATING-LITERAL** <i class="fa-solid fa-arrow-right"></i>
FRACTION EXPONENT-PART? | DIGIT+ EXPONENT-PART

**FRACTION** <i class="fa-solid fa-arrow-right"></i>
DIGIT* `.` DIGIT+ | DIGIT+ `.`

**EXPONENT-PART** <i class="fa-solid fa-arrow-right"></i>
{ `e` | `E` } SIGN? DIGIT+

**HEX-FLOATING-LITERAL** <i class="fa-solid fa-arrow-right"></i>
{ `0x` | `0X` } HEX-FRACTION 
BINARY-EXPONENT-PART? | { `0x` | `0X` } HEX-DIGIT+ BINARY-EXPONENT-PART

**HEX-FRACTION** <i class="fa-solid fa-arrow-right"></i>
HEX-DIGIT* `.` HEX-DIGIT+ | HEX-DIGIT+ `.`

**BINARY-EXPONENT-PART** <i class="fa-solid fa-arrow-right"></i>
{ `p` | `P` } SIGN? HEX-DIGIT+

## String
**STRING-LITERAL** <i class="fa-solid fa-arrow-right"></i>
`"` { ^{ `"` | `\` } | ASCII-ESCAPE | UNICODE-ESCAPE | QUOTE-ESCAPE | STRING-CONTINUE }* `"`

**STRING-CONTINUE** <i class="fa-solid fa-arrow-right"></i> `\` CR? LF

**QUOTE-ESCAPE** <i class="fa-solid fa-arrow-right"></i> `\"`

**ASCII-ESCAPE** <i class="fa-solid fa-arrow-right"></i> `\x` HEX-DIGIT HEX-DIGIT | `\n` | `\r` | `\t` | `\\` | `\0`

**UNICODE-ESCAPE** <i class="fa-solid fa-arrow-right"></i>
`\u` HEX-DIGIT{1,6}
## Digit

**DIGIT** <i class="fa-solid fa-arrow-right"></i> 
`0`-`9`

**OCTAL-DIGIT** <i class="fa-solid fa-arrow-right"></i>
`0`-`7`

**HEX-DIGIT** <i class="fa-solid fa-arrow-right"></i>
`0`-`9` | `a` - `f` | `A` - `F`

**SIGN** <i class="fa-solid fa-arrow-right"></i>
`-` | `+`