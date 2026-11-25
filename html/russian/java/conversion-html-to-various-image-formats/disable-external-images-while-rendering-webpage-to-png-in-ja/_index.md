---
category: general
date: 2026-05-31
description: Отключите внешние изображения при рендеринге веб‑страницы в PNG на Java
  с использованием Aspose HTML. Узнайте, как безопасно загрузить веб‑страницу в песочнице
  и сохранить HTML‑документ в PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: ru
og_description: Отключите внешние изображения при рендеринге веб‑страницы в PNG на
  Java. Это пошаговое руководство показывает, как загрузить веб‑страницу в песочнице
  и сохранить HTML‑документ в формате PNG.
og_title: Отключить внешние изображения при рендеринге веб‑страницы в PNG на Java
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Отключить внешние изображения при рендеринге веб‑страницы в PNG на Java
url: /ru/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Отключение внешних изображений при рендеринге веб‑страницы в PNG на Java

Когда‑нибудь нужно было **отключить внешние изображения** при рендеринге веб‑страницы в PNG на Java? Возможно, вы создаёте сервис миниатюр, который должен быть изолирован от публичного интернета, или просто хотите гарантировать, что ни одно стороннее изображение не утечёт во время конвертации. В любом случае, вы попали в нужное место.

В этом руководстве мы пройдёмся по загрузке веб‑страницы в «песочнице», отключим загрузку внешних изображений и, наконец, сохраним HTML‑документ как PNG‑файл — все это с помощью Aspose.HTML for Java. К концу вы получите готовый к запуску пример и несколько практических советов, как избежать типичных подводных камней.

## Что вы узнаете

- **Как рендерить HTML в изображение Java** с помощью `Converter` из Aspose.HTML.  
- Точные шаги **загрузки веб‑страницы в песочнице** с пользовательским viewport и DPI.  
- Конфигурацию, необходимую для **отключения внешних изображений** при сохранении страницы.  
- Как **сохранить HTML‑документ как PNG** (или любой другой поддерживаемый формат) на диск.  
- Обработку граничных случаев, подсказки по производительности и рекомендации по отладке.

### Предварительные требования

- Установлен Java 8 или новее (код также работает с JDK 11+).  
- Maven или Gradle для получения библиотеки Aspose.HTML for Java.  
- Базовое знакомство с синтаксисом Java и обработкой исключений.  
- Интернет‑соединение для первоначальной загрузки страницы (если только вы не обслуживаете HTML локально).

> **Полезный совет:** Если вы работаете за корпоративным прокси, задайте свойства JVM `http.proxyHost` и `http.proxyPort` перед запуском примера.

---

## Шаг 1: Настройте проект и добавьте Aspose.HTML

Первым делом — добавьте зависимость Aspose.HTML. Если вы используете Maven, поместите следующее в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Для Gradle эквивалент выглядит так:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

После того как библиотека появится в classpath, можно приступать к кодированию.

---

## Шаг 2: **Отключить внешние изображения** с помощью среды «песочницы»

Суть решения заключается в `DocumentSandbox`. Передавая `false` в параметр *allowExternalImages*, мы инструктируем Aspose.HTML игнорировать любые теги `<img>`, указывающие на URL‑адреса за пределами песочницы. Это именно тот механизм, который **отключает внешние изображения**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Почему это важно:** Без песочницы рендерер попытался бы скачать каждое изображение, указанное на странице, что может быть медленно, ненадёжно или даже представлять угрозу безопасности. Установка флага в `false` гарантирует чистый, автономный проход рендеринга.

---

## Шаг 3: **Загрузить веб‑страницу в песочнице**  

Теперь указываем Aspose.HTML URL, который нужно захватить. Конструктор `HTMLDocument` принимает экземпляр песочницы, автоматически применяя только что заданные ограничения.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Если страница сильно зависит от внешних скриптов для построения макета, вы можете заметить отсутствие контента, потому что мы также отключили скрипты. В этом случае переключите флаг `allowExternalScripts` в `true`, оставив `allowExternalImages` равным `false`.

---

## Шаг 4: **Рендерить веб‑страницу в PNG**  

