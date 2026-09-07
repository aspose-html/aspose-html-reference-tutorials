---
category: general
date: 2026-09-07
description: Узнайте, как создавать изображение из HTML с помощью Aspose.HTML в C#.
  Это пошаговое руководство также показывает, как рендерить HTML в изображение и конвертировать
  HTML в PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create image from html
- render html to image
- convert html to png
- save html as png
- set image width height
language: ru
lastmod: 2026-09-07
og_description: Создайте изображение из HTML в C# с помощью Aspose.HTML. Следуйте
  этому руководству, чтобы отобразить HTML в изображение, конвертировать HTML в PNG
  и задать ширину и высоту изображения для идеального результата.
og_image_alt: Screenshot of a rendered PNG image generated from an HTML file using
  Aspose.HTML
og_title: Создание изображения из HTML в C# – полное руководство по Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: Learn how to create image from HTML with Aspose.HTML in C#. This step‑by‑step
    guide also shows how to render HTML to image and convert HTML to PNG.
  headline: How to create image from HTML using Aspose.HTML in C#
  type: TechArticle
tags:
- Aspose.HTML
- C#
- image rendering
title: Как создать изображение из HTML с помощью Aspose.HTML на C#
url: /ru/net/generate-jpg-and-png-images/how-to-create-image-from-html-using-aspose-html-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать изображение из HTML с помощью Aspose.HTML на C#

Если вам нужно **создать изображение из HTML** в .NET‑приложении, это руководство покажет вам точные шаги с Aspose.HTML. Вы узнаете, как **рендерить HTML в изображение**, выбрать PNG в качестве формата вывода и управлять размерами вывода, чтобы изображение выглядело точно так, как вы ожидаете.

В руководстве покрыты все необходимые детали: требуемые пакеты NuGet, полный пример кода, объяснения каждой опции и советы по распространённым подводным камням. К концу вы сможете **конвертировать HTML в PNG**, **сохранить HTML как PNG** и **задать ширину и высоту изображения** программно.

## Предварительные требования

