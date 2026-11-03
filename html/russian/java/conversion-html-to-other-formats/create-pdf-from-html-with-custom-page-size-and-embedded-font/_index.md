---
category: general
date: 2026-03-05
description: Быстро создавайте PDF из HTML с помощью Aspose.HTML — задавайте пользовательский
  размер страницы PDF, внедряйте шрифты и изучайте, как конвертировать HTML в PDF
  с полным кодом.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- html to pdf conversion
- custom pdf page size
- embed fonts pdf
language: ru
og_description: Создайте PDF из HTML с помощью Aspose.HTML. Это руководство показывает,
  как установить пользовательский размер страницы PDF, внедрить шрифты в PDF и выполнить
  преобразование HTML в PDF.
og_title: Создать PDF из HTML — пользовательский размер страницы и встроенные шрифты
tags:
- Java
- PDF
- Aspose.HTML
title: Создать PDF из HTML с пользовательским размером страницы и встроенными шрифтами
url: /ru/java/conversion-html-to-other-formats/create-pdf-from-html-with-custom-page-size-and-embedded-font/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF из HTML с пользовательским размером страницы и встраиванием шрифтов

Когда‑то вам нужно **создать PDF из HTML**, но вы застряли на этапе стилизации? Вы не одиноки. Будь то преобразование маркетинговой посадочной страницы в печатный брошюру или архивирование счетов, сгенерированных в веб‑приложении, вам, скорее всего, нужен PDF, точно соответствующий размерам вашего бренда и сохраняющий чёткость всех шрифтов.  

В этом руководстве мы пройдемся по полностью готовому к запуску примеру, который показывает, как **конвертировать HTML в PDF** с помощью Aspose.HTML for Java, задать **пользовательский размер страницы PDF** и включить **встраивание шрифтов PDF**, чтобы результат выглядел одинаково на любой машине. К концу вы получите один Java‑класс, который можно добавить в проект и сразу начинать генерировать PDF‑файлы.

## Что вы узнаете

* Как добавить библиотеку Aspose.HTML в проект Maven или Gradle.  
* Как настроить **PdfConversionOptions** для **пользовательского размера страницы PDF** (в данном случае 8,5 × 11 дюймов).  
* Как включить **embed fonts pdf**, чтобы текст отображался корректно даже при отсутствии оригинальных шрифтов на целевой системе.  
* Как выполнить **HTML to PDF conversion** и получить количество страниц в полученном документе.  

Без лишних слов, только практическое решение «от начала до конца», которое можно скопировать‑вставить.

## Предварительные требования

Прежде чем приступить, убедитесь, что у вас есть:

* Установленный Java 17 или новее (API работает с Java 8+, но более новые JDK дают лучшую производительность).  
* Инструмент сборки — Maven или Gradle — для загрузки JAR‑файла Aspose.HTML из репозитория Maven Central.  
* HTML‑файл (`sample.html`), который вы хотите превратить в PDF.  
* Небольшой интерес к макетам PDF‑страниц — об этом мы расскажем в коде.

> **Pro tip:** Если у вас нет готового HTML‑файла, просто создайте простой с `<h1>` и абзацем; конверсия будет работать так же.

## Шаг 1: Добавьте Aspose.HTML в ваш проект (Convert HTML to PDF)

Если вы используете **Maven**, поместите следующую зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- latest at time of writing -->
</dependency>
```

Для **Gradle** добавьте эту строку в `build.gradle`:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Эта единственная строка даст вам всё необходимое для **html to pdf conversion** — `Converter`, классы опций и утилиты рисования.

## Шаг 2: Настройте пользовательский размер страницы PDF (Custom PDF Page Size)

Теперь, когда библиотека находится в classpath, можно начинать формировать вывод. Объект `PdfConversionOptions` позволяет задавать размеры страницы, отступы и включать встраивание шрифтов. Ниже код, который задаёт **custom pdf page size** 8,5 × 11 дюймов с полдюймовыми отступами со всех сторон:

```java
// Step 2: Create PDF conversion options and configure page size, margins, and font embedding
PdfConversionOptions pdfOptions = new PdfConversionOptions();

// Set a custom PDF page size – 8.5 × 11 inches (Letter)
pdfOptions.setPageSize(new SizeF(Unit.inch(8.5), Unit.inch(11)));

// Margins are also expressed in inches; here we use 0.5 in on each side
pdfOptions.setMargins(0.5, 0.5, 0.5, 0.5); // left, top, right, bottom

// Enable font embedding so the PDF looks the same everywhere
pdfOptions.setEmbedFonts(true);
```

Обратите внимание на вызов `setEmbedFonts(true)`. Это флаг, который говорит Aspose.HTML **embed fonts PDF** в файлы, устраняя проблему «отсутствующего шрифта», которую иногда видят при открытии PDF на другом компьютере.

## Шаг 3: Выполните конверсию HTML в PDF

С готовыми опциями сама конверсия сводится к одной строке. Мы указываем `Converter` исходный HTML‑файл и целевой PDF‑файл, а затем передаём построенные опции:

```java
// Step 3: Convert the HTML file to PDF using the configured options
String htmlPath = "YOUR_DIRECTORY/sample.html";
String pdfPath  = "YOUR_DIRECTORY/custom.pdf";

