---
category: general
date: 2026-04-06
description: Узнайте, как включить сглаживание, задать ширину и высоту изображения
  и сохранить документ в формате PNG в C# — быстрый гид по экспорту документа в изображение.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: ru
og_description: Как включить сглаживание при экспорте документа в изображение. Это
  руководство покажет, как задать ширину изображения, высоту изображения и сохранить
  документ в формате PNG.
og_title: Как включить сглаживание — экспортировать документ в изображение
tags:
- C#
- ImageRendering
- Antialiasing
title: Как включить сглаживание — экспортировать документ в изображение с C#
url: /ru/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как включить сглаживание – экспортировать документ в изображение в C#

Задумывались когда‑нибудь **как включить сглаживание** при преобразовании документа в картинку? Возможно, вы попробовали простой вызов `Save`, и результат получился зубчатым, особенно на диагональных линиях. Хорошая новость: не нужен волшебник графики — достаточно нескольких строк C# и правильных параметров.

В этом руководстве мы пройдемся по установке ширины изображения, высоты изображения и, наконец, **сохраним документ как PNG**, чтобы вы могли **экспортировать документ в изображение** с плавными краями. К концу вы получите готовый фрагмент кода, который создаст чёткий PNG 800 × 600 с включённым сглаживанием.

## Предварительные требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+)  
- Ссылка на библиотеку рендеринга, поддерживающую `ImageRenderingOptions` (например, Aspose.Words, Syncfusion или любой API, предоставляющий аналогичные свойства)  
- Базовое понимание синтаксиса C#  

Никакой тяжёлой настройки — просто добавьте пакет NuGet и можно начинать.

## Шаг 1: Установите библиотеку рендеринга

Сначала подключите пакет к вашему проекту. Если вы используете Aspose.Words, выполните:

```bash
dotnet add package Aspose.Words
```

> **Совет:** Держите версию библиотеки актуальной; последний релиз (по состоянию на апрель 2026) добавил улучшения производительности для сглаживания.

## Шаг 2: Создайте объект Document

Загрузите или создайте документ, который хотите отрендерить. Ниже минимальный пример, создающий одностраничный документ с простым абзацем:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

Класс `Document` — точка входа; всё, что вы рендерите, происходит из него. В реальных проектах вы, скорее всего, загрузите существующий .docx:

```csharp
// Document doc = new Document("input.docx");
```

## Шаг 3: Определите параметры рендеринга (ширина, высота, сглаживание)

Теперь отвечаем на главный вопрос: **как включить сглаживание**. Объект `ImageRenderingOptions` позволяет переключать сглаживание и задавать размеры.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Обратите внимание на комментарии: они явно указывают **set image width**, **set image height** и **UseAntialiasing** — три параметра, которые имеют наибольшее значение, когда нужен отполированный PNG.

### Почему важно сглаживание

Без сглаживания диагональные линии и кривые выглядят ступенчатыми, потому что рендерер рассматривает каждый пиксель как включённый или выключенный. Включив его, вы смешиваете пиксели по краям, получая мягкое визуальное сглаживание, похожее на то, что делает фоторедактор. Цена — небольшое увеличение времени обработки, но для большинства экспортов, ориентированных на UI, это пренебрежимо.

## Шаг 4: Сохраните документ как PNG (Экспортировать документ в изображение)

С готовыми параметрами мы, наконец, **сохраняем документ как PNG**. Метод `Save` принимает путь к файлу и параметры, которые мы только что настроили.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

И всё — ваш документ теперь 800 × 600 PNG с применённым сглаживанием. Открыв `output.png`, вы увидите чистый текст, гладкие линии и отсутствие зубчатых артефактов.

### Проверка результата

Быстро проверьте файл в любом просмотрщике изображений. Обратите внимание на:

- Правильные размеры (800 × 600)  
- Отсутствие видимых ступенчатых краёв у текста или фигур  
- Прозрачный фон, если в документе не был задан цвет фона (большинство библиотек по умолчанию используют белый)

Если изображение выглядит зубчатым, убедитесь, что `UseAntialiasing = true` не переопределяется где‑то ещё.

## Шаг 5: Особые случаи и варианты

### Изменение формата вывода

Хотите JPEG вместо PNG? Просто измените расширение файла и, при желании, настройте сжатие:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Экспорт нескольких страниц

Если исходный документ содержит несколько страниц, рендерер по умолчанию создаёт отдельные файлы изображений для каждой страницы. Можно пройтись по страницам в цикле:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Сохранение в поток (например, HTTP‑ответ)

Если вы создаёте веб‑API, возможно, понадобится вернуть PNG напрямую:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Полный рабочий пример

Ниже полностью готовая к копированию программа, включающая все обсуждённые шаги:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

Запуск этой программы создаст `output.png` в папке исполняемого файла. Откройте его, и вы увидите гладкий PNG 800 × 600 — именно то, чего мы добивались.

## Часто задаваемые вопросы и устранение неполадок

- **Что делать, если изображение выглядит размытым?**  
  Размытие может возникнуть при масштабировании небольшого исходного листа. Держите размер исходной страницы близким к целевым размерам или увеличьте DPI через `imageOptions.Resolution` (например, `Resolution = 300`).

- **Работает ли это в .NET Framework?**  
  Да. Тот же API доступен в классическом фреймворке; просто подключите соответствующую DLL.

- **Можно ли управлять цветом фона?**  
  Конечно. Установите `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` перед сохранением.

- **Сглаживание аппаратно ускорено?**  
  Большинство библиотек выполняют программное сглаживание. Если нужна GPU‑акселерация, ищите движок рендеринга, который явно поддерживает её.

## Заключение

Мы рассмотрели **как включить сглаживание** при **экспорте документа в изображение**, прошли через **установку ширины изображения** и **высоты изображения**, а также показали точные шаги для **сохранения документа как PNG**. Приведённый выше фрагмент готов к использованию в продакшене, и теперь вы можете адаптировать его под JPEG, многостраничные PDF или даже потоковую передачу изображения клиенту.

Дальше вы можете добавить водяные знаки, настроить DPI для печатного качества или интегрировать эту логику в endpoint ASP.NET Core. Принципы остаются теми же — меняем только путь к файлу на поток ответа.

Приятного кодинга и наслаждайтесь чёткими, сглаженными изображениями! 

![Rendered PNG with antialiasing enabled](output.png "Rendered PNG with antialiasing enabled")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}