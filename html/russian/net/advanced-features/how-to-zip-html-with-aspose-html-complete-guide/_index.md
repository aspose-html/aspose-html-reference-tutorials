---
category: general
date: 2026-03-02
description: Узнайте, как упаковать HTML в zip с помощью Aspose HTML, пользовательского
  обработчика ресурсов и .NET ZipArchive. Пошаговое руководство по созданию zip‑архива
  и встраиванию ресурсов.
draft: false
keywords:
- how to zip html
- custom resource handler
- aspose html save
- how to create zip
- how to embed resources
language: ru
og_description: Узнайте, как упаковать HTML в zip с помощью Aspose HTML, пользовательского
  обработчика ресурсов и .NET ZipArchive. Следуйте инструкциям, чтобы создать zip‑архив
  и встроить ресурсы.
og_title: Как упаковать HTML в zip с помощью Aspose HTML – Полное руководство
tags:
- Aspose.HTML
- C#
- ZIP archive
title: Как заархивировать HTML с помощью Aspose HTML – Полное руководство
url: /ru/net/advanced-features/how-to-zip-html-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как упаковать HTML в ZIP с помощью Aspose HTML – Полное руководство

Когда‑нибудь вам нужно было **упаковать HTML** вместе со всеми изображениями, CSS‑файлами и скриптами, на которые он ссылается? Возможно, вы создаёте пакет для загрузки офлайн‑справочной системы, или просто хотите разместить статический сайт в виде одного файла. В любом случае, знание **как упаковать HTML** — полезный навык в арсенале .NET‑разработчика.

В этом руководстве мы пройдём практическое решение, использующее **Aspose.HTML**, **пользовательский обработчик ресурсов** и встроенный класс `System.IO.Compression.ZipArchive`. К концу вы точно будете знать, как **сохранить** HTML‑документ в ZIP, **встроить ресурсы** и даже подправить процесс, если понадобится поддержка необычных URI.

> **Pro tip:** Тот же шаблон работает с PDF, SVG или любыми другими форматами, насыщенными веб‑ресурсами — просто замените класс Aspose.

---

## Что понадобится

- .NET 6 или новее (код также компилируется под .NET Framework)
- NuGet‑пакет **Aspose.HTML for .NET** (`Aspose.Html`)
- Базовое понимание потоков C# и ввода‑вывода файлов
- HTML‑страница, ссылающаяся на внешние ресурсы (изображения, CSS, JS)

Никакие дополнительные сторонние ZIP‑библиотеки не требуются; стандартное пространство имён `System.IO.Compression` делает всю тяжёлую работу.

---

## Шаг 1: Создать пользовательский ResourceHandler (custom resource handler)

Aspose.HTML вызывает `ResourceHandler` каждый раз, когда встречает внешнюю ссылку при сохранении. По умолчанию он пытается загрузить ресурс из интернета, но нам нужно **встроить** точные файлы, находящиеся на диске. Здесь и пригодится **пользовательский обработчик ресурсов**.

```csharp
using System;
using System.IO;
using Aspose.Html;

// Step 1 – custom handler that copies local files into the output stream
class MyResourceHandler : ResourceHandler
{
    public override void HandleResource(string uri, Stream outputStream)
    {
        // Assume uri is a local file path; adjust logic for URLs if needed
        using (var source = new FileStream(uri, FileMode.Open, FileAccess.Read))
        {
            source.CopyTo(outputStream);
        }
    }
}
```

**Почему это важно:**  
Если пропустить этот шаг, Aspose будет выполнять HTTP‑запрос для каждого `src` или `href`. Это добавит задержку, может не пройти через файрволы и подорвет цель автономного ZIP‑файла. Наш обработчик гарантирует, что именно тот файл, который есть у вас на диске, окажется внутри архива.

---

## Шаг 2: Загрузить HTML‑документ (aspose html save)

Aspose.HTML может принимать URL, путь к файлу или строку с чистым HTML. В этом примере мы загрузим удалённую страницу, но тот же код работает и с локальным файлом.

```csharp
using Aspose.Html;

// Step 2 – load the HTML document (URL, file path, or raw string)
var htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

**Что происходит под капотом?**  
Класс `HTMLDocument` парсит разметку, строит DOM и разрешает относительные URL. Когда позже вызываете `Save`, Aspose проходит по DOM, запрашивает ваш `ResourceHandler` для каждого внешнего файла и записывает всё в целевой поток.

---

## Шаг 3: Подготовить ZIP‑архив в памяти (how to create zip)

Вместо записи временных файлов на диск мы будем держать всё в памяти с помощью `MemoryStream`. Такой подход быстрее и не захламляет файловую систему.

```csharp
using System.IO;
using System.IO.Compression;

// Step 3 – create a memory‑backed ZIP archive
using var archiveStream = new MemoryStream();
using var archive = new ZipArchive(archiveStream, ZipArchiveMode.Create, true);
```

**Примечание о граничных случаях:**  
Если ваш HTML ссылается на очень большие ресурсы (например, изображения высокого разрешения), поток в памяти может потребовать много ОЗУ. В таком случае переключитесь на ZIP, основанный на `FileStream` (`new FileStream("temp.zip", FileMode.Create)`).

---

## Шаг 4: Сохранить HTML‑документ в ZIP (aspose html save)

Теперь объединяем всё: документ, наш `MyResourceHandler` и ZIP‑архив.

```csharp
// Step 4 – save HTML + resources into the ZIP
var resourceHandler = new MyResourceHandler();
htmlDoc.Save(archive, resourceHandler);
```

За кулисами Aspose создаёт запись для основного HTML‑файла (обычно `index.html`) и дополнительные записи для каждого ресурса (например, `images/logo.png`). `resourceHandler` записывает бинарные данные непосредственно в эти записи.

---

## Шаг 5: Записать ZIP на диск (how to embed resources)

Наконец, сохраняем архив из памяти в файл. Вы можете выбрать любую папку; просто замените `YOUR_DIRECTORY` на ваш реальный путь.

```csharp
using System.IO;