После загрузки документа преобразовать его в изображение можно одной строкой с помощью `Converter.convert`. Объект `ImageSaveOptions` позволяет выбрать формат вывода; здесь мы выбираем PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

Полученный файл `sandboxed.png` содержит снимок страницы **без каких‑либо внешних изображений** — остаются только встроенные SVG или графика в формате base64, если они есть.

---

## Шаг 5: Проверка результата и отладка типовых проблем

После запуска программы откройте `sandboxed.png` в любом просмотрщике изображений. Вы должны увидеть макет страницы, текст и стили CSS, но все элементы `<img src="http://…">` будут пустыми (обычно отображаются как белый прямоугольник или полностью опускаются).

### Типичные затруднения и способы их устранения

| Симптом | Вероятная причина | Решение |
|---|---|---|
| Пустая страница | Целевой URL блокирует запрос (например, Cloudflare) | Добавьте необходимые заголовки в user‑agent песочницы или используйте прокси. |
| Отсутствуют шрифты | Файлы шрифтов размещены внешне | Установите шрифты локально или внедрите их через `@font-face` с data URI. |
| Сдвиг макета | CSS‑файлы загружаются извне и были заблокированы | Установите `allowExternalScripts` в `true` *только* для загрузки CSS, затем перезапустите. |
| `java.lang.OutOfMemoryError` | Рендеринг очень большой страницы при высоком DPI | Уменьшите размер viewport или DPI, либо увеличьте размер кучи JVM (`-Xmx2g`). |

---

## Шаг 6: Расширение примера — сохранение в другие форматы

Тот же код работает для JPEG, BMP или даже PDF. Достаточно изменить значение перечисления `SaveFormat`:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

Если нужен PDF, замените `ImageSaveOptions` на `PdfSaveOptions` и скорректируйте расширение файла соответственно.

---

## Полный рабочий пример (готов к копированию)

Ниже представлен **полный, готовый к запуску** код. Создайте новый Java‑класс, вставьте код, убедитесь, что каталог `output` существует, и запустите программу.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Ожидаемый вывод** (консоль):

```
PNG image saved to: output/sandboxed.png
```

Откройте `sandboxed.png` — вы увидите страницу, отрендеренную **без внешних изображений**.

---

## Часто задаваемые вопросы

**В: Могу ли я всё ещё отображать изображения, встроенные в HTML?**  
О: Да. Встроенные `data:` URI или изображения в формате base64 считаются частью документа и появятся в PNG.

**В: Что если нужно оставить некоторые внешние изображения, а остальные заблокировать?**  
О: Песочница работает как переключатель «всё или ничего». Для более тонкой настройки скачайте разрешённые изображения самостоятельно, внедрите их как data URI, а затем выполните рендеринг.

**В: Работает ли такой подход на безголовых серверах?**  
О: Абсолютно. Aspose.HTML — чисто Java‑библиотека; ей не нужен дисплейный сервер или браузерный движок.

**В: Чем это отличается от Selenium или Puppeteer?**  
О: Selenium управляет реальным браузером, что тяжеловесно и сложнее «запесочить». Aspose.HTML рендерит HTML непосредственно в памяти, обеспечивая детерминированную производительность и более простые средства контроля безопасности, такие как **disable external images**.

---

## Заключение

Теперь у вас есть надёжный сквозной рецепт **отключения внешних изображений при рендеринге веб‑страницы в PNG на Java**. Используя `DocumentSandbox`, вы получаете строгий контроль над тем, какие внешние ресурсы разрешены, обеспечивая как безопасность, так и воспроизводимость. Далее вы можете экспериментировать с различными размерами viewport, настройками DPI или форматами вывода — каждая настройка открывает новые возможности для создания миниатюр, превью или архивных снимков.

Готовы к следующему вызову? Попробуйте рендерить пакет URL‑ов параллельно или интегрировать эту логику в микросервис Spring Boot, который будет возвращать PNG‑файлы по запросу. Возможности безграничны, когда совмещаете гибкость Aspose.HTML с инструментами параллелизма Java.

Счастливого кодинга и не забудьте поделиться своими историями успеха в комментариях!

## Что изучать дальше?

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [How to Render HTML to PNG with Aspose – Complete Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}