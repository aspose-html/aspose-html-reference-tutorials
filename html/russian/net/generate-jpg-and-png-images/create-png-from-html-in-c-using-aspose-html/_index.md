---
category: general
date: 2026-08-12
description: Создайте PNG из HTML на C# с помощью Aspose.HTML. Узнайте, как преобразовать
  HTML в PNG и отобразить HTML как изображение всего за несколько строк кода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from html
- convert html to png
- render html as image
- how to render html to image
language: ru
lastmod: 2026-08-12
og_description: Создайте PNG из HTML в C# с помощью Aspose.HTML. Это руководство показывает,
  как быстро отобразить HTML в виде изображения, охватывая варианты конвертации, настройку
  кода и устранение неполадок.
og_image_alt: Screenshot of a C# program converting HTML to a PNG image
og_title: Создание PNG из HTML в C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Create PNG from HTML in C# with Aspose.HTML. Learn how to convert HTML
    to PNG and render HTML as image in just a few lines of code.
  headline: Create PNG from HTML in C# using Aspose.HTML
  type: TechArticle
- description: Create PNG from HTML in C# with Aspose.HTML. Learn how to convert HTML
    to PNG and render HTML as image in just a few lines of code.
  name: Create PNG from HTML in C# using Aspose.HTML
  steps:
  - name: Why this works
    text: '- **`HtmlDocument.Open`** parses the HTML string into a DOM that Aspose.HTML
      can render. - **`ImageRenderingOptions`** lets you control anti‑aliasing, text
      hinting, and font handling, which are essential when you **render HTML as image**
      to avoid blurry text. - **`ImageConverter.ConvertHtmlToImage`*'
  - name: 1. Preparing the HTML source
    text: You can load HTML from a string (as shown), a local file, or a remote URL.
  - name: 2. Fine‑tuning rendering options
    text: '| Option | Effect | When to adjust | |--------|--------|----------------|
      | `UseAntialiasing` | Reduces jagged edges on vector graphics | Always enable
      for high‑quality output | | `TextOptions.UseHinting` | Sharpens glyph edges
      | Important for small font sizes | | `FontOptions.WebFontStyle` | Choose'
  - name: 3. Performing the conversion
    text: The `ImageConverter` overload you used writes a single PNG file. If you
      need multiple pages (e.g., a multi‑page HTML document), use the overload that
      returns a collection of images.
  - name: a. Missing fonts
    text: If the HTML references a custom web font that isn’t installed on the server,
      the rendered text falls back to a default font, which may affect layout.
  - name: b. Large pages and memory consumption
    text: Rendering a very tall page can consume a lot of RAM.
  - name: c. Transparent backgrounds
    text: PNG supports transparency, but the default background is white.
  type: HowTo
tags:
- Aspose.HTML
- C#
- image rendering
- HTML conversion
title: Создание PNG из HTML в C# с использованием Aspose.HTML
url: /ru/net/generate-jpg-and-png-images/create-png-from-html-in-c-using-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PNG из HTML в C# с использованием Aspose.HTML

Если вам нужно **создать PNG из HTML** в приложении .NET, это руководство проведёт вас через весь процесс. Вы увидите, как **конвертировать HTML в PNG** всего несколькими строками кода C#, используя мощный движок рендеринга Aspose.HTML.

Рендеринг HTML в виде изображения — распространённая задача при генерации миниатюр, превью писем или отчётов, которые должны быть встроены в PDF. В последующих разделах вы узнаете точные шаги, увидите полностью рабочий пример и поймёте, почему каждый параметр важен.

## Что вы узнаете

- Как построить `HtmlDocument` из строки или файла.  
- Как настроить `ImageRenderingOptions` для повышения качества.  
- Как **конвертировать HTML в PNG** и сохранить результат на диск.  
- Советы по работе со шрифтами, большими страницами и пользовательскими путями вывода.  

**Предварительные требования**  
- .NET 6.0 SDK (или новее) установлен.  
- Действительная лицензия Aspose.HTML for .NET (или временный оценочный ключ).  
- Базовые знания C# и Visual Studio или любой совместимой с .NET IDE.

---

## Создание PNG из HTML с помощью Aspose.HTML

Первый шаг — подготовить окружение и добавить ссылки на необходимые пространства имён Aspose.HTML.

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;
using Aspose.Html.Converters;

namespace HtmlToPngDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Build the HTML document from a raw string.
            var html = "<html><body><p style='font-weight:bold;'>Bold text</p></body></html>";
            using var document = new HtmlDocument();
            document.Open(html);

            // 2️⃣ Configure rendering options for best visual fidelity.
            var renderOptions = new ImageRenderingOptions
            {
                UseAntialiasing = true,                     // Smooths edges of drawn shapes
                TextOptions = { UseHinting = true },        // Improves glyph clarity
                FontOptions = { WebFontStyle = WebFontStyle.Normal } // Uses standard web‑font style
            };

            // 3️⃣ Convert the HTML document to a PNG file.
            string outputPath = @"output.png";
            ImageConverter.ConvertHtmlToImage(document, outputPath, renderOptions);

            Console.WriteLine($"PNG image created at: {outputPath}");
        }
    }
}
```

### Почему это работает

- **`HtmlDocument.Open`** разбирает строку HTML в DOM, который может рендерить Aspose.HTML.  
- **`ImageRenderingOptions`** позволяет управлять анти‑алиасингом, подсказками текста и обработкой шрифтов, что необходимо при **рендеринге HTML в изображение**, чтобы избежать размытых символов.  
- **`ImageConverter.ConvertHtmlToImage`** выполняет основную работу: растеризует DOM в bitmap и записывает файл PNG.

Запуск программы генерирует `output.png`, содержащий жирный абзац точно так же, как в исходном HTML.

---

## Пошаговое преобразование HTML в PNG

Ниже более детальный разбор каждой фазы. Понимание назначения каждой строки поможет адаптировать код для более крупных или сложных страниц.

### 1. Подготовка источника HTML

HTML можно загрузить из строки (как показано), локального файла или удалённого URL.

```csharp
// Load from a file
var document = new HtmlDocument();
document.Open(@"C:\templates\invoice.html");

