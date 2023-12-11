## Flexbox
A **flexbox** teljesebb kontrollt ad egy konténer gyerekei felett, *reszponzív* módon
- Elemek igazítása egymáshoz és a konténer széleihez
- Elemek automatikus méretezése arányosan
- Elemek sorrendjének variálása
![[flexbox-layout.png]]
#### Tulajdonságok a konténeren
`display: flex`: Az elemeket befoglaló konténeren meg kell adni, hogy flexbox elrendezést használjon.
`flex-direction`: Gyerekek elrendezése
	- `row`: vízszintesen
	- `column`: függőleges tengely mentén
`flex-wrap:` sor/oszloptörés engedélyezése
`justify-content`: Elemek **elrendezés**e, tagolása a főtengely (*main axis*) mentén
	- A gyerekek közt megmaradt helyet osztja be.
![[flex-irányok.png|500]]
`align-items`: Gyerekek igazítása a **főtengelyre merőlegesen**
- [!] Hasonlít a `justify-content`-re, de fontos különbség, hogy <mark style="background: #FFF3A3A6;">nem a gyerekek közt megmaradt helyet osztja be, hanem a gyerekek és a flexbox széle közötti helyet!</mark>
	- Tehát ez akkor is működik, ha valamelyik gyerek „nyúlós” (mivel az a főtengely mentén nyúlik).
	- A gyerekek a kereszttengelyen is nyújthatók, erre van a `stretch` opció
	- Például ha 3 különböző magassábú flex konténerünk van, akkor az `align-items: center;` a kereszttengely mentén középre rendezi őket.
`align-content`: *Több sornyi flexbox elemek sorainak* igazítása a kereszttengely mentén.
	- Egyetlen sornyi flexbox elemre nincs hatásra.
	- Értékei kb. ugyanazok és kb. ugyanazt jelentik, mint a `justify-content` esetén, azonban itt van külön `stretch` érték is (ami a default), itt a gyerekektől függ a „nyúlás”.

- [i] `align-items` és `justify-content`: egyes elemekre vonatkoznak.
- [i] `align-content`: Több sornyi elemre vonatkozik, a kereszttengely mentén 
#### Tulajdonságok a konkrét flex elemeken
`flex-grow`: szabályozza, hogy az elem nyúljon-e, ha marad hely a főtengelyen
`flex-shrink`: összenyomható-e az elem, ha kevés a hely, és nem lehet sort törni.
`flex-basis`: az elem alapértelmezett mérete, nyújtás/összenyomás előtt
	- alapból ez is `auto`, ami a gyerek főtengely menti méretét veszi fel
	- Megadhatunk konkrét értéket is, ekkor *felülírjuk a főtengely menti méretet.*
`flex`: shorthand az előző háromra
	`flex: 1 1 auto`: rugalmas
	`flex: 0 0 auto`: rugalmatlan
`align-self`: az ekem felülírhatja saját magára a konténerek beállított `align-items` értéket.
`order`: Az elem alapvetően a HTML-ben definiált sorrendben jelenik meg. De ezzel variálhatunk rajta. **Negatív szám is lehet, alapértelmezetten 0.**

- [!] Nem alkalmazható az egyes flexbox elemekre a: `float, clear, vertical-align`
<div style="page-break-after: always;"></div>
## Bootstrap
- [p] Könnyen tanulható és használható a részletes dokumentáció miatt.
- [p] Kiváló grid rendszer a reszponzív layout kialakításához.
- [p] Nem kell mindent nulláról megírni, csomó kész stílussal érkezik.
- [p] Rengeteg időt meg lehet vele takarítani.
- [p] Számos shortcut osztályt tartalmaz (pl. `success`, `warning`, passzoló színekkel és ikonokkal)
- [p] Sok segítséget ad az űrlapok és táblázatok formázásához.
- [i] Kiindulási alapnak használjuk
### Bootstrap Grid
**mobile first tervezés:** mobilra mondjuk meg az elrendezést, majd ezt a képernyő növekedésével fokozatosan felülbírálhatjuk.
- Sorokra és oszlopokra bontja a képernyőt
	- Minden sor **12** azonos méretű oszlopból áll
	- A sorok száma, mérete tetszőleges.
	- Egy konkrét tartalmi elem több oszlopon is átnyúlhat
	- A sorok magasságát jellemzően a legmagasabb konkrét cellája határozza meg.
