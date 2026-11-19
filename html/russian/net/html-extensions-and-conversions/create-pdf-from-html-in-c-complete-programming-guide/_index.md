---
category: general
date: 2026-06-22
description: Создавайте PDF из HTML в C# быстро — узнайте, как конвертировать HTML
  в PDF, сохранять HTML как PDF и экспортировать HTML в PDF с помощью простой библиотеки.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- save html as pdf
- export html as pdf
- how to convert html to pdf
language: ru
og_description: Создайте PDF из HTML в C# с помощью лёгкого конвертера. Это руководство
  покажет, как конвертировать HTML в PDF, сохранить HTML как PDF и экспортировать
  HTML в PDF с чистым кодом.
og_title: Создание PDF из HTML в C# – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create PDF from HTML in C# quickly—learn how to convert HTML to PDF,
    save HTML as PDF, and export HTML as PDF with a simple library.
  headline: Create PDF from HTML in C# – Complete Programming Guide
  type: TechArticle
- description: Create PDF from HTML in C# quickly—learn how to convert HTML to PDF,
    save HTML as PDF, and export HTML as PDF with a simple library.
  name: Create PDF from HTML in C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code works on .NET Core and .NET Framework
      alike). - Basic familiarity with C# and the command line. - An HTML file you
      want to turn into a PDF (we’ll call it `input.html`).'
  - name: How It Works
    text: 1. **Reading the HTML** – We pull the raw HTML string from `input.html`.
      This step is crucial for the **save html as pdf** part because the converter
      works with a string, not a file handle. 2. **Creating a `PdfDocument`** – Think
      of this as the blank canvas where each page will be painted. 3. **`Pdf
  - name: Handling CSS and Images
    text: '```csharp // Load HTML with a base URL so relative paths resolve correctly.
      string baseUrl = Path.GetDirectoryName(htmlPath) ?? ""; PdfGenerator.AddPdfPages(pdf,
      htmlContent, PageSize.A4, new PdfGenerateConfig { BaseUrl = new Uri($"file:///{baseUrl}/")
      }); ```'
  - name: Large Documents & Pagination
    text: 'If your HTML creates many pages, the library automatically adds them. However,
      you might want to control page breaks manually:'
  type: HowTo
tags:
- C#
- HTML
- PDF
- Conversion
title: Создание PDF из HTML в C# – Полное руководство по программированию
url: /ru/net/html-extensions-and-conversions/create-pdf-from-html-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF из HTML в C# – Полное руководство по программированию

Ever wondered how to **create PDF from HTML** without wrestling with a dozen command‑line tools? You're not alone. Most developers hit that snag when they need to turn a dynamic web page into a printable report, an invoice, or a downloadable brochure.

В этом руководстве мы пройдём через простой, сквозной процесс, который позволяет вам **convert HTML to PDF**, **save HTML as PDF** и даже **export HTML as PDF** всего несколькими строками C#. К концу вы получите переиспользуемый метод, который можно добавить в любой проект .NET — без скрытых зависимостей, без волшебства.

## Что вы узнаете

- Как настроить минимальное консольное приложение C# для конвертации HTML‑в‑PDF.  
- Точный код, необходимый для **create PDF from HTML** с использованием популярной библиотеки *HtmlRenderer.PdfSharp* (или любой аналогичной библиотеки).  
- Почему вы можете предпочесть синхронный вызов вместо асинхронного и в каких случаях каждый из них имеет смысл.  
- Распространённые подводные камни — отсутствие CSS, большие изображения и относительные пути — и как их обойти.  
- Быстрый тест, который вы можете выполнить, чтобы убедиться, что вывод соответствует ожиданиям.

### Требования

- .NET 6.0 SDK или новее (код работает как на .NET Core, так и на .NET Framework).  
- Базовое знакомство с C# и командной строкой.  
- HTML‑файл, который вы хотите превратить в PDF (будем называть его `input.html`).  

Если у вас есть всё это, давайте погрузимся.

## Создание PDF из HTML — настройка проекта

Сначала создайте новый консольный проект. Откройте терминал и введите:

```bash
dotnet new console -n HtmlToPdfDemo
cd HtmlToPdfDemo
```

Затем добавьте библиотеку конвертации. Для этого примера мы будем использовать **HtmlRenderer.PdfSharp**, которая оборачивает PdfSharp и сразу поддерживает большинство HTML/CSS:

```bash
dotnet add package HtmlRenderer.PdfSharp --version 1.7.2
```

> **Pro tip:** Если вы нацелены на .NET Framework, вы всё равно можете использовать тот же пакет NuGet; просто убедитесь, что ваш файл проекта нацелен на соответствующую версию фреймворка.

Теперь у вас есть всё необходимое для **convert html to pdf**.

## Конвертация HTML в PDF — использование HtmlToPdfConverter

Создайте новый файл класса с именем `PdfConverter.cs` (или оставьте всё в `Program.cs` для быстрой демонстрации). Ниже приведён **полный, исполняемый** пример, который загружает HTML‑документ, конвертирует его и записывает результат на диск.

```csharp
using System;
using System.IO;
using TheArtOfDev.HtmlRenderer.PdfSharp;   // Namespace from HtmlRenderer.PdfSharp
using PdfSharp.Pdf;