// Step 5 – persist the ZIP file
File.WriteAllBytes(@"YOUR_DIRECTORY\sample.zip", archiveStream.ToArray());

// Optional: verify the archive size
Console.WriteLine($"ZIP created: {new FileInfo(@"YOUR_DIRECTORY\sample.zip").Length} bytes");
```

**Подсказка для проверки:**  
Откройте полученный `sample.zip` в проводнике архивов вашей ОС. Вы должны увидеть `index.html` и иерархию папок, отражающую оригинальные расположения ресурсов. Дважды щёлкните `index.html` — страница должна отобразиться офлайн без отсутствующих изображений или стилей.

---

## Полный рабочий пример (Все шаги вместе)

Ниже полностью готовая к запуску программа. Скопируйте её в новый проект Console App, восстановите NuGet‑пакет `Aspose.Html` и нажмите **F5**.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

// Step 1: Custom ResourceHandler that copies each external resource into the ZIP entry.
class MyResourceHandler : ResourceHandler
{
    public override void HandleResource(string uri, Stream outputStream)
    {
        // Handle both absolute file paths and relative URLs.
        if (File.Exists(uri))
        {
            using var source = new FileStream(uri, FileMode.Open, FileAccess.Read);
            source.CopyTo(outputStream);
        }
        else
        {
            // Fallback: try to download from the web (rarely needed for offline ZIPs).
            using var client = new System.Net.WebClient();
            var data = client.DownloadData(uri);
            outputStream.Write(data, 0, data.Length);
        }
    }
}

class Program
{
    static void Main()
    {
        // Step 2: Load the HTML document (URL, file path, or raw HTML string).
        var htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // Step 3: Prepare an in‑memory ZIP archive.
        using var archiveStream = new MemoryStream();
        using var archive = new ZipArchive(archiveStream, ZipArchiveMode.Create, true);

        // Step 4: Save the HTML + its resources into the ZIP.
        var resourceHandler = new MyResourceHandler();
        htmlDoc.Save(archive, resourceHandler);

        // Step 5: Persist the ZIP to disk.
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "sample.zip");
        File.WriteAllBytes(outputPath, archiveStream.ToArray());

        Console.WriteLine($"✅ ZIP created at: {outputPath}");
    }
}
```

**Ожидаемый результат:**  
Файл `sample.zip` появится на вашем рабочем столе. Распакуйте его и откройте `index.html` — страница будет выглядеть точно так же, как онлайн‑версия, но теперь полностью работает офлайн.

---

## Часто задаваемые вопросы (FAQs)

### Работает ли это с локальными HTML‑файлами?
Абсолютно. Замените URL в `HTMLDocument` на путь к файлу, например `new HTMLDocument(@"C:\site\index.html")`. Тот же `MyResourceHandler` скопирует локальные ресурсы.

### Что если ресурс — data‑URI (base64‑закодированный)?
Aspose рассматривает data‑URI как уже встроенные, поэтому обработчик не вызывается. Дополнительных действий не требуется.

### Можно ли управлять структурой папок внутри ZIP?
Да. Перед вызовом `htmlDoc.Save` можно задать `htmlDoc.SaveOptions` и указать базовый путь. Либо изменить `MyResourceHandler`, чтобы добавлять префикс папки при создании записей.

### Как добавить файл README в архив?
Просто создайте новую запись вручную:

```csharp
var readme = archive.CreateEntry("README.txt");
using var writer = new StreamWriter(readme.Open());
writer.WriteLine("This ZIP contains an offline HTML site.");
```

---

## Следующие шаги и смежные темы

- **Как встроить ресурсы** в другие форматы (PDF, SVG) с помощью аналогичных API Aspose.  
- **Настройка уровня сжатия**: `new ZipArchive(stream, ZipArchiveMode.Create, true, Encoding.UTF8)` позволяет передать `ZipArchiveEntry.CompressionLevel` для более быстрого или более компактного архива.  
- **Отдача ZIP через ASP.NET Core**: вернуть `MemoryStream` как файловый результат (`File(archiveStream, "application/zip", "site.zip")`).  

Поэкспериментируйте с этими вариантами, чтобы подобрать оптимальное решение для вашего проекта. Шаблон, который мы рассмотрели, достаточно гибок для большинства сценариев «упаковать всё в один файл».

---

## Заключение

Мы только что продемонстрировали **как упаковать HTML** с помощью Aspose.HTML, **пользовательского обработчика ресурсов** и класса .NET `ZipArchive`. Создав обработчик, который передаёт локальные файлы, загрузив документ, упаковав всё в память и, наконец, сохранив ZIP, вы получаете полностью автономный архив, готовый к распространению.  

Теперь вы уверенно можете создавать zip‑пакеты для статических сайтов, экспортировать наборы документации или даже автоматизировать офлайн‑резервные копии — всё это с несколькими строками C#.

Есть свой вариант решения? Оставьте комментарий, и счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}