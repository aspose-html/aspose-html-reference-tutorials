---
category: general
date: 2026-06-29
description: Узнайте, как установить DPI и разрешение изображения при конвертации
  HTML в PNG с помощью Aspose HTML Converter. Включён пошаговый пример на Java.
draft: false
keywords:
- how to set dpi
- convert html to png
- set image resolution
- convert html page
- aspose html converter
language: ru
og_description: Как установить DPI при конвертации HTML в Aspose. Это руководство
  показывает, как преобразовать HTML‑страницу в PNG‑изображение высокого разрешения
  на Java.
og_title: Как установить DPI при конвертации HTML в PNG – учебник Aspose HTML
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to set DPI and image resolution while converting HTML to
    PNG with Aspose HTML Converter. Step‑by‑step Java example included.
  headline: How to Set DPI When Converting HTML to PNG – Complete Aspose HTML Guide
  type: TechArticle
- description: Learn how to set DPI and image resolution while converting HTML to
    PNG with Aspose HTML Converter. Step‑by‑step Java example included.
  name: How to Set DPI When Converting HTML to PNG – Complete Aspose HTML Guide
  steps:
  - name: 1. Different Output Formats
    text: Aspose.HTML isn’t limited to PNG. Swap the file extension and use a matching
      options class, e.g., `JpegConversionOptions` for JPEGs. The DPI logic stays
      identical.
  - name: 2. Dynamically Determining Screen Size
    text: 'If you need the sandbox to mimic a mobile device, read the dimensions from
      a config file:'
  - name: 3. Batch Conversion
    text: Wrap the conversion call inside a loop that iterates over a directory of
      HTML files. Remember to reuse the same `Sandbox` and `ImageConversionOptions`
      objects to avoid unnecessary allocations.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Image Processing
title: Как установить DPI при конвертации HTML в PNG – Полное руководство Aspose HTML
url: /ru/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png-complete-aspose-h/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как установить DPI при конвертации HTML в PNG – Полное руководство по Aspose HTML

Когда‑нибудь задавались вопросом **как установить DPI** для PNG, который вы генерируете из HTML‑страницы? Во многих сценариях отчётности или автоматизации скриншотов значение по умолчанию 96 dpi просто недостаточно чёткое. Хорошая новость в том, что Aspose.HTML for Java даёт вам полный контроль над симуляцией экрана и разрешением изображения, так что вы можете увеличить DPI до 300 или даже 600, используя всего несколько строк кода.

В этом руководстве мы пройдём реальный пример на Java, который **конвертирует HTML‑страницу в PNG**, явно **устанавливая DPI** и **разрешение изображения**. К концу вы получите готовый к запуску класс, поймёте, почему каждое настройка важна, и узнаете, как подстроить её под разные задачи, такие как печать с высоким разрешением или веб‑миниатюры.

> **Быстрый обзор:** Основные шаги: (1) создать `Sandbox`, имитирующий экран, (2) задать его DPI, (3) настроить `ImageConversionOptions` с нужным разрешением и (4) вызвать `Converter.convert`. Никаких внешних инструментов, никаких командных строк — только чистый Java.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

