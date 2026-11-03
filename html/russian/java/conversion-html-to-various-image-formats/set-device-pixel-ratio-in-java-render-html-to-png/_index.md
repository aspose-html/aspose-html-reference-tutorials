---
category: general
date: 2026-03-14
description: Узнайте, как установить коэффициент пикселей устройства в Java и сохранить
  веб‑страницу в формате PNG с помощью Aspose.HTML — полное руководство по конвертации
  HTML в PNG.
draft: false
keywords:
- set device pixel ratio
- save webpage as png
- how to render png
- html to png conversion
- java html to image
language: ru
og_description: Узнайте, как установить коэффициент пикселей устройства в Java и сохранить
  веб-страницу в формате PNG с помощью Aspose.HTML, пошагово рассматривая процесс
  преобразования HTML в PNG.
og_title: Установить коэффициент пикселей устройства в Java – Рендеринг HTML в PNG
tags:
- java
- aspose-html
- image-rendering
title: Установить коэффициент пикселей устройства в Java – рендеринг HTML в PNG
url: /ru/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-render-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set device pixel ratio in Java – Render HTML to PNG

Когда‑нибудь нужно **установить device pixel ratio** при создании скриншота веб‑страницы в Java? Возможно, вы разрабатываете сервис предварительного просмотра для мобильных устройств, или просто хотите получить чёткую миниатюру, правильно отображающуюся на Retina‑экране. В любом случае вы попали по адресу. В этом руководстве мы пройдем весь процесс **html to png conversion**, и вы увидите, как **save webpage as png** с помощью библиотеки Aspose.HTML.

Мы рассмотрим всё: от настройки «песочницы», имитирующей viewport iPhone, до загрузки удалённой HTML‑страницы и записи результата на диск. К концу вы узнаете, **how to render png** программно, и получите переиспользуемый фрагмент кода, который можно вставить в любой Java‑проект, требующий **java html to image** возможностей.

## What You’ll Need

Прежде чем погрузиться в код, убедитесь, что у вас есть следующее:

- **Java Development Kit (JDK) 8 или новее** – библиотека работает с любой современной JDK.
- **Aspose.HTML for Java** – последнюю JAR‑ку можно взять из репозитория Aspose Maven или скачать zip‑файл с официального сайта.
- **IDE** (IntelliJ IDEA, Eclipse или даже VS Code) – любой инструмент, позволяющий компилировать и запускать Java.
- Интернет‑соединение, если планируете загружать живой URL (в примере используется `https://example.com/mobile.html`).

Это всё. Никаких дополнительных средств сборки или нативных бинарных файлов не требуется.

## Step 1: Configure the Sandbox and set device pixel ratio

Первое, что нужно сделать — создать **Sandbox**, имитирующую мобильное устройство. Здесь вы действительно **set device pixel ratio**, чтобы соответствовать экрану с высокой плотностью пикселей (например, 2× Retina‑дисплей iPhone).

```java
import com.aspose.html.rendering.SandboxOptions;

// Create sandbox options
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixel width of iPhone 6/7/8
sandboxOptions.setScreenHeight(667);         // CSS pixel height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
sandboxOptions.setUserAgent(
    "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
    "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

// Build the sandbox
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

**Почему это важно:** `devicePixelRatio` сообщает движку рендеринга, сколько физических пикселей соответствует одному CSS‑пикселю. Без его установки полученное изображение будет размытым на экранах с высоким DPI. Явно задав значение, вы гарантируете, что сгенерированный PNG будет содержать нужный уровень детализации.

> **Pro tip:** Если вы нацелены на Android‑устройства, можно использовать `3.0` для устройств с 3× масштабированием. Соответственно скорректируйте ширину/высоту.

## Step 2: Load the HTML page for html to png conversion

Теперь, когда песочница готова, можно загрузить страницу, которую нужно захватить. Класс Aspose.HTML `HTMLDocument` принимает URL и экземпляр sandbox, поэтому страница рендерится точно так же, как на имитируемом устройстве.

```java
import com.aspose.html.HTMLDocument;

// Load the remote page inside the sandbox
HTMLDocument document = new HTMLDocument(
    "https://example.com/mobile.html", // Replace with your own URL
    mobileSandbox);
```

**Что происходит под капотом?** Библиотека получает HTML, парсит CSS, исполняет JavaScript (если включён), и раскладывает страницу, используя заданные ранее размеры viewport. Этот шаг — ядро **java html to image** конвертации, потому что он даёт полностью отрендеренный DOM, готовый к растеризации.

> **Edge case:** Если страница использует внешние шрифты, убедитесь, что они доступны машине, где выполняется код. Иначе текст может переключиться на шрифт по умолчанию, изменив визуальный результат.

## Step 3: Save webpage as PNG – how to render png with Aspose.HTML

После рендеринга документа остаётся лишь записать PNG‑файл на диск. Класс `PngSaveOptions` позволяет настроить уровень сжатия и другие PNG‑специфичные параметры, но значения по умолчанию подходят для большинства сценариев.

```java
import com.aspose.html.saving.PngSaveOptions;

