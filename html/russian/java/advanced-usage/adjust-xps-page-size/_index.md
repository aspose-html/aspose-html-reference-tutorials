---
date: 2026-03-18
description: Узнайте, как конвертировать HTML в XPS и регулировать размер страницы
  XPS с помощью Aspose.HTML для Java. Легко контролируйте размеры вывода.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Преобразовать HTML в XPS и изменить размер страницы XPS с помощью Aspose.HTML
  для Java
url: /ru/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Конвертировать HTML в XPS и изменить размер страницы XPS с помощью Aspose.HTML для Java

В этом руководстве вы узнаете **как конвертировать HTML в XPS** и точно настроить размер полученной страницы, используя Aspose.HTML для Java. Независимо от того, создаёте ли вы печатные отчёты, счета‑фактуры или архивные документы, контроль над размерами XPS‑файла гарантирует, что вывод будет выглядеть именно так, как вы ожидаете. Мы пройдём каждый шаг — от настройки окружения до рендеринга окончательного XPS‑файла — чтобы вы могли сразу внедрить эту возможность в свои Java‑приложения.

## Быстрые ответы
- **Что означает “convert HTML to XPS”?** Это рендеринг HTML‑документа в XPS‑файл с сохранением макета и стилей.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для разработки; для продакшна требуется коммерческая лицензия.  
- **Какая версия Java поддерживается?** Java 8 или выше (рекомендовано JDK 11+).  
- **Можно ли изменить размер страницы?** Да — Aspose.HTML позволяет задать пользовательские размеры перед рендерингом.  
- **Сколько времени занимает конвертация?** Обычно менее секунды для стандартных страниц; более крупные документы могут занимать дольше.

## Что означает конвертация HTML в XPS?
Конвертация HTML в XPS подразумевает преобразование веб‑ориентированного файла разметки в документ XPS (XML Paper Specification) — фиксированный, готовый к печати формат, похожий на PDF. Это полезно, когда нужны высококачественные, независимые от устройства документы для архивирования или печати из Java‑приложений.

## Зачем изменять размер страницы XPS?
Настройка размера страницы даёт вам контроль над физическими размерами конечного документа (например, A4, Letter, пользовательские этикетки). Это предотвращает нежелательное масштабирование, обеспечивает точное размещение содержимого и может уменьшить размер файла, устранив лишние пустые области.

## Предварительные требования

Перед началом убедитесь, что у вас есть следующее:

1. **Среда разработки Java** — установленный Java Development Kit (JDK).  
2. **Библиотека Aspose.HTML для Java** — скачайте и подключите её к вашему проекту. Библиотеку можно найти [здесь](https://releases.aspose.com/html/java/).  
3. **Исходный HTML‑файл** — подготовьте HTML‑файл, который вы хотите отрендерить и настроить размер страницы XPS. Вы можете использовать любой свой HTML‑файл для этого руководства.

## Импорт пакетов

Сначала импортируйте необходимые классы. Эти пакеты дают доступ к работе с документами, рендерингу и настройкам страниц.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Пошаговое руководство

Ниже представлена краткая нумерованная последовательность шагов, отражающая оригинальные действия и дополненная пояснениями для лучшего понимания.

### Шаг 1: Установить имя входного файла

Прочитайте исходный HTML‑файл с помощью `FileInputStream`. Этот поток передаёт необработанный HTML в движок Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Шаг 2: Создать HTML‑документ и задать стили

Создайте экземпляр `HTMLDocument`, представляющий содержимое, которое будет рендериться. В этом примере мы также внедряем небольшой блок CSS для демонстрации стилей — замените его на свою разметку при необходимости.

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

### Шаг 3: Создать параметры рендеринга XPS

Создайте объект `XpsRenderingOptions`, который будет хранить все настройки, влияющие на конвертацию из HTML в XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Шаг 4: Настроить размер страницы  

**Как задать размер страницы XPS** — определите пользовательский размер страницы (ширина × высота в пунктах) и укажите рендереру, следует ли автоматически расширять её до самой широкой страницы. Установка `adjustToWidestPage` в `false` сохраняет точные размеры, которые вы указали.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Шаг 5: Сгенерировать вывод

Наконец, создайте `XpsDevice` с настроенными параметрами и выполните рендеринг HTML‑документа. В результате получится полностью сформированный XPS‑файл с пользовательскими размерами страниц, которые вы задали.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Распространённые проблемы и решения

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Blank XPS output** | Поток ввода не закрыт или `HTMLDocument` указывает на неправильный файл. | Убедитесь, что `FileInputStream` правильно обёрнут в блок `try‑with‑resources`, а путь к файлу указан точно. |
| **Page size not applied** | `adjustToWidestPage` оставлен со значением `true`. | Установите `pageSetup.setAdjustToWidestPage(false);`, как показано в Шаге 4. |
| **Unsupported CSS** | Aspose.HTML поддерживает лишь часть CSS. | Используйте базовые свойства макета, шрифтов и цветов; избегайте сложных селекторов и CSS Grid. |
| **LicenseException** | Запуск без действующей лицензии в продакшн‑среде. | Примените временную или приобретённую лицензию перед рендерингом (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Часто задаваемые вопросы

**Q: Что такое Aspose.HTML для Java?**  
A: Aspose.HTML для Java — это Java‑библиотека, позволяющая разработчикам работать с HTML‑документами и конвертировать их в различные форматы, такие как XPS, PDF и изображения.

**Q: Где можно скачать Aspose.HTML для Java?**  
A: Вы можете скачать библиотеку Aspose.HTML для Java по [этой ссылке](https://releases.aspose.com/html/java/).

**Q: Доступна ли бесплатная пробная версия Aspose.HTML для Java?**  
A: Да, бесплатную пробную версию Aspose.HTML для Java можно получить [здесь](https://releases.aspose.com/).

**Q: Как получить временную лицензию для Aspose.HTML для Java?**  
A: Чтобы получить временную лицензию для Aspose.HTML для Java, посетите [эту страницу](https://purchase.aspose.com/temporary-license/).

**Q: Есть ли поддержка Aspose.HTML для Java?**  
A: Да, вы можете получить помощь и поддержку в сообществе Aspose на [форуме Aspose](https://forum.aspose.com/).

**Q: Можно ли конвертировать HTML в XPS на сервере без графического интерфейса?**  
A: Абсолютно. Aspose.HTML работает в средах без GUI; достаточно правильно настроить Java‑runtime.

**Q: Поддерживает ли библиотека пользовательские отступы страницы?**  
A: Да. Используйте `PageSetup.setMarginTop()`, `setMarginBottom()` и т.д. перед передачей `PageSetup` в параметры рендеринга.

## Заключение

Мы прошли полный процесс **конвертации HTML в XPS** и настройки размера страницы с помощью Aspose.HTML для Java. Следуя этим шагам, вы сможете генерировать готовые к печати XPS‑документы, точно соответствующие вашим требованиям к макету. Экспериментируйте с различными размерами страниц, стилями или добавляйте заголовки и колонтитулы, чтобы адаптировать решение под нужды вашего проекта.

Если у вас возникнут вопросы или потребуется дополнительная помощь, изучите [документацию Aspose.HTML для Java](https://reference.aspose.com/html/java/) или присоединитесь к обсуждению на [форуме Aspose](https://forum.aspose.com/).

---

**Last Updated:** 2026-03-18  
**Tested With:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}