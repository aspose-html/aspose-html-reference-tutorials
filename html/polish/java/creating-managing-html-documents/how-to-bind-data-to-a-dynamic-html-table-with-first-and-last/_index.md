---
category: general
date: 2026-09-07
description: jak powiązać dane w dynamicznej tabeli HTML – dowiedz się, jak generować
  wiersze tabeli i efektywnie wypełniać pola imienia i nazwiska
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: pl
lastmod: 2026-09-07
og_description: jak powiązać dane w dynamicznej tabeli HTML. Ten poradnik pokazuje,
  jak generować wiersze tabeli, wyświetlać imię i nazwisko oraz wypełniać wiersze
  tabeli przy użyciu JavaScriptu.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Jak powiązać dane z dynamiczną tabelą HTML – przewodnik krok po kroku
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
title: Jak powiązać dane z dynamiczną tabelą HTML z kolumnami imienia i nazwiska
url: /pl/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak powiązać dane z dynamiczną tabelą HTML z kolumnami imienia i nazwiska

Jeśli potrzebujesz **jak powiązać dane** w tabeli, która rośnie wraz z każdym rekordem, ten przewodnik przedstawia pełne rozwiązanie. Zobaczysz, jak wygenerować dynamiczną tabelę HTML, wypełnić wiersze tabeli i wyświetlić imię oraz nazwisko każdej osoby bez pisania powtarzalnego kodu.

Przykład używa lekkiej składni szablonów, która działa w każdej nowoczesnej przeglądarce, ale koncepcje mają zastosowanie do Handlebars, Mustache lub silników po stronie serwera. Po zakończeniu samouczka możesz skopiować kod do swojego projektu i od razu rozpocząć powiązywanie danych.

## Co obejmuje ten samouczek

* Jak zbudować źródło danych zawierające wiele osób  
* Jak stworzyć wielokrotnego użytku szablon tabeli, który powtarza się dla każdego wpisu  
* Jak powiązać dane i wygenerować ostateczny znacznik HTML  
* Typowe pułapki przy wypełnianiu wierszy tabeli i jak ich unikać  

Nie są wymagane zewnętrzne biblioteki, choć ten sam wzorzec działa z popularnymi frameworkami szablonów. Jedynym wymogiem wstępnym jest podstawowa znajomość HTML i JavaScript.

## Wymagania wstępne

* Nowoczesna przeglądarka (Chrome, Edge, Firefox lub Safari)  
* Edytor plików HTML/JavaScript  
* Opcjonalnie: plik JSON lub obiekt JavaScript reprezentujący kolekcję osób  

## Krok 1: Zdefiniuj źródło danych

Najpierw utwórz obiekt JavaScript, który odzwierciedla strukturę używaną w szablonie. Każda osoba ma imię, nazwisko oraz obiekt adresu.

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

**Dlaczego to ważne:** Hierarchia obiektów (`Persons.Person`) pasuje do pętli `{{#foreach Persons.Person}}` w szablonie, umożliwiając silnikowi automatyczne iterowanie po każdym wpisie.

## Krok 2: Napisz szablon tabeli z blokiem powtarzania

Poniższy szablon używa prostej składni w stylu Mustache (`{{#foreach}}`), aby powtórzyć element `<tr>` dla każdej osoby. Umieść szablon wewnątrz znacznika `<script type="text/template">`, aby przeglądarka go ignorowała, dopóki go nie przetworzysz.

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

**Dlaczego to ważne:** Dyrektywa `{{#foreach Persons.Person}}` instruuje silnik, aby powtórzył wszystko pomiędzy otwierającym i zamykającym tagiem dla każdego obiektu osoby. Wewnątrz wiersza możesz odwołać się do dowolnej właściwości (`{{FirstName}}`, `{{LastName}}` itp.), aby **dynamicznie wypełniać wiersze tabeli**.

## Krok 3: Zaimplementuj małą funkcję renderującą

Ponieważ samouczek musi być samodzielny, napiszemy minimalny renderer, który zastępuje znaczniki w stylu Mustache rzeczywistymi wartościami. Funkcja przegląda obiekt danych, rozwija blok powtarzania i wstawia ostateczny HTML na stronę.

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

**Dlaczego to ważne:** Renderer pokazuje **jak generować tabelę** w znacznikach programowo, bez użycia pełnej biblioteki. Wyjaśnia także transformację od szablonu do ostatecznego HTML, co ułatwia późniejsze dostosowanie kodu do innych silników szablonów.

## Krok 4: Dodaj miejsce, w którym pojawi się wygenerowana tabela

Utwórz pusty `<div>`, który skrypt wypełni po renderowaniu.

```html
<div id="output"></div>
```

Gdy strona się załaduje, skrypt zastąpi zawartość tego `<div>` w pełni wypełnioną tabelą.

## Krok 5: Zweryfikuj wynik

Otwórz plik HTML w przeglądarce. Powinieneś zobaczyć tabelę, która wymienia pełne imię i nazwisko oraz adres każdej osoby:

| Osoba           | Adres                           |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

Jeśli dodasz więcej obiektów do tablicy `data.Persons.Person`, tabela automatycznie się rozrośnie — spełniając wymóg **wypełniania wierszy tabeli**.

## Porada: obsługa pustych kolekcji

Gdy tablica danych jest pusta, renderer obecnie generuje pusty nagłówek tabeli. Aby zapewnić lepsze doświadczenie użytkownika, dodaj zabezpieczenie:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Ta mała zmiana zapobiega wyświetleniu pustej tabeli i daje użytkownikom natychmiastową informację zwrotną.

## Typowe warianty i przypadki brzegowe

| Sytuacja                               | Dostosowanie                                                                 |
|----------------------------------------|----------------------------------------------------------------------------|
| Używanie silnika po stronie serwera (np. Handlebars) | Zastąp niestandardową funkcję `renderTemplate` wywołaniem `Handlebars.compile` i przekaż ten sam obiekt danych. |
| Potrzeba sortowania wierszy alfabetycznie       | Posortuj `data.Persons.Person` przed wywołaniem `renderTemplate`.               |
| Dodanie kolumny dla numeru telefonu       | Rozszerz `<tr>` o `<td>{{Phone}}</td>` i uwzględnij `Phone` w każdym obiekcie osoby. |
| Duże zestawy danych (setki wierszy)     | Renderuj wiersze w partiach lub użyj wirtualnego przewijania, aby UI pozostało responsywne. |

## Pełny działający przykład

Poniżej znajduje się kompletny plik HTML, który możesz skopiować i wkleić do `index.html`. Zawiera wszystkie elementy omówione powyżej.

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

**Oczekiwany wynik**

Strona wyświetla tabelę z dwoma wierszami, każdy pokazujący pełne imię i nazwisko oraz sformatowany adres osoby. Dodanie większej liczby obiektów do tablicy `Person` automatycznie dodaje nowe wiersze — demonstrując **jak generować elementy tabeli** z danych.

## Podsumowanie

Teraz wiesz **jak powiązać dane** z **dynamiczną tabelą HTML**, generować wiersze dla każdego rekordu i wyświetlać wartości imienia i nazwiska obok adresu

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak dodać CSS – Inline CSS do dokumentów HTML w Aspose.HTML dla Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Jak edytować drzewo dokumentu HTML w Aspose.HTML dla Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Jak włączyć JavaScript w Aspose HTML – Ładowanie HTML i pobieranie tekstu](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}