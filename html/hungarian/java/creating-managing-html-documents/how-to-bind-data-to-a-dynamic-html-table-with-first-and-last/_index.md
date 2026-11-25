---
category: general
date: 2026-09-07
description: Hogyan kössük össze az adatokat egy dinamikus HTML táblázatban – tanulja
  meg, hogyan generáljon táblázatsorokat, és hogyan töltse fel hatékonyan a keresztnév
  és vezetéknév mezőket.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: hu
lastmod: 2026-09-07
og_description: Hogyan kössünk adatokat egy dinamikus HTML táblázatban. Ez az útmutató
  bemutatja, hogyan generáljunk táblázatsorokat, jelenítsük meg a kereszt- és vezetéknevet,
  és töltsük fel a táblázatsorokat JavaScript segítségével.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Hogyan kössünk adatot egy dinamikus HTML táblához – lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: how to bind data in a dynamic HTML table – learn how to generate table
    rows and populate first and last name fields efficiently
  headline: How to bind data to a dynamic HTML table with first and last name columns
  type: TechArticle
tags:
- data binding
- html table
- templating
title: Hogyan kössünk adatot egy dinamikus HTML táblázathoz, amelynek keresztnév és
  vezetéknév oszlopai vannak
url: /hu/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan kössük össze az adatokat egy dinamikus HTML táblázattal, amely tartalmazza a keresztnév és vezetéknév oszlopokat

Ha **hogyan kössük össze az adatokat** egy olyan táblázatba, amely minden rekord hozzáadásával nő, ez az útmutató egy teljes megoldást mutat be. Meg fogod látni, hogyan generálj egy dinamikus HTML táblázatot, töltsd fel a táblázatsorokat, és jelenítsd meg minden személy keresztnév és vezetéknév értékét anélkül, hogy ismétlődő markupot írnál.

A példa egy könnyűsúlyú sablonnyelvet használ, amely bármely modern böngészőben működik, de a koncepciók alkalmazhatók a Handlebars, Mustache vagy szerver‑oldali motorokra is. A tutorial végére a kódot be tudod másolni a projektedbe, és azonnal elkezdhetsz adatokat kötni.

## Amit ez a tutorial lefed

* Hogyan strukturálj egy adatforrást, amely több személyt tartalmaz  
* Hogyan hozz létre egy újrahasználható táblázatsablont, amely minden bejegyzésnél ismétlődik  
* Hogyan kössük össze az adatokat és generáljuk a végleges HTML markupot  
* Gyakori buktatók a táblázatsorok feltöltésekor és hogyan kerüld el őket  

Nem szükséges külső könyvtár, bár ugyanaz a minta népszerű sablonkeretekkel is működik. Az egyetlen előfeltétel az alap HTML és JavaScript ismeret.

## Előfeltételek

* Egy modern böngésző (Chrome, Edge, Firefox vagy Safari)  
* Egy szerkesztő HTML/JavaScript fájlokhoz  
* Opcionális: egy JSON fájl vagy JavaScript objektum, amely a személyek gyűjteményét reprezentálja  

## 1. lépés: Az adatforrás meghatározása

Először hozz létre egy JavaScript objektumot, amely tükrözi a sablonban használt struktúrát. Minden személynek van keresztneve, vezetékneve és egy cím objektuma.

```html
<script>
  // Data source – an array of person objects
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: {
            Street: "Maple",
            Number: "12A",
            City: "Springfield"
          }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: {
            Street: "Oak",
            Number: "34B",
            City: "Riverdale"
          }
        }
        // Add more person objects as needed
      ]
    }
  };
</script>
```

**Miért fontos:** Az objektumhierarchia (`Persons.Person`) megegyezik a sablonban lévő `{{#foreach Persons.Person}}` ciklussal, lehetővé téve a motor számára, hogy automatikusan végigmenjen minden bejegyzésen.

## 2. lépés: Írd meg a táblázatsablont egy ismétlődő blokkal

Az alábbi sablon egy egyszerű Mustache‑stílusú szintaxist (`{{#foreach}}`) használ, hogy minden személyhez megismételje a `<tr>` elemet. Helyezd a sablont egy `<script type="text/template">` címkébe, hogy a böngésző figyelmen kívül hagyja, amíg fel nem dolgozod.

