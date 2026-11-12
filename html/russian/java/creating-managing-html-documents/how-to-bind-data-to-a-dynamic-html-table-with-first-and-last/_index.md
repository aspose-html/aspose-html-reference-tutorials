---
category: general
date: 2026-09-07
description: как привязывать данные в динамической HTML‑таблице — узнайте, как эффективно
  генерировать строки таблицы и заполнять поля имени и фамилии
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: ru
lastmod: 2026-09-07
og_description: как привязать данные в динамической HTML‑таблице. Этот учебник показывает,
  как генерировать строки таблицы, отображать имя и фамилию и заполнять строки таблицы
  с помощью JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Как привязать данные к динамической HTML‑таблице — пошаговое руководство
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
title: Как привязать данные к динамической HTML‑таблице с колонками имени и фамилии
url: /ru/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как привязать данные к динамической HTML‑таблице с колонками имени и фамилии

Если вам нужно **привязать данные** к таблице, которая растёт с каждой записью, это руководство предлагает полное решение. Вы увидите, как создать динамическую HTML‑таблицу, заполнять строки таблицы и отображать имя и фамилию каждого человека без написания повторяющегося разметки.

Пример использует лёгкий синтаксис шаблонов, который работает в любом современном браузере, но концепции применимы к Handlebars, Mustache или серверным движкам. К концу урока вы сможете скопировать код в свой проект и сразу начать привязывать данные.

## Что покрывает это руководство

* Как структурировать источник данных, содержащий несколько человек  
* Как создать переиспользуемый шаблон таблицы, который повторяется для каждой записи  
* Как привязать данные и сгенерировать окончательную HTML‑разметку  
* Распространённые подводные камни при заполнении строк таблицы и как их избежать  

Внешние библиотеки не требуются, хотя тот же шаблон работает с популярными фреймворками шаблонизации. Единственное требование — базовые знания HTML и JavaScript.

## Предварительные требования

* Современный браузер (Chrome, Edge, Firefox или Safari)  
* Редактор для файлов HTML/JavaScript  
* Необязательно: JSON‑файл или объект JavaScript, представляющий коллекцию людей  

## Шаг 1: Определите источник данных

Сначала создайте объект JavaScript, который отражает структуру, используемую в шаблоне. Каждый человек имеет имя, фамилию и объект адреса.

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

**Почему это важно:** Иерархия объекта (`Persons.Person`) соответствует циклу `{{#foreach Persons.Person}}` в шаблоне, позволяя движку автоматически проходить по каждой записи.

## Шаг 2: Напишите шаблон таблицы с блоком повторения

Шаблон ниже использует простой синтаксис в стиле Mustache (`{{#foreach}}`) для повторения `<tr>` для каждого человека. Поместите шаблон внутрь тега `<script type="text/template">`, чтобы браузер игнорировал его до обработки.

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

**Почему это важно:** Директива `{{#foreach Persons.Person}}` сообщает движку повторять всё между открывающим и закрывающим тегами для каждого объекта человека. Внутри строки вы можете ссылаться на любое свойство (`{{FirstName}}`, `{{LastName}}` и т.д.), чтобы **заполнять строки таблицы** динамически.

## Шаг 3: Реализуйте небольшую функцию рендеринга

Поскольку руководство должно быть автономным, мы напишем минимальный рендерер, который заменяет заполнители в стиле Mustache реальными значениями. Функция проходит по объекту данных, разворачивает блок повторения и вставляет окончательный HTML на страницу.

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

**Почему это важно:** Рендерер демонстрирует **как генерировать таблицу** программно без подключения полной библиотеки. Он также проясняет трансформацию от шаблона к финальному HTML, что поможет адаптировать код под другие движки шаблонизации в дальнейшем.

## Шаг 4: Добавьте место‑заполнитель, где появится сгенерированная таблица

Создайте пустой `<div>`, который скрипт заполнит после рендеринга.

```html
<div id="output"></div>
```

При загрузке страницы скрипт заменит содержимое этого `<div>` полностью заполненной таблицей.

## Шаг 5: Проверьте результат

Откройте HTML‑файл в браузере. Вы должны увидеть таблицу, в которой перечислены полные имена и адреса каждого человека:

| Person          | Address                         |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

Если добавить больше объектов в массив `data.Persons.Person`, таблица автоматически расширится — удовлетворяя требование **заполнять строки таблицы**.

## Совет профессионала: обработка пустых коллекций

Когда массив данных пуст, текущий рендерер выводит только заголовок таблицы. Чтобы улучшить пользовательский опыт, добавьте проверку:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Это небольшое изменение предотвращает появление пустой таблицы и сразу даёт пользователю обратную связь.

## Распространённые варианты и граничные случаи

| Ситуация                               | Корректировка                                                                 |
|----------------------------------------|----------------------------------------------------------------------------|
| Использование серверного движка (например, Handlebars) | Замените пользовательскую `renderTemplate` на `Handlebars.compile` и передайте тот же объект данных. |
| Необходимо сортировать строки по алфавиту | Отсортируйте `data.Persons.Person` перед вызовом `renderTemplate`.               |
| Добавление колонки с номером телефона  | Расширьте `<tr>` добавив `<td>{{Phone}}</td>` и включите `Phone` в каждый объект человека. |
| Большие наборы данных (сотни строк)   | Рендерите строки порциями или используйте виртуальную прокрутку для поддержания отзывчивости UI. |

## Полный рабочий пример

Ниже представлен полный HTML‑файл, который можно скопировать‑вставить в `index.html`. Он содержит все обсуждаемые выше части.

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

**Ожидаемый вывод**

Страница отображает таблицу с двумя строками, каждая из которых показывает полное имя и отформатированный адрес человека. Добавление новых объектов в массив `Person` автоматически добавит новые строки — демонстрируя **как генерировать элементы таблицы** из данных.

## Заключение

Теперь вы знаете **как привязать данные** к **динамической HTML‑таблице**, генерировать строки для каждой записи и отображать значения имени и фамилии рядом с адресом.

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Enable JavaScript in Aspose HTML – Load HTML & Get Text](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}