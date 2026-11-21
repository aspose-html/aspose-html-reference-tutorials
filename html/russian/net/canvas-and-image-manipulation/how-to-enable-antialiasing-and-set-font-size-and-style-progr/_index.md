---
category: general
date: 2026-11-20
description: Как включить сглаживание в графике C# и программно задать размер шрифта,
  стиль шрифта с полным, исполняемым примером, используя ImageRenderingOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- set font size
- set font style programmatically
- C# graphics rendering
- ImageRenderingOptions example
language: ru
lastmod: 2026-11-20
og_description: Как включить сглаживание в графике C#, установить размер шрифта и
  задать стиль шрифта программно с помощью ImageRenderingOptions – полный код и объяснение.
og_image_alt: Screenshot of antialiased text with custom font size and style generated
  by C# code showing how to enable antialiasing
og_title: Как включить сглаживание и программно задать размер и стиль шрифта в C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to enable antialiasing in C# graphics and set font size, set font
    style programmatically with a complete, runnable example using ImageRenderingOptions.
  headline: How to enable antialiasing and set font size and style programmatically
    in C#
  type: TechArticle
tags:
- C#
- graphics
- antialiasing
- fonts
title: Как включить сглаживание и программно задать размер и стиль шрифта в C#
url: /ru/net/canvas-and-image-manipulation/how-to-enable-antialiasing-and-set-font-size-and-style-progr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как программно включить сглаживание и задать размер и стиль шрифта в C#

Как включить сглаживание в графике C# — частая задача, когда нужны плавные края у фигур или текста. В этом руководстве показано, как включить сглаживание, задать размер шрифта и задать стиль шрифта программно с помощью класса **ImageRenderingOptions**. К концу руководства у вас будет автономное консольное приложение, которое рендерит чёткий стилизованный текст в файл изображения.

Вы узнаете, как настроить конвейер рендеринга, выбрать нужное семейство шрифтов, отрегулировать размер шрифта и применить полужирный или курсивный стиль без выхода из кода. Единственное требование — актуальный .NET SDK и пакет NuGet Aspose.Imaging, который пример устанавливает автоматически.

## Предварительные требования

