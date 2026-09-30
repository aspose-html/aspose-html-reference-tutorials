---
category: general
date: 2026-02-13
description: Узнайте, как создать пользовательский обработчик ресурсов на C# для преобразования
  HTML в ZIP‑архив, создавая zip‑файл в памяти с помощью Aspose.HTML — пошаговое руководство.
draft: false
keywords:
- custom resource handler
- convert html zip archive
- create zip from memory
- Aspose HTML
- in‑memory streaming
- C# zip compression
language: ru
og_description: Узнайте полное решение на C# по использованию пользовательского обработчика
  ресурсов для преобразования HTML в ZIP‑архив непосредственно в памяти.
og_title: Пользовательский обработчик ресурсов – Преобразование HTML в ZIP из памяти
tags:
- C#
- Aspose.HTML
- ZipArchive
- MemoryStream
title: Пользовательский обработчик ресурсов в C# – Преобразование HTML в ZIP‑архив
  из памяти
url: /ru/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-archive-fro/
---

we keep spaces.

Make sure we keep code block placeholders unchanged.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пользовательский обработчик ресурсов – Преобразование HTML в ZIP‑архив из памяти

Когда‑нибудь вам нужен был **custom resource handler**, чтобы собрать каждое изображение, CSS‑файл или скрипт, которые загружает HTML‑страница, а затем упаковать всё в zip, не касаясь диска? Вы не одиноки. Во многих сценариях веб‑автоматизации или шаблонизации электронных писем вам нужен весь документ в виде единого, переносимого пакета, и вы предпочли бы держать всё в ОЗУ для скорости и безопасности.

В этом руководстве мы пройдем полный, исполняемый пример, который покажет, как **convert HTML zip archive** с помощью **custom resource handler** и затем **create zip from memory** с использованием `System.IO.Compression` из .NET. К концу у вас будет автономный метод, который можно добавить в любой C#‑проект, использующий Aspose.HTML.

## Что понадобится

- .NET 6+ (or .NET Framework 4.7.2+)  
- Aspose.HTML for .NET (NuGet package `Aspose.HTML`)  
- Basic familiarity with streams and the `ZipArchive` class  

Никаких внешних инструментов, никаких временных файлов, только чистая обработка в памяти.

## Шаг 1: Определите пользовательский обработчик ресурсов

Суть решения — класс, наследующий `Aspose.Html.ResourceHandler`. Его задача — предоставить новый `Stream` для каждого внешнего ресурса, запрашиваемого HTML‑движком. Возвращая новый `MemoryStream` каждый раз, мы изолируем данные и готовим их к последующей упаковке.

```csharp
using System.IO;
using Aspose.Html;

// Step 1 – Custom handler that stores resources in memory
class MemoryResourceHandler : ResourceHandler
{
    // The framework calls this method for every external resource (images, CSS, etc.)
    public override Stream HandleResource(Resource resource)
    {
        // We give the engine an empty stream; later we’ll fill it with the actual bytes.
        // Using MemoryStream means everything stays in RAM.
        return new MemoryStream();
    }
}
```

**Почему это важно:**  
Если позволить Aspose.HTML записывать ресурсы на диск, потом придётся их удалять. Обработчик в памяти устраняет накладные расходы ввода‑вывода и делает код безопасным для изолированных сред (например, Azure Functions).

## Шаг 2: Загрузите ваш HTML‑документ

Далее укажите Aspose.HTML HTML‑файл, который нужно упаковать. Документ может находиться на диске, быть URL‑адресом или даже простой строкой. Здесь для простоты используем путь к файлу.

```csharp
using Aspose.Html;

// Step 2 – Load the source HTML
HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/input.html");
```

> **Совет:** Если ваш HTML ссылается на относительные ресурсы, убедитесь, что `input.html` находится в той же папке, что и эти файлы, иначе обработчик не сможет их найти.

## Шаг 3: Подключите обработчик и сохраните в MemoryStream

Теперь мы создаём экземпляр обработчика и указываем Aspose.HTML использовать его через `HtmlSaveOptions.OutputStorage`. Полученный HTML (включая переписанные URL‑ы ресурсов) попадает в `MemoryStream`.