PdfConversionResult conversionResult = Converter.convertHTML(htmlPath, pdfPath, pdfOptions);
```

Если всё прошло успешно, `conversionResult` будет содержать метаданные о сгенерированном PDF, например количество страниц.

## Шаг 4: Проверьте результат — подсчёт страниц

Всегда полезно убедиться, что конверсия прошла успешно. `PdfConversionResult` предоставляет простой способ прочитать количество страниц:

```java
// Step 4: Output the number of pages in the generated PDF
System.out.println("Custom PDF created, pages: " + conversionResult.getPageCount());
```

Запуск программы должен вывести что‑то вроде:

```
Custom PDF created, pages: 1
```

Эта строка сообщает, что **html to pdf conversion** создал одностраничный PDF, соответствующий **custom pdf page size**, который вы задали. Если ваш исходный HTML длиннее, количество страниц увеличится автоматически.

## Полный рабочий пример

Ниже представлен полный Java‑класс, который можно скопировать в файл `ConvertHtmlToPdfWithOptions.java`. Замените `YOUR_DIRECTORY` на реальный путь к папке, где находится `sample.html`.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.pdf.PdfConversionOptions;
import com.aspose.html.converters.pdf.PdfConversionResult;
import com.aspose.html.drawing.SizeF;
import com.aspose.html.drawing.Unit;

public class ConvertHtmlToPdfWithOptions {
    public static void main(String[] args) throws Exception {

        // Step 1: Create PDF conversion options and configure page size, margins, and font embedding
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(new SizeF(Unit.inch(8.5), Unit.inch(11)));
        pdfOptions.setMargins(0.5, 0.5, 0.5, 0.5);   // left, top, right, bottom (in inches)
        pdfOptions.setEmbedFonts(true);            // embed fonts PDF for consistent rendering

        // Step 2: Convert the HTML file to PDF using the configured options
        String htmlPath = "YOUR_DIRECTORY/sample.html";
        String pdfPath  = "YOUR_DIRECTORY/custom.pdf";
        PdfConversionResult conversionResult = Converter.convertHTML(htmlPath, pdfPath, pdfOptions);

        // Step 3: Output the number of pages in the generated PDF
        System.out.println("Custom PDF created, pages: " + conversionResult.getPageCount());
    }
}
```

### Ожидаемый результат

После компиляции (`javac ConvertHtmlToPdfWithOptions.java`) и запуска класса (`java ConvertHtmlToPdfWithOptions`) вы найдёте `custom.pdf` в той же папке. Откройте его любой программой‑просмотрщиком PDF; вы увидите ваш оригинальный HTML, отрисованный на **custom pdf page size** с правильно встроенными шрифтами. Никаких предупреждений о недостающих глифах, никаких сдвигов макета.

![Создание PDF из HTML: пример с превью сгенерированного PDF](/images/create-pdf-from-html-preview.png "превью создания pdf из html")

## Часто задаваемые вопросы и особые случаи

**Что если мой HTML ссылается на внешние CSS или изображения?**  
Aspose.HTML следует тем же правилам, что и браузер. Пока пути абсолютные или относительные к расположению HTML‑файла, конвертер их подхватит. Для удалённых URL убедитесь, что машина, выполняющая конверсию, имеет доступ в интернет.

**Можно ли изменить ориентацию страницы на альбомную?**  
Конечно. Просто поменяйте местами значения ширины и высоты при вызове `setPageSize`:

```java
pdfOptions.setPageSize(new SizeF(Unit.inch(11), Unit.inch(8.5)));
```

**Нужна ли лицензия Aspose.HTML для продакшн‑использования?**  
Библиотека работает в режиме оценки, но добавляет водяной знак в PDF. Для коммерческих проектов требуется действующий файл лицензии — его достаточно загрузить в начале программы: `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`.

**А как насчёт Unicode‑шрифтов?**  
Если ваш HTML содержит нелатинские символы, убедитесь, что встраиваемые шрифты поддерживают эти кодовые точки. Включение `setEmbedFonts(true)` встроит весь файл шрифта, и PDF будет корректно отображать Unicode на любом устройстве.

## Заключение

Теперь вы точно знаете, как **создать PDF из HTML**, контролируя **custom pdf page size** и гарантируя **embed fonts PDF** для безупречного кросс‑платформенного рендеринга. Пример охватывает весь конвейер **html to pdf conversion** — от настройки зависимостей, через конфигурацию опций, до проверки результата.

Хотите идти дальше? Попробуйте поэкспериментировать с:

* **Несколькими размерами страниц** в одном документе (разные опции для каждой конверсии).  
* **Шаблонами заголовков/подвалов** с помощью `PdfPageSettings` в Aspose.HTML.  
* **Функциями безопасности**, например защитой паролем (`PdfEncryptionOptions`).  

Все эти возможности опираются на ту же основу, которую мы только что построили, так что вы будете готовы к их реализации без проблем.

Счастливого кодинга и приятного превращения веб‑страниц в идеально оформленные PDF!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}