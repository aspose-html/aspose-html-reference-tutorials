---
date: 2026-04-05
description: Узнайте, как генерировать PDF из HTML, настраивать шрифты, применять
  пользовательский CSS, использовать временную лицензию и конвертировать HTML в PDF
  на Java с Aspose.HTML.
keywords:
- generate pdf from html
- convert html pdf java
- add custom fonts pdf
- fonts not showing pdf
linktitle: Настройка шрифтов в Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: 'Создание PDF из HTML: настройка шрифтов с помощью Aspose.HTML для Java'
url: /ru/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Настройка шрифтов для HTML‑to‑PDF Java с Aspose.HTML

## Введение
В этом руководстве вы узнаете, как **generate PDF from HTML** с помощью Aspose.HTML и как настроить шрифты для конвертации HTML‑to‑PDF в Java. При работе с HTML‑документами правильная настройка шрифтов гарантирует, что сгенерированный PDF будет выглядеть точно так же, как оригинальная веб‑страница — сохранятся фирменные цвета, типографика и макет. Независимо от того, создаёте ли вы отчёты, счета‑фактуры или любой конвейер генерации документов, правильная конфигурация шрифтов — ключ к профессиональному виду PDF. Давайте пройдём весь процесс от подготовки окружения до конвертации HTML в PDF с пользовательскими шрифтами и CSS.

## Быстрые ответы
- **What is the primary purpose of this tutorial?** Настроить шрифты для конвертации HTML‑to‑PDF в Java с использованием Aspose.HTML.  
- **Which library handles the conversion?** Aspose.HTML for Java (класс `Converter`).  
- **Do I need a license?** Временная лицензия Aspose снимает ограничения оценки; полная лицензия требуется для продакшн.  
- **Where should my custom fonts be placed?** В папке, указанной в `FontsLookupFolder`, например, в каталоге `fonts` рядом с вашим проектом.  
- **Can I customize PDF output?** Да — используйте `PdfSaveOptions` для настройки размера страницы, полей и прочего.

## Что такое **generate PDF from HTML** и почему конфигурация шрифтов важна?
Процесс **generate PDF from HTML** преобразует HTML‑документ в страницу PDF. Шрифты играют ключевую роль в рендеринге, так как они влияют на макет, межстрочный интервал и визуальное соответствие. Указывая Aspose.HTML на папку с пользовательскими шрифтами, вы гарантируете, что PDF будет использовать именно те типографские наборы, которые вы задали для веб‑страницы, исключая резервные шрифты и сохраняя фирменную консистентность.

## Почему использовать Aspose.HTML для конфигурации шрифтов?
- **Accurate rendering:** Поддерживает CSS2.1 и многие возможности CSS3, поэтому ваш HTML выглядит одинаково в PDF.  
- **Cross‑platform:** Работает на любой ОС, где запущен Java 1.8+.  
- **License flexibility:** Тестируйте с временной лицензией, затем переключитесь на полную лицензию для продакшн.  
- **Performance:** Быстрая конверсия даже для сложных страниц.

## Предварительные требования
Перед началом убедитесь, что у вас есть следующее:

