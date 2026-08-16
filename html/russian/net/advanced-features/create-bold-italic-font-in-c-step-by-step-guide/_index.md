---
category: general
date: 2026-08-15
description: Быстро создайте полужирный курсивный шрифт в C#. Узнайте, как создать
  шрифт в C# с полужирным и курсивным стилями, используя встроенный класс Font.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create bold italic font
- create font in c#
- C# FontStyle
- text styling C#
- System.Drawing.Font
language: ru
lastmod: 2026-08-15
og_description: Создайте полужирный курсивный шрифт в C# с понятным примером. Этот
  учебник показывает, как создать шрифт в C# с использованием флагов FontStyle и объясняет
  распространённые подводные камни.
og_image_alt: Screenshot of text rendered with a bold italic Arial font in a C# console
  window
og_title: Создание жирного курсивного шрифта в C# – полное руководство по кодированию
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  headline: Create bold italic font in C# – step‑by‑step guide
  type: TechArticle
- description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  name: Create bold italic font in C# – step‑by‑step guide
  steps:
  - name: Save the code to a file named `Program.cs`.
    text: Save the code to a file named `Program.cs`.
  - name: Open a terminal in the file’s directory.
    text: Open a terminal in the file’s directory.
  - name: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
    text: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
  - name: Replace the generated `Program.cs` with the code above.
    text: Replace the generated `Program.cs` with the code above.
  - name: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
    text: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
  - name: Build and run with `dotnet run`.
    text: Build and run with `dotnet run`.
  type: HowTo
tags:
- C#
- fonts
- text styling
title: Создание полужирного курсивного шрифта в C# – пошаговое руководство
url: /ru/net/advanced-features/create-bold-italic-font-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание полужирного курсивного шрифта в C# – пошаговое руководство

Если вам нужно **создать полужирный курсивный шрифт** в C#, это руководство покажет, как это сделать. Вы увидите полностью рабочий пример, который также демонстрирует, как **создавать шрифт в C#** с помощью стандартного класса .NET `Font`.

Работа с пользовательскими шрифтами – обычная часть разработки Windows‑приложений, генерации PDF или рендеринга HTML на сервере. К концу этого урока вы сможете создать шрифт, который одновременно полужирный и курсивный, поймёте, почему используется побитовое `|`, и научитесь обрабатывать типичные ситуации, такие как отсутствие запрашиваемого семейства шрифтов.

## Что вы узнаете

* Как импортировать необходимые пространства имён для работы со шрифтами.  
* Синтаксис объединения `FontStyle.Bold` и `FontStyle.Italic`.  
* Как проверить, что шрифт был создан успешно.  
* Советы по обработке резервных вариантов, когда требуемое семейство не установлено.  

Никакие внешние библиотеки не требуются — всё использует базовую библиотеку классов .NET Framework / .NET Core.

## Предварительные требования

* .NET 6.0 SDK или новее (код также работает на .NET Framework 4.6+).  
* Редактор кода или IDE (Visual Studio, VS Code, Rider и т.д.).  
* Базовое знакомство с синтаксисом C#.  

Если у вас есть эти требования, вы можете следовать инструкциям без дополнительной настройки.

## Шаг 1: Добавьте необходимые директивы using

Класс `Font` находится в пространстве имён `System.Drawing`, которое является частью пакета NuGet `System.Drawing.Common` для .NET Core/.NET 5+. Добавьте пространство имён в начале файла:

```csharp
using System;
using System.Drawing;   // Provides Font and FontStyle
```

> **Почему это важно** – без строки `using System.Drawing;` компилятор не сможет найти `Font` или `FontStyle`, что приведёт к ошибке «type or namespace name could not be found».

## Шаг 2: Объедините полужирный и курсивный стили с помощью побитового оператора OR

В .NET `FontStyle` — это перечисление, помеченное атрибутом `[Flags]`. Это значит, что вы можете комбинировать несколько значений, используя оператор `|` (побитовое ИЛИ):

```csharp
// Step 2: Create a Font that is both bold and italic
var font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
```

### Пояснение

* `"Arial"` – название семейства шрифта. Если в системе нет Arial, конструктор переключится на шрифт по умолчанию.  
* `12` – размер в пунктах.  
* `FontStyle.Bold | FontStyle.Italic` – объединяет два флага стиля. Оператор `|` объединяет бинарные представления каждого флага, получая единое значение, которое обозначает «полужирный + курсивный».

> **Pro tip:** Всегда используйте имена перечислений (`FontStyle.Bold`), а не «магические» числа; это повышает читаемость и предотвращает ошибки при изменении значений перечисления.

## Шаг 3: Проверьте созданный шрифт (необязательно, но рекомендуется)

Вывод свойств шрифта помогает убедиться, что комбинация стилей прошла успешно, особенно при отладке на новой машине.

```csharp
// Step 3: Output the font details to the console
Console.WriteLine($"Font family: {font.Name}");
Console.WriteLine($"Size (pt): {font.Size}");
Console.WriteLine($"Style: {font.Style}");
```

**Ожидаемый вывод**

```
Font family: Arial
Size (pt): 12
Style: Bold, Italic
```

Если в выводе присутствуют оба `Bold` и `Italic`, шрифт создан корректно.

## Шаг 4: Отрисуйте пример строки (визуальное подтверждение)

В консольном приложении вы не увидите реального оформления глифов, но можете сгенерировать изображение, чтобы доказать результат. Ниже приведён фрагмент, который рисует «Hello, World!» полужирным курсивным шрифтом и сохраняет его как *sample.png*:

