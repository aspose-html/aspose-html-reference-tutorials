---
category: general
date: 2026-03-07
description: Отображение HTML Java в PNG путём преобразования длинной HTML‑страницы
  в изображение. Узнайте, как конвертировать HTML в изображение, выводить PNG из HTML
  и создавать изображение из длинного HTML с помощью Aspose.
draft: false
keywords:
- render html java
- convert html to image
- output png from html
- create image from long html
language: ru
og_description: Рендеринг HTML Java в файл PNG. Это руководство показывает, как преобразовать
  HTML в изображение, вывести PNG из HTML и создать изображение из длинного HTML с
  помощью Aspose.
og_title: Рендер HTML в Java – Преобразовать длинную страницу в PNG
tags:
- Java
- Aspose.HTML
- Image Rendering
title: 'Отрисовка HTML в Java: Преобразование длинной страницы в PNG'
url: /ru/java/conversion-html-to-various-image-formats/render-html-java-convert-long-page-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Render HTML Java – Convert Long Page to PNG

Когда‑то вам нужно **render HTML Java** и получить чёткий PNG‑файл, но страница, с которой вы работаете, тянется бесконечно? Это частая проблема, когда у вас есть длинный отчёт, список счетов или прокручиваемый блог‑пост, который нужно заскриншотить для письма или архива.  

Хорошая новость? Вы можете **convert HTML to image** всего в несколько строк кода Java, благодаря движку рендеринга Aspose.HTML. В этом руководстве мы пройдёмся по процессу превращения объёмного HTML‑документа в одностраничный PNG, объясним, почему важны каждое из настроек, и покажем, как адаптировать процесс под другие форматы вывода.

К концу этого руководства вы сможете **output PNG from HTML**, разбить многокилобайтную страницу на удобные куски‑изображения и даже использовать тот же подход для **create image from long HTML** для PDF, JPEG или BMP.

## What You’ll Need

- **Java Development Kit (JDK) 8 or newer** – код работает на любой современной JDK.  
- **Aspose.HTML for Java** library (version 23.10 or later). Вы можете получить её из Maven Central или с сайта Aspose.  
- **long HTML file** который нужно отрендерить (в примере используется `longpage.html`).  
- IDE или текстовый редактор (IntelliJ IDEA, Eclipse, VS Code… выбирайте сами).

Никаких внешних сервисов, никаких нативных бинарных файлов – всё происходит в чистой Java.

## Step 1: Set Up the Project and Add Aspose.HTML

Сначала создайте новый Maven (или Gradle) проект. Если вы используете Maven, добавьте зависимость Aspose.HTML в ваш `pom.xml`:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

> **Pro tip:** Aspose предлагает бесплатную 30‑дневную trial‑лицензию. Поместите файл `aspose.html.lic` в ваш classpath, чтобы избавиться от водяного знака оценки.

## Step 2: Load the Source HTML Document

Теперь загрузим HTML, который нужно конвертировать. Класс `HTMLDocument` принимает URI, поэтому мы превратим локальный путь в file‑URI с помощью `java.nio.file.Paths`.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// ...

// Load the HTML file from disk
HTMLDocument htmlDoc = new HTMLDocument(
        Paths.get("YOUR_DIRECTORY/longpage.html")
             .toUri()
             .toString()
);
```

Почему **URI**? Aspose.HTML может разрешать относительные ресурсы (CSS, изображения, шрифты) на основе местоположения документа, гарантируя, что полученное изображение будет выглядеть точно так же, как в браузере.

## Step 3: Define Conversion Options for a Single Slice

«Длинная» страница часто превышает размер рендеринга по умолчанию. Вместо того чтобы рендерить всю прокручиваемую высоту (которая может достигать десятков тысяч пикселей), мы попросим рендерер создать **page slice** — своего рода виртуальную страницу в PDF.  

Ключевые свойства:

- `setPageWidth(int)`: ширина выходного изображения в пикселях.  
- `setPageHeight(int)`: высота того куска, который вам нужен.  
- `setPageNumber(int)`: какой кусок рендерить (нумерация с 1).

```java
import com.aspose.html.rendering.ImageConversionOptions;

// ...

ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setPageWidth(1024);   // Desired PNG width
conversionOptions.setPageHeight(1000); // Height of one slice
conversionOptions.setPageNumber(2);    // Render the second slice (1‑based)
```

> **Why slice?** Рендеринг всего документа может потребовать гигабайты ОЗУ и создать неудобное в работе изображение. Делая срезы, вы экономите память и при необходимости можете собрать их вместе, получив полностраничный вид.

## Step 4: Render the Slice to PNG

С документом и параметрами, `Renderer` берёт на себя тяжёлую работу. Обернём его в блок `try‑with‑resources`, чтобы нативные ресурсы освобождались автоматически.

```java
import com.aspose.html.rendering.Renderer;
import java.nio.file.Paths;

