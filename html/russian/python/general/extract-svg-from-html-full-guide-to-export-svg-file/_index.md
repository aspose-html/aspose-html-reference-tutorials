---
category: general
date: 2026-06-04
description: Извлеките SVG из HTML и экспортируйте файл SVG с пользовательскими параметрами
  сохранения, сохраняя внешний CSS без изменений. Следуйте этому пошаговому руководству.
draft: false
keywords:
- extract svg from html
- export svg file
- svg save options
- svg external css
- inline svg markup
language: ru
og_description: Быстро извлеките SVG из HTML. В этом руководстве показано, как экспортировать
  SVG‑файл, используя параметры сохранения SVG, при этом сохраняя внешние CSS.
og_title: Извлечение SVG из HTML – Руководство по экспорту SVG‑файла
schemas:
- author: Aspose
  dateModified: '2026-06-04'
  description: Extract SVG from HTML and export SVG file with custom SVG save options,
    keeping external CSS intact. Follow this step‑by‑step tutorial.
  headline: Extract SVG from HTML – Full Guide to Export SVG File
  type: TechArticle
tags:
- SVG
- HTML
- Export
- Scripting
title: Извлечение SVG из HTML – Полное руководство по экспорту SVG‑файла
url: /ru/python/general/extract-svg-from-html-full-guide-to-export-svg-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение SVG из HTML – Полное руководство по экспорту SVG-файла

Когда‑нибудь вам нужно было **extract svg from html**, но вы не были уверены, какие вызовы API действительно дают чистый, автономный файл? Вы не одиноки. Во многих проектах веб‑автоматизации SVG находится внутри страницы, и извлечь его, сохранив оригинальное оформление, довольно сложно.  

В этом руководстве мы пройдемся по полному решению, которое не только **extracts the SVG**, но и покажет, как **export svg file** с точными **svg save options**, обеспечивая, что ваш **svg external css** остаётся внешним, а **inline svg markup** остаётся нетронутым.

## Что вы узнаете

- Как загрузить HTML‑документ с диска.
- Как найти первый элемент `<svg>` (или любой другой, который нужен).
- Как создать `SVGDocument` из **inline svg markup**.
- Какие **svg save options** отключают встраивание CSS, чтобы стили оставались во внешних файлах.
- Точные шаги для **export svg file** в нужную вам папку.
- Советы по работе с несколькими SVG, сохранению ID и устранению распространённых проблем.

Никаких тяжёлых зависимостей, только встроенные объекты скриптинга, которые вы получаете с Adobe InDesign (или любой средой, предоставляющей `HTMLDocument`, `SVGDocument` и `SVGSaveOptions`). Возьмите текстовый редактор, скопируйте код, и вы готовы к работе.

![Extract SVG from HTML workflow](extract-svg-workflow.png){alt="Рабочий процесс извлечения SVG из HTML"}

## Требования

- Adobe InDesign (или совместимый хост ExtendScript) версии 2022 или новее.
- Базовое знакомство с синтаксисом JavaScript/ExtendScript.
- HTML‑файл, содержащий хотя бы один элемент `<svg>`, который вы хотите извлечь.

Если вы удовлетворяете этим трём пунктам, можете пропустить раздел «setup» и перейти сразу к коду.

---

## Извлечение SVG из HTML – Шаг 1: Загрузка HTML‑документа

Прежде всего: вам нужен доступ к HTML‑странице, содержащей SVG. Конструктор `HTMLDocument` принимает путь к файлу и парсит разметку за вас.

```javascript
// Step 1: Load the HTML document
var htmlPath = File("YOUR_DIRECTORY/page.html"); // adjust the path
var htmlDoc = new HTMLDocument(htmlPath);
```

> **Почему это важно:** Загрузка документа предоставляет вам объектную модель, похожую на DOM, поэтому вы можете запрашивать элементы так же, как в браузере. Без этого вам пришлось бы использовать хрупкие поиски строк.

---

## Извлечение SVG из HTML – Шаг 2: Поиск первого элемента `<svg>`

Теперь, когда DOM готов, давайте получим первый узел SVG. Если нужен другой, просто измените индекс или используйте более специфичный селектор.

```javascript
// Step 2: Locate the first <svg> element
var svgElements = htmlDoc.getElementsByTagName("svg");
if (svgElements.length === 0) {
    throw new Error("No <svg> elements found in the HTML file.");
}
var svgElement = svgElements[0]; // you could loop through all if needed
```

