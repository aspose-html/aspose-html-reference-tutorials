---
title: Тонкая настройка конвертеров в .NET с помощью Aspose.HTML
linktitle: Тонкая настройка конвертеров в .NET
second_title: API манипуляции HTML Aspose.HTML .NET
description: Узнайте, как преобразовать HTML в PDF, XPS и изображения с помощью Aspose.HTML для .NET. Пошаговое руководство с примерами кода и часто задаваемыми вопросами.
weight: 16
url: /ru/net/advanced-features/fine-tuning-converters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Тонкая настройка конвертеров в .NET с помощью Aspose.HTML


## Введение

Aspose.HTML для .NET — это мощная библиотека, которая позволяет разработчикам манипулировать и конвертировать HTML-документы в различных форматах. Если вам нужно конвертировать HTML в PDF, XPS или изображения или выполнить другие задачи, связанные с HTML, Aspose.HTML предоставляет надежный набор инструментов, которые помогут вам выполнить работу.

В этом уроке мы рассмотрим некоторые основные функции Aspose.HTML для .NET и предоставим пошаговые объяснения для каждого примера. К концу этого урока у вас будет четкое понимание того, как использовать Aspose.HTML для .NET в ваших приложениях .NET.

## Предпосылки

Прежде чем мы углубимся в примеры, убедитесь, что у вас выполнены следующие предварительные условия:

-  Aspose.HTML for .NET: У вас должна быть установлена библиотека Aspose.HTML for .NET. Вы можете загрузить ее с[ссылка для скачивания](https://releases.aspose.com/html/net/).

-  Временная лицензия (необязательно): Если у вас нет действующей лицензии, вы можете получить временную лицензию у[здесь](https://purchase.aspose.com/temporary-license/).

Теперь давайте рассмотрим некоторые распространенные варианты использования Aspose.HTML для .NET.

## Импорт пространств имен

В коде C# начните с импорта необходимых пространств имен:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Конвертировать HTML в PDF

### Шаг 1: Подготовка HTML-кода

```csharp
var code = @"<span>Hello World!!</span>";
```

### Шаг 2: Инициализация HTML-документа

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3: Создайте PDF-устройство и укажите выходной файл

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Шаг 4: Преобразование HTML в PDF

```csharp
document.RenderTo(device);
```

Этот пример преобразует фрагмент HTML в документ PDF. Вы можете настроить код HTML и выходной файл по мере необходимости.

## Установить пользовательский размер страницы

### Шаг 1: Подготовка HTML-кода

```csharp
var code = @"<span>Hello World!!</span>";
```

### Шаг 2: Инициализация HTML-документа

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3: Создайте параметры рендеринга PDF-файла

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### Шаг 4: Создайте PDF-устройство и укажите параметры и выходной файл

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Шаг 5: Преобразование HTML в PDF

```csharp
document.RenderTo(device);
```

В этом примере показано, как задать индивидуальный размер страницы для итогового PDF-документа.

## Настроить разрешение

### Шаг 1: Подготовьте HTML-код и сохраните его в файле

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Шаг 2: Инициализация HTML-документа

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Шаг 3: Создайте параметры рендеринга PDF для низкого разрешения

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Шаг 4: Создайте устройство PDF и укажите параметры и выходной файл для низкого разрешения

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Шаг 5: Преобразование HTML в PDF для низкого разрешения

```csharp
document.RenderTo(device);
```

### Шаг 6: Создайте параметры рендеринга PDF для высокого разрешения

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Шаг 7: Создайте устройство PDF и укажите параметры и выходной файл для высокого разрешения

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Шаг 8: Преобразование HTML в PDF для получения высокого разрешения

```csharp
document.RenderTo(device);
```

В этом примере показано, как настроить разрешение при преобразовании HTML в PDF, учитывая экраны как с низким, так и с высоким разрешением.

## Укажите цвет фона

### Шаг 1: Подготовьте HTML-код и сохраните его в файле

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Шаг 2: Инициализация HTML-документа

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Шаг 3: Инициализация параметров рендеринга PDF с помощью цвета фона

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Шаг 4: Создайте PDF-устройство и укажите параметры и выходной файл

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Шаг 5: Преобразование HTML в PDF

```csharp
document.RenderTo(device);
```

В этом примере показано, как указать цвет фона при конвертации HTML в PDF.

## Установить размеры левой и правой страницы

### Шаг 1: Подготовка HTML-кода

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Шаг 2: Инициализация HTML-документа

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3: Создайте параметры рендеринга PDF с размерами левой и правой страницы

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Шаг 4: Создайте PDF-устройство и укажите параметры и выходной файл

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Шаг 5: Преобразование HTML в PDF

```csharp
document.RenderTo(device);
```

В этом примере показано, как установить разные размеры страниц для левой и правой страниц при конвертации HTML в PDF.

## Отрегулируйте размер страницы в соответствии с содержимым

### Шаг 1: Подготовка HTML-кода

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Шаг 2: Инициализация HTML-документа

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3: Создайте параметры рендеринга PDF-файла

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Шаг 4: Создайте PDF-устройство и укажите параметры и выходной файл

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Шаг 5: Преобразование HTML в PDF

```csharp
document.RenderTo(device);
```

В этом примере показано, как подогнать размер страницы под максимально широкое содержимое при конвертации HTML в PDF.

## Укажите разрешения PDF

### Шаг 1: Подготовка HTML-кода

```csharp
var code = @"<div>Hello World!!</div>";
```

### Шаг 2: Инициализация HTML-документа

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3: Создайте параметры рендеринга PDF с разрешениями

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Шаг 4: Создайте PDF-устройство и укажите параметры и выходной файл

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Шаг 5: Преобразование HTML в PDF

```csharp
document.RenderTo(device);
```

В этом примере показано, как указать разрешения и шифрование при преобразовании HTML в защищенный PDF.

## Укажите параметры, специфичные для изображения

### Шаг 1: Подготовка HTML-кода

```csharp
var code = @"<div>Hello World!!</div>";
```

### Шаг 2: Инициализация HTML-документа

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3: Создание параметров рендеринга изображения

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Шаг 4: Создайте устройство изображения и укажите параметры и выходной файл

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Шаг 5: Преобразование HTML в изображение

```csharp
document.RenderTo(device);
```

В этом примере показано, как преобразовать HTML в изображение с определенными параметрами рендеринга, такими как формат, разрешение и режим сглаживания.

## Укажите параметры рендеринга XPS

### Шаг 1: Подготовка HTML-кода

```csharp
var code = @"<span>Hello World!!</span>";
```

### Шаг 2: Инициализация HTML-документа

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3: Создание параметров рендеринга XPS с учетом размера страницы

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Шаг 4: Создайте устройство XPS и укажите параметры и выходной файл

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Шаг 5: Преобразование HTML в XPS

```csharp
document.RenderTo(device);
```

В этом примере показано, как преобразовать HTML в XPS с пользовательскими размерами страницы и параметрами рендеринга.

## Объединить несколько HTML-документов в PDF

### Шаг 1: Подготовка HTML-кода для нескольких документов

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Шаг 2: Создание HTML-документов для слияния

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Шаг 3: Инициализация HTML-рендерера

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Шаг 4: Создайте устройство PDF для объединенного вывода

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Шаг 5: Объедините HTML-документы в PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

В этом примере показано, как объединить несколько HTML-документов в один PDF-файл с помощью Aspose.HTML для .NET.

## Установить тайм-аут рендеринга

### Шаг 1: Подготовка HTML-кода с помощью JavaScript

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### Шаг 2: Инициализация HTML-документа

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3: Инициализация HTML-рендерера

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Шаг 4: Создайте устройство PDF и установите время ожидания рендеринга

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Шаг 5: Преобразование HTML в PDF с тайм-аутом

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

В этом примере показано, как установить тайм-аут рендеринга при конвертации HTML в PDF, что может быть полезно при работе с динамическим контентом или длительными скриптами.

## Заключение

Aspose.HTML для .NET — это универсальная библиотека, которая позволяет разработчикам эффективно работать с HTML-документами. В этом руководстве мы рассмотрели различные примеры, от базовых преобразований HTML в PDF до более продвинутых функций, таких как пользовательские размеры страниц, разрешения и разрешения. Следуя этим примерам, вы сможете использовать весь потенциал Aspose.HTML для .NET в своих приложениях .NET.

 Если у вас есть какие-либо вопросы или вам нужна дополнительная помощь, не стесняйтесь посетить[Форум Aspose.HTML](https://forum.aspose.com/) за поддержку и руководство.

## Часто задаваемые вопросы

### В1. Что такое Aspose.HTML для .NET?
   
A1: Aspose.HTML для .NET — это библиотека .NET, которая позволяет разработчикам программно манипулировать и преобразовывать HTML-документы. Она предлагает широкий спектр функций для работы с HTML-контентом, включая HTML в PDF, XPS и преобразование изображений, а также расширенные параметры рендеринга.

### В2. Где я могу скачать Aspose.HTML для .NET?

 A2: Вы можете загрузить Aspose.HTML для .NET с сайта[ссылка для скачивания](https://releases.aspose.com/html/net/).

### В3. Нужна ли мне лицензия для использования Aspose.HTML для .NET?

A3: Хотя вы можете использовать Aspose.HTML для .NET без лицензии, рекомендуется получить лицензию для производственного использования, чтобы разблокировать все функции и удалить все водяные знаки или ограничения.

### В4. Как защитить мои PDF-файлы, созданные с помощью Aspose.HTML для .NET?

A4: Вы можете указать разрешения PDF и настройки шифрования при рендеринге HTML в PDF с помощью Aspose.HTML для .NET. Это позволяет вам контролировать, кто может получать доступ и изменять полученные файлы PDF.

### В5. Могу ли я конвертировать HTML в другие форматы, такие как XPS или изображения?

A5: Да, Aspose.HTML для .NET поддерживает преобразование HTML в различные форматы, включая PDF, XPS и изображения (например, JPEG). Вы можете настроить параметры преобразования в соответствии с вашими конкретными требованиями.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
