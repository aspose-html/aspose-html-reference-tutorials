---
category: general
date: 2026-03-26
description: Top‑level await példa, amely élő demóban mutatja be az await delay JavaScriptet,
  a számláló növelő osztályt és a nyilvános osztálymezőket JavaScriptben.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: hu
og_description: Felső szintű await példa, amely bemutatja az await delay JavaScript-et,
  a számláló növelő osztályt és a nyilvános osztálymezőket JavaScriptben egy tömör
  útmutatóban.
og_title: Felső szintű await példa – Await késleltetés használata JavaScriptben
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: top level await példa – Await késleltetés használata JavaScriptben
url: /hu/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# top level await példa – await delay használata JavaScriptben

Gondolkodtál már azon, hogyan lehet megállítani egy modul végrehajtását anélkül, hogy mindent egy async IIFE‑be csomagolnál? Erre pontosan a **top level await példa** szolgál. Ebben az útmutatóban egy apró weboldalon keresztül mutatjuk be, hogyan használjuk az `await delay javascript`‑et a munka elhalasztásához, majd hogyan hozunk létre egy `increment counter class`‑t, amely a **public class fields javascript**‑et használja. A végére egy teljes, másol‑és‑beilleszthető kódrészletet kapsz, amely bármely modern böngészőben fut.

Mindent lefedünk, a nyilvános mezővel rendelkező osztály definiálásától a egyszerű promise‑alapú késleltető segédfüggvény összekötéséig. Nincs külső könyvtár, nincs build lépés – csak tiszta HTML, egy `<script type="module">`, és a legújabb ECMAScript funkciók. Ha már jártas vagy az async függvényekben, látni fogod, miért érződik természetes kiterjesztésnek a top‑level await. Ha újonc vagy a **javascript class public field** szintaxisban, ne aggódj – minden sor mögötti okot elmagyarázzuk.

## Mit fogsz megtanulni

- Hogyan működik egy **top level await példa** egy modul‑scriptben.
- Az `await delay javascript` segédfüggvény mintája, amely a `setTimeout`‑ot utánzva promise‑ot ad vissza.
- Hogyan írj egy **increment counter class**‑t, amely nyilvános mezőt (`count`) és egy statikus inicializációs blokkot használ.
- Várható konzolkimenet és hogyan ellenőrizheted, hogy a statikus blokk a script többi része előtt lefut.
- Tippek a gyakori buktatók hibaelhárításához, például régebbi böngészők, amelyek nem támogatják a top‑level await‑ot.

> **Pro tipp:** A modern böngészők (Chrome 106+, Firefox 102+, Edge 106+) már támogatják a top‑level await‑ot. Ha régebbi környezetet kell támogatnod, fontold meg a Vite vagy Babel‑hez hasonló eszközök használatát a bundlinghoz.

## 1. lépés – Osztály definiálása nyilvános mezővel és statikus blokkal

A demónk első része egy olyan osztály, amely egy numerikus számlálót tárol. Vedd észre a `count = 0;` sort – ez a **public class fields javascript** szintaxis, amely az ES2022‑ben jelent meg. Konstruktor nélkül hoz létre egy példány tulajdonságot.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**Miért statikus blokk?** Lehetővé teszi, hogy egyszeri inicializációs logikát (például naplózást) futtassunk a modul értelmezésekor, *mielőtt* bármilyen top‑level await lefutna. Így garantáljuk, hogy az üzenet elsőként jelenik meg a konzolon, bizonyítva, hogy az osztály korán kiértékelődött.

## 2. lépés – `await delay javascript` segédfüggvény létrehozása

Ezután egy apró promise‑alapú késleltető függvényre van szükség. Lényegében a `setTimeout` köré csomagol, de a visszaadott promise‑nak köszönhetően await‑olható.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Szélsőséges eset:** Ha az `ms` negatív vagy nem szám, a `setTimeout` `0`‑ként kezeli. Hozzáadhatsz validációt, de egy demóhoz a egy soros változat olvashatóbb.

## 3. lépés – Top‑Level Await használata a végrehajtás szüneteltetéséhez

