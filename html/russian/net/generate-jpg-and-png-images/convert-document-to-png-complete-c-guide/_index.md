---
category: general
date: 2026-02-19
description: Узнайте, как конвертировать документ в PNG, задавать размеры изображения
  и регулировать качество изображения в C# с простым пошаговым примером.
draft: false
keywords:
- convert document to png
- set image dimensions
- save rendered image
- adjust image quality
- set custom image size
language: ru
og_description: Преобразуйте документ в PNG в C#, задав размеры изображения, отрегулировав
  качество и сохранив отрисованное изображение — всё в одном руководстве.
og_title: Преобразовать документ в PNG – Полное руководство по C#
tags:
- C#
- Image Rendering
- Document Processing
title: Конвертировать документ в PNG – Полное руководство по C#
url: /ru/net/generate-jpg-and-png-images/convert-document-to-png-complete-c-guide/
---

English phrase? It's not a technical term, can translate.

But we must preserve the markdown formatting.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Конвертация документа в PNG – Полное руководство на C#

Когда‑то вам нужно **convert document to PNG**, но вы не уверены, какие настройки дадут чёткое изображение правильного размера? Вы не одиноки. Во многих проектах — отчёты, миниатюры или веб‑превью — правильные размеры и качество изображения имеют решающее значение, а код ниже показывает, как это сделать.

В этом руководстве мы пройдёмся по загрузке документа, настройке **set image dimensions**, корректировке **adjust image quality** и, наконец, **save rendered image** на диск. К концу вы также узнаете, как **set custom image size** для любой ситуации.

## Что вы узнаете

- Как загрузить документ с помощью популярной .NET‑библиотеки рендеринга (используется Aspose.Words for .NET, но концепции применимы к аналогичным API).  
- Пошаговый процесс **convert document to PNG** с управлением шириной, высотой и сглаживанием.  
- Способы **set image dimensions** и **adjust image quality** для приложений, критичных к производительности.  
- Как **save rendered image** безопасно и работать с многостраничными документами.  
- Советы для особых случаев, таких как рендеринг отдельной страницы или работа с большими файлами.

> **Prerequisite:** .NET 6+ SDK, Visual Studio 2022 (или любой другой IDE), и пакет NuGet Aspose.Words for .NET. Если вы используете другой движок рендеринга, просто замените класс `ImageRenderingOptions` на эквивалент в вашей библиотеке.

---

## Шаг 1 – Convert Document to PNG с нужным размером

Первое, что нужно сделать — создать экземпляр `ImageRenderingOptions` и указать рендереру, какого размера должен быть PNG. Здесь и вступает в действие **set image dimensions**.

```csharp
using System;
using System.Drawing.Imaging;               // For ImageFormat
using Aspose.Words;                         // Core document API
using Aspose.Words.Rendering;               // Image rendering helpers

class Program
{
    static void Main()
    {
        // Load the source document (DOCX, PDF, etc.)
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Create an ImageRenderingOptions instance
        ImageRenderingOptions imageRenderOptions = new ImageRenderingOptions();

        // Configure the image size, format, and quality
        imageRenderOptions.Width = 1024;                     // width in pixels
        imageRenderOptions.Height = 768;                     // height in pixels
        imageRenderOptions.OutputFormat = ImageFormat.Png;  // PNG output
        imageRenderOptions.UseAntialiasing = true;           // smoother edges

        // Render the first page to a PNG file
        document.RenderToImage("YOUR_DIRECTORY/output.png", imageRenderOptions);
    }
}
```

**Почему это важно:**  
- **Width & Height** позволяют **set custom image size** без последующего изменения размера, что сохраняет чёткость.  
- **UseAntialiasing** — ключевой флаг для **adjust image quality**: включите его для более плавных краёв, отключите для ускорения рендеринга.  
- Прямой вывод в PNG обеспечивает безупречную глубину цвета, идеально подходящую для UI‑миниатюр.

> **Совет профессионала:** Если нужен более высокий DPI (dots per inch), задайте `imageRenderOptions.Resolution = 300;` перед рендерингом. Более высокий DPI улучшает качество печати, но увеличивает размер файла.

## Шаг 2 – Set Image Dimensions и Adjust Image Quality

Иногда размер страницы по умолчанию не подходит. Может потребоваться ландшафтная миниатюра для веб‑галереи или квадратный значок для мобильного приложения. Здесь вы **set image dimensions** вручную.

```csharp
// Example: Create a square 500×500 PNG with high quality
imageRenderOptions.Width = 500;
imageRenderOptions.Height = 500;
imageRenderOptions.UseAntialiasing = true;   // high‑quality rendering
imageRenderOptions.OutputFormat = ImageFormat.Png;
```

**Что происходит под капотом?**  
Рендерер масштабирует оригинальные векторные данные страницы до указанной вами пиксельной сетки. Поскольку PNG — без потерь, масштабирование не вводит артефактов сжатия, но флаг **adjust image quality** (анти‑алиасинг) определяет, насколько плавными будут края. Отключение анти‑алиасинга может ускорить пакетную обработку при генерации сотен миниатюр.

### Когда настраивать качество

| Сценарий | Рекомендуемая настройка |
|----------|--------------------------|
| Предпросмотр в реальном времени (например, UI) | `UseAntialiasing = false` |
| Финальные материалы для маркетинга | `UseAntialiasing = true` |
| Большая пакетная конверсия | Экспериментируйте с `Resolution` и `UseAntialiasing`, чтобы найти баланс между скоростью и чёткостью |

