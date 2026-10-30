---
category: general
date: 2026-04-23
description: Как читать файл XHTML и извлекать атрибуты href, необходимые Java‑разработчикам.
  Узнайте, как перебрать список узлов в Java с понятным примером Java XPath с пространством
  имён.
draft: false
keywords:
- how to read xhtml file
- extract href attributes java
- iterate node list java
- java xpath namespace example
- aspose html xpath
language: ru
og_description: Как читать файл XHTML и извлекать атрибуты href с помощью Java. Это
  руководство демонстрирует полный пример Java XPath с пространством имён и итерацию
  списка узлов.
og_title: Как прочитать файл XHTML в Java – пример использования пространства имён
  XPath
tags:
- Java
- XPath
- XML
- Aspose.HTML
title: Как прочитать файл XHTML в Java – пример использования пространства имён XPath
url: /ru/java/creating-managing-html-documents/how-to-read-xhtml-file-in-java-xpath-namespace-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как читать XHTML файл в Java – пример с пространством имён XPath

Когда‑нибудь нужно было **прочитать XHTML файл** и извлечь из него все ссылки, но пространство имён XML постоянно мешало? Вы не одиноки. В моей повседневной работе с веб‑скрейпингом и обработкой документов столкновение с атрибутом `xmlns` — обычное препятствие, особенно когда вам нужен просто быстрый список значений `href`.  

К счастью, с несколькими строками Java и Aspose.HTML вы можете загрузить файл, указать XPath, что означает пространство имён XHTML, и затем **перебрать список узлов**, чтобы вывести каждую ссылку. В этом руководстве мы пройдём полный, исполняемый пример, который показывает, как *читать XHTML файл*, **извлекать атрибуты href java**, и корректно работать с пространствами имён.  

Мы также рассмотрим несколько вариантов — что если документ использует другой префикс, или вам нужно защититься от отсутствующих атрибутов? К концу вы получите надёжный **java xpath namespace example**, который можно вставить в любой проект.

---

## Требования

- Java 8 или новее (код также работает с Java 11+)  
- Библиотека Aspose.HTML for Java (бесплатная пробная версия или лицензия) – добавьте Maven‑артефакт `com.aspose:aspose-html:23.10` или эквивалентный JAR в ваш classpath.  
- Простой XHTML файл (`sample.xhtml`), размещённый где‑то на диске.  
- Базовое знакомство с XPath‑выражениями.

> **Pro tip:** Если вы используете Maven, добавьте эту зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

---

## Шаг 1 – Загрузка XHTML документа

Первое, что нужно сделать, — предоставить Aspose.HTML доступ к вашему файлу. Считайте `Document` точкой входа; он парсит разметку и строит DOM, который вы можете запросить.

```java
import com.aspose.html.Dom.Document;

// ...

// Replace with the actual path to your XHTML file
String xhtmlPath = "C:/myproject/sample.xhtml";
Document xhtmlDoc = new Document(xhtmlPath);
```

> **Почему это важно:** Загрузка файла в объект `Document` проверяет разметку и нормализует пространства имён, что делает последующий шаг с XPath надёжным.

---

## Шаг 2 – Определение простого NamespaceContext

XPath необходимо знать, к чему привязан префикс `xhtml:`. Вы могли бы использовать полноценную реализацию `NamespaceContext`, но для одного пространства имён достаточно небольшого анонимного класса.

```java
import javax.xml.namespace.NamespaceContext;
import java.util.Iterator;

NamespaceContext xhtmlNs = new NamespaceContext() {
    @Override
    public String getNamespaceURI(String prefix) {
        // The standard namespace for XHTML
        return "http://www.w3.org/1999/xhtml";
    }

    @Override
    public String getPrefix(String uri) { return null; }

    @Override
    public Iterator<String> getPrefixes(String uri) { return null; }
};
```

> **Что если документ использует другой префикс?** Пока вы сохраняете тот же URI (`http://www.w3.org/1999/xhtml`), вы можете выбрать любой префикс в XPath‑выражении; `NamespaceContext` заполняет пробел.

---

## Шаг 3 – Выполнение XPath‑запроса для выбора всех элементов `<a>`

Теперь начинается главное в **java xpath namespace example**. Выражение `//xhtml:body//xhtml:a` проходит от элемента `<body>` к каждому тегу `<a>`, учитывая пространство имён, которое мы только что задали.

```java
import com.aspose.html.Dom.NodeList;
import com.aspose.html.Dom.Element;

// ...

NodeList anchorNodes = xhtmlDoc.evaluateXPath("//xhtml:body//xhtml:a", xhtmlNs);
```

> **Почему использовать `//xhtml:body//xhtml:a`?**  
> - `//xhtml:body` гарантирует, что мы начинаем внутри элемента body, игнорируя случайные теги `<a>`, которые могут появиться в `<head>`.  
> - Двойной слеш после `body` (`//xhtml:a`) захватывает ссылки любой вложенности, будь то прямые дочерние элементы или вложенные в `<div>`, `<p>` и т.д.

---

## Шаг 4 – Перебор списка узлов и вывод атрибутов `href`

Наконец, мы проходим по `NodeList`. Каждый узел — это `Element`, поэтому можно вызвать `getAttribute("href")`. Мы также защищаемся от отсутствующих атрибутов — некоторые теги `<a>` могут быть заглушками без `href`.

