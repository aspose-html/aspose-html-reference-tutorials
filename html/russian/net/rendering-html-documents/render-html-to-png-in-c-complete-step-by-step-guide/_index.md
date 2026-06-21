---
category: general
date: 2026-02-21
description: Быстро преобразуйте HTML в PNG с помощью Aspose.HTML. Узнайте, как конвертировать
  HTML в изображение, задать ширину и высоту изображения и сохранить HTML как PNG
  в несколько строк кода C#.
draft: false
keywords:
- render html to png
- convert html to image
- save html as png
- set image width height
- generate png from html
language: ru
og_description: Отображайте HTML в PNG с помощью Aspose.HTML. Этот учебник показывает,
  как преобразовать HTML в изображение, установить ширину и высоту изображения и сохранить
  HTML как PNG в C#.
og_title: Рендеринг HTML в PNG на C# – Полное руководство
tags:
- Aspose.HTML
- C#
- Image Rendering
title: Преобразование HTML в PNG в C# – Полное пошаговое руководство
url: /ru/net/rendering-html-documents/render-html-to-png-in-c-complete-step-by-step-guide/
---

output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование HTML в PNG – Полное пошаговое руководство

Когда‑нибудь вам нужно было **преобразовать HTML в PNG**, но вы не знали, какую библиотеку выбрать или как настроить вывод? Вы не одиноки. Многие разработчики сталкиваются с тем же, когда пытаются *преобразовать HTML в изображение* для миниатюр писем, снимков отчётов или автоматизированного UI‑тестирования.  

В этом руководстве мы пройдём практический, готовый к запуску пример, который покажет, как **сохранить HTML как PNG**, управлять размерами изображения и настраивать качество рендеринга — все это с помощью нескольких строк кода Aspose.HTML для .NET. К концу вы получите переиспользуемый фрагмент, который можно вставить в любой проект на C#.

## Что вам понадобится

Прежде чем начать, убедитесь, что у вас есть:

- **.NET 6.0 или новее** (API работает с .NET Framework, .NET Core и .NET 5+)
- NuGet‑пакет **Aspose.HTML for .NET** (`Aspose.Html`) установлен в вашем проекте.
- Базовое понимание синтаксиса C# — ничего сложного не требуется.
- Папка вывода, куда будет записан сгенерированный PNG.

И всё. Никаких дополнительных SDK, никаких внешних бинарных файлов, только одна ссылка на NuGet.

## Преобразование HTML в PNG – Создание документа

Первое, что мы делаем, — создаём объект `HTMLDocument`, содержащий разметку, которую хотим растеризовать. HTML можно загрузить из строки, файла или даже URL. Для ясности начнём с простой встроенной строки.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;
using System.Drawing;   // for Color

// Step 1: Create an HTML document with sample content
HTMLDocument htmlDoc = new HTMLDocument(
    "<html><body><p style='font-family:Arial; font-size:24px;'>Sample text</p></body></html>");
```

> **Почему это важно:** Используя `HTMLDocument`, мы позволяем Aspose.HTML обрабатывать парсинг CSS, раскладку и разрешение шрифтов точно так же, как браузер. Это гарантирует, что полученный PNG будет выглядеть идентично тому, что пользователь видит в Chrome или Edge.

## Преобразование HTML в изображение – Настройка параметров рендеринга

Далее мы определяем, как движок должен растеризовать разметку. Здесь вы **указываете ширину и высоту изображения**, включаете сглаживание и выбираете цвет фона.

```csharp
// Step 2: Set up image rendering options (antialiasing, hinting, background, size)
ImageRenderingOptions renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,                 // smoother edges for shapes and text
    TextOptions = { UseHinting = true },    // clearer glyph shapes on high‑DPI
    BackColor = Color.White,                // solid white background (transparent also works)
    Width = 800,                            // set image width
    Height = 600                            // set image height
};
```

> **Совет профессионала:** Если опустить `Width` и `Height`, Aspose.HTML использует внутренний размер страницы, который может быть слишком маленьким для миниатюр. Явное задание этих значений даёт полный контроль над конечными размерами PNG.

## Генерация PNG из HTML – Применение стилей шрифтов (по желанию)

Иногда нужны жирный, курсивный или комбинированный стиль. Перечисление `WebFontStyle` позволяет объединять флаги с помощью побитового ИЛИ (`|`). Этот шаг необязателен, но демонстрирует, как **генерировать PNG из HTML** с пользовательским стилизацией.

```csharp
// Step 3: Combine desired font styles using the WebFontStyle enum
WebFontStyle combinedFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

