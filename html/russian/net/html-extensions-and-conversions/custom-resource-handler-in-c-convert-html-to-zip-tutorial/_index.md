---
category: general
date: 2026-02-10
description: Пользовательский обработчик ресурсов позволяет конвертировать HTML в
  ZIP на C#. Узнайте, как сохранять HTML в виде zip и эффективно передавать HTML‑ресурсы
  в поток.
draft: false
keywords:
- custom resource handler
- convert html to zip
- save html as zip
- create zip with html
- stream html resources
language: ru
og_description: Пользовательский обработчик ресурсов позволяет конвертировать HTML
  в ZIP на C#. Следуйте этому пошаговому руководству, чтобы сохранить HTML в виде
  zip и передавать HTML‑ресурсы в поток.
og_title: Пользовательский обработчик ресурсов в C# — Преобразование HTML в ZIP
tags:
- Aspose.HTML
- C#
- ZIP archive
- file streaming
title: Пользовательский обработчик ресурсов в C# — учебник по конвертации HTML в ZIP
url: /ru/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пользовательский обработчик ресурсов – Преобразование HTML в ZIP на C#

Когда‑нибудь задумывались, как **custom resource handler** превратить сырой HTML сразу в ZIP‑файл? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно собрать страницу HTML вместе с её ресурсами, не оставляя временных файлов на диске. Хорошая новость? С Aspose.HTML вы можете сделать всё в памяти, а ключ к этому — пользовательский обработчик ресурсов.

В этом руководстве мы пройдём полный, исполняемый пример, показывающий, как **convert HTML to ZIP**, **save HTML as ZIP** и **stream HTML resources** «на лету». К концу у вас будет один метод, принимающий строку HTML и выдающий готовый к загрузке `result.zip`, содержащий страницу и все связанные ресурсы.

> **Требования** – .NET 6+ (or .NET Framework 4.6+), Aspose.HTML for .NET installed, and a basic understanding of streams. No external tools required.

---

## Пользовательский обработчик ресурсов – Основная концепция

Объект *resource handler* в Aspose.HTML определяет, **куда** попадает каждая часть документа — в файл на диске, в буфер памяти или, как мы покажем, в запись внутри ZIP‑архива. Наследуясь от `ResourceHandler`, вы получаете полный контроль над местом вывода основного HTML‑файла **и** всех вспомогательных ресурсов (CSS, изображения, шрифты и т.д.).

Считайте его дорожным полицейским для ресурсов вашего документа: метод `HandleResource` предоставляет вам `Stream` для основного HTML, а событие `ResourceSaving` позволяет перехватить каждый зависимый файл непосредственно перед записью.

---

## Шаг 1: Реализация пользовательского обработчика ресурсов

Сначала создайте класс, наследующий `ResourceHandler`. Мы переопределим `HandleResource`, чтобы предоставить Aspose новый `MemoryStream` для вывода основного HTML. Для связанных ресурсов позже подключим `ResourceSaving`.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System.IO;

/// <summary>
/// Supplies a stream for every resource the HTML document needs to save.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a new stream for the main HTML content.
    /// </summary>
    public override Stream HandleResource(ResourceInfo info)
    {
        // In real life you might return a FileStream or a ZipEntry stream.
        // Here we just hand back a clean MemoryStream.
        return new MemoryStream();
    }
}
```

**Why this matters:** Возврат нового `MemoryStream` означает, что HTML никогда не записывается на файловую систему. Это основа для чистого создания ZIP‑файла полностью в памяти.

---

## Шаг 2: Сохранение HTML в один MemoryStream

Теперь, когда у нас есть обработчик, мы можем создать HTML‑документ и полностью захватить его в памяти. Этот шаг необязателен, если нужен только ZIP, но он демонстрирует работу обработчика в изоляции.

```csharp
using Aspose.Html;

// Sample HTML – replace with your own markup or load from a file.
string htmlContent = "<html><head><title>Demo</title></head><body>Hello world!</body></html>";

// Create the document from a string.
HTMLDocument htmlDocument = new HTMLDocument(htmlContent);

// Instantiate our custom handler.
MyHandler memoryHandler = new MyHandler();

using (MemoryStream htmlStream = new MemoryStream())
{
    // Save triggers HandleResource and writes the HTML into htmlStream.
    htmlDocument.Save(htmlStream, memoryHandler);

    // Reset position for potential reading.
    htmlStream.Position = 0;

    // For demo purposes, dump the HTML to console.
    using (StreamReader reader = new StreamReader(htmlStream))
    {
        Console.WriteLine("Generated HTML:");
        Console.WriteLine(reader.ReadToEnd());
    }
}
```

**Ожидаемый вывод** (formatted for readability):

```
Generated HTML:
<html><head><title>Demo</title></head><body>Hello world!</body></html>
```

Если запустить этот фрагмент, вы увидите, что HTML существует только в ОЗУ — никаких временных файлов не создаётся.

---

## Шаг 3: Упаковка HTML и ресурсов в ZIP‑архив

Теперь наступает самая интересная часть: объединение HTML **и** всех связанных ресурсов в ZIP‑файл без записи промежуточных файлов на диск. Мы используем `System.IO.Compression.ZipArchive` совместно с событием `ResourceSaving`.

```csharp
using Aspose.Html;
using System.IO;
using System.IO.Compression;