Most jön a főszereplő: a top‑level await. Mivel a scriptünk modul (`type="module"`), közvetlenül a felső szinten helyezhetünk `await`‑ot. Ez addig szünetelteti a modult, amíg a promise feloldódik, így irányíthatjuk a mellékhatások sorrendjét.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Gyakori kérdés:** „Használhatok‑e top‑level await‑ot egy normál `<script>` tagben?” Nem – csak modul‑scriptben működik. Ha elfelejted a `type="module"` attribútumot, szintaxis hibát kapsz.

## 4. lépés – Az osztály példányosítása, növelés és az eredmény naplózása

Végül mindent összerakunk: létrehozzuk a példányt, meghívjuk az `increment()`‑t, és kiírjuk a végső számlálót. Ez mutatja be a **increment counter class** működését.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Várható konzolkimenet

```
Counter class initialized
Final count: 1
```

Ha a DevTools‑ban nyitod meg az oldalt, a statikus‑blokk üzenetnek **előbb** kell megjelennie, mint a késleltetés befejeződik, ezzel bizonyítva, hogy az osztály előbb lett kiértékelve.

## 5. lépés – Miért használjunk nyilvános osztálymezőket a konstruktor helyett?

Lehet, hogy azt kérdezed, miért nem írtuk így:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Mindkét megközelítés működik, de a **public class fields javascript** tisztább, deklaratívabb szintaxist biztosít. A mező egyszer definiálódik, nem minden konstruktorhívásnál, ami olvashatóbbá teszi a kódot, ha az osztály nagyobb lesz. Emellett a statikus blokkok nem helyezhetők konstruktorba, így az inicializációs logika szétválasztása természetesebb.

## 6. lépés – A példa adaptálása valós alkalmazásokhoz

Éles környezetben gyakran több számlálóra lesz szükség. Néhány gyors ötlet:

- **Több számláló:** Tárold őket egy `Map`‑ben, amelynek kulcsa egy azonosító.
- **Állandó állapot:** Cseréld le a `console.log`‑ot `localStorage` írásokra.
- **Aszinkron inicializáció:** Használd a statikus blokkot konfiguráció lekérésére a szerverről, mielőtt bármely példány létrejönne.

Ezek a minták továbbra is profitálnak a top‑level await‑ból, mivel egyszer le tudod kérni az adatot a modul betöltésekor, és garantálhatod, hogy minden fogyasztó számára készen áll.

## Gyakran Ismételt Kérdések

**Q: Blokkolja a top‑level await a többi modult?**  
A: Nem. Minden modul önállóan fut. Csak az a modul, amelyik await‑ot tartalmaz, szünetel; a többi modul továbbra is párhuzamosan töltődik.

**Q: Mi van, ha a késleltető promise elutasítódik?**  
A: A nem kezelt elutasítás megszakítja a modul kiértékelését, és hibaként jelenik meg a konzolon. Ha elegáns visszaesést szeretnél, csomagold az await‑ot `try…catch`‑be.

**Q: Kötelező a `static` kulcsszó?**  
A: A számláló maga számára nem, de a statikus blokk kényelmes módja annak, hogy a kód *egyszer* fusson le betöltéskor – ideális naplózáshoz vagy funkció‑detektáláshoz.

## Összegzés

Épp most építettél egy **top level await példát**, amely bemutatja az `await delay javascript`‑et, egy **increment counter class**‑t, és a **public class fields javascript** erejét. A teljes, futtatható kódrészlet fent található, és a konzolkimenet bizonyítja, hogy a statikus blokk a késleltetett kód előtt fut le.

Innen tovább kísérletezhetsz összetettebb async folyamatokkal, kicserélheted a késleltetést egy valódi API‑hívásra, vagy bővítheted az osztályt további metódusokkal. Ne feledd, a modern JavaScript lehetővé teszi, hogy a modulokat elsőrendű async entitásként kezeld – extra csomagolók nélkül.

Boldog kódolást, és nyugodtan oszd meg a saját változataidat a kommentekben. Ha hasznosnak találtad ezt az útmutatót, oszd meg egy kollégáddal, aki még küzd az async mintákkal!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}