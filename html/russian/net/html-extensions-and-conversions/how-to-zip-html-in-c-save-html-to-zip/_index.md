---
category: general
date: 2025-12-29
description: Как быстро упаковать HTML в ZIP в C# с использованием Aspose.HTML — сохранить
  HTML в ZIP с помощью пользовательского ZipResourceHandler. Узнайте пошагово.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: ru
og_description: Как быстро упаковать HTML в ZIP в C# с помощью Aspose.HTML. Следуйте
  этому руководству, чтобы сохранить HTML в ZIP и создать архив ZIP с пользовательской
  обработкой ресурсов.
og_title: Как упаковать HTML в zip в C# – Сохранить HTML в zip
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Как упаковать HTML в ZIP в C# – Сохранить HTML в ZIP
url: /ru/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как заархивировать HTML в ZIP в C# – Сохранить HTML в ZIP

Как заархивировать HTML в C# – это частая потребность, когда нужно упаковать веб‑страницы для офлайн‑использования. Будь то один файл со всеми изображениями или экспорт целого сайта, **сохранение HTML в zip** делает всё аккуратным и портативным. В этом руководстве мы пройдём через полностью готовое решение, которое не только упаковывает разметку HTML, но и напрямую потоково записывает каждый используемый ресурс в архив.

Вы узнаете, как:

* Программно создавать zip‑архив с помощью `System.IO.Compression` из .NET.
* Подключить пользовательский `ResourceHandler` к Aspose.HTML, чтобы ресурсы сразу попадали в zip.
* Обрабатывать особые случаи, такие как существующие zip‑файлы и большие бинарные ресурсы.

Никаких внешних инструментов – только C#, Aspose.HTML и несколько строк кода.

## Что понадобится

Прежде чем начать, убедитесь, что у вас есть:

* **.NET 6+** (код также работает на .NET Framework 4.6.2 и новее).
* **Aspose.HTML for .NET** – можно взять бесплатную пробную версию с сайта Aspose или использовать лицензированную копию.
* Среда разработки (Visual Studio, VS Code, Rider — что вам удобно).

Это всё. Дополнительных NuGet‑пакетов не требуется, кроме `System.IO.Compression` (входит в .NET) и `Aspose.HTML`.

## Шаг 1: Создание проекта и импортов

Создайте новый консольный проект (или вставьте код в существующий). Добавьте необходимые директивы `using` в начало файла:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **Pro tip:** Если вы используете Visual Studio, IDE предложит добавить недостающий NuGet‑пакет для `Aspose.Html`. Примите предложение — и вы готовы к работе.

## Шаг 2: Реализация собственного ZipResourceHandler

Aspose.HTML вызывает `ResourceHandler` каждый раз, когда необходимо записать ресурс (изображение, CSS‑файл, скрипт). Переопределив `HandleResource`, мы можем точно определить, куда будет помещён каждый ресурс. Ниже показан обработчик, который создаёт запись в zip, соответствующую логическому пути ресурса, и возвращает поток записи, указывающий непосредственно на эту запись.

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**Почему это важно:**  
Вместо записи ресурсов во временную папку и последующего архивирования, этот обработчик потоково передаёт данные, экономя ввод‑вывод на диск и снижая потребление памяти. Он также гарантирует, что внутренняя иерархия папок в zip будет соответствовать относительным путям HTML, что ожидают браузеры при распаковке и открытии страницы.

## Шаг 3: Подготовка zip‑архива

Теперь откроем (или создадим) целевой zip‑файл. Флаг `FileMode.Create` перезаписывает любой существующий файл — идеальный вариант для повторяемых сборок. Если нужно сохранить существующий архив, переключитесь на `FileMode.OpenOrCreate` и обработайте дублирующиеся записи соответствующим образом.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Edge case:** Если процесс завершится с ошибкой до выхода из блока `using`, архив может оказаться повреждённым. Запуск кода внутри `try/catch` и удаление частично созданного файла в случае неудачи — простая защита.

## Шаг 4: Создание HTML‑документа с встроенным ресурсом

Для демонстрации создадим небольшую HTML‑страницу, которая ссылается на изображение `image.png`. В реальном проекте HTML обычно загружается из файла или строки из базы данных.

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

Если у вас есть реальные файлы изображений на диске, их можно добавить в zip вручную перед сохранением HTML, либо позволить Aspose.HTML загрузить их через обработчик (например, по URL). Наш обработчик работает как с локальными путями, так и с удалёнными URL.

## Шаг 5: Настройка параметров сохранения для использования ZipResourceHandler

Теперь укажем Aspose.HTML использовать наш пользовательский обработчик при записи ресурсов. Класс `HTMLSaveOptions` также позволяет задать имя выходного файла внутри zip (по умолчанию — `index.html`).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## Шаг 6: Сохранение документа — всё потоково попадает в zip

Наконец, вызываем `Save`. Aspose.HTML разбирает разметку, находит тег `<img>`, вызывает `HandleResource` для `image.png` и записывает как HTML‑файл, так и изображение в один и тот же zip‑архив.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

Когда блоки `using` завершаются, `ZipArchive` финализирует файл, делая его готовым к распространению.

### Полный рабочий пример

Ниже представлен весь код программы целиком. Скопируйте его в `Program.cs` и запустите — никаких дополнительных правок не требуется.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**Ожидаемый результат:** После выполнения `output.zip` будет содержать две записи:

```
index.html
image.png
```

Если распаковать архив и открыть `index.html` в браузере, изображение отобразится корректно, потому что относительный путь сохранён.

## Часто задаваемые вопросы

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}