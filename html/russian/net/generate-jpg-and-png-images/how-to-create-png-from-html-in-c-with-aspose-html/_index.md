---
category: general
date: 2026-11-14
description: Создайте PNG из HTML в C# с помощью Aspose.HTML – пошаговое руководство
  по рендерингу HTML в PNG, конвертации HTML в изображение и сохранению HTML в виде
  PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PNG from HTML
- render HTML to PNG
- convert HTML to image
- save HTML as PNG
- render HTML to image
language: ru
lastmod: 2026-11-14
og_description: Создайте PNG из HTML в C# с помощью Aspose.HTML. Узнайте, как отобразить
  HTML в PNG, преобразовать HTML в изображение и сохранить HTML как PNG за несколько
  простых шагов.
og_image_alt: Diagram illustrating create PNG from HTML workflow using Aspose.HTML
  in C#
og_title: Создание PNG из HTML в C# – полный учебник по Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Create PNG from HTML in C# using Aspose.HTML – a step‑by‑step guide
    to render HTML to PNG, convert HTML to image, and save HTML as PNG.
  headline: How to create PNG from HTML in C# with Aspose.HTML
  type: TechArticle
- description: Create PNG from HTML in C# using Aspose.HTML – a step‑by‑step guide
    to render HTML to PNG, convert HTML to image, and save HTML as PNG.
  name: How to create PNG from HTML in C# with Aspose.HTML
  steps:
  - name: Prerequisites
    text: '* .NET 6.0 SDK or later (the code also works with .NET Core 3.1 and .NET
      Framework 4.7+). * Visual Studio 2022 or any IDE that supports C#. * Basic familiarity
      with C# async/await is helpful but not required.'
  - name: Install Aspose.HTML
    text: 'Open a terminal in your project folder and run:'
  - name: Create a custom resource handler (optional but recommended)
    text: 'When the HTML references external assets (e.g., `logo.png`, CSS files,
      web fonts), Aspose.HTML asks a `ResourceHandler` for a stream. By providing
      our own handler we can:'
  - name: Build the HTML document
    text: You can load HTML from a string, a URL, or a file. For simplicity the tutorial
      uses an inline string that contains an image placeholder.
  - name: Configure image save options
    text: '`ImageSaveOptions` tells Aspose.HTML what raster format to produce and
      which `ResourceHandler` to use.'
  - name: Render the HTML to PNG
    text: The `RenderToImage` method performs the actual conversion. It takes a file
      path and the options defined above.
  - name: Verify the result
    text: Open the generated PNG with any image viewer. You should see the heading
      “Hello, Aspose.HTML!” and a blank placeholder where `logo.png` would appear
      (because our handler returns an empty stream). To **convert HTML to image**
      with the real logo, replace `MyHandler` with a version that loads the actua
  - name: Extending the solution (optional)
    text: Extending the solution (optional)
  type: HowTo
tags:
- Aspose.HTML
- C#
- Image rendering
title: Как создать PNG из HTML в C# с помощью Aspose.HTML
url: /ru/net/generate-jpg-and-png-images/how-to-create-png-from-html-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать PNG из HTML в C# с помощью Aspose.HTML

Если вам нужно **создать PNG из HTML** в .NET‑приложении, это руководство покажет вам точные шаги. Вы узнаете, как **рендерить HTML в PNG**, работать с внешними ресурсами и **сохранять HTML как PNG**, не выходя из среды C#.

В примере используется Aspose.HTML 5.x — полностью управляемая библиотека, которая рендерит HTML, CSS и SVG в растровые изображения. Не требуются внешние браузеры или нативные зависимости, что делает решение идеальным для серверной генерации изображений, создания миниатюр электронных писем или предварительной обработки PDF.

## Что вы достигнете

К концу этого руководства вы сможете:

* Настроить C#‑проект с пакетом NuGet Aspose.HTML.  
* Реализовать пользовательский `ResourceHandler` для управления тем, как загружаются изображения, CSS и шрифты.  
* **Рендерить HTML в PNG** с помощью `ImageSaveOptions`.  
* Проверить полученный файл и понять, как **конвертировать HTML в изображение** в других форматах.

### Требования

* .NET 6.0 SDK или новее (код также работает с .NET Core 3.1 и .NET Framework 4.7+).  
* Visual Studio 2022 или любой IDE, поддерживающий C#.  
* Базовое знакомство с C# async/await будет полезным, но не является обязательным.

