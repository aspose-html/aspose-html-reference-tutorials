---
category: general
date: 2026-05-31
description: Создайте PNG из HTML с помощью Aspose.HTML в C#. Узнайте, как отрисовать
  HTML в PNG, задать ширину и высоту изображения и преобразовать HTML в изображение
  с пользовательским обработчиком памяти.
draft: false
keywords:
- create png from html
- render html to png
- convert html to image
- how to use aspose
- set image width height
language: ru
og_description: Создавайте PNG из HTML мгновенно. Это руководство показывает, как
  отрендерить HTML в PNG, задать ширину и высоту изображения и преобразовать HTML
  в изображение с помощью Aspose.HTML.
og_title: Создание PNG из HTML с Aspose.HTML – Полный учебник по C#
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create PNG from HTML using Aspose.HTML in C#. Learn how to render HTML
    to PNG, set image width height, and convert HTML to image with a custom memory
    handler.
  headline: Create PNG from HTML with Aspose.HTML – Full C# Guide
  type: TechArticle
tags:
- Aspose.HTML
- C#
- Image Rendering
- HTML to Image
title: Создание PNG из HTML с помощью Aspose.HTML – Полное руководство по C#
url: /ru/net/generate-jpg-and-png-images/create-png-from-html-with-aspose-html-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PNG из HTML с Aspose.HTML – Полное руководство на C#  

Нужно **создать PNG из HTML** в проекте .NET? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда им требуется быстрый снимок веб‑страницы для отчетов, миниатюр или предварительного просмотра в письмах.  

В этом руководстве мы пошагово разберём пример, который **преобразует HTML в PNG**, покажет, как **установить ширину и высоту изображения**, и даже объяснит, **как использовать мощный API Aspose** без записи временных файлов на диск. К концу вы получите автономное решение, работающее только в памяти, которое функционирует как в Windows, так и в Linux.

---

## Что вы получите

- Полностью готовая, исполняемая программа на C#, которая **преобразует HTML в изображение** с помощью Aspose.HTML.  
- Понимание конвейера **render html to png**: создание документа, стилизация, обработка ресурсов и окончательная отрисовка.  
- Советы по настройке размера вывода, сглаживанию и работе с ресурсами в памяти (идеально для облачных сценариев).  
- Краткий чек‑лист распространённых подводных камней и способов их избежать.  

### Предварительные требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+).  
- Действительная лицензия Aspose.HTML for .NET (или бесплатная пробная версия).  
- Базовые знания C# и концепций HTML/CSS.  

> **Pro tip:** Если вы работаете на Linux‑CI‑раннере, флаг `UseAntialiasing` в `ImageRenderingOptions` вам пригодится — он сглаживает края даже когда стандартный графический стек работает без дисплея.  

---

## Шаг 1 – Создание PNG из HTML: настройка Aspose.HTML

Для начала подключим необходимые пространства имён. Эти using‑директивы дают доступ к модели документа, движку рендеринга и пользовательскому обработчику ресурсов, который понадобится позже.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Saving;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;
```

> **Почему именно эти пространства имён?**  
> `Aspose.Html` содержит основной класс `HTMLDocument`, а `Aspose.Html.Rendering.Image` предоставляет `ImageRenderingOptions` и методы `RenderToFile`, которые действительно **преобразуют HTML в изображение**. Пространства имён `Saving` и `Drawing` позволяют настраивать шрифты и обработку ресурсов.  

---

## Шаг 2 – Рендеринг HTML в PNG с пользовательскими параметрами

Теперь мы настраиваем внешний вид конечного PNG. Объект `ImageRenderingOptions` позволяет **установить ширину и высоту изображения**, включить сглаживание и даже выбрать цвет фона, если нужна прозрачность.

```csharp
var imageOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,   // smooths out text and vector edges
    Width = 800,              // set image width height to 800×600 pixels
    Height = 600
};
```

> **Edge case:** Если не указать `Width`/`Height`, Aspose подгонит размер изображения под размеры разметки HTML, что может привести к неожиданно высоким изображениям для длинных страниц. Явное задание этих параметров, как мы делаем здесь, обеспечивает предсказуемый результат.  

---

## Шаг 3 – Преобразование HTML в изображение с использованием обработчика ресурсов в памяти

При рендеринге на безголовом сервере часто не требуется, чтобы библиотека записывала временные файлы на диск. Здесь на помощь приходит пользовательский `ResourceHandler`. Ниже показанный обработчик захватывает любые внешние ресурсы (например, шрифты или изображения) в памяти и отбрасывает их — идеально для простых фрагментов.

```csharp
// Define a custom resource handler that stores resources in memory
class MemoryHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info) => new MemoryStream();
}
```

> **How it works:** Каждый раз, когда Aspose требуется получить ресурс (например, внешний CSS‑файл), вызывается `HandleResource`. Возвращая новый `MemoryStream`, мы полностью избегаем ввода‑вывода файловой системы. Если действительно нужно загрузить внешние активы, можно заполнить поток байтами файла.  

---

## Шаг 4 – Создание HTML‑документа и применение стилей

Мы создадим небольшой HTML‑фрагмент непосредственно из строки. Затем, используя DOM‑API, применим стили **жирный и курсив** через `WebFontStyle`. Это демонстрирует, что документ можно изменять так же, как в браузере.

```csharp
// Create an HTML document from a string
var document = new HTMLDocument(
    "<html><body><p style='font-size:20px;'>Hello</p></body></html>");

