---
title: Точная настройка конвертеров в .NET с помощью Aspose.HTML
linktitle: Точная настройка преобразователей в .NET
second_title: Aspose.HTML .NET API манипулирования HTML
description: Узнайте, как конвертировать HTML в PDF, XPS и изображения с помощью Aspose.HTML для .NET. Пошаговое руководство с примерами кода и часто задаваемыми вопросами.
type: docs
weight: 16
url: /ru/net/advanced-features/fine-tuning-converters/
---

## Введение

Aspose.HTML for .NET — это мощная библиотека, которая позволяет разработчикам манипулировать и конвертировать HTML-документы в различные форматы. Если вам нужно конвертировать HTML в PDF, XPS или изображения или выполнить другие задачи, связанные с HTML, Aspose.HTML предоставляет надежный набор инструментов, которые помогут вам выполнить работу.

В этом руководстве мы рассмотрим некоторые важные функции Aspose.HTML для .NET и предоставим пошаговые объяснения для каждого примера. К концу этого руководства вы получите четкое представление о том, как использовать Aspose.HTML для .NET в ваших .NET-приложениях.

## Предварительные условия

Прежде чем мы углубимся в примеры, убедитесь, что у вас есть следующие предварительные условия:

- Aspose.HTML для .NET: у вас должна быть установлена библиотека Aspose.HTML для .NET. Вы можете скачать его с сайта[ссылка для скачивания](https://releases.aspose.com/html/net/).

-  Временная лицензия (необязательно). Если у вас нет действующей лицензии, вы можете получить временную лицензию на сайте[здесь](https://purchase.aspose.com/temporary-license/).

Теперь давайте рассмотрим некоторые распространенные случаи использования Aspose.HTML для .NET.

## Импортировать пространства имен

В своем коде C# начните с импорта необходимых пространств имен:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Конвертировать HTML в PDF

### Шаг 1. Подготовьте HTML-код

```csharp
var code = @"<span>Hello World!!</span>";
```

### Шаг 2. Инициализируйте HTML-документ

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3. Создайте PDF-устройство и укажите выходной файл

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Шаг 4. Преобразование HTML в PDF

```csharp
document.RenderTo(device);
```

В этом примере фрагмент HTML преобразуется в документ PDF. Вы можете настроить HTML-код и выходной файл по мере необходимости.

## Установить пользовательский размер страницы

### Шаг 1. Подготовьте HTML-код

```csharp
var code = @"<span>Hello World!!</span>";
```

### Шаг 2. Инициализируйте HTML-документ

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3. Создайте параметры рендеринга PDF

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

### Шаг 4. Создайте PDF-устройство, укажите параметры и выходной файл.

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Шаг 5. Преобразование HTML в PDF

```csharp
document.RenderTo(device);
```

В этом примере показано, как установить собственный размер страницы для полученного PDF-документа.

## Настроить разрешение

### Шаг 1. Подготовьте HTML-код и сохраните его в файл.

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

### Шаг 2. Инициализируйте HTML-документ

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Шаг 3. Создайте параметры рендеринга PDF для низкого разрешения

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Шаг 4. Создайте PDF-устройство, укажите параметры и выходной файл для низкого разрешения.

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Шаг 5. Преобразование HTML в PDF для низкого разрешения

```csharp
document.RenderTo(device);
```

### Шаг 6. Создайте параметры рендеринга PDF для высокого разрешения

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Шаг 7. Создайте PDF-устройство, укажите параметры и выходной файл для высокого разрешения.

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Шаг 8. Преобразование HTML в PDF для высокого разрешения

```csharp
document.RenderTo(device);
```

В этом примере показано, как настроить разрешение при рендеринге HTML в PDF с учетом экранов как с низким, так и с высоким разрешением.

## Укажите цвет фона

### Шаг 1. Подготовьте HTML-код и сохраните его в файл.

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Шаг 2. Инициализируйте HTML-документ

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Шаг 3. Инициализация параметров рендеринга PDF с использованием цвета фона

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Шаг 4. Создайте PDF-устройство, укажите параметры и выходной файл.

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Шаг 5. Преобразование HTML в PDF

```csharp
document.RenderTo(device);
```

В этом примере показано, как указать цвет фона при преобразовании HTML в PDF.

## Установите размеры левой и правой страницы

### Шаг 1. Подготовьте HTML-код

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Шаг 2. Инициализируйте HTML-документ

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3. Создайте параметры рендеринга PDF с размерами левой и правой страниц.

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Шаг 4. Создайте PDF-устройство, укажите параметры и выходной файл.

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Шаг 5. Преобразование HTML в PDF

```csharp
document.RenderTo(device);
```

В этом примере показано, как установить разные размеры левой и правой страниц при преобразовании HTML в PDF.

## Отрегулируйте размер страницы в соответствии с содержимым

### Шаг 1. Подготовьте HTML-код

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Шаг 2. Инициализируйте HTML-документ

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3. Создайте параметры рендеринга PDF

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Шаг 4. Создайте PDF-устройство, укажите параметры и выходной файл.

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Шаг 5. Преобразование HTML в PDF

```csharp
document.RenderTo(device);
```

В этом примере показано, как настроить размер страницы для самого широкого содержимого при преобразовании HTML в PDF.

## Укажите разрешения PDF

### Шаг 1. Подготовьте HTML-код

```csharp
var code = @"<div>Hello World!!</div>";
```

### Шаг 2. Инициализируйте HTML-документ

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3. Создайте параметры рендеринга PDF с разрешениями

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Шаг 4. Создайте PDF-устройство, укажите параметры и выходной файл.

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Шаг 5. Преобразование HTML в PDF

```csharp
document.RenderTo(device);
```

В этом примере показано, как указать разрешения и шифрование при преобразовании HTML в защищенный PDF-файл.

## Укажите параметры для конкретного изображения

### Шаг 1. Подготовьте HTML-код

```csharp
var code = @"<div>Hello World!!</div>";
```

### Шаг 2. Инициализируйте HTML-документ

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3. Создайте параметры рендеринга изображения

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Шаг 4. Создайте устройство образа, укажите параметры и выходной файл.

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Шаг 5. Преобразование HTML в изображение

```csharp
document.RenderTo(device);
```

В этом примере показано, как преобразовать HTML в изображение с определенными параметрами рендеринга, такими как формат, разрешение и режим сглаживания.

## Укажите параметры рендеринга XPS

### Шаг 1. Подготовьте HTML-код

```csharp
var code = @"<span>Hello World!!</span>";
```

### Шаг 2. Инициализируйте HTML-документ

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3. Создайте параметры рендеринга XPS с размером страницы

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Шаг 4. Создайте устройство XPS, укажите параметры и выходной файл.

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Шаг 5. Преобразование HTML в XPS

```csharp
document.RenderTo(device);
```

В этом примере показано, как преобразовать HTML в XPS с настраиваемым размером страницы и параметрами рендеринга.

## Объедините несколько HTML-документов в PDF

### Шаг 1. Подготовьте HTML-код для нескольких документов

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Шаг 2. Создайте HTML-документы для объединения

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Шаг 3. Инициализируйте средство HTML-рендеринга

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Шаг 4. Создайте PDF-устройство для объединенного вывода

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Шаг 5. Объединение HTML-документов в PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

В этом примере показано, как объединить несколько документов HTML в один файл PDF с помощью Aspose.HTML для .NET.

## Установить тайм-аут рендеринга

### Шаг 1. Подготовьте HTML-код с помощью JavaScript

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

### Шаг 2. Инициализируйте HTML-документ

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Шаг 3. Инициализируйте средство HTML-рендеринга

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Шаг 4. Создайте PDF-устройство и установите тайм-аут рендеринга

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Шаг 5. Преобразование HTML в PDF с тайм-аутом

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

В этом примере показано, как установить тайм-аут рендеринга при преобразовании HTML в PDF, что может быть полезно при работе с динамическим содержимым или долго выполняющимися скриптами.

## Заключение

Aspose.HTML for .NET — это универсальная библиотека, которая позволяет разработчикам эффективно работать с HTML-документами. В этом руководстве мы рассмотрели различные примеры: от базового преобразования HTML в PDF до более продвинутых функций, таких как пользовательские размеры страниц, разрешения и разрешения. Следуя этим примерам, вы сможете использовать весь потенциал Aspose.HTML для .NET в своих .NET-приложениях.

 Если у вас есть какие-либо вопросы или вам нужна дополнительная помощь, не стесняйтесь посетить[Форум Aspose.HTML](https://forum.aspose.com/) за поддержку и руководство.

## Часто задаваемые вопросы

### Вопрос 1. Что такое Aspose.HTML для .NET?
   
A1: Aspose.HTML for .NET — это библиотека .NET, которая позволяет разработчикам программно манипулировать и преобразовывать HTML-документы. Он предлагает широкий спектр функций для работы с HTML-контентом, включая преобразование HTML в PDF, XPS и изображений, а также расширенные возможности рендеринга.

### В2. Где я могу скачать Aspose.HTML для .NET?

 A2: Вы можете скачать Aspose.HTML для .NET с сайта[ссылка для скачивания](https://releases.aspose.com/html/net/).

### Вопрос 3. Нужна ли мне лицензия для использования Aspose.HTML для .NET?

О3: Хотя вы можете использовать Aspose.HTML для .NET без лицензии, рекомендуется получить лицензию для промышленного использования, чтобы разблокировать все функции и удалить любые водяные знаки или ограничения.

### Вопрос 4. Как я могу защитить свои PDF-файлы, созданные с помощью Aspose.HTML для .NET?

A4: Вы можете указать разрешения PDF и настройки шифрования при рендеринге HTML в PDF с помощью Aspose.HTML для .NET. Это позволяет вам контролировать, кто может получать доступ к полученным PDF-файлам и изменять их.

### Вопрос 5. Могу ли я конвертировать HTML в другие форматы, такие как XPS или изображения?

О5: Да, Aspose.HTML для .NET поддерживает преобразование HTML в различные форматы, включая PDF, XPS и изображения (например, JPEG). Вы можете настроить параметры преобразования в соответствии с вашими конкретными требованиями.