##### Használata
A grid gyökere a `container` vagy `container-fluid` osztály
- Ebbe pedig `row` oszállyal ellátott konténereket teszünk, amikbe kizárólag `col-*` osztályú elemek kerülnek.

> [!NOTE] A col-* osztályok viselkedése
> 
> Egy prefixszel megadhatjuk, melyik töréspont **fölött** alkalmazza
> 	- pl: `col-sm-*` a tableteken és desktopokon érvényesül, de mobilon nem
> 	<mark style="background: #FFF3A3A6;">A specifikusabb osztály felülírja a kevésbé specifikusat!</mark>
> 		- `xs >> sm >> md >> lg >> xl >> xxl`
> - `*`: megadja, hogy hány oszlopot foglaljon el a cella, Alapértelmezetten: *12*
> -  A reszponzív oszlopszélességekhez a különböző töréspontokra vonatkozó oszlop szélességeket egyszerre kell megadni. Vagyis egy-egy elemnek több class-t kell megadni. *pl egyszerre* `.col-md-4` és `.col-6`
> 	- A `col-{méret}` **minden felbontásra vonatkozik**, hiszen ez a legkisebb.
> 	- A `col-md-{méret}` viszont **csak 768 px felett.**

A Bootstrap 4-től a `col`-t imegában s használhatjuk mint lehetséges oszlop szélességet.
-  Ha nem adjuk meg a töréspontot, akkor ebben az esetben az adott oszlop <mark style="background: #CACFD9A6;">mérete automatikusan kerül meghatározásra.</mark>


`col-{méret}-auto`: Lehetőség nyílik változó szélességű oszlopok definiálására is.
	- <mark style="background: #BBFABBA6;">A tartalom mérete határozza meg</mark> az oszlop szélességét.
- [!] Egy cellán belül vehetünk fel új `row`-t amit a `col`-ok segítségével további cellákra oszthatunk.
 `.row-cols-{sm}-*` osztály segítségével gyorsan <mark style="background: #BBFABBA6;">megadhatjuk, hogy mennyi oszlopot szeretnénk használni</mark>
	 - A gyerekekre így már csak a `.col` osztályt kell rátennünk!
- [i]  ez csak egy egyszerűsített megadása a `.col-*` osztályoknak, amik rákerülnek az egyes oszlopokra.
	 - A `.row-cols-auto` is használható.

#### Bootstrap osztályok flexboxos elrendezésez
| Bootstrap                     | Pure CSS                                      |
| ----------------------------- | --------------------------------------------- |
| .d-{sm}-flex                  | { display: flex }                             |
| .flex-{sm}-column             | { flex-direction: flex-column }               |
| .justify-content-{sm}-between | { justify-content: space-between }            |
| .align-items-{sm}-center      | { align-items: center }                       |
| .align-self-{sm}-center       | { align-self: center }                        |
| .flex-{sm}-grow-1             | { flex-grow: 1}                               |
| .flex-wrap                    | sortörés engedélyezése                        |
| .m{se}-auto                   | jobbra / balra igazítás automatikus margóval. |
| .m{t\|b\|l\|r}-{0-9}          | *felső/alső/bal/jobb* margó                   |
| .p{t\|b\|l\|r}-{0-9}                              |    *felső/alső/bal/jobb* padding                                            |

- [b] Az oszlopoka**t függőlegesen is tudjuk igazítani** az alábbi bootstrap classokkal
	- `align-self-start, align-self-center, align-self-end`
- [b] A teljes sorokat is lehet függőlegesen igazítani, `align-items`-el
#### HTML elemek reszponzív megjelenítése / elrejtése
`d-{value}` mérettől függően mindig elrejti/megjeleníti
`d-{breakpoint}-{value}`: adott képernyő méreten elrejti/megjeleníti
`{value}` : a lehetséges display értékek: `non, inline, inline-block, block, flex, ...`


- [?] Annyira sok formázást tartalmaz a bootstrap, hogy az összes osztályt nem lehet felsorolni. De van hozzá jó dokumentáció: https://getbootstrap.com/docs/5.2/getting-started/introduction/

Cheat sheet: https://getbootstrap.com/docs/5.0/examples/cheatsheet/
<div style="page-break-after: always;"></div>

## SCSS
A **SASS** egy CSS preprocesszor. Új funkciókkal bővíti és egyszerűsíti az életünket:
- változók
- szabályok egymásba ágyazása
- mixinek
- függvények és operátorok

