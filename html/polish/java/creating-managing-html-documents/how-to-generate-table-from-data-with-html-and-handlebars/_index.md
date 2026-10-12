---
category: general
date: 2026-10-12
description: Dowiedz się, jak generować tabelę z danych i wypełniać ją z JSON przy
  użyciu Handlebars. Przewodnik krok po kroku, jak powielać wiersze tabeli w dynamicznych
  tabelach HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: pl
lastmod: 2026-10-12
og_description: Wygeneruj tabelę z danych i wypełnij ją danymi z JSON przy użyciu
  Handlebars. Skorzystaj z tego samouczka, aby tworzyć dynamiczne tabele HTML z powtarzającymi
  się wierszami.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Generowanie tabeli z danych przy użyciu Handlebars – kompletny przewodnik
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
title: Jak wygenerować tabelę z danych przy użyciu HTML i Handlebars
url: /pl/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak generować tabelę z danych przy użyciu HTML i Handlebars

Jeśli potrzebujesz **generować tabelę z danych** na stronie internetowej, ten tutorial pokaże Ci dokładnie, jak to zrobić. Dzięki prostemu pętli Handlebars możesz **wypełnić tabelę z JSON**, utworzyć **powtarzające się wiersze tabeli** i uzyskać w pełni **dynamiczną tabelę HTML**, która aktualizuje się za każdym razem, gdy zmieni się źródło.

W ciągu kilku minut zobaczysz kompletny, działający przykład, zrozumiesz, dlaczego każdy element ma znaczenie, oraz nauczysz się, jak dostosować wzorzec do bardziej złożonych scenariuszy, takich jak warunkowe kolumny czy zagnieżdżone obiekty.

## Co zbudujesz

Stworzymy tabelę HTML, która:

* Odczytuje ładunek JSON zawierający listę osób.
* Powtarza wiersz tabeli dla każdej osoby (`repeat table rows`).
* Wstawia imię, nazwisko i adres każdej osoby do odpowiednich komórek.
* Działa bez renderowania po stronie serwera – cały proces odbywa się w przeglądarce.

**Wymagania wstępne**

* Podstawowa znajomość HTML i JavaScript.
* Nowoczesna przeglądarka (Chrome, Edge, Firefox lub Safari).
* Handlebars.js – załadujemy go z CDN, więc nie są potrzebne narzędzia do budowania.

---

## Krok 1: Przygotuj źródło danych JSON

Pierwszym krokiem jest zdefiniowanie obiektu JavaScript, który naśladuje JSON, który otrzymałbyś z API. Handlebars działa na zwykłych obiektach, więc możesz osadzić dane bezpośrednio w znaczniku `<script>` w celach demonstracyjnych.

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

**Dlaczego to ważne** – Trzymając dane w osobnym elemencie `<script>`, możesz łatwo wymienić je później na prawdziwe wywołanie AJAX. Struktura (`Persons.Person`) odpowiada ścieżce użytej w bloku Handlebars `{{#foreach Persons.Person}}`, co jest niezbędne do **populate table from JSON**.

---

## Krok 2: Napisz szablon Handlebars, który powtarza wiersze

Następnie utwórz blok `<script type="text/x-handlebars-template">`, który zawiera znacznik tabeli. Handlebars zastąpi znaczniki rzeczywistymi wartościami i powtórzy `<tr>` dla każdej osoby.

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

**Wyjaśnienie kluczowych części**

* `{{#foreach Persons.Person}}` instruuje Handlebars, aby **repeat table rows** dla każdego elementu w tablicy `Persons.Person`.
* Wyrażenia `{{FirstName}} {{LastName}}` oraz `{{Address.*}}` pobierają wartości z bieżącego elementu tablicy.
* Otoczenie całej tabeli atrybutem `data_merge` jest opcjonalne; może być przydatne przy dalszym przetwarzaniu lub selektorach CSS.

---

## Krok 3: Załaduj Handlebars i skompiluj szablon