// Re‑use the same HTMLDocument from the previous step.
HTMLDocument htmlDocument = new HTMLDocument("<html><body>Hello world!</body></html>");

// Path where the final ZIP will be written.
string zipPath = Path.Combine(Environment.CurrentDirectory, "result.zip");

// Open a FileStream for the ZIP file.
using (FileStream zipFile = new FileStream(zipPath, FileMode.Create))
using (ZipArchive zipArchive = new ZipArchive(zipFile, ZipArchiveMode.Update))
{
    // Create a fresh handler for the ZIP operation.
    MyHandler zipHandler = new MyHandler();

    // Hook the ResourceSaving event – this fires for every resource.
    zipHandler.ResourceSaving += (sender, e) =>
    {
        // Ensure we don't create leading folder entries like "/css/style.css".
        string entryName = e.ResourceInfo.Path.TrimStart('/');

        // Create a new entry inside the ZIP.
        ZipArchiveEntry entry = zipArchive.CreateEntry(entryName);

        // Provide the stream that Aspose will write into.
        e.Stream = entry.Open();
    };

    // Save the document; the handler will fill the ZIP for us.
    htmlDocument.Save(zipHandler);
}

// Verify the ZIP exists.
Console.WriteLine($"ZIP created at: {zipPath}");
```

### Что происходит за кулисами?

1. **`ResourceSaving` fires** для основного HTML‑файла и каждого связанного ресурса.
2. Наша лямбда‑функция создаёт соответствующую запись (`CreateEntry`) внутри открытого ZIP.
3. Присваивая `e.Stream = entry.Open()`, мы передаём Aspose поток для записи, который пишет непосредственно в запись ZIP.
4. После завершения `htmlDocument.Save` ZIP содержит полностью сформированную HTML‑страницу и все CSS, изображения или шрифты, указанные в разметке.

**Result:** Один файл `result.zip`, который можно отдать браузерам, прикрепить к письмам или сохранить в blob‑хранилище — без оставшихся временных файлов.

---

## Бонус: Использование ZIP в Web API

Если вы создаёте конечную точку ASP.NET Core, возвращающую ZIP по запросу, применяется тот же принцип. Ниже компактный метод контроллера:

```csharp
[ApiController]
[Route("api/[controller]")]
public class HtmlZipController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult DownloadZip()
    {
        // Build the document (could be loaded from a DB, etc.).
        var html = "<html><body><h1>Dynamic report</h1></body></html>";
        var doc = new HTMLDocument(html);
        var handler = new MyHandler();

        // Prepare an in‑memory ZIP.
        using var zipStream = new MemoryStream();
        using (var archive = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            handler.ResourceSaving += (s, e) =>
            {
                var entry = archive.CreateEntry(e.ResourceInfo.Path.TrimStart('/'));
                e.Stream = entry.Open();
            };
            doc.Save(handler);
        }

        zipStream.Position = 0;
        return File(zipStream, "application/zip", "report.zip");
    }
}
```

Теперь GET‑запрос к `/api/HtmlZip/download` передаёт сгенерированный zip напрямую клиенту — идеально для отчётов «на лету».

---

## Распространённые ошибки и профессиональные советы

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Пустые папки в ZIP** | `ResourceInfo.Path` начинается с `/`, вызывая запись вида `/` | Используйте `TrimStart('/')`, как показано в обработчике события. |
| **Отсутствующие изображения** | Изображения, указанные абсолютными URL, не загружаются автоматически | Установите `htmlDocument.Options.ResourceLoading = ResourceLoadingMode.Stream` и предоставьте пользовательский `ResourceHandler`, который загружает удалённые ресурсы. |
| **Большие файлы вызывают нагрузку на память** | Все потоки удерживаются в памяти до закрытия ZIP | Переключите `ZipArchiveMode.Update` на `Create` и записывайте каждую запись напрямую без буферизации, либо используйте поток с диска, если размер превышает ОЗУ. |
| **Исключение “The stream does not support seeking”** | Попытка повторного использования не‑перемещаемого потока для нескольких ресурсов | Всегда предоставляйте новый `MemoryStream` или `entry.Open()` для каждого ресурса. |

---

## Заключение

Мы только что показали, как **custom resource handler** позволяет **convert HTML to ZIP**, **save HTML as ZIP** и **stream HTML resources** без обращения к файловой системе. Переопределяя `HandleResource` и используя `ResourceSaving`, вы получаете детальный контроль над каждым байтом, выходящим из Aspose.HTML.

Эта схема масштабируется: замените in‑memory `MemoryStream` на поток облачного блоба, добавьте настройки сжатия или подключите слой логирования для аудита упакованных ресурсов. Возможности безграничны, когда вы контролируете конвейер ресурсов.

Готовы к следующему шагу? Попробуйте внедрить CSS и изображения в ваш HTML, поэкспериментируйте с загрузкой удалённых ресурсов или интегрируйте этот процесс в Azure Function, возвращающую ZIP по запросу. Приятного кодинга!

*Изображение, иллюстрирующее процесс работы пользовательского обработчика ресурсов, преобразующего HTML в ZIP‑файл.*

![процесс работы пользовательского обработчика ресурсов](https://example.com/placeholder-image.png "процесс работы пользовательского обработчика ресурсов")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}