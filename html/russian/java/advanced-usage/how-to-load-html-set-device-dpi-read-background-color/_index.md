---
category: general
date: 2026-02-16
description: Как загрузить HTML в Java, установить DPI устройства, задать виртуальный
  размер экрана и получить вычисленный цвет фона любого элемента.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: ru
og_description: Как загрузить HTML в Java, установить DPI устройства, задать виртуальный
  размер экрана и получить вычисленный цвет фона любого элемента.
og_title: Как загрузить HTML, установить DPI устройства и прочитать цвет фона
tags:
- Aspose.HTML
- Java
title: Как загрузить HTML, установить DPI устройства и прочитать цвет фона
url: /ru/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как загрузить HTML, установить DPI устройства и прочитать цвет фона

Когда‑нибудь задавались вопросом **как загрузить html** в Java‑приложении и затем проанализировать стили страницы? Вы не одиноки — разработчикам часто нужно отрисовать веб‑страницу вне экрана, получить окончательные значения CSS и использовать их для конвертации в PDF, скриншотов или даже автоматических тестов.  

В этом руководстве мы пройдем всё это шаг за шагом: загрузим HTML‑файл, **установим DPI устройства**, определим **виртуальный размер экрана** и, наконец, **прочитаем цвет фона** из элемента `<body>`. К концу у вас будет полностью рабочий фрагмент кода, который выводит **вычисленный цвет фона** — без загадок, просто Java.

## Что понадобится

* Java 17 или новее (код работает с любой современной JDK).  
* Aspose.HTML for Java 23.9 или новее — скачайте JAR с сайта Aspose или добавьте его через Maven.  
* Простой HTML‑файл (например, `responsive.html`), в котором в CSS задаётся цвет фона.

Вот и всё — никаких дополнительных фреймворков, никаких драйверов браузера. Готовы? Приступим.

![Диаграмма, показывающая как загрузить html и извлечь вычисленные стили](/images/load-html-diagram.png){alt="Диаграмма, показывающая как загрузить html и извлечь вычисленные стили"}

## Шаг 1: Как загрузить HTML и настроить параметры рендеринга

Первое, что вы делаете, — создаёте объект `HtmlLoadOptions`. Этот объект сообщает Aspose.HTML **как загрузить html** — включая размеры виртуального экрана и DPI, которые вы хотите эмулировать.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Почему это важно:**  
Установка виртуального размера экрана гарантирует, что медиа‑запросы вроде `@media (max-width: 600px)` работают так, как если бы страница отрисовывалась на реальном мониторе. DPI влияет на то, как единицы CSS `px` сопоставляются с физическими пикселями — это критично, когда вы позже генерируете изображения или PDF.

## Шаг 2: Загрузить HTML‑файл, используя настроенные параметры

Теперь мы действительно загружаем файл. Обратите внимание, что мы передаём те же `loadOptions`, которые только что настроили.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Если файл не найден, Aspose бросает понятный `FileNotFoundException`. В продакшене вы, возможно, захотите обернуть это в try‑catch и использовать строку HTML по умолчанию.

## Шаг 3: Установить виртуальный размер экрана и DPI устройства (явно)

Хотя мы уже вызвали `setScreenSize` и `setDeviceDpi` выше, стоит отметить, что **установить виртуальный размер экрана** и **установить DPI устройства** можно изменить в любой момент до рендеринга. Например, вы можете увеличить DPI для скриншотов высокого разрешения:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Не забудьте перезагрузить документ, если измените эти настройки после первой загрузки — Aspose рассматривает их как неизменные после создания `Document`.

## Шаг 4: Прочитать цвет фона и получить вычисленный цвет фона

Имея документ в памяти, вы можете запросить вычисленный стиль любого элемента. Здесь мы сосредоточимся на теге `<body>`, но тот же подход работает для `<div>`, `<p>` или даже псевдо‑элементов.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**Что вы увидите:** Если `responsive.html` содержит `body { background: #ff5722; }`, консоль выведет что‑то вроде:

```
Computed background color: rgba(255,87,34,1)
```

Это результат **получения вычисленного цвета фона** — Aspose разрешает все правила каскада CSS, медиа‑запросы и даже объявления `!important` перед тем, как вернуть окончательное значение.

## Полный рабочий пример

Объединив всё вместе, представляем полностью готовую к копированию программу:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Ожидаемый вывод

```
Computed background color: rgba(255,255,255,1)
```

*(Точные значения RGBA зависят от CSS в вашем HTML‑файле.)*

## Распространённые подводные камни и профессиональные советы

* **Отсутствует настройка DPI?** По умолчанию Aspose использует 96 DPI, что может размыть скриншоты высокого разрешения. Всегда задавайте её явно, если нужен чёткий вывод.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}