---
date: 2026-05-30
description: Узнайте, как конвертировать EPUB в PDF на Java с помощью Aspose.HTML,
  задавая пользовательский размер страницы PDF и другие параметры сохранения PDF.
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: Указание параметров сохранения PDF для EPUB в PDF
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Пользовательский размер страницы PDF - Указание параметров сохранения PDF для
  EPUB в PDF
url: /ru/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пользовательский размер страницы PDF: указание параметров сохранения PDF для EPUB в PDF

## Введение

Aspose.HTML for Java упрощает **конвертацию EPUB в PDF** и предоставляет полный контроль над выводом, включая установку **пользовательского размера страницы PDF**. В этом пошаговом руководстве мы пройдем всё необходимое — от подготовки среды до настройки `PdfSaveOptions`, чтобы сгенерированный PDF точно соответствовал требуемым размерам страниц. Независимо от того, создаёте ли вы конвейер публикаций, платформу электронного обучения или просто автоматизируете конвертацию документов, представленные техники будут вам полезны.

## Быстрые ответы
- **Какова основная цель этого руководства?** Конвертировать файл EPUB в PDF с применением пользовательского размера страницы PDF.  
- **Какая библиотека используется?** Aspose.HTML for Java.  
- **Нужна ли лицензия?** Доступна бесплатная пробная версия; для продакшна требуется коммерческая лицензия.  
- **Можно ли изменить цвет фона?** Да, с помощью `PdfSaveOptions`.  
- **Поддерживается ли Java 8+?** Абсолютно — любой современный Java‑runtime подходит.

## Что такое пользовательский размер страницы PDF?

Пользовательский размер страницы PDF позволяет задать точную ширину и высоту каждой страницы в итоговом PDF, вместо использования стандартных размеров, таких как A4 или Letter.  
Вы можете задавать размеры в пунктах (1 point = 1/72 дюйма) или конвертировать их из пикселей, получая пиксель‑точный контроль над финальной разметкой. Это идеально для электронных книг, листовок или любого дизайна, который должен соответствовать заранее определённому формату без последующей ручной обработки.

## Почему стоит использовать Aspose.HTML для конвертации EPUB в PDF?

Aspose.HTML преобразует EPUB в PDF всего в два строки кода, сохраняя сложные макеты, встроенные шрифты и изображения высокого разрешения. Библиотека поддерживает **более 50 форматов ввода и вывода**, может рендерить PDF до **2 000 страниц** без загрузки всего файла в память и работает на Windows, Linux и macOS с одинаковыми результатами. Кроме того, библиотека предоставляет детальные параметры сохранения PDF, позволяя настраивать размер страницы, цвет фона, отступы и степень сжатия — всё из Java.

## Предварительные требования
- **Среда разработки Java:** установленный и настроенный JDK 8 или новее.  
- **Aspose.HTML for Java:** скачайте последнюю JAR‑файл с [веб‑сайта](https://releases.aspose.com/html/java/).  
- **Файл EPUB:** документ `.epub`, который вы хотите конвертировать.  

Теперь, когда всё готово, приступим к реальным шагам конвертации.

## Как конвертировать EPUB в PDF с пользовательским размером страницы?

`FileInputStream` — класс Java, читающий необработанные байты из файла.  
`PdfSaveOptions` — класс в Aspose.HTML, конфигурирующий параметры вывода PDF, такие как размер страницы и цвет фона.  
Загрузите ваш EPUB с помощью `FileInputStream`, настройте `PdfSaveOptions` для указания точных размеров страниц и вызовите конвертер. Ниже представлена трёхшаговая последовательность, выполняющая конвертацию менее чем за минуту для типичных размеров электронных книг и масштабируемая для больших коллекций с минимальными изменениями кода.

### Шаг 1: Открыть файл EPUB

Сначала создайте `FileInputStream`, указывающий на ваш исходный `.epub`. Оставляйте поток открытым до завершения конвертации, чтобы избежать ошибок «пустой страницы».

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### Шаг 2: Определить параметры сохранения PDF

`PdfSaveOptions` — класс конфигурации Aspose.HTML, управляющий настройками вывода PDF, включая размер страницы, цвет фона и отступы.  
`Length.fromPixels` преобразует пиксели экрана в пункты PDF (1 пункт = 1/72 дюйма), позволяя задавать размеры в привычных пиксельных единицах.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

#### Совет профессионала:
- **Пиксели vs. Пункты:** `Length.fromPixels` преобразует пиксели экрана в пункты PDF (1 пункт = 1/72 дюйма). Выбирайте значения, соответствующие конечному размеру печати, который вам нужен.

### Шаг 3: Конвертировать EPUB в PDF

Имея поток ввода и пользовательские параметры, вызовите конвертер. Выходной PDF будет сохранён в указанное вами место, сохраняя точно те размеры страниц, которые вы задали.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` — метод, включающий параллельную обработку страниц во время конвертации PDF.

## Полный исходный код

Полный, готовый к запуску пример объединяет три шага выше в один Java‑класс. Замените шаблонные пути на свои собственные местоположения файлов.

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Распространённые проблемы и их решения

| Проблема | Причина | Решение |
|----------|----------|----------|
| **PDF‑страницы пустые** | Поток ввода закрыт до завершения конвертации | Оставьте блок `try‑with‑resources` открытым до завершения `convertEPUB`. |
| **Неправильные размеры страниц** | Используются пиксели, которые не соответствуют требуемому размеру печати | Преобразуйте желаемые дюймы в пункты (`1 inch = 72 points`), а затем в пиксели с помощью `Length.fromPixels`. |
| **Отсутствуют шрифты** | Шрифты не вложены в EPUB | Убедитесь, что шрифты упакованы внутри EPUB или установите их на хост‑машине. |
| **Снижение производительности при больших книгах** | Отрисовка каждой страницы последовательно | Включите многопоточную отрисовку через `PdfSaveOptions.setEnableParallelProcessing(true)` для ускорения обработки EPUB‑книг более 500 страниц. |

## Часто задаваемые вопросы (FAQ)

**Q:** Является ли Aspose.HTML for Java бесплатной библиотекой?  
**A:** Aspose.HTML for Java — коммерческая библиотека, но вы можете получить бесплатную пробную версию с их [веб‑сайта](https://releases.aspose.com/html/java/).

**Q:** Какие форматы EPUB поддерживаются для конвертации?  
**A:** Aspose.HTML for Java поддерживает EPUB 2.0, EPUB 3.0 и EPUB 3.1, обрабатывая книги с переflow‑able и фиксированным макетом с полной поддержкой CSS.

**Q:** Можно ли дальше настраивать вывод PDF?  
**A:** Да, вы можете настроить вывод PDF, изменяя параметры страницы, цвет фона, уровень сжатия и другие настройки в `PdfSaveOptions`.

**Q:** Есть ли ограничения у пробной версии Aspose.HTML for Java?  
**A:** Пробная версия может добавлять водяной знак на первые несколько страниц и ограничивает максимальный размер файла до 10 МБ; покупка лицензии снимает эти ограничения.

**Q:** Где можно получить поддержку по Aspose.HTML for Java?  
**A:** Ответы на вопросы и поддержку можно найти на [форуме Aspose.HTML](https://forum.aspose.com/).

---

**Последнее обновление:** 2026-05-30  
**Тестировано с:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Автор:** Aspose

## Связанные руководства

- [Настройка размера страницы PDF с помощью Aspose.HTML для Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Как конвертировать EPUB в PDF с помощью Java — используя Aspose.HTML](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [Конвертация EPUB в PDF и изображения с Aspose.HTML for Java](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}