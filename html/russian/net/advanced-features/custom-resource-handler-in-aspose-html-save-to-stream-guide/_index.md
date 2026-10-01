---
category: general
date: 2026-02-22
description: Пользовательский обработчик ресурсов позволяет захватывать вывод HTML.
  Узнайте, как загрузить HTML‑документ, использовать Aspose HTML save и сохранить
  HTML в поток с простым примером на C#.
draft: false
keywords:
- custom resource handler
- load html document
- aspose html save
- save html to stream
- capture html output
language: ru
og_description: Узнайте, как пользовательский обработчик ресурсов захватывает вывод
  HTML, загружает HTML‑документ и сохраняет HTML в поток с помощью Aspose HTML в C#.
og_title: Пользовательский обработчик ресурсов в Aspose HTML – Руководство по сохранению
  в поток
tags:
- aspose-html
- csharp
- streaming
- resource-handler
title: Пользовательский обработчик ресурсов в Aspose HTML – руководство по сохранению
  в поток
url: /ru/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пользовательский обработчик ресурсов – Захват HTML‑вывода с помощью Aspose HTML

Когда‑нибудь вам нужен был **custom resource handler**, чтобы перехватывать каждый файл, который Aspose HTML записывает во время конвертации? Возможно, вы хотели направлять HTML, изображения или CSS сразу в память, а не на диск. Это очень распространённый сценарий при построении веб‑сервиса, который должен оставаться без состояния, или когда просто нужно **save HTML to stream** для последующей обработки.

> **Почему это важно?**  
> Захват HTML‑вывода в памяти позволяет избежать ввода‑вывода файловой системы, уменьшить задержки в облачных функциях и даёт полный контроль над именованием, сжатием или даже трансформациями «на лету».

---

## Что понадобится

- **.NET 6** или новее (код также работает на .NET Framework 4.7+).  
- NuGet‑пакет **Aspose.HTML for .NET** (`Aspose.Html`).  
- Простой HTML‑файл (`input.html`), размещённый в доступной папке.  
- Любая удобная IDE — Visual Studio, Rider или VS Code с расширениями C#.

Дополнительная конфигурация не требуется; API делает всю тяжёлую работу.

---

## Шаг 1 – Создание пользовательского обработчика ресурсов

Суть этой техники — наследовать `Aspose.Html.Rendering.ResourceHandler`. Переопределяя `HandleResource`, вы решаете, **куда** будет направлен каждый поток ресурса. В нашем случае мы возвращаем новый `MemoryStream` для каждого запроса, что означает, что каждый CSS, изображение или вложенный HTML‑фрагмент живёт только в ОЗУ.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

/// <summary>
/// Custom handler that writes every resource to a new MemoryStream.
/// </summary>
class MemoryStreamHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // The ResourceInfo gives you the original URL and MIME type.
        // You could inspect it here to decide whether to skip certain files.
        // For this tutorial we just allocate a fresh stream.
        return new MemoryStream();
    }
}
```

**Pro tip:** Если нужно отслеживать потоки (например, чтобы позже записать их в ZIP‑архив), храните их в `Dictionary<string, MemoryStream>`, где ключом является `resourceInfo.Uri`.

---

## Шаг 2 – Загрузка HTML‑документа

Прежде чем что‑то сохранять, необходимо **load HTML document** в экземпляр `HTMLDocument`. Aspose HTML может читать из пути к файлу, URL или даже из строки. Здесь мы используем локальный файл для простоты.

```csharp
// Adjust the path to point at your real HTML file.
string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Load the source HTML document.
HTMLDocument htmlDocument = new HTMLDocument(htmlPath);
```

Если ваш HTML ссылается на внешние ресурсы (изображения, шрифты и т.д.), убедитесь, что базовый URI указан правильно; иначе обработчик не сможет их найти.

---

## Шаг 3 – Создание экземпляра пользовательского обработчика

Теперь мы создаём экземпляр обработчика, определённого ранее. Никаких хитростей — просто обычный `new`. Этот объект будет передан в метод `Save` на следующем шаге.

```csharp
// Step 3: Instantiate the custom handler.
MemoryStreamHandler resourceHandler = new MemoryStreamHandler();
```

Поскольку обработчик существует только в памяти, вам не нужно беспокоиться о разрешениях файловой системы или очистке диска.

---

## Шаг 4 – Сохранение документа с помощью Aspose HTML Save

Операция **Aspose HTML save** принимает `ResourceHandler`. Пока движок проходит по DOM и разрешает каждый связанный ресурс, он вызывает `HandleResource`. Наша реализация возвращает `MemoryStream`, поэтому каждый кусок оказывается в ОЗУ.

```csharp
// Step 4: Save the document.
// The handler's HandleResource method will be invoked for each output stream.
htmlDocument.Save(resourceHandler);
```

На этом этапе конверсия завершена, но потоки всё ещё находятся в памяти. Теперь их можно читать, записывать в базу данных или возвращать в ответе API.

---

## Шаг 5 – Получение и проверка захваченных потоков

Поскольку мы каждый раз возвращали новый `MemoryStream`, нам нужен способ хранить ссылки. Ниже представлено небольшое расширение предыдущего обработчика, которое сохраняет каждый поток в словарь, чтобы вы могли исследовать их после сохранения.

```csharp
class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;   // Remember the stream by its URI.
        return ms;
    }
}

