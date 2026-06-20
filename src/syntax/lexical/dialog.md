# Dialogs

Dialog tokens are only recognized at the beginning of a line, after optional
horizontal whitespace. They are used by scene text statements.

**DIALOG** <i class="fa-solid fa-arrow-right"></i>
- SINGLE-LINE-DIALOG
- MULTI-LINE-DIALOG

**SINGLE-LINE-DIALOG** <i class="fa-solid fa-arrow-right"></i>
- LINE-START HORIZONTAL-WHITESPACE* `#` DIALOG-CHARACTER? DIALOG-TEXT? { LF | EOF }

**MULTI-LINE-DIALOG** <i class="fa-solid fa-arrow-right"></i>
- LINE-START HORIZONTAL-WHITESPACE* `##` DIALOG-CHARACTER? DIALOG-TEXT? LF MULTI-LINE-DIALOG-BODY LINE-START `##` HORIZONTAL-WHITESPACE* { LF | EOF }

**MULTI-LINE-DIALOG-BODY** <i class="fa-solid fa-arrow-right"></i>
- DIALOG-TEXT-LINE*

**DIALOG-TEXT-LINE** <i class="fa-solid fa-arrow-right"></i>
- DIALOG-TEXT LF

**DIALOG-TEXT** <i class="fa-solid fa-arrow-right"></i>
- { DIALOG-TEXT-CHAR | DIALOG-ESCAPE }*

**DIALOG-TEXT-CHAR** <i class="fa-solid fa-arrow-right"></i>
- ^{ LF | EOF | `\` }

**DIALOG-CHARACTER** <i class="fa-solid fa-arrow-right"></i>
- { DIALOG-CHARACTER-CHAR | `\:` }+ `:`

**DIALOG-CHARACTER-CHAR** <i class="fa-solid fa-arrow-right"></i>
- ^{ LF | EOF | `:` | `\` }

**DIALOG-ESCAPE** <i class="fa-solid fa-arrow-right"></i>
- `\:`
- `\n`

**TEXT-ANNOTATION-MARKER** <i class="fa-solid fa-arrow-right"></i>
- LINE-START HORIZONTAL-WHITESPACE* `~~`

**LINE-START**

The start of the file, or the position immediately after a line feed.

A dialog character name is only recognized on the first line of a dialog token,
immediately after the leading marker.

The leading `#` or `##` marker must not be preceded by any non-whitespace
character on the same line.

In a single-line dialog, all characters after the leading `#` until the end of
the line are dialog text.

In a multi-line dialog, all characters after the leading `##` and before the
ending `##` are dialog text. The ending `##` must appear at the start of a new
line.

Source line breaks inside a multi-line dialog are not preserved in the final
text value. Use `\n` in the dialog text to insert a preserved line break.

Use `\:` to insert a literal colon where a colon would otherwise be parsed as
the character-name separator.

Comment markers inside dialog text are treated as ordinary text.