> **Полезный совет:** Aspose.HTML лицензируется на разработчика или на сервер. Для оценки вы можете использовать временный лицензионный ключ; библиотека работает в пробном режиме с водяным знаком на отрендеренном изображении.

## Как создать PNG из HTML с помощью Aspose.HTML

Ядро решения состоит из трёх небольших классов: пользовательского `ResourceHandler`, метода, который создает `HTMLDocument`, и вызова рендеринга, который **сохраняет HTML как PNG**. В следующих разделах рассматривается каждая часть.

### Шаг 1: Установить Aspose.HTML

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.Html
```

Пакет включает `Aspose.Html`, `Aspose.Html.Rendering` и `Aspose.Html.Rendering.Image`, которые необходимы для вывода изображений.

### Шаг 2: Создать пользовательский обработчик ресурсов (необязательно, но рекомендуется)

Когда HTML ссылается на внешние ресурсы (например, `logo.png`, CSS‑файлы, веб‑шрифты), Aspose.HTML запрашивает у `ResourceHandler` поток. Предоставив собственный обработчик, мы можем:

* Вести журнал каждого запрашиваемого URL.  
* Перенаправлять ресурсы на CDN или в кэш в памяти.  
* Предотвращать сетевые вызовы в изолированных средах.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

/// <summary>
/// Supplies a stream for each external resource referenced by the HTML.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a <see cref="Stream"/> that Aspose.HTML will read from.
    /// </summary>
    /// <param name="info">Information about the requested resource.</param>
    /// <returns>A writable <see cref="MemoryStream"/>.</returns>
    public override Stream HandleResource(ResourceInfo info)
    {
        // For demonstration we return an empty MemoryStream.
        // In production you could download the resource, read it from disk,
        // or generate it on the fly.
        return new MemoryStream();
    }
}
```

**Зачем использовать пользовательский обработчик?**  
Если HTML содержит `<img src="logo.png">`, обработчик по умолчанию попытается прочитать `logo.png` из файловой системы относительно текущего рабочего каталога. В облачных сервисах файловая система может быть только для чтения, поэтому пользовательский обработчик позволяет контролировать источник каждого ресурса.

### Шаг 3: Создать HTML‑документ

Вы можете загрузить HTML из строки, URL или файла. Для простоты в руководстве используется встроенная строка, содержащая заполнитель изображения.

```csharp
// Build a simple HTML document with an image reference.
string markup = @"
<html>
  <head>
    <style>
      body { font-family: Arial, sans-serif; background:#f8f8f8; }
      img { width:150px; height:auto; }
    </style>
  </head>
  <body>
    <h1>Hello, Aspose.HTML!</h1>
    <img src='logo.png' alt='Company logo'>
  </body>
</html>";

HTMLDocument html = new HTMLDocument(markup);
```

Если у вас уже есть HTML‑файл, замените конструктор на `new HTMLDocument("path/to/file.html")`.

### Шаг 4: Настроить параметры сохранения изображения

`ImageSaveOptions` указывает Aspose.HTML, какой растровый формат создавать и какой `ResourceHandler` использовать.

```csharp
// Choose PNG as the output format.
ImageSaveOptions options = new ImageSaveOptions(SaveFormat.Png)
{
    // Attach the custom handler defined in Step 2.
    ResourceHandler = new MyHandler(),

    // Optional: control the image size and background.
    Width = 1024,               // Width in pixels.
    Height = 768,               // Height in pixels.
    BackgroundColor = System.Drawing.Color.White
};
```

Вы также можете задать `Resolution`, `PageNumber` или `PageCount`, чтобы рендерить конкретные страницы, когда источник — HTML‑документ с несколькими фреймами.

### Шаг 5: Рендерить HTML в PNG

Метод `RenderToImage` выполняет фактическое преобразование. Он принимает путь к файлу и параметры, определённые выше.

```csharp
// Render the HTML document to a PNG file.
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");
html.RenderToImage(outputPath, options);

// Inform the user.
Console.WriteLine($"HTML has been rendered to PNG at: {outputPath}");
```

Когда метод завершится, `output.png` будет содержать растровый снимок разметки, включая любые изображения, предоставленные `MyHandler`.

