---
category: general
date: 2026-03-05
description: Как выполнять запросы к HTML в Java, чтобы читать HTML‑файл и извлекать
  изображения. Узнайте, как читать HTML‑файл в Java, получать URL изображений в Java
  и перебрать NodeList в Java.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: ru
og_description: Как выполнять запросы к HTML в Java и получать URL изображений. Это
  руководство показывает, как читать HTML‑файл в Java, находить изображения и проходить
  по NodeList в Java.
og_title: Как выполнять запросы к HTML в Java — извлекать URL изображений
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: Как выполнять запросы к HTML в Java — извлекать URL изображений
url: /ru/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять запросы к HTML в Java – Извлечение URL изображений

Когда‑то задумывались **как выполнять запросы к HTML** в Java, чтобы вытянуть каждое изображение со страницы? Вы не одиноки — разработчикам постоянно нужно читать HTML‑файлы, собирать изображения и делать с полученными URL что‑то полезное. В этом руководстве мы пройдем практический пример, который показывает точно **как выполнять запросы к HTML**, как читать HTML‑файл в стиле Java и получать URL изображений на Java.

Мы будем использовать Aspose.HTML for Java, но концепции — XPath, CSS‑селекторы и перебор `NodeList` — применимы к любой библиотеке DOM. К концу этого руководства вы будете уверенно знать **как извлекать изображения**, как **перебирать NodeList Java**, и у вас будет готовый фрагмент кода, который можно сразу вставить в проект.

![Как выполнять запросы к HTML в Java пример](https://example.com/placeholder.png "Как выполнять запросы к HTML в Java")

---

## Что вы узнаете

- Загрузка HTML‑документа с диска (read HTML file Java)  
- Поиск тегов `<img>` с помощью XPath и CSS‑селекторов (how to extract images)  
- Перебор полученного `NodeList` (iterate over NodeList Java)  
- Вывод атрибута `src` каждого изображения (get image URLs Java)

Никаких внешних сервисов, никаких сложных инструментов сборки — только чистый Java и одна зависимость Maven.

---

## Требования

- Установлен Java 8 или новее  
- Maven или Gradle для управления зависимостями  
- Базовое знакомство со структурой HTML  
- По желанию: простой HTML‑файл (`sample.html`) с несколькими элементами `<figure><img …></figure>`

Если всё это у вас есть, можно сразу переходить к делу.

---

## Шаг 1: Read HTML File Java – загрузка документа

Первое, что нужно сделать, — загрузить HTML в память. Класс `HTMLDocument` из Aspose.HTML делает всю тяжёлую работу. Представьте, что вы открываете книгу, чтобы листать её страницы.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**Почему это важно:** Загрузка файла даёт вам дерево DOM, которое можно запросить. Если путь указан неверно, вы получите `FileNotFoundException`, поэтому проверьте расположение перед запуском.

---

## Шаг 2: Locate Images with XPath – How to Extract Images

XPath — мощный язык запросов, позволяющий точно указывать нужные узлы. Здесь мы запрашиваем каждый `<img>` внутри `<figure>`, у которого также есть атрибут `alt`.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**Почему XPath?** Он лаконичен и работает даже с «грязным» HTML. Выражение `//figure/img[@alt]` переводится как: «любой `<img>` внутри `<figure>`, имеющий атрибут `alt`». Если нужно отфильтровать по другим атрибутам, просто измените скобки.

---

## Шаг 3: Locate Images with CSS Selector – Alternative Way to Extract Images

Иногда удобнее использовать синтаксис CSS, потому что он совпадает с тем, что пишете в таблицах стилей. `querySelectorAll` принимает тот же селектор, что и в браузере.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**Почему оба способа?** Показав оба, мы даём возможность выбрать инструмент, который вам ближе. На практике обычно используют один из них, но наличие обоих примеров делает руководство более полным.

---

## Шаг 4: Iterate Over NodeList Java – Get Image URLs Java

Теперь, когда у нас есть коллекция, её нужно пройти. Здесь и вступает в действие **iterate over NodeList Java**. Мы извлекаем атрибут `src` каждого изображения и выводим его.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**Почему обычный `for`‑цикл?** `NodeList` из Aspose не реализует `Iterable`, поэтому синтаксис `for‑each` не скомпилируется. Перебор по индексу — надёжный способ **iterate over NodeList Java**.

---

## Ожидаемый вывод

Запуск программы против примера HTML, например:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

даст примерно такой результат:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

Если ваш файл содержит больше тегов `<img>`, соответствующих условию, количество строк увеличится соответственно.

---

## Частые ошибки и профессиональные советы

- **Проблемы с путём к файлу:** используйте абсолютный путь или разместите `sample.html` относительно рабочей директории проекта.  
- **Отсутствует атрибут `alt`:** наши запросы XPath/CSS фильтруют по `[@alt]`. Если нужны *все* изображения, уберите фильтр (`//figure/img` или `figure img`).  
- **Производительность:** для огромных документов стоит рассмотреть потоковые парсеры, но для большинства задач веб‑скрейпинга подход DOM подходит.  
- **Проблемы с кодировкой:** Aspose.HTML учитывает charset, объявленный в HTML. Если видите «кракозябры», убедитесь, что файл сохранён в UTF‑8.  

---

## Как расширить пример

Теперь, когда вы умеете **get image URLs Java**, можно добавить:

1. **Скачивание изображений** с помощью `java.net.URL` и `Files.copy`.  
2. **Сохранение URL в базе данных** для последующей обработки.  
3. **Фильтрацию по расширению файла** (`src.endsWith(".png")`).  

Все эти задачи легко реализуются, расширяя цикл из Шага 4.

---

## Заключение

В этом руководстве мы рассмотрели **как выполнять запросы к HTML** в Java от начала до конца: загрузка файла, поиск изображений с помощью XPath и CSS‑селекторов, а также **перебор NodeList Java** для вывода `src` каждого изображения. Теперь у вас есть прочная база для **how to extract images**, и вы точно знаете **how to read HTML file Java** с помощью Aspose.HTML.

Не стесняйтесь адаптировать код под свои задачи скрейпинга — будь то извлечение других атрибутов, работа с тегами `<a>` или передача URL в загрузчик. Схема остаётся той же: загрузить, запросить, перебрать и выполнить действие.

Есть вопросы или хотите поделиться интересным кейсом? Оставляйте комментарий ниже, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}