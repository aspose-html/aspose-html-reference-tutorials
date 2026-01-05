---
category: general
date: 2026-01-04
description: Создайте PDF пользовательского размера из HTML в Java с помощью Aspose.HTML
  — узнайте, как установить размер страницы и увеличить DPI при конвертации HTML в
  PDF.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- html to pdf java
- set pdf page size
- increase pdf dpi
language: ru
og_description: Создайте PDF пользовательского размера из HTML в Java с помощью Aspose.HTML.
  Установите размер страницы, увеличьте DPI и выполните полное преобразование HTML
  в PDF.
og_title: Создание PDF пользовательского размера из HTML в Java – Полный учебник
tags:
- Java
- PDF
- Aspose
- HTML conversion
title: Создание PDF нестандартного размера из HTML в Java – полное руководство
url: /ru/java/conversion-html-to-other-formats/create-pdf-custom-size-from-html-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF пользовательского размера из HTML в Java – Полное руководство

Когда‑нибудь вам нужно было **создать PDF пользовательского размера** из HTML‑источника, но вы не знали, как контролировать размеры или чёткость изображений? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда вывод по умолчанию A4 выглядит некорректно для их шаблонов счетов или рекламных листовок.  

В этом руководстве мы пройдем через **полный, исполняемый пример**, который покажет, как **преобразовать HTML в PDF**, явно **устанавливая размер страницы PDF** и **увеличивая DPI PDF** для более чёткой графики. К концу вы получите готовый Java‑класс, который можно адаптировать под любой проект, требующий PDF пользовательского размера.

## Что понадобится

- **Java 17** или новее (код использует современный синтаксис `var`, но при необходимости можно откатить).  
- Библиотека **Aspose.HTML for Java** — рекомендуется версия 23.9 или новее.  
- HTML‑файл, который вы хотите превратить в PDF (назовём его `input.html`).  
- Немного уверенности в работе с IDE (IntelliJ IDEA, Eclipse или VS Code подойдут).  

Других зависимостей не требуется; JAR‑ы Aspose включают всё необходимое.

## Шаг 1: Добавьте Aspose.HTML в ваш проект

Если вы используете Maven, вставьте следующий фрагмент в ваш `pom.xml`. Для Gradle или простых JAR‑only настроек применимы те же координаты.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

> **Pro tip:** Aspose предлагает бесплатную оценочную лицензию, которую можно встроить как ресурсный файл. Просто разместите `Aspose.HTML.lic` в папке `src/main/resources`, и библиотека автоматически её подхватит.

## Шаг 2: Создайте Java‑класс для конвертации

Ниже полное исходное файл. Обратите внимание, что каждая строка прокомментирована, чтобы объяснить **почему** мы это делаем, а не только **что** делаем.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.rendering.PageSize;
import com.aspose.html.rendering.Unit;

/**
 * Demonstrates how to convert an HTML file to a PDF with a custom page size
 * and a higher DPI (dots per inch) for sharper images.
 *
 * Run this class from your IDE or via `java -cp <classpath> ConvertWithOptions`.
 */
public class ConvertWithOptions {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1: Prepare conversion options
        // -----------------------------------------------------------------
        PdfConversionOptions conversionOptions = new PdfConversionOptions();

        // Set the page size to A5 (148 mm × 210 mm) – you can change these numbers
        // to any dimensions you need, e.g., a custom flyer size.
        conversionOptions.setPageSize(new PageSize(Unit.MILLIMETERS, 148, 210));

        // Choose a higher resolution: 150 DPI gives noticeably sharper raster images.
        // The default is usually 96 DPI, which can look blurry on printed media.
        conversionOptions.setResolution(150);

        // -----------------------------------------------------------------
        // Step 2: Perform the conversion
        // -----------------------------------------------------------------
        // Replace "YOUR_DIRECTORY" with the actual folder where your files live.
        String inputHtml = "YOUR_DIRECTORY/input.html";
        String outputPdf = "YOUR_DIRECTORY/output.pdf";

        // The static convert method does the heavy lifting.
        Converter.convert(inputHtml, outputPdf, conversionOptions);

