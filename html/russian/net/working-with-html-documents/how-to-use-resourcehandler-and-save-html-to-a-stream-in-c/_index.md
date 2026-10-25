---
category: general
date: 2026-10-25
description: Как использовать ResourceHandler для контроля загрузки ресурсов и как
  сохранить HTML в поток с помощью Aspose.HTML на C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use resourcehandler
- how to save html to stream
- Aspose.HTML ResourceHandler
- HTML to MemoryStream C#
- custom resource handling C#
language: ru
lastmod: 2026-10-25
og_description: Как использовать ResourceHandler для контроля загрузки ресурсов и
  как сохранить HTML в поток с помощью Aspose.HTML для .NET.
og_image_alt: Screenshot of C# code using ResourceHandler to save HTML to a memory
  stream
og_title: Как использовать ResourceHandler и сохранять HTML в поток в C#
schemas:
- author: Aspose
  dateModified: '2026-10-25'
  description: How to use ResourceHandler to control resource loading and how to save
    HTML to a stream using Aspose.HTML in C#.
  headline: How to use ResourceHandler and save HTML to a stream in C#
  type: TechArticle
- description: How to use ResourceHandler to control resource loading and how to save
    HTML to a stream using Aspose.HTML in C#.
  name: How to use ResourceHandler and save HTML to a stream in C#
  steps:
  - name: Expected output
    text: 'Running the code above prints:'
  - name: 1. Embedding real resources
    text: 'If you need to embed an image, modify `MyHandler` to return a stream that
      contains the image bytes:'
  - name: 2. Handling large documents
    text: For very large HTML files, consider using `BufferedStream` or writing directly
      to a file‑based `FileStream` if memory becomes a bottleneck. The pattern for
      **how to save HTML to a stream** stays the same; only the stream type changes.
  - name: 3. Thread safety
    text: '`ResourceHandler` instances are **not** guaranteed to be thread‑safe. If
      you plan to reuse a handler across parallel conversions, either:'
  - name: 4. Disposing resources
    text: Both `HTMLDocument` and any streams you create implement `IDisposable`.
      Wrapping them in `using` blocks, as shown in Step 4, guarantees clean release
      of unmanaged resources.
  - name: What’s next?
    text: '* **Embed real images or CSS** by extending `MyHandler` (see the “Embedding
      real resources” section). * **Convert the stream to PDF** with `HtmlConverter.ConvertHtml`
      if you need a printable version. * **Stream the result directly from a Web API**
      using `FileStreamResult` or `MemoryStream` in ASP.NE'
  type: HowTo
tags:
- Aspose.HTML
- C#
- Stream handling
title: Как использовать ResourceHandler и сохранять HTML в поток в C#
url: /ru/net/working-with-html-documents/how-to-use-resourcehandler-and-save-html-to-a-stream-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать ResourceHandler и сохранять HTML в поток в C#

Если вам нужно **how to use ResourceHandler** при рендеринге HTML с помощью Aspose.HTML, это руководство покажет вам полное готовое решение. Вы также узнаете **how to save HTML to a stream**, чтобы можно было передать результат без обращения к файловой системе.

Работа с HTML в памяти часто требуется при генерации писем, ответов API или PDF «на лету». К концу этого руководства у вас будет автономная программа на C#, которая создаёт `HTMLDocument`, предоставляет пользовательский `ResourceHandler` и записывает результат в `MemoryStream`.

## Prerequisites

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 или новее (код также работает с .NET Core 3.1 и .NET Framework 4.7+)
* Пакет NuGet **Aspose.HTML for .NET**  
  ```bash
  dotnet add package Aspose.HTML
  ```
* Базовое понимание async/await в C# (необязательно, но полезно)

## What the tutorial covers

* Как **how to use ResourceHandler** для перехвата запросов к изображениям, CSS или скриптам
* Как настроить `HtmlSaveOptions` с пользовательским обработчиком
* Как **how to save HTML to a stream** с использованием `MemoryStream`
* Обработка граничных случаев, таких как отсутствие ресурсов и освобождение потока
* Советы по расширению обработчика для последующего внедрения реальных ресурсов

## Step 1: Create a simple HTML document from a string

Первый шаг — создать `HTMLDocument` из сырого HTML. Этот объект представляет дерево DOM, которое будет рендерить Aspose.HTML.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using System.IO;

// Simple HTML markup – you can replace this with any valid HTML string.
string htmlContent = "<html><body>Hello World</body></html>";

// The HTMLDocument constructor parses the string into a DOM.
HTMLDocument document = new HTMLDocument(htmlContent);
```

> **Why this matters:** Создание документа из строки сохраняет весь процесс в памяти, что особенно важно, когда позже вы **how to save HTML to a stream** без обращения к диску.

## Step 2: Implement a custom ResourceHandler

`ResourceHandler` — это точка входа, которую Aspose.HTML использует каждый раз, когда нужен внешний ресурс (изображения, CSS, шрифты и т.д.). Переопределяя `HandleResource`, вы решаете, какой поток возвращать для каждого запроса.

```csharp
// Define a handler that supplies an empty stream for every resource request.
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(Resource resource)
    {
        // Returning an empty MemoryStream effectively disables external resources.
        // You could return a real image stream here if you need to embed assets.
        return new MemoryStream();
    }
}

