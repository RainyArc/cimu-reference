# Dialogs

DIALOG <i class="fa-solid fa-arrow-right"></i> SINGLE-LINE-DIALOG | MULTI-LINE-DIALOG

SINGLE-LINE-DIALOG <i class="fa-solid fa-arrow-right"></i>
^ `#` CHARACTER? { ^ LF | EOF }+ { LF | EOF }

MULTI-LINE-DIALOG <i class="fa-solid fa-arrow-right"></i>
^ `##` CHARACTER? { ^ EOF }+ `##`

CHARACTER <i class="fa-solid fa-arrow-right"></i>
{ ^ LF | EOF | `:`}+ `:`
