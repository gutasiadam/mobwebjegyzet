A **jQuery** egy gyors, kicsi és funkciógazdag JavaScript könyvtár, amivel egyszerű:

- a HTML dokumentum manipulálása,
- a kliens oldali <mark style="background: #FFF3A3A6;">eseménykezelők</mark> készítése,
-  az animáció,
-  és az aszinkron kommunikáció a szerverrel (AJAX kérések)
- **böngészőfüggetlen**
- **könnyű kiterjeszthetőség, számos jQuery pluginnel**
A jQuery egyik legfontosabb eseménye a `document ready` esemény.
- Akkor fut le, amikor a document **letöltődött**
- [!] Az előtt mielőtt a képeket és külső hivatkozásokat elkezdené tölteni a böngésző. 

### Selectorok
`$("*")` - Minden elem
`$("#staff")` - A staf ID-jú elem. Amit először talál meg, ha több ugyanolyan ID-jű lenne.
`$(".meta")` - Adott osztállyal rendelkező elemek
`$("img")` - Adott tag

Ezután használhatóak összetett (akár hierarchikus) selectorok is, mint CSS-ben.
### Form Validáció
Ha a beépített szabályok nem megfelelőek, készíthetünk egyedi szabályt.
jQuery validate-et pont erre találták ki.
	– Szabályok JavaScriptben megadhatók.
	– Egyedi hibaüzenetet adhatunk meg.
	– Kliens oldalon validál, nem küldi el a szerverre ha hibás.
```js
$(document).ready(function() {
	$("#registrationForm").validate({
		rules: {
			firstName: "required",
		}
		messages: {
			firstName: "Kötelező megadni"
		}
	}
});
```
További lehetséges validate elemek:

`errorClass` és `validClass`
	-  Milyen CSS osztály vonatkozzon a helyes és az érvénytelen adatokra.
`highlight()` és `unhighlight()` függvények
	- Függvény amivel testreszabhatjuk a validációs szabályok kiértékelése utáni megjelenítést.
`setDefault`
	- Alapértelmezett működést tudjuk vele átállítani.
## $.ajax({…})
A szinkron kommunikáció előnytelen számunka, nem a legjobb a felhasználói élmény, mert villan, ugrál, stb...

Megoldás: **aszinkron kommunikáció**
- [p] Jobb felhasználói élmény
- [p] Gyorsabb
- [p] Nincs felhasználói felület blokkolás
- [p] Nem frissül a teljes oldal
- [p] Megmarad a munkaállapot
- [p] Kevesebb adat a hálózaton
- [p] Kevesebb szerveroldali feldolgozás

Vannak azért hátrányai is:
- [c] A böngésző history funkciók támogatása nehézkes
- [c] Forgalomszámlálás, méretezés, tesztelés nehéz
- [c] Felhasználói szokások változnak, új dizájn elvárások.
- [c] Komplex fejlesztői feladat 

Négy technológia szükséges a működéséhez:

-  *XMLHttpRequest (XHR)*
	- Lényegében egy mini-böngésző, aszinkron végrehajtással. A választ a callback függvényben lehet feldolgozni
- *JavaScript*
-  *DHTML + DOM*
	- DOM + JS + CSS
	- A szervertől érkező válasz alapján a felhasználói felület frissítésére
- *XML vagy JSON*
	- Átküldött adatstruktúra sorosítására alkalmas
	- Az XML redundáns, nehézkes
	- [n] A JSON viszont egyszerű adatcserére született, sorosítás jól támogatott.

jQuery függvények:
`$.ajax`: Ez mindent tud, csak sok a paramétere
`$.load, $.get, $.post, $.script, $.json`

