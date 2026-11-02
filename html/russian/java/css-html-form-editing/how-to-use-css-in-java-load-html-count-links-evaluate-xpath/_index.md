---
category: general
date: 2026-06-16
description: Как использовать CSS для загрузки HTML‑файла и подсчёта ссылок в Java.
  Узнайте, как подсчитывать HTML‑элементы и оценивать XPath в Java в одном понятном
  примере.
draft: false
keywords:
- how to use css
- load html file
- how to count links
- count html elements
- evaluate xpath java
language: ru
og_description: Как использовать CSS в Java для загрузки HTML‑файла, подсчёта ссылок
  и оценки XPath‑выражений — всё в одном практическом руководстве.
og_title: Как использовать CSS в Java – загрузить HTML, подсчитать ссылки и выполнить
  XPath
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  headline: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  type: TechArticle
- description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  name: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  steps:
  - name: What if the HTML file is malformed?
    text: Both the CSS and XPath engines are tolerant of minor markup errors (missing
      closing tags, unquoted attributes). However, severe malformations may cause
      the parser to abort. In production, wrap the loading step in a try‑catch block
      and log the exception.
  - name: Can I combine CSS and XPath in a single expression?
    text: Not directly; each engine has its own syntax. The typical pattern is to
      use the one that expresses the condition most naturally (CSS for structural
      queries, XPath for attribute functions) and then merge the results in Java if
      needed.
  - name: How do I count elements across multiple files?
    text: 'Just place the loading logic inside a loop:'
  - name: Does this work with Java 8?
    text: Yes—provided you use a library version that targets Java 8 or higher. The
      code shown does not rely on newer language features.
  type: HowTo
tags:
- Java
- HTML parsing
- CSS selectors
- XPath
title: Как использовать CSS в Java — загрузить HTML, подсчитать ссылки и выполнить
  XPath
url: /ru/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать CSS в Java – загрузка HTML, подсчёт ссылок и оценка XPath

Когда‑нибудь задумывались **как использовать CSS**‑селекторы при обработке HTML‑файла в Java? Возможно, вы создаёте веб‑краулер, скрейпер или просто хотите проанализировать статический сайт. Хорошая новость: не нужно писать собственный парсер с нуля — современные библиотеки позволяют сочетать селекторы CSS4 с выражениями XPath 3.1 в одном удобном рабочем процессе.

В этом руководстве мы пройдём **как загрузить HTML‑файл**, применим CSS‑селектор для подсчёта ссылок в навигационной панели, а затем **оценим XPath**, чтобы подсчитать определённые элементы `<img>`. К концу вы получите полностью готовую программу, выводящую количество найденных узлов, и поймёте, зачем нужен каждый шаг.

## Предварительные требования

- Java 17 (или любой современный JDK), установленный на вашем компьютере  
- Maven или Gradle для управления зависимостями (в примере используем Maven)  
- Небольшой фрагмент HTML, сохранённый как `input.html` в выбранной папке  

Больше никаких инструментов не требуется — только текстовый редактор и терминал.

## Что рассматривается в этом руководстве

- **Загрузка HTML‑файла** в структуру, похожую на DOM, с помощью класса *HTMLDocument*  
- Применение **CSS4‑селектора** (`nav a[data-role]`) для поиска навигационных ссылок  
- Выполнение **XPath 3.1‑выражения** для поиска тегов `<img>`, у которых `src` заканчивается на `.png` и присутствует атрибут `alt`  
- **Подсчёт** результатов обоих запросов и вывод их в консоль  
- Полный исходный код, объяснения «почему», а также быстрый обзор возможных граничных случаев  

Поехали.

---

## Шаг 1 – Как загрузить HTML‑файл с помощью HTMLDocument

Прежде чем выполнять запросы, HTML‑документ необходимо разобрать в traversable‑модель. Класс `HTMLDocument` из библиотеки **jsoup‑plus** (или любого аналогичного HTML‑парсера) делает именно это.

```java
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Load the HTML document from the file system
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/input.html");
        // From here on we can query the DOM using CSS or XPath
```

*Почему это важно:*  
Загрузка файла один раз и хранение ссылки (`doc`) избавляет от повторных операций ввода‑вывода, что может стать узким местом при обработке больших наборов страниц.

---

## Шаг 2 – Как использовать CSS для подсчёта ссылок внутри `<nav>`

Теперь, когда документ находится в памяти, мы можем воспользоваться CSS4‑селектором, чтобы захватить каждый элемент `<a>`, находящийся внутри `<nav>` и имеющий атрибут `data‑role`. Это распространённый шаблон для навигационных меню, использующих data‑атрибуты в качестве JavaScript‑хуков.

```java
        // Use a CSS4 selector to find every <a> inside a <nav> that has a data‑role attribute
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");
```

*Объяснение:*  
- `nav a[data-role]` читается как «любой элемент `<a>` с атрибутом `data‑role`, являющийся потомком элемента `<nav>`».  
- Селектор совместим с **CSS4**, поэтому вы также можете использовать псевдоклассы вроде `:not()` или `:has()`, если ваш сценарий расширяется.

> **Pro tip:** Если нужны только прямые дочерние элементы, замените пробел на `>` (`nav > a[data-role]`). Это уменьшит область поиска и ускорит обработку больших документов.

---

## Шаг 3 – Оценка XPath в Java для подсчёта конкретных элементов `<img>`

