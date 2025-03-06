---
title: Настройте размер страницы XPS с помощью Aspose.HTML для Java
linktitle: Настройка размера страницы XPS
second_title: Обработка Java HTML с помощью Aspose.HTML
description: Узнайте, как настроить размер страницы XPS с помощью Aspose.HTML для Java. Легко контролируйте выходные размеры ваших документов XPS.
weight: 16
url: /ru/java/advanced-usage/adjust-xps-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Настройте размер страницы XPS с помощью Aspose.HTML для Java


В этом уроке мы проведем вас через процесс настройки размера страницы XPS с помощью Aspose.HTML для Java. Эта мощная библиотека позволяет вам манипулировать документами HTML и отображать их в различных форматах, включая XPS. Настройка размера страницы имеет важное значение, когда вам нужно контролировать выходные размеры вашего документа XPS.

## Предпосылки

Прежде чем начать, убедитесь, что у вас выполнены следующие предварительные условия:

1. Среда разработки Java: убедитесь, что в вашей системе установлен Java Development Kit (JDK).

2.  Библиотека Aspose.HTML for Java: Вам необходимо загрузить и включить библиотеку Aspose.HTML for Java в ваш проект Java. Библиотеку можно найти[здесь](https://releases.aspose.com/html/java/).

3. Входной HTML-файл: Подготовьте HTML-файл, который вы хотите отрендерить, и настройте размер страницы XPS. Вы можете использовать свой собственный HTML-файл для этого руководства.

## Импортные пакеты

Во-первых, вам нужно импортировать необходимые пакеты для работы с Aspose.HTML для Java. Включите эти пакеты в начало вашего класса Java:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Шаг 1: Задайте имя входного файла

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 На этом этапе мы считываем ваш входной HTML-файл с помощью`FileInputStream`.

## Шаг 2: Создайте HTML-документ и задайте стили

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

 Этот шаг включает в себя создание`HTMLDocument` и добавление к нему стилей.

## Шаг 3: Создание параметров рендеринга XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Здесь мы создаем параметры рендеринга XPS для настройки процесса рендеринга.

## Шаг 4: Настройте размер страницы

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

На этом этапе необходимо задать размер страницы и указать, следует ли подгонять его под самую широкую страницу.

## Шаг 5: Рендеринг вывода

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

На последнем этапе мы визуализируем вывод XPS, используя настроенные параметры.

## Заключение

В этом уроке мы показали вам, как настроить размер страницы XPS с помощью Aspose.HTML для Java. Вы можете контролировать выходные размеры ваших документов XPS, гарантируя, что они соответствуют вашим конкретным требованиям. С помощью предоставленного кода и шагов вы можете легко реализовать эту функцию в своих приложениях Java.

 Если у вас есть какие-либо вопросы или вам нужна дополнительная помощь, посетите[Документация Aspose.HTML для Java](https://reference.aspose.com/html/java/) или попросите о помощи на[Форум Aspose](https://forum.aspose.com/).

## Часто задаваемые вопросы

### В1: Что такое Aspose.HTML для Java?

A1: Aspose.HTML для Java — это библиотека Java, которая позволяет разработчикам обрабатывать и конвертировать HTML-документы в различные форматы, такие как XPS, PDF и изображения.

### В2: Где я могу скачать Aspose.HTML для Java?

 A2: Вы можете загрузить библиотеку Aspose.HTML для Java с сайта[эта ссылка](https://releases.aspose.com/html/java/).

### В3: Существует ли бесплатная пробная версия Aspose.HTML для Java?

 A3: Да, вы можете получить бесплатную пробную версию Aspose.HTML для Java по ссылке[здесь](https://releases.aspose.com/).

### В4: Как получить временную лицензию на Aspose.HTML для Java?

 A4: Чтобы получить временную лицензию на Aspose.HTML для Java, посетите[эта страница](https://purchase.aspose.com/temporary-license/).

### В5: Могу ли я получить поддержку Aspose.HTML для Java?

 A5: Да, вы можете обратиться за помощью и поддержкой к сообществу Aspose на[Форум Aspose](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
