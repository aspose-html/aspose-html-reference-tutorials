---
category: general
date: 2026-03-04
description: Как подсвечивать HTML, ищя текст в HTML и оборачивая каждое совпадение
  в тег <mark>. Пошаговое руководство на Java по замене текста элементами <mark>.
draft: false
keywords:
- how to highlight html
- search text in html
- highlight word in html
- highlight occurrences of word
- replace text with mark
language: ru
og_description: Как подсвечивать HTML, ищя текст в HTML и оборачивая совпадения тегом
  <mark>. Полный пример на Java для замены текста тегом <mark>.
og_title: Как подсветить HTML – поиск текста и замена на <mark>
tags:
- Aspose.HTML
- Java
- Text Processing
title: Как подсветить HTML — поиск текста и замена на <mark>
url: /ru/java/editing-html-documents/how-to-highlight-html-search-text-replace-with-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выделить HTML – поиск текста и замена на `<mark>`

Когда‑нибудь задавались вопросом **как выделить HTML**, когда определённое слово встречается несколько раз? Возможно, вы создаёте сайт документации, движок блога или просто хотите подчеркнуть название бренда на статической странице. Хорошая новость? Всё довольно просто, как только вы узнаете, как искать текст в HTML и оборачивать результаты элементом `<mark>`.

В этом руководстве мы пройдём полный пример на Java, который загружает HTML‑файл, ищет целевое слово, заменяет каждое его вхождение тегом `<mark>` и, наконец, сохраняет выделенную версию. К концу вы сможете **highlight word in HTML**, **highlight occurrences of word**, и даже **replace text with mark** без нарушения окружающей разметки.

> **Что вам понадобится**  
> • Java 17 или новее (код работает и с более старыми версиями)  
> • Библиотека Aspose.HTML for Java (бесплатная пробная версия или лицензированная копия)  
> • Простой HTML‑файл, который вы хотите обработать  

![Скриншот, показывающий выделенный HTML‑вывод – как выделить html](/images/highlight-html-example.png "пример того, как выделить html")

## Шаг 1 – Загрузка HTML‑документа (Как выделить HTML)

Сначала нам нужно загрузить исходный файл в память. Класс `Document` из Aspose.HTML выполняет всю тяжёлую работу, разбирая разметку в структуру, похожую на DOM, которую мы можем запрашивать.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Load the original HTML file
        Document document = new Document("YOUR_DIRECTORY/article.html");
```

**Почему это важно:** Загрузка документа даёт нам чистую объектную модель, поэтому мы можем безопасно манипулировать текстовыми узлами, не опасаясь нарушить теги или атрибуты. Кроме того, происходит нормализация пробелов, что делает последующий шаг **search text in html** более надёжным.

## Шаг 2 – Поиск текста в HTML для целевого слова

Теперь, когда документ готов, мы будем искать каждое вхождение слова, которое хотим выделить. Метод `searchText` возвращает список объектов `TextMatch`, каждый из которых описывает, где находится совпадение в DOM.

```java
        // Define what we want to highlight
        String searchTerm = "Aspose";

        // Find all matches – this is the core of "search text in html"
        List<TextMatch> matches = document.searchText(searchTerm);
```

**Полезный совет:** По умолчанию поиск чувствителен к регистру. Если нужен поиск без учёта регистра, преобразуйте как текст документа, так и `searchTerm` к одному регистру перед вызовом `searchText`, либо используйте подход на основе регулярных выражений, предоставляемый библиотекой.

## Шаг 3 – Замена текста на `<mark>` (выделение слова в HTML)

Для каждого совпадения мы будем восстанавливать текст содержащего узла, вставляя элемент `<mark>` вокруг точного слова. Это гарантирует, что мы изменяем только целевой текст, а остальная часть HTML остаётся нетронутой.

```java
        // Iterate over each match and wrap it with <mark>
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();

            // Preserve text before and after the match
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;

            // Replace the node's content with the new fragment
            parentNode.setTextContent(highlightedFragment);
        }
