---
date: 2026-08-28
description: Настройте размер страницы XPS при конвертации HTML в XPS на Java с использованием
  Aspose.HTML. Рендеринг HTML в XPS с точными размерами.
keywords:
- adjust xps page size
- render html to xps
- aspose.html java
- xps conversion java
- html to xps
lastmod: 2026-08-28
linktitle: Настройка размера страницы XPS
og_description: Настройте размер страницы XPS при конвертации HTML в XPS на Java с
  использованием Aspose.HTML. Узнайте, как быстро рендерить HTML в XPS с точными размерами.
og_image_alt: Tutorial showing how to adjust XPS page size during HTML to XPS conversion
  with Aspose.HTML for Java
og_title: Настройка размера страницы XPS при конвертации HTML в XPS на Java
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  headline: Adjust XPS page size when converting HTML to XPS in Java
  type: TechArticle
- description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  name: Adjust XPS page size when converting HTML to XPS in Java
  steps:
  - name: set the input file name
    text: The `FileInputStream` class reads raw bytes from a file, providing the HTML
      source to the renderer.
  - name: create an HTML document and set styles
    text: The `HTMLDocument` class represents an in‑memory HTML DOM used by Aspose.HTML
      for rendering.
  - name: create XPS rendering options
    text: The `XpsRenderingOptions` class holds settings that control how HTML is
      rendered to XPS, such as page size and image quality.
  - name: adjust the page size
    text: '**How to set XPS page size** – Define a custom page size (width × height
      in points) and tell the renderer whether it should automatically expand to the
      widest page. Setting `adjustToWidestPage` to `false` preserves the exact dimensions
      you specify. The `PageSetup` class defines page size, margins, a'
  - name: render the output
    text: The `XpsDevice` class is the rendering target that writes the processed
      content to an XPS file.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a Java library that allows developers to manipulate
      and convert HTML documents into various formats, such as XPS, PDF, and images.
      You can download the library from [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).
    question: What is Aspose.HTML for Java?
  - answer: You can download the Aspose.HTML for Java library from [Aspose product
      releases page](https://releases.aspose.com/).
    question: Where can I download Aspose.HTML for Java?
  - answer: Yes, you can get a free trial of Aspose.HTML for Java from the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: Is there a free trial available for Aspose.HTML for Java?
  - answer: To get a temporary license for Aspose.HTML for Java, visit the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for Aspose.HTML for Java?
  - answer: Yes, you can seek help and support from the Aspose community on the [Aspose
      Forum](https://forum.aspose.com/).
    question: Can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- adjust xps page size
- Aspose.HTML
- Java XPS conversion
- HTML to XPS
- document rendering
title: Настройка размера страницы XPS при конвертации HTML в XPS на Java
url: /ru/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Настройка размера страницы XPS при конвертации HTML в XPS на Java

В этом руководстве вы узнаете **как настроить размер страницы XPS** при конвертации HTML в XPS с помощью Aspose.HTML for Java. Независимо от того, нужны ли вам печатные счета‑фактуры, архивные отчёты или этикетки нестандартных размеров, контроль над размерами страницы гарантирует, что итоговый XPS будет выглядеть точно так, как задумано. Мы пройдём настройку окружения, параметры рендеринга и генерацию финального XPS, чтобы вы могли встроить эту возможность непосредственно в свои Java‑приложения.

## Быстрые ответы
- **Что означает «convert HTML to XPS»?** Он рендерит HTML‑документ в файл XPS, сохраняя макет и стили.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для разработки; для продакшн‑использования требуется коммерческая лицензия.  
- **Какая версия Java поддерживается?** Java 8 или выше (рекомендовано JDK 11+).  
- **Можно ли изменить размер страницы?** Да — Aspose.HTML позволяет задать пользовательские размеры перед рендерингом.  
- **Сколько времени занимает конвертация?** Обычно менее секунды для стандартных страниц; более крупные документы могут занимать больше времени.

## Что такое конвертация HTML в XPS?

Конвертация HTML в XPS означает преобразование веб‑ориентированного файла разметки в документ XPS (XML Paper Specification) — фиксированный, готовый к печати формат, похожий на PDF. Это полезно, когда требуются высококачественные, независимые от устройства документы для архивирования или печати из Java‑приложений.

## Зачем настраивать размер страницы XPS?

Настройка размера страницы XPS даёт вам контроль над физическими размерами конечного документа (например, A4, Letter, пользовательские этикетки). Это предотвращает нежелательное масштабирование, гарантирует точное размещение содержимого и может уменьшить размер файла, устраняя лишние пустые области.

## Как отрендерить HTML в XPS с пользовательским размером страницы?

Загрузите ваш HTML, настройте `XpsRenderingOptions` с помощью `PageSetup`, который задаёт точную ширину и высоту, необходимые вам, затем выполните рендеринг в `XpsDevice`. Этот двухшаговый процесс позволяет сохранить макет неизменным, одновременно задавая требуемые размеры, всё в одном вызове API.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть следующие предварительные требования:

1. **Java Development Environment** – установленный на вашей системе Java Development Kit (JDK).  
2. **Aspose.HTML for Java Library** – Скачайте и подключите библиотеку Aspose.HTML for Java в ваш проект. Вы можете найти библиотеку на странице [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).  
3. **Input HTML File** – Подготовьте HTML‑файл, который вы хотите отрендерить и настроить размер страницы XPS. Вы можете использовать свой собственный HTML‑файл для этого руководства.

## Импорт пакетов

Класс `Page` представляет размеры страницы и настройки для вывода XPS. Класс `HtmlRenderer` выполняет конвертацию из HTML в XPS.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Пошаговое руководство

Ниже представлена краткая нумерованная пошаговая инструкция, отражающая оригинальные шаги с добавлением дополнительного контекста для ясности.

### Шаг 1: задать имя входного файла

Класс `FileInputStream` читает необработанные байты из файла, предоставляя HTML‑исходник рендереру.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Шаг 2: создать HTML‑документ и задать стили

Класс `HTMLDocument` представляет DOM HTML в памяти, используемый Aspose.HTML для рендеринга.

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### Шаг 3: создать параметры рендеринга XPS

Класс `XpsRenderingOptions` содержит настройки, управляющие тем, как HTML рендерится в XPS, такие как размер страницы и качество изображений.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Шаг 4: настроить размер страницы  

**Как задать размер страницы XPS** – Определите пользовательский размер страницы (ширина × высота в пунктах) и укажите рендереру, следует ли автоматически расширять её до самой широкой страницы. Установка `adjustToWidestPage` в `false` сохраняет точные размеры, которые вы задаёте.

Класс `PageSetup` определяет размер страницы, отступы и ориентацию для вывода XPS.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Шаг 5: отрендерить вывод

Класс `XpsDevice` — цель рендеринга, записывающая обработанное содержимое в файл XPS.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Распространённые проблемы и решения

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Пустой вывод XPS** | Поток ввода не закрыт или HTMLDocument указывает на неправильный файл. | Убедитесь, что `FileInputStream` правильно обёрнут в блок try‑with‑resources, и путь к файлу указан верно. |
| **Размер страницы не применён** | `adjustToWidestPage` оставлен `true`. | Установите `pageSetup.setAdjustToWidestPage(false);`, как показано в Шаге 4. |
| **Неподдерживаемый CSS** | Aspose.HTML поддерживает лишь часть CSS. | Используйте базовый макет, шрифты и цвета; избегайте сложных селекторов или CSS Grid. |
| **LicenseException** | Запуск без действующей лицензии в продакшн‑среде. | Примените временную или приобретённую лицензию перед рендерингом (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Часто задаваемые вопросы

**Q: Что такое Aspose.HTML for Java?**  
A: Aspose.HTML for Java — это Java‑библиотека, позволяющая разработчикам манипулировать и конвертировать HTML‑документы в различные форматы, такие как XPS, PDF и изображения. Вы можете скачать библиотеку со страницы [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).

**Q: Где можно скачать Aspose.HTML for Java?**  
A: Вы можете скачать библиотеку Aspose.HTML for Java со страницы [Aspose product releases page](https://releases.aspose.com/).

**Q: Доступна ли бесплатная пробная версия Aspose.HTML for Java?**  
A: Да, вы можете получить бесплатную пробную версию Aspose.HTML for Java на странице [temporary license request page](https://purchase.aspose.com/temporary-license/).

**Q: Как получить временную лицензию для Aspose.HTML for Java?**  
A: Чтобы получить временную лицензию для Aspose.HTML for Java, посетите страницу [temporary license request page](https://purchase.aspose.com/temporary-license/).

**Q: Можно ли получить поддержку для Aspose.HTML for Java?**  
A: Да, вы можете обратиться за помощью и поддержкой к сообществу Aspose на [Aspose Forum](https://forum.aspose.com/).

**Q: Можно ли конвертировать HTML в XPS на сервере без графического интерфейса?**  
A: Конечно. Aspose.HTML работает в средах без GUI; просто убедитесь, что Java‑runtime правильно настроен.

**Q: Поддерживает ли библиотека пользовательские поля страницы?**  
A: Да. Используйте `PageSetup.setMarginTop()`, `setMarginBottom()` и т.д., перед тем как назначить `PageSetup` в параметры рендеринга.

## Заключение

Мы прошли полный процесс **конвертации HTML в XPS** и **настройки размера страницы XPS** с помощью Aspose.HTML for Java. Следуя этим шагам, вы сможете создавать готовые к печати XPS‑документы, соответствующие вашим точным требованиям к макету. Не стесняйтесь экспериментировать с различными размерами страниц, стилями или даже добавлять заголовки и колонтитулы, чтобы удовлетворить потребности вашего проекта.

Если у вас есть вопросы или нужна дополнительная помощь, ознакомьтесь с [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/) или присоединитесь к обсуждению на [Aspose Forum](https://forum.aspose.com/).

---

**Последнее обновление:** 2026-08-28  
**Тестировано с:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Автор:** Aspose

## Связанные руководства

- [Конвертировать HTML в XPS с помощью Aspose.HTML for Java](/html/java/conversion-html-to-other-formats/convert-html-to-xps/)
- [Настроить размер страницы PDF с Aspose.HTML for Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Конвертация EPUB в XPS с Aspose.HTML for Java](/html/java/converting-epub-to-xps/convert-epub-to-xps/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}