```csharp
using Aspose.Html.Saving;
using System.IO;

// Step 3 – Prepare the handler and an in‑memory buffer for the final HTML
var resourceHandler = new MemoryResourceHandler();

using (MemoryStream htmlMemoryStream = new MemoryStream())
{
    document.Save(htmlMemoryStream, new HtmlSaveOptions
    {
        OutputStorage = resourceHandler // redirects all resources to the handler
    });

    // At this point htmlMemoryStream contains the full HTML file,
    // while each external resource resides in the streams returned by the handler.
```

**Что происходит под капотом?**  
Когда вызывается `document.Save`, Aspose.HTML запрашивает у `MemoryResourceHandler` поток для каждого ресурса. Поскольку мы возвращаем пустые `MemoryStream`‑ы, движок записывает необработанные байты непосредственно в память. Временные файлы не создаются.

## Шаг 4: Сформируйте ZIP‑архив полностью в памяти

Теперь начинается интересная часть: мы создадим `ZipArchive`, который находится внутри другого `MemoryStream`. Это позволяет **create zip from memory** без обращения к файловой системе.

```csharp
    // Step 4 – Build the ZIP archive in memory
    using (MemoryStream zipMemoryStream = new MemoryStream())
    using (var zipArchive = new ZipArchive(zipMemoryStream, ZipArchiveMode.Create, leaveOpen: true))
    {
        // 4a – Add the main HTML file
        var htmlEntry = zipArchive.CreateEntry("index.html");
        using (var entryStream = htmlEntry.Open())
        {
            // Reset the position of the HTML stream before copying
            htmlMemoryStream.Position = 0;
            htmlMemoryStream.CopyTo(entryStream);
        }

        // 4b – Add each resource that the handler captured
        // The handler stored each resource in a fresh MemoryStream, which we can enumerate.
        // For demonstration, assume we kept a list of those streams (you could store them in a dictionary).
        // Example placeholder – replace with your actual collection:
        // foreach (var kvp in capturedResources)
        // {
        //     var resourceEntry = zipArchive.CreateEntry(kvp.Key); // kvp.Key = relative path
        //     using var entry = resourceEntry.Open();
        //     kvp.Value.Position = 0;
        //     kvp.Value.CopyTo(entry);
        // }

        // When we’re done, flush everything
        zipArchive.Dispose(); // optional because of using, but makes intent clear
    }

    // At this stage zipMemoryStream holds the complete ZIP file.
    // You can return it, write it to a response stream, or save it to disk if you wish.
}
```

> **Примечание:** Закомментированный фрагмент показывает, как можно собрать потоки внутри `MemoryResourceHandler`. В продакшн‑сценарии вы бы сохраняли каждый `MemoryStream` в словарь, ключом которого является исходный URL ресурса, а затем проходили бы их здесь, чтобы добавить в архив.

**Зачем хранить ZIP в памяти?**  
Хранение архива в `MemoryStream` упрощает отправку его напрямую HTTP‑клиенту (`FileResult` в ASP.NET Core) или загрузку в облачное хранилище без промежуточного файла.

## Шаг 5: (Опционально) Сохраните ZIP на диск

Если всё же нужен физический файл — возможно для отладки — просто запишите `zipMemoryStream` на диск:

```csharp
// Optional: write the in‑memory ZIP to a file for inspection
File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipMemoryStream.ToArray());
```

## Полный рабочий пример

Собрав всё вместе, представляем готовую к копированию программу, которая **converts HTML to a ZIP archive** полностью в памяти.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class MemoryResourceHandler : ResourceHandler
{
    // Capture each resource in a dictionary for later retrieval
    public static readonly System.Collections.Generic.Dictionary<string, MemoryStream> Captured = new();

    public override Stream HandleResource(Resource resource)
    {
        var ms = new MemoryStream();
        // Store the stream using the resource's absolute URL as the key
        Captured[resource.Uri.AbsoluteUri] = ms;
        return ms;
    }
}

