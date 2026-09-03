---
category: general
date: 2026-01-01
description: Изучите, как выполнять запросы к HTML с помощью Java, как выбирать CSS
  и извлекать элементы из HTML с практическими примерами и подсчётом узлов.
draft: false
keywords:
- how to query html
- how to select css
- extract elements from html
- select multiple css classes
- how to count nodes
language: ru
og_description: Освойте запросы HTML в Java, научитесь выбирать CSS, извлекать элементы
  из HTML и подсчитывать узлы с реальными примерами кода.
og_title: Как выполнять запросы к HTML в Java – Полный учебник
tags:
- Java
- HTML parsing
- Aspose.HTML
title: Как запрашивать HTML в Java — Полный учебник
url: /ru/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять запросы к HTML в Java – Полный учебник

Когда‑нибудь задумывались **как выполнять запросы к HTML** из Java‑программы, не теряя волосы? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно извлечь данные из статического каталога или спарсить простую страницу, а привычные приёмы работы с DOM кажутся громоздкими.  

Хорошие новости? С несколькими строками кода вы можете загрузить HTML‑файл, выполнить XPath или CSS‑селекторы и даже подсчитать нужные узлы — всё в одном аккуратном потоке. В этом руководстве мы пройдемся по **как выполнять запросы к HTML**, **как выбирать CSS**, а также покажем, как **извлекать элементы из HTML**, **выбирать несколько CSS‑классов** и **как подсчитывать узлы** с помощью Aspose.HTML for Java.

## Что вы узнаете

- Загрузить HTML‑документ с диска или по URL.  
- Использовать XPath для поиска элементов, соответствующих сложным условиям.  
- Применять CSS‑селекторы, включая запросы нескольких классов.  
- Подсчитывать результаты программно.  
- Советы, подводные камни и варианты для реальных сценариев.

*Требования*: Java 8+, Maven или Gradle, и копия библиотеки Aspose.HTML for Java (бесплатная пробная версия подходит для экспериментов).

---