> **Полезный совет:** `svgElements` — это коллекция, похожая на массив, поэтому вы можете итерировать её, чтобы **export multiple svg files** в последующей итерации.

---

## Inline SVG Markup – Шаг 3: Создание SVGDocument

Свойство `outerHTML` возвращает полную разметку элемента `<svg>`, включая любые встроенные атрибуты. Передача этой строки в `SVGDocument` даёт вам полноценный объект SVG, которым можно управлять или сохранять.

```javascript
// Step 3: Create an SVGDocument from the extracted markup
var svgMarkup = svgElement.outerHTML; // this is the inline svg markup
var svgDoc = new SVGDocument(svgMarkup);
```

> **Почему мы используем `outerHTML`:** Он захватывает элемент *и* его дочерние элементы, сохраняет градиенты, фильтры и любые встроенные блоки `<style>`, которые могут быть частью **inline svg markup**.

---

## SVG Save Options – Шаг 4: Настройка параметров экспорта

По умолчанию InDesign встраивает CSS непосредственно в SVG, что может увеличить размер файла и нарушить внешние стили. Чтобы сохранить таблицу стилей отдельно, переключите флаг `embedCSS`.

```javascript
// Step 4: Configure SVG save options (disable CSS embedding)
var svgOptions = new SVGSaveOptions();
svgOptions.embedCSS = false;      // ensures svg external css stays external
svgOptions.embedImages = false;   // optional: keep images as links
svgOptions.fontType = SVGFontType.OUTLINE; // optional: outline fonts
```

> **Что означает «svg external css»:** Когда `embedCSS` равно `false`, любые теги `<style>` удаляются, и SVG ссылается на отдельный CSS‑файл (если он существует). Это идеально для рабочих процессов, использующих общую таблицу стилей для множества SVG‑ресурсов.

---

## Export SVG File – Шаг 5: Сохранение извлечённого SVG

Наконец, запишите SVG на диск. Метод `save` учитывает заданные выше параметры, создавая чистый файл, готовый для веба или дальнейшей обработки.

```javascript
// Step 5: Save the extracted SVG to a separate file
var outputPath = File("YOUR_DIRECTORY/extracted.svg");
svgDoc.save(outputPath, svgOptions);
```

**Ожидаемый результат:** Файл с именем `extracted.svg` появится в `YOUR_DIRECTORY`. Откройте его в браузере — вы должны увидеть графику, отрисованную точно так же, как в оригинальном HTML, но теперь весь CSS загружается из внешних источников.

---

## Обработка нескольких SVG (Опционально)

Если ваша HTML‑страница содержит несколько SVG, оберните логику поиска и сохранения в цикл:

```javascript
for (var i = 0; i < svgElements.length; i++) {
    var element = svgElements[i];
    var doc = new SVGDocument(element.outerHTML);
    var outFile = File("YOUR_DIRECTORY/svg_" + i + ".svg");
    doc.save(outFile, svgOptions);
}
```

Эта небольшая правка позволяет вам **export svg file** массово без переписывания кода.

---

## Распространённые проблемы и как их избежать

| Признак | Вероятная причина | Решение |
|---------|-------------------|---------|
| SVG отображается пустым в браузере | CSS был встроен, а затем удалён, из‑за чего потерялись правила стилей | Убедитесь, что `svgOptions.embedCSS = false` только когда у вас готова внешняя таблица стилей. |
| Текст выглядит зазубренным | Шрифты не были преобразованы в контуры | Установите `svgOptions.fontType = SVGFontType.OUTLINE`. |
| Изображения отсутствуют | `embedImages` оставлен true, но изображения внешние | Установите `svgOptions.embedImages = false` и храните файлы изображений рядом с SVG. |
| ID конфликтуют при объединении нескольких SVG | Каждый SVG сохраняет свои оригинальные ID | Проведите пост‑обработку простым скриптом переименования или используйте опцию InDesign «unique IDs», если доступна. |

---

## Полный скрипт – готов к копированию и вставке

Ниже приведён полный скрипт, готовый к вставке в окно ExtendScript Toolkit и запуску. Замените `YOUR_DIRECTORY` на папку, содержащую ваш HTML‑файл.



## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Сохранить SVG‑документ в Aspose.HTML для Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Как конвертировать SVG в XPS с помощью Aspose.HTML для Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Создать PDF из SVG с помощью Aspose.HTML для Java](/html/hindi/java/conversion-html-to-other-formats/convert-svg-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}