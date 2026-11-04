---
category: general
date: 2026-09-07
description: jak svázat data v dynamické HTML tabulce – naučte se efektivně generovat
  řádky tabulky a vyplňovat pole jména a příjmení
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: cs
lastmod: 2026-09-07
og_description: jak svázat data v dynamické HTML tabulce. Tento tutoriál ukazuje,
  jak generovat řádky tabulky, zobrazit jméno a příjmení a naplnit řádky tabulky pomocí
  JavaScriptu.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Jak svázat data s dynamickou HTML tabulkou – krok za krokem průvodce
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
title: Jak svázat data s dynamickou HTML tabulkou se sloupci jméno a příjmení
url: /cs/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak svázat data s dynamickou HTML tabulkou se sloupci křestní a příjmení

Pokud potřebujete **svázat data** do tabulky, která roste s každým záznamem, tento návod ukazuje kompletní řešení. Uvidíte, jak vygenerovat dynamickou HTML tabulku, naplnit řádky tabulky a zobrazit křestní i příjmení každé osoby, aniž byste museli psát opakující se značky.

Příklad používá lehkou šablonovací syntaxi, která funguje v jakémkoli moderním prohlížeči, ale koncepty platí i pro Handlebars, Mustache nebo server‑side enginy. Na konci tutoriálu můžete kód zkopírovat do svého projektu a okamžitě začít svazovat data.

## Co tento tutoriál pokrývá

* Jak strukturovat zdroj dat obsahující více osob  
* Jak vytvořit znovupoužitelnou šablonu tabulky, která se opakuje pro každý záznam  
* Jak svázat data a vygenerovat finální HTML značky  
* Běžné úskalí při naplňování řádků tabulky a jak se jim vyhnout  

Externí knihovny nejsou vyžadovány, i když stejný vzor funguje s populárními šablonovacími frameworky. Jedinou podmínkou jsou základní znalosti HTML a JavaScriptu.

## Předpoklady

* Moderní prohlížeč (Chrome, Edge, Firefox nebo Safari)  
* Editor pro soubory HTML/JavaScript  
* Volitelně: JSON soubor nebo JavaScript objekt představující kolekci osob  

## Krok 1: Definujte zdroj dat

Nejprve vytvořte JavaScript objekt, který odráží strukturu použité v šabloně. Každá osoba má křestní jméno, příjmení a objekt adresy.

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

**Proč je to důležité:** Hierarchie objektu (`Persons.Person`) odpovídá smyčce `{{#foreach Persons.Person}}` v šabloně, což umožňuje enginu automaticky iterovat přes každý záznam.

## Krok 2: Napište šablonu tabulky s blokem opakování

Níže uvedená šablona používá jednoduchou Mustache‑stylovou syntaxi (`{{#foreach}}`) k opakování `<tr>` pro každou osobu. Umístěte šablonu do značky `<script type="text/template">`, aby ji prohlížeč ignoroval, dokud ji nebudete zpracovávat.

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

**Proč je to důležité:** Direktiva `{{#foreach Persons.Person}}` říká enginu, aby opakoval vše mezi otevírací a uzavírací značkou pro každý objekt osoby. Uvnitř řádku můžete odkazovat na libovolnou vlastnost (`{{FirstName}}`, `{{LastName}}` atd.) a **dynamicky naplňovat řádky tabulky**.

## Krok 3: Implementujte malou funkci pro vykreslení

Protože tutoriál musí být samostatný, napíšeme minimální vykreslovač, který nahradí Mustache‑stylové zástupné symboly skutečnými hodnotami. Funkce prochází datový objekt, rozšiřuje blok opakování a vloží finální HTML do stránky.

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

**Proč je to důležité:** Vykreslovač ukazuje **jak generovat tabulku** programově bez nutnosti načítat kompletní knihovnu. Také objasňuje transformaci ze šablony na finální HTML, což vám pomůže později přizpůsobit kód jiným šablonovacím enginům.

## Krok 4: Přidejte zástupný prvek, kam se vygenerovaná tabulka zobrazí

Vytvořte prázdný `<div>`, který skript po vykreslení naplní.

```html
<div id="output"></div>
```

Když se stránka načte, skript nahradí obsah tohoto `<div>` plně vyplněnou tabulkou.

## Krok 5: Ověřte výsledek

Otevřete HTML soubor v prohlížeči. Měli byste vidět tabulku, která vypisuje celé jméno a adresu každé osoby:

| Osoba           | Adresa                          |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

Pokud přidáte další objekty do pole `data.Persons.Person`, tabulka se automaticky rozroste — splní tak požadavek **naplnit řádky tabulky**.

## Tip: zpracování prázdných kolekcí

Když je datové pole prázdné, vykreslovač nyní vytváří prázdnou hlavičku tabulky. Pro lepší uživatelský zážitek přidejte podmínku:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Tato malá úprava zabrání zobrazení prázdné tabulky a poskytne uživatelům okamžitou zpětnou vazbu.

## Běžné varianty a okrajové případy

| Situace                                 | Úprava                                                                 |
|----------------------------------------|------------------------------------------------------------------------|
| Použití server‑side enginu (např. Handlebars) | Nahraďte vlastní `renderTemplate` voláním `Handlebars.compile` a předáním stejného datového objektu. |
| Potřeba seřadit řádky abecedně          | Seřaďte `data.Persons.Person` před voláním `renderTemplate`.          |
| Přidání sloupce pro telefonní číslo     | Rozšiřte `<tr>` o `<td>{{Phone}}</td>` a zahrňte `Phone` do každého objektu osoby. |
| Velké datové sady (stovky řádků)        | Vykreslujte řádky po částech nebo použijte virtuální posouvání, aby UI zůstalo responzivní. |

## Kompletní funkční příklad

Níže je celý HTML soubor, který můžete zkopírovat do `index.html`. Obsahuje všechny části probírané výše.

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

**Očekávaný výstup**

Stránka vykreslí tabulku se dvěma řádky, přičemž každý zobrazuje celé jméno a formátovanou adresu osoby. Přidáním dalších objektů do pole `Person` se automaticky přidají nové řádky — ukazuje **jak generovat tabulkové elementy** z dat.

## Závěr

Nyní už víte **jak svázat data** s **dynamickou HTML tabulkou**, generovat řádky pro každý záznam a zobrazovat hodnoty křestního a příjmení vedle adresy.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční kódové příklady s podrobným krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vlastních projektech.

- [Jak přidat CSS – Inline CSS do HTML dokumentů v Aspose.HTML pro Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Jak upravit HTML Document Tree v Aspose.HTML pro Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Jak povolit JavaScript v Aspose HTML – Načíst HTML a získat text](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}