# Lexical Structure

The lexer translates source text into a stream of tokens.

**TOKEN** <i class="fa-solid fa-arrow-right"></i>
- KEYWORD
- IDENTIFIER
- LITERAL
- PUNCTUATOR
- DIALOG
- COMMENT

Whitespace separates tokens but is otherwise ignored, except where it is part of
a dialog token.

Comments are normally ignored by the parser. Inside dialog text, comment
markers are treated as ordinary text.

Macro token blocks consume token trees instead of regular expressions or
statements. A macro may receive any token accepted by the lexer, with balanced
delimiters.
