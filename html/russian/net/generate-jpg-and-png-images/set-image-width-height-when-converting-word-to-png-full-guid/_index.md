---
category: general
date: 2026-05-22
description: Установите ширину и высоту изображения при конвертации документа Word
  в PNG. Узнайте, как экспортировать docx в изображение с высококачественной отрисовкой
  в пошаговом руководстве.
draft: false
keywords:
- set image width height
- convert word to png
- save docx as png
- export docx as image
- how to render word
language: ru
og_description: Установите ширину и высоту изображения при конвертации документа Word
  в PNG. Этот учебник показывает, как экспортировать docx в изображение с настройками
  высокого качества.
og_title: Установка ширины и высоты изображения при конвертации Word в PNG – Полное
  руководство
schemas:
- author: Aspose
  dateModified: '2026-05-22'
  description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  headline: Set Image Width Height When Converting Word to PNG – Full Guide
  type: TechArticle
- description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  name: Set Image Width Height When Converting Word to PNG – Full Guide
  steps:
  - name: 1. Preserve Transparent Backgrounds
    text: 'If your Word document contains shapes with transparent backgrounds and
      you want to keep that transparency, set the `BackgroundColor` to `Color.Transparent`:'
  - name: 2. Render Only a Specific Range
    text: Sometimes you only need a paragraph or a table, not the whole page. Use
      `DocumentVisitor` to extract the node and render it separately. That’s a more
      advanced scenario, but it shows **how to render word** content at a granular
      level.
  - name: 3. Adjust DPI Dynamically
    text: 'If you need different DPI per page (e.g., high‑resolution for the cover
      page), modify `Resolution` inside the loop:'
  - name: 4. Batch Processing
    text: When converting dozens of documents, wrap the whole flow in a method and
      reuse the same `ImageRenderingOptions` instance. Re‑using the options object
      reduces allocation overhead.
  type: HowTo
tags:
- Aspose.Words
- C#
- Image Rendering
title: Установка ширины и высоты изображения при конвертации Word в PNG – Полное руководство
url: /ru/net/generate-jpg-and-png-images/set-image-width-height-when-converting-word-to-png-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Установить ширину и высоту изображения при конвертации Word в PNG – Полное руководство

Задумывались ли вы когда‑нибудь, как **установить ширину и высоту изображения** при **конвертации Word в PNG**? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда экспорт по умолчанию дает размытое изображение или неправильные размеры, и затем тратят часы в поисках действительно работающего решения.

В этом руководстве мы пройдем чистое, сквозное решение, показывающее **как отрисовать word** документы в виде PNG‑изображений, позволяющее вам **сохранить docx как PNG** с точным контролем ширины‑высоты и высококачественным сглаживанием. К концу вы получите готовый фрагмент кода, твердое понимание параметров API и несколько профессиональных советов, как избежать распространённых подводных камней.

## Что вы узнаете

- Загрузить файл `.docx` с помощью Aspose.Words for .NET.
- **Установить ширину и высоту изображения** с помощью `ImageRenderingOptions`.
- **Экспортировать docx как изображение** (PNG) с включённым сглаживанием.
- Как **конвертировать word в png** для одной страницы или всего документа.
- Советы по работе с большими документами, учёту DPI и путям файловой системы.

Никаких внешних инструментов, без лишних командных строк — только чистый C#‑код, который можно вставить в любой .NET‑проект.

---

## Необходимые условия

Прежде чем мы начнём, убедитесь, что у вас есть следующее:

| Требование | Почему это важно |
|------------|-------------------|
| **.NET 6.0+** (or .NET Framework 4.7.2) | Aspose.Words поддерживает оба, но более новые среды обеспечивают лучшую производительность. |
| **Aspose.Words for .NET** NuGet package (`Install-Package Aspose.Words`) | Предоставляет класс `Document` и движок рендеринга. |
| A **Word document** (`.docx`) you want to turn into a PNG. | Исходный документ, который вы будете конвертировать. |
| Basic C# knowledge – you’ll understand `using` statements and object initialization. | Делает процесс обучения более плавным. |

Если вам не хватает NuGet‑пакета, выполните это в консоли диспетчера пакетов:

```powershell
Install-Package Aspose.Words
```

Вот и всё — как только пакет установлен, вы готовы начинать кодировать.

## Шаг 1: Загрузить исходный документ

