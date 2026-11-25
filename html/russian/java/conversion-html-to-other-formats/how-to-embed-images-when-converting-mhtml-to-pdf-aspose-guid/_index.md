---
category: general
date: 2026-03-29
description: Как внедрять изображения при конвертации MHTML в PDF с помощью Aspose HTML.
  Сократите размер PDF‑файла и освоите техники преобразования Aspose HTML в PDF за
  считанные минуты.
draft: false
keywords:
- how to embed images
- convert mhtml to pdf
- reduce pdf file size
- aspose html to pdf
- reduce pdf size
language: ru
og_description: Как внедрять изображения при конвертации MHTML в PDF с помощью Aspose
  HTML. Узнайте, как уменьшить размер PDF‑файла и получить максимум от Aspose HTML
  to PDF.
og_title: Как встроить изображения при конвертации MHTML в PDF – руководство Aspose
tags:
- Aspose
- Java
- PDF
- MHTML
title: Как встраивать изображения при конвертации MHTML в PDF – руководство Aspose
url: /ru/java/conversion-html-to-other-formats/how-to-embed-images-when-converting-mhtml-to-pdf-aspose-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как встраивать изображения при конвертации MHTML в PDF – руководство Aspose

Когда‑нибудь задавались вопросом **как встраивать изображения** при конвертации MHTML‑в‑PDF и сохранять полученный файл лёгким? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда их PDF‑файлы разрастаются, потому что каждый ресурс — шрифты, скрипты, даже крошечные иконки — помещается внутрь. Хорошая новость? С Aspose.HTML for Java вы можете указать конвертеру встраивать **только изображения**, а всё остальное оставлять внешними ссылками. Эта небольшая настройка часто резко уменьшает размер PDF.

В этом руководстве мы пройдем процесс конвертации отчёта MHTML в PDF, сосредоточимся на **том, как встраивать изображения**, и добавим несколько советов по **уменьшению размера PDF‑файла**. К концу вы получите готовый к запуску Java‑класс, поймёте, почему встраивание только изображений имеет значение, и узнаете, куда обратиться, если позже понадобится встраивать шрифты или другие ресурсы. Никаких расплывчатых «см. документацию» обходных путей — только полное решение, готовое к копированию.

## Что вы узнаете

- Точные вызовы API, необходимые для **конвертации MHTML в PDF** с помощью Aspose.HTML.  
- Как настроить `PdfConversionOptions`, чтобы конвертер **встраивал только изображения**.  
- Почему встраивание только изображений помогает **уменьшить размер PDF** и когда может потребоваться другая настройка.  
- Полный, исполняемый пример на Java, который можно добавить в любой проект Maven/Gradle.  
- Распространённые подводные камни (отсутствующие ресурсы, неверные пути к файлам) и быстрые решения.

### Предварительные требования

- Установлен Java 8 или новее.  
- Maven или Gradle для управления зависимостями (мы покажем фрагмент Maven).  
- Библиотека Aspose.HTML for Java (можно взять бесплатную пробную версию с сайта Aspose).  
- Файл MHTML, который нужно превратить в PDF (в примере используется `report.mhtml`).

> **Pro tip:** Держите ваш MHTML и результирующий PDF в одной папке во время тестирования; относительные пути упрощают работу.

---

## Шаг 1 – Добавьте Aspose.HTML в ваш проект

Если вы используете Maven, вставьте следующее в ваш `pom.xml`. Показанная версия — последняя на март 2026; проверяйте репозиторий Aspose на наличие более новых релизов.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

Для Gradle эквивалент выглядит так:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

После того как зависимость будет разрешена, вы сможете импортировать необходимые классы.

## Шаг 2 – Создайте параметры конвертации и задайте режим встраивания

Суть **того, как встраивать изображения** кроется в `PdfConversionOptions`. По умолчанию Aspose встраивает *все* ресурсы (шрифты, CSS, изображения). Мы изменим это на `EMBED_IMAGES_ONLY`.

```java
// Step 2: Prepare conversion options – embed only images
PdfConversionOptions options = new PdfConversionOptions();
options.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);
```

Зачем это нужно? Представьте корпоративный отчёт, который ссылается на корпоративный шрифт, хранящийся на сетевом диске. Встраивание этого шрифта увеличивает PDF на сотни килобайт, хотя просмотрщик может загрузить его удалённо. Встраивая только изображения, PDF сохраняет нужную визуальную точность и остаётся лёгким.

## Шаг 3 – Выполните конвертацию

Теперь вызываем `Converter.convert`, передавая путь к исходному MHTML, путь к целевому PDF и только что настроенные параметры.

```java
// Step 3: Convert MHTML to PDF using the options above
String sourcePath = "YOUR_DIRECTORY/report.mhtml";
String targetPath = "YOUR_DIRECTORY/report.pdf";

Converter.convert(sourcePath, targetPath, options);
```

Если всё настроено правильно, рядом с вашим файлом MHTML появится `report.pdf`. Откройте его — все картинки из оригинального отчёта должны быть на месте, а шрифты и CSS останутся внешними ссылками.

## Шаг 4 – Проверьте уменьшение размера PDF

