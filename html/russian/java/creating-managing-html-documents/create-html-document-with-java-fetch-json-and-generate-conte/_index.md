---
category: general
date: 2026-02-11
description: Создайте HTML‑документ в Java с помощью Aspose.HTML. Узнайте, как получать
  JSON‑JavaScript, добавлять элемент script, генерировать HTML из JSON и преобразовывать
  JSON в pre.
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: ru
og_description: Создайте HTML‑документ на Java с помощью Aspose.HTML. Получите JSON‑JavaScript,
  добавьте элемент script, сгенерируйте HTML из JSON и преобразуйте JSON в pre — всё
  в одном руководстве.
og_title: Создание HTML‑документа в Java – Полное руководство
tags:
- Aspose.HTML
- Java
- Web Automation
title: Создание HTML‑документа с помощью Java – получение JSON и генерация контента
url: /ru/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать HTML‑документ – Полный учебник по Java

Когда‑нибудь вам нужно было **create HTML document** «на лету», но вы не знали, как подтянуть удалённые данные? Вы не одиноки. Во многих проектах требуется получить JSON с помощью JavaScript, внедрить результат в страницу и затем сохранить окончательную разметку как статический файл. Это руководство покажет, как сделать именно это с помощью Aspose.HTML for Java.

Мы пройдём каждый шаг: от создания пустого документа, до **fetch JSON JavaScript**, до **add script element**, и, наконец, до **generate HTML from JSON** и **convert JSON to pre** тегов. В конце у вас будет готовый к использованию `fetchResult.html`, содержащий полученные данные в виде красиво отформатированного JSON.

## Предварительные требования

- Java 17 или новее (код также компилируется с JDK 11+)
- Библиотека Aspose.HTML for Java (доступна через Maven Central)
- Базовое знакомство с HTML и асинхронным JavaScript
- IDE или обычные команды `javac`/`java`

Никакие дополнительные фреймворки не требуются — всё работает локально.

## Шаг 1: Настройка проекта и импорт Aspose.HTML

Сначала добавьте зависимость Aspose.HTML в ваш `pom.xml` (или скачайте JAR вручную).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **Pro tip:** Держите номер версии актуальным; новые релизы исправляют ошибки и улучшают движок скриптов.

## Шаг 2: **Create HTML Document** – пустой холст

Мы начинаем с создания пустого `HTMLDocument`. Представьте его как чистую страницу, в которую позже вставим наш скрипт.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

Зачем нам объект документа? `ScriptEngine` из Aspose.HTML работает с DOM, а не с простой строкой. Создавая корректный документ, мы предоставляем движку реальную среду для выполнения нашего **fetch JSON JavaScript**.

## Шаг 3: Написать фрагмент JavaScript – **Fetch JSON JavaScript** и **Convert JSON to pre**

Сердце учебника находится в этой многострочной строке. Она выполняет асинхронный `fetch`, парсит JSON, а затем записывает элемент `<pre>` с красиво отформатированными данными.

```java
        // Step 3: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;
```

Обратите внимание на комментарий *Convert JSON to <pre>* — именно это делает вызов `JSON.stringify(..., null, 2)`. Он добавляет отступы, делая вывод удобочитаемым.

## Шаг 4: **Add Script Element** в документ

Теперь мы создаём тег `<script>`, помещаем в него наш код и прикрепляем его к `<body>`. Это и есть часть **add script element**.

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

Почему именно к `<body>`? В реальном браузере скрипт выполнится сразу после парсинга. Добавляя его в DOM, мы имитируем именно такое поведение, гарантируя, что асинхронный fetch запустится, когда мы позже вызовем движок.

## Шаг 5: Запуск Script Engine – дать асинхронному fetch завершиться

Aspose.HTML предоставляет `ScriptEngine`, способный выполнять JavaScript, основанный на DOM. Мы вызываем `run()` и ждём, пока цепочка промисов завершится.

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

Движок блокирует выполнение, пока все отложенные задачи (наш fetch) не будут завершены, гарантируя, что сгенерированный HTML уже содержит данные.

## Шаг 6: **Generate HTML from JSON** – сохранить результат

Наконец мы сохраняем документ на диск. Файл теперь содержит блок `<pre>` с JSON‑полезной нагрузкой.

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

Запуск программы создаёт `fetchResult.html`. Откройте его в любом браузере, и вы увидите примерно следующее:

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

Это результат **generate HTML from JSON**, который вы искали.

## Полный рабочий пример

Ниже приведён полностью готовый к запуску исходный файл. Скопируйте, вставьте, при необходимости измените путь вывода и запустите `java JsFetchExample`.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();

        // Step 2: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;

        // Step 3: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);

        // Step 4: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();

        // Step 5: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

## Ожидаемый вывод и проверка

1. **Консоль:** Вы увидите `HTML with fetched data saved.`  
2. **Файл (`fetchResult.html`):** При открытии он отображает JSON внутри блока `<pre>`, красиво отформатированного.  
3. **Проверка:** Если посмотреть исходный код страницы, вы найдёте только элемент `<pre>` — никаких лишних тегов `<script>` не осталось, поскольку движок уже выполнил их.

## Часто задаваемые вопросы и особые случаи

| Question | Answer |
|----------|--------|
| *What if the API returns an error?* | Wrap the `fetch` call in a `try…catch` block and write an error message to the body instead of the JSON. |
| *Can I fetch multiple resources?* | Yes—just chain additional `await fetch(...)` calls or use `Promise.all`. The final `innerHTML` can concatenate several `<pre>` blocks. |
| *Do I need to set CORS headers?* | Since the script runs inside Aspose.HTML’s sandbox, it respects the same‑origin policy. The public JSONPlaceholder endpoint already allows cross‑origin requests. |
| *How to change the output directory at runtime?* | Pass the path as a command‑line argument (`args[0]`) and replace the hard‑coded string in `htmlDoc.save`. |
| *Is there a way to embed CSS for styling?* | Absolutely. Create a `<style>` element, set its `textContent` to your CSS, and append it to `<head>` before running the engine. |

## Советы для продакшн‑использования

- **Cache the JSON** if the endpoint is slow; you can write the fetched string to a file and reuse it.  
- **Sanitize the data** before injecting it, especially if the source isn’t trusted. Use `JSON.stringify` safely or escape HTML entities.  
- **Configure the ScriptEngine timeout** (`scriptEngine.setTimeout(5000)`) to avoid hanging on unresponsive services.  

## Визуальное резюме

![пример создания html‑документа, показывающий сгенерированный HTML с JSON внутри тега pre](fetchResult.png "Скриншот сгенерированного HTML‑документа")

*Alt text:* *пример создания html‑документа – сгенерированный HTML‑файл, отображающий полученный JSON внутри элемента pre.*

## Заключение

Теперь вы знаете, как **create HTML document** программно в Java, **fetch JSON JavaScript**, **add script element**, **generate HTML from JSON** и **convert JSON to pre** для читаемого вывода. Весь процесс работает офлайн, требует только Aspose.HTML и создаёт чистый статический файл, который можно разместить где угодно.

Далее попробуйте расширить скрипт: пройтись по массиву объектов, добавить CSS‑стили или генерировать несколько страниц одной техникой. Вы также можете заменить URL в `fetch` на свой собственный API, чтобы превратить динамические данные в статические снимки — идеально для SEO‑дружелюбного предварительного рендеринга.

Счастливого кодинга, и делитесь своими экспериментами в комментариях!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}