## Шаг 3 – Save Rendered Image to Disk

После настройки параметров последний шаг — **save rendered image**. Метод `RenderToImage` создаёт файл за вас, но всё равно стоит проверить путь вывода и обработать возможные ошибки ввода‑вывода.

```csharp
try
{
    string outputPath = "YOUR_DIRECTORY/output.png";
    document.RenderToImage(outputPath, imageRenderOptions);
    Console.WriteLine($"✅ Successfully saved PNG to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ Failed to save PNG: {ex.Message}");
}
```

**Зачем оборачивать в try/catch?**  
Проблемы с правами доступа, нехваткой места на диске или неверный путь могут вызвать исключения. Перехватывая их, вы избегаете падения сервиса — особенно важно в веб‑API, которые конвертируют документы «на лету».

### Проверка результата

Откройте сгенерированный файл в любом просмотрщике изображений. Вы должны увидеть PNG с заданной шириной и высотой, а также плавными краями, если был включён анти‑алиасинг. Если размеры выглядят неверно, проверьте, не перепутали ли вы `Width` и `Height`.

## Опционально – Set Custom Image Size для разных сценариев

Иногда требуется набор изображений разных разрешений (например, миниатюры, средние, большие). Вместо жёсткого кодирования каждого размера, пройдитесь по массиву объектов размеров.

```csharp
var sizes = new (int width, int height)[]
{
    (200, 200),   // tiny thumbnail
    (800, 600),   // medium preview
    (1920, 1080)  // full‑HD preview
};

foreach (var (w, h) in sizes)
{
    imageRenderOptions.Width = w;
    imageRenderOptions.Height = h;
    string outFile = $"YOUR_DIRECTORY/output_{w}x{h}.png";
    document.RenderToImage(outFile, imageRenderOptions);
    Console.WriteLine($"Saved {outFile}");
}
```

**Ключевые выводы:**  

- Этот шаблон позволяет **set custom image size** «на лету», делая код DRY.  
- Вы также можете менять `UseAntialiasing` в зависимости от размера — высокое качество для больших изображений, быстрая отрисовка для крошечных миниатюр.  
- Не забудьте освободить объект `Document` после завершения (`document.Dispose();`), чтобы освободить нативные ресурсы.

---

## Работа с многостраничными документами

Приведённый выше фрагмент рендерит только первую страницу. Если ваш источник содержит несколько страниц и вам нужен PNG для каждой, перебирайте `document.PageCount`.

```csharp
for (int pageIndex = 0; pageIndex < document.PageCount; pageIndex++)
{
    // Adjust options if you want per‑page customizations
    imageRenderOptions.PageIndex = pageIndex; // tells the renderer which page

    string outPath = $"YOUR_DIRECTORY/page_{pageIndex + 1}.png";
    document.RenderToImage(outPath, imageRenderOptions);
    Console.WriteLine($"Page {pageIndex + 1} saved as PNG.");
}
```

**Зачем использовать `PageIndex`?**  
Он указывает рендереру, какую страницу отрисовывать. По умолчанию используется страница 0 (первая). Такой подход гарантирует, что каждая страница получит собственный PNG, сохраняя workflow **convert document to png** для многостраничных PDF, DOCX или ODT.

---

## Полный рабочий пример

Ниже представлена полностью готовая программа, которую можно скопировать в новый консольный проект. Она охватывает загрузку, конфигурацию, рендеринг, обработку ошибок и поддержку многостраничных документов — всё в одном месте.

```csharp
using System;
using System.Drawing.Imaging;
using Aspose.Words;
using Aspose.Words.Rendering;

class ConvertToPngDemo
{
    static void Main()
    {
        // 1️⃣ Load the source document
        Document doc = new Document("YOUR_DIRECTORY/input.docx");

        // 2️⃣ Prepare rendering options (set image dimensions, quality, format)
        ImageRenderingOptions opts = new ImageRenderingOptions
        {
            Width = 1024,
            Height = 768,
            OutputFormat = ImageFormat.Png,
            UseAntialiasing = true,
            Resolution = 150 // optional DPI tweak
        };

        // 3️⃣ Render each page to its own PNG file
        for (int i = 0; i < doc.PageCount; i++)
        {
            opts.PageIndex = i; // select page
            string outPath = $"YOUR_DIRECTORY/output_page_{i + 1}.png";

            try
            {
                doc.RenderToImage(outPath, opts);
                Console.WriteLine($"✅ Page {i + 1} saved → {outPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Error on page {i + 1}: {ex.Message}");
            }
        }

        // Clean up
        doc.Dispose();
    }
}
```

**Ожидаемый результат:**  
Набор PNG‑файлов с именами `output_page_1.png`, `output_page_2.png`, … каждый размером 1024 × 768 пикселей, с применённым анти‑алиасингом. Откройте любой файл — изображение должно быть чётким, правильно пропорциональным и готовым к использованию в вебе или на десктопе.

---

## Заключение

Теперь вы знаете, как **convert document to PNG** в C#, точно **set image dimensions**, **adjust image quality** и эффективно **save rendered image**. Независимо от того, генерируете ли вы одну миниатюру или целую галерею страниц, показанный шаблон даёт полный контроль над результатом.

Следующий шаг? Попробуйте заменить `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}