        // -----------------------------------------------------------------
        // Step 3: Confirmation
        // -----------------------------------------------------------------
        System.out.println("Custom conversion done. PDF created at: " + outputPdf);
    }
}
```

### Почему эти настройки важны

- **`setPageSize`** – По умолчанию Aspose использует A4 (210 mm × 297 mm). Изменив его, вы сможете подогнать содержимое под брошюру, чек или любой другой нестандартный формат.  
- **`setResolution`** – DPI влияет на растеризацию фоновых изображений CSS, SVG и даже рендеринг текста при просмотре PDF на экране. Более высокий DPI → больший размер файла, но более чёткий результат — идеально для печатных материалов.  

## Шаг 3: Запустите код и проверьте результат

1. Скомпилируйте класс:

   ```bash
   javac -cp "path/to/aspose-html.jar" ConvertWithOptions.java
   ```

2. Выполните его:

   ```bash
   java -cp ".:path/to/aspose-html.jar" ConvertWithOptions
   ```

3. Откройте `output.pdf` в любом PDF‑просмотрщике. Вы должны увидеть HTML, отрисованный на **странице формата A5** с заметно более чёткими изображениями.

> **Что если мне нужна альбомная ориентация?**  
> Просто поменяйте местами значения ширины и высоты при создании `PageSize`, либо используйте вспомогательный `PageSize.LANDSCAPE`, если предпочитаете более декларативный подход.

## Шаг 4: Распространённые варианты и граничные случаи

| Сценарий | Как адаптировать код |
|----------|-----------------------|
| **Разные единицы измерения (дюймы, пункты)** | Замените `Unit.MILLIMETERS` на `Unit.INCHES` или `Unit.POINTS`. |
| **Несколько HTML‑файлов в один PDF** | Создайте один объект `PdfConversionOptions`, затем многократно вызывайте `Converter.convert`, добавляя каждый вывод в один экземпляр `PdfDocument`. |
| **Динамический размер страницы для каждого документа** | Вычисляйте ширину/высоту во время выполнения (например, на основе конфигурации JSON) перед вызовом `setPageSize`. |
| **Запуск в веб‑службе** | Оберните логику конвертации в servlet или Spring‑контроллер, передавая PDF‑байты обратно как `application/pdf`. |
| **Ограничения памяти** | Используйте `PdfConversionOptions.setMemoryLimit(...)` для ограничения использования кучи; Aspose при необходимости будет использовать диск. |

## Шаг 5: Советы по устранению неполадок

- **Пустые страницы** – Убедитесь, что ваш HTML содержит элемент `<body>` и что все внешние CSS/JS ресурсы доступны из рабочей директории JVM.  
- **Отсутствие шрифтов** – Установите необходимые шрифты на сервере или внедрите их через `PdfConversionOptions.setFontEmbeddingMode(...)`.  
- **Неожиданный DPI** – Проверьте, что вы не переопределяете разрешение позже в конвейере (например, через пост‑процессор PDF).  

## Визуальная ссылка

Ниже быстрый скриншот сгенерированного PDF (портрет A5). Alt‑текст специально содержит ключевое слово для целей SEO.

![Создание PDF пользовательского размера пример](https://example.com/images/create-pdf-custom-size.png "Создание PDF пользовательского размера пример")

## Итоги: Что мы достигли

Мы **создали Java‑программу, конвертирующую HTML в PDF**, явно **устанавливающую пользовательский размер страницы** и **увеличивающую DPI** для более чёткого вывода. Решение автономно, использует только Aspose.HTML и может быть внедрено в любой Maven‑проект.

## Следующие шаги и смежные темы

- **Пакетная обработка:** Пройдитесь по каталогу HTML‑файлов и объедините их в один PDF.  
- **Продвинутое стилизование:** Используйте правила CSS `@page` для управления полями, заголовками и нижними колонтитулами.  
- **Соображения безопасности:** Очистите пользовательский HTML перед конвертацией, чтобы избежать внедрения скриптов.  

Если вас интересует более глубокая работа с PDF — например, добавление закладок, шифрование документа или наложение водяных знаков — ознакомьтесь с библиотекой Aspose **PDF for Java**. Она отлично сочетается с потоком конвертации HTML, который мы только что построили.

Счастливого кодинга, и пусть ваши PDF всегда имеют именно тот размер, который вам нужен!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}