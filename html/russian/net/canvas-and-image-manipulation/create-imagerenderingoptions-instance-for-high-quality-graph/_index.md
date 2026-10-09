---
category: general
date: 2026-10-09
description: Создайте экземпляр ImageRenderingOptions, чтобы включить сглаживание
  и улучшить качество отрисовки графики в приложениях .NET.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create imagerenderingoptions instance
- ImageRenderingOptions
- antialiasing
- SmoothingMode
- graphics rendering
language: ru
lastmod: 2026-10-09
og_description: Создайте экземпляр ImageRenderingOptions, чтобы включить сглаживание
  и добиться более плавного рендеринга графики в .NET. Следуйте пошаговому руководству.
og_image_alt: Screenshot showing smooth edges after enabling antialiasing with ImageRenderingOptions
og_title: Создайте экземпляр ImageRenderingOptions — повысите качество графики в .NET
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  headline: Create imagerenderingoptions instance for high‑quality graphics rendering
  type: TechArticle
- description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  name: Create imagerenderingoptions instance for high‑quality graphics rendering
  steps:
  - name: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
    text: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
  - name: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
    text: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
  - name: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
    text: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
  type: HowTo
tags:
- .NET
- C#
- rendering
title: Создать экземпляр ImageRenderingOptions для высококачественного рендеринга
  графики
url: /ru/net/canvas-and-image-manipulation/create-imagerenderingoptions-instance-for-high-quality-graph/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создайте экземпляр ImageRenderingOptions для высококачественного рендеринга графики

Если вам нужно **создать экземпляр ImageRenderingOptions** для получения более плавной графики, это руководство покажет, как это сделать. Настраивая сглаживание, вы устраняете зубчатые края и получаете профессиональный результат без дополнительных библиотек.

Вы узнаете, как создать `ImageRenderingOptions`, включить сглаживание и применить параметры к движку рендеринга, такому как Aspose.Slides или System.Drawing. В руководстве предполагается, что вы знакомы с базовым синтаксисом C# и у вас готова среда разработки .NET.

## Требования

- .NET 6.0 или новее (API доступно в .NET Standard 2.0+)
- Ссылка на сборку, содержащую `ImageRenderingOptions` (например, `Aspose.Slides.NET`)
- IDE, например Visual Studio 2022 или VS Code с расширением C#
- Базовое понимание конвейеров рендеринга графики

## Шаг 1: Создайте экземпляр ImageRenderingOptions

Первой операцией является выделение нового объекта `ImageRenderingOptions`. Этот объект служит контейнером для всех флагов, связанных с рендерингом.

```csharp
using Aspose.Slides;          // Replace with the appropriate namespace
using Aspose.Slides.Export;   // Needed for ImageRenderingOptions

// Step 1: Create the ImageRenderingOptions instance
ImageRenderingOptions imgOptions = new ImageRenderingOptions();
```

Создание экземпляра дает вам полный контроль над тем, как векторная графика растеризуется. Позже вы сможете включать или отключать отдельные функции, такие как сглаживание, режим рендеринга текста или сжатие изображений.

## Шаг 2: Включите сглаживание для улучшения рендеринга графики

Сглаживание (antialiasing) делает переходы между цветами пикселей более плавными, уменьшая ступенчатый эффект на диагональных или изогнутых линиях. Устаревшее свойство `SmoothingMode` помечено как устаревшее; `UseAntialiasing` — современный и рекомендуемый подход.

```csharp
// Step 2: Turn on antialiasing for smoother output
imgOptions.UseAntialiasing = true;
```

Установка `UseAntialiasing` в `true` сообщает движку рендеринга применить высококачественный фильтр во время растеризации. Этот флаг работает как для векторных фигур, так и для текста, обеспечивая единообразную визуальную точность на слайде.

### Почему не использовать SmoothingMode?

`SmoothingMode` относится к `System.Drawing.Graphics` и влияет только на рисование GDI+. При рендеринге слайдов или PDF через Aspose.Slides единственным флагом, который учитывается библиотекой, является `ImageRenderingOptions.UseAntialiasing`. Использование нового свойства гарантирует совместимость в будущем и устраняет неожиданное поведение на платформах, отличных от Windows.

## Шаг 3: Примените параметры к операции рендеринга

После настройки экземпляра `ImageRenderingOptions` передайте его в метод, выполняющий фактическое рендеринг. Ниже приведён полностью рабочий пример, который загружает презентацию, рендерит первый слайд в PNG и сохраняет изображение с включённым сглаживанием.