```csharp
// Step 4: Draw text to an image file for visual confirmation
using (var bitmap = new Bitmap(300, 100))
using (var graphics = Graphics.FromImage(bitmap))
{
    graphics.Clear(Color.White);
    var brush = Brushes.Black;
    graphics.DrawString("Hello, World!", font, brush, new PointF(10, 30));
    bitmap.Save("sample.png");
    Console.WriteLine("Image saved as sample.png");
}
```

После выполнения программы откройте *sample.png*, чтобы увидеть текст, отрисованный полужирным курсивным стилем.

![Текст, отрисованный полужирным курсивным шрифтом](sample.png)

*Текст alt: Скриншот текста, отрисованного полужирным курсивным шрифтом Arial в консольном окне C#* – этот alt‑текст удовлетворяет требованиям SEO для альтернативных описаний изображений.

## Шаг 5: Корректный резервный вариант, когда семейство шрифта недоступно

Если запрашиваемое семейство (например, «Arial») не установлено, конструктор `Font` бросает `ArgumentException`. Оберните создание в блок `try/catch` и переключитесь на известный безопасный шрифт, например «Segoe UI».

```csharp
Font font;
try
{
    font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
}
catch (ArgumentException)
{
    Console.WriteLine("Arial not found – falling back to Segoe UI.");
    font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
}
```

**Зачем это нужно?** В контейнеризованных или безголовых средах набор шрифтов может отличаться от типичного настольного компьютера. Предоставление резервного варианта предотвращает падения во время выполнения и обеспечивает единообразное оформление.

## Полный, готовый к запуску пример

Объединив всё вместе, получаем полную программу, которую можно скопировать, вставить и запустить:

```csharp
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create the font (bold + italic)
        Font font;
        try
        {
            font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
        }
        catch (ArgumentException)
        {
            Console.WriteLine("Arial not found – using Segoe UI as fallback.");
            font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
        }

        // Display font information
        Console.WriteLine($"Font family: {font.Name}");
        Console.WriteLine($"Size (pt): {font.Size}");
        Console.WriteLine($"Style: {font.Style}");

        // Render a sample image
        using (var bitmap = new Bitmap(300, 100))
        using (var graphics = Graphics.FromImage(bitmap))
        {
            graphics.Clear(Color.White);
            graphics.DrawString("Hello, World!", font, Brushes.Black, new PointF(10, 30));
            bitmap.Save("sample.png");
        }

        Console.WriteLine("Sample image saved as sample.png");
    }
}
```

### Как запустить

1. Сохраните код в файл с именем `Program.cs`.  
2. Откройте терминал в каталоге с файлом.  
3. Выполните `dotnet new console -n FontDemo` (если нужен шаблон проекта).  
4. Замените сгенерированный `Program.cs` на код выше.  
5. Выполните `dotnet add package System.Drawing.Common` (требуется для .NET Core/5+).  
6. Скомпилируйте и запустите командой `dotnet run`.  

Вы увидите вывод в консоли, подтверждающий свойства шрифта, а `sample.png` появится в папке проекта.

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| **Отсутствует пакет `System.Drawing.Common`** | .NET Core не включает `System.Drawing` по умолчанию. | Выполните `dotnet add package System.Drawing.Common`. |
| **Семейство шрифта не установлено** | В безголовых Docker‑образах часто нет Windows‑шрифтов. | Используйте резервный шрифт или установите необходимые шрифты в контейнере. |
| **Неправильное использование `|`** | Использование `+` вместо `|` приводит к неверной комбинации. | Всегда комбинируйте значения `FontStyle` побитовым оператором OR (`|`). |
| **Не освобождаете объект `Font`** | Отсутствие вызова `Dispose` может привести к утечке GDI‑ресурсов. | Оберните `Font` в `using`‑блок или вызовите `font.Dispose()` после использования. |

## Заключение

Теперь вы знаете, как **создавать полужирный курсивный шрифт** в C# и как **создавать шрифт в C#** безопасно и эффективно. В руководстве рассмотрены импорт нужного пространства имён, объединение флагов `FontStyle`, проверка результата, визуальная отрисовка примера и обработка отсутствия семейства шрифтов.

Далее вы можете изучить:

* **Создание подчёркнутых или зачёркнутых шрифтов** – добавьте `FontStyle.Underline` или `FontStyle.Strikeout`.  
* **Использование пользовательских TrueType‑шрифтов** – загрузите файл `.ttf` через `PrivateFontCollection`.  
* **Применение шрифтов в WinForms, WPF или генерации PDF** – тот же объект `Font` можно передать UI‑контролам или сторонним библиотекам.

Экспериментируйте с разными семействами, размерами и комбинациями стилей. Если возникнут проблемы, обратитесь к таблице «Распространённые подводные камни» или проверьте официальную [документацию .NET для System.Drawing.Font](https://learn.microsoft.com/dotnet/api/system.drawing.font). Приятного кодинга!

## Что изучать дальше?

Следующие учебники охватывают смежные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Cara Menggabungkan Font Secara Programatis di C# – Panduan Langkah demi Langkah](/html/indonesian/net/advanced-features/how-to-combine-fonts-programmatically-in-c-step-by-step-guid/)
- [Create HTML Document with Styled Text and Export to PDF – Full Guide](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [convert docx to png – create zip archive c# tutorial](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}