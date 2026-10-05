---
category: general
date: 2026-02-22
description: Установите коэффициент пикселей устройства в Java с помощью песочницы
  Aspose.HTML. Узнайте, как задать пользовательский агент, получить заголовок страницы
  в Java и конвертировать HTML в PNG в одном руководстве.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: ru
og_description: Установите коэффициент пикселей устройства в Java с использованием
  песочницы Aspose.HTML. Этот учебник показывает, как задать пользовательский агент,
  получить заголовок страницы в Java и конвертировать HTML в PNG.
og_title: Установка коэффициента пикселей устройства в Java — Полное руководство
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Установка коэффициента пикселей устройства в Java – Полное руководство
url: /ru/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Установка коэффициента пикселей устройства в Java – Полное руководство

Когда‑то задумывались, как **установить коэффициент пикселей устройства** при рендеринге веб‑страницы из Java? Вы не одиноки. Многие разработчики хотят эмулировать экраны мобильных устройств с высоким DPI, чтобы скриншоты выглядели чётко, особенно когда позже **сохраняют html как изображение** для отчётов или маркетинговых материалов. В этом руководстве мы пройдём через практический пример, который делает именно это — а также покажем, как **установить пользовательский user agent**, **получить заголовок страницы java**, и **конвертировать html в png** с помощью Aspose.HTML.

Сначала мы кратко рассмотрим API песочницы, затем подробно разберём каждый шаг настройки и, наконец, создадим PNG‑файл, который будет соответствовать реальному дисплею iPhone. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой Java‑проект. Никаких внешних инструментов не требуется, только чистый Java и Aspose.HTML 7.x (или новее).

---

## Требования

- Java 17 или новее (код компилируется и в более ранних версиях, но рекомендуется 17).
- Библиотека Aspose.HTML for Java (скачайте с официального сайта Aspose; координаты Maven: `com.aspose:aspose-html:23.10`).
- IDE или текстовый редактор по вашему выбору (IntelliJ IDEA, VS Code, Eclipse… всё подходит).
- Доступ в Интернет для демонстрационного URL (`https://example.com/responsive.html`), либо замените его любой публичной HTML‑страницей, которой вы владеете.

> **Pro tip:** Если вы работаете за прокси, настройте системные свойства JVM `http.proxyHost` и `http.proxyPort` перед запуском кода.

---

## Шаг 1: Установка коэффициента пикселей устройства и других параметров песочницы

Первым делом нам нужен экземпляр **SandboxOptions**, где мы задаём виртуальный размер экрана и *коэффициент пикселей устройства* (DPR). DPR — это фактор, который сообщает браузеру, сколько физических пикселей соответствует одному CSS‑пикселю. На Retina‑iPhone DPR обычно **2.0**, поэтому мы будем использовать именно это значение.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Почему это важно:** Если не задать правильный DPR, полученное изображение будет размытым или слишком большим, потому что растеризатор предполагает соответствие 1:1 пикселей.

---

## Шаг 2: Установка пользовательского User Agent

Сайты часто отдают разный markup в зависимости от заголовка **User‑Agent**. Чтобы наша страница вела себя так же, как на реальном iPhone, мы внедряем пользовательскую строку, имитирующую Safari на iOS.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Особый случай:** Некоторые сайты также проверяют заголовок `Accept-Language`. Если вы заметили отсутствие переводов, добавьте `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");`.

---

## Шаг 3: Загрузка страницы в песочницу и получение заголовка

Теперь мы создаём песочницу с только что определёнными параметрами. Объект **Sandbox** изолирует процесс рендеринга, гарантируя, что наши настройки DPR и user‑agent будут применены.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

После загрузки страницы получить заголовок так же просто, как вызвать `getTitle()`. Это удовлетворяет требованию **get page title java**.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Ожидаемый вывод в консоль**

```
Title: Responsive Demo – Mobile View
```

Если заголовок пустой, проверьте URL или убедитесь, что страница не блокируется политиками CORS.

---

## Шаг 4: Конвертация HTML в PNG и сохранение HTML как изображения

Aspose.HTML позволяет напрямую рендерить DOM в файл изображения. Поскольку мы уже задали DPR = 2.0, полученный PNG будет иметь двойную плотность пикселей, давая чёткий скриншот.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

Метод `save` автоматически определяет расширение файла и выбирает соответствующий рендерер. Если нужен другой формат (JPEG, BMP), просто измените имя файла.

> **А если нужен конкретный размер изображения?**  
> Используйте `ImageSaveOptions` для управления шириной, высотой и цветом фона:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

---

## Полный рабочий пример

Ниже приведена полностью готовая к запуску программа, объединяющая все шаги. Скопируйте её в файл `SandboxDemo.java`, добавьте зависимость Aspose.HTML и выполните `java SandboxDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

Запуск программы создаёт два PNG‑файла:

| Файл | Описание |
|------|----------|
| `mobile_view.png` | Рендеринг по умолчанию с настроенным DPR. |
| `mobile_view_custom.png` | Рендеринг с явно заданными шириной/высотой (полезно для фиксированных активов). |

Откройте любой из файлов в просмотрщике изображений, чтобы убедиться в высоком разрешении вывода.

---

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|--------|-------|
| **Что делать, если страница содержит JavaScript, изменяющий DOM после загрузки?** | Aspose.HTML по умолчанию исполняет скрипты. Если нужен статический снимок до выполнения скриптов, установите `sandboxOptions.setEnableJavaScript(false)`. |
| **Можно ли рендерить страницу, требующую аутентификации?** | Да. Используйте `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` или внедрите cookies через `sandboxOptions.getCookies().add(...)`. |
| **Ограничен ли DPR значением 2.0?** | Нет. Можно задать любое положительное число с плавающей точкой (например, 3.0 для ультра‑высоких DPI). Учтите, что больший DPR приводит к большим файлам изображений. |
| **Как работать со страницами, содержащими крупные ресурсы (изображения, шрифты)?** | Увеличьте лимит памяти песочницы: `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (в байтах). Это предотвратит ошибки out‑of‑memory на тяжёлых страницах. |
| **Нужно ли закрывать песочницу вручную?** | Класс `Sandbox` реализует `AutoCloseable`. Оберните его в блок `try‑with‑resources` для автоматической очистки. |

---

## Заключение

Мы продемонстрировали, как **установить коэффициент пикселей устройства** в Java‑песочнице, **задать пользовательский user agent**, **получить заголовок страницы java** и **конвертировать html в png** (фактически **сохранить html как изображение**) с помощью Aspose.HTML. Полный пример показывает практический рабочий процесс, который можно адаптировать для автоматической генерации скриншотов, визуального регрессионного тестирования или любой задачи, требующей пиксель‑точного представления веб‑страницы.

Экспериментируйте — изменяйте DPR на 3.0, подставляйте user‑agent для Android, или указывайте локальный HTML‑файл. Та же схема работает с PDF, SVG и даже многостраничным рендерингом.

Если это руководство оказалось полезным, изучите связанные темы, такие как **генерация PDF с Aspose.HTML**, **альтернативы headless Chrome** или **пакетный рендеринг нескольких URL**. Приятного кодинга, и пусть ваши скриншоты всегда будут кристально‑чёткими! 

![установка коэффициента пикселей устройства в Java sandbox](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}