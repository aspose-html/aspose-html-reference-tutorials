---
category: general
date: 2026-03-29
description: Узнайте, как использовать ZipArchive в C# для преобразования HTML в ZIP,
  сохранения HTML в ZIP и сжатия изображений HTML — всё в одном понятном руководстве.
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: ru
og_description: Узнайте, как использовать ZipArchive в C# для преобразования HTML
  в ZIP, сохранения HTML в ZIP и сжатия изображений HTML с полным, готовым к запуску
  примером.
og_title: Как использовать ZipArchive — Сохранить HTML и ресурсы в ZIP‑файл
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: Как использовать ZipArchive – сохранить HTML и ресурсы в ZIP‑файл
url: /ru/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать ZipArchive – Сохранить HTML и ресурсы в ZIP‑файл

Задумывались ли вы **как использовать ZipArchive**, чтобы собрать HTML‑страницу вместе с её изображениями, CSS и другими ресурсами? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно отправить автономный HTML‑пакет, особенно если страница ссылается на внешние ресурсы. Хорошая новость: несколько строк кода на C# и Aspose.HTML позволяют **преобразовать HTML в ZIP**, **сохранить HTML в ZIP** и даже **сжать изображения HTML**, не выходя из IDE.

В этом руководстве мы пройдём весь процесс — от создания простого `HTMLDocument` до обработки каждого связанного ресурса через пользовательский `ResourceHandler`. К концу вы получите готовый ZIP‑файл, который можно разместить на любом веб‑сервере или отправить в виде вложения письма. Никаких внешних скриптов, никаких ручных копирований — только чистый .NET.

## Prerequisites

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

- **.NET 6+** (или .NET Framework 4.6+). Используемые API входят в `System.IO.Compression`.
- **Aspose.HTML for .NET** установлен (NuGet‑пакет `Aspose.Html`).
- Базовые знания синтаксиса C#.
- IDE, например Visual Studio или VS Code.

Это всё. Никаких дополнительных инструментов, никаких сторонних zip‑утилит. Готовы? Поехали.

## Step 1: Set Up the Project and Add Dependencies

Создайте новый консольный проект:

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

Пакет `Aspose.Html` предоставляет нам класс `HTMLDocument` и базовый класс `ResourceHandler`, который мы расширим позже. Пространство имён `System.IO.Compression` из коробки содержит `ZipArchive` и `ZipArchiveEntry`.

> **Pro tip:** Если вы нацелены на .NET 6, можете использовать top‑level statements, чтобы упростить метод `Main`. Ниже показан классический вариант с классом `Program` для наглядности.

## Step 2: Create a Custom Resource Handler