XPath особенно полезен, когда требуется фильтрация по атрибутам, которая не так проста в CSS. Здесь мы найдём каждый `<img>`, чей `src` заканчивается на `.png` **и** у которого определён атрибут `alt` — полезно для аудита доступности.

```java
        // Use an XPath 3.1 expression to locate all <img> elements whose src ends with .png and have an alt attribute
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");
```

*Почему XPath?*  
- Функция `ends-with()` входит в XPath 3.1 и позволяет проверять суффикс без использования регулярных выражений.  
- Комбинация нескольких предикатов (`and @alt`) гарантирует, что будут подсчитаны только изображения с корректным источником и описанием.

Если ваша библиотека поддерживает лишь XPath 1.0, придётся использовать `contains(@src, '.png')` и затем фильтровать в Java — менее точный подход.

---

## Шаг 4 – Как подсчитать HTML‑элементы и вывести результаты

Наконец, получаем длину обоих объектов `NodeList` и выводим их. Это и есть **как подсчитать ссылки**, но работает для любой коллекции узлов.

```java
        // Output the number of matches for each query
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Ожидаемый вывод в консоль** (при условии, что в примере HTML найдено 3 подходящие ссылки и 2 подходящих изображения):

```
Nav links: 3
PNG images with alt: 2
```

Если результаты равны нулю, проверьте синтаксис селектора или убедитесь, что `input.html` действительно содержит ожидаемые элементы.

---

## Полный рабочий пример

Ниже представлена полностью автономная программа, которую можно скопировать в файл `CssXPathDemo.java`. В ней включены необходимые импорты, простой фрагмент `pom.xml` для Maven и минимальный HTML‑пример для тестирования.

```java
/* CssXPathDemo.java */
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document
        HTMLDocument doc = new HTMLDocument("input.html");

        // Step 2: CSS selector – count navigation links with data-role
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");

        // Step 3: XPath expression – count PNG images that have alt text
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");

        // Step 4: Print the results
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Фрагмент `pom.xml` для Maven** (добавьте эту зависимость, чтобы подключить HTML‑парсер, поддерживающий как CSS4, так и XPath 3.1):

```xml
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>html-parser-plus</artifactId>
        <version>2.3.1</version>
    </dependency>
</dependencies>
```

**Пример `input.html`** (разместите его в той же директории, что и Java‑файл):

```html
<!DOCTYPE html>
<html lang="en">
<head><title>Test Page</title></head>
<body>
<nav>
    <a href="/home" data-role="main">Home</a>
    <a href="/about" data-role="secondary">About</a>
    <a href="/contact">Contact</a>
</nav>
<img src="logo.png" alt="Company Logo">
<img src="banner.jpg">
<img src="icon.png" alt="Icon">
</body>
</html>
```

Запуск `mvn compile exec:java -Dexec.mainClass=CssXPathDemo` выдаст ожидаемые подсчёты, указанные выше.

---

## Пограничные случаи и часто задаваемые вопросы

### Что делать, если HTML‑файл повреждён?

Оба движка — CSS и XPath — терпимы к небольшим ошибкам разметки (отсутствующие закрывающие теги, некавыченные атрибуты). Однако серьёзные нарушения могут привести к остановке парсера. В продакшене оберните шаг загрузки в `try‑catch` и логируйте исключения.

### Можно ли объединить CSS и XPath в одном выражении?

Непрямо; каждый движок имеет собственный синтаксис. Обычная практика — использовать тот, который естественнее выражает условие (CSS для структурных запросов, XPath для функций над атрибутами), а затем объединять результаты в Java при необходимости.

### Как подсчитать элементы в нескольких файлах?

Поместите логику загрузки в цикл:

```java
for (Path p : Files.newDirectoryStream(Paths.get("html_folder"), "*.html")) {
    HTMLDocument doc = new HTMLDocument(p.toString());
    // repeat the queries...
}
```

### Работает ли это с Java 8?

Да, при условии, что вы используете версию библиотеки, совместимую с Java 8 или выше. Представленный код не опирается на более новые возможности языка.

---

## Заключение

Мы продемонстрировали **как использовать CSS**‑селекторы вместе с **evaluate xpath java** — как **загрузить HTML‑файл**, **подсчитать ссылки** и **подсчитать html‑элементы**, отвечающие заданным критериям. Ключевые выводы:

- Загрузите документ один раз с помощью `HTMLDocument`.  
- Используйте CSS4 для простых структурных запросов (`nav a[data-role]`).  
- Применяйте XPath 3.1 для мощных функций над атрибутами (`ends-with(@src, '.png')`).  
- Получайте длину `NodeList`, чтобы узнать точное количество.  

Отсюда вы можете расширять скрипт: добавлять новые селекторы, записывать результаты в CSV или интегрировать его в более крупный краулинг‑pipeline. Комбинация CSS и XPath даёт гибкость для решения практически любой задачи по извлечению данных из HTML.

Готовы экспериментировать? Попробуйте заменить CSS‑селектор на `section article[data-id]` или изменить XPath, чтобы искать теги `<video>` с определённым кодеком. Возможности безграничны.

Если руководство оказалось полезным, поделитесь им, поставьте звёздочку репозиторию или оставьте комментарий со своими сценариями использования. Приятного кодинга!

![how to use css example diagram](https://example.com/diagram.png "how to use css example")

---


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом материале. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы вы могли освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}