```java
for (int i = 0; i < anchorNodes.getLength(); i++) {
    Element anchor = (Element) anchorNodes.item(i);
    String href = anchor.getAttribute("href");
    if (href != null && !href.isEmpty()) {
        System.out.println(href);
    } else {
        // Optional: indicate a link without href
        System.out.println("[No href attribute]");
    }
}
```

**Ожидаемый вывод** (при условии, что `sample.xhtml` содержит три реальных ссылки):

```
https://example.com/home
https://example.com/about
https://example.com/contact
```

Если у какого‑либо `<a>` нет `href`, вместо него будет выведено `[No href attribute]`.

---

## Полный, готовый к запуску пример

Собрав все части вместе, вы получаете автономную программу, которую можно сразу же скомпилировать и запустить.

```java
import com.aspose.html.Dom.Document;
import com.aspose.html.Dom.Element;
import com.aspose.html.Dom.NodeList;
import javax.xml.namespace.NamespaceContext;
import java.util.Iterator;

public class XPathWithNamespaces {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the XHTML document
        Document xhtmlDoc = new Document("C:/myproject/sample.xhtml");

        // Step 2: Provide a simple NamespaceContext for the XHTML namespace
        NamespaceContext xhtmlNs = new NamespaceContext() {
            @Override
            public String getNamespaceURI(String prefix) {
                return "http://www.w3.org/1999/xhtml";
            }
            @Override
            public String getPrefix(String uri) { return null; }
            @Override
            public Iterator<String> getPrefixes(String uri) { return null; }
        };

        // Step 3: Select all <a> elements inside the body using an XPath expression
        NodeList anchorNodes = xhtmlDoc.evaluateXPath("//xhtml:body//xhtml:a", xhtmlNs);

        // Step 4: Iterate over the selected nodes and print each link's href attribute
        for (int i = 0; i < anchorNodes.getLength(); i++) {
            Element anchorElement = (Element) anchorNodes.item(i);
            String href = anchorElement.getAttribute("href");
            if (href != null && !href.isEmpty()) {
                System.out.println(href);
            } else {
                System.out.println("[No href attribute]");
            }
        }
    }
}
```

> **Подсказка:** Если нужно обработать большой файл, рассмотрите потоковую загрузку документа с помощью `HtmlDocument` вместо загрузки всего DOM в память. Основная логика XPath остаётся той же.

---

## Часто задаваемые вопросы и особые случаи

### 1. Что если XHTML файл использует пространство имён по умолчанию без префикса?
Вы всё равно можете использовать префикс в XPath‑выражении; просто сопоставьте его в `NamespaceContext`, как показано. XPath никогда не видит «по‑умолчанию» — он работает только с явными префиксами.

### 2. Могу ли я извлекать другие атрибуты (например, `title` или `rel`) одновременно?
Конечно. Внутри цикла вызывайте `anchorElement.getAttribute("title")` или любое другое имя атрибута. Можно даже создать небольшой POJO для хранения данных.

### 3. Как обрабатывать некорректный XHTML?
Aspose.HTML прощает ошибки и пытается исправить распространённые проблемы. Если парсинг не удался, перехватите исключение и запишите путь к файлу для последующего анализа.

### 4. Что насчёт относительных URL?
`href`, который вы получаете, точно такой же, как в разметке. Чтобы разрешить его относительно базового URL документа, используйте `java.net.URI`:

```java
URI base = new URI(xhtmlDoc.getBaseUrl());
URI resolved = base.resolve(href);
System.out.println(resolved);
```

### 5. Нужно ли закрывать `Document`?
Да, вызовите `xhtmlDoc.dispose();` после завершения, чтобы освободить нативные ресурсы (Aspose.HTML использует нативную память).

---

## Альтернативные подходы (если не используется Aspose.HTML)

- **Standard JAXP с `DocumentBuilderFactory`** – потребуется включить поддержку пространств имён и использовать `XPathFactory`. Код будет длиннее и более подвержен ошибкам.  
- **JSoup** – отлично подходит для HTML, но рассматривает его как HTML, а не XML, поэтому обработка пространств имён отсутствует.  
- **XMLBeans или JAXB** – избыточно для простого извлечения ссылок.

Для большинства проектов, уже использующих Aspose.HTML, показанный выше метод является самым чистым и производительным.

---

## Заключение

Мы только что продемонстрировали **как читать XHTML файл** в Java, настроили **java xpath namespace example** и **iterate node list java**, чтобы извлечь каждый атрибут `href`. Ключевые шаги: загрузка документа, определение `NamespaceContext`, выполнение XPath‑запроса с пространством имён и перебор полученных узлов.  

Отсюда вы можете расширить решение — сохранять URL в список, фильтровать по домену или записывать их в CSV. Этот шаблон также работает с любым другим XML с пространствами имён, так что вы готовы решать похожие задачи.

---

### Что дальше?

- **Изучить другие оси XPath** (`preceding-sibling`, `following` и др.), чтобы извлекать более сложные отношения.  
- **Комбинировать с HTTP‑клиентами** (например, `HttpClient`) для автоматического получения связанных страниц.  
- **Добавить модульные тесты** с использованием JUnit, чтобы проверить, что ваше XPath‑выражение возвращает ожидаемое количество ссылок.

Удачной разработки, и не позволяйте пространствам имён замедлять вас!  

![Диаграмма, показывающая как Java‑программа читает XHTML файл, применяет XPath с учётом пространства имён и выводит значения href – как читать xhtml файл](https://example.com/images/xhtml-read-diagram.png "как читать xhtml файл")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}