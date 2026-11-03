---
category: general
date: 2026-03-04
description: Узнайте, как установить DPI при конвертации HTML в PNG. В этом руководстве
  также рассматриваются экспорт HTML в PNG, сохранение HTML как PNG и создание PNG
  из HTML с помощью Aspose.HTML для Java.
draft: false
keywords:
- how to set dpi
- convert html to png
- export html as png
- save html as png
- generate png from html
language: ru
og_description: 'Как установить DPI при конвертации HTML в PNG: объяснение. Следуйте
  пошаговому руководству, чтобы экспортировать HTML в PNG, сохранить HTML как PNG
  и создать PNG из HTML.'
og_title: Как установить DPI при конвертации HTML в PNG
tags:
- Aspose.HTML
- Java
- Image Conversion
title: Как установить DPI при конвертации HTML в PNG
url: /ru/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как установить DPI при конвертации HTML в PNG

Вы когда‑нибудь задумывались **как установить DPI** для растрового изображения, которое вы генерируете из веб‑страницы? Возможно, вы создаёте инструмент отчётности, сервис миниатюр или конвейер готовых к печати ресурсов — любой из этих сценариев обычно начинается с HTML‑документа, который нужно превратить в PNG высокого разрешения.  

Хорошая новость в том, что Aspose.HTML for Java делает процесс **конвертации HTML в PNG** простым как раз, и вы можете управлять DPI всего одной строкой кода. В этом руководстве мы пройдём весь процесс, от загрузки вашего HTML‑файла до экспорта его в PNG с разрешением 300 DPI, а также коснёмся связанных задач, таких как **export HTML as PNG**, **save HTML as PNG** и **generate PNG from HTML**.

## Что вы узнаете

- Как настроить DPI (dots per inch) для выходного изображения.
- Разницу между DPI, разрешением и качеством сжатия.
- Полный, готовый к запуску пример на Java, который можно скопировать и вставить.
- Распространённые подводные камни (например, отсутствие шрифтов, большие страницы) и как их избежать.
- Быстрые советы по настройке вывода, когда нужно **convert HTML to PNG** в разных средах.

### Предварительные требования

- Java 8 или новее, установленный на вашем компьютере.
- Библиотека Aspose.HTML for Java (последняя версия на март 2026). Вы можете получить её из Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

- Простой файл `input.html`, который вы хотите превратить в PNG‑изображение.

---

## Как установить DPI при конвертации HTML в PNG