// ...

try (Renderer renderer = new Renderer()) {
    renderer.render(
            htmlDoc,
            Paths.get("YOUR_DIRECTORY/page2.png"),
            conversionOptions
    );
}
System.out.println("Second slice rendered to page2.png");
```

Если всё прошло без ошибок, вы найдёте `page2.png` в целевой папке. Откройте его любой программой‑просмотрщиком — вы должны увидеть точный фрагмент оригинального HTML, соответствующий второму куску высотой 1000 пикселей.

## Step 5: Verify the Output and Optional Tweaks

Быстрая проверка поможет обнаружить недостающие ресурсы или проблемы с разметкой на раннем этапе.

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

// ...

BufferedImage img = ImageIO.read(new File("YOUR_DIRECTORY/page2.png"));
System.out.println("Image dimensions: " + img.getWidth() + "x" + img.getHeight());
```

Если размеры не совпадают с теми, что вы задали в `PageWidth`/`PageHeight`, проверьте настройки DPI или правила CSS `@media print`, которые могут переопределять размер.

### Common Adjustments

| Goal | Setting to tweak |
|------|------------------|
| **Higher resolution** | `conversionOptions.setResolution(300);` (DPI) |
| **Transparent background** | `conversionOptions.setBackgroundColor(Color.TRANSPARENT);` |
| **Render the whole page** | Omit `setPageHeight`/`setPageNumber` – the renderer will output the full scroll height as one massive PNG. |
| **Create JPEG instead of PNG** | Change the output file extension to `.jpg`; the renderer picks the format from the file name. |

## Full, Runnable Example

Ниже полная реализация класса, которую можно скопировать в файл `PartialImageRender.java`. Замените `YOUR_DIRECTORY` на реальный путь к папке, содержащей `longpage.html`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.*;
import java.nio.file.Paths;

/**
 * Demonstrates how to render a specific slice of a long HTML page to PNG.
 * This example uses Aspose.HTML for Java and works with JDK 8+.
 */
public class PartialImageRender {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument(
                Paths.get("YOUR_DIRECTORY/longpage.html")
                     .toUri()
                     .toString());

        // Step 2: Define conversion options to render only a specific page slice
        ImageConversionOptions conversionOptions = new ImageConversionOptions();
        conversionOptions.setPageWidth(1024);   // width of the output image
        conversionOptions.setPageHeight(1000); // height of a single page slice
        conversionOptions.setPageNumber(2);    // render the second slice (1‑based)

        // Optional: increase DPI for sharper output
        // conversionOptions.setResolution(300);

        // Step 3: Render the selected page slice to a PNG file
        try (Renderer renderer = new Renderer()) {
            renderer.render(htmlDoc,
                    Paths.get("YOUR_DIRECTORY/page2.png"),
                    conversionOptions);
        }

        // Step 4: Confirm that the image has been created
        System.out.println("Second slice rendered to page2.png");
    }
}
```

Сохраните, скомпилируйте и запустите:

```bash
javac -cp "path/to/aspose-html.jar" PartialImageRender.java
java -cp ".:path/to/aspose-html.jar" PartialImageRender
```

В консоли появится сообщение, подтверждающее создание PNG‑файла.

## Frequently Asked Questions

**Q: Does this work with HTML that contains external CSS or JavaScript?**  
A: Yes. As long as the external resources are reachable via absolute URLs or relative to the HTML file’s folder, Aspose.HTML will fetch them during rendering. For offline scenarios, bundle the CSS/JS next to the HTML file.

**Q: What if the HTML uses web fonts?**  
A: Aspose.HTML supports `@font-face`. Ensure the font files are either embedded as base64 or placed in a location the renderer can access.

**Q: Can I render to PDF instead of PNG?**  
A: Absolutely. Swap `ImageConversionOptions` for `PdfConversionOptions` and change the output file extension to `.pdf`. The same slicing logic applies.

**Q: My page is wider than 1024 px – will it be truncated?**  
A: The renderer scales the content to fit the specified width, preserving aspect ratio. If you need the full width, increase `setPageWidth`.

## Wrap‑Up

We’ve just **rendered HTML Java** to a PNG image, sliced a long page into a manageable chunk, and covered the most common tweaks you might need. Whether you’re generating thumbnails for a CMS

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}