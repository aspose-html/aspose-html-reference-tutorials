---
category: general
date: 2026-10-28
description: Узнайте, как открывать ссылки в новой вкладке, разбирая HTML на Java,
  находя внешние ссылки и добавляя target="_blank".
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: ru
lastmod: 2026-10-28
og_description: 'Открывать ссылки в новой вкладке с помощью Java: парсить HTML, находить
  внешние ссылки, добавлять target="_blank" и сохранять изменённый HTML.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Открытие ссылок в новой вкладке с помощью Java – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Как открыть ссылки в новой вкладке с помощью Java
url: /ru/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как открыть ссылки в новой вкладке с помощью Java

Если вам нужно **открывать ссылки в новой вкладке** из статического HTML‑файла, это руководство покажет, как это сделать. Вы научитесь **разбирать HTML в Java**, **находить внешние ссылки**, **добавлять target blank** и **сохранять изменённый HTML** без выхода из вашей IDE.

Открытие внешних ссылок в новой вкладке браузера улучшает пользовательский опыт и удерживает посетителей на исходной странице. Ниже представленное решение работает с любым HTML‑документом, требует только популярную библиотеку jsoup и работает на Java 8 и новее.

## Требования

* Установлен JDK 8 +
* Инструмент сборки (Maven или Gradle) для получения зависимости **jsoup**
* HTML‑файл, содержащий теги `<a>` с классом `external`

Веб‑сервер или дополнительные фреймворки не требуются — jsoup обрабатывает всё локально.

## Шаг 1: Настройте jsoup в вашем проекте

Добавьте jsoup как зависимость. Если вы используете Maven, разместите это в `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Для Gradle добавьте следующую строку в `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Эти координаты подтягивают последнюю стабильную версию (по состоянию на октябрь 2026). После синхронизации вы сможете импортировать классы `org.jsoup` в ваши Java‑файлы.

## Шаг 2: Разбор HTML‑документа

Разбор файла — первый шаг к **открытию ссылок в новой вкладке**. Метод `Jsoup.parse` читает файл в изменяемую структуру, похожую на DOM.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Почему это важно*: `Document` предоставляет CSS‑подобные селекторы, что делает поиск нужных элементов тривиальным.

## Шаг 3: Поиск внешних ссылок

Теперь найдите каждый элемент `<a>`, имеющий класс `external`. Это соответствует требованию **find external links**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` — это коллекция найденных узлов. Если селектор возвращает пустой набор, в вашем HTML отсутствует класс или используется другая схема именования — скорректируйте селектор соответственно.

## Шаг 4: Добавьте `target="_blank"` к каждой ссылке

Для каждого узла, возвращённого **find external links**, установите атрибут `target` в `_blank`. Это удовлетворяет шагу **add target blank** и гарантирует, что браузеры откроют ссылку в новой вкладке.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

Метод `attr` перезаписывает любое существующее значение `target`, обеспечивая согласованное поведение всех внешних якорей.

## Шаг 5: Сохраните изменённый HTML

После обновления DOM запишите изменения обратно в файл. Это завершает часть руководства **save modified html**.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` сериализует весь документ, сохраняя отступы и форматирование, как изначально разобрал jsoup.

## Полный рабочий пример

Объединение всех шагов даёт автономную программу, которую можно скопировать, вставить и запустить.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Ожидаемый вывод

Предположим, `sample.html` содержит:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

После запуска программы, `updated.html` будет содержать:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Только внешняя ссылка получила атрибут `target="_blank"`, что означает, что браузеры теперь откроют её в новой вкладке.

## Профессиональные советы и распространённые подводные камни

* **Pro tip:** Если нужно рассматривать ссылки, начинающиеся с `http://` или `https://`, как внешние даже без CSS‑класса, расширьте селектор: `doc.select("a[href^=http]")`.
* **Edge case:** На некоторых страницах уже указан `target="_self"`; вызов `attr` перезаписывает его, обеспечивая согласованное поведение.
* **Performance:** Для очень больших HTML‑файлов рассмотрите потоковый разбор (`Jsoup.parse(File, String, String, Parser.htmlParser())`), чтобы снизить потребление памяти.
* **Testing:** Проверьте результат, открыв `updated.html` в браузере и изучив ссылку с помощью инструментов разработчика — ищите атрибут `target`.

## Заключение

Теперь у вас есть полное, готовое к запуску решение для **открытия ссылок в новой вкладке** с помощью Java. Руководство охватывало, как **parse html in java**, **find external links**, **add target blank** и **save modified html**, всё это с помощью лёгкой библиотеки jsoup.

Отсюда вы можете:

* Расширить селектор для обработки других шаблонов ссылок (например, `rel="external"`).  
* Скомбинировать эту логику с шагом сборки, который обрабатывает все HTML‑файлы в проекте.  
* Интегрировать код в более крупный конвейер управления контентом.

Не стесняйтесь экспериментировать с различными селекторами или форматами вывода и делиться результатами с сообществом!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как использовать CSS в Java – загрузка HTML, подсчёт ссылок и оценка XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [Как разбирать HTML в Java – извлечение текста из HTML‑статей](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Создание нового HTML‑элемента с Java – полное руководство Aspose.HTML](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}