// Apply bold and italic styling to the paragraph using WebFontStyle
var paragraph = document.QuerySelector("p");
paragraph.Style.Font = new WebFontStyle { Bold = true, Italic = true };
```

> **Why modify the DOM?**  
> Во многих реальных сценариях вы получаете необработанный HTML из базы данных или API. Возможность программно менять стили гарантирует, что конечный PNG будет соответствовать вашим фирменным требованиям без изменения исходной разметки.  

---

## Шаг 5 – Сохранение документа с пользовательским обработчиком памяти

Перед рендерингом мы просим документ **сохранить** себя, используя `MemoryHandler`. Этот шаг не обязателен для рендеринга, но показывает, как можно перехватить процесс сохранения — полезно, если позже планируется передавать PNG напрямую в HTTP‑ответ.

```csharp
// Save the document using the custom memory‑based resource handler
document.Save(new MemoryHandler());
```

> **Note:** Если вам нужен только PNG‑файл, вы можете пропустить вызов `Save`. Мы оставляем его здесь, чтобы показать полный рабочий процесс, включающий как сохранение, так и рендеринг.  

---

## Шаг 6 – Рендеринг документа в PNG‑файл

Наконец, вызываем `RenderToFile`, передавая путь вывода и ранее настроенный `imageOptions`. Метод блокирует выполнение до завершения записи PNG, гарантируя, что файл существует к моменту выполнения следующей строки кода.

```csharp
// Render the document to a PNG file with the configured options
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");
document.RenderToFile(outputPath, imageOptions);

Console.WriteLine($"✅ PNG generated at: {outputPath}");
```

> **Expected output:** PNG‑файл размером 800 × 600 пикселей с именем `output.png`, содержащий текст «Hello» жирный‑курсив, размер шрифта 20 px, центрированный на белом фоне.  

---

## Полный рабочий пример (готовый к копированию)

Ниже представлен весь код программы, готовый к вставке в консольный проект. Дополнительные файлы не требуются.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Saving;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

class MemoryHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info) => new MemoryStream();
}

class Program
{
    static void Main()
    {
        // Step 2 – configure rendering options (set image width height)
        var imageOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            Width = 800,
            Height = 600
        };

        // Step 3 – create HTML document from a string
        var html = "<html><body><p style='font-size:20px;'>Hello</p></body></html>";
        var document = new HTMLDocument(html);

        // Step 4 – apply bold & italic styling
        var paragraph = document.QuerySelector("p");
        paragraph.Style.Font = new WebFontStyle { Bold = true, Italic = true };

        // Step 5 – optional save with custom memory handler
        document.Save(new MemoryHandler());

        // Step 6 – render to PNG
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");
        document.RenderToFile(outputPath, imageOptions);

        Console.WriteLine($"✅ PNG generated at: {outputPath}");
    }
}
```

Запустите программу (`dotnet run`), и PNG появится в папке проекта. Откройте его в любом просмотрщике изображений, чтобы убедиться, что текст жирный‑курсив, а размеры соответствуют заданным значениям.

---

## Часто задаваемые вопросы и подводные камни

| Question | Answer |
|----------|--------|
| **Нужна ли лицензия для пробного использования?** | Aspose.HTML предоставляет 30‑дневную бесплатную пробную версию, работающую без ключа лицензии, но в ней появляется водяной знак. Для продакшна необходимо применить лицензию, чтобы убрать его. |
| **Что делать, если мой HTML ссылается на внешние CSS или изображения?** | Расширьте `MemoryHandler`, чтобы получать эти ресурсы по удалённому URL или встраивать их как массивы байтов. Возврат заполненного `MemoryStream` позволит рендереру использовать их. |
| **Можно ли рендерить в JPEG или GIF вместо PNG?** | Конечно. Измените расширение файла в `RenderToFile` и настройте `ImageRenderingOptions`, задав `OutputFormat = ImageFormat.Jpeg` (или `Gif`). |
| **Требуется ли `UseAntialiasing` в Windows?** | Не обязательно, но он улучшает качество на дисплеях с низким DPI и в безголовых Linux‑контейнерах, где стандартный растеризатор может работать неидеально. |
| **Как передать PNG напрямую в ответ ASP.NET?** | Пропустите вызов `RenderToFile` и используйте `document.Render(imageOptions, stream)`, где `stream` — это `HttpResponse.Body`. Это полностью избавит от ввода‑вывода на диск. |

---

## Следующие шаги и связанные темы

- **Пакетная обработка:** Пройтись по коллекции HTML‑строк и сгенерировать PNG для каждой, переиспользуя один экземпляр `MemoryHandler` для снижения потребления памяти.  
- **Динамический размер:** Использовать `document.Body.GetBoundingClientRect()` для вычисления естественной высоты контента, затем передать эти размеры в `ImageRenderingOptions`.  
- **Встраивание шрифтов:** Загрузить пользовательские веб‑шрифты в `MemoryStream` и назначить их через правила `@font-face`.  

## Что стоит изучить дальше?

- [Как использовать Aspose для рендеринга HTML в PNG – пошаговое руководство](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)  
- [Как рендерить HTML в PNG с Aspose – полное руководство](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)  
- [Рендеринг HTML как PNG в .NET с Aspose.HTML](/html/english/net/rendering-html-documents/render-html-as-png/)  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}