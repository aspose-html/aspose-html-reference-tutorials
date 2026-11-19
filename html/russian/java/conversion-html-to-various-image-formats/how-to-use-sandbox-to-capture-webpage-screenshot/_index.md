---
category: general
date: 2026-03-25
description: Как использовать sandbox для захвата скриншота веб‑страницы с помощью
  Aspose.HTML для Java. Узнайте, как сохранить HTML как PNG, конвертировать HTML в
  изображение и преобразовать HTML в PNG за несколько минут.
draft: false
keywords:
- how to use sandbox
- capture webpage screenshot
- save html as png
- html to image conversion
- html to png conversion
language: ru
og_description: Как использовать песочницу для захвата скриншота веб‑страницы. Этот
  учебник показывает, как сохранить HTML в PNG, охватывая преобразование HTML в изображение
  и преобразование HTML в PNG с помощью Aspose.HTML для Java.
og_title: Как использовать Sandbox для захвата скриншота веб‑страницы
tags:
- Aspose.HTML
- Java
- Web Automation
title: Как использовать Sandbox для захвата скриншота веб‑страницы
url: /ru/java/conversion-html-to-various-image-formats/how-to-use-sandbox-to-capture-webpage-screenshot/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать Sandbox для создания скриншота веб‑страницы

Создание скриншота веб‑страницы в sandbox — частая задача, когда нужен пиксель‑точный предварительный просмотр адаптивной страницы. В этом руководстве мы также покажем, как **сохранить HTML как PNG** с помощью Aspose.HTML for Java, охватывая всё от *преобразования html в изображение* до *преобразования html в png* в одном воспроизводимом примере.

Представьте, что вы тестируете маркетинговую посадочную страницу, которая выглядит по‑разному на телефоне, планшете и настольном компьютере. Вместо того чтобы открывать три браузера, вы можете запустить sandbox, указать ему URL и мгновенно получить PNG, точно соответствующий тому, что отобразит реальное устройство. К концу этого урока у вас будет полностью готовая, исполняемая Java‑программа, делающая именно это, а также несколько практических советов, которые вы сможете использовать в своих проектах.

## Что понадобится

- **Aspose.HTML for Java** (v23.9 или новее). Библиотека доступна через Maven Central, так что добавить зависимость проще простого.  
- **JDK 11+**, установленный на вашем компьютере.  
- IDE или текстовый редактор по вашему выбору (IntelliJ IDEA, VS Code, Eclipse… любой подойдет).  
- Доступ в Интернет для примера URL (`https://example.com/responsive.html`) или замените его любой страницей, которую хотите захватить.

Никаких дополнительных нативных бинарных файлов или безголовых браузеров не требуется — sandbox работает полностью в памяти.

---

## Как использовать Sandbox – Шаг 1: Определить виртуальное устройство

Первое, что нужно сделать, — указать sandbox, какой размер экрана вы хотите эмулировать. Здесь проявляется основной ключевой запрос: *как использовать sandbox* для конкретного viewport.

```java
// Step 1: Create a DeviceInfo that describes the virtual screen
DeviceInfo sandboxDevice = new DeviceInfo();
sandboxDevice.setWidth(800);               // width in pixels
sandboxDevice.setHeight(600);              // height in pixels
sandboxDevice.setDevicePixelRatio(1.0);    // 1 × for standard displays
sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");
```

**Почему это важно:**  
Установка ширины и высоты заставляет движок макета воспринимать страницу так, как если бы она отображалась на мониторе 800×600. Параметр `devicePixelRatio` влияет на то, как работают CSS‑медиа‑запросы (`@media (min‑device‑pixel‑ratio: ...)`), обеспечивая соответствие скриншота реальному опыту.

> **Совет:** Если нужен скриншот с высоким DPI (например, Retina‑дисплеи), увеличьте `devicePixelRatio` до `2.0` и соответственно увеличьте ширину/высоту.

---

## Захват скриншота веб‑страницы – Шаг 2: Загрузить страницу внутри Sandbox

Теперь мы просим Aspose.HTML загрузить удалённый HTML и отрисовать его внутри только что определённого sandbox. Этот шаг — сердце **захвата скриншота веб‑страницы**.

```java
// Step 2: Load the remote HTML page using the sandboxed environment
HTMLDocument document = new HTMLDocument(
        "https://example.com/responsive.html",
        new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));
```

**Что происходит под капотом?**  
`HTMLDocumentLoadOptions` получает экземпляр `Sandbox`, содержащий наш `DeviceInfo`. Библиотека затем создаёт безголовый контекст рендеринга, который учитывает viewport, строку user‑agent и любой JavaScript, который может выполнить страница — *всё без запуска Chrome или Firefox*.

Если целевая страница требует аутентификации, вы можете добавить cookies или пользовательские заголовки через `HTMLDocumentLoadOptions`. Это полезный сценарий, когда вы работаете с интранет‑порталами.

---

## Сохранить HTML как PNG – Шаг 3: Преобразовать отрендеренный документ в изображение

После рендеринга страницы последний шаг — **сохранить HTML как PNG**. Это фактический этап *преобразования html в png*.

