---
category: general
date: 2026-10-12
description: Tanulja meg, hogyan generáljon táblázatot adatokból, és hogyan töltse
  fel a táblázatot JSON-ból Handlebars segítségével. Lépésről‑lépésre útmutató a táblázatsorok
  ismétléséhez dinamikus HTML‑táblázatokban.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: hu
lastmod: 2026-10-12
og_description: Készíts táblázatot adatokból, és töltsd fel a táblázatot JSON‑ból
  Handlebars segítségével. Kövesd ezt az útmutatót, hogy dinamikus HTML táblázatokat
  hozz létre ismétlődő sorokkal.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Táblázat létrehozása adatokból Handlebars segítségével – teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-12'
  description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  headline: How to generate table from data with HTML and Handlebars
  type: TechArticle
- description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  name: How to generate table from data with HTML and Handlebars
  steps:
  - name: 1. Empty data sets
    text: 'If the JSON array is empty, Handlebars will still render the header row
      but no data rows. To display a friendly message, wrap the table in a conditional
      block:'
  - name: 2. Nested loops (e.g., multiple addresses per person)
    text: 'When a person can have several addresses, you can nest another `{{#foreach}}`
      inside the row:'
  - name: 3. Using a real API
    text: 'Replace the static `<script id="people-data">` with a fetch call:'
  - name: 4. Accessibility considerations
    text: '* Add `scope="col"` to `<th>` elements. * Use `<caption>` to describe the
      table purpose. * Ensure sufficient color contrast if you apply custom CSS.'
  type: HowTo
tags:
- HTML
- Handlebars
- JSON
- templating
title: Táblázat generálása adatokból HTML és Handlebars segítségével
url: /hu/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan generáljunk táblázatot adatokból HTML és Handlebars segítségével

Ha egy weboldalon **táblázatot kell generálni adatokból**, ez a tutorial pontosan megmutatja, hogyan teheted. Egy egyszerű Handlebars ciklus segítségével **táblázatot tölthetsz fel JSON-ból**, **ismétlődő táblázatsorokat** hozhatsz létre, és egy teljesen **dinamikus HTML táblázatot** kapsz, amely frissül, amikor a forrás változik.

A következő néhány percben egy teljes, futtatható példát látsz, megérted, miért fontos minden részlet, és megtanulod, hogyan alkalmazd a mintát összetettebb helyzetekben, például feltételes oszlopok vagy beágyazott objektumok esetén.

## Mit fogunk építeni

* Beolvas egy JSON payloadot, amely személyek listáját tartalmaz.
* Minden személyhez (`repeat table rows`) egy táblázatsort ismétel.
* Minden személy keresztnevét, vezetéknevét és címét a megfelelő cellákba helyezi.
* Szerver‑oldali renderelés nélkül működik – a teljes folyamat a böngészőben zajlik.

**Előfeltételek**

* Alapvető HTML és JavaScript ismeretek.
* Modern böngésző (Chrome, Edge, Firefox vagy Safari).
* Handlebars.js – CDN‑ről töltjük be, így nincs szükség build eszközökre.

---

## 1. lépés: Készítsd elő a JSON adatforrást

Az első lépés egy JavaScript objektum definiálása, amely utánozza az API‑tól kapott JSON‑t. A Handlebars egyszerű objektumokkal működik, ezért a demonstráció kedvéért közvetlenül egy `<script>` címkébe ágyazhatod be az adatot.

```html
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>
```

**Miért fontos** – Ha az adatot egy külön `<script>` elemben tartod, később könnyen kicserélheted egy valódi AJAX hívásra. A struktúra (`Persons.Person`) megegyezik a Handlebars `{{#foreach Persons.Person}}` blokkban használt úttal, ami elengedhetetlen a **populate table from JSON**-hez.

---

## 2. lépés: Írd meg a Handlebars sablont, amely ismétli a sorokat

Ezután hozz létre egy `<script type="text/x-handlebars-template">` blokkot, amely a táblázat jelölőnyelvét tartalmazza. A Handlebars helyettesíti a placeholder‑eket a tényleges értékekkel, és minden személyhez megismétli a `<tr>` elemet.

