---
category: general
date: 2026-10-15
description: Комбинируйте стили шрифтов в C#, задавая семейство шрифта и размер с
  помощью конструктора Aspose.HTML Font. Узнайте, как быстро создавать жирный курсивный
  текст.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- combine font styles
- set font family
- set font size c#
- c# font constructor
- create bold italic text
language: ru
lastmod: 2026-10-15
og_description: Комбинируйте стили шрифтов в C# с помощью конструктора Aspose.HTML
  Font. Этот учебник показывает, как установить семейство шрифта, задать размер шрифта
  в C# и создать полужирный курсивный текст.
og_image_alt: Screenshot of C# code that combines font styles with Aspose.HTML
og_title: Комбинирование стилей шрифтов в C# — быстрый гид по Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Combine font styles in C# by setting font family and size using the
    Aspose.HTML Font constructor. Learn to create bold italic text quickly.
  headline: How to combine font styles in C# with Aspose.HTML
  type: TechArticle
- description: Combine font styles in C# by setting font family and size using the
    Aspose.HTML Font constructor. Learn to create bold italic text quickly.
  name: How to combine font styles in C# with Aspose.HTML
  steps:
  - name: Explanation
    text: '- `"Arial"` – **set font family** to Arial, a widely supported sans‑serif
      typeface. - `12` – **set font size c#** to 12 points, which is a comfortable
      default for body text. - `WebFontStyle.Bold | WebFontStyle.Italic` – this expression
      **combines font styles**. The `|` operator merges the `Bold` and'
  - name: Why this works
    text: '- `paragraph.Style.FontFamily` uses the **set font family** value from
      the `Font` instance. - `paragraph.Style.FontSize` uses the **set font size c#**
      you defined. - The explicit `FontWeight` and `FontStyle` assignments mirror
      the **combine font styles** flags, ensuring the rendered output matches t'
  - name: Pro tip on performance
    text: 'Creating many `Font` objects inside a tight loop can degrade performance.
      Cache commonly used fonts in a dictionary and reuse them:'
  type: HowTo
tags:
- C#
- Aspose.HTML
- Font styling
title: Как комбинировать стили шрифтов в C# с Aspose.HTML
url: /ru/net/html-document-manipulation/how-to-combine-font-styles-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как комбинировать стили шрифтов в C# с Aspose.HTML

Если вам нужно **комбинировать стили шрифтов** в приложении на C#, это руководство покажет вам лаконичный способ сделать это с помощью Aspose.HTML. Вы узнаете, как задать семейство шрифтов, установить размер шрифта c#, и использовать **c# font constructor** для создания полужирного курсивного текста всего в несколько строк кода.

Разработчики часто задаются вопросом, нужно ли создавать отдельные объекты `Font` для каждого стиля или один конструктор может обрабатывать несколько атрибутов. Ответ: вы можете комбинировать стили напрямую при создании шрифта. В этом руководстве рассматривается весь процесс, от импорта нужного пространства имён до рендеринга стилизованного текста в HTML‑документе.

## Требования

- Aspose.HTML for .NET установлен (NuGet‑пакет `Aspose.HTML` версии 23.9 или новее).
- .NET 6.0+ или .NET Framework 4.7.2+.
- Базовое знакомство с синтаксисом C# и объектно‑ориентированным программированием.

Дополнительные сторонние библиотеки не требуются.

## Шаг 1: Импортируйте пространство имён drawing

Первое, что нужно сделать, — **импортировать пространство имён Aspose.Html.Drawing**, чтобы иметь доступ к классу `Font` и связанным утилитам рисования.

```csharp
using Aspose.Html.Drawing;
```

> **Почему?** Класс `Font` находится в `Aspose.Html.Drawing`. Импорт этого пространства имён делает тип доступным без необходимости полностью квалифицировать его каждый раз, что сохраняет ваш код чистым и читаемым.

## Шаг 2: Используйте конструктор шрифта C# для задания семейства, размера и комбинирования стилей

**c# font constructor** принимает три параметра: имя семейства шрифта, размер в пунктах и побитовое сочетание флагов `WebFontStyle`. Используя побитовый оператор ИЛИ (`|`), вы можете **комбинировать стили шрифтов**, например, полужирный и курсив.

```csharp
// Create a Font instance that is both bold and italic
var font = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);
```

### Объяснение

- `"Arial"` – **set font family** (задать семейство шрифта) Arial, широко поддерживаемый шрифт без засечек.
- `12` – **set font size c#** (задать размер шрифта c#) 12 пунктов, что является удобным значением по умолчанию для основного текста.
- `WebFontStyle.Bold | WebFontStyle.Italic` – это выражение **combines font styles** (комбинирует стили шрифтов). Оператор `|` объединяет флаги `Bold` и `Italic` в одно значение, позволяя конструктору создать шрифт, одновременно полужирный *и* курсивный.

> **Pro tip:** Если нужно добавить подчеркивание или зачеркивание, включите `WebFontStyle.Underline` или `WebFontStyle.Strikethrough` в то же выражение.

## Шаг 3: Примените шрифт к HTML‑элементу

Теперь, когда у вас есть объект `Font`, вы можете применить его к любому HTML‑элементу, поддерживающему стили. Ниже мы создаём простой HTML‑документ, добавляем абзац и назначаем комбинированный стиль.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

// Create a new HTML document
var document = new HTMLDocument();

// Add a paragraph element
var paragraph = document.CreateElement("p");
paragraph.InnerHtml = "This text is bold and italic using combined font styles.";
document.Body.AppendChild(paragraph);

// Apply the Font object to the paragraph's style
paragraph.Style.FontFamily = font.Family;
paragraph.Style.FontSize = $"{font.Size}pt";
paragraph.Style.FontWeight = "bold";
paragraph.Style.FontStyle = "italic";