```csharp
using System;
using Aspose.Slides;
using Aspose.Slides.Export;

class Program
{
    static void Main()
    {
        // Load a sample presentation
        using Presentation pres = new Presentation("sample.pptx");

        // Create and configure ImageRenderingOptions
        ImageRenderingOptions imgOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true   // Enable antialiasing
        };

        // Render the first slide to a PNG file
        Slide slide = pres.Slides[0];
        slide.GetThumbnail(2f, 2f, imgOptions)   // 2x scale for higher resolution
            .Save("slide1_antialiased.png", Export.SaveFormat.Png);

        Console.WriteLine("Slide rendered with antialiasing.");
    }
}
```

**Пояснение ключевых строк**

- `new Presentation("sample.pptx")` загружает исходный файл.  
- `GetThumbnail(2f, 2f, imgOptions)` создаёт bitmap слайда в двойном масштабе DPI, применяя настроенные параметры рендеринга.  
- Полученный PNG (`slide1_antialiased.png`) отображает плавные кривые и текст благодаря `UseAntialiasing = true`.

### Ожидаемый результат

Откройте `slide1_antialiased.png` в любом просмотрщике изображений. По сравнению с рендерингом без сглаживания вы заметите:

- Закруглённые углы фигур без зубчатых ступеней.  
- Края текста чёткие, но смягчённые, без пикселизированных артефактов.  
- Общая визуальная качество соответствует тому, что вы видите в оригинальном представлении PowerPoint.

## Шаг 4: Дополнительные настройки для продвинутого рендеринга графики

Хотя сглаживание — самый распространённый флаг, `ImageRenderingOptions` предлагает и другие возможности:

| Свойство | Назначение | Типичное значение |
|----------|------------|-------------------|
| `UseHighQualityRendering` | Включает субпиксельный рендеринг текста | `true` |
| `PixelFormat` | Определяет глубину цвета выходного bitmap | `PixelFormat.Format32bppArgb` |
| `ImageFormat` | Задаёт целевой формат изображения (PNG, JPEG и т.д.) | `Export.SaveFormat.Png` |

Эти параметры можно комбинировать:

```csharp
imgOptions.UseHighQualityRendering = true;
imgOptions.PixelFormat = System.Drawing.Imaging.PixelFormat.Format32bppArgb;
```

**Совет профессионала:** При генерации PDF большого масштаба или PNG высокого разрешения оставляйте `UseAntialiasing` включённым, но следите за потреблением памяти. Сглаживание добавляет дополнительную нагрузку, что может быть заметно на слабых машинах.

## Распространённые ошибки и как их избежать

1. **Забыли передать параметры** – Методы рендеринга, принимающие `ImageRenderingOptions`, игнорируют сглаживание, если вызвать перегрузку без параметра options. Всегда используйте трёхпараметрический `GetThumbnail` или аналогичный метод.  
2. **Смешивание SmoothingMode с ImageRenderingOptions** – Установка `Graphics.SmoothingMode` не влияет на рендеринг Aspose.Slides. Полагайтесь исключительно на `UseAntialiasing`.  
3. **Использование устаревшей версии библиотеки** – `ImageRenderingOptions` появился в Aspose.Slides 20.5. Убедитесь, что ваш пакет NuGet обновлён; иначе класс может отсутствовать или не содержать свойства `UseAntialiasing`.

## Заключение

Теперь вы знаете, как **создать экземпляр ImageRenderingOptions**, включить сглаживание и интегрировать параметры в рабочий процесс рендеринга. Этот подход гарантирует более плавный рендеринг графики, заменяя устаревшую настройку `SmoothingMode`, и работает последовательно на всех платформах .NET.

Далее вы можете исследовать дополнительные флаги рендеринга, экспериментировать с различными масштабами DPI или комбинировать технику с экспортом в PDF для создания печатных материалов высокого качества. Освоение `ImageRenderingOptions` — фундаментальная часть программирования высокоточной графики в .NET.

---


## Что следует изучить дальше?


В следующих руководствах рассматриваются тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Создать PNG из HTML – Полное руководство по рендерингу C#](/html/english/net/rendering-html-documents/create-png-from-html-full-c-rendering-guide/)
- [Создать изображение из HTML в C# – Полное пошаговое руководство](/html/english/net/rendering-html-documents/create-image-from-html-in-c-complete-step-by-step-guide/)
- [Создать текст на холсте – Полное руководство по рендерингу текста на изображениях](/html/english/net/canvas-and-image-manipulation/create-canvas-text-full-guide-to-rendering-text-on-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}