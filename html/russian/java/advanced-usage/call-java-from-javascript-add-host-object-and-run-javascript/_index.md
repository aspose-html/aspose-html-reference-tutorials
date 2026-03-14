---
category: general
date: 2026-03-14
description: Узнайте, как вызывать Java из JavaScript с помощью Aspose.HTML. Это руководство
  показывает, как добавить объект‑хост, выполнить JavaScript в Java и вести журнал
  из JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: ru
og_description: Вызов Java из JavaScript с помощью Aspose.HTML. Добавьте объект хоста,
  выполните JavaScript в Java и выводите сообщения из JavaScript в одном учебнике.
og_title: Вызов Java из JavaScript — полное руководство с объектом‑хостом
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Вызов Java из JavaScript – добавление хост‑объекта и выполнение JavaScript
  в Java
url: /ru/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

block placeholders unchanged.

Also keep markdown formatting.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Вызов Java из JavaScript – Добавление хост‑объекта и выполнение JavaScript в Java

Когда‑нибудь нужно было **вызвать Java из JavaScript** внутри Java‑приложения? Возможно, вы создаёте динамический движок HTML‑отчётов или просто хотите предоставить Java‑логгер скрипту, которым управляете. В этом руководстве вы увидите, как добавить хост‑объект, выполнить JavaScript в Java и даже **логировать из JavaScript** обратно в JVM — всё с помощью Aspose.HTML.

Мы пройдем через полностью готовый пример, который создаёт пустой HTML‑документ, внедряет Java‑класс `Logger` в качестве хост‑объекта, выполняет небольшой скрипт и выводит результат в консоль. Никакого внешнего веб‑браузера, никакой «магии» — просто обычный Java‑код, который можно скопировать‑вставить и запустить уже сегодня.

## Prerequisites

- Java 17 (или любой современный JDK), установленный и настроенный.
- Библиотека Aspose.HTML for Java (версия 23.10 или новее). Вы можете получить её из Maven Central или с сайта Aspose.
- Простой IDE или текстовый редактор; пример также работает из командной строки.

> **Pro tip:** Если вы используете Maven, добавьте следующую зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Или для Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Теперь, когда основы улажены, давайте погрузимся в пошаговое решение.

## Step 1: Create a Minimal Java Project

Сначала создайте новый Java‑класс под названием `JsHostObjectDemo`. Класс будет содержать наш метод `main` и определение хост‑объекта. Хранение всего в одном файле делает руководство самодостаточным и простым для копирования.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### Why an `HTMLDocument`?

Класс `HTMLDocument` из Aspose.HTML поднимает полноценную среду скриптов, совместимую с HTML‑5. Даже если мы никогда не загружаем разметку, объект `window` документа даёт доступ к JavaScript‑движку, где происходит магия **run JavaScript in Java**.

## Step 2: Add the Host Object – “javaLogger”

Строка

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

выполняет основную работу для требования **add host object**. Регистрируя экземпляр `Logger` под именем `"javaLogger"`, любой скрипт, выполненный в этом документе, может вызвать `javaLogger.log(...)`. Это ядро концепции **javascript host object**: мост, позволяющий JavaScript обращаться к JVM.

### Common Pitfalls

- **Naming collisions** – Если в вашем скрипте уже существует глобальная переменная `javaLogger`, хост‑объект будет перезаписан. Выберите уникальное имя.
- **Thread safety** – Хост‑объект разделяется между выполнениями скриптов в одном документе. Если планируете запускать скрипты параллельно, сделайте класс потокобезопасным (например, используйте `synchronized` или примитивы из `java.util.concurrent`).

## Step 3: Write and Execute JavaScript

Скрипт, который мы передаём в `eval`, преднамеренно маленький:

```javascript
javaLogger.log('Hello from JavaScript!');
```

Когда вызывается `document.getWindow().eval(script)`, движок ищет `javaLogger` в глобальной области, находит добавленный нами Java‑объект и вызывает его метод `log` с переданной строкой.