```html
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Header row describing the columns -->
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <!-- Data row – this block is repeated for each Person -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**A kulcsfontosságú részek magyarázata**

* `{{#foreach Persons.Person}}` azt mondja a Handlebars‑nek, hogy **ismételje a táblázatsorokat** minden `Persons.Person` tömbbeli bejegyzéshez.
* A `{{FirstName}} {{LastName}}` és `{{Address.*}}` kifejezések az aktuális tömb elem értékeit veszik.
* A teljes táblázat `data_merge` attribútummal való körülvétele opcionális; hasznos lehet downstream feldolgozáshoz vagy CSS szelektorokhoz.

---

## 3. lépés: Töltsd be a Handlebars‑t és fordítsd le a sablont

A Handlebars‑t CDN‑ről töltjük be, a JSON‑t feldolgozzuk, a sablont lefordítjuk, és a végleges HTML‑t beillesztjük az oldalba.

```html
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  // Parse the JSON stored in the <script id="people-data">
  const rawData = document.getElementById('people-data').textContent;
  const context = JSON.parse(rawData);

  // Grab the template markup and compile it
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);

  // Generate the final HTML by applying the context
  const html = template(context);

  // Insert the generated table into the DOM
  document.getElementById('output').innerHTML = html;
</script>
```

**Miért fordítsuk le futásidőben?** – A sablon egyszeri lefordítása és újrahasználata gyorsabbá teszi az oldalt, különösen gyakran változó adatok esetén. Ez a minta egyszerűvé teszi a **populate table from JSON** többszöri végrehajtását az oldal újratöltése nélkül.

---

## 4. lépés: Foglalj helyet a generált táblázatnak

Adj hozzá egy helyőrző `<div>` elemet, ahol a dinamikus táblázat megjelenik. Ez tisztán tartja a markup‑ot, és szétválasztja a statikus elrendezést a generált tartalomtól.

```html
<div id="output"></div>
```

Amikor a 3. lépésben lévő script fut, a `<div id="output">` egy teljes `<table>` elemet fog tartalmazni, készen állva a stílusozásra vagy további manipulációra.

---

## 5. lépés: Ellenőrizd a kimenetet és stílusozd a táblázatot (opcionális)

Nyisd meg az oldalt egy böngészőben, és egy alább látható táblázatot kell látnod:

![Screenshot showing generated table from data](image.png "Screenshot showing generated table from data")

```html
<table border="1" data_merge="true">
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <tr>
    <td>Alice Anderson</td>
    <td>Maple 123, Springfield</td>
  </tr>
  <tr>
    <td>Bob Baker</td>
    <td>Oak 456, Rivertown</td>
  </tr>
</table>
```

**Opcionális stílus** – Ha tisztább megjelenést szeretnél, adj hozzá néhány CSS szabályt:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Szélsőséges esetek és gyakori variációk kezelése

### 1. Üres adathalmazok

Ha a JSON tömb üres, a Handlebars még mindig megjeleníti a fejlécsort, de nem jelenít meg adat sorokat. Barátságos üzenet megjelenítéséhez tedd a táblázatot egy feltételes blokkba:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Beágyazott ciklusok (pl. több cím személyenként)

Ha egy személynek több címe lehet, egy másik `{{#foreach}}` ciklust ágyazhatsz be a sorba:

```handlebars
{{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>
      {{#foreach Address}}
        {{Street}} {{Number}}, {{City}}<br>
      {{/foreach}}
    </td>
  </tr>
{{/foreach}}
```

### 3. Valódi API használata

Cseréld le a statikus `<script id="people-data">` elemet egy fetch hívásra:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Ez bemutatja ugyanazt a **dynamic table rows** technikát élő adatok lekérése közben.

### 4. Hozzáférhetőségi szempontok

* Adj `scope="col"` attribútumot a `<th>` elemekhez.
* Használj `<caption>` elemet a táblázat céljának leírásához.
* Biztosíts elegendő színkontrasztot, ha egyedi CSS‑t alkalmazol.

---

## Teljes, futtatható példa

Másold az alábbi blokkot egy `index.html` fájlba, és nyisd meg egy böngészőben. Az oldal **generate table from data**, **populate table from JSON**, és automatikusan ismétli a sorokat.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dynamic table from JSON</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; border: 1px solid #ddd; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<!-- Step 1: JSON data source -->
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>

<!-- Step 2: Handlebars template -->
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th scope="col">Person</th>
    <th scope="col">Address</th>
  </tr>
  {{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
  {{/foreach}}
</table>
</script>

<!-- Step 4: Container for the generated table -->
<div id="output"></div>

<!-- Step 3: Load Handlebars, compile, and render -->
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  const raw = document.getElementById('people-data').textContent;
  const context = JSON.parse(raw);
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);
  document.getElementById('output').innerHTML = template(context);
</script>

</body>
</html>
```

**Várt eredmény**

Egy két soros táblázat (plusz fejléc) mutatja az “Alice Anderson” és “Bob Baker” neveket a megfelelő címekkel. Az oldal offline is működik, bizonyítva, hogy **generate table from data** szerverkomponens nélkül is megvalósítható.

---

## Összegzés

Most már tudod, hogyan **generate table from data** Handlebars sablon segítségével, **populate table from JSON**, és hogyan hozz létre **repeat table rows**, amelyek egy **dynamic HTML table**-t alkotnak. A minta nagyobb adathalmazokra, beágyazott struktúrákra és élő API hívásokra is skálázható, erős alapot biztosítva bármilyen kliensoldali jelentéshez vagy admin UI‑hoz.

**Következő lépések**

* Fedezd fel a Handlebars segédfüggvényeit dátumok vagy számok formázásához.
* Kombináld ezt a megközelítést CSS Grid‑del vagy Flexbox‑szal a reszponzív táblázatelrendezésekhez.
* Integrálj lapozó vagy rendező könyvtárakat a nagyon nagy adathalmazok kezeléséhez.

Nyugodtan kísérletezz különböző JSON struktúrákkal, adj hozzá feltételes oszlopokat, vagy cseréld le a Handlebars‑t egy másik sablonmotorra – az új képességeid lehetővé teszik, hogy rugalmas, adat‑vezérelt felületeket építs gyorsan és megbízhatóan.

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [HTML dokumentum létrehozása Java‑val – JSON lekérése és tartalom generálása](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Adatkezelés és adatfolyam-kezelés Aspose.HTML‑ben Java számára](/html/english/java/data-handling-stream-management/)
- [HTML betöltése Java‑ban – Lépésről‑lépésre útmutató](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}