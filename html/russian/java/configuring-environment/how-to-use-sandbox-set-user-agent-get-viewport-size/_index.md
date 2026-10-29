---
category: general
date: 2026-04-03
description: Узнайте, как использовать sandbox в Aspose.HTML Java для установки пользовательского
  агента, задания размеров и мгновенного получения размера области просмотра. Полный
  код, объяснения и советы включены.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: ru
og_description: Узнайте, как использовать sandbox в Aspose.HTML Java для установки
  пользовательского агента, задания размеров и мгновенного получения размеров области
  просмотра. Полное руководство с кодом и лучшими практиками.
og_title: Как использовать Sandbox – установить агент пользователя и получить размер
  области просмотра
tags:
- AsposeHTML
- Java
- Sandbox
title: Как использовать Sandbox — установить User Agent и получить размер области
  просмотра
url: /ru/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать Sandbox – задать User Agent и получить размер Viewport

Когда‑нибудь задумывались **как использовать sandbox** при рендеринге HTML с Aspose.HTML for Java? Возможно, вы столкнулись с проблемой имитации конкретного размера экрана или захотели подменить строку user‑agent, чтобы страница вела себя так, как будто её открывает мобильный браузер.  

Хорошая новость: API sandbox позволяет сделать именно это, а также получить вычисленный размер viewport после загрузки страницы. В этом руководстве мы пройдемся по созданию sandbox, установке размеров, задаванию пользовательского user agent, загрузке удалённой страницы и, наконец, чтению размеров viewport. К концу вы будете знать **как задать размер**, **как получить viewport** и почему эти шаги важны для надёжного безголового рендеринга.

> **Быстрый результат:** вы получите исполняемый Java‑класс, который за секунды выведет что‑то вроде `Viewport: 1280×800`.

---

## Что понадобится

- **Aspose.HTML for Java** версии 24.6 или новее (используемый API появился в 24.5).  
- Набор разработки Java 17+ (подойдёт любой современный JDK).  
- IDE или простой текстовый редактор — никаких специальных плагинов не требуется.  
- Доступ в Интернет, если хотите загрузить внешний URL, например `https://example.com`.

И всё. Maven/Gradle не обязателен; при желании можно просто добавить JAR‑файлы в classpath вручную.  

---

## Как использовать Sandbox – Обзор

Sandbox изолирует движок рендеринга от ОС‑хоста, позволяя задать виртуальный экран (ширина, высота, DPI) и пользовательскую строку **user agent**. Представьте его как миниатюрное окно браузера, полностью живущее в памяти. Когда позже вы запрашиваете у `HTMLDocument` его представление по умолчанию, движок сообщает **размер viewport**, рассчитанный на основе настроек sandbox.  

Ниже схематичный поток:

1. **Создать** `DocumentSandbox` и настроить ширину, высоту, DPI и user‑agent.  
2. **Загрузить** `HTMLDocument` внутри этого sandbox.  
3. **Запросить** у документа представление по умолчанию, чтобы получить размер viewport.  

Перейдём к каждому шагу.

---

## Шаг 1: Создать Sandbox и задать размер

Сначала создаём sandbox и указываем, каким должен быть виртуальный экран. Здесь вы отвечаете на вопрос **как задать размер** для безголового рендеринга.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Совет:** если тестируете адаптивный макет, попробуйте узкую ширину, например `360`, чтобы эмулировать телефон, или широкую, например `1920`, для десктопа. Sandbox учитывает установленный DPI, поэтому экран с высокой плотностью (например, 144 DPI) будет влиять на media‑queries, использующие `device-pixel-ratio`.

---

## Шаг 2: Задать User Agent для Sandbox

Зачем нужен пользовательский **user agent**? Некоторые сайты отдают разный markup или скрипты в зависимости от объявленного браузера. Вызвав `setUserAgent`, вы можете заставить страницу думать, что её открывает Chrome, Firefox или мобильное устройство.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Теперь страница будет думать, что её рендерит iPhone. Если нужно **задать user agent** обратно к умолчанию, просто используйте строку “AsposeHTML/24.6 …”, которую использовали ранее.

---

## Шаг 3: Загрузить HTML‑документ внутри Sandbox

Когда sandbox готов, можно загрузить любой URL или локальный HTML‑файл. Конструктор `HTMLDocument` принимает sandbox вторым аргументом, связывая их вместе.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

Блок `try‑with‑resources` гарантирует корректное освобождение документа, освобождая нативные ресурсы, которые Aspose.HTML выделяет под капотом.

---

## Шаг 4: Получить размер Viewport из документа

Вот момент, которого вы ждали: получение **размера viewport**, вычисленного движком рендеринга. Это отвечает на вопрос **как получить viewport** после разметки страницы.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

При запуске программы вы должны увидеть что‑то вроде:

```
Viewport: 1280×800
```

Если вы изменили размеры sandbox в Шаге 1, напечатанные числа отразят новые значения — идеальный способ автоматических тестов, проверяющих точки перелома адаптивного дизайна.

---

## Полный рабочий пример

Ниже полностью готовый к запуску класс, объединяющий все части. Скопируйте его в файл `SandboxExample.java`, добавьте JAR‑файлы Aspose.HTML в classpath и выполните `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Ожидаемый вывод** (при указанных выше настройках sandbox):

```
Viewport: 1280×800
```

Если задать другую ширину/высоту в sandbox, вывод изменится соответственно — именно то, что нужно при тестировании адаптивных дизайнов.

---

## Пограничные случаи и часто задаваемые вопросы

### Что если страница использует `window.innerWidth` вместо CSS‑медиа‑запросов?

Виртуальный размер экрана sandbox влияет как на CSS‑разметку, так и на JavaScript‑значения `window.innerWidth/innerHeight`. Поэтому **как получить viewport** через JavaScript вернёт те же числа, что и в консоли Java.

### Можно ли запускать несколько sandbox‑ов параллельно?

Да. Каждый экземпляр `DocumentSandbox` независим, поэтому можно создать пул потоков, дать каждому свой sandbox с разными размерами и рендерить десятки страниц одновременно. Только помните, что JAR‑файлы потокобезопасны (они таковыми являются).

### Влияет ли настройка DPI на масштабирование изображений?

Однозначно. Более высокий DPI заставляет один CSS‑пиксель соответствовать большему количеству физических пикселей, из‑за чего изображения высокого разрешения выглядят более чёткими. Если тестируете ретина‑стиль ресурсы, попробуйте `sandbox.setDeviceDpi(144)`.

### Как обрабатывать HTTPS‑сертификаты, которые являются самоподписанными

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}