* .NET 6.0 или новее установлен (код также работает с .NET 5 и .NET Framework 4.7+).
* Visual Studio 2022 (или любой IDE, поддерживающий C#).
* Лицензия Aspose.HTML for .NET или бесплатный оценочный ключ. Установите пакет через NuGet:

```bash
dotnet add package Aspose.HTML
```

* HTML‑файл (`input.html`), который вы хотите превратить в изображение. Поместите его в папку, к которой ваш проект может обращаться.

## Шаг 1: Загрузите HTML‑документ, который хотите отрендерить

Первая операция — создать экземпляр `HTMLDocument`, указывающий на ваш исходный файл. Aspose.HTML автоматически читает разметку, CSS и внешние ресурсы (изображения, шрифты).

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;

// Load the HTML file from disk
var document = new HTMLDocument(@"C:\MyProject\Resources\input.html");
```

*Почему это важно:* Загрузка документа отделяет парсинг от рендеринга, позволяя переиспользовать один объект `HTMLDocument` для нескольких проходов рендеринга (например, с разными размерами изображения).

## Шаг 2: Настройте параметры рендеринга изображения (задать ширину и высоту изображения, формат, качество)

`ImageRenderingOptions` позволяет точно настроить вывод. Здесь мы включаем сглаживание, задаём жирный шрифт Arial, включаем подсказки текста и явно **задаём ширину и высоту изображения** 800 × 600 px. `ImageFormat` установлен в PNG, который является без потерь и широко поддерживается.

```csharp
var renderingOptions = new ImageRenderingOptions
{
    // Smooth graphics with anti‑aliasing
    UseAntialiasing = true,

    // Font used when the HTML references a generic family (e.g., sans‑serif)
    Font = new Font("Arial", 12, WebFontStyle.Bold),

    // Improves the clarity of rendered text
    TextOptions = new TextOptions { UseHinting = true },

    // Explicitly set the output dimensions – this is the “set image width height” part
    Width = 800,
    Height = 600,

    // Choose PNG as the output format – “convert HTML to PNG”
    ImageFormat = ImageFormat.Png
};
```

**Подсказка:** Если опустить `Width` и `Height`, Aspose.HTML использует внутренний размер HTML, что может привести к очень большому или очень маленькому изображению. Всегда задавайте размеры, когда нужны предсказуемые результаты.

## Шаг 3: Создайте рендерер с настроенными параметрами

Класс `ImageRenderer` выполняет фактическое преобразование. Передача `renderingOptions`, которые вы только что создали, гарантирует, что рендерер будет учитывать ваши настройки.

```csharp
var renderer = new ImageRenderer(renderingOptions);
```

*Почему это важно:* Разделение рендерера и параметров позволяет переиспользовать один и тот же рендерер для разных документов, сохраняя единую конфигурацию.

## Шаг 4: Отрендерите HTML‑документ в PNG‑файл — «сохранить HTML как PNG»

Теперь вызовите `Render`, передав исходный документ и путь к целевому файлу. Метод блокирует выполнение, пока изображение не будет записано на диск.

```csharp
// Render the HTML to a PNG file – “save HTML as PNG”
renderer.Render(document, @"C:\MyProject\Resources\output.png");
```

После завершения вызова `output.png` содержит растровый снимок `input.html`. Вы можете открыть файл в любом просмотрщике изображений, чтобы проверить результат.

### Ожидаемый результат

Запуск полной программы создаёт PNG‑файл со следующими свойствами:

* **Размеры:** 800 × 600 px (как задано в `Width`/`Height`).
* **Формат:** PNG (без потерь, поддерживает прозрачность).
* **Визуальное качество:** Сглаженная графика и подсказки текста, соответствующие внешнему виду оригинального HTML в современном браузере.

## Полный, исполняемый пример

Ниже представлен весь код программы, который вы можете скопировать в консольное приложение (`Program.cs`). Скорректируйте пути к файлам под вашу среду.

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;

namespace HtmlToPngDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the HTML document
            var htmlPath = @"C:\MyProject\Resources\input.html";
            var document = new HTMLDocument(htmlPath);

            // 2️⃣ Set rendering options – width, height, format, quality
            var renderingOptions = new ImageRenderingOptions
            {
                UseAntialiasing = true,
                Font = new Font("Arial", 12, WebFontStyle.Bold),
                TextOptions = new TextOptions { UseHinting = true },
                Width = 800,          // set image width
                Height = 600,         // set image height
                ImageFormat = ImageFormat.Png
            };

            // 3️⃣ Create the renderer
            var renderer = new ImageRenderer(renderingOptions);

            // 4️⃣ Render and save the PNG file
            var outputPath = @"C:\MyProject\Resources\output.png";
            renderer.Render(document, outputPath);

            Console.WriteLine($"HTML has been rendered to image: {outputPath}");
        }
    }
}
```

Запустите программу (`dotnet run` или нажмите **F5** в Visual Studio). После выполнения откройте `output.png` — вы увидите отрендеренную страницу точно так, как определено HTML и CSS.

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| **Что если мой HTML ссылается на внешние изображения или CSS?** | Aspose.HTML использует относительные пути от местоположения HTML‑файла. Убедитесь, что эти ресурсы доступны, либо используйте абсолютный URL. |
| **Можно ли рендерить в JPEG вместо PNG?** | Да. Измените `ImageFormat = ImageFormat.Jpeg` и при необходимости задайте `JpegQuality` в `ImageRenderingOptions`. |
| **Как отрендерить несколько страниц из одного HTML‑файла?** | Используйте функции пагинации `Document` (`document.Pages`) и вызывайте `renderer.Render(page, ...)` для каждой страницы. |
| **Что если мне нужен более высокий DPI для печати?** | Задайте `renderingOptions.DpiX` и `renderingOptions.DpiY` (например, 300) перед созданием рендерера. |
| **Нужно ли анти‑алиасинг для векторной графики?** | Он улучшает плавность линий и кривых, но вы можете отключить его (`UseAntialiasing = false`) для более быстрого рендеринга больших пакетов. |

## Совет по производительности — переиспользуйте рендерер

Если вам нужно конвертировать множество HTML‑файлов пакетно, создайте один экземпляр `ImageRenderer` и переиспользуйте его:

```csharp
var renderer = new ImageRenderer(renderingOptions);
foreach (var htmlFile in Directory.GetFiles(inputFolder, "*.html"))
{
    var doc = new HTMLDocument(htmlFile);
    var outFile = Path.ChangeExtension(htmlFile, ".png");
    renderer.Render(doc, outFile);
}
```

Переиспользование рендерера избавляет от повторного выделения внутренних ресурсов, снижая нагрузку на CPU и память.

## Заключение

Теперь вы знаете, как **создать изображение из HTML** с помощью Aspose.HTML в C#. Следуя четырём шагам — загрузке документа, настройке параметров рендеринга (включая **задание ширины и высоты изображения**), созданию рендерера и, наконец, **рендерингу HTML в изображение** — вы можете надёжно **конвертировать HTML в PNG** и **сохранить HTML как PNG** для миниатюр, предварительных просмотров в письмах или конвейеров генерации PDF.

Далее вы можете изучить:

* **render html to image** с разными форматами (JPEG, BMP, GIF).
* Добавление водяных знаков или наложений с помощью `Graphics` после рендеринга.
* Интеграцию этого преобразования в ASP.NET Core API для генерации изображений по запросу.

Не стесняйтесь экспериментировать с параметрами, и позвольте гибкости Aspose.HTML выполнить тяжёлую работу за вас. Приятного кодинга!

## Что изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и изучить альтернативные подходы к реализации в ваших проектах.

- [Как использовать Aspose для рендеринга HTML в PNG — пошаговое руководство](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Учебник HTML в изображение — рендеринг HTML в PNG на C#](/html/english/net/generate-jpg-and-png-images/html-to-image-tutorial-render-html-to-png-in-c/)
- [Создание PNG из HTML с Aspose.Html — пошаговое руководство](/html/english/net/generate-jpg-and-png-images/create-png-from-html-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}