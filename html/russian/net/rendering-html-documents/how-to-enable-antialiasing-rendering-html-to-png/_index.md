---
category: general
date: 2026-07-08
description: Узнайте, как включить сглаживание при рендеринге HTML в PNG с помощью
  Aspose HTML. В этом руководстве также рассматривается преобразование HTML в изображение
  и сохранение HTML в формате PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- render html to png
- convert html to image
- save html as png
- aspose html to png
language: ru
lastmod: 2026-07-08
og_description: Как включить сглаживание при рендеринге HTML в PNG с помощью Aspose
  HTML. Следуйте этому пошаговому руководству, чтобы преобразовать HTML в изображение
  и сохранить HTML как PNG.
og_image_alt: Screenshot of HTML rendered to PNG with antialiasing enabled – how to
  enable antialiasing
og_title: Как включить сглаживание при рендеринге HTML в PNG – руководство Aspose
schemas:
- author: Aspose
  dateModified: '2026-07-08'
  description: Learn how to enable antialiasing when you render HTML to PNG using
    Aspose HTML. This guide also covers convert html to image and save html as png.
  headline: How to Enable Antialiasing Rendering HTML to PNG
  type: TechArticle
- description: Learn how to enable antialiasing when you render HTML to PNG using
    Aspose HTML. This guide also covers convert html to image and save html as png.
  name: How to Enable Antialiasing Rendering HTML to PNG
  steps:
  - name: '**HTMLDocument** – works entirely in memory, so you don’t need any physical
      `.html` files. Perfect for on‑the‑fly conversions.'
    text: '**HTMLDocument** – works entirely in memory, so you don’t need any physical
      `.html` files. Perfect for on‑the‑fly conversions.'
  - name: '**WebFontStyle** – shows that you can style text before rendering; the
      bold‑italic combo is just a demo.'
    text: '**WebFontStyle** – shows that you can style text before rendering; the
      bold‑italic combo is just a demo.'
  - name: '**ImageRenderingOptions.UseAntialiasing** – this flag is the answer to
      **how to enable antialiasing**; set it to `true` and the rasterizer will smooth
      edges.'
    text: '**ImageRenderingOptions.UseAntialiasing** – this flag is the answer to
      **how to enable antialiasing**; set it to `true` and the rasterizer will smooth
      edges.'
  - name: '**TextOptions.UseHinting** – hinting improves the clarity of glyphs, especially
      at small sizes. It’s a nice companion to antialiasing.'
    text: '**TextOptions.UseHinting** – hinting improves the clarity of glyphs, especially
      at small sizes. It’s a nice companion to antialiasing.'
  - name: '**ImageSaveOptions** – bundles both rendering and text options, then tells
      Aspose to output a PNG file.'
    text: '**ImageSaveOptions** – bundles both rendering and text options, then tells
      Aspose to output a PNG file.'
  type: HowTo
tags:
- Aspose
- C#
- Image Rendering
title: Как включить сглаживание при рендеринге HTML в PNG
url: /ru/net/rendering-html-documents/how-to-enable-antialiasing-rendering-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как включить сглаживание при рендеринге HTML в PNG

Когда‑нибудь задумывались **как включить сглаживание** при преобразовании веб‑страницы в чёткое PNG‑изображение? Вы не одиноки — многие разработчики сталкиваются с проблемой, когда результат выглядит зубчатым или размытым. Хорошая новость в том, что с Aspose.HTML вы можете сгладить эти края всего за несколько строк кода. В этом руководстве мы пройдём по точным шагам, как рендерить HTML в PNG, конвертировать HTML в изображение и, наконец, **сохранить HTML как PNG** с включённым сглаживанием.

> **Что вы получите:** полностью готовый к запуску пример на C#, объяснение каждой опции и советы по работе с крайними случаями, такими как пользовательские шрифты или большие страницы.

## Как включить сглаживание при рендеринге HTML в PNG

Первое, что нужно понять, — **почему сглаживание важно**. Когда движок рендеринга рисует формы или текст, он приближает кривые пикселями. Без сглаживания эти приближения создают артефакты «ступенчатости», особенно заметные на диагональных линиях или тонких шрифтах. Включение сглаживания заставляет движок смешивать соседние пиксели, получая более плавный визуальный результат.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;

// Step 1: Create an in‑memory HTML document
HTMLDocument htmlDoc = new HTMLDocument("<html><body><h1>Sample</h1></body></html>");

// Step 2: Define the desired font style (bold + italic)
WebFontStyle fontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

// Step 3: Configure image rendering options – enable antialiasing for smoother graphics
ImageRenderingOptions imageOpts = new ImageRenderingOptions();
imageOpts.UseAntialiasing = true;

// Step 4: Configure text rendering options – enable hinting for clearer text
TextOptions textOpts = new TextOptions();
textOpts.UseHinting = true;

// Step 5: Combine rendering and text options into PNG save options
ImageSaveOptions pngSaveOpts = new ImageSaveOptions(SaveFormat.Png)
{
    RenderingOptions = imageOpts,
    TextOptions = textOpts
};

