# Scene Grammar

**SCENE-BLOCK** <i class="fa-solid fa-arrow-right"></i>
- `{` SCENE-STATEMENT-LIST? `}`

**SCENE-STATEMENT-LIST** <i class="fa-solid fa-arrow-right"></i>
- SCENE-STATEMENT
- SCENE-STATEMENT-LIST SCENE-STATEMENT

**SCENE-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- STATEMENT
- TEXT-STATEMENT
- SAVE-POINT-STATEMENT
- LABEL-STATEMENT

A scene block is a superset of a regular block. It accepts regular statements
and expressions, including `if`, `switch`, `for`, and `while`, and it also
accepts scene-only statements.

Scene-only statements are valid only in the top-level scope of a scene. They
are not valid inside nested regular blocks.

## Text

**TEXT-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- DIALOG TEXT-ANNOTATION?

Text is story text emitted by a scene. A text statement starts with a leading
marker, either `#` or `##`. There must not be any non-whitespace character
between the start of the line and the leading marker.

For a single-line text statement, all characters after `#` until the end of the
line are treated as text, except the marker character `#`.

For a multi-line text statement, all characters after the leading `##` and
before the ending `##` are treated as text, except the marker character `#`.
The ending `##` must appear at the start of a new line.

Line breaks inside multi-line text are not preserved. Use `\n` to insert a line
break into the final text value.

Comments inside text are treated as ordinary text.

**TEXT-ANNOTATION** <i class="fa-solid fa-arrow-right"></i>
- `~~` TEXT-ANNOTATION-LIST

**TEXT-ANNOTATION-LIST** <i class="fa-solid fa-arrow-right"></i>
- TEXT-ANNOTATION-ITEM
- TEXT-ANNOTATION-LIST `;` TEXT-ANNOTATION-ITEM

**TEXT-ANNOTATION-ITEM** <i class="fa-solid fa-arrow-right"></i>
- TEXT-ANNOTATION-TARGET-LIST `:` TEXT-ANNOTATION-BODY

**TEXT-ANNOTATION-TARGET-LIST** <i class="fa-solid fa-arrow-right"></i>
- TEXT-ANNOTATION-TARGET
- TEXT-ANNOTATION-TARGET-LIST `,` TEXT-ANNOTATION-TARGET

**TEXT-ANNOTATION-TARGET** <i class="fa-solid fa-arrow-right"></i>
- IDENTIFIER
- `$` INTEGER-LITERAL

**TEXT-ANNOTATION-BODY** <i class="fa-solid fa-arrow-right"></i>
- `{` TEXT-ANNOTATION-ATTRIBUTE-LIST? `}`

**TEXT-ANNOTATION-ATTRIBUTE-LIST** <i class="fa-solid fa-arrow-right"></i>
- TEXT-ANNOTATION-ATTRIBUTE
- TEXT-ANNOTATION-ATTRIBUTE-LIST `,` TEXT-ANNOTATION-ATTRIBUTE

**TEXT-ANNOTATION-ATTRIBUTE** <i class="fa-solid fa-arrow-right"></i>
- IDENTIFIER `:` EXPRESSION

Example:

```cimu
#Narration before a branch.

if visited {
    var count = count + 1;
}

var line = switch mood {
    Happy => "Welcome back.",
    Sad => "Are you alright?",
    default => "Hello.",
};

#Narration text
#Alice:This is a line of dialog.
##Alice:This is a very long dialog line.
Continue writing on the next source line.
Use \n to insert a preserved line break.
##
#Alice#{red:This} is {colored} dialog.
~~ red: { color: "red" }; $1,$2: { color: "blue" };
```

## Save Points

**SAVE-POINT-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- `&`
- `&` IDENTIFIER

A save point is valid only in the top-level scope of a scene.

Example:

```cimu
&
&a_save_point
```

## Labels

**LABEL-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- `'` IDENTIFIER BLOCK-EXPRESSION

A label block may access variables declared in the label block and variables
declared in the containing scene. It may not access variables declared in other
labels.

Example:

```cimu
'label1 {
}
```