### Шаг 6: Проверить результат

Откройте сгенерированный PNG в любом просмотрщике изображений. Вы должны увидеть заголовок «Hello, Aspose.HTML!» и пустой заполнитель там, где должен быть `logo.png` (поскольку наш обработчик возвращает пустой поток). Чтобы **конвертировать HTML в изображение** с реальным логотипом, замените `MyHandler` на версию, которая загружает фактический файл:

```csharp
public override Stream HandleResource(ResourceInfo info)
{
    if (info.Uri.EndsWith("logo.png", StringComparison.OrdinalIgnoreCase))
    {
        // Load the real logo from disk.
        return File.OpenRead(@"C:\Images\logo.png");
    }
    // Fallback for other resources.
    return base.HandleResource(info);
}
```

Перезапустите программу, и логотип появится в выходном PNG.

### Шаг 7: Расширение решения (необязательно)

#### Рендеринг HTML в другие форматы изображений

Чтобы **рендерить HTML в изображение** в JPEG, BMP или TIFF, просто измените `SaveFormat`:

```csharp
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.Jpeg);
html.RenderToImage("output.jpg", jpegOptions);
```

#### Генерация нескольких страниц

Если ваш HTML содержит разрывы страниц (`<div style="page-break-after:always;">`), вы можете рендерить каждую страницу отдельно:

```csharp
for (int i = 0; i < html.PageCount; i++)
{
    options.PageNumber = i + 1; // 1‑based index
    string pagePath = $"output_page_{i + 1}.png";
    html.RenderToImage(pagePath, options);
}
```

#### Использовать асинхронный рендеринг для сервисов с высокой пропускной способностью

Aspose.HTML также предоставляет асинхронный API:

```csharp
await html.RenderToImageAsync(outputPath, options);
```

Это полезно, когда рендеринг выполняется внутри конечной точки ASP.NET Core, которая должна оставаться отзывчивой.

## Полный, исполняемый пример

Ниже представлено автономное консольное приложение, которое объединяет все части. Скопируйте код в новый .NET‑консольный проект и запустите его.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

namespace HtmlToPngDemo
{
    /// <summary>
    /// Supplies a stream for each external resource referenced by the HTML.
    /// </summary>
    class MyHandler : ResourceHandler
    {
        public override Stream HandleResource(ResourceInfo info)
        {
            // Load the real logo if the request is for "logo.png".
            if (info.Uri.EndsWith("logo.png", StringComparison.OrdinalIgnoreCase))
            {
                // Adjust the path to where your logo actually lives.
                string logoPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "logo.png");
                return File.OpenRead(logoPath);
            }

            // For any other resource return an empty stream.
            return new MemoryStream();
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Build the HTML markup.
            string markup = @"
            <html>
              <head>
                <style>
                  body { font-family: Arial, sans-serif; background:#f8f8f8; }
                  img { width:150px; height:auto; }
                </style>
              </head>
              <body>
                <h1>Hello, Aspose.HTML!</h1>
                <img src='logo.png' alt='Company logo'>
              </body>
            </html>";

            // 2️⃣ Create the HTML document object.
            HTMLDocument html = new HTMLDocument(markup);

            // 3️⃣ Configure PNG output options.
            ImageSaveOptions options = new ImageSaveOptions(SaveFormat.Png)
            {
                Width = 1024,
                Height = 768,
                BackgroundColor = System.Drawing.Color.White,
                ResourceHandler = new MyHandler()
            };

            // 4️⃣ Render the document to a PNG file.
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");
            html.RenderToImage(outputPath, options);

            Console.WriteLine($"✅ HTML successfully rendered to PNG at: {outputPath}");
        }
    }
}
```

**Ожидаемый результат:**  
Файл с именем `output.png` (≈ 1024 × 768 px) появляется в рабочем каталоге программы. Изображение содержит заголовок и

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создать PNG из HTML с Aspose.HTML – Полное пошаговое руководство](/html/english/net/generate-jpg-and-png-images/create-png-from-html-with-aspose-html-full-step-by-step-guid/)
- [Создать HTML‑документ и отрендерить HTML в PNG – Полное руководство C#](/html/english/net/rendering-html-documents/create-html-document-and-render-html-to-png-full-c-guide/)
- [Как использовать Aspose для рендеринга HTML в PNG – Пошаговое руководство](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}