A végén az elkészített fájlból CSS-t állítunk elő, így a böngészőhöz ugyanúgy CSS jut el, *csak hatékonyabban tudjuk elkészíteni*.

A SASS preprocesszornak kétféle szintaxisa van: SASS és SCSS. A tárgy csak az SCSS-el foglalkozik.

#### Változók
- Értékek újrahasznosítása, úgy, hogy csak egy helyen kelljen megadni.
- Szintén van scope-juk.
- [p] Átláthatóbb kód
- [p] Könnyebb karbantartani, mert csak egyetlen helyen kell lecserélni. 

```scss
$page-min-width: 1200px;
$page-min-height: 800px;

html {
	min-width: $page-min-width;
	min-height: $page-min-height;
	height: 100%;
}
```
*példa változók használatára*

```scss
$text-color: blue; // globális változó

.error {
	$text-color: red; // lokális változó
	color: $text-color;
}

.normal-text {
	color: $text-color;
}
```
 *változók lokalitása*

```scss
$text-color: blue;
.error {
	$text-color: red;
	color: $text-color;
	$text-color: green !global;
}

.normal-text {
	color: $text-color; //zöld lesz
}
```
*!global flag.*. Ilyenkor a névütközés esetén a külső, globális változóra hivatkozik az SCSS.
#### Mixinek
A mixinekkel egy **osztályba szervezzünk több tulajdonság beállítását**, **amit később egy sorban újra hasznosítunk**, akár úgy is, hogy *bemenő paraméter*t kap.
Hasznos lehet a vendor prefixek miatti többféle szabálybeállításnál.

```scss
@mixin square($size, $color) {
	width: $size;
	height: $size;
	background-color: $color;
}

.small-blue-square {
	@include square(20px, rgb(0,0,255));
}

.big-red-square {
	@include square(300px, rgb(255,0,0));
}
```
*mixinek*. Újra felhasználunk egy kódrészletet.

#### Függvények
```scss
@function column-width($col, $total:8) {
	@return percentage($col/$total);
}

.col-3 {
	width: column-width($total: 8, $col: 3); // 37.5%
}
```
*Függvények* létrehozásánál az egyes paramétereknek alapértelmezettértéket is adhatunk. Ha több paramétere van egy függvénynek, akkor <mark style="background: #CACFD9A6;">a nevesített paraméterekkel átláthatóbb kódot készíthetünk és a paraméter sorrendet sem kell betartani.</mark>

Szabályokat generálhatunk **ciklusok** segítségével is:
```scss
@for $i from 1 through $total {
	.col-#{$i} { width: column-width($i) };
}
```

#### Mixin vagy függvény?
**A Mixin kimenete közvetlenül CSS-re fordítható. Tulajdonság érték párokat kapunk vissza.** A függvények viszont egy konkrét értéket adnak vissza, amit egy CSS tulajdonsághoz kell rendelni.
Vagyis **akkor használjunk függvényt, ha csak számításokat szeretnénk végrehajtani.**
#### Egymásba ágyazás:
Sokkal átláthatóbban fogalmazhatjuk meg az összetett CSS szabályokat, ha azokat egymásba ágyazzuk:
```scss
ul {
list-style: none;
	li {
		padding: 15px;
		display: inline-block;
		a {
			text-decoration: none;
			font-size: 16px;
			color: #444;
		}
	}
}
```
##### Parent selector (&):
 A *&* lehetőséget ad összetettebb szabályok definiálására is, a gyerekből meaghatunk a szülőre vonatkozó szabályokat is. (hasznos pl. hover esetén)
#### Extend
SCSS-ben az **extend** segítségével tudjuk megoldani azt, hogy a *több szabályban is használt részleteket egy helyre szervezzük ki és később azt az új szabályokban csak kiegészítsük.*


> [!NOTE] Extend vs. Mixin
>Fontos különbség a mixinhez képest, hogy itt <mark style="background: #FFB86CA6;">az extend ezeket a szabályokat egyetlen css blokkba generálja</mark>. 
> - *Pl.* ha a `.message` és a `.success`-be is betettük az extend-et, akkor az egy `.messgae, .success {` fejlécű blokkot tesz a css-be, míg a mixin belegnerálja külön mindkettőnek a blokkjába az értékeket.
#### Importálás
Nagy méretű SCSS esetén átláthatóbbá tehetjük a kódot, ha azokat külön fájlokba szervezzük. Importálásra használjuk az **@import** kulcsszót.
