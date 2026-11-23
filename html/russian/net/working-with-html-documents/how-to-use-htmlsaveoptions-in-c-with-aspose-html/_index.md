---
category: general
date: 2026-09-10
description: Узнайте, как использовать HtmlSaveOptions в C# для управления стилями
  веб‑шрифтов и сохранения HTML‑файлов с помощью Aspose.HTML. Включён полный пример
  кода и практические советы.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use htmlsaveoptions
- Aspose HTML library
- WebFontStyle flags
- HTMLDocument conversion
- C# save HTML
- Aspose.Html SaveOptions
language: ru
lastmod: 2026-09-10
og_description: Как использовать HtmlSaveOptions в C# для включения жирных и курсивных
  стилей веб‑шрифтов при сохранении HTML с помощью Aspose.HTML. Следуйте полному примеру
  и советам по лучшим практикам.
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: Как использовать HtmlSaveOptions в C# с Aspose.HTML – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  headline: How to use HtmlSaveOptions in C# with Aspose.HTML
  type: TechArticle
- description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  name: How to use HtmlSaveOptions in C# with Aspose.HTML
  steps:
  - name: Why configure WebFontStyle?
    text: 'When you export an HTML document, Aspose.HTML can embed web fonts that
      match the original styling. By setting `WebFontStyle`, you tell the exporter
      which font variants to include. This reduces the final file size when you only
      need specific styles and guarantees that the rendered output matches the '
  - name: 5.1 Controlling CSS embedding
    text: 'You can decide whether to embed CSS inline, keep external links, or embed
      everything:'
  - name: 5.2 Saving to a specific encoding
    text: '```csharp saveOptions.Encoding = Encoding.UTF8; ```'
  - name: 5.3 Handling large documents
    text: 'For very large HTML files, consider streaming the output to avoid high
      memory consumption:'
  - name: 5.4 Error handling best practice
    text: 'Wrap the entire workflow in a try‑catch block and log the exception details.
      This ensures that any I/O or parsing errors are captured:'
  - name: Expected console output
    text: '``` HTML saved successfully to ''YOUR_DIRECTORY/output.html''. ```'
  type: HowTo
tags:
- Aspose.HTML
- C#
- HTML processing
title: Как использовать HtmlSaveOptions в C# с Aspose.HTML
url: /ru/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать HtmlSaveOptions в C# с Aspose.HTML

Если вам нужно контролировать, как Aspose.HTML сохраняет HTML‑документ, **изучение использования HtmlSaveOptions необходимо**. В этом руководстве показано шаг за шагом, как использовать HtmlSaveOptions для включения жирных и курсивных стилей веб‑шрифтов при сохранении документа.

Библиотека Aspose HTML предоставляет богатый API для загрузки, изменения и экспорта HTML‑контента. К концу этого руководства вы сможете:

