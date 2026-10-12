---
category: general
date: 2026-10-12
description: Узнайте, как генерировать таблицу из данных и заполнять её из JSON с
  помощью Handlebars. Пошаговое руководство по повторяющимся строкам таблицы в динамических
  HTML‑таблицах.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: ru
lastmod: 2026-10-12
og_description: Создайте таблицу из данных и заполните её из JSON с помощью Handlebars.
  Следуйте этому руководству, чтобы создавать динамические HTML‑таблицы с повторяющимися
  строками.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Создание таблицы из данных с Handlebars – полное руководство
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
title: Как создать таблицу из данных с помощью HTML и Handlebars
url: /ru/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сгенерировать таблицу из данных с помощью HTML и Handlebars

Если вам нужно **сгенерировать таблицу из данных** на веб‑странице, этот учебник покажет, как это сделать. С помощью простого цикла Handlebars вы сможете **заполнять таблицу из JSON**, создавать **повторяющиеся строки таблицы** и получить полностью **динамическую HTML‑таблицу**, которая обновляется каждый раз при изменении источника.

В течение нескольких минут вы увидите полностью рабочий пример, поймёте, почему каждый элемент важен, и научитесь адаптировать шаблон для более сложных сценариев, таких как условные столбцы или вложенные объекты.

## Что вы создадите

Мы создадим HTML‑таблицу, которая:

* Считывает JSON‑полезную нагрузку, содержащую список людей.
* Повторяет строку таблицы для каждого человека (`repeat table rows`).
* Вставляет имя, фамилию и адрес каждого человека в соответствующие ячейки.
* Работает без серверного рендеринга — весь процесс происходит в браузере.

**Prerequisites**

* Базовые знания HTML и JavaScript.
* Современный браузер (Chrome, Edge, Firefox или Safari).
* Handlebars.js — мы загрузим его из CDN, поэтому инструменты сборки не требуются.

---

## Шаг 1: Подготовьте источник данных JSON

Первый шаг — определить объект JavaScript, имитирующий JSON, который вы получили бы от API. Handlebars работает с обычными объектами, поэтому для демонстрации данные можно встроить напрямую в тег `<script>`.

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

**Почему это важно** — размещая данные в отдельном элементе `<script>`, вы сможете легко заменить их реальным AJAX‑запросом позже. Структура (`Persons.Person`) соответствует пути, используемому в блоке Handlebars `{{#foreach Persons.Person}}`, что необходимо для **populate table from JSON**.

---

## Шаг 2: Напишите шаблон Handlebars, повторяющий строки

Далее создайте блок `<script type="text/x-handlebars-template">`, содержащий разметку таблицы. Handlebars заменит заполнители реальными значениями и повторит `<tr>` для каждого человека.

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

**Пояснение ключевых частей**

* `{{#foreach Persons.Person}}` указывает Handlebars **repeat table rows** для каждой записи в массиве `Persons.Person`.
* Выражения `{{FirstName}} {{LastName}}` и `{{Address.*}}` извлекают значения из текущего элемента массива.
* Оборачивание всей таблицы в атрибут `data_merge` необязательно; это может быть полезно для последующей обработки или CSS‑селекторов.

---

## Шаг 3: Загрузите Handlebars и скомпилируйте шаблон

Мы получим Handlebars из CDN, разберём JSON, скомпилируем шаблон и вставим готовый HTML в страницу.

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

**Почему компилировать во время выполнения?** — компиляция шаблона один раз и его повторное использование ускоряют страницу, особенно когда данные часто меняются. Этот подход также упрощает **populate table from JSON** несколько раз без перезагрузки страницы.

---

## Шаг 4: Зарезервируйте контейнер для сгенерированной таблицы

Добавьте заполнитель `<div>`, где появится динамическая таблица. Это сохраняет разметку чистой и разделяет статический макет и генерируемый контент.

```html
<div id="output"></div>
```

Когда скрипт из Шага 3 выполнится, `<div id="output">` будет содержать полностью сформированный элемент `<table>`, готовый к стилизации или дальнейшей манипуляции.

---

## Шаг 5: Проверьте вывод и при желании стилизуйте таблицу

Откройте страницу в браузере, и вы должны увидеть таблицу, похожую на изображение ниже:

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

**Необязательная стилизация** — если хотите более чистый вид, добавьте несколько правил CSS:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Обработка граничных случаев и распространённые варианты

### 1. Пустые наборы данных

Если массив JSON пуст, Handlebars всё равно отрисует строку заголовка, но без строк данных. Чтобы вывести дружелюбное сообщение, оберните таблицу в условный блок:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Вложенные циклы (например, несколько адресов у человека)

Когда у человека может быть несколько адресов, можно вложить ещё один `{{#foreach}}` внутрь строки:

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

### 3. Использование реального API

Замените статический `<script id="people-data">` вызовом `fetch`:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Это демонстрирует ту же технику **dynamic table rows**, но с получением живых данных.

### 4. Соображения доступности

* Добавьте `scope="col"` к элементам `<th>`.
* Используйте `<caption>` для описания назначения таблицы.
* Обеспечьте достаточный контраст цветов, если применяете собственный CSS.

---

## Полный, готовый к запуску пример

Скопируйте следующий блок в файл `index.html` и откройте его в браузере. Страница **generate table from data**, **populate table from JSON** и автоматически повторит строки.

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

**Ожидаемый результат**

Таблица из двух строк (плюс заголовок) с «Alice Anderson» и «Bob Baker» и их соответствующими адресами. Страница работает офлайн, доказывая, что можно **generate table from data** без серверных компонентов.

---

## Заключение

Теперь вы знаете, как **generate table from data** с помощью шаблона Handlebars, **populate table from JSON** и создавать **repeat table rows**, образующие **dynamic HTML table**. Этот паттерн масштабируется до больших наборов данных, вложенных структур и живых API‑вызовов, предоставляя надёжную основу для любого клиентского отчёта или административного интерфейса.

**Следующие шаги**

* Исследуйте Handlebars‑helpers для форматирования дат или чисел.
* Сочетайте этот подход с CSS Grid или Flexbox для адаптивных макетов таблиц.
* Интегрируйте пагинацию или библиотеки сортировки для работы с очень большими наборами данных.

Не стесняйтесь экспериментировать с различными формами JSON, добавлять условные столбцы или заменять Handlebars другим шаблонизатором — ваши новые навыки позволят быстро и надёжно создавать гибкие, управляемые данными интерфейсы.

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}