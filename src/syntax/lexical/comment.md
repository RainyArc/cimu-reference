# Comments

**COMMENT** <i class="fa-solid fa-arrow-right"></i> SINGLE-LINE-COMMENT | MULTI-LINE-COMMENT

**SINGLE-LINE-COMMENT** <i class="fa-solid fa-arrow-right"></i>
`//` { ^ EOF | LF }* { EOF | LF }

**MULTI-LINE-COMMENT** <i class="fa-solid fa-arrow-right"></i>
`/*` { ^ `*/` }* `*/`