class Program
{
    static void Main()
    {
        // Load the HTML file
        HtmlDocument doc = new HtmlDocument("YOUR_DIRECTORY/input.html");

        // Attach the custom handler
        var handler = new MemoryResourceHandler();

        // Save HTML + resources to memory
        using var htmlStream = new MemoryStream();
        doc.Save(htmlStream, new HtmlSaveOptions { OutputStorage = handler });

        // Create the ZIP archive in memory
        using var zipStream = new MemoryStream();
        using (var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            // Add the HTML file
            var htmlEntry = zip.CreateEntry("index.html");
            using (var entry = htmlEntry.Open())
            {
                htmlStream.Position = 0;
                htmlStream.CopyTo(entry);
            }

            // Add each captured resource
            foreach (var kvp in MemoryResourceHandler.Captured)
            {
                // Derive a sane relative path from the URL
                var uri = new Uri(kvp.Key);
                var relativePath = uri.AbsolutePath.TrimStart('/');
                var resEntry = zip.CreateEntry(relativePath);
                using var entry = resEntry.Open();
                kvp.Value.Position = 0;
                kvp.Value.CopyTo(entry);
            }
        }

        // The ZIP is ready – write it out or return it from a web API
        File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipStream.ToArray());

        Console.WriteLine("HTML successfully packaged into output.zip");
    }
}
```

### Ожидаемый результат

Запуск программы создаёт `output.zip`, содержащий:

- `index.html` – переписанный HTML, указывающий на упакованные ресурсы.  
- Все изображения, CSS‑ и JavaScript‑файлы, на которые ссылается оригинальная страница, сохранённые с их исходными относительными путями.

Откройте `index.html` из ZIP в любом браузере, и вы увидите страницу, отрисованную точно так же, как когда она находилась в файловой системе.

## Часто задаваемые вопросы и особые случаи

| Question | Answer |
|----------|--------|
| **Что если ресурс огромный (например, видео)?** | Поскольку всё хранится в памяти, очень большие файлы могут вызвать `OutOfMemoryException`. В таком случае поток следует направлять напрямую во временный файл или ограничить принимаемый размер. |
| **Нужно ли обрабатывать дублирующиеся URL‑ы ресурсов?** | Словарь обработчика перезапишет дубликаты. Если нужно оставить только одну копию, проверяйте `Captured.ContainsKey` перед добавлением. |
| **Можно ли использовать это в контроллере ASP.NET Core?** | Конечно. Верните `File(zipStream.ToArray(), "application/zip", "page.zip")` из метода действия. |
| **А как насчёт HTTPS‑ресурсов?** | Aspose.HTML загрузит их автоматически, пока среда доверяет SSL‑сертификату. Для самоподписанных сертификатов настройте `ServicePointManager.ServerCertificateValidationCallback`. |
| **Является ли пользовательский обработчик потокобезопасным?** | В примере используется статический словарь, который *не* потокобезопасен. Оберните доступы в lock или используйте `ConcurrentDictionary`, если планируете обрабатывать много документов одновременно. |

## Советы для продакшн‑использования

- **Reuse the handler** только для одного документа; создавайте новый экземпляр для каждого запроса, чтобы избежать перекрестного доступа между пользователями.  
- **Dispose streams** своевременно. Хотя блоки `using` покрывают большинство случаев, любые потоки, хранящиеся в словаре, следует освобождать после создания ZIP.  
- **Validate the HTML** перед обработкой, чтобы отловить некорректную разметку, которая может заставить обработчик запрашивать неожиданные ресурсы.  
- **Compress aggressively** задав `ZipArchiveEntry.CompressionLevel = CompressionLevel.Optimal`, если важен размер файла.  

## Заключение

Мы рассмотрели всё, что нужно, чтобы **custom resource handler** пройтись по HTML‑странице, захватить каждый связанный ресурс и **create zip from memory** без обращения к диску. Показанный шаблон достаточно гибок для веб‑сервисов, фоновых задач или даже настольных утилит, которым требуется поставлять автономный HTML‑пакет.

Попробуйте — замените `YOUR_DIRECTORY/input.html` любой страницей, настройте обработчик для хранения ресурсов в `ConcurrentDictionary`, и у вас будет надёжный конвейер HTML‑в‑ZIP в памяти, готовый к продакшн.

---

*Готовы к следующему уровню?* Далее изучите, как **convert HTML to PDF** с помощью Aspose.HTML, или поэкспериментируйте с шифрованием ZIP для дополнительной безопасности. Возможности безграничны, когда вы освоите потоковую обработку в памяти в C#. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}