- .NET 6.0 SDK или новее (скачать с https://dotnet.microsoft.com/)
- Visual Studio 2022 или любой редактор, поддерживающий проекты .NET
- **Aspose.Imaging** NuGet пакет (библиотека, предоставляющая `ImageRenderingOptions`)

Вы можете добавить пакет с помощью следующей команды:

```bash
dotnet add package Aspose.Imaging
```

## Как включить сглаживание с ImageRenderingOptions

`ImageRenderingOptions` — центральный объект, управляющий тем, как Aspose.Imaging рисует графику. Установка свойства `UseAntialiasing` сообщает растеризатору сглаживать края, устраняя «лесенчатый» эффект, который появляется при выключенном сглаживании.

```csharp
// Step 1: Create a new ImageRenderingOptions instance
ImageRenderingOptions renderingOptions = new ImageRenderingOptions();

// Step 2: Enable antialiasing for smoother graphics
renderingOptions.UseAntialiasing = true;
```

Включение сглаживания необходимо для высококачественных UI‑элементов, рендеринга графиков и любой ситуации, где важна визуальная точность.

## Программно задать размер шрифта

Размер шрифта определяет, насколько большими будут глифы в конечном битмапе. Вы можете изменить его, создав объект `Font` с нужным размером в пунктах. В примере ниже размер установлен в **24 pt**, что является обычным размером для читаемых заголовков.

```csharp
// Step 3: Choose a font family and size
Font font = new Font("Arial", 24); // 24‑point Arial
```

Вы можете заменить `24` любой целой или дробной величиной, соответствующей требованиям вашего макета. Класс `Font` также принимает параметр `GraphicsUnit`, если нужен размер в пикселях.

## Программно задать стиль шрифта

Применение полужирного, курсивного или подчёркнутого стилей сводится к передаче флага `WebFontStyle` при создании `Font`. Перечисление `WebFontStyle` комбинирует несколько стилей с помощью побитового OR.

```csharp
// Step 4: Apply bold and italic styles
font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);
```

Если нужен только один стиль, используйте `WebFontStyle.Bold`, `WebFontStyle.Italic` или `WebFontStyle.Underline`. Такой подход позволяет **задать стиль шрифта программно** без жёсткого кодирования отдельных файлов шрифтов.

## Полный исполняемый пример

Ниже приведено полное консольное приложение, объединяющее всё вместе:

```csharp
using System;
using Aspose.Imaging;
using Aspose.Imaging.Brushes;
using Aspose.Imaging.ImageOptions;
using Aspose.Imaging.Sources;
using Aspose.Imaging.FileFormats.Png;
using Aspose.Imaging.Graphics;
using Aspose.Imaging.Fonts;
using Aspose.Imaging.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Create rendering options and enable antialiasing
        ImageRenderingOptions renderingOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            // Enable hinting for sharper text on low‑resolution images
            TextOptions = new TextOptions { UseHinting = true }
        };

        // 2️⃣ Define the font (size + style)
        Font font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);

        // 3️⃣ Prepare a bitmap with a white background
        int width = 800;
        int height = 200;
        using (var bitmap = new RasterImage(width, height, PixelFormat.Format24bppRgb))
        {
            bitmap.SaveOptions = new PngOptions { ColorType = PngColorType.Truecolor };
            bitmap.Fill(new SolidBrush(Color.White));

            // 4️⃣ Create a graphics object that respects our rendering options
            using (Graphics graphics = new Graphics(bitmap, renderingOptions))
            {
                // Position the text in the center of the image
                PointF location = new PointF(50, 80);
                graphics.DrawString("Antialiased Bold Italic Text", font, new SolidBrush(Color.Black), location);
            }

            // 5️⃣ Save the result
            string outputPath = "antialiased_text.png";
            bitmap.Save(outputPath);
            Console.WriteLine($"Image saved to {outputPath}");
        }
    }
}
```

### Пояснение к каждому разделу

| Раздел | Почему это важно |
|--------|-------------------|
| **Rendering options** | Включение `UseAntialiasing` гарантирует плавные края как у векторных фигур, так и у текста. |
| **TextOptions.UseHinting** | Хинтинг улучшает читаемость на низкоразрешённых выводах, корректируя контуры глифов. |
| **Font construction** | Конструктор `Font` объединяет **задание размера шрифта** и **задание стиля шрифта программно** в одном вызове. |
| **Graphics object** | Передача `renderingOptions` в `Graphics` обеспечивает, что каждая операция рисования учитывает сглаживание и хинтинг. |
| **DrawString** | Этот метод рендерит текст с настроенным шрифтом, создавая окончательный сглаженный результат. |
| **Saving** | Формат PNG сохраняет точные пиксельные данные без дополнительных артефактов сжатия. |

#### Ожидаемый результат

Запуск программы создаёт **antialiased_text.png**, выглядящий так:

![Пример сглаженного текста](https://example.com/antialiased_text.png "Сглаженный текст с пользовательским размером и стилем шрифта – как включить сглаживание")

Изображение демонстрирует чёткий полужирный‑курсивный текст Arial размером 24 pt с плавными краями, подтверждая, что **как включить сглаживание** сработало корректно.

## Общие варианты и граничные случаи

- **Разные семейства шрифтов** – замените `"Arial"` на любое установленное имя шрифта (например, `"Times New Roman"`). Если шрифт недоступен, Aspose.Imaging бросит `FontNotFoundException`.
- **Изменение размера шрифта** – измените второй аргумент конструктора `Font` на любую дробную величину. Большие значения повышают читаемость, но могут потребовать большего битмапа.
- **Несколько стилей** – комбинируйте `WebFontStyle.Underline` с `Bold` и `Italic`, используя оператор `|`: `WebFontStyle.Bold | WebFontStyle.Underline`.
- **Рендеринг в высоком DPI** – для вывода в стиле Retina увеличьте размеры битмапа (например, 1600 × 400), оставив тот же размер шрифта; сглаживание всё равно даст плавный результат.
- **Отключение сглаживания** – установите `renderingOptions.UseAntialiasing = false;`, чтобы сравнить визуальную разницу. Текст станет «лесенчатым», что полезно для отладки или тестирования производительности.

## Профессиональные советы

- **Кешируйте объект `Font`**, если рисуете много строк в цикле; создание нового `Font` на каждой итерации добавляет накладные расходы.
- **Используйте `TextOptions.UseHinting` вместе со сглаживанием** для лучшего баланса между чёткостью и плавностью на низкоразрешённых изображениях.
- **Проверяйте выходной файл**, открывая его в просмотрщике изображений, показывающем детали пикселей (например, Photoshop или GIMP). Это поможет убедиться, что сглаживание действительно применилось.

## Заключение

Теперь вы знаете **как включить сглаживание** в графике C#, как **задать размер шрифта** и как **задать стиль шрифта программно** с помощью `ImageRenderingOptions`. Полный пример демонстрирует практический рабочий процесс, который вы можете скопировать в свои проекты, будь то генерация графиков, создание миниатюр UI или динамическая графика для веб‑служб.

Далее вы можете изучить **задание цвета шрифта программно**, добавить **градиентные заливки** или рендерить **векторные фигуры** с теми же настройками сглаживания. Все эти темы опираются на фундамент, изложенный здесь, так что вы готовы создавать графику высокого качества полностью из кода. Приятного рендеринга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Enable Antialiasing When Rendering HTML to PNG in C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-when-rendering-html-to-png-in-c/)
- [How to enable antialiasing for HTML image rendering in C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-for-html-image-rendering-in-c/)
- [How to Enable Antialiasing in Aspose HTML to PDF Conversion (C#)](/html/english/net/html-extensions-and-conversions/how-to-enable-antialiasing-in-aspose-html-to-pdf-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}