![how to query html example](https://example.com/images/query-html.png "Screenshot showing how to query html with Java")

## Как выполнять запросы к HTML – загрузка документа

Прежде чем задавать любые вопросы, вам нужен объект документа для interrogate. Класс `HTMLDocument` из Aspose.HTML делает всю тяжёлую работу.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;
import java.util.List;

public class QueryDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document you want to query
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/catalog.html");
```

> **Почему это важно** – Загрузка файла создаёт DOM‑дерево в памяти. Отсюда вы можете выполнять как XPath, так и CSS‑запросы, не беспокоясь о сетевой задержке или некорректной разметке. Если файл не найден, Aspose бросает понятный `FileNotFoundException`, что упрощает отладку.

### Pro tip
Если вы получаете HTML с удалённого сайта, просто передайте строку URL в `HTMLDocument` — Aspose загрузит и разберёт его за вас.

## Как выбирать CSS – использование CSS‑селекторов

Как только DOM готов, выбор узлов с помощью CSS так же прост, как однострочник. Давайте получим каждый элемент, у которого есть класс `featured` или `highlight`.

```java
        // Step 2: Locate elements marked as featured or highlighted using a CSS selector
        List<Element> featuredElements = document.selectCss(".featured, .highlight");

        // Step 3: Output the number of elements found by the CSS selector
        System.out.println("Featured elements: " + featuredElements.size());
```

> **Explanation** – Селектор `.featured, .highlight` сообщает движку вернуть *любой* элемент, у которого атрибут `class` содержит `featured` **или** `highlight`. Это канонический способ **выбирать несколько CSS‑классов** в одном запросе.

### Edge case
Если элемент содержит оба класса (например, `<div class="featured highlight">`), он появится **один раз** в списке результатов, предотвращая двойной подсчёт.

## Извлекать элементы из HTML – комбинирование XPath и CSS

XPath блистает, когда нужна реляционная логика, например «все узлы `<book>`, где цена превышает 30». Ниже точный фрагмент из оригинального примера:

```java
        // Step 4: Find all <book> elements with a price greater than 30 using XPath
        List<Element> expensiveBooks = document.selectXPath("//book[price>30]");

        // Step 5: Output the number of books that match the XPath query
        System.out.println("Expensive books count: " + expensiveBooks.size());
```

> **Why XPath?** – XPath может напрямую оценивать числовые сравнения (`price>30`), чего CSS не умеет. Он также позволяет обходить отношения родитель/дитя без дополнительного кода.

### Variation
Если нужно получить *заголовки* этих дорогих книг, можно добавить второй запрос:

```java
        List<Element> titles = expensiveBooks.get(0).selectXPath("./title");
        System.out.println("First expensive book title: " + titles.get(0).getTextContent());
```

## Выбирать несколько CSS‑классов – продвинутые приёмы селекторов

Иногда требуется нацелиться на элементы, которые **одновременно** имеют несколько классов, например `class="product featured"`. Синтаксис CSS для этого — конкатенированный селектор без запятых.

```java
        // Example: select <div> elements that are both .product and .featured
        List<Element> productFeatured = document.selectCss("div.product.featured");
        System.out.println("Product‑featured divs: " + productFeatured.size());
```

> **Key point** – Между именами классов нет пробела; пробел означал бы «потомок». Этот шаблон необходим, когда вы **выбираете несколько CSS‑классов**, работающих совместно для стилизации компонента.

## Как подсчитывать узлы – получение точных итогов

Подсчёт узлов часто является завершающим шагом в конвейере извлечения данных. Вы уже видели использование `list.size()` после каждого запроса, но давайте обернём это в переиспользуемый помощник.

```java
    /**
     * Returns the count of elements that match the given CSS selector.
     */
    private static int countByCss(HTMLDocument doc, String selector) {
        return doc.selectCss(selector).size();
    }

    /**
     * Returns the count of elements that match the given XPath expression.
     */
    private static int countByXPath(HTMLDocument doc, String xpath) {
        return doc.selectXPath(xpath).size();
    }

    public static void main(String[] args) throws Exception {
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/catalog.html");

        System.out.println("Expensive books: " + countByXPath(doc, "//book[price>30]"));
        System.out.println("Featured items: " + countByCss(doc, ".featured, .highlight"));
        System.out.println("Product‑featured divs: " + countByCss(doc, "div.product.featured"));
    }
```

> **Why wrap it?** – Централизация логики подсчёта делает код проще для тестирования и уменьшает дублирование. Это также проясняет **как подсчитывать узлы** для будущих читателей.

### Common pitfalls
- **Whitespace in class attributes** – `"featured "` (пробел в конце) всё равно совпадает с `.featured`, потому что селектор обрезает пробелы.
- **Case sensitivity** – Имена классов в HTML чувствительны к регистру в режиме XML; убедитесь, что ваш исходный HTML использует единый регистр.

## Полный рабочий пример

Объединив всё вместе, представляем автономную программу, которую можно скопировать и вставить в вашу IDE:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;
import java.util.List;

public class QueryDemo {

    private static int countByCss(HTMLDocument doc, String selector) {
        return doc.selectCss(selector).size();
    }

    private static int countByXPath(HTMLDocument doc, String xpath) {
        return doc.selectXPath(xpath).size();
    }

    public static void main(String[] args) throws Exception {
        // Load the HTML file (adjust the path as needed)
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/catalog.html");

        // XPath: books priced over 30
        int expensiveBooks = countByXPath(document, "//book[price>30]");
        System.out.println("Expensive books count: " + expensiveBooks);

        // CSS: featured or highlighted elements
        int featured = countByCss(document, ".featured, .highlight");
        System.out.println("Featured elements: " + featured);

        // CSS: elements that are both .product and .featured
        int productFeatured = countByCss(document, "div.product.featured");
        System.out.println("Product‑featured divs: " + productFeatured);
    }
}
```

**Expected output** (при типичном `catalog.html`):

```
Expensive books count: 4
Featured elements: 7
Product‑featured divs: 2
```

Если ваш файл содержит меньше совпадающих узлов, цифры скорректируются соответственно — без сюрпризов.

---

## Заключение

Мы рассмотрели **как выполнять запросы к HTML** с помощью Aspose.HTML for Java, продемонстрировали **как выбирать CSS**, показали, как **извлекать элементы из HTML**, разобрали **выбор нескольких CSS‑классов** и объяснили **как подсчитывать узлы** надёжно.  

Главный вывод? Загрузка документа один раз и последующее повторное использование того же экземпляра `HTMLDocument` позволяет смешивать XPath и CSS‑запросы без потерь в производительности.  

Готовы к следующему шагу? Попробуйте цепочкой соединять селекторы, чтобы вытягивать значения атрибутов (`@href`, `@src`) или экспортировать набор результатов в JSON для дальнейшей обработки. Вы также можете изучить обработку пагинации, если ваш исходный HTML разбит на несколько страниц.

Есть сложный селектор или крайний случай, который не поддаётся? Оставьте комментарий ниже, и мы разберёмся вместе. Приятных запросов!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}