namespace HtmlToPdfDemo
{
    /// <summary>
    /// Simple helper that encapsulates the HTML → PDF conversion logic.
    /// </summary>
    public static class PdfConverter
    {
        /// <summary>
        /// Converts the specified HTML file to a PDF and saves it.
        /// </summary>
        /// <param name="htmlPath">Full path to the source HTML file.</param>
        /// <param name="pdfPath">Full path where the PDF should be written.</param>
        public static void ConvertHtmlToPdf(string htmlPath, string pdfPath)
        {
            // Validate inputs early – helps you avoid vague exceptions later.
            if (!File.Exists(htmlPath))
                throw new FileNotFoundException($"HTML file not found: {htmlPath}");

            // Read the HTML content. Using UTF‑8 ensures you keep any special characters.
            string htmlContent = File.ReadAllText(htmlPath);

            // Create a new PDF document. This is the container that will hold our pages.
            using PdfDocument pdf = new PdfDocument();

            // The HtmlRender library does the heavy lifting. It parses the HTML and draws it onto a PDF page.
            PdfGenerator.AddPdfPages(pdf, htmlContent, PageSize.A4);

            // Finally, write the PDF to the destination path.
            pdf.Save(pdfPath);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment.
            string inputHtml = Path.Combine(Environment.CurrentDirectory, "input.html");
            string outputPdf = Path.Combine(Environment.CurrentDirectory, "output.pdf");

            try
            {
                PdfConverter.ConvertHtmlToPdf(inputHtml, outputPdf);
                Console.WriteLine($"✅ Success! PDF created at: {outputPdf}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to create PDF: {ex.Message}");
            }
        }
    }
}
```

### Как это работает

1. **Reading the HTML** – Мы получаем строку сырого HTML из `input.html`. Этот шаг критичен для части **save html as pdf**, потому что конвертер работает со строкой, а не с файловым дескриптором.  
2. **Creating a `PdfDocument`** – Представьте это как пустой холст, на котором будет рисоваться каждая страница.  
3. `PdfGenerator.AddPdfPages` – Сердце библиотеки; она парсит HTML, применяет базовый CSS и рендерит его на одну или несколько страниц A4.  
4. **Saving the file** – Вызов `pdf.Save` записывает бинарный PDF на диск, фактически **export html as pdf**.

Запустите программу:

```bash
dotnet run
```

Если всё настроено правильно, вы увидите зелёную галочку и найдете `output.pdf` рядом с вашим исполняемым файлом.

## Сохранение HTML в PDF — детали работы с файлами

Вы можете задаться вопросом, *«Почему бы не передавать PDF напрямую в ответ?»* Хороший вопрос. Во многих сценариях веб‑API вы действительно будете передавать байты, но для настольных приложений или пакетных заданий часто нужен физический файл. Приведённый выше код уже **save html as pdf** вызовом `pdf.Save(pdfPath)`.

A couple of nuances:

- **Overwrite protection** – `pdf.Save` безмолвно заменит существующий файл. Если нужна безопасность, сначала проверьте `File.Exists(pdfPath)` и либо переименуйте, либо запросите подтверждение у пользователя.  
- **Folder permissions** – Убедитесь, что процесс имеет права записи в целевую папку, особенно в Linux‑контейнерах, где пользователь по умолчанию может быть ограничен.  
- **Encoding** – HTML‑файл должен быть в кодировке UTF‑8; иначе в конечном PDF могут появиться искажённые символы.

## Экспорт HTML в PDF — расширенные параметры

Простой пример работает для большинства статических страниц, но в реальном мире HTML часто включает внешние CSS, изображения или даже JavaScript. Вот как можно расширить конвертер для обработки этих случаев.

### Обработка CSS и изображений

```csharp
// Load HTML with a base URL so relative paths resolve correctly.
string baseUrl = Path.GetDirectoryName(htmlPath) ?? "";
PdfGenerator.AddPdfPages(pdf, htmlContent, PageSize.A4, 
    new PdfGenerateConfig
    {
        BaseUrl = new Uri($"file:///{baseUrl}/")
    });
```

- **BaseUrl** указывает рендереру, где искать `src="images/logo.png"` или `href="styles/main.css"`.  
- Для удалённых ресурсов вы можете задать `BaseUrl` как HTTP‑URL, но будьте осторожны с сетевой задержкой.

### Большие документы и разбиение на страницы

Если ваш HTML создаёт много страниц, библиотека автоматически добавит их. Тем не менее, вы можете управлять разрывами страниц вручную:

```html
<div style="page-break-after: always;"></div>
```

В C# вы также можете разбить HTML на секции и вызывать `AddPdfPages` последовательно, получая более тонкий контроль над заголовками и нижними колонтитулами.

## Как конвертировать HTML в PDF — распространённые подводные камни

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| Отсутствуют шрифты | PdfSharp по умолчанию использует только стандартные шрифты. | Встроить TrueType‑шрифты через `PdfFontResolver`. |
| Изображения не отображаются | Относительные пути сломаны или форматы не поддерживаются. | Использовать `BaseUrl` или встроить изображения в Base64. |
| CSS не применяется | Библиотека поддерживает только подмножество CSS. | Держите стили простыми или предварительно обработайте HTML с помощью безголового браузера (например, Puppeteer). |
| Недостаток памяти при больших страницах | Все страницы хранятся в памяти до вызова `Save`. | Конвертировать частями или использовать потоковый API, если доступен. |

## Ожидаемый результат

После запуска примера откройте `output.pdf` в любом просмотрщике PDF. Вы должны увидеть точную визуализацию `input.html` — заголовки, абзацы и изображения (если есть) — все размещённые на страницах A4. Размер файла обычно варьируется от 50 KB для простого текста до нескольких сотен килобайт для страниц с большим количеством изображений.

![create pdf from html example output](https://example.com/assets/create-pdf-from-html.png "create pdf from html example output")

*Скриншот выше показывает простую HTML‑страницу, преобразованную в чистый PDF.*

## Итоги и дальше

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создание PDF из HTML — пошаговое руководство C#](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)
- [Конвертация HTML в PDF в .NET с Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Создание HTML‑документа со стилизованным текстом и экспорт в PDF — полное руководство](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}