```java
// Step 3: Convert the rendered document to PNG and write it to disk
try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
    Converter.convertDocument(
            document,
            new ConversionOptions(ConversionFormat.PNG),
            out);
}
```

Когда `Converter` завершит работу, вы найдёте файл `responsive_page.png` в папке `output`. Откройте его, и вы увидите точно то, как страница выглядела при 800×600 пикселях — без UI браузера, без полос прокрутки, только чистый рендер.

**Распространённые подводные камни:**  
- **Ошибки доступа к файлам:** Убедитесь, что каталог существует (`output/` в примере) и ваш процесс имеет право записывать в него.  
- **Большие страницы:** Очень длинные страницы могут создавать огромные PNG‑файлы; вы можете ограничить высоту в `DeviceInfo` или обрезать изображение после конвертации.  
- **Динамический контент:** Если страница загружает данные через AJAX после первоначальной загрузки, возможно, понадобится небольшая задержка (`Thread.sleep(2000)`) перед конвертацией, либо использовать `HTMLDocumentLoadOptions.setWaitForResources(true)`.

---

### Преобразование html в изображение – Расширенные параметры

Aspose.HTML предлагает несколько настроек, позволяющих точно настроить **преобразование html в изображение**:

| Опция | Описание | Когда использовать |
|--------|-------------|-------------|
| `ConversionOptions.setQuality(int)` | Устанавливает уровень сжатия PNG (0‑100). | Сократить размер файла для веб‑активов. |
| `ConversionOptions.setBackgroundColor(Color)` | Принудительно задаёт цвет фона (по умолчанию прозрачный). | Полезно, когда на странице есть прозрачные участки. |
| `ConversionOptions.setPageSize(PageSize)` | Переопределяет размер sandbox для выходного изображения. | Создание миниатюр другого разрешения. |

Ниже короткий фрагмент, который задаёт белый фон и качество 90 %:

```java
ConversionOptions pngOptions = new ConversionOptions(ConversionFormat.PNG);
pngOptions.setBackgroundColor(java.awt.Color.WHITE);
pngOptions.setQuality(90);

try (FileOutputStream out = new FileOutputStream("output/white_bg_page.png")) {
    Converter.convertDocument(document, pngOptions, out);
}
```

---

## Полный рабочий пример

Объединив всё вместе, получаем полную программу, которую можно скопировать в файл `SandboxResponsiveExample.java` и запустить:

```java
import com.aspose.html.devices.DeviceInfo;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.ConversionOptions;
import com.aspose.html.converters.ConversionFormat;
import com.aspose.html.render.HTMLDocument;
import com.aspose.html.render.HTMLDocumentLoadOptions;
import com.aspose.html.render.Sandbox;

import java.io.FileOutputStream;

public class SandboxResponsiveExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Define a sandbox with the desired viewport (800×600) and device pixel ratio
        DeviceInfo sandboxDevice = new DeviceInfo();
        sandboxDevice.setWidth(800);
        sandboxDevice.setHeight(600);
        sandboxDevice.setDevicePixelRatio(1.0);
        sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");

        // Step 2: Load the remote HTML page inside the sandboxed environment
        HTMLDocument document = new HTMLDocument(
                "https://example.com/responsive.html",
                new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));

        // Step 3: Convert the document to PNG – the output reflects exactly how the page looks on the defined screen size
        try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
            Converter.convertDocument(
                    document,
                    new ConversionOptions(ConversionFormat.PNG),
                    out);
        }

        System.out.println("Screenshot saved to output/responsive_page.png");
    }
}
```

Запуск программы выводит строку подтверждения и сохраняет PNG в папку `output`. Откройте файл, и вы увидите точную копию удалённой страницы в указанном размере.

---

## Часто задаваемые вопросы

**В: Работает ли это с локальными HTML‑файлами?**  
О: Конечно. Замените URL на URI `file://` или передайте путь `java.io.File` в конструктор `HTMLDocument`.

**В: Что если нужен PDF вместо PNG?**  
О: Замените `ConversionFormat.PNG` на `ConversionFormat.PDF`. Остальной код остаётся без изменений.

**В: Можно ли захватить скриншот полной страницы (со скроллом)?**  
О: Установите высоту `DeviceInfo` равной высоте прокрутки страницы (`document.getDocumentElement().getScrollHeight()`) перед конвертацией, либо используйте `ConversionOptions.setPageSize`, чтобы увеличить канвас.

---

## Заключение

Теперь вы знаете, **как использовать sandbox** для захвата скриншота веб‑страницы, сохранения HTML как PNG и надёжного преобразования html в изображение с помощью Aspose.HTML for Java. Этот подход лёгок, полностью программируем и обходится без накладных расходов традиционных безголовых браузеров.

**Что дальше?** Попробуйте заменить вывод PNG на PDF, поэкспериментировать с различными коэффициентами `devicePixelRatio`, чтобы имитировать Retina‑дисплеи, или автоматизировать пакетную обработку десятков URL. Тот же приём sandbox можно также использовать для **преобразования html в png** в CI‑конвейерах, визуальном регрессионном тестировании или генерации миниатюр для системы управления контентом.

Не стесняйтесь оставлять комментарии, если возникнут проблемы, и счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}