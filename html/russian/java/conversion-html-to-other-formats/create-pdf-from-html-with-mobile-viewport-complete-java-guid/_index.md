---
category: general
date: 2026-03-18
description: Быстро создавайте PDF из HTML на Java. Узнайте, как конвертировать HTML
  в PDF, симулировать экран iPhone и задавать размер экрана для адаптивных PDF.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- simulate iphone screen
- how to set screen
- how to convert html
language: ru
og_description: Создайте PDF из HTML в Java. Это руководство показывает, как конвертировать
  HTML в PDF, имитировать экран iPhone и задавать размеры экрана для идеальных адаптивных
  PDF.
og_title: Создание PDF из HTML с мобильным viewport — учебник по Java
tags:
- Java
- Aspose.HTML
- PDF
- Responsive Design
- Mobile Viewport
title: Создание PDF из HTML с мобильным viewport – Полное руководство по Java
url: /ru/java/conversion-html-to-other-formats/create-pdf-from-html-with-mobile-viewport-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF из HTML с мобильным viewport – Полное руководство на Java

Когда‑то вам нужно было **create PDF from HTML**, но результат выглядел как настольная страница на крошечном экране телефона? Вы не одиноки. При конвертации адаптивного сайта в PDF, viewport по умолчанию часто игнорирует мобильные брейкпоинты, оставляя вас с тесным беспорядком.  

Хорошая новость? Вы можете **convert HTML to PDF**, **simulating an iPhone screen**, используя простой Java‑код. В этом руководстве мы пройдем каждый шаг — как задать размер экрана, как настроить коэффициент масштабирования устройства и почему эти настройки важны для пиксель‑идеального PDF.

> **Pro tip:** Если вы уже использовали Aspose.HTML для простых конвертаций, вы обнаружите, что настройки viewport находятся всего в нескольких строках кода от вас.

---

## Что вы узнаете

* Как **create PDF from HTML** с помощью Aspose.HTML for Java.  
* Точный код для **simulate iPhone screen** размеров (375 × 667 px @ 2× плотность).  
* Где разместить параметры **how to set screen** в конвейере конвертации.  
* Распространённые подводные камни при конвертации адаптивных страниц и как их избежать.  
* Полный, готовый к запуску пример на Java, который можно скопировать‑вставить в IDE.

### Требования

* Java 17 или новее (код компилируется и в более старых версиях, но рекомендуется 17).  
* Библиотека Aspose.HTML for Java — вы можете скачать последнюю JAR‑файл с [Aspose website](https://products.aspose.com/html/java).  
* Простой HTML‑файл (`input.html`), который нужно превратить в PDF.  
* Базовое знакомство с Maven или Gradle (мы покажем фрагмент Maven).

---

## Шаг 1 – Добавьте Aspose.HTML в ваш проект

Сначала вам нужна библиотека в classpath. Если вы используете Maven, добавьте эту зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Why this matters:** Aspose.HTML выполняет тяжёлую работу — парсинг HTML, применение CSS и растрирование макета. Без неё вам пришлось бы писать полноценный браузерный движок, а это *много* работы.

Если вы предпочитаете Gradle, эквивалент выглядит так:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

---

## Шаг 2 – Подготовьте параметры загрузки и смоделируйте iPhone viewport

Теперь мы настроим параметры **how to set screen**. Класс `HtmlLoadOptions` позволяет указать Aspose, какого размера и с какой плотностью пикселей следует «притворяться», что у браузера.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;

public class ViewportDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create load options for the HTML document
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();

        // 2️⃣ Simulate a mobile viewport (iPhone 6/7/8) – 375 × 667 pixels with retina density
        loadOptions.setScreenSize(new Size(375, 667));
        loadOptions.setDeviceScaleFactor(2.0);

        // 3️⃣ Convert the HTML file to PDF using the configured viewport
        Converter.convertDocument(
                "YOUR_DIRECTORY/input.html",          // source HTML
                "YOUR_DIRECTORY/output.pdf",          // destination PDF
                new PdfSaveOptions(),
                loadOptions);

        // 4️⃣ Notify that the conversion is complete
        System.out.println("Responsive conversion using mobile viewport.");
    }
}
```

### Почему эти цифры?

* **375 × 667** соответствует логическим CSS‑пикселям iPhone 6/7/8 в портретной ориентации.  
* **DeviceScaleFactor = 2.0** сообщает рендереру, что каждый CSS‑пиксель соответствует двум физическим пикселям, имитируя Retina‑дисплей.  

Если нужен другой девайс — например iPhone 12 Pro Max, измените размер на `428 × 926` и оставьте коэффициент масштабирования `3.0`.

---

## Шаг 3 – Запустите конвертацию и проверьте результат

Скомпилируйте и запустите класс:

```bash
mvn compile exec:java -Dexec.mainClass=ViewportDemo
```

После завершения программы откройте `output.pdf`. Вы должны увидеть:

* Все media‑queries, нацеленные на `max-width: 375px`, применены корректно.  
* Изображения отрисованы чётко благодаря 2× коэффициенту масштабирования.  
* Текст, соблюдающий иерархию размеров шрифтов для мобильных, определённую в CSS.

Если PDF всё ещё выглядит как настольная страница, дважды проверьте, что ваш HTML использует responsive meta‑тег:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Без этого тега даже идеальная настройка viewport не активирует мобильную таблицу стилей.

---

## Шаг 4 – Обработка внешних ресурсов (изображения, шрифты, CSS)

Когда вы **convert HTML to PDF**, Aspose.HTML пытается загрузить каждый связанный ресурс. Если вы конвертируете страницу, находящуюся в локальной файловой системе, абсолютные URL (`file:///…`) работают без проблем. Для удалённых ресурсов могут возникнуть:

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **404 errors for images** | HTML ссылается на URL, требующий аутентификации. | Используйте `HtmlLoadOptions.setBaseUrl("file:///C:/myproject/")` для разрешения относительных путей или внедрите изображения в виде Base64. |
| **Missing web fonts** | PDF‑движок не может скачать файл шрифта. | Скачайте файлы `.woff`/`.ttf` локально и укажите их относительным путём. |
| **CSS not applied** | CSS‑файл заблокирован CORS. | Разместите CSS на сервере, разрешающем кросс‑origin запросы, либо встроите CSS непосредственно в HTML. |

Быстрый способ проверить загрузку ресурсов — обернуть вызов конвертации в блок try‑catch и вывести сообщение `Exception`. Aspose.HTML предоставляет детальные логи, указывающие точный URL, который не удалось загрузить.

```java
try {
    Converter.convertDocument(...);
} catch (Exception ex) {
    System.err.println("Conversion failed: " + ex.getMessage());
}
```

---

## Шаг 5 – Расширенные настройки (опционально)

### a) Change PDF Page Size

По умолчанию Aspose.HTML создаёт страницу PDF, соответствующую размеру viewport. Если вам нужен A4 или Letter, добавьте конфигурацию `PdfSaveOptions`:

```java
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PageSize.A4);
Converter.convertDocument("input.html", "output.pdf", pdfOptions, loadOptions);
```

### b) Add a Header/Footer Programmatically

Вы можете добавить простой header/footer после конвертации, используя Aspose.PDF (отдельная библиотека). Рабочий процесс:

1. Конвертировать HTML → PDF (как показано).  
2. Открыть полученный PDF с помощью Aspose.PDF.  
3. Добавить объекты `HeaderFooter` на каждую страницу.

```java
import com.aspose.pdf.*;

Document pdfDoc = new Document("output.pdf");
for (Page page : pdfDoc.getPages()) {
    page.addHeaderFooter(new HeaderFooter("Generated on " + LocalDate.now()));
}
pdfDoc.save("output-with-header.pdf");
```

### c) Batch Conversion

Если у вас есть папка с HTML‑файлами, выполните цикл по ним:

```java
Files.list(Paths.get("html_folder"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(p -> {
         String pdfPath = p.toString().replace(".html", ".pdf");
         Converter.convertDocument(p.toString(), pdfPath, new PdfSaveOptions(), loadOptions);
     });
```

---

## Часто задаваемые вопросы (FAQ)

**Q: Does this work with JavaScript‑heavy pages?**  
A: Aspose.HTML поддерживает подмножество JavaScript. Простые манипуляции DOM и изменения CSS обычно работают, но сложные фреймворки (React, Angular) могут потребовать предварительно отрендеренный статический HTML‑снимок.

**Q: What if I need to convert a page that uses `@media print` rules?**  
A: Библиотека автоматически учитывает `@media print`. Однако, если вы также задаёте мобильный viewport, таблица стилей `print` может переопределить некоторые мобильные стили. Протестируйте оба сценария.

**Q: Can I set a custom DPI for the PDF?**  
A: Да. Используйте `PdfSaveOptions.setDpi(300)` перед конвертацией. Более высокий DPI приводит к большим файлам, но изображения становятся чётче.

---

## Ожидаемый скриншот результата

Ниже показана иллюстрация финальной страницы PDF (смоделирован мобильный viewport).  
![Скриншот PDF, сгенерированного демонстрацией create pdf from html, показывающий макет размера iPhone]  

*Текст alt‑изображения содержит основной ключевой запрос для SEO.*

---

## Заключение

Теперь у вас есть надёжный workflow **create pdf from html**, который учитывает мобильные брейкпоинты, имитирует экран iPhone и даёт полный контроль над размерами страниц. Настраивая `HtmlLoadOptions`, вы можете ответить на вопрос «**how to set screen**» для любого устройства, а используя `Converter.convertDocument`, вы освоили **how to convert html** в Java.

Готовы к следующему вызову? Попробуйте сочетать этот подход с Aspose.PDF для добавления водяных знаков, объединения нескольких PDF или защиты документа паролем. И не забывайте экспериментировать с другими устройствами — просто измените значения `Size` и `DeviceScaleFactor` под нужную вам плотность пикселей.

Счастливого кодинга, и пусть ваши PDF всегда выглядят так же чётко на бумаге, как на экране телефона! 

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}