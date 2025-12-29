---
category: general
date: 2025-12-29
description: Создайте HTML‑документ на C# и узнайте, как задать семейство шрифтов,
  установить размер шрифта, затем сохранить HTML как PDF или преобразовать HTML в
  PDF с помощью Aspose.HTML.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: ru
og_description: Создайте HTML‑документ на C# и мгновенно посмотрите, как задать семейство
  шрифтов, установить размер шрифта, затем сохранить HTML как PDF или преобразовать
  HTML в PDF с помощью Aspose.HTML.
og_title: Создать HTML‑документ – стилизованный текст и экспорт в PDF
tags:
- aspnet
- csharp
- pdf-generation
title: Создайте HTML‑документ со стилизованным текстом и экспортируйте в PDF — полное
  руководство
url: /ru/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание HTML‑документа со стилизованным текстом и экспорт в PDF

Когда‑нибудь нужно **создать HTML‑документ** «на лету» и превратить его в PDF, не выходя из кода C#? Возможно, вы разрабатываете движок отчётности, генератор счетов‑фактур или просто быстрый предварительный просмотр для пользователей. Хорошая новость: это можно сделать в пару строк с помощью Aspose.HTML, получив полный контроль над семейством шрифтов, размером шрифта и даже стилями полужирный‑курсив.

В этом руководстве мы пройдём весь процесс — от создания HTML‑документа в памяти до сохранения его в виде PDF‑файла. К концу вы точно будете знать, как **установить семейство шрифта**, **установить размер шрифта** и **сохранить HTML как PDF** (также известное как **конвертировать HTML в PDF**) с чистым, готовым к продакшну примером кода.

## Что понадобится

- .NET 6+ (API работает как с .NET Core, так и с .NET Framework)  
- NuGet‑пакет Aspose.HTML for .NET (`Aspose.Html`) — установите через `dotnet add package Aspose.Html`  
- Папка на диске, куда можно записать сгенерированный PDF  

Никаких внешних HTML‑шаблонов, никаких сторонних конвертеров, только чистый C#.

![создание HTML документа иллюстрация](/images/create-html-document.png){alt="пример создания HTML документа"}

## Шаг 1: Создание HTML‑документа

Сначала нам нужен пустой объект HTML‑документа. Представьте его как чистый холст, на котором позже будет нарисован ваш стилизованный абзац.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Почему это важно:** `HTMLDocument` предоставляет структуру, похожую на DOM, которую можно программно изменять. Нет необходимости работать со строками или файловым вводом‑выводом до самого конца.

## Шаг 2: Добавление абзаца и установка семейства шрифта и размера

Теперь создадим элемент `<p>`, вставим в него текст и явно зададим семейство шрифта и размер. Здесь в игру вступают ключевые слова **set font family** и **set font size**.

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Совет:** Если нужен безопасный запасной шрифт, можно указать список через запятую, например `"Arial, Helvetica, sans-serif"`; браузер (или Aspose) выберет первый доступный шрифт.

## Шаг 3: Применение полужирного и курсивного стилей с помощью флагов WebFontStyle

Aspose.HTML предоставляет удобный enum `WebFontStyle`, позволяющий комбинировать стили с помощью побитового ИЛИ. Сделаем текст одновременно полужирным **и** курсивным.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**Что происходит под капотом?** Свойство `FontStyle` преобразуется в CSS‑объявления `font-weight` и `font-style`. Объединяя флаги, мы избегаем написания двух отдельных строк CSS.

## Шаг 4: Конвертация HTML в PDF (Save HTML as PDF)

Последний шаг — сама конвертация. Одним вызовом `Save` Aspose.HTML рендерит DOM и записывает PDF‑файл на диск. Это покрывает требования **save html as pdf** и **convert html to pdf**.

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Ожидаемый результат:** Откройте `styled.pdf`, и вы увидите один абзац с текстом «Bold & Italic text» размером 18 px Arial, отрисованный полужирным и курсивным. Размеры PDF соответствуют стандартному листу A4, а текст можно выделять — благодаря векторному рендерингу.

## Полный рабочий пример

Объединив всё вместе, получаем полностью готовую к запуску программу:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### Запуск кода

1. Установите NuGet‑пакет Aspose.HTML:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. Замените `C:\Temp\styled.pdf` на путь к папке, в которую у вас есть права записи.  
3. Соберите и запустите: `dotnet run`.  

Вы увидите сообщение в консоли с подтверждением пути к файлу, а PDF будет содержать стилизованный абзац.

## Часто задаваемые вопросы и особые случаи

- **Что делать, если нужен пользовательский веб‑шрифт?**  
  Загрузите шрифт с помощью `HTMLFontFaceRule` или подключите удалённый файл `@font-face` CSS перед созданием абзаца.

- **Можно ли добавить изображения перед конвертацией?**  
  Конечно. Используйте `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` и задайте `img.Source` на локальный путь или data‑URI.

- **Как работать с многостраничными PDF?**  
  Добавляйте больше элементов (таблицы, div‑ы и т.д.), и Aspose.HTML автоматически разбивает содержимое на страницы, когда высота превышает размер листа.

- **Можно ли управлять метаданными PDF?**  
  Передайте экземпляр `PdfSaveOptions` и задайте свойства, такие как `Author`, `Title` или `PdfAConformanceLevel`.

## Итоги

Мы рассмотрели, как **создать HTML‑документ** в C#, **установить семейство шрифта**, **установить размер шрифта**, применить полужирный‑курсивный стиль и, наконец, **сохранить HTML как PDF** — по сути **конвертировать HTML в PDF** с помощью Aspose.HTML. Этот фрагмент кода достаточно короток, чтобы вставить его в любой .NET‑проект, но при этом достаточно полон, чтобы служить надёжной основой для более сложных сценариев отчётности.

## Следующие шаги

- Поэкспериментируйте с CSS‑классами для переиспользуемых стилей.  
- Объединяйте несколько абзацев, таблиц и изображений для создания более насыщенных PDF.  
- Изучите соответствие PDF/A, если нужны архивные документы.  

Не стесняйтесь менять шрифт, размер или цвета — возможности генерации программно ограничены только вашим воображением. Приятного кодинга, и пусть ваши PDF всегда отображаются точно так, как вы задумали!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}