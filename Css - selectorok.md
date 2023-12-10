#egyetem 

`a {}` - tetszőleges HTML tag
`.osztaly {}` - tetszőleges HTML osztály
`#egyedi_azonosito` - HTML id alapján
`a[href] {}` - ha létezik az attribútum
`a href=[*|$|~]` ha:
- \*: Tartalmazza / egyenlő?
- $: azzal végződik, hogy:
- ~: tartalmazza azt, hogy

Szóközök nékül, teljes egyezés kell, egyébként pedig:
`nav > .main{}` - Tag alatt közvetlenül osztály
`nav .main{}` - Tagen belüli osztály (összes leszármazott)
`img ~ p {}` - Utána következő Testvér **elemek** (ugyanazon DOM szinten)
`img + p {}`  - Utána következő Testvér **elem**