* Загрузить существующий HTML‑файл в `HTMLDocument`.
* Настроить `HtmlSaveOptions` для применения конкретных флагов `WebFontStyle`.
* Сохранить изменённый документ в новое место или в поток.
* Расширить решение для других стилей шрифтов, пользовательского CSS и обработки ошибок.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 или новее установлен.
* Действующая лицензия для **Aspose.HTML for .NET** (бесплатная пробная версия подходит для этого примера).
* Visual Studio 2022 (или любая IDE для C#) для компиляции и запуска кода.

Дополнительные пакеты NuGet не требуются, кроме `Aspose.HTML`.

## Шаг 1: Настройте проект и импортируйте пространства имён

Создайте новый проект **Console App** и добавьте пакет Aspose.HTML через NuGet:

```bash
dotnet add package Aspose.HTML
```

Затем, в начале файла `Program.cs`, импортируйте необходимые пространства имён:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

Эти пространства имён предоставляют типы `HTMLDocument`, `HtmlSaveOptions` и `WebFontStyle`, которые вы будете использовать в течение всего руководства.

## Шаг 2: Загрузите исходный HTML‑документ

Первая операция — прочитать HTML, который вы хотите обработать. Замените `"YOUR_DIRECTORY/input.html"` на фактический путь к вашему файлу.

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` разбирает разметку, строит дерево DOM и готовит его к изменению. Если файл не существует, будет выброшено исключение, поэтому в продакшн‑коде рекомендуется обернуть этот вызов в блок try‑catch.

## Шаг 3: Создайте и настройте HtmlSaveOptions

`HtmlSaveOptions` позволяет точно настроить процесс сохранения. Чтобы включить жирные и курсивные стили веб‑шрифтов, объедините соответствующие флаги `WebFontStyle` с помощью побитового оператора ИЛИ (`|`).

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### Зачем настраивать WebFontStyle?

При экспорте HTML‑документа Aspose.HTML может встраивать веб‑шрифты, соответствующие оригинальному оформлению. Устанавливая `WebFontStyle`, вы указываете экспортеру, какие варианты шрифтов включать. Это уменьшает размер конечного файла, если нужны только определённые стили, и гарантирует, что отрендеренный результат будет соответствовать исходному.

#### Распространённые варианты

| Желаемый стиль | Соответствующий флаг `WebFontStyle` |
|----------------|-------------------------------------|
| Обычный (regular) | `WebFontStyle.Regular` |
| Жирный | `WebFontStyle.Bold` |
| Курсив | `WebFontStyle.Italic` |
| Жирный + Курсив | `WebFontStyle.Bold | WebFontStyle.Italic` |
| Все варианты | `WebFontStyle.All` |

Вы можете комбинировать любые варианты, подходящие для вашего сценария.

## Шаг 4: Сохраните документ с настроенными параметрами

Теперь запишите документ в новый файл. Метод `Save` принимает путь назначения и подготовленный экземпляр `HtmlSaveOptions`.

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

Если необходимо записать в поток памяти (например, для отправки файла по HTTP), используйте перегрузку, принимающую объект `Stream`:

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## Шаг 5: Проверьте результат

Откройте `output.html` в браузере или проверьте файл в текстовом редакторе. Вы должны увидеть, что блок `<style>` теперь содержит правила `@font-face` для жирных и курсивных вариантов всех веб‑шрифтов, указанных в оригинальном документе.

**Ожидаемый фрагмент вывода:**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

Если оригинальный HTML ссылался на семейство шрифтов, имеющее только обычный вес, Aspose.HTML включит только этот файл, учитывая конфигурацию `WebFontStyle`.

## Продвинутый уровень: Использование HtmlSaveOptions с дополнительными возможностями

### 5.1 Управление встраиванием CSS

Вы можете решить, встраивать ли CSS непосредственно, оставлять внешние ссылки или встраивать всё:

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 Сохранение с определённой кодировкой

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 Обработка больших документов

Для очень больших HTML‑файлов рассмотрите возможность потоковой записи вывода, чтобы избежать высокого потребления памяти:

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 Лучшие практики обработки ошибок

Обёрните весь процесс в блок try‑catch и запишите детали исключения в журнал. Это гарантирует, что любые ошибки ввода‑вывода или парсинга будут зафиксированы:

```csharp
try
{
    // Load, configure, and save as shown earlier
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error processing HTML: {ex.Message}");
}
```

## Совет профессионала: Переиспользуйте HtmlSaveOptions при множественных сохранениях

Если необходимо сохранить несколько документов с одинаковой конфигурацией стилей шрифтов, создайте один экземпляр `HtmlSaveOptions` и переиспользуйте его. Это уменьшает накладные расходы на создание объектов и гарантирует согласованный вывод.

```csharp
HtmlSaveOptions sharedOptions = new HtmlSaveOptions
{
    WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
    CssSavingMode = CssSavingMode.EmbedAllCss
};

foreach (var file in Directory.GetFiles("input_folder", "*.html"))
{
    HTMLDocument doc = new HTMLDocument(file);
    string outputPath = Path.Combine("output_folder", Path.GetFileName(file));
    doc.Save(outputPath, sharedOptions);
}
```

## Полный исполняемый пример

Ниже представлена полная программа, включающая все обсуждаемые шаги. Скопируйте её в `Program.cs` и запустите после корректировки путей к файлам.

```csharp
using System;
using System.IO;
using System.Text;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath = "YOUR_DIRECTORY/input.html";
        string outputPath = "YOUR_DIRECTORY/output.html";

        try
        {
            // Step 1: Load the source HTML document
            HTMLDocument document = new HTMLDocument(inputPath);

            // Step 2: Create HtmlSaveOptions and enable bold + italic web‑font styles
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
                // Optional: embed all CSS and use UTF‑8 encoding
                CssSavingMode = CssSavingMode.EmbedAllCss,
                Encoding = Encoding.UTF8
            };

            // Step 3: Save the document with the configured options
            document.Save(outputPath, saveOptions);

            Console.WriteLine($"HTML saved successfully to '{outputPath}'.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Ожидаемый вывод в консоль

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

Откройте сгенерированный `output.html`, чтобы убедиться, что присутствуют жирные и курсивные стили веб‑шрифтов.

## Заключение

Теперь вы знаете **как использовать HtmlSaveOptions** для управления встраиванием веб‑шрифтов, обработкой CSS и кодировкой при сохранении HTML с помощью библиотеки Aspose HTML в C#. Настраивая флаги `WebFontStyle`, вы можете адаптировать вывод, включив только необходимые варианты шрифтов, что повышает производительность и уменьшает размер файла.

Отсюда вы можете изучать другие свойства `HtmlSaveOptions`, такие как `ImageSavingMode`, `JavaScriptSavingMode`, или комбинировать несколько параметров для сложных конвейеров преобразования. Поэкспериментируйте с сохранением в потоки для веб‑API или интегрируйте процесс в более крупную систему генерации документов.

---

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающие освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [How to Save HTML with Aspose.Html – Complete C# Guide](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [How to Use Aspose to Render HTML to PNG in C#](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}