Быстрая проверка помогает убедиться, что вы действительно **уменьшили размер PDF**. Сравните размер файла до и после изменения режима встраивания:

```java
File before = new File("YOUR_DIRECTORY/report_full.pdf"); // generated with default settings
File after  = new File(targetPath); // our image‑only PDF

System.out.println("Full embed size: " + before.length() / 1024 + " KB");
System.out.println("Images‑only size: " + after.length() / 1024 + " KB");
```

В большинстве случаев вы увидите снижение на 30‑70 % в зависимости от количества шрифтов или CSS‑файлов, которые изначально встраивались. Это значительный выигрыш для тех, кто распространяет PDF‑файлы через веб или хранит их в облачном бакете.

## Шаг 5 – Полный, исполняемый пример

Ниже представлен весь Java‑класс, который можно скопировать в вашу IDE. Замените `YOUR_DIRECTORY` реальным путём к папке, где находится `report.mhtml`.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.converters.ResourceEmbeddingMode;

import java.io.File;

public class MhtmlToPdf {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define source and destination ----------
        String sourcePath = "YOUR_DIRECTORY/report.mhtml";
        String targetPath = "YOUR_DIRECTORY/report.pdf";

        // ---------- Step 2: Set conversion options (embed only images) ----------
        PdfConversionOptions conversionOptions = new PdfConversionOptions();
        conversionOptions.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);

        // ---------- Step 3: Run the conversion ----------
        Converter.convert(sourcePath, targetPath, conversionOptions);
        System.out.println("Conversion complete! PDF saved to: " + targetPath);

        // ---------- Step 4: (Optional) Show size reduction ----------
        File outputPdf = new File(targetPath);
        System.out.println("Resulting PDF size: " + outputPdf.length() / 1024 + " KB");
    }
}
```

**Ожидаемый вывод** (в консоли):

```
Conversion complete! PDF saved to: YOUR_DIRECTORY/report.pdf
Resulting PDF size: 842 KB
```

Откройте `report.pdf` в любом просмотрщике; вы должны увидеть все оригинальные изображения, отрисованные корректно. Если заметите пропавшие картинки, проверьте, что URL‑адреса изображений в MHTML являются абсолютными или что файлы доступны машине, выполняющей конвертацию.

## Часто задаваемые вопросы и обработка граничных случаев

### Что если мне *нужно* встраивать шрифты?

Переключите `ResourceEmbeddingMode` на `EMBED_ALL` или `EMBED_FONTS_ONLY`. Перечисление предлагает четыре варианта:

| Mode                     | Что встраивается |
|--------------------------|-------------------|
| `EMBED_ALL`              | Изображения, шрифты, CSS |
| `EMBED_IMAGES_ONLY`      | Только изображения (по умолчанию) |
| `EMBED_FONTS_ONLY`       | Только шрифты |
| `EMBED_NONE`             | Ничего (только внешние ссылки) |

### Мой MHTML содержит внешние CSS, влияющие на макет — будет ли PDF выглядеть испорченным?

Поскольку мы не встраиваем CSS, конвертер всё равно загрузит его во время конвертации. Если CSS размещён во внутренней сети, недоступной серверу конвертации, макет может вернуться к значениям по умолчанию. В таких случаях либо встраивайте CSS (`EMBED_ALL`), либо скопируйте таблицу стилей локально и измените MHTML, чтобы он указывал на локальный файл.

### Можно ли пакетно обрабатывать папку файлов MHTML?

Конечно. Оберните логику конвертации в цикл, который проходит по `File.listFiles()` и меняет имя целевого файла соответственно. Просто не забудьте переиспользовать один экземпляр `PdfConversionOptions` для повышения производительности.

### Что насчёт потребления памяти при работе с огромными документами?

Aspose.HTML потоково обрабатывает контент, поэтому использование памяти остаётся умеренным. Однако очень большие изображения могут вызвать всплески памяти. Если вы получаете `OutOfMemoryError`, рассмотрите возможность уменьшения разрешения изображений перед встраиванием — Aspose предоставляет `ImageConversionOptions` для этого, но это тема другого руководства.

## Заключение

Теперь вы знаете **как встраивать изображения** при конвертации MHTML в PDF с помощью Aspose.HTML и видели, почему эта небольшая настройка может **значительно уменьшить размер PDF**. Полный пример на Java, готовый к копированию, демонстрирует весь процесс — от добавления зависимости Maven до вывода окончательного размера файла.

Отсюда вы можете:

- Поэкспериментировать с `EMBED_FONTS_ONLY`, если ваши PDF‑файлы должны быть полностью автономными.  
- Автоматизировать пакетную конвертацию для всей папки отчётов.  
- Скомбинировать эту технику с API оптимизации PDF от Aspose для ещё более небольших файлов.

Независимо от того, создаёте ли вы сервис отчётности, конвейер email‑в‑PDF или просто упорядочиваете архивные веб‑страницы, контроль над тем, что встраивается, — ключевой рычаг для повышения производительности и снижения затрат. Попробуйте, настройте параметры и держите ваши PDF‑файлы как можно более лёгкими.

*Счастливого кодинга!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}