Когда Aspose.HTML сохраняет документ, он запрашивает у `ResourceHandler` поток (`Stream`) для каждого внешнего файла (изображения, CSS, шрифты и т.д.). Переопределив `HandleResource`, мы можем направлять каждый ресурс сразу в запись ZIP‑архива.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Writes each HTML resource (image, CSS, etc.) directly into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        // Ensure a folder hierarchy inside the zip (optional but tidy)
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open(); // Aspose streams the content into this entry.
    }
}
```

**Почему это важно:** Вместо того чтобы сначала записывать ресурсы на диск, а затем архивировать их, обработчик передаёт их напрямую, что уменьшает нагрузку на ввод‑вывод и гарантирует синхронность ZIP‑файла с содержимым HTML.

## Step 3: Build the HTML Document

Для демонстрации встроим небольшой HTML‑фрагмент, который ссылается на внешнее изображение `logo.png`. В реальном проекте HTML может загружаться из файла или базы данных.

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

Если вам нужно **сжать изображения HTML**, просто разместите файл изображения рядом с исполняемым файлом (или внедрите его как ресурс). `ZipResourceHandler` автоматически добавит изображение в архив.

## Step 4: Open (or Create) the ZIP File and Save

Теперь соединяем всё вместе. Открываем `FileStream` для выходного ZIP‑файла, создаём `ZipArchive` в режиме *Update* и передаём наш пользовательский обработчик в `HTMLDocument.Save`.

```csharp
using (var fileStream = new FileStream("output.zip", FileMode.Create))
using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
{
    // Initialise the handler with the open ZipArchive.
    var zipHandler = new ZipResourceHandler(zipArchive);

    // Save the HTML document; the handler writes HTML, images, CSS, etc. into the zip.
    htmlDocument.Save(zipHandler);
}
```

Когда блоки `using` завершаются, ZIP‑архив автоматически финализируется и закрывается. В получившемся `output.zip` будет:

- `index.html` (сериализованный HTML‑документ)
- `logo.png` (изображение, указанное в HTML)

Проверьте содержимое, открыв архив в любом файловом менеджере.

## Step 5: Verify the Result (Optional)

Всегда полезно убедиться, что архив действительно работает. Ниже короткий фрагмент, который можно выполнить после предыдущего кода, чтобы вывести список записей:

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

Вы должны увидеть что‑то вроде:

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

Откройте `index.html` из распакованной папки — изображение отобразится корректно, подтверждая, что **save HTML to ZIP** выполнено успешно.

## Common Variations & Edge Cases

### 1. Using a Different Entry Name for the HTML File

По умолчанию Aspose сохраняет HTML в `index.html`. Если нужен другое имя, задайте `htmlDocument.FileName` перед сохранением:

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. Adding Additional Files Manually

Иногда требуется добавить дополнительные файлы (например, README). Их можно добавить напрямую в `ZipArchive` до вызова `htmlDocument.Save`:

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. Handling Large Images Efficiently

Если ваш HTML ссылается на очень большие изображения, рекомендуется уменьшить их размер заранее, чтобы сократить размер архива. Пакет `System.Drawing.Common` может помочь:

```csharp
// Example: Resize logo.png to a max width of 800px before zipping.
using (var img = System.Drawing.Image.FromFile("logo.png"))
{
    int maxWidth = 800;
    if (img.Width > maxWidth)
    {
        var ratio = (double)maxWidth / img.Width;
        var newHeight = (int)(img.Height * ratio);
        using var thumb = img.GetThumbnailImage(maxWidth, newHeight, () => false, IntPtr.Zero);
        thumb.Save("logo_resized.png");
    }
}
```

Затем укажите в HTML `<img src='logo_resized.png'>`.

## Full, Runnable Example

Ниже полная программа, которую можно скопировать в `Program.cs`. Она компилируется и работает «из коробки», при условии, что установлен NuGet‑пакет Aspose.HTML.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Custom handler that streams each resource into a zip entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create an HTML document that references an external image.
        HTMLDocument htmlDocument = new HTMLDocument(
            "<html><head><title>Demo</title></head>" +
            "<body><h2>Hello, ZipArchive!</h2>" +
            "<img src='logo.png' alt='Demo logo'></body></html>"
        );

        // 2️⃣ Open (or create) the output zip file.
        using (var fileStream = new FileStream("output.zip", FileMode.Create))
        using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Initialise the custom handler.
            var zipHandler = new ZipResourceHandler(zipArchive);

            // 4️⃣ Save the HTML; resources get streamed into the zip.
            htmlDocument.Save(zipHandler);
        }

        Console.WriteLine("✅ HTML document and its resources have been saved to output.zip");
    }
}
```

**Ожидаемый вывод:** В консоли появится сообщение об успехе, а `output.zip` появится в папке проекта и будет содержать `index.html` и `logo.png`.

## Frequently Asked Questions

- **Does this work on .NET Core?**  
  Да. `System.IO.Compression.ZipArchive` входит в .NET Standard, поэтому тот же код работает на .NET 5, .NET 6 и .NET 7.

- **What if I need to **compress HTML images** more aggressively?**  
  Вы можете предварительно обработать изображения (изменить размер, конвертировать в WebP и т.д.) перед их добавлением в архив. Сам обработчик просто передаёт полученные данные.

- **Can I encrypt the zip?**  
  `ZipArchive` поддерживает AES‑шифрование только через сторонние библиотеки (например, `SharpZipLib`). Если требуется шифрование, создайте архив этой библиотекой, а затем передайте поток Aspose в виде пользовательского `ResourceHandler`.

- **Is there a way to set the root folder inside the zip?**  
  Да — добавьте имя папки к `resourceName` внутри `HandleResource`, например `var entry = _zipArchive.CreateEntry($"site/{resourceName}", ...)`.

## Conclusion

Теперь вы знаете **как использовать ZipArchive** в C# для **преобразования HTML в ZIP**, **сохранения HTML в ZIP** и **сжатия изображений HTML** в едином, чистом рабочем процессе. Расширив `ResourceHandler`, мы избежали создания временных файлов и сделали процесс экономным по памяти. Этот подход легко масштабируется: просто разместите полученный ZIP‑файл на веб‑сервере, отправьте его по почте или сохраните в облаке.

Дальнейшие шаги, которые стоит изучить:

- **Create ZIP archives programmatically** для целых папок сайта (`create zip archive c#`).
- **Add PDF or DOCX conversions** перед архивированием для более богатых пакетов документации.
- **Integrate with ASP.NET Core** для потоковой передачи ZIP‑файла напрямую клиенту (`FileStreamResult`).

Есть вопросы о zip‑ировании HTML, работе со шрифтами или оптимизации размеров изображений? Оставляйте комментарий или пишите мне на Stack Overflow. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}