// Load from a URL (requires internet access)
document.Open("https://example.com/report.html");
```

**Подсказка:** При загрузке внешних ресурсов (CSS, изображения) убедитесь, что свойство `BaseUrl` указывает на правильную папку, чтобы относительные ссылки корректно разрешались.

### 2. Тонкая настройка параметров рендеринга

| Параметр | Эффект | Когда менять |
|----------|--------|--------------|
| `UseAntialiasing` | Снижает «зубчатость» векторной графики | Всегда включать для высокого качества |
| `TextOptions.UseHinting` | Делает контуры глифов более чёткими | Важно для небольших размеров шрифта |
| `FontOptions.WebFontStyle` | Выбирает обычный, курсивный или наклонный рендеринг веб‑шрифтов | Используйте `WebFontStyle.Oblique` для наклонных шрифтов |
| `ResolutionX` / `ResolutionY` | DPI выходного изображения | Увеличьте для печатных PNG (например, 300 DPI) |

Пример увеличения DPI:

```csharp
renderOptions.ResolutionX = 300;
renderOptions.ResolutionY = 300;
```

### 3. Выполнение конвертации

Перегрузка `ImageConverter`, которую вы использовали, записывает один файл PNG. Если нужны несколько страниц (например, многостраничный HTML‑документ), используйте перегрузку, возвращающую коллекцию изображений.

```csharp
ImageConverter.ConvertHtmlToImages(document, "output_folder", renderOptions);
```

Каждая страница будет сохранена как `output_folder/page_0.png`, `page_1.png` и т.д.

---

## Рендеринг HTML в изображение — типичные подводные камни

### a. Отсутствие шрифтов

Если HTML ссылается на пользовательский веб‑шрифт, который не установлен на сервере, отрендеренный текст будет заменён шрифтом по умолчанию, что может изменить макет.

**Решение:** Встроить шрифт с помощью правила `@font-face` в вашем CSS или указать локальную папку шрифтов через `FontOptions`.

```csharp
renderOptions.FontOptions.FontFolder = @"C:\fonts";
```

### b. Большие страницы и потребление памяти

Рендеринг очень высокой страницы может потреблять значительный объём ОЗУ.

**Решение:** Установить максимальную высоту или разбить документ на секции перед конвертацией.

```csharp
renderOptions.PageHeight = 2000; // pixels
```

### c. Прозрачные фоны

PNG поддерживает прозрачность, но фон по умолчанию — белый.

**Решение:** Изменить цвет фона на прозрачный.

```csharp
renderOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

---

## Как рендерить HTML в изображение — полный пример

Объединив всё вместе, получаем готовый для продакшна фрагмент, покрывающий самые частые требования:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;
using Aspose.Html.Converters;

namespace HtmlToPngDemo
{
    class Program
    {
        static void Main()
        {
            // Load HTML (string, file, or URL)
            string html = "<html><head><style>p{font-weight:bold;color:#0066CC;}</style></head>"
                        + "<body><p>Bold blue text</p></body></html>";
            using var document = new HtmlDocument();
            document.Open(html);

            // Configure rendering for high quality and transparency
            var renderOptions = new ImageRenderingOptions
            {
                UseAntialiasing = true,
                TextOptions = { UseHinting = true },
                FontOptions = { WebFontStyle = WebFontStyle.Normal, FontFolder = @"C:\fonts" },
                BackgroundColor = System.Drawing.Color.Transparent,
                ResolutionX = 150,
                ResolutionY = 150
            };

            // Convert and save
            string outPath = @"C:\temp\html_snapshot.png";
            ImageConverter.ConvertHtmlToImage(document, outPath, renderOptions);

            Console.WriteLine($"Image saved to {outPath}");
        }
    }
}
```

**Ожидаемый результат:** Файл `html_snapshot.png`, содержащий жирный синий абзац на прозрачном холсте. Изображение будет анти‑алиасировано, а текст — чётким благодаря подсказкам.

---

## Заключение

Теперь вы знаете, как **создать PNG из HTML** в C# с помощью Aspose.HTML. Создавая `HtmlDocument`, настраивая `ImageRenderingOptions` и вызывая `ImageConverter.ConvertHtmlToImage`, вы надёжно **конвертируете HTML в PNG** и **рендерите HTML как изображение** для любых сценариев автоматизации.

Дальше вы можете исследовать:

- Генерацию миниатюр для динамических веб‑страниц.  
- Встраивание PNG в PDF с помощью Aspose.PDF.  
- Использование того же подхода для создания JPEG или BMP, изменив расширение файла.  

Экспериментируйте с DPI, цветами фона и многостраничным рендерингом, чтобы точно соответствовать потребностям вашего проекта. Приятного кодинга!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Render HTML as PNG in .NET with Aspose.HTML](/html/english/net/rendering-html-documents/render-html-as-png/)
- [How to Render HTML as PNG – Complete C# Guide](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [Create PNG from HTML – Full C# Rendering Guide](/html/english/net/rendering-html-documents/create-png-from-html-full-c-rendering-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}