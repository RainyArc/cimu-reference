# Statements

**STATEMENT-LIST** <i class="fa-solid fa-arrow-right"></i>
- STATEMENT
- STATEMENT-LIST STATEMENT

**STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- EMPTY-STATEMENT
- EXPRESSION-STATEMENT
- DECLARATION-STATEMENT
- CONTROL-FLOW-STATEMENT
- BLOCK-EXPRESSION

**EMPTY-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- `;`

**EXPRESSION-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- EXPRESSION `;`
- IF-EXPRESSION
- SWITCH-EXPRESSION

**DECLARATION-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- VARIABLE-DECLARATION `;`

**CONTROL-FLOW-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- RETURN-STATEMENT
- BREAK-STATEMENT
- CONTINUE-STATEMENT
- GOTO-STATEMENT
- WHILE-STATEMENT
- FOR-STATEMENT

**RETURN-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- `return` EXPRESSION? `;`

**BREAK-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- `break` `;`

**CONTINUE-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- `continue` `;`

**GOTO-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- `goto` IDENTIFIER `;`

**WHILE-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- `while` EXPRESSION BLOCK-EXPRESSION

**FOR-STATEMENT** <i class="fa-solid fa-arrow-right"></i>
- `for` `(` FOR-INIT? `;` EXPRESSION? `;` EXPRESSION? `)` BLOCK-EXPRESSION

**FOR-INIT** <i class="fa-solid fa-arrow-right"></i>
- VARIABLE-DECLARATION
- EXPRESSION