// Step 4: Apply the combined font style to the document via CSS
htmlDoc.Body.Style.FontStyle = combinedFontStyle.ToString(); // enum → CSS string
```

> **Что происходит:** `combinedFontStyle.ToString()` возвращает `"Bold, Italic"`, что движок переводит в корректное CSS‑значение `font-style`. В результате получаем PNG, где текст отображается одновременно жирным и курсивным.

## Сохранение HTML как PNG – Финальный вызов рендеринга

Теперь собираем всё вместе. Рендерер `Image` записывает растеризованное содержимое в файл на диске.

```csharp
// Step 5: Render the HTML document to a PNG image file
using (Image renderer = new Image())
{
    renderer.Save(htmlDoc, renderingOptions, "output.png");
}
```

Запуск программы создаёт `output.png` в рабочем каталоге. Откройте его, и вы увидите результат **render html to png** — чёткий, сглаженный текст на белом фоне, точно 800 × 600 пикселей.

![пример вывода render html to png](output.png)

> **Ожидаемый результат:** PNG‑файл, показывающий «Sample text» 24‑px Arial, жирный и курсивный, центрированный в изображении. Если изменить строку HTML или значения `Width`/`Height`, PNG обновится соответственно.

## Преобразование HTML в изображение – Распространённые варианты и граничные случаи

### 1. Рендеринг удалённой веб‑страницы

Если нужно **преобразовать HTML в изображение** из живого URL, просто передайте URL в `HTMLDocument`:

```csharp
HTMLDocument remoteDoc = new HTMLDocument("https://example.com");
renderer.Save(remoteDoc, renderingOptions, "remote.png");
```

Убедитесь, что целевой сайт разрешает программный доступ (CORS, аутентификация и т.д.).

### 2. Прозрачные фоны

Установите `BackColor = Color.Transparent` и выберите формат PNG, поддерживающий альфа‑каналы. Это удобно для наложения изображения на другие UI‑элементы.

### 3. Вывод высокого разрешения

Для графики, готовой к печати, увеличьте `Width` и `Height`, одновременно задав `DPI`:

```csharp
renderingOptions.DpiX = 300;
renderingOptions.DpiY = 300;
renderingOptions.Width = 2400;   // 8 × 300 dpi
renderingOptions.Height = 1800;  // 6 × 300 dpi
```

### 4. Работа с большими таблицами стилей

Aspose.HTML автоматически загружает связанные CSS‑файлы. Если хотите ограничить сетевые запросы, внедрите критический CSS непосредственно в строку HTML или используйте `ResourceLoadingOptions` для кэширования ресурсов.

## Полный, готовый к запуску пример

Ниже представлена полная программа, которую можно скопировать и вставить в консольное приложение. В ней собраны все шаги, комментарии и необязательные настройки, обсуждённые выше.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;
using System.Drawing;   // for Color

namespace HtmlToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the HTML document (inline string for demo)
            HTMLDocument htmlDoc = new HTMLDocument(
                "<html><body>" +
                "<h1 style='font-family:Arial; color:#2E86C1;'>Aspose.HTML Demo</h1>" +
                "<p style='font-family:Arial; font-size:24px;'>Sample text</p>" +
                "</body></html>");

            // 2️⃣ Configure rendering options – this is where we **set image width height**
            ImageRenderingOptions renderingOptions = new ImageRenderingOptions
            {
                UseAntialiasing = true,
                TextOptions = { UseHinting = true },
                BackColor = Color.White,
                Width = 800,
                Height = 600
            };

            // 3️⃣ (Optional) Apply combined font style – bold + italic
            WebFontStyle combinedStyle = WebFontStyle.Bold | WebFontStyle.Italic;
            htmlDoc.Body.Style.FontStyle = combinedStyle.ToString();

            // 4️⃣ Render and **save HTML as PNG**
            using (Image renderer = new Image())
            {
                renderer.Save(htmlDoc, renderingOptions, "output.png");
            }

            // 5️⃣ Let the user know we’re done
            System.Console.WriteLine("✅ PNG generated: output.png");
        }
    }
}
```

Скомпилируйте и запустите (`dotnet run`, если используете .NET CLI). Консоль подтвердит создание файла, а `output.png` появится рядом с исполняемым файлом.

## Итоги

Мы рассмотрели всё, что нужно для **преобразования HTML в PNG** с помощью Aspose.HTML в C#. От создания документа, настройки параметров рендеринга, применения пользовательских стилей шрифтов до финального сохранения изображения — каждый шаг объяснялся **почему** он важен, а не только **как** его выполнить.  

Если вам нужно **преобразовать HTML в изображение** в других форматах, просто измените расширение файла в `renderer.Save` на `.jpeg` или `.bmp` и скорректируйте `ImageSaveOptions` соответственно. Хотите пакетную обработку десятков страниц? Оберните блок рендеринга в цикл `foreach` и передавайте каждую строку HTML или URL.

### Что дальше?

- **Изучите генерацию PDF** — Aspose.HTML также умеет экспортировать в PDF с похожими параметрами.
- **Объединяйте несколько страниц** — рендерьте каждую страницу многостраничного HTML‑документа в отдельные PNG.
- **Интеграция с ASP.NET Core** — возвращайте PNG напрямую как `FileResult` для мгновенных скриншотов.

Экспериментируйте с настройками, меняйте HTML‑контент или внедряйте этот код в веб‑службу. Возможности безграничны, когда вы можете **генерировать PNG из HTML** «на лету».

Есть вопросы или сложный кейс? Оставляйте комментарий ниже, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}