- **Java 17** (или любой современный JDK), установленный и настроенный в вашей IDE.
- Библиотека **Aspose.HTML for Java** (Maven‑артефакт `com.aspose:aspose-html`). Последнюю версию можно взять из [репозитория Aspose Maven](https://repo.aspose.com/repo) или скачать JAR напрямую.
- Простой HTML‑файл (`page.html`), который вы хотите превратить в PNG. Поместите его в доступное место, например `C:/temp/page.html`.
- Базовое знакомство с обработкой исключений в Java — ничего сложного.

Если что‑то из перечисленного вам незнакомо, сделайте паузу и установите недостающие компоненты. Остальная часть руководства предполагает, что вы умеете открывать Java‑проект и добавлять внешние JAR‑файлы.

## Шаг 1: Настройте Maven‑проект (или добавьте JAR вручную)

Если вы используете Maven, добавьте зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.11</version> <!-- Check for the newest version -->
</dependency>
```

В противном случае поместите `aspose-html-*.jar` в папку `libs` вашего проекта и добавьте её в путь сборки. Этот шаг напрямую не связан с **тем, как установить DPI**, но без библиотеки вы не сможете получить доступ к классу `Sandbox`, который делает управление DPI возможным.

## Шаг 2: Создайте Sandbox, имитирующий реальный экран

*Sandbox* — это способ Aspose воспроизвести окружение браузера. Представьте его как виртуальный монитор, где вы задаёте ширину, высоту и, что главное, **DPI**. Ниже фрагмент кода, создающий экран 1024 × 768 при 96 dpi — базовый уровень перед тем, как мы повысим разрешение:

```java
// Step 2.1: Initialise the sandbox
Sandbox sandbox = new Sandbox();

// Step 2.2: Define virtual screen dimensions (pixels)
sandbox.setScreenWidth(1024);
sandbox.setScreenHeight(768);

// Step 2.3: Set the DPI – this is the key to controlling image sharpness
sandbox.setDpi(96); // Change this value to 300, 600, etc., later
```

> **Почему sandbox?** Без него Aspose будет использовать настройки экрана хост‑машины, что приводит к непоследовательным результатам на разных компьютерах разработчиков. Зафиксировав DPI, вы гарантируете одинаковый вид конвертации независимо от того, запускаете ли вы её на ноутбуке или CI‑сервере.

## Шаг 3: Настройте параметры конвертации изображения – задайте разрешение

Теперь, когда sandbox готов, мы указываем конвертеру, какое **разрешение изображения** нам нужно. Класс `ImageConversionOptions` позволяет задать DPI выходного PNG независимо от DPI sandbox, давая вам два рычага управления.

```java
// Step 3.1: Prepare conversion options
ImageConversionOptions conversionOptions = new ImageConversionOptions();

// Step 3.2: Desired output DPI – this directly influences PNG quality
conversionOptions.setResolution(300); // 300 dpi is print‑quality; increase for sharper prints

// Step 3.3: Bind the sandbox to the options so the layout engine respects our virtual screen
conversionOptions.setSandbox(sandbox);
```

**Подсказка:** Если нужен PNG с 600 dpi для высококачественных брошюр, просто замените `setResolution(300)` на `setResolution(600)`. Учтите, что большие значения DPI увеличивают потребление памяти и время обработки, поэтому сначала протестируйте на небольшой странице.

## Шаг 4: Конвертируйте HTML‑страницу в PNG

С готовыми sandbox и параметрами шаг **convert html to png** сводится к одной строке:

```java
// Step 4: Perform the conversion
Converter.convert(
        "C:/temp/page.html",   // Source HTML file (convert html page)
        "C:/temp/page.png",    // Destination PNG file
        conversionOptions);    // Options that include DPI and sandbox
```

Если всё прошло успешно, вы увидите сообщение в консоли на следующем этапе.

## Шаг 5: Проверьте результат и выведите подтверждение

Быстрый `System.out.println` сообщает, что работа завершена. В реальном проекте вы, возможно, захотите проверить размер файла, размеры изображения или даже программно открыть PNG для проверки DPI.

```java
System.out.println("PNG generated with sandboxed layout at 300 dpi.");
```

Запуск класса создаст `page.png` в той же папке, где находится ваш HTML‑файл. Откройте его в просмотрщике изображений, который показывает DPI (например, Windows Photo Viewer → Properties → Details) и убедитесь, что указано **300 dpi**.

## Полный рабочий пример

Собрав всё вместе, получаем автономный Java‑класс, который можно скопировать‑вставить в вашу IDE:

```java
import com.aspose.html.conversions.Converter;
import com.aspose.html.conversions.options.ImageConversionOptions;
import com.aspose.html.sandbox.Sandbox;

public class HtmlToPngWithSandbox {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox that simulates a 1024×768 screen with 96 dpi.
        Sandbox sandbox = new Sandbox();
        sandbox.setScreenWidth(1024);
        sandbox.setScreenHeight(768);
        sandbox.setDpi(96); // <-- This is where you learn how to set dpi

        // Step 2: Configure image conversion options – 300 dpi PNG using the sandbox.
        ImageConversionOptions conversionOptions = new ImageConversionOptions();
        conversionOptions.setResolution(300); // Set image resolution (dpi)
        conversionOptions.setSandbox(sandbox);

        // Step 3: Convert the HTML page to a PNG image using the defined options.
        Converter.convert(
                "C:/temp/page.html",   // convert html page
                "C:/temp/page.png",    // output PNG
                conversionOptions);    // includes dpi and resolution settings

        // Step 4: Indicate that the conversion has completed.
        System.out.println("PNG generated with sandboxed layout at 300 dpi.");
    }
}
```

> **Помните:** Строка `sandbox.setDpi(96);` — это часть *как установить dpi*. Отрегулируйте её под нужную плотность экрана; `conversionOptions.setResolution(300);` управляет конечным DPI изображения.

## Обработка типичных проблем

| Ситуация | На что обратить внимание | Предлагаемое решение |
|-----------|--------------------------|----------------------|
| **Out‑of‑Memory errors** при использовании 600 dpi | Высокий DPI резко увеличивает размер растра (например, 1024 × 768 @ 600 dpi ≈ 4 МП). | Уменьшите размеры экрана или выполните конвертацию потоково, используя обратные вызовы `ConversionProgress`. |
| **HTML использует внешние CSS/JS, которые не загружаются** | Sandbox работает в изоляции; удалённые ресурсы должны быть доступны. | Указывайте абсолютные URL‑ы или внедряйте CSS напрямую в HTML. |
| **Неправильный DPI в результате** | Вы изменили `sandbox.setDpi`, но забыли скорректировать `conversionOptions.setResolution`. | Убедитесь, что оба значения согласованы с целевым выводом. |
| **FileNotFoundException** | Ошибка в пути или отсутствие прав доступа к файлу. | Используйте `Paths.get(...).toAbsolutePath()` и проверьте права чтения/записи. |

## Расширенные варианты

### 1. Другие форматы вывода

Aspose.HTML не ограничивается PNG. Поменяйте расширение файла и используйте соответствующий класс параметров, например `JpegConversionOptions` для JPEG. Логика DPI остаётся той же.

```java
import com.aspose.html.conversions.options.JpegConversionOptions;

