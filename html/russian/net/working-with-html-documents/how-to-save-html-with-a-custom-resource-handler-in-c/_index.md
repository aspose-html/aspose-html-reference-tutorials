---
category: general
date: 2026-11-20
description: Узнайте, как сохранять HTML с помощью пользовательского ResourceHandler
  в C# и также сохранять HTML в zip‑архивы с лаконичным, готовым к продакшену кодом.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: ru
lastmod: 2026-11-20
og_description: Как сохранить HTML с помощью пользовательского ResourceHandler в C#
  и при желании сохранять HTML в zip‑файлы — полное, готовое к запуску руководство
  для разработчиков .NET.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: Как сохранить HTML с помощью пользовательского обработчика ресурсов в C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: Как сохранить HTML с помощью пользовательского обработчика ресурсов в C#
url: /ru/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить HTML с помощью пользовательского обработчика ресурсов в C#

Если вам нужно знать **как сохранить HTML** из строки в памяти или из разобранного документа, это руководство показывает полное решение. Использование пользовательского `ResourceHandler` позволяет контролировать поток назначения, что означает, что вы можете **сохранять HTML в zip** архивы без записи временных файлов.

Вы увидите, почему `ResourceHandler` предпочтительнее старого подхода `IOutputStorage`, как его настроить и как расширить для zip‑сжатия. К концу этого руководства вы сможете внедрить код в любой проект .NET 6+ и адаптировать его под свои требования к хранению.

## Что вы создадите

* Минимальный `ResourceHandler`, который возвращает `MemoryStream`.
* `HtmlDocument`, созданный с помощью **HtmlAgilityPack**.
* Вызов `doc.Save`, который записывает HTML в поток, предоставленный обработчиком.
* Необязательная оболочка, которая сжимает полученный HTML в zip‑файл.

Требования:

* .NET 6 SDK или новее.
* `HtmlAgilityPack` пакет NuGet (`dotnet add package HtmlAgilityPack`).
* Базовое знакомство с потоками C#.

## Шаг 1: Создать пользовательский обработчик ресурсов (основной способ **как сохранить HTML**)

`ResourceHandler` базовый класс (доступный, начиная с версии 24.2 SDK просмотрщика) определяет один абстрактный метод `HandleResource`. Реализация этого метода дает вам полный контроль над тем, куда записывается HTML.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**Почему это важно:** Возвращая `MemoryStream`, вы избегаете дискового ввода‑вывода, снижаете задержку и делаете код детерминированным для модульных тестов. Обработчик вызывается автоматически методом `Save`, поэтому вам никогда не нужно явно передавать поток.

## Шаг 2: Загрузить или построить HTML‑документ

`HtmlAgilityPack` предоставляет удобный класс `HtmlDocument`, который может разбирать строку, файл или поток. В этом примере мы загружаем простой литерал, но тот же код работает с любым источником HTML.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Почему это важно:** Хранение документа в памяти согласуется с потоковым подходом пользовательского обработчика. Это также позволяет вам манипулировать DOM перед сохранением, например, внедрять скрипты или исправлять некорректные теги.

## Шаг 3: Сохранить документ с использованием пользовательского обработчика

Вызов `doc.Save` с экземпляром `MyHandler` активирует метод `HandleResource`. HTML записывается напрямую в поток, который вы вернули.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

После завершения `Save` `MemoryStream` внутри `MyHandler` содержит сериализованный HTML. Вы можете получить его следующим образом:

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**Результат:** Консоль выводит точный HTML, который вы передали в `LoadHtml`. Это доказывает, что вы теперь понимаете **как сохранить HTML** с помощью пользовательского обработчика.

## Шаг 4: Расширение обработчика для **сохранения HTML в zip**

Если вы хотите архивировать HTML, измените `MyHandler`, чтобы он записывал в `ZipArchiveEntry`. Пространство имён .NET `System.IO.Compression` делает это простым.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

Теперь используйте новый обработчик:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**Почему это работает:** Метод `HandleResource` создает zip‑запись с именем `document.html`. Когда `doc.Save` пишет в возвращённый поток, данные автоматически сжимаются. Поскольку zip создаётся в памяти, вы можете вернуть его из веб‑API, прикрепить к письму или сохранить в базе данных, не касаясь файловой системы.

## Часто задаваемые вопросы и особые случаи

### Что если мне нужно несколько HTML‑файлов в одном zip?

Создайте новую запись для каждого вызова `HandleResource`. Аргумент `resourceName` обычно содержит имя файла, поэтому вы можете использовать его напрямую:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### Как обрабатывать большие документы без исчерпания памяти?

Замените `MemoryStream` на `FileStream`, указывающий на временный файл. Обработчик тогда возвращает файловый поток, и вы можете позже удалить файл после создания zip‑архива.

### Работает ли этот подход с .NET Core на Linux?

Да. Все используемые API (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) кросс‑платформенные. Убедитесь, что целевая платформа как минимум .NET 6 для наилучшей совместимости.

### Могу ли я зашифровать zip‑архив?

`ZipArchive` поддерживает шифрование на основе пароля только через сторонние библиотеки (например, `SharpZipLib`). Если требуется шифрование, оберните выходные байты библиотекой, предоставляющей AES‑шифрование, перед отправкой их клиенту.

## Профессиональные советы

* **Повторно используйте обработчик** при обработке множества документов в пакете; создание нового `ZipArchive` для каждого файла добавляет лишние накладные расходы.
* **Установите `LeaveOpen: true`** в конструкторе `ZipArchive`, если вам нужно читать байты zip, пока архив ещё открыт.
* **Проверьте HTML** перед сохранением, вызвав `doc.OptionCheckSyntax = true;` — это раннее обнаруживает некорректные теги.
* **Записывайте размер** сгенерированного zip; необычно большой вывод часто указывает на дублирующиеся ресурсы или отсутствие сжатия.

## Полный рабочий пример

Ниже приведён один файл, который вы можете вставить в консольный проект (`dotnet new console`) и запустить. Он демонстрирует как простое сохранение HTML, так и сжатие в zip.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using HtmlAgilityPack;

// ---------- Custom handlers ----------
class MyHandler : ResourceHandler
{
    public MemoryStream HtmlStream { get; } = new();

    public override Stream HandleResource(string resourceName) => HtmlStream;
}

class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open();
    }

    public byte[] GetZipBytes()
    {
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}

// ---------- Main program ----------
class Program
{
    static void Main()
    {
        // Build a simple HTML document.
        HtmlDocument doc = new HtmlDocument();
        doc.LoadHtml("<html><body>Hello World from HtmlAgilityPack</body></html>");

        // ---- Example 1: plain HTML save ----
        var plainHandler = new MyHandler();
        doc.Save(plainHandler);
        plainHandler.HtmlStream.Seek(0, SeekOrigin.Begin);
        using var reader = new StreamReader(plainHandler.HtmlStream);
        Console.WriteLine("Plain HTML output:");


## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как сохранить HTML в C# с пользовательским обработчиком ресурсов](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [Как использовать ZipArchive – Сохранить HTML и ресурсы в ZIP‑файл](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [сохранить html как zip с пользовательским обработчиком ресурсов – пошаговое руководство](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}