```html
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Table header -->
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <!-- Row populated with each person's data -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**Miért fontos:** A `{{#foreach Persons.Person}}` utasítás azt mondja a motornak, hogy minden személyobjektusra ismételje meg a nyitó és záró címkék közötti tartalmat. A soron belül bármelyik tulajdonságra hivatkozhatsz (`{{FirstName}}`, `{{LastName}}`, stb.), hogy **dinamikusan töltsd fel a táblázatsorokat**.

## 3. lépés: Implementálj egy kis renderelő függvényt

Mivel a tutorial önálló kell legyen, egy minimális renderert írunk, amely a Mustache‑stílusú helyőrzőket valós értékekkel helyettesíti. A függvény bejárja az adatobjektumot, kibővíti az ismétlődő blokkot, és beilleszti a végleges HTML-t az oldalba.

```html
<script>
  /**
   * Renders a template that contains a single {{#foreach}} block.
   * This implementation is intentionally simple and works for the
   * specific structure used in this tutorial.
   *
   * @param {string} tmpl   The raw template string.
   * @param {object} ctx    The data context (e.g., the `data` object).
   * @returns {string}      The rendered HTML.
   */
  function renderTemplate(tmpl, ctx) {
    // Extract the foreach expression and the block to repeat
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl; // No foreach found

    const path = match[1].trim(); // e.g., "Persons.Person"
    const block = match[2];       // HTML that repeats

    // Resolve the array from the context (supports dot notation)
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items)) return tmpl;

    // Render each item
    const renderedBlocks = items.map(item => {
      // Replace each {{property}} with the corresponding value
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });

    // Replace the whole foreach section with the concatenated rows
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  // When the DOM is ready, render the table
  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>
```

**Miért fontos:** A renderelő bemutatja, **hogyan generáljunk táblázat** markupot programozottan anélkül, hogy teljes könyvtárat beemelnénk. Emellett tisztázza a sablonról a végleges HTML-re való átalakulást, ami segít később a kód más sablonmotorokra való adaptálásában.

## 4. lépés: Adj hozzá egy helyőrzőt, ahol a generált táblázat megjelenik

Hozz létre egy üres `<div>` elemet, amelyet a szkript a renderelés után kitölt.

```html
<div id="output"></div>
```

Amikor az oldal betöltődik, a szkript lecseréli ennek a `<div>`-nek a tartalmát a teljesen feltöltött táblázatra.

## 5. lépés: Ellenőrizd az eredményt

Nyisd meg a HTML fájlt egy böngészőben. Egy olyan táblázatot kell látnod, amely felsorolja minden személy teljes nevét és címét:

| Személy          | Cím                         |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

Ha több objektumot adsz hozzá a `data.Persons.Person` tömbhöz, a táblázat automatikusan növekszik—teljesítve a **táblázatsorok feltöltése** követelményt.

## Profi tipp: üres gyűjtemények kezelése

Amikor az adat tömb üres, a renderelő jelenleg egy üres táblázatfejlécet ad ki. A felhasználói élmény javítása érdekében adj hozzá egy védelmet:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Ez a kis változtatás megakadályozza, hogy üres táblázat jelenjen meg, és azonnali visszajelzést ad a felhasználóknak.

## Gyakori variációk és szélhelyzetek

| Helyzet                               | Módosítás                                                                 |
|----------------------------------------|----------------------------------------------------------------------------|
| Szerver‑oldali motor használata (pl. Handlebars) | Cseréld le a saját `renderTemplate`-et a `Handlebars.compile`-ra, és add át ugyanazt az adatobjektumot. |
| Sorok betűrend szerinti rendezésére van szükség       | Rendezd a `data.Persons.Person` tömböt a `renderTemplate` hívása előtt.               |
| Telefonszám oszlop hozzáadása       | Bővítsd a `<tr>`-t `<td>{{Phone}}</td>`-vel, és szerepeltess `Phone`-t minden személyobjektumban. |
| Nagy adatállományok (száz sor)     | Rendereld a sorokat darabokban vagy használj virtuális görgetést, hogy a UI reagálóképessége megmaradjon. |

## Teljes működő példa

Az alábbiakban a teljes HTML fájl látható, amelyet átmásolhatsz a `index.html`-be. Tartalmazza az összes fent tárgyalt elemet.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to bind data to a dynamic HTML table</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<h1>Dynamic HTML table bound to JavaScript data</h1>

<!-- Step 2: Table template -->
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>

<!-- Step 1: Data source -->
<script>
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: { Street: "Maple", Number: "12A", City: "Springfield" }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: { Street: "Oak", Number: "34B", City: "Riverdale" }
        }
        // Add more entries as needed
      ]
    }
  };
</script>

<!-- Step 4: Output container -->
<div id="output"></div>

<!-- Step 3: Rendering logic -->
<script>
  function renderTemplate(tmpl, ctx) {
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl;
    const path = match[1].trim();
    const block = match[2];
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items) || items.length === 0) {
      return '<p>No records found.</p>';
    }
    const renderedBlocks = items.map(item => {
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>

</body>
</html>
```

**Várható kimenet**

Az oldal egy két soros táblázatot jelenít meg, ahol minden sor egy személy teljes nevét és formázott címét mutatja. További objektumok hozzáadása a `Person` tömbhöz automatikusan új sorokat ad hozzá—bemutatva, **hogyan generáljunk táblázat** elemeket az adatokból.

## Összegzés

Most már tudod, **hogyan kössük össze az adatokat** egy **dinamikus HTML táblázattal**, hogyan generálj sorokat minden rekordhoz, és hogyan jelenítsd meg a keresztnév és vezetéknév értékeket a cím mellett

## Mit érdemes még megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljesen működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan adjunk hozzá CSS‑t – Inline CSS HTML dokumentumokhoz Aspose.HTML for Java-ban](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Hogyan szerkesszük a HTML dokumentumfát Aspose.HTML for Java-ban](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Hogyan engedélyezzük a JavaScriptet az Aspose HTML‑ben – HTML betöltése és szöveg kinyerése](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}