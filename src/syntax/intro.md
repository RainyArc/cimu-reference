# Syntax

This chapter uses a compact grammar notation to describe lexical and syntactic
rules.

## Notation

**PRODUCTION-NAME** <i class="fa-solid fa-arrow-right"></i>
- PRODUCTION-BODY

A production defines the possible forms of a grammar term.

## Literal Tokens

Text wrapped in backticks is matched literally.

```text
`if`
`+`
`{`
```

## Sequence and Choice

**SEQUENCE** <i class="fa-solid fa-arrow-right"></i>
- A B

`A B` means `A` followed by `B`.

**CHOICE** <i class="fa-solid fa-arrow-right"></i>
- A | B

`A | B` means either `A` or `B`.

**GROUP** <i class="fa-solid fa-arrow-right"></i>
- { A }

Braces without backticks group grammar terms. Backticked braces, such as `` `{`
`` and `` `}` ``, are literal tokens.

## Repetition

**OPTIONAL** <i class="fa-solid fa-arrow-right"></i>
- A?

`A?` means zero or one `A`.

**ZERO-OR-MORE** <i class="fa-solid fa-arrow-right"></i>
- A*

`A*` means zero or more `A`.

**ONE-OR-MORE** <i class="fa-solid fa-arrow-right"></i>
- A+

`A+` means one or more `A`.

**COUNTED-REPETITION** <i class="fa-solid fa-arrow-right"></i>
- A{m,n}

`A{m,n}` means at least `m` and at most `n` repetitions of `A`.

## Ranges

**RANGE** <i class="fa-solid fa-arrow-right"></i>
- `a`-`z`

A range matches any character from the first character through the second
character, inclusive.

## Exclusion

**EXCLUSION** <i class="fa-solid fa-arrow-right"></i>
- ^A
- ^{ A | B }

`^A` means any token or character except `A`.

`^{ A | B }` means any token or character except `A` and except `B`.

## Special Names

**EOF**

The end of the source file.