// Step 6: Save the HTML document as a PNG image using the configured options
htmlDoc.Save("YOUR_DIRECTORY/sample.png", pngSaveOpts);
```

### Почему каждый элемент важен

1. **HTMLDocument** — работает полностью в памяти, поэтому вам не нужны физические файлы `.html`. Идеально подходит для конвертации «на лету».
2. **WebFontStyle** — показывает, что вы можете стилизовать текст перед рендерингом; комбинация жирный‑курсив лишь демонстрация.
3. **ImageRenderingOptions.UseAntialiasing** — этот флаг отвечает на вопрос **как включить сглаживание**; установите его в `true`, и растеризатор сгладит края.
4. **TextOptions.UseHinting** — хинтинг улучшает чёткость глифов, особенно при небольших размерах. Хороший компаньон к сглаживанию.
5. **ImageSaveOptions** — объединяет параметры рендеринга и текста, затем указывает Aspose вывести файл PNG.

## Рендеринг HTML в PNG с помощью Aspose

Теперь, когда вы знаете **как включить сглаживание**, давайте рассмотрим более широкую картину **render html to png**. Aspose.HTML абстрагирует всю тяжёлую работу:

- **Automatic layout** — движок парсит CSS, вычисляет модели коробок и позиционирует элементы так же, как браузер.
- **Resolution control** — вы можете задать DPI через `ImageRenderingOptions.Resolution`, что удобно для печати высокого разрешения.
- **Background handling** — установите `imageOpts.BackgroundColor`, если нужен прозрачный или цветной холст.

```csharp
imageOpts.Resolution = new SizeF(300, 300); // 300 DPI for print‑quality PNG
```

> **Pro tip:** Если вы конвертируете страницу, содержащую внешние ресурсы (изображения, шрифты), убедитесь, что задали `htmlDoc.BaseUrl` на папку, где находятся эти ресурсы. В противном случае рендерер их пропустит.

## Конвертация HTML в изображение — расширенные параметры

Фраза **convert html to image** часто подразумевает не только PNG. Aspose поддерживает JPEG, BMP, TIFF и даже GIF. Переключение форматов так же просто, как изменение перечисления `SaveFormat`:

```csharp
ImageSaveOptions jpegOpts = new ImageSaveOptions(SaveFormat.Jpeg)
{
    RenderingOptions = imageOpts,
    TextOptions = textOpts,
    Quality = 90 // JPEG quality (0‑100)
};

htmlDoc.Save("sample.jpg", jpegOpts);
```

Когда вам нужен векторный вывод, рассмотрите `SvgSaveOptions`. Тот же конвейер рендеринга применяется, поэтому вы получаете одинаковое сглаживание во всех форматах.

### Крайний случай: Очень длинные страницы

Если ваш HTML длиннее типичного экрана, Aspose по умолчанию создаст одно высокое изображение. Это может сильно увеличить потребление памяти. Чтобы смягчить проблему, вы можете разбить документ на несколько страниц:

```csharp
var pageHeight = 1080; // pixels
var totalHeight = htmlDoc.DocumentElement.ScrollHeight;
for (int offset = 0; offset < totalHeight; offset += pageHeight)
{
    imageOpts.Viewport = new RectangleF(0, offset, htmlDoc.DocumentElement.ScrollWidth, pageHeight);
    htmlDoc.Save($"page_{offset / pageHeight}.png", pngSaveOpts);
}
```

## Сохранение HTML как PNG — последний шаг

На данном этапе вы увидели **как включить сглаживание**, научились **render html to png** и изучили варианты **convert html to image**. Финальный шаг — **save html as png** — уже продемонстрирован в оригинальном фрагменте, но давайте оформим его в переиспользуемый метод:

```csharp
public static void SaveHtmlAsPng(string html, string outputPath, bool antialias = true)
{
    // Create document
    var doc = new HTMLDocument(html);

    // Rendering options
    var imgOpts = new ImageRenderingOptions
    {
        UseAntialiasing = antialias,
        Resolution = new SizeF(96, 96) // default screen DPI
    };

    // Text options
    var txtOpts = new TextOptions { UseHinting = true };

    // Combine into save options
    var saveOpts = new ImageSaveOptions(SaveFormat.Png)
    {
        RenderingOptions = imgOpts,
        TextOptions = txtOpts
    };

    // Save
    doc.Save(outputPath, saveOpts);
}
```

Теперь вы можете вызвать `SaveHtmlAsPng("<html>…</html>", @"C:\temp\output.png")` из любой части проекта. Параметр `antialias` позволяет включать или отключать функцию сглаживания, давая вам полный контроль над **как включить сглаживание** во время выполнения.

## Aspose HTML в PNG — полностью рабочий пример

Ниже представлено автономное консольное приложение, которое объединяет всё вместе. Скопируйте‑вставьте, замените плейсхолдер `YOUR_DIRECTORY` и запустите с .NET 6 или новее.



## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как использовать Aspose для рендеринга HTML в PNG – пошаговое руководство](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Как рендерить HTML в PNG с Aspose – полное руководство](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [Рендеринг HTML в PNG в .NET с Aspose.HTML](/html/english/net/rendering-html-documents/render-html-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}