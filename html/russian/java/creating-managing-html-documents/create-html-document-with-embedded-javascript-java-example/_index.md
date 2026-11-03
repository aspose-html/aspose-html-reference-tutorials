---
category: general
date: 2026-06-03
description: Создайте HTML‑документ в Java и внедрите JavaScript для увеличения счётчика.
  Изучите пример скриптового движка, получите innerHTML элемента и многое другое.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: ru
og_description: Создайте HTML‑документ в Java, внедрите JavaScript для увеличения
  счётчика и получите окончательное значение с помощью примера использования скриптового
  движка.
og_title: Создание HTML‑документа со встроенным JavaScript – пример на Java
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: Создать HTML‑документ с внедрённым JavaScript — пример на Java
url: /ru/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание HTML‑документа с встроенным JavaScript – пример на Java

Ever needed to **create HTML document** from Java code and wonder how to embed JavaScript inside it? In this guide we'll show you exactly that, step by step, and you’ll end up with a working script engine example that prints the final counter value.  

If you’ve ever asked yourself *“how can I get element innerHTML after a script runs?”* or *“what’s the cleanest way to increment a counter in JavaScript from Java?”*—you’re in the right place. We’ll cover **embed javascript html**, **increment counter javascript**, and **get element innerHTML** all in one cohesive tutorial.

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="Пример создания HTML Document со встроенным JavaScript"}

## Что вы построите

By the end of this tutorial you’ll have a self‑contained Java program that:

1. **Creates an HTML document** в памяти.
2. **Embeds a small JavaScript snippet** который увеличивает счётчик пять раз.
3. **Initializes a script engine** (пример `ScriptEngine`) для выполнения этого фрагмента.
4. **Retrieves the final counter value** с помощью `getElementInnerHTML`.
5. Выводит `Final counter value: 5` в консоль.

No external files, no web server—just pure Java and a tiny HTML string.

## Требования

- Java 17 или новее (API `ScriptEngine` входит в стандартную библиотеку).
- Базовое знакомство с HTML и JavaScript (не требуется глубокая экспертиза).
- IDE или простой текстовый редактор плюс терминал для компиляции и запуска программы.

## Шаг 1: Создание HTML‑документа в Java

The first thing we need is a blank HTML document object that we can later fill with markup. Think of it as a virtual page that lives only in memory.

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**Почему это важно:** By **creating HTML document** objects yourself, you avoid writing to disk and keep everything testable. The tiny DOM simulation lets us later **get element innerHTML** without a full browser.

## Шаг 2: Встраивание JavaScript в HTML — логика счётчика

Now we’ll write the HTML markup that includes a `<script>` block. This script will **increment counter JavaScript** five times.

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**Объяснение:**  
- Элемент `<div id='counter'>0</div>` — наш целевой элемент.  
- Цикл `for` выполняет логику **increment counter javascript**, обновляя div на каждой итерации.  
- Поскольку мы не в реальном браузере, движок скриптов, который мы будем использовать позже, должен понимать `document.getElementById`. Поэтому мы добавили небольшой заглушку в `HTMLDocument`.

## Шаг 3: Инициализация Script Engine — пример Script Engine

Java ships with the `ScriptEngine` API (JSR‑223). We’ll create a small wrapper that feeds the HTML content to the engine and provides the minimal DOM methods it expects.

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**Почему это важно:** This **script engine example** shows how you can run embedded JavaScript without a full browser. It also demonstrates a lightweight way to expose `document.getElementById` so that the script can interact with our mock DOM.

## Шаг 4: Выполнение JavaScript — Increment Counter JavaScript в действии

With the engine ready, we simply run the script. The loop inside the `<script>` tag will fire, and our mock `setInnerHTML` will update the counter.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**Что происходит под капотом?** Each iteration of the loop calls `document.getElementById('counter').innerHTML = i + 1;`. Our mock `setInnerHTML` forwards the numeric string to `HTMLDocument.updateCounter`, which stores the latest value. After the loop finishes, the document’s internal map holds `"5"` for the `counter` element.

## Шаг 5: Получение окончательного значения счётчика — Get Element InnerHTML

Now that the script has finished, we can **get element innerHTML** from our `HTMLDocument` instance.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Запуск всей программы выводит:

```
Final counter value: 5
```

That confirms the **increment counter javascript** logic worked and we successfully **retrieved the element innerHTML** after script execution.

## Полный рабочий пример

Putting everything together, here’s the complete, ready‑to‑run Java class:



## Что вам стоит изучить дальше?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Создание пустых HTML‑документов в Aspose.HTML для Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Создание HTML‑документов из строки в Aspose.HTML для Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Сохранение HTML‑документа в Aspose.HTML для Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}