// Instantiate the handler so it can be attached to the save options.
MyHandler customHandler = new MyHandler();
```

> **Why you might need this:** При генерации HTML для писем или ответов API часто не нужны внешние запросы. Подача пустых потоков предотвращает ошибки 404 и ускоряет рендеринг. Это демонстрирует **how to use ResourceHandler** для «безресурсного» вывода.

## Step 3: Configure HtmlSaveOptions to use the custom handler

`HtmlSaveOptions` позволяет управлять процессом сохранения. Присвойте свойству `ResourceHandler` вашу пользовательскую реализацию.

```csharp
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Attach the handler so every resource request goes through MyHandler.
    ResourceHandler = customHandler
};
```

> **Tip:** Если позже понадобится внедрить CSS или изображения, замените `MyHandler` на версию, которая возвращает соответствующие потоки на основе `resource.Uri`.

## Step 4: Save the document to a MemoryStream

Теперь у вас есть всё, что нужно для **how to save HTML to a stream**. Использование `MemoryStream` сохраняет вывод в ОЗУ, что упрощает передачу по HTTP, хранение в базе данных или передачу другому API.

```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    // The Save method writes the HTML (and any referenced resources) into the stream.
    document.Save(outputStream, saveOptions);

    // Reset the position so callers can read from the beginning.
    outputStream.Position = 0;

    // Example: Convert the stream to a string for debugging.
    using (StreamReader reader = new StreamReader(outputStream))
    {
        string resultHtml = reader.ReadToEnd();
        System.Console.WriteLine(resultHtml);
    }

    // At this point, outputStream can be returned from a web API, attached to an email,
    // or passed to another component without ever touching the file system.
}
```

### Expected output

Выполнение приведённого кода выводит:

```html
<html><head></head><body>Hello World</body></html>
```

Поскольку пользовательский обработчик возвращает пустые потоки, внешние теги `<link>` и `<img>` не разрешаются, и HTML остаётся чистым.

## Common variations and edge cases

### 1. Embedding real resources

Если необходимо внедрить изображение, измените `MyHandler`, чтобы он возвращал поток, содержащий байты изображения:

```csharp
public override Stream HandleResource(Resource resource)
{
    if (resource.Uri.EndsWith(".png"))
    {
        // Load the PNG from embedded resources or a database.
        byte[] imageBytes = File.ReadAllBytes("logo.png");
        return new MemoryStream(imageBytes);
    }
    return new MemoryStream(); // Fallback for other resources.
}
```

### 2. Handling large documents

Для очень больших HTML‑файлов рассмотрите использование `BufferedStream` или запись напрямую в файловый `FileStream`, если память становится узким местом. Схема **how to save HTML to a stream** остаётся той же; меняется только тип потока.

### 3. Thread safety

Экземпляры `ResourceHandler` **не** гарантируют потокобезопасность. Если планируется повторное использование обработчика в параллельных конверсиях, выбирайте один из вариантов:

* Создавать новый обработчик для каждой конверсии, или
* Защищать общий статус внутри `HandleResource` с помощью блокировок.

### 4. Disposing resources

И `HTMLDocument`, и любые создаваемые потоки реализуют `IDisposable`. Оборачивание их в блоки `using`, как показано в Шаге 4, гарантирует корректное освобождение неуправляемых ресурсов.

## Pro tip: Re‑using the same MemoryStream

Если нужно объединить несколько HTML‑выводов в один поток, сбрасывайте позицию перед каждым вызовом `Save`:

```csharp
outputStream.Position = 0; // Clear previous content
document.Save(outputStream, saveOptions);
```

Либо создавайте новый `MemoryStream` для каждой конверсии, чтобы избежать случайного смешения данных.

## Full working example

Ниже представлена полная программа, которую можно скопировать и вставить в консольное приложение. Она компилируется с .NET 6.0 и Aspose.HTML 23.9 (или новее).

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using System;
using System.IO;

namespace ResourceHandlerDemo
{
    // Custom handler that supplies empty streams for any requested resource.
    class MyHandler : ResourceHandler
    {
        public override Stream HandleResource(Resource resource)
        {
            // Return an empty stream to suppress external resources.
            return new MemoryStream();
        }
    }

    class Program
    {
        static void Main()
        {
            // Step 1: Create the HTML document.
            string htmlContent = "<html><body>Hello World</body></html>";
            HTMLDocument document = new HTMLDocument(htmlContent);

            // Step 2: Attach the custom ResourceHandler.
            MyHandler customHandler = new MyHandler();

            // Step 3: Configure save options.
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                ResourceHandler = customHandler
            };

            // Step 4: Save to a MemoryStream.
            using (MemoryStream outputStream = new MemoryStream())
            {
                document.Save(outputStream, saveOptions);
                outputStream.Position = 0;

                // Display the generated HTML for verification.
                using (StreamReader reader = new StreamReader(outputStream))
                {
                    string resultHtml = reader.ReadToEnd();
                    Console.WriteLine("Generated HTML:");
                    Console.WriteLine(resultHtml);
                }
            }
        }
    }
}
```

Запустите программу, и вы увидите сгенерированный HTML, выведенный в консоль, что подтверждает корректную работу **how to use ResourceHandler** и **how to save HTML to a stream** вместе.

## Conclusion

В этом руководстве продемонстрировано, как **how to use ResourceHandler** для управления загрузкой внешних ресурсов и как **how to save HTML to a stream** с помощью Aspose.HTML в C#. Теперь у вас есть переиспользуемый шаблон для генерации HTML в памяти, что идеально подходит для веб‑API, шаблонов писем и конвейеров конвертации в PDF.

### What’s next?

* **Embed real images or CSS** расширив `MyHandler` (см. раздел «Embedding real resources»).
* **Convert the stream to PDF** с помощью `HtmlConverter.ConvertHtml`, если нужен печатный вариант.
* **Stream the result directly from a Web API** используя `FileStreamResult` или `MemoryStream` в ASP.NET.

## What Should You Learn Next?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Save HTML in C# with Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [how to use handler in Aspose.HTML – Load HTML, Save as ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-handler-in-aspose-html-load-html-save-as-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}