// Usage:
var trackingHandler = new TrackingMemoryStreamHandler();
htmlDocument.Save(trackingHandler);

// Example: write the main HTML output to console (as text)
if (trackingHandler.Streams.TryGetValue(htmlPath, out var mainStream))
{
    mainStream.Position = 0; // rewind
    using var reader = new StreamReader(mainStream);
    string html = reader.ReadToEnd();
    Console.WriteLine("=== Rendered HTML ===");
    Console.WriteLine(html);
}
```

Запуск этого кода выведет финальный HTML, сгенерированный Aspose, подтверждая, что **capture html output** работает как ожидалось.

---

## Пограничные случаи и часто задаваемые вопросы

### 1. Что делать, если документ огромный?

Потребление памяти может быстро расти. Для больших PDF‑файлов или HTML с множеством изображений высокого разрешения рассмотрите возможность потоковой записи непосредственно в `FileStream` или **buffered network stream** вместо `MemoryStream`. Обработчик может решить, что использовать, исходя из `resourceInfo.MimeType`.

### 2. Нужно ли освобождать потоки?

Да. После завершения обработки вызывайте `Dispose()` для каждого `MemoryStream` (или позвольте блоку `using` сделать это). В примере с отслеживанием мы могли бы добавить:

```csharp
foreach (var ms in trackingHandler.Streams.Values)
    ms.Dispose();
```

### 3. Можно ли переименовать ресурсы перед сохранением?

Конечно. Внутри `HandleResource` у вас есть доступ к `resourceInfo.Uri`. Вы можете изменить его, добавить префикс или даже пропустить отдельные файлы, вернув `null`.

```csharp
if (resourceInfo.MimeType.StartsWith("image/"))
    return null; // Skip images completely.
```

### 4. Является ли этот подход потокобезопасным?

Один экземпляр обработчика **не должен** использоваться одновременно в нескольких вызовах `Save`. Создавайте новый обработчик для каждой конверсии или защищайте внутренний словарь блокировкой, если необходимо переиспользовать его.

---

## Полный рабочий пример

Ниже полностью готовая программа, которую можно вставить в консольное приложение. Она демонстрирует всё — от загрузки HTML‑файла до вывода захваченного результата.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;

class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;
        return ms;
    }
}

class SaveToStreamTutorial
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the HTML document you want to render.
        // -------------------------------------------------
        string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");
        if (!File.Exists(htmlPath))
        {
            Console.WriteLine($"Cannot find {htmlPath}");
            return;
        }

        HTMLDocument htmlDocument = new HTMLDocument(htmlPath);

        // -------------------------------------------------
        // Step 2: Create the custom handler that captures streams.
        // -------------------------------------------------
        var handler = new TrackingMemoryStreamHandler();

        // -------------------------------------------------
        // Step 3: Save the document – Aspose will invoke our handler.
        // -------------------------------------------------
        htmlDocument.Save(handler);

        // -------------------------------------------------
        // Step 4: Retrieve the main HTML output and display it.
        // -------------------------------------------------
        if (handler.Streams.TryGetValue(htmlPath, out var mainStream))
        {
            mainStream.Position = 0; // rewind to start
            using var reader = new StreamReader(mainStream);
            string renderedHtml = reader.ReadToEnd();
            Console.WriteLine("=== Rendered HTML Output ===");
            Console.WriteLine(renderedHtml);
        }
        else
        {
            Console.WriteLine("Main HTML stream not found.");
        }

        // -------------------------------------------------
        // Step 5: Clean up.
        // -------------------------------------------------
        foreach (var ms in handler.Streams.Values)
            ms.Dispose();

        Console.WriteLine("All streams disposed. Done.");
    }
}
```

**Expected output:** Консоль выводит полностью отрендеренный HTML (включая любой встроенный CSS, который мог сгенерировать Aspose) и подтверждение, что все потоки были освобождены.

---

## Заключение

Вы только что узнали, как реализовать **custom resource handler** в Aspose HTML, **load an HTML document** и **save HTML to stream**, одновременно **capturing the HTML output** для дальнейшей обработки. Этот шаблон лёгок, учитывает многопоточность и полностью расширяем — вы можете заменить `MemoryStream` на файл, сетевой сокет или API облачного хранилища за несколько строк кода.

Далее вы можете изучить:

- **Saving to a ZIP archive** (идеально для упаковки HTML, CSS и изображений).  
- **Applying transformations** (например, минификация CSS «на лету»).  
- **Streaming directly to an HTTP response** в ASP.NET Core для мгновенной загрузки.

Попробуйте, и вы увидите, насколько мощным может быть настроенный **custom resource handler** в реальных сценариях. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}