### Expected Output

Запуск метода `main` выводит следующую строку в консоль:

```
[JS] Hello from JavaScript!
```

Эта крошечная строка доказывает, что мы успешно **call java from javascript**, а **log from javascript** появляется точно там, где обычно выводится сообщение Java `System.out`.

## Step 4: Extending the Host – More Than Just Logging

Если нужно открыть дополнительный функционал (например, доступ к файлам, запросы к базе данных), просто добавьте новые методы в класс `Logger` — или создайте совершенно новый хост‑класс. Ниже быстрый пример, который также возвращает значение:

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

Теперь консоль показывает:

```
[JS] 3+4=7
```

Это демонстрирует гибкость паттерна **javascript host object**: вы можете открыть любой Java‑API, который нужен, при условии, что типы данных конвертируемы между Java и JavaScript (примитивы, строки, массивы и т.д.).

## Step 5: Clean Up Resources

Когда работа со средой скриптов завершена, освободите `HTMLDocument`, чтобы освободить нативные ресурсы:

```java
document.dispose(); // Important for long‑running applications
```

Пропуск освобождения может привести к утечкам памяти, особенно если вы создаёте много документов в цикле.

## Full Working Example

Ниже полный исходный файл, который можно сразу скомпилировать и запустить. Сохраните его как `JsHostObjectDemo.java`, убедитесь, что JAR‑файл Aspose.HTML находится в classpath, и выполните `java JsHostObjectDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

Запуск этой программы выдаёт:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

Это весь рабочий процесс **call java from javascript** в нескольких строках.

## Frequently Asked Questions

### Does this work on Android?

Aspose.HTML — чисто Java‑библиотека, поэтому работает на любой JVM, включая Dalvik/ART Android. Просто включите JAR, и возможности хост‑объекта будут доступны.

### What if I need to pass complex objects?

Можно открыть POJO (plain old Java objects) с полями, геттерами и сеттерами. Движок автоматически сопоставит их с объектами JavaScript. Для коллекций используйте `java.util.List` или массивы — оба конвертируются.

### How does error handling work?

Если скрипт бросает ошибку JavaScript, `eval` пробросит `ScriptException`. Оберните вызов в блок try‑catch, чтобы залогировать или восстановиться:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Can I run multiple scripts sequentially?

Конечно. Один и тот же экземпляр `HTMLDocument` сохраняет глобальную область, поэтому можно вызывать `eval` многократно. Просто следите за конфликтами имён переменных между скриптами.

## Best Practices & Tips

- **Name your host objects clearly** — `javaLogger`, `javaUtils` и т.п. — чтобы избежать путаницы.
- **Keep host methods small and side‑effect free** по возможности; это упрощает отладку.
- **Dispose of the document** как можно скорее; это освобождает нативную память, которую выделяет Aspose.HTML.
- **Validate inputs** из JavaScript, особенно если скрипты поступают из ненадёжных источников. Обрабатывайте их как любые внешние данные.

## Conclusion

Теперь у вас есть надёжный сквозной пример того, как **call java from javascript** с помощью **adding a host object**, **running JavaScript in Java** и **logging from JavaScript** при использовании Aspose.HTML. Этот паттерн мощный: любой Java‑сервис можно открыть скриптам, превратив ваше Java‑приложение в лёгкую скриптовую платформу.

Далее вы можете изучить:

- Внедрение полной HTML‑страницы и манипуляцию DOM из JavaScript.
- Использование хост‑объекта для передачи данных обратно в Java (например, сериализация в JSON).
- Интеграцию с другими скриптовыми движками, такими как Nashorn или GraalVM, для более широкого спектра языков.

Попробуйте, измените классы `Logger` или `Utils`, и посмотрите, насколько далеко вы сможете продвинуть концепцию **javascript host object** в своих проектах

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}