// Define PNG options (optional)
PngSaveOptions pngOptions = new PngSaveOptions();
// You could adjust pngOptions.setCompressionLevel(9); for maximum compression

// Save the rendered page as a PNG image
document.save("output/mobile_view.png", pngOptions);

System.out.println("Mobile view rendered and saved as PNG.");
```

Запустив программу, вы получите `mobile_view.png` в папке `output`. Откройте его — вы увидите точный снимок удалённой страницы, отрендеренный в высокой плотности, которую вы задали через **set device pixel ratio**.

### Quick verification

```text
$ java -jar MobileRenderTutorial.jar
Mobile view rendered and saved as PNG.
$ ls output
mobile_view.png
```

Откройте изображение в любом просмотрщике; текст должен быть чётким, иконки — резкими, а макет — идентичным тому, что виден на реальном iPhone.

## Optional: Adjusting the Rendering Pipeline

### Changing the DPI dynamically

Если нужно генерировать изображения для разных плотностей экранов, оберните создание sandbox в метод:

```java
private static Sandbox createSandbox(double dpr) {
    SandboxOptions opts = new SandboxOptions();
    opts.setScreenWidth(375);
    opts.setScreenHeight(667);
    opts.setDevicePixelRatio(dpr); // Pass 1.0, 2.0, 3.0, etc.
    opts.setUserAgent("...");
    return new Sandbox(opts);
}
```

Затем вызывайте `createSandbox(3.0)` для 3× устройства. Такая гибкость удобна, когда вы создаёте сервис, возвращающий миниатюры для iPhone, iPad и Android‑планшетов одновременно.

### Rendering without JavaScript

Если захватываемая страница содержит тяжёлые скрипты, которые вам не нужны, можно отключить JavaScript для более быстрой **html to png conversion**:

```java
sandboxOptions.setJavaScriptEnabled(false);
```

Отключение скриптов может сократить время рендеринга вдвое, но имейте в виду, что некоторый динамический контент может исчезнуть.

## Common Pitfalls and How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Blurry output** | `devicePixelRatio` оставлен по умолчанию (1.0) | Явно **set device pixel ratio** to 2.0 или выше |
| **Missing fonts** | Внешние шрифты блокируются файрволом | Обеспечьте доступ к интернету или внедрите шрифты локально |
| **Out‑of‑memory errors** | Рендеринг очень больших страниц при высоком DPI | Ограничьте размер viewport или уменьшите `devicePixelRatio` |
| **Incorrect URL** | Используется относительный путь без базового URL | Укажите полный абсолютный URL или задайте `document.setBaseUrl()` |

Раннее решение этих проблем спасёт от длительных сессий отладки.

## Full Working Example

Ниже полная, готовая к запуску Java‑программа. Скопируйте её в файл `MobileRenderTutorial.java`, добавьте Aspose.HTML JAR в classpath и выполните.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.Sandbox;
import com.aspose.html.rendering.SandboxOptions;
import com.aspose.html.saving.PngSaveOptions;

public class MobileRenderTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox that mimics a mobile device viewport
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixel width
        sandboxOptions.setScreenHeight(667);         // CSS pixel height
        sandboxOptions.setDevicePixelRatio(2.0);     // High‑density screen (set device pixel ratio)
        sandboxOptions.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // Step 2: Load the HTML page inside the sandbox
        HTMLDocument document = new HTMLDocument(
            "https://example.com/mobile.html", // Replace with your own URL
            mobileSandbox);

        // Step 3: Render the page to a PNG image
        PngSaveOptions pngOptions = new PngSaveOptions();
        document.save("output/mobile_view.png", pngOptions);

        System.out.println("Mobile view rendered.");
    }
}
```

> **Result:** Программа создаёт `output/mobile_view.png` — скриншот высокого разрешения, учитывающий **set device pixel ratio**, который вы задали.

## Visual Confirmation

<img src="output/mobile_view.png" alt="set device pixel ratio example screenshot" width="400"/>

Изображение выше (заполнитель) показывает финальный PNG после процесса рендеринга. Обратите внимание на чёткий текст и правильно масштабированные элементы UI — именно то, чего вы ожидаете, когда **set device pixel ratio** настроен корректно.

## Conclusion

Теперь вы уверенно знаете, как **set device pixel ratio** в Java, выполнить **html to png conversion** и **save webpage as png** с помощью Aspose.HTML. Это покрывает основной рабочий процесс «как отрендерить png» и предоставляет переиспользуемый шаблон для любой задачи **java html to image**.

Готовы к следующему шагу? Попробуйте заменить URL на динамическую страницу, поэкспериментировать с различными значениями `devicePixelRatio` или интегрировать этот фрагмент в endpoint Spring Boot, который будет возвращать PNG‑файлы по запросу. Возможности безграничны, а с фундаментальными знаниями расширять решение будет проще простого.

Happy coding, and feel free to drop a comment

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}