// ...

JpegConversionOptions jpegOpts = new JpegConversionOptions();
jpegOpts.setResolution(300);
jpegOpts.setSandbox(sandbox);

Converter.convert("page.html", "page.jpg", jpegOpts);
```

### 2. Динамическое определение размеров экрана

Если нужно, чтобы sandbox имитировал мобильное устройство, считайте размеры из конфигурационного файла:

```java
sandbox.setScreenWidth(Integer.parseInt(System.getProperty("screen.width", "375")));
sandbox.setScreenHeight(Integer.parseInt(System.getProperty("screen.height", "667")));
sandbox.setDpi(Integer.parseInt(System.getProperty("screen.dpi", "96")));
```

Запустите с параметрами `-Dscreen.width=375 -Dscreen.height=667 -Dscreen.dpi=326`, чтобы эмулировать дисплей iPhone Retina.

### 3. Пакетная конвертация

Обёрните вызов конвертации в цикл, проходящий по каталогу HTML‑файлов. Не забудьте переиспользовать один и тот же объект `Sandbox` и `ImageConversionOptions`, чтобы избежать лишних выделений памяти.

```java
Files.list(Paths.get("C:/temp/html"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(htmlPath -> {
         String pngPath = htmlPath.toString().replace(".html", ".png");
         Converter.convert(htmlPath.toString(), pngPath, conversionOptions);
     });
```

## Ожидаемый результат

Запуск класса с настройками по умолчанию выдаёт PNG‑файл приблизительно **1024 × 768 пикселей** при **300 dpi**. В большинстве графических редакторов размеры будут отображаться как 1024 × 768, а метаданные DPI покажут 300. Если распечатать изображение шириной 1 дюйм, вы получите чёткую линию в 300 пикселей — идеально для высококачественных листовок.

## Визуальное резюме

![how to set dpi in Aspose HTML conversion](/images/aspose-dpi-example.png "how to set dpi – Aspose HTML sandbox example")

*Скриншот показывает метаданные DPI сгенерированного PNG (300 dpi).*

## Заключение

Мы рассмотрели **как установить DPI** при **конвертации HTML в PNG** с помощью **Aspose HTML Converter** на Java. Создав sandbox, настроив `ImageConversionOptions` и вызвав `Converter.convert`, вы получаете пиксельный контроль над симуляцией экрана и конечным разрешением изображения. Будь то печатные счета, высококачественные веб‑ресурсы или автоматические миниатюры, тот же шаблон применим — просто подберите нужные DPI и размеры экрана под ваш случай.

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как использовать Aspose для рендеринга HTML в PNG – пошаговое руководство](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Как конвертировать HTML в JPEG с помощью Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)
- [Как конвертировать HTML в BMP с помощью Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-bmp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}