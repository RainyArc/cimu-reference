# Types

A type classifies values and determines which operations may be applied to
those values.

Every value in Cimu has a type. The type of a value may be a primitive type, a
derived type such as a nullable or array type, or a named type introduced by a
declaration.

## Primitive Types

Primitive types are built into the language. Their names are predeclared type
names.

The primitive types are:

- `int`
- `bigint`
- `float`
- `bool`
- `char`
- `str`
- `void`

### int

The `int` type is a 32-bit signed integer type.

The range of `int` is from `-2147483648` to `2147483647`, inclusive.

`int` is intended for ordinary counters, indexes, flags, and small arithmetic
values used by gameplay and scene logic.

### bigint

The `bigint` type is an arbitrary-precision signed integer type.

A `bigint` value is not limited to a fixed number of bits. Its size is limited
by available memory.

`bigint` is intended for integer computations that must not be constrained by
the range of `int`.

### float

The `float` type is an IEEE 754 double-precision binary floating-point type.

`float` is intended for values such as time, position, opacity, volume, and
interpolation factors.

### bool

The `bool` type has two values: `true` and `false`.

Boolean literals are created with the `true` and `false` keywords.

Boolean values are produced by logical and comparison operations. Conditions in
`if`, `while`, `for`, and `switch`-related control flow use boolean values
where a condition is required.

#### Logical Not

The `!` operator computes logical negation.

| `b` | `!b` |
| --- | --- |
| `true` | `false` |
| `false` | `true` |

#### Logical Or

The `|` operator computes logical or on boolean operands.

| `a` | `b` | `a \| b` |
| --- | --- | --- |
| `true` | `true` | `true` |
| `true` | `false` | `true` |
| `false` | `true` | `true` |
| `false` | `false` | `false` |

The `||` operator has the same truth table as `|`, but evaluates its
right-hand operand only when the left-hand operand is `false`.

#### Logical And

The `&` operator computes logical and on boolean operands.

| `a` | `b` | `a & b` |
| --- | --- | --- |
| `true` | `true` | `true` |
| `true` | `false` | `false` |
| `false` | `true` | `false` |
| `false` | `false` | `false` |

The `&&` operator has the same truth table as `&`, but evaluates its
right-hand operand only when the left-hand operand is `true`.

#### Logical Xor

The `^` operator computes logical xor on boolean operands.

| `a` | `b` | `a ^ b` |
| --- | --- | --- |
| `true` | `true` | `false` |
| `true` | `false` | `true` |
| `false` | `true` | `true` |
| `false` | `false` | `false` |

#### Comparisons

Boolean values may be compared.

| `a` | `b` | `a == b` |
| --- | --- | --- |
| `true` | `true` | `true` |
| `true` | `false` | `false` |
| `false` | `true` | `false` |
| `false` | `false` | `true` |

| `a` | `b` | `a > b` |
| --- | --- | --- |
| `true` | `true` | `false` |
| `true` | `false` | `true` |
| `false` | `true` | `false` |
| `false` | `false` | `false` |

The remaining comparison operators are defined in terms of `==` and `>`.

- `a != b` is the same as `!(a == b)`.
- `a >= b` is the same as `(a == b) | (a > b)`.
- `a < b` is the same as `!(a >= b)`.
- `a <= b` is the same as `(a == b) | (a < b)`.

### char

The `char` type represents a Unicode scalar value.

A Unicode scalar value is any Unicode code point except surrogate code points.

Character literals have type `char`.

```cimu
'a'
'\n'
'\u3042'
```

The `char` type represents a single scalar value, not a user-perceived
grapheme cluster.

### str

The `str` type represents text.

String literals have type `str`.

Dialog text is source-level scene text. The scene system may attach spans and
annotations to dialog text before it is displayed, but the textual content is
represented as text.

### void

The `void` type represents the absence of a useful value.

Functions that do not return a useful value have `void` as their result type.
A value of type `void` is not used as ordinary data.

## Nullable Types

A nullable type is written by appending `?` to a type.

```cimu
str?
Result?
```

If `T` is a type, `T?` is a distinct type modeled as a built-in tagged union
with two cases:

- `Some`, which carries a value of type `T`
- `None`, which carries no data

The `nil` keyword constructs the `None` case of a nullable type.

The `??` operator evaluates to the value carried by `Some`, or to the fallback
expression on its right-hand side when the nullable value is `None`.

The `?.` operator performs optional access. If the receiver is `Some`, the
access is applied to the carried value and the result is wrapped as `Some`. If
the receiver is `None`, the result is `None`.

The postfix `!` operator forcefully unwraps a nullable value. It evaluates to
the value carried by `Some`, or raises a runtime error if the value is `None`.

```cimu
var name: str? = nil;
var display = name ?? "Unknown";
var length = name?.length;
var required_name = name!;
```

Nullable values may be matched with `switch`.

```cimu
var display = switch name {
    Some(value) => value,
    None => "Unknown",
};
```

## Array Types

An array type is written by appending `[]` to the element type.

```cimu
int[]
str?[]
Result[]
```

If `T` is a type, `T[]` is an array whose elements have type `T`.

Array types may be nested.

```cimu
int[][]
```

Nullable and array type suffixes compose according to the type syntax.

```cimu
str?[]  // array of nullable str values
str[]?  // nullable array of str values
```


## Struct Types

A struct type is a named product type with named fields.

Each field has a name and a type.

```cimu
struct Character {
    name: str,
    affection: int,
}
```

A value of a struct type contains one value for each field.

## Enum Types

An enum type is a named type with a fixed set of tags.

```cimu
enum Mood {
    Happy,
    Sad,
    Neutral,
}
```

An enum value is one of its tags. Enum tags do not carry data.

An enum value is constructed with a type-qualified tag.

```cimu
var mood = Mood.Happy;
```

Enum values may be matched by `switch`.

## Union Types

A union type is a named tagged union type tied to a tag enum.

Use a union when each tag needs to carry data.

```cimu
enum ResultTag {
    Ok,
    Err,
    None,
}

union Result(ResultTag) {
    Ok: str,
    Err: Error,
    None,
}
```

The type in parentheses is the tag enum. Each union case name should match a
variant of the tag enum.

At runtime, a union value has one active case. A case may carry a payload or no
data. When a case carries a payload, the active case determines which payload
type is valid.

Tagged union values are constructed with a type-qualified case. A case with a
payload takes one expression argument. A case without a payload takes no
argument.

```cimu
var ok = Result.Ok("done");
var err = Result.Err(error);
var none = Result.None;
```

Tagged union values may be matched by `switch`. A case pattern may bind the
payload of the active case.

```cimu
var message = switch result {
    Ok(value) => value,
    Err(error) => error.message,
};
```

## Interface Types

An interface type describes a set of required members.

```cimu
interface Speaker {
    fn speak(line: str): void;
}
```

The exact rules for implementing and satisfying interfaces are specified by the
interface semantics.

## Parenthesized Types

Parentheses may be used to group a type expression.

```cimu
(str)?
```

Parentheses do not create a distinct type by themselves.