1. **Java Development Kit (JDK) 1.8+** – код работает на любой современной JDK.  
2. **Aspose.HTML for Java** – загрузите последнюю JAR с [Aspose website](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse или любой совместимый с Java редактор.  
4. **Basic Java knowledge** – вы должны быть уверены в работе с классами, методами и вводом/выводом файлов.  
5. **Aspose.HTML license** – [temporary license](https://purchase.aspose.com/temporary-license/) снимет ограничения оценки.

## Импорт пакетов
Сначала импортируйте основные классы Java и Aspose.HTML, которые вам понадобятся.  

```java
import java.io.IOException;
```

Эти импорты дают вам доступ к работе с файлами и API Aspose.HTML.

## Как добавить пользовательские шрифты при генерации PDF
Ниже мы объясним, почему важна работа со шрифтами, как применить пользовательский CSS и как **use a temporary license** чтобы разблокировать полную функциональность во время тестирования решения.

## Пошаговое руководство

### Шаг 1: Создать HTML‑контент
Мы начнём с создания простого HTML‑файла, который позже преобразуем в PDF.

#### 1.1 Написать HTML‑код
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

Этот фрагмент определяет заголовок и абзац. При желании можете расширить HTML дополнительными элементами, если нужно протестировать другие стили.

#### 1.2 Сохранить HTML в файл
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

`FileWriter` записывает строку в `user-agent-fontsetting.html` в папке вашего проекта. После этого шага у вас будет физический HTML‑файл, готовый к обработке.

### Шаг 2: Настроить окружение Aspose.HTML
Теперь настроим объект `Configuration` Aspose.HTML, который позволяет контролировать, как рендерится HTML.

#### 2.1 Создать экземпляр Configuration
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

Объект `Configuration` является точкой входа для настройки параметров рендеринга, таких как работа со шрифтами и поведение пользовательского агента.

#### 2.2 Доступ к сервису User Agent
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

`IUserAgentService` управляет таблицами стилей, шрифтами и другими деталями рендеринга. Мы будем использовать его для внедрения пользовательского CSS и указания папки со шрифтами.

### Шаг 3: Применить пользовательские стили и шрифты
С готовым окружением мы можем добавить правила CSS и указать Aspose.HTML, где искать наши шрифты.

#### 3.1 Установить пользовательский CSS
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

Этот CSS окрашивает заголовок в коричневый, а абзац — в серый. Вы можете добавить любые корректные правила CSS; Aspose.HTML поддерживает полную спецификацию CSS2.1 и многие возможности CSS3. *(Это пример **apply custom css**.)*

#### 3.2 Указать папку с пользовательскими шрифтами
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

Поместите любые файлы `.ttf` или `.otf`, которые хотите использовать, в папку `fonts`, расположенную в корне вашего проекта. Aspose.HTML автоматически загрузит эти шрифты при рендеринге.

> **Pro tip:** Если у вас несколько семейств шрифтов, храните их в подпапках и добавляйте каждый родительский каталог в `FontsLookupFolder`, используя список, разделённый точкой с запятой.

### Шаг 4: Загрузить HTML‑документ с конфигурацией
Теперь загрузим ранее созданный HTML‑файл, применив только что построенную пользовательскую конфигурацию.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

Объект `HTMLDocument` теперь представляет стилизованный HTML, готовый к конвертации.

### Шаг 5: Конвертировать HTML в PDF
Наконец, мы выполняем **aspose html pdf conversion**, чтобы создать PDF‑файл, учитывающий наши пользовательские шрифты и стили.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

Объект `PdfSaveOptions` позволяет настроить параметры вывода, такие как размер страницы, сжатие и метаданные. Для базовой конвертации параметры по умолчанию работают отлично.

### Шаг 6: Очистить ресурсы
Корректное освобождение ресурсов предотвращает утечки памяти, особенно при обработке большого количества документов в длительно работающем приложении.

#### 6.1 Освободить HTMLDocument
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 Освободить Configuration
```java
if (configuration != null) {
    configuration.dispose();
}
```

Эти вызовы освобождают нативные ресурсы, выделенные Aspose.HTML.

## Распространённые проблемы и решения
| Проблема | Решение |
|----------|---------|
| **Шрифты не отображаются** | Убедитесь, что папка `fonts` правильно указана и содержит корректные файлы `.ttf`/`.otf`. При необходимости используйте абсолютные пути, если папка находится за пределами каталога проекта. |
| **PDF выглядит пустым** | Убедитесь, что путь к HTML‑файлу правильный и файл доступен для чтения. Проверьте, что объект `Configuration` передаётся в конструктор `HTMLDocument`. |
| **Исключение лицензии** | Примените временную или полную лицензию Aspose перед вызовом любых API Aspose. Поместите файл лицензии в classpath и загрузите его с помощью `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`. |
| **Неожиданное отображение CSS** | Aspose.HTML поддерживает большинство CSS, но не все современные возможности (например, CSS Grid). Упростите стили или используйте поддерживаемые свойства CSS. |

## Часто задаваемые вопросы

**Q: Можно ли использовать любой шрифт с Aspose.HTML для Java?**  
A: Да, любой TrueType (`.ttf`) или OpenType (`.otf`) шрифт, поддерживаемый вашей операционной системой, может быть использован. Просто поместите файлы в папку, указанную в `FontsLookupFolder`.

**Q: Нужна ли лицензия для использования Aspose.HTML для Java?**  
A: Хотя библиотеку можно оценивать без лицензии, [temporary license](https://purchase.aspose.com/temporary-license/) снимает ограничения оценки. Для продакшн требуется полная лицензия.

**Q: Как можно настроить вывод PDF?**  
A: Передайте сконфигурированный экземпляр `PdfSaveOptions` в `convertHTML`. Вы можете задать размер страницы, поля, уровень сжатия и многое другое.

**Q: Можно ли применять более сложные стили CSS?**  
A: Да, Aspose.HTML поддерживает широкий набор CSS. Сложные селекторы, медиазапросы и псевдоклассы работают как в браузере, хотя некоторые новейшие возможности CSS3/4 могут быть не полностью поддержаны.

**Q: Где можно найти больше примеров и документацию?**  
A: Посетите официальную [Aspose.HTML for Java documentation page](https://reference.aspose.com/html/java/) для подробных ссылок на API и дополнительных примеров кода.

**Q: Как временная лицензия Aspose влияет на конверсию?**  
A: Временная лицензия снимает ограничение в 10 страниц и водяной знак, которые появляются в режиме оценки, позволяя полностью протестировать рабочий процесс **aspose html pdf conversion**.

---

**Последнее обновление:** 2026-04-05  
**Тестировано с:** Aspose.HTML for Java 24.12 (последняя версия на момент написания)  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}