```

**Объяснение:**  
- `getStartOffset`/`getEndOffset` дают нам точные позиции символов совпадения внутри его родительского узла.  
- Разделяя оригинальный текст (`textBefore` и `textAfter`), мы сохраняем всё остальное точно в том виде, в каком было.  
- Оборачивание совпадения в `<mark>` — канонический способ **replace text with mark** и получения нативного выделения браузером без дополнительного CSS.

### Особые случаи и советы

- **Несколько совпадений в одном узле:** Цикл обрабатывает каждый `TextMatch` последовательно. Поскольку мы заменяем содержимое всего узла каждый раз, последующие смещения меняются. Aspose.HTML возвращает совпадения в порядке документа, поэтому простая замена работает в большинстве случаев. Если вы столкнётесь с перекрывающимися совпадениями, рассмотрите возможность собрать все совпадения сначала, а затем перестроить узел за один проход.  
- **Элементы, которые не могут содержать сырой HTML:** Если родительский узел — блок `<script>` или `<style>`, вставка `<mark>` нарушит страницу. Вы можете пропустить такие узлы, проверив `parentNode.getNodeName()` перед заменой.

## Шаг 4 – Сохранение выделенного документа (выделение вхождений слова)

После завершения всех замен мы сохраняем изменённый DOM обратно на диск. Выходной файл будет содержать оригинальную разметку плюс новые теги `<mark>`, эффективно **highlighting occurrences of word** “Aspose”.

```java
        // Write the modified HTML back to a new file
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

Откройте `highlighted.html` в любом браузере, и вы увидите каждое слово “Aspose”, обёрнутое в желтоватый фон (стиль по умолчанию для `<mark>`). Если вы предпочитаете кастомный вид, добавьте небольшое правило CSS:

```html
<style>
    mark { background-color: #fffa8b; color: #000; }
</style>
```

## Часто задаваемые вопросы (Search Text in HTML – FAQs)

**В: Что если слово встречается внутри значения атрибута?**  
**О:** `searchText` ищет только в текстовом содержимом узлов, а не в строках атрибутов. Чтобы выделить значения атрибутов, необходимо перебрать элементы и вручную проверить атрибуты.

**В: Можно ли выделить несколько разных слов за один проход?**  
**О:** Конечно. Сформируйте список терминов, пройдитесь по каждому и выполните ту же логику замены. Просто будьте осторожны с перекрывающимися совпадениями.

**В: Работает ли это с тегами, специфичными для HTML5, такими как `<section>` или `<article>`?**  
**О:** Да. Aspose.HTML полностью поддерживает современные элементы HTML5, поэтому обход DOM работает независимо от типа тега.

## Полный рабочий пример (все шаги вместе)

Ниже представлен полный, готовый к запуску Java‑программ, демонстрирующий весь процесс — от загрузки файла до сохранения выделенного результата.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        Document document = new Document("YOUR_DIRECTORY/article.html");

        // Step 2: Search for the word "Aspose"
        String searchTerm = "Aspose";
        List<TextMatch> matches = document.searchText(searchTerm);

        // Step 3: Wrap each found occurrence with a <mark> element
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted HTML fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;
            parentNode.setTextContent(highlightedFragment);
        }

        // Step 4: Save the highlighted document
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

**Ожидаемый результат:** Откройте `highlighted.html`, и вы увидите каждое вхождение “Aspose” выделенным. Другие части страницы не изменены, и файл остаётся корректным HTML‑документом.

## Заключение

Мы рассмотрели **how to highlight HTML** программно **searching text in HTML**, оборачивая каждое совпадение тегом `<mark>` и, наконец, сохраняем изменения. Этот подход позволяет вам **highlight word in HTML**, **highlight occurrences of word**, и **replace text with mark** без написания хрупкого кода для работы со строками.

Следующие шаги? Попробуйте расширить скрипт, добавив:
- Принимать поисковый термин в качестве аргумента командной строки.  
- Генерировать CSS‑файл, определяющий пользовательский цвет выделения.  
- Обрабатывать целую папку HTML‑файлов в одном пакете.  

Эти варианты углубят ваше понимание как Aspose.HTML API, так и общих шаблонов обработки текста.

Если вы столкнётесь с проблемами или у вас есть идеи для дальнейших улучшений, оставьте комментарий ниже. Счастливого выделения!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}