XMLHttpRequest példa:
```js
// A kérés elküldése

var xhr = new XMLHttpRequest()
xhr.open( "GET", strUrl, true ); // true = aszinkron
xhr.onreadystatechange = onStateChanged;
xhr.send( null );

// A válasz feldolgozása
function onStateChanged() {
	if( xhr.readyState == 4 ) { // READYSTATE_COMPLETE
		if( xhr.status == 200 ) { // HTTP_OK
		// Az xhr.responseText tulajdonság feldolgozása.
		}
	else {
		alert( "Hiba történt, a hibakód: " + xhr.status ); }
	}
}
```

AJAX példa:
```js
$("button").click(function(){  
  $.ajax({url: "demo_test.txt", success: function(result){  
    $("#div1").html(result);  
  }});  
});
```
**Same-origin policy**: Csak oda lehet visszaívni, ahonnan az oldal letöltődött!

A `Fetch API` viszont **CORS**-kompatibilis: [[WEB04-Javascript (alapok+haladó)#Fetch API]]

##### CORS:
**Cross-Origin Resource Sharing**
Tartozik hozzá egy `Preflight` request, amivel elkéri a kliens a szervertől az `Access-Control`-hoz tartozó header-eket. A szerver megmondja, mit tehet a kliens. Ehhez süti alapból nem megy át.

A kliens Az *Origin* mezőben elküldi a kérő oldal címét.

> [!example] Same-origin policy kivételek
> **Egyes HTML elemekre nem vonatkozik a same-origin policy**, mint például az `img, script, link, iframe`
##### Nehézségek:
- [?] Átirányítás a válaszban:
	- A kliensnek követnie kell.
- [?] Lejár a cookie.
	-  Lejár a session cookie → megszűnik a session a szerveren, de nem tudja értesíteni a klienst.
	- Lejárt az authentication cookie → átirányítás a bejelentkezés oldalra, ami HTML választ küld.
- [?] Szerveroldali hiba
	-  pl. kezeletlen kivétel, 5xx szerver oldali hiba, túl nagy méretű kérés, timeout.
	- Szerver oldali általános hibakezelő átirányít egy HTML hibaoldalra.
	- Érvénytelen XML vagy JSON tartalom, a kliens nem tudja feldolgozni.
- <mark style="background: #BBFABBA6;">A sok kérés együtt nagy forgalmat generálhat.</mark>

## Websocket
Adott intervallumonként pollozhatunk a szervertől ajax-al, de nem azonnal jelennek meg az adatok, és sok a felesleges kommunikáció. 
Megoldás lehet a **Long-polling**, ahol a kline sdirekt sokáig nyitva tartja a kapcsolatot. Ha van változás, akkor vissza tudja küldeni a szerver.
- [p] Egyszerű megvalósítás
- [p] Működik minden böngészőben
- [p] Azonnal értesül a kliens
- [c] Bonyolultabb szerveroldali implementáció
- [c] Jobban terheli a szerveroldalt, mert foglalni kell a kapcsolathoz tartozó erőforrásokat. 
Megoldás: **websocket**

**Full-duplex, kétirányú TCP kommunikáció egyetlen socketen keresztül.**
- HTTP-től független TCP kommunikáció.
- ws:// és wss:// URI séma.
- A kliens egy `Connection:Upgrade` fejléccel kéri a protokoll váltást (handshake).
- Bármilyen alkalmazásban használható.
- 80 és 443 portokat használ, nincs tűzfal probléma.
- Nem bájt, hanem üzenetfolyam
- [p] Nincsenek HTTP fejlécekkel járó overheadek, gyorsabb
- [c]  A szabvány sok változáson ment keresztül, az RFC-nek megfelelőt csak azújabb böngészők támogatják.
- [c] Régi webszerverek nem támogatják

```js 
//Használat példa
var socket = new WebSocket('ws://localhost:8080/');
socket.onopen = function () {
	console.log('Connected!');
};

socket.onmessage = function (event) {
	console.log('Received data: ' + event.data);
	socket.close();
};

socket.onclose = function () {
	console.log('Lost connection!');
};

socket.onerror = function () {
	console.log('Error!');
};

socket.send('hello, world!');
```