Pobierzemy Handlebars z CDN, sparsujemy JSON, skompilujemy szablon i wstrzykniemy ostateczny HTML do strony.

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

**Dlaczego kompilować w czasie wykonywania?** – Kompilacja szablonu raz i ponowne jego użycie utrzymuje stronę szybką, szczególnie gdy dane zmieniają się często. Ten wzorzec umożliwia również łatwe **populate table from JSON** wielokrotnie bez przeładowywania strony.

---

## Krok 4: Zarezerwuj kontener dla wygenerowanej tabeli

Dodaj placeholder `<div>`, w którym pojawi się dynamiczna tabela. Dzięki temu znacznik pozostaje czysty, a obowiązki pomiędzy statycznym układem a generowaną treścią są rozdzielone.

```html
<div id="output"></div>
```

Gdy skrypt z Kroku 3 zostanie uruchomiony, `<div id="output">` będzie zawierał w pełni utworzony element `<table>`, gotowy do stylizacji lub dalszej manipulacji.

---

## Krok 5: Zweryfikuj wynik i (opcjonalnie) wystylizuj tabelę

Otwórz stronę w przeglądarce – powinieneś zobaczyć tabelę podobną do tej poniżej:

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

**Opcjonalna stylizacja** – Jeśli chcesz uzyskać czystszy wygląd, dodaj kilka reguł CSS:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Obsługa przypadków brzegowych i typowych wariacji

### 1. Puste zestawy danych

Jeśli tablica JSON jest pusta, Handlebars nadal wyrenderuje wiersz nagłówka, ale nie wyświetli wierszy danych. Aby pokazać przyjazny komunikat, otocz tabelę blokiem warunkowym:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Zagnieżdżone pętle (np. wiele adresów dla jednej osoby)

Gdy osoba może mieć kilka adresów, możesz zagnieździć kolejny `{{#foreach}}` wewnątrz wiersza:

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

### 3. Korzystanie z prawdziwego API

Zastąp statyczny `<script id="people-data">` wywołaniem `fetch`:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

To demonstruje tę samą technikę **dynamic table rows**, ale pobierając dane na żywo.

### 4. Uwagi dotyczące dostępności

* Dodaj `scope="col"` do elementów `<th>`.
* Użyj `<caption>` do opisania przeznaczenia tabeli.
* Zapewnij wystarczający kontrast kolorów, jeśli stosujesz własny CSS.

---

## Pełny, działający przykład

Skopiuj poniższy blok do pliku `index.html` i otwórz go w przeglądarce. Strona **generate table from data**, **populate table from JSON** i automatycznie powtórzy wiersze.

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

**Oczekiwany rezultat**

Tabela dwuwierszowa (plus nagłówek) pokazująca „Alice Anderson” i „Bob Baker” wraz z ich odpowiednimi adresami. Strona działa offline, co dowodzi, że możesz **generate table from data** bez żadnego komponentu serwerowego.

---

## Zakończenie

Teraz wiesz, jak **generate table from data** przy użyciu szablonu Handlebars, **populate table from JSON** oraz tworzyć **repeat table rows**, które tworzą **dynamiczną tabelę HTML**. Wzorzec skaluje się do większych zestawów danych, zagnieżdżonych struktur i wywołań API w czasie rzeczywistym, dając solidną podstawę dla każdego raportowania po stronie klienta lub interfejsu administracyjnego.

**Kolejne kroki**

* Poznaj pomocniki Handlebars do formatowania dat lub liczb.
* Połącz to podejście z CSS Grid lub Flexbox, aby uzyskać responsywne układy tabel.
* Zintegruj biblioteki paginacji lub sortowania, aby obsłużyć bardzo duże zestawy danych.

Śmiało eksperymentuj z różnymi kształtami JSON, dodawaj warunkowe kolumny lub wymień Handlebars na inny silnik szablonów – Twoje nowe umiejętności pozwolą Ci szybko i niezawodnie budować elastyczne, oparte na danych interfejsy.

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu oraz krok‑po‑kroku wyjaśnienia, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}