![Diagram showing DPI setting in code – how to set dpi when converting HTML to PNG](https://example.com/images/dpi-setting.png)

**Первый шаг**, который контролирует чёткость изображения, — это свойство `Resolution` класса `ImageSaveOptions`. Ниже мы разберём процесс на небольшие шаги.

### Шаг 1: Определите пути ввода и вывода (convert html to png)

Сначала укажите конвертеру, где находится ваш исходный HTML и куда следует записать PNG.

```java
// Step 1 – file locations
String htmlFilePath = "YOUR_DIRECTORY/input.html";
String pngFilePath  = "YOUR_DIRECTORY/output.png";
```

> **Почему это важно:** Жёстко задавать пути приемлемо для демонстрации, но в продакшене вы, скорее всего, будете получать их из конфигурации или аргументов командной строки. Это делает код гибким для любого рабочего процесса **save HTML as PNG**.

### Шаг 2: Создайте ImageSaveOptions и установите DPI (how to set dpi)

Теперь мы создаём экземпляр `ImageSaveOptions` для PNG и задаём DPI равным 300. DPI определяет, сколько пикселей помещается в один дюйм при печати изображения или отображении его в естественном размере.

```java
// Step 2 – configure PNG options
ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
saveOptions.setResolution(300);   // <-- This is the DPI you asked for
saveOptions.setQuality(95);       // PNG compression (0‑100); higher = larger file, better fidelity
```

> **Объяснение:**  
> - `setResolution(300)` указывает Aspose.HTML отрисовать страницу с 300 точками на дюйм.  
> - `setQuality(95)` необязательно для PNG; оно контролирует уровень сжатия ZLIB. Вы можете уменьшить его для получения меньших файлов, если вам не нужен каждый пиксель в идеальном виде.

### Шаг 3: Выполните конвертацию (export html as png)

With the options ready, the actual conversion is a one‑liner.

```java
// Step 3 – run the conversion
Converter.convert(htmlFilePath, pngFilePath, saveOptions);
```

> **Что происходит за кулисами?** Aspose.HTML парсит HTML, применяет CSS, формирует DOM, растеризует макет с запрошенным DPI и, наконец, записывает PNG‑файл. Если вам нужно **generate PNG from HTML** в веб‑службе, вы можете заменить пути к файлам потоками.

## Полный рабочий пример

Объединив всё вместе, представляем полный Java‑класс, который вы можете скомпилировать и запустить.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.*;
import com.aspose.html.saving.*;

public class ConvertHtmlToPngWithDpi {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the input HTML file and the output PNG file
        String htmlFilePath = "YOUR_DIRECTORY/input.html";
        String pngFilePath  = "YOUR_DIRECTORY/output.png";

        // Step 2: Create image save options for PNG and configure high‑resolution output
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        saveOptions.setResolution(300);   // Set resolution to 300 DPI (how to set dpi)
        saveOptions.setQuality(95);       // PNG compression quality (0‑100)

        // Step 3: Perform the conversion from HTML to PNG using the configured options
        Converter.convert(htmlFilePath, pngFilePath, saveOptions);

        System.out.println("Conversion complete! PNG saved at " + pngFilePath);
    }
}
```

Запустите программу, и вы найдете чёткий PNG с 300 DPI в указанном месте. Откройте его в любом просмотрщике изображений и проверьте свойства изображения — DPI должно показывать **300**.

---

## Часто задаваемые вопросы и крайние случаи

### Что делать, если настройка DPI, кажется, игнорируется?

- **Убедитесь, что вы используете актуальную версию Aspose.HTML.** Старые версии игнорировали `Resolution` для PNG.
- **Проверьте размер исходного HTML.** Маленькая HTML‑страница, отрисованная с 300 DPI, всё равно может дать небольшие пиксельные размеры. DPI влияет только на коэффициент масштабирования, а не на собственный размер страницы.

### Чем DPI отличается от размеров изображения?

DPI — это *физическая* величина (точек на дюйм). Фактическая ширина/высота в пикселях вычисляется как:

```
pixel width  = CSS width  * DPI / 96
pixel height = CSS height * DPI / 96
```

Если ширина тела вашего HTML составляет 800 px, при 300 DPI выходной PNG будет примерно 2500 px в ширину (800 × 300 ÷ 96).

### Могу ли я использовать другие форматы (JPEG, BMP), одновременно контролируя DPI?

Конечно. Просто замените `SaveFormat.PNG` на `SaveFormat.JPEG` (или `BMP`) и оставьте `setResolution`. Помните, что JPEG также учитывает параметр `Quality`, который соответствует уровню сжатия.

### Что делать с шрифтами, которые не установлены на сервере?

Aspose.HTML переключится на шрифт по умолчанию, что может изменить макет. Чтобы гарантировать идентичный рендеринг, внедрите необходимые шрифты с помощью `FontSettings`:

```java
FontSettings fontSettings = new FontSettings();
fontSettings.setFontFolder("YOUR_FONT_DIRECTORY", true);
saveOptions.setFontSettings(fontSettings);
```

### Генерация нескольких PNG в пакетном режиме

Если вам нужно **generate PNG from HTML** для множества файлов, оберните логику конвертации в цикл и переиспользуйте один экземпляр `ImageSaveOptions`. Это уменьшит нагрузку на память и ускорит обработку.

```java
for (Path htmlPath : Files.newDirectoryStream(Paths.get("batch_html"))) {
    String outPath = htmlPath.toString().replace(".html", ".png");
    Converter.convert(htmlPath.toString(), outPath, saveOptions);
}
```

---

## Профессиональные советы для экспорта PNG высокого качества

1. **Используйте CSS, дружелюбный к векторам** (например, `transform: scale(1)`), чтобы избежать артефактов сглаживания при высоком DPI.  
2. **Установите цвет фона**, если ваш HTML содержит прозрачные элементы и вам нужен сплошной холст:

   ```java
   saveOptions.setBackgroundColor(Color.WHITE);
   ```

3. **Избегайте встроенных base64‑изображений** размером более нескольких МБ — они могут увеличить потребление памяти во время конвертации.  
4. **Тестируйте на экранах с разными DPI** (например, мониторы 72 DPI против принтеров 300 DPI), чтобы убедиться, что визуальное качество соответствует ожиданиям.  
5. **Используйте `setPageSize()`**, если хотите, чтобы PNG соответствовал конкретному размеру печати (A4, Letter и т.д.), независимо от исходных размеров HTML.

---

## Заключение

Мы рассмотрели **как установить DPI** при **конвертации HTML в PNG** с помощью Aspose.HTML for Java, продемонстрировали полный готовый к запуску пример и изучили связанные задачи, такие как **export HTML as PNG**, **save HTML as PNG** и **generate PNG from HTML**. Настраивая `ImageSaveOptions.setResolution`, вы контролируете физическую чёткость вывода, а `setQuality` позволяет балансировать размер файла и визуальное качество.

Что дальше? Попробуйте заменить формат PNG на JPEG, чтобы увидеть, как сжатие взаимодействует с DPI, или поэкспериментируйте с пакетной обработкой для **convert HTML to PNG** в масштабе. Вы также можете исследовать добавление водяных знаков или пользовательских метаданных — оба поддерживаются богатым API Aspose.HTML.

Есть сложный сценарий, который не был рассмотрен? Оставьте комментарий, и мы разберёмся вместе. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}