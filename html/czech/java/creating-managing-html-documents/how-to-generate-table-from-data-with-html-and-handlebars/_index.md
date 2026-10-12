---
category: general
date: 2026-10-12
description: Naučte se, jak vytvořit tabulku z dat a naplnit ji z JSON pomocí Handlebars.
  Krok za krokem průvodce opakováním řádků tabulky v dynamických HTML tabulkách.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: cs
lastmod: 2026-10-12
og_description: Vytvořte tabulku z dat a naplňte ji z JSON pomocí Handlebars. Postupujte
  podle tohoto tutoriálu a vytvořte dynamické HTML tabulky s opakujícími se řádky.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Vytvořte tabulku z dat pomocí Handlebars – kompletní průvodce
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
title: Jak vygenerovat tabulku z dat pomocí HTML a Handlebars
url: /cs/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak generovat tabulku z dat pomocí HTML a Handlebars

Pokud potřebujete **generovat tabulku z dat** na webové stránce, tento tutoriál vám přesně ukáže, jak na to. Pomocí jednoduché smyčky Handlebars můžete **naplnit tabulku z JSON**, vytvořit **opakovat řádky tabulky** a získat plně **dynamickou HTML tabulku**, která se aktualizuje vždy, když se zdroj změní.

V následujících několika minutách uvidíte kompletní, spustitelný příklad, pochopíte, proč je každá část důležitá, a naučíte se, jak přizpůsobit vzor pro složitější scénáře, jako jsou podmíněné sloupce nebo vnořené objekty.

## Co vytvoříte

Vytvoříme HTML tabulku, která:

* Načte JSON payload obsahující seznam osob.
* Opakuje řádek tabulky pro každou osobu (`repeat table rows`).
* Vloží křestní jméno, příjmení a adresu každé osoby do příslušných buněk.
* Funguje bez server‑side renderování – celý proces probíhá v prohlížeči.

**Požadavky**

* Základní znalosti HTML a JavaScriptu.
* Moderní prohlížeč (Chrome, Edge, Firefox nebo Safari).
* Handlebars.js – načteme jej z CDN, takže nejsou potřeba žádné nástroje pro sestavení.

---

## Krok 1: Připravte zdroj dat JSON

Prvním krokem je definovat JavaScriptový objekt, který napodobuje JSON, který byste získali z API. Handlebars pracuje s obyčejnými objekty, takže můžete data vložit přímo do značky `<script>` pro demonstrační účely.

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

**Proč je to důležité** – Uložení dat do samostatného elementu `<script>` vám umožní později snadno nahradit skutečným AJAX voláním. Struktura (`Persons.Person`) odpovídá cestě použité v Handlebars bloku `{{#foreach Persons.Person}}`, což je nezbytné pro **naplnit tabulku z JSON**.

---

## Krok 2: Napište Handlebars šablonu, která opakuje řádky

Dále vytvořte blok `<script type="text/x-handlebars-template">`, který obsahuje značky tabulky. Handlebars nahradí zástupné symboly skutečnými hodnotami a opakuje `<tr>` pro každou osobu.

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

**Vysvětlení klíčových částí**

* `{{#foreach Persons.Person}}` říká Handlebars, aby **opakoval řádky tabulky** pro každý záznam v poli `Persons.Person`.
* Výrazy `{{FirstName}} {{LastName}}` a `{{Address.*}}` získávají hodnoty z aktuálního prvku pole.
* Zabalení celé tabulky do atributu `data_merge` je volitelné; může být užitečné pro následné zpracování nebo CSS selektory.

---

## Krok 3: Načtěte Handlebars a zkompilujte šablonu

Načteme Handlebars z CDN, rozparsujeme JSON, zkompilujeme šablonu a vložíme finální HTML do stránky.

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

**Proč kompilovat za běhu?** – Kompilace šablony jednou a její opakované používání udržuje stránku rychlou, zejména když se data často mění. Tento vzor také usnadňuje **naplnit tabulku z JSON** vícekrát bez nutnosti znovu načíst stránku.

---

## Krok 4: Vyhraďte kontejner pro vygenerovanou tabulku

Přidejte zástupný `<div>`, kde se zobrazí dynamická tabulka. To udržuje značky čisté a odděluje starost o statické rozvržení od generovaného obsahu.

```html
<div id="output"></div>
```

Když se spustí skript ze Krok 3, `<div id="output">` bude obsahovat plně vytvořený element `<table>`, připravený k stylování nebo dalším úpravám.

---

## Krok 5: Ověřte výstup a stylujte tabulku (volitelné)

Otevřete stránku v prohlížeči a měli byste vidět tabulku podobnou té níže:

![Snímek obrazovky ukazující vygenerovanou tabulku z dat](image.png "Snímek obrazovky ukazující vygenerovanou tabulku z dat")

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

**Volitelné stylování** – Pokud chcete čistší vzhled, přidejte několik CSS pravidel:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Řešení okrajových případů a běžných variant

### 1. Prázdné datové sady

Pokud je pole JSON prázdné, Handlebars stále vykreslí řádek hlavičky, ale žádné řádky s daty. Pro zobrazení přátelské zprávy obalte tabulku podmíněným blokem:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Vnořené smyčky (např. více adres na osobu)

Když může mít osoba několik adres, můžete uvnitř řádku vložit další `{{#foreach}}`:

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

### 3. Použití skutečného API

Nahraďte statický `<script id="people-data">` voláním fetch:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Toto demonstruje stejnou techniku **dynamických řádků tabulky** při načítání živých dat.

### 4. Úvahy o přístupnosti

* Přidejte `scope="col"` k elementům `<th>`.
* Použijte `<caption>` k popisu účelu tabulky.
* Zajistěte dostatečný kontrast barev, pokud použijete vlastní CSS.

---

## Kompletní, spustitelný příklad

Zkopírujte následující blok do souboru `index.html` a otevřete jej v prohlížeči. Stránka **vygeneruje tabulku z dat**, **naplní tabulku z JSON** a automaticky bude opakovat řádky.

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

**Očekávaný výsledek**

Tabulka se dvěma řádky (plus hlavička) zobrazující „Alice Anderson“ a „Bob Baker“ s jejich příslušnými adresami. Stránka funguje offline, což dokazuje, že můžete **generovat tabulku z dat** bez jakékoli serverové komponenty.

---

## Závěr

Nyní víte, jak **generovat tabulku z dat** pomocí Handlebars šablony, **naplnit tabulku z JSON** a vytvořit **opakovat řádky tabulky**, které tvoří **dynamickou HTML tabulku**. Tento vzor se škáluje na větší datové sady, vnořené struktury a živá volání API, což vám poskytuje robustní základ pro jakékoli klientské reportování nebo administrativní UI.

**Další kroky**

* Prozkoumejte Handlebars pomocníky pro formátování dat nebo čísel.
* Kombinujte tento přístup s CSS Grid nebo Flexbox pro responzivní rozvržení tabulek.
* Integrujte knihovny pro stránkování nebo řazení, abyste zvládli velmi velké datové sady.

Neváhejte experimentovat s různými tvary JSON, přidávat podmíněné sloupce nebo vyměnit Handlebars za jiný šablonovací engine – vaše nové dovednosti vám umožní rychle a spolehlivě vytvářet flexibilní, datově řízené rozhraní.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}