---
category: general
date: 2026-09-29
description: Узнайте, как выбирать элементы по классу, читать HTML из файла и находить
  внешние ссылки в Java. Это пошаговое руководство охватывает эффективную итерацию
  NodeList.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: ru
lastmod: 2026-09-29
og_description: Выбирайте элементы по классу в Java, читайте HTML из файла и находите
  внешние ссылки с помощью querySelectorAll. Следуйте полному примеру, чтобы перебрать
  NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Выбор элементов по классу в Java — полное руководство с querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: Как выбрать элементы по классу в Java с помощью querySelectorAll
url: /ru/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выбрать элементы по классу в Java с помощью querySelectorAll

Если вам нужно **выбирать элементы по классу** при обработке HTML‑файла в Java, это руководство покажет, как это сделать. Вы научитесь читать HTML из файла, использовать `querySelectorAll` для поиска внешних ссылок и безопасно перебрать полученный `NodeList`.

Работа с HTML в Java часто кажется тяжёлой, но современные библиотеки предоставляют лаконичный API, основанный на CSS‑селекторах. Пример ниже использует **jsoup** (версия 1.17.2), поскольку он реализует селекторы в стиле `querySelectorAll` и возвращает коллекцию `Elements`, которая ведёт себя как `NodeList`. При необходимости вы можете адаптировать ту же логику к другим реализациям DOM.

## Предварительные требования

* Установлен JDK 17 или новее.
* Maven или Gradle для управления зависимостями.
* Базовое знакомство с потоками Java и моделью DOM.

Add jsoup to your project:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Шаг 1: Чтение HTML из файла

Первая задача — загрузить HTML‑документ с диска. `Jsoup.parse(Path, Charset)` читает файл и строит дерево DOM, которое можно запросить.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Почему это важно*: загрузка файла один раз избавляет от повторных операций ввода‑вывода при последующей итерации по элементам. Объект `Document` содержит полное дерево DOM, позволяя выполнять быстрые запросы селекторов.

## Шаг 2: Использование `querySelectorAll` для выбора элементов по классу

Теперь, когда документ находится в памяти, вы можете **выбирать элементы по классу** с помощью CSS‑селектора. Селектор `"a.external"` соответствует тегам `<a>`, имеющим класс `external` — именно то, что нужно для **поиска внешних ссылок**.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Почему это важно*: использование селектора класса одновременно выразительно и эффективно. Библиотека преобразует селектор в оптимизированный обход, поэтому нет необходимости писать ручные циклы по каждому узлу.

## Шаг 3: Итерация NodeList (Elements) в Java

`Elements` реализует `Iterable<Element>`, что означает, что вы можете использовать обычный цикл `for‑each` для **итерации NodeList в Java**. Приведённый ниже цикл выводит атрибут `href` каждой ссылки.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Почему это важно*: прямая итерация сохраняет читаемость кода и избавляет от накладных расходов на преобразование коллекции в поток, когда нужен лишь простой вывод.

## Полный рабочий пример

Объединение трёх шагов даёт автономную программу, которую можно запустить из командной строки.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### Ожидаемый вывод

Assuming `input.html` contains:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Running the program prints:

```
External link: https://example.com
External link: https://openai.com
```

## Профессиональные советы и распространённые подводные камни

* **Кодировка важна** – всегда читайте файл в UTF‑8 (или в той кодировке, которая соответствует вашему источнику). Неправильная кодировка может испортить символы в значениях атрибутов.
* **Несколько классов** – если элемент имеет несколько классов (например, `class="btn external"`), селектор `"a.external"` всё равно сработает, потому что CSS‑селекторы классов проверяют наличие токена, а не точное совпадение строки.
* **Совет по производительности** – если нужен только атрибут `href`, его можно запросить напрямую с помощью `doc.select("a.external[href]").eachAttr("href")`. Это избавляет от создания полных объектов `Element` для каждого совпадения.
* **Безопасность от null** – `link.attr("href")` возвращает пустую строку, если атрибут отсутствует, поэтому проверка на null перед выводом не требуется.

## Часто задаваемые вопросы

**В: Работает ли это с HTML‑фрагментами, у которых отсутствует корневой `<html>`?**  
**О:** Да. `Jsoup.parse` рассматривает ввод как фрагмент и автоматически добавляет недостающие корневые элементы, позволяя селекторам работать с телом фрагмента.

**В: Можно ли использовать `querySelectorAll` без jsoup?**  
**О:** Стандартный Java DOM API (`org.w3c.dom`) не включает `querySelectorAll`. Библиотеки, такие как **HTMLUnit** или **jodd-lagarto**, предоставляют аналогичные методы. Показанный здесь шаблон — загрузка, выбор с помощью CSS, итерация — остаётся тем же.

**В: Что делать, если нужно изменить ссылки, а не просто вывести их?**  
**О:** После получения каждого `Element` вы можете вызвать `link.attr("href", "newUrl")`, а затем записать документ обратно на диск с помощью `Files.writeString`.

## Заключение

Теперь вы знаете, как **выбирать элементы по классу**, **читать HTML из файла**, **находить внешние ссылки** и **итерировать NodeList в Java** с помощью селекторов в стиле `querySelectorAll`. Полный пример демонстрирует чистый, готовый к продакшену рабочий процесс, который можно встроить в более крупные конвейеры скрейпинга или трансформации.

Далее изучайте связанные темы, такие как **парсинг динамического контента с HTMLUnit**, **запись изменённого HTML обратно на диск** или **использование потоков Java для сбора URL‑ов ссылок в список**. Каждая из них опирается на основную технику выбора по классу, продемонстрированную здесь. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как выполнять запросы к HTML в Java — Выбирать элементы, фильтровать по атрибуту и получать текст](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Итерация NodeList в Java — Чтение HTML и получение src изображений](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Загрузка HTML‑документов из файла в Aspose.HTML для Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}