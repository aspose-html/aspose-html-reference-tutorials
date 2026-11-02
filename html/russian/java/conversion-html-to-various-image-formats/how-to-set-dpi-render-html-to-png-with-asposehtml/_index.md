---
category: general
date: 2026-01-14
description: как установить DPI при конвертации URL в PNG. Узнайте, как рендерить
  HTML в PNG, задавать размер области просмотра и сохранять HTML как PNG с помощью
  Aspose.HTML в Java.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: ru
og_description: как установить DPI при конвертации URL в PNG. Пошаговое руководство
  по рендерингу HTML в PNG, управлению размером области просмотра и сохранению HTML
  как PNG с помощью Aspose.HTML.
og_title: как установить dpi – рендеринг HTML в PNG с помощью AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: как задать dpi – преобразование HTML в PNG с AsposeHTML
url: /ru/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как установить dpi – рендеринг HTML в PNG с AsposeHTML

Когда‑нибудь задавались вопросом, **как установить dpi** для изображения, похожего на скриншот, сгенерированного из веб‑страницы? Возможно, вам нужен PNG с 300 DPI для печати или низкокачественная миниатюра для мобильного приложения. В любом случае, трюк заключается в том, чтобы сообщить движку рендеринга желаемый логический DPI, а затем позволить ему выполнить всю тяжелую работу.  

В этом руководстве мы возьмём живой URL, отрендерим его в файл PNG, **установим размер области просмотра**, скорректируем DPI и, наконец, **сохраним HTML как PNG** — всё это с помощью Aspose.HTML for Java. Никаких внешних браузеров, никаких громоздких инструментов командной строки — только чистый Java‑код, который можно добавить в любой проект Maven или Gradle.

> **Совет:** Если вам нужна лишь быстрая миниатюра, можете оставить DPI на уровне 96 DPI (по умолчанию для большинства экранов). Для готовых к печати ресурсов увеличьте его до 300 DPI или выше.

![пример установки dpi](https://example.com/images/how-to-set-dpi.png "пример установки dpi")

## Что понадобится

- **Java 17** (или любой современный JDK).  
- **Aspose.HTML for Java** 24.10 или новее. Вы можете получить его из Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Подключение к Интернету для получения целевой страницы (в примере используется `https://example.com/sample.html`).  
- Разрешение на запись в папку вывода.

И всё — без Selenium, без headless Chrome. Aspose.HTML выполняет рендеринг в процессе, что означает, что вы остаётесь внутри JVM и избегаете накладных расходов на запуск браузера.

## Шаг 1 – Загрузка HTML‑документа из URL

Сначала мы создаём экземпляр `HTMLDocument`, указывающий на страницу, которую хотим захватить. Конструктор автоматически загружает HTML, парсит его и подготавливает DOM.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Почему это важно:* Загружая документ напрямую, вы избавляетесь от необходимости использовать отдельный HTTP‑клиент. Aspose.HTML учитывает перенаправления, cookies и даже базовую аутентификацию, если вы встраиваете учётные данные в URL.

## Шаг 2 – Создание sandbox‑окружения с нужным DPI и областью просмотра

**Sandbox** — это способ Aspose.HTML имитировать браузерную среду. Здесь мы заставляем его «думать», что это экран 1280 × 720, и, что особенно важно, задаём **device DPI**. Изменение DPI меняет плотность пикселей отрендеренного изображения без изменения логического размера.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Почему вы можете менять эти значения:*  
- **Viewport size** контролирует, как работают CSS‑медиа‑запросы (`@media (max-width: …)`).  
- **Device DPI** влияет на физический размер изображения при печати. Изображение с 96 DPI выглядит нормально на экранах; изображение с 300 DPI сохраняет чёткость на бумаге.  

Если вам нужна квадратная миниатюра, просто измените `setViewportSize(500, 500)` и оставьте DPI низким.

## Шаг 3 – Выбор PNG в качестве формата вывода

Aspose.HTML поддерживает несколько растровых форматов (PNG, JPEG, BMP, GIF). PNG — без потерь, что делает его идеальным для скриншотов, где требуется сохранить каждый пиксель.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

Вы также можете настроить уровень сжатия (`pngOptions.setCompressionLevel(9)`), если вас беспокоит размер файла.

## Шаг 4 – Рендеринг и сохранение изображения

Теперь мы просим документ **сохранить** себя как изображение. Метод `save` принимает путь к файлу и ранее настроенные параметры.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Когда программа завершится, вы найдёте PNG‑файл по пути `YOUR_DIRECTORY/sandboxed.png`. Откройте его — если вы задали DPI 300, метаданные изображения отразят это, хотя пиксельные размеры останутся 1280 × 720.

## Шаг 5 – Проверка DPI (необязательно, но полезно)

Если вы хотите двойной проверкой убедиться, что DPI действительно применён, можете прочитать метаданные PNG с помощью лёгкой библиотеки, такой как **metadata‑extractor**:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Вы должны увидеть `300` (или то значение, которое задали) выведенным в консоль. Этот шаг не обязателен для **рендеринга**, но это быстрая проверка, особенно когда вы **генерируете** ресурсы для **печати**.

## Часто задаваемые вопросы и особые случаи

### «Что если страница использует JavaScript для загрузки контента?»

Aspose.HTML выполняет **ограниченный набор** JavaScript. Для большинства статических сайтов это работает сразу же. Если страница сильно зависит от клиентских **фреймворков** (React, Angular, Vue), вам может потребоваться предварительно отрендерить страницу или использовать headless‑браузер. Тем не менее, установка DPI работает одинаково, как только DOM готов.

### «Можно ли отрендерить PDF вместо PNG?»

Конечно. Замените `ImageSaveOptions` на `PdfSaveOptions` и измените расширение выходного файла на `.pdf`. Настройка DPI по‑прежнему влияет на растровый вид любых встроенных изображений.

### «А как насчёт скриншотов высокого разрешения для Retina‑дисплеев?»

Просто удвойте размеры viewport, оставив DPI на уровне 96 DPI, либо оставьте viewport и увеличьте DPI до 192. Получившийся PNG будет содержать вдвое больше пикселей, обеспечивая чёткое ощущение Retina.

### «Нужно ли освобождать ресурсы?»

`HTMLDocument` реализует `AutoCloseable`. В продакшн‑приложении оберните его в блок try‑with‑resources:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

Это гарантирует своевременное освобождение нативных ресурсов.

## Полный рабочий пример (готовый к копированию и вставке)

Ниже представлен полный, готовый к запуску код. Замените `YOUR_DIRECTORY` реальной папкой на вашем компьютере.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Запустите класс, и вы получите PNG, который учитывает указанные вами настройки **how to set dpi**.

## Заключение

Мы прошли процесс **how to set dpi** при **рендеринге HTML в PNG**, рассмотрели шаг **set viewport size** и показали, как **сохранить HTML как PNG** с помощью Aspose.HTML for Java. Основные выводы:

- Используйте **sandbox** для управления DPI и viewport.  
- Выбирайте правильные **ImageSaveOptions** для безпотерьного вывода.  
- Проверьте метаданные DPI, если необходимо гарантировать качество печати.  

Отсюда вы можете экспериментировать с различными значениями DPI, большими viewport или даже пакетно обрабатывать список URL‑ов. Хотите преобразовать весь сайт в PNG‑миниатюры? Просто пройдитесь по массиву URL‑ов и повторно используйте ту же конфигурацию sandbox.

Удачного рендеринга, и пусть ваши скриншоты всегда будут пиксельно‑идеальными!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}