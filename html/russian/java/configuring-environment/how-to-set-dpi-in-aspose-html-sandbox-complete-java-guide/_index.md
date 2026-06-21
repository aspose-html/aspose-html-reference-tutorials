---
category: general
date: 2026-04-02
description: Узнайте, как установить DPI, задать размер области просмотра и установить
  пользовательский агент в Aspose.HTML Sandbox. Пошаговый пример на Java с полным
  кодом и советами.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: ru
og_description: Освойте, как установить DPI, задать размер области просмотра и указать
  пользовательский агент в Aspose.HTML Sandbox с полным примером на Java.
og_title: Как установить DPI в Aspose.HTML Sandbox – учебник Java
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Как установить DPI в песочнице Aspose.HTML – Полное руководство по Java
url: /ru/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как установить DPI в песочнице Aspose.HTML – Полное руководство на Java

Когда‑то задумывались **как установить DPI** при рендеринге веб‑страницы с помощью Aspose.HTML? Вы не одиноки. Во многих тестовых сценариях необходимо, чтобы макет соответствовал определённой плотности экрана — например, готовым к печати PDF‑файлам или скриншотам высокого разрешения. Хорошая новость: песочница Aspose.HTML позволяет управлять DPI, размером области просмотра и даже строкой user‑agent в одном удобном пакете.

В этом руководстве мы пройдём практический пример на Java, который **устанавливает DPI**, **устанавливает размер области просмотра** и **устанавливает user‑agent** одновременно. К концу вы получите готовую к запуску программу, поймёте, почему каждую настройку важно задавать, и сможете адаптировать песочницу под свои проекты.

---

## Что вам понадобится

- **Java 17** (или любой современный JDK; API совместим с Java 8+)
- **Aspose.HTML for Java** библиотека (версия 23.12 или новее)
- IDE или простой текстовый редактор + компиляция через командную строку
- Доступ в Интернет для примера URL (`https://example.com`)

Внешние инструменты сборки не требуются; код компилируется с помощью `javac` и запускается через `java`. Если вы предпочитаете Maven или Gradle, просто добавьте зависимость Aspose.HTML — ничего сложного.

---

## Шаг 1: Создать песочницу, определяющую среду рендеринга

Песочница — это место, где вы говорите Aspose.HTML, какой «экран» вы имитируете. Здесь мы задаём **область просмотра 1024 × 768**, **DPI 96** и пользовательскую **строку user‑agent**.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Почему это важно:**  
- **DPI** влияет на то, как единицы CSS `pt` преобразуются в пиксели; более высокое DPI даёт более чёткое изображение.  
- **Размер области просмотра** определяет точки прерывания макета, которые будет использовать адаптивный CSS.  
- **User‑agent** может вызывать вариации контента на сервере (мобильный vs десктопный).

> **Pro tip:** Если вы позже генерируете PDF, подберите DPI, соответствующее целевому разрешению печати (например, 300 dpi для печати высокого качества).

---

## Шаг 2: Загрузить веб‑страницу внутри песочницы

Теперь указываем песочнице URL. Конструктор `HTMLDocument` принимает объект песочницы, поэтому движок разметки учитывает заданные нами параметры.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**Что происходит «под капотом»?**  
Aspose.HTML создаёт изолированный контекст рендеринга, похожий на безголовый браузер, но без накладных расходов полного Chromium‑экземпляра. Это делает операцию быстрой и экономичной по памяти — идеально для пакетной обработки.

---

## Шаг 3: Взаимодействие с DOM — чтение заголовка страницы

Для демонстрации получим заголовок и выведем его. В реальном проекте вы можете сделать скриншот, экспортировать в PDF или собрать данные.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Ожидаемый вывод** (при доступности `https://example.com`):

```
Title inside sandbox: Example Domain
```

Если сайт вернёт другой заголовок, вы увидите его — других изменений не требуется.

---

## Шаг 4: Проверка настроек (необязательная отладка)