Самое первое, что нужно сделать, — указать библиотеке путь к файлу Word, который вы хотите преобразовать.

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Load the .docx file from disk
Document doc = new Document(@"C:\MyFiles\input.docx");
```

**Почему это важно:** Класс `Document` читает весь пакет Word в память, предоставляя доступ к страницам, стилям и всему остальному. Если путь неверен, вы получите `FileNotFoundException`, поэтому дважды проверьте, что файл существует и путь использует экранированные обратные слеши (`\\`) или дословную строку (`@`).  

> **Pro tip:** Оберните вызов загрузки в блок `try/catch`, если ожидаете, что файл может отсутствовать во время выполнения.

## Шаг 2: Настроить параметры рендеринга изображения (Установить ширину и высоту изображения)

Теперь начинается сердце руководства: **как установить ширину и высоту изображения**, чтобы полученный PNG не был растянутым или пикселизированным. Класс `ImageRenderingOptions` даёт тонкую настройку размеров, DPI и сглаживания.

```csharp
// Create rendering options and explicitly set width and height
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Desired output size in pixels
    Width = 1024,          // Set image width height: 1024px wide
    Height = 768,          // Set image width height: 768px tall

    // High‑quality antialiasing works on Windows, Linux, and macOS
    UseAntialiasing = true,

    // Optional: increase DPI for sharper output (default is 96)
    Resolution = 300
};
```

Объяснение ключевых свойств:

- `Width` и `Height` — Точные пиксельные размеры, которые вам нужны. Устанавливая их, вы **устанавливаете ширину и высоту изображения** напрямую, переопределяя размер страницы по умолчанию.
- `UseAntialiasing` — Включает высококачественное сглаживание текста и векторной графики, что критично, когда вы **конвертируете word в png** и хотите чёткие края.
- `Resolution` — Более высокий DPI даёт больше деталей, особенно для сложных макетов. Следите за использованием памяти; изображение с 300 DPI может быть большим.

> **Почему не полагаться просто на размер по умолчанию?** По умолчанию используется физический размер страницы (например, A4 при 96 DPI). Это часто даёт изображение 794 × 1123 пикселя — подходит в некоторых случаях, но не когда нужен конкретный UI‑миниатюра или фиксированный превью.

## Шаг 3: Рендеринг и сохранение в PNG (Экспорт Docx как изображения)

С загруженным документом и настроенными параметрами вы наконец можете **экспортировать docx как изображение**. Метод `RenderToImage` делает всю тяжёлую работу.

```csharp
// Render the first page (page index 0) to a PNG file
doc.RenderToImage(@"C:\MyFiles\output.png", imageOptions);
```

Если хотите отрендерить **весь документ** (все страницы) в отдельные PNG‑файлы, пройдитесь по коллекции страниц:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string outPath = $@"C:\MyFiles\page_{i + 1}.png";
    doc.RenderToImage(outPath, imageOptions, i);
}
```

**Что происходит под капотом?** Рендерер растеризует каждую страницу, используя заданные вами размеры, применяет сглаживание и записывает поток PNG‑байтов на диск. Поскольку PNG — без потерь, вы сохраняете полную точность оригинального макета Word.

**Ожидаемый результат:** Чёткий PNG‑файл точно 1024 × 768 пикселей (или любой размер, который вы указали). Откройте его в любой программе‑просмотрщике, и вы увидите содержимое Word, отрисованное точно так же, как в оригинальном документе, но теперь в виде растрового изображения.

## Расширенные советы и варианты

### 1. Сохранить прозрачный фон

Если ваш документ Word содержит фигуры с прозрачным фоном и вы хотите сохранить эту прозрачность, задайте `BackgroundColor` как `Color.Transparent`:

```csharp
imageOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### 2. Рендерить только определённый диапазон

Иногда нужен лишь абзац или таблица, а не вся страница. Используйте `DocumentVisitor`, чтобы извлечь узел и отрендерить его отдельно. Это более продвинутый сценарий, но он показывает **как отрисовать word** контент на более гранулярном уровне.

### 3. Динамически регулировать DPI

Если нужен разный DPI для разных страниц (например, высокое разрешение для обложки), измените `Resolution` внутри цикла:

```csharp
if (i == 0) imageOptions.Resolution = 600; // cover page
else imageOptions.Resolution = 300;
```

### 4. Пакетная обработка

При конвертации десятков документов оберните весь процесс в метод и переиспользуйте один экземпляр `ImageRenderingOptions`. Переиспользование объекта параметров уменьшает накладные расходы на выделение памяти.

## Распространённые ошибки и как их избежать

| Признак | Вероятная причина | Решение |
|---------|-------------------|---------|
| PNG размытый, несмотря на высокий DPI | `UseAntialiasing` left `false` | Set `UseAntialiasing = true`. |
| Размер вывода не соответствует `Width`/`Height` | DPI not considered | Multiply desired size by `Resolution / 96` or adjust `Resolution`. |
| Исключение Out‑of‑memory при больших документах | Rendering whole document at 300 DPI | Render one page at a time, dispose of each image after saving. |
| PNG показывает белый фон на прозрачных изображениях | `BackgroundColor` not set | Set `imageOptions.BackgroundColor = Color.Transparent`. |

## Полный рабочий пример

Ниже приведена автономная программа, которую можно скопировать и вставить в консольное приложение. Она демонстрирует **конвертировать word в png**, **сохранить docx как png** и, конечно, **установить ширину и высоту изображения**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;
using System.Drawing; // For Color

namespace WordToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            string inputPath = @"C:\MyFiles\input.docx";
            Document doc = new Document(inputPath);

            // 2️⃣ Configure rendering options (set image width height)
            ImageRenderingOptions options = new ImageRenderingOptions
            {
                Width = 1024,          // Desired pixel width
                Height = 768,          // Desired pixel height
                UseAntialiasing = true,
                Resolution = 300,
                BackgroundColor = Color.Transparent // Keep transparency if needed
            };

            // 3️⃣ Render the first page to PNG (export docx as image)
            string outputPath = @"C:\MyFiles\output.png";
            doc.RenderToImage(outputPath, options);

            Console.WriteLine($"✅ Document rendered successfully to {outputPath}");
            // Optional: render all pages
            //RenderAllPages(doc, options);
        }

        // Helper method for batch rendering (uncomment if needed)
        static void RenderAllPages(Document doc, ImageRenderingOptions options)
        {
            for (int i = 0; i < doc.PageCount; i++)
            {
                string pagePath = $@"C:\MyFiles\page_{i + 1}.png";
                doc.RenderToImage(pagePath, options, i);
                Console.WriteLine($"Page {i + 1} saved to {pagePath}");
            }
        }
    }
}
```

**Запустите:** Скомпилируйте проект, разместите корректный `input.docx` по указанному пути и выполните. Вы должны увидеть `output.png` точно **1024 × 768** пикселей, отрисованный с плавными краями.

## Похожие руководства

- [Как включить сглаживание при конвертации DOCX в PNG/JPG](/html/english/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/)
- [конвертировать docx в png – создание zip-архива c# руководство](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)
- [Как использовать Aspose для рендеринга HTML в PNG – пошаговое руководство](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}