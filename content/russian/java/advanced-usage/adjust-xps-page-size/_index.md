---
title: Настройте размер страницы XPS с помощью Aspose.HTML для Java
linktitle: Настройка размера страницы XPS
second_title: Обработка Java HTML с помощью Aspose.HTML
description: Узнайте, как настроить размер страницы XPS с помощью Aspose.HTML для Java. Легко управляйте выходными размерами документов XPS.
type: docs
weight: 16
url: /ru/java/advanced-usage/adjust-xps-page-size/
---

В этом уроке мы покажем вам процесс настройки размера страницы XPS с помощью Aspose.HTML для Java. Эта мощная библиотека позволяет вам манипулировать HTML-документами и отображать их в различных форматах, включая XPS. Настройка размера страницы необходима, когда вам нужно контролировать выходные размеры вашего документа XPS.

## Предварительные условия

Прежде чем мы начнем, убедитесь, что у вас есть следующие предварительные условия:

1. Среда разработки Java: убедитесь, что в вашей системе установлен Java Development Kit (JDK).

2.  Библиотека Aspose.HTML для Java: вам необходимо загрузить и включить библиотеку Aspose.HTML для Java в свой проект Java. Вы можете найти библиотеку[здесь](https://releases.aspose.com/html/java/).

3. Входной HTML-файл: подготовьте HTML-файл, который вы хотите отобразить, и настройте для него размер страницы XPS. Для этого урока вы можете использовать свой собственный HTML-файл.

## Импортировать пакеты

Во-первых, вам необходимо импортировать необходимые пакеты для работы с Aspose.HTML for Java. Включите эти пакеты в начало вашего класса Java:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Шаг 1. Установите имя входного файла

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 На этом этапе мы читаем ваш входной HTML-файл, используя`FileInputStream`.

## Шаг 2. Создайте HTML-документ и установите стили.

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Этот шаг предполагает создание`HTMLDocument` и добавление к нему стилей.

## Шаг 3. Создайте параметры рендеринга XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Здесь мы создаем параметры рендеринга XPS для настройки процесса рендеринга.

## Шаг 4. Отрегулируйте размер страницы.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Этот шаг включает в себя настройку размера страницы и указание, следует ли настроить его на самую широкую страницу.

## Шаг 5: визуализируйте результат

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

На последнем этапе мы визуализируем выходные данные XPS, используя настроенные параметры.

## Заключение

В этом уроке мы показали вам, как настроить размер страницы XPS с помощью Aspose.HTML для Java. Вы можете контролировать выходные размеры документов XPS, гарантируя, что они соответствуют вашим конкретным требованиям. С помощью предоставленного кода и шагов вы можете легко реализовать эту функцию в своих приложениях Java.

 Если у вас есть какие-либо вопросы или вам нужна дополнительная помощь, посетите[Документация Aspose.HTML для Java](https://reference.aspose.com/html/java/) или попросите помощи на[Аспосе Форум](https://forum.aspose.com/).

## Часто задаваемые вопросы

### Вопрос 1. Что такое Aspose.HTML для Java?

A1: Aspose.HTML for Java — это библиотека Java, которая позволяет разработчикам манипулировать и конвертировать HTML-документы в различные форматы, такие как XPS, PDF и изображения.

### Вопрос 2. Где я могу скачать Aspose.HTML для Java?

 A2: Вы можете загрузить библиотеку Aspose.HTML для Java с сайта[эта ссылка](https://releases.aspose.com/html/java/).

### Вопрос 3: Существует ли бесплатная пробная версия Aspose.HTML для Java?

 О3: Да, вы можете получить бесплатную пробную версию Aspose.HTML для Java на сайте[здесь](https://releases.aspose.com/).

### Вопрос 4: Как я могу получить временную лицензию на Aspose.HTML для Java?

 A4: Чтобы получить временную лицензию на Aspose.HTML для Java, посетите[эта страница](https://purchase.aspose.com/temporary-license/).

### Вопрос 5: Могу ли я получить поддержку Aspose.HTML для Java?

 О5: Да, вы можете обратиться за помощью и поддержкой к сообществу Aspose на сайте[Аспосе Форум](https://forum.aspose.com/).