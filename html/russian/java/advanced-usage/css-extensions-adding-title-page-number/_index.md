---
date: 2025-12-05
description: Узнайте, как установить поля HTML‑страницы в Java с помощью Aspose.HTML
  и добавить номера страниц и заголовки в ваши документы.
language: ru
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Как установить поля HTML‑страницы в Java с помощью Aspose.HTML
url: /java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как установить поля HTML‑страницы в Java с помощью Aspose.HTML

В этом руководстве вы узнаете, **как установить поля HTML‑страницы в Java** с помощью Aspose.HTML для Java. Мы пройдёмся по созданию пользовательских полей страницы, вставке номеров страниц и добавлению заголовка документа — всё с понятным пошаговым кодом, который вы можете скопировать в свой проект.

## Быстрые ответы
- **Какая библиотека нужна?** Aspose.HTML for Java  
- **Можно ли управлять полями программно?** Да, через правило CSS `@page` в пользовательской таблице стилей  
- **Какие форматы вывода поддерживают поля?** XPS, PDF и другие растровые форматы  
- **Нужна ли лицензия для продакшна?** Требуется действующая лицензия Aspose.HTML для использования не в режиме пробной версии  
- **Совместимо ли это с Java 11+?** Абсолютно — библиотека работает с современными версиями Java  

## Что означает «Установка полей HTML‑страницы в Java»?
Установка полей HTML‑страницы в Java означает настройку движка рендеринга (предоставляемого Aspose.HTML) для применения CSS‑свойств page‑box до того, как документ будет преобразован в печатный формат, такой как XPS или PDF. Определяя пользовательское правило `@page`, вы контролируете печатную область, номера страниц и содержимое верхних/нижних колонтитулов.

## Почему стоит использовать Aspose.HTML для управления полями?
- **Точная раскладка** — CSS `@page` обеспечивает пиксель‑точный контроль над полями, верхними и нижними колонтитулами.  
- **Согласованность между форматами** — Одни и те же определения полей работают для XPS, PDF и вывода изображений.  
- **Отсутствие зависимости от браузера** — Рендеринг происходит на сервере, поэтому вам не нужен headless‑браузер.  

## Предварительные требования

Перед началом убедитесь, что у вас есть следующие требования:

1. **Среда разработки Java** — установлен JDK 11 или новее.  
2. **Aspose.HTML for Java** — Скачайте и установите библиотеку по ссылке [here](https://releases.aspose.com/html/java/).  

## Импорт пакетов

Чтобы начать, импортируйте необходимые классы Aspose.HTML:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Как установить поля HTML‑страницы в Java – пошаговое руководство

### Шаг 1: Инициализация конфигурации и определение пользовательских полей страницы

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

В этом блоке мы создаём объект `Configuration`, получаем `IUserAgentService` и внедряем правило CSS `@page`, которое определяет поля, счётчик страниц в правом нижнем углу и заголовок документа в верхнем центре.

### Шаг 2: Создание HTML‑документа

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Здесь мы создаём `HTMLDocument` с простым фрагментом “Hello World”. Та же конфигурация из Шага 1 применяется, поэтому пользовательские поля учитываются при рендеринге документа.

### Шаг 3: Рендеринг в файл XPS (или любой поддерживаемый вывод)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Этот шаг создаёт `XpsDevice`, который записывает отрендеренные страницы в `output.xps`. Поля, номера страниц и заголовок, определённые ранее, появятся в итоговом файле.

## Распространённые проблемы и советы

- **Поля не изменились** — Убедитесь, что правило `@page` не переопределяется другими таблицами стилей. Вызов `setUserStyleSheet` принудительно задаёт высший приоритет.  
- **Номера страниц отображаются как «NaN»** — Проверьте, что вы используете Aspose.HTML версии 23.10 или новее; в более старых версиях отсутствует функция `currentPageNumber()`.  
- **Выходной файл пустой** — Убедитесь, что путь `Resources.output` корректен и у вас есть права записи.  

## Часто задаваемые вопросы

### Q1: Что такое Aspose.HTML for Java?

**A:** Aspose.HTML for Java — это Java‑библиотека, предоставляющая мощные инструменты для работы с HTML‑документами в Java‑приложениях, включая конвертацию, рендеринг и манипуляцию.

### Q2: Можно ли дальше настраивать поля страницы?

**A:** Да, просто отредактируйте CSS внутри `setUserStyleSheet`. Вы можете изменить любые значения `margin-*` или добавить дополнительные блоки `@top-*` / `@bottom-*`.

### Q3: Как добавить больше содержимого в HTML‑документ?

**A:** Замените строку в `new HTMLDocument("<div>Hello World!!!</div>", …)` на свою HTML‑разметку или загрузите внешний файл, используя конструктор `HTMLDocument(String url, …)`.

### Q4: Совместим ли Aspose.HTML for Java с другими форматами документов?

**A:** Абсолютно. Один и тот же `HTMLDocument` можно отрендерить в PDF, XPS, изображения или даже EPUB, заменив устройство вывода (например, `PdfDevice`, `PngDevice`).

### Q5: Нужна ли лицензия для использования Aspose.HTML for Java?

**A:** Да, лицензия требуется для продакшн‑использования. Вы можете получить пробную версию или приобрести лицензию по ссылке [here](https://purchase.aspose.com/buy) или [here](https://releases.aspose.com/).

### Q6: Как задать разные поля для нечётных и чётных страниц?

**A:** Используйте псевдоклассы `@page :left` и `@page :right` в своей таблице стилей, чтобы определить отдельные поля для левой (чётной) и правой (нечётной) страниц.

### Q7: Можно ли встроить пользовательские шрифты в отрендеренный документ?

**A:** Да. Добавьте правила `@font-face` в пользовательскую таблицу стилей и используйте эти шрифты в вашем HTML‑содержимом.

## Заключение

Вы теперь освоили **как установить поля HTML‑страницы в Java** с помощью Aspose.HTML и знаете, как добавить номера страниц и заголовок, чтобы ваши документы выглядели профессионально. Не стесняйтесь экспериментировать с дополнительными блоками `@page`, пользовательскими шрифтами или различными форматами вывода, чтобы удовлетворить потребности вашего проекта.

Если возникнут сложности, официальная [документация Aspose.HTML for Java](https://reference.aspose.com/html/java/) и [форум поддержки Aspose](https://forum.aspose.com/) — отличные места для получения помощи.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 23.12  
**Author:** Aspose  

---