// Render the document to an image (optional verification step)
using (var renderer = new ImageRenderer())
{
    renderer.Render(document, "output.png");
}
```

### Почему это работает

- `paragraph.Style.FontFamily` использует значение **set font family** (заданного семейства шрифта) из экземпляра `Font`.
- `paragraph.Style.FontSize` использует **set font size c#** (заданный размер шрифта c#), который вы определили.
- Явные назначения `FontWeight` и `FontStyle` отражают флаги **combine font styles** (комбинирования стилей шрифтов), гарантируя, что отрендеренный вывод соответствует ожидаемому полужирному‑курсивному виду.

> **Edge case:** Если выбранное семейство шрифта не поддерживает варианты курсив или полужирный, браузер может имитировать стиль, что может повлиять на визуальную точность. Всегда тестируйте с фактическим шрифтом, который планируете использовать.

## Шаг 4: Проверьте результат

Запустите программу и откройте `output.png`. Вы должны увидеть предложение, отрендеренное шрифтом Arial, 12 pt, с применёнными одновременно полужирным и курсивным стилями. Это подтверждает, что **c# font constructor** правильно комбинировал стили.

Если вы предпочитаете просматривать HTML напрямую, можете пропустить шаг рендеринга и сохранить документ:

```csharp
document.Save("styled.html");
```

Откройте `styled.html` в любом современном браузере, чтобы увидеть тот же стилизованный абзац.

## Распространённые варианты и советы

| Goal | Code snippet | Notes |
|------|--------------|-------|
| **Только полужирный** | `new Font("Arial", 12, WebFontStyle.Bold)` | Используйте один флаг, если курсив не нужен. |
| **Полужирный, курсив, подчеркивание** | `new Font("Arial", 12, WebFontStyle.Bold \| WebFontStyle.Italic \| WebFontStyle.Underline)` | Комбинируйте столько стилей, сколько требуется. |
| **Динамический размер** | `var size = 14; var font = new Font("Times New Roman", size, WebFontStyle.Italic);` | Размер можно вычислять во время выполнения. |
| **Пользовательское семейство шрифтов** | `new Font("MyCustomFont", 10, WebFontStyle.Bold)` | Убедитесь, что пользовательский шрифт доступен движку рендеринга (например, через `@font-face`). |

### Совет по производительности

Создание большого количества объектов `Font` внутри плотного цикла может ухудшить производительность. Кешируйте часто используемые шрифты в словаре и переиспользуйте их:

```csharp
var fontCache = new Dictionary<string, Font>();
string key = "Arial_12_BoldItalic";

if (!fontCache.TryGetValue(key, out var cachedFont))
{
    cachedFont = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);
    fontCache[key] = cachedFont;
}
```

## Полный пример, готовый к запуску

Ниже приведена автономная программа, которую вы можете скопировать, вставить и запустить. Она демонстрирует весь процесс от импорта пространства имён до рендеринга стилизованного текста.

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

class Program
{
    static void Main()
    {
        // Step 1: Import Aspose.Html.Drawing (already done via using statements)

        // Step 2: Create a Font that combines bold and italic
        var font = new Font("Arial", 12, WebFontStyle.Bold | WebFontStyle.Italic);

        // Step 3: Build a simple HTML document
        var document = new HTMLDocument();
        var paragraph = document.CreateElement("p");
        paragraph.InnerHtml = "This text is bold and italic using combined font styles.";
        document.Body.AppendChild(paragraph);

        // Apply font settings
        paragraph.Style.FontFamily = font.Family;
        paragraph.Style.FontSize = $"{font.Size}pt";
        paragraph.Style.FontWeight = "bold";
        paragraph.Style.FontStyle = "italic";

        // Optional: Render to PNG for visual verification
        using (var renderer = new ImageRenderer())
        {
            renderer.Render(document, "output.png");
        }

        // Save HTML for manual inspection
        document.Save("styled.html");

        Console.WriteLine("Styled document generated: styled.html and output.png");
    }
}
```

**Ожидаемый результат**

- `styled.html` показывает абзац с Arial 12 pt, полужирный и курсив.
- `output.png` содержит изображение того же стилизованного абзаца.

## Заключение

Теперь вы знаете, как **комбинировать стили шрифтов** в C# с помощью Aspose.HTML **c# font constructor**. Задав **set font family**, **set font size c#** и передав побитовое ИЛИ флагов `WebFontStyle`, вы можете **создавать полужирный курсивный текст** (или любую другую комбинацию) с минимальным количеством кода. Применяйте тот же шаблон к другим элементам, кешируйте шрифты для повышения производительности и расширяйте подход, добавляя подчеркивание или зачеркивание по необходимости.

Готовы изучать дальше? Попробуйте:

- Использовать `WebFontStyle.Underline` для **set font underline**.
- Загружать пользовательские веб‑шрифты с помощью `@font-face` и применять их через тот же конструктор.
- Рендерить PDF вместо изображений, заменив `ImageRenderer` на `PdfRenderer`.

Happy coding, and enjoy the flexibility of styling text programmatically in C#!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создать HTML‑документ C# – Текст полужирный курсив с пользовательским шрифтом](/html/english/net/html-document-manipulation/create-html-document-c-bold-italic-text-with-custom-font/)
- [Создать HTML‑документ C# – Рендер в PNG с полужирным курсивным шрифтом](/html/english/net/rendering-html-documents/create-html-document-c-render-to-png-with-bold-italic-font/)
- [Сохранить HTML как PDF в C# – Полное руководство с шрифтами](/html/indonesian/net/html-extensions-and-conversions/save-html-as-pdf-in-c-complete-guide-with-fonts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}