Иногда хочется убедиться, что песочница действительно учитывает ваш DPI и размер области просмотра. Aspose.HTML не раскрывает эти значения напрямую, но их можно вывести, измерив размеры элементов.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

Если в CSS указано `width: 200pt;`, при **96 dpi** вы должны увидеть `200pt * (96/72) ≈ 267px`. Измените DPI и запустите снова, чтобы увидеть изменение числа — это доказательство того, что **как установить dpi** действительно работает.

---

## Полный исходный код в одном блоке

Скопируйте‑вставьте следующее в файл `SandboxExample.java`. Он компилируется «как есть»; просто убедитесь, что JAR‑файл Aspose.HTML находится в classpath.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Скомпилировать и запустить:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

Вы должны увидеть напечатанный заголовок, подтверждая, что песочница работает с **установленным dpi**, **установленным размером области просмотра** и **установленным user‑agent**, которые вы задали.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если нужен другой DPI?

Просто измените второй аргумент `DocumentSandbox`. Для PDF‑файлов, готовых к печати, можно использовать `300`:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

Большее DPI даёт больше пикселей для тех же CSS‑точек, улучшая качество растра, но потребляет больше памяти.

### Можно ли загрузить локальный HTML‑файл вместо URL?

Конечно. Замените URL на путь к файлу:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Убедитесь, что путь абсолютный и использует схему `file:///`.

### Как изменить user‑agent после создания песочницы?

Песочница неизменяема — как только вы передаёте её в `HTMLDocument`, настройки фиксируются. Чтобы использовать другой user‑agent, создайте новый `DocumentSandbox` с нужной строкой.

### Поддерживает ли Aspose.HTML выполнение JavaScript?

Да, движок исполняет большинство клиентских скриптов. Если скрипт изменяет DOM после загрузки, можно подождать немного:

```java
webDoc.waitForLoad();
```

Или использовать логику, аналогичную `setTimeout`, внутри страницы перед запросом элементов.

---

## Визуальное подтверждение (изображение)

Ниже показан скриншот консоли с успешным запуском. Обратите внимание, что вывод заголовка совпадает со страницей, подтверждая, что песочница учла наши настройки.

![Консольный вывод, показывающий как установить dpi в песочнице Aspose.HTML](/images/console-output.png)

*Alt text:* *Консольный вывод, демонстрирующий установку dpi, размера области просмотра и user‑agent в песочнице Aspose.HTML.*

---

## Итоги и дальнейшие шаги

Мы рассмотрели **как установить DPI** (96 dpi в примере), **как установить размер области просмотра** (1024 × 768) и **как установить user‑agent** (пользовательская строка) с помощью API песочницы Aspose.HTML. Полностью рабочая Java‑программа доказывает, что эти настройки не просто теоретические — они напрямую влияют на рендеринг и взаимодействие с DOM.

Готовы к следующему?

- **Экспорт в PDF:** После загрузки страницы вызовите `webDoc.save("output.pdf", SaveFormat.PDF);`, чтобы получить PDF высокого разрешения, отражающий заданный DPI.  
- **Создание скриншота:** Используйте `webDoc.renderToBitmap("screenshot.png");` для пиксель‑точных изображений.  
- **Эксперименты с адаптивными макетами:** Меняйте размеры области просмотра, чтобы тестировать мобильные брейкпоинты без реального устройства.  

Экспериментируйте с различными значениями DPI, комбинациями размеров области просмотра и строками user‑agent, наблюдая, как серверы и CSS реагируют. Песочница — это лёгкая игровая площадка, экономящая время на запуск полноценных браузеров.

---

### Продолжайте исследовать

- **Документация Aspose.HTML** — подробный обзор параметров `DocumentSandbox`.  
- **Продвинутые медиазапросы CSS** — узнайте, как размер области просмотра активирует разные стили.  
- **Подмена User‑Agent** — изучите, как некоторые сайты предоставляют альтернативную разметку в зависимости от строки агента.

Есть вопросы или сложный кейс? Оставьте комментарий, и мы разберёмся вместе. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}