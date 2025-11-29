---
date: 2025-11-29
description: Узнайте, как конвертировать HTML в XPS и регулировать размер страницы
  XPS с помощью Aspose.HTML для Java. Легко контролируйте размеры вывода.
language: ru
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Преобразовать HTML в XPS и изменить размер страницы XPS с помощью Aspose.HTML
  для Java
url: /java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование HTML в XPS и настройка размера страницы XPS с помощью Aspose.HTML для Java

В этом руководстве вы узнаете **как преобразовать HTML в XPS** и точно настроить размер полученной страницы с помощью Aspose.HTML для Java. Независимо от того, создаёте ли вы печатные отчёты, счета‑фактуры или архивные документы, контроль размеров XPS гарантирует, что результат будет выглядеть точно так, как вы ожидаете. Мы пройдём каждый шаг — от настройки окружения до рендеринга окончательного XPS‑файла — чтобы вы могли сразу интегрировать эту возможность в свои Java‑приложения.

## Быстрые ответы
- **Что означает «преобразовать HTML в XPS»?** Он рендерит HTML‑документ в файл XPS, сохраняющий макет и стили.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для разработки; коммерческая лицензия требуется для продакшн.  
- **Какая версия Java поддерживается?** Java 8 или выше (рекомендовано JDK 11+).  
- **Можно ли изменить размер страницы?** Да — Aspose.HTML позволяет задать пользовательские размеры перед рендерингом.  
- **Сколько времени занимает конвертация?** Обычно менее секунды для стандартных страниц; более крупные документы могут занять больше времени.

## Что такое преобразование HTML в XPS?
Преобразование HTML в XPS означает взятие веб‑ориентированного файла разметки и создание документа XPS (XML Paper Specification) — фиксированного, готового к печати формата, похожего на PDF. Это полезно, когда требуются высококачественные, независимые от устройства документы для архивирования или печати из Java‑приложений.

## Почему стоит настраивать размер страницы XPS?
Настройка размера страницы даёт вам контроль над физическими размерами конечного документа (например, A4, Letter, пользовательские этикетки). Это предотвращает нежелательное масштабирование, гарантирует точное размещение содержимого и может уменьшить размер файла, устранив лишние пустые области.

## Требования

Перед началом убедитесь, что у вас есть следующие требования:

1. **Среда разработки Java** — установленный Java Development Kit (JDK) на вашей системе.  
2. **Библиотека Aspose.HTML for Java** — скачайте и подключите библиотеку Aspose.HTML for Java в ваш проект. Вы можете найти библиотеку [здесь](https://releases.aspose.com/html/java/).  
3. **Входной HTML‑файл** — подготовьте HTML‑файл, который вы хотите отрендерить и настроить размер страницы XPS. Вы можете использовать свой собственный HTML‑файл для этого руководства.

## Импорт пакетов

Сначала импортируйте необходимые классы. Эти пакеты предоставляют доступ к работе с документами, рендерингу и настройкам страниц.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Шаг 1: Установите имя входного файла

Прочитайте исходный HTML‑файл с помощью `FileInputStream`. Этот поток передаёт необработанный HTML в движок Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## Шаг 2: Создайте HTML‑документ и задайте стили

Создайте экземпляр `HTMLDocument`, представляющий содержимое, которое будет отрендерено. В этом примере мы также внедряем небольшой блок CSS для демонстрации стилей — при желании замените его своей разметкой.

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

## Шаг 3: Создайте параметры рендеринга XPS

Создайте экземпляр `XpsRenderingOptions`, который будет хранить все настройки, влияющие на преобразование HTML в XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## Шаг 4: Настройте размер страницы

Задайте пользовательский размер страницы (ширина × высота в пунктах) и укажите рендереру, следует ли автоматически расширяться до самой широкой страницы. Установка `adjustToWidestPage` в `false` сохраняет точные указанные вами размеры.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## Шаг 5: Сгенерируйте вывод

Наконец, создайте `XpsDevice` с настроенными параметрами и отрендерите HTML‑документ. В результате получится полностью сформированный XPS‑файл с пользовательскими размерами страниц, которые вы задали.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Распространённые проблемы и решения

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Пустой XPS‑вывод** | Поток ввода не закрыт или `HTMLDocument` указывает на неверный файл. | Убедитесь, что `FileInputStream` правильно обёрнут в блок try‑with‑resources и путь к файлу точный. |
| **Размер страницы не применён** | `adjustToWidestPage` оставлен как `true`. | Установите `pageSetup.setAdjustToWidestPage(false);` как показано в Шаге 4. |
| **Неподдерживаемый CSS** | Aspose.HTML поддерживает подмножество CSS. | Используйте базовый макет, шрифты и цвета; избегайте сложных селекторов или CSS Grid. |
| **LicenseException** | Запуск без действующей лицензии в продакшн. | Примените временную или приобретённую лицензию перед рендерингом (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Часто задаваемые вопросы

**В: Что такое Aspose.HTML for Java?**  
О: Aspose.HTML for Java — это Java‑библиотека, позволяющая разработчикам манипулировать и конвертировать HTML‑документы в различные форматы, такие как XPS, PDF и изображения.

**В: Где можно скачать Aspose.HTML for Java?**  
О: Вы можете скачать библиотеку Aspose.HTML for Java по [этой ссылке](https://releases.aspose.com/html/java/).

**В: Доступна ли бесплатная пробная версия Aspose.HTML for Java?**  
О: Да, вы можете получить бесплатную пробную версию Aspose.HTML for Java [здесь](https://releases.aspose.com/).

**В: Как получить временную лицензию для Aspose.HTML for Java?**  
О: Чтобы получить временную лицензию для Aspose.HTML for Java, посетите [эту страницу](https://purchase.aspose.com/temporary-license/).

**В: Можно ли получить поддержку для Aspose.HTML for Java?**  
О: Да, вы можете обратиться за помощью и поддержкой к сообществу Aspose на [форуме Aspose](https://forum.aspose.com/).

**В: Можно ли конвертировать HTML в XPS на сервере без графического интерфейса?**  
О: Абсолютно. Aspose.HTML работает в средах без GUI; просто убедитесь, что Java‑runtime правильно сконфигурирован.

**В: Поддерживает ли библиотека пользовательские поля страницы?**  
О: Да. Используйте `PageSetup.setMarginTop()`, `setMarginBottom()` и т.д., перед тем как назначить `PageSetup` в параметры рендеринга.

## Заключение

Мы прошли полный процесс **преобразования HTML в XPS** и настройки размера страницы с помощью Aspose.HTML for Java. Следуя этим шагам, вы сможете генерировать готовые к печати XPS‑документы, соответствующие вашим точным требованиям к макету. Не стесняйтесь экспериментировать с различными размерами страниц, стилями или даже добавлять заголовки и колонтитулы, чтобы удовлетворить потребности вашего проекта.

Если у вас есть вопросы или нужна дополнительная помощь, изучите [документацию Aspose.HTML for Java](https://reference.aspose.com/html/java/) или присоединитесь к обсуждению на [форуме Aspose](https://forum.aspose.com/).

---

**Последнее обновление:** 2025-11-29  
**Тестировано с:** Aspose.HTML for Java 24.11 (последняя версия на момент написания)  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}