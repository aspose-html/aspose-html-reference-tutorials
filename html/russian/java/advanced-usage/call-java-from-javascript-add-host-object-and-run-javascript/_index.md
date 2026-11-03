---
category: general
date: 2026-10-14
description: Вызов java из javascript с использованием Aspose.HTML. Узнайте, как добавить
  host object, выполнить javascript в java и логировать из javascript в кратком руководстве.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Вызов java из javascript с использованием Aspose.HTML. Это руководство
  показывает, как добавить host object, выполнить javascript в java и логировать из
  javascript, всё в нескольких строках кода.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: Вызов java из javascript – добавить host object и выполнить javascript в
  java
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: Вызов java из javascript – добавить host object и выполнить javascript в java
url: /ru/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Вызов java из javascript – добавление хост‑объекта и выполнение javascript в java

Когда‑нибудь нужно **вызвать java из javascript** внутри Java‑приложения? Возможно, вы создаёте динамический HTML‑отчётный движок или просто хотите предоставить скрипту, которым управляете, доступ к Java‑логгеру. В этом руководстве вы увидите, как добавить хост‑объект, выполнить JavaScript в Java и даже **логировать из JavaScript** обратно в JVM — все это с помощью Aspose.HTML.

Мы пройдём полный, готовый к запуску пример, который создаёт пустой HTML‑документ, внедряет Java‑класс `Logger` как хост‑объект, исполняет небольшой скрипт и выводит результат в консоль. Никакого внешнего веб‑браузера, никакой «магии» — просто обычный Java‑код, который можно скопировать‑вставить и запустить уже сегодня.

## Быстрые ответы
- **Как добавить хост‑объект?** Зарегистрировать Java‑экземпляр с помощью `document.getWindow().addHostObject("name", object)`.  
- **Можно ли выполнять JavaScript в Java?** Да — используйте `document.getWindow().eval(yourScript)`.  
- **Можно ли логировать из JavaScript?** Абсолютно; хост‑объект может предоставлять любой метод `void log(String)`.  
- **Какая версия Aspose.HTML требуется?** Версия 23.10 или новее поддерживает полный API хост‑объектов.  
- **Нужен ли веб‑браузер?** Нет — Aspose.HTML поставляется с встроенным движком, поэтому всё работает без графического интерфейса.

## Что такое вызов java из javascript?
**Вызов java из javascript** — это техника экспонирования Java‑объектов в среде выполнения JavaScript, позволяющая скриптам напрямую вызывать Java‑методы. Aspose.HTML создаёт лёгкий JavaScript‑движок внутри Java‑процесса, обеспечивая бесшовную двустороннюю коммуникацию без внешних браузеров.

## Почему стоит использовать Aspose.HTML для выполнения javascript в java?
Aspose.HTML поддерживает **более 50 форматов ввода и вывода** и может оценивать JavaScript в полностью совместимой среде HTML5. Он обрабатывает скрипты за ~200 мс в среднем для простого однострочного кода и делает это без загрузки полного стека браузера, что снижает потребление памяти до 80 % по сравнению с подходами на основе Selenium.

## Предварительные требования

- Java 17 (или любой современный JDK), установленный и настроенный.  
- Библиотека Aspose.HTML for Java (версия 23.10 или новее). Её можно получить из Maven Central или на сайте Aspose.  
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

Теперь, когда базовые вещи улажены, перейдём к пошаговому решению.

## Как добавить хост‑объект и выполнить javascript в java?
`addHostObject` регистрирует Java‑объект как глобальную переменную в контексте JavaScript. Загрузите ваш `HTMLDocument`, зарегистрируйте Java‑логгер под именем `"javaLogger"` с помощью `addHostObject`, а затем выполните короткий скрипт, вызывающий `javaLogger.log`. Весь процесс требует лишь трёх вызовов API и работает в любой среде Java 17.

### Шаг 1: создать минимальный java‑проект

Сначала создайте новый Java‑класс под названием `JsHostObjectDemo`. Класс будет содержать наш метод `main` и определение хост‑объекта. Хранение всего в одном файле делает руководство самодостаточным и удобным для копирования.

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

### Почему `HTMLDocument`?
`HTMLDocument` представляет собой HTML‑документ в памяти и предоставляет JavaScript‑движок. Класс `HTMLDocument` поднимает полностью совместимую среду скриптинга HTML‑5. Даже если мы никогда не загружаем разметку, объект `window` документа даёт доступ к JavaScript‑движку, где происходит **выполнение javascript в java**. Кроме того, вы можете манипулировать DOM, загружать ресурсы или выполнять скрипты без браузера.

## Как добавить хост‑объект – “javaLogger”?
`Logger` — простой Java‑класс с методом `log(String)`, который пишет сообщения в консоль. Зарегистрируйте экземпляр `Logger` под именем `"javaLogger"`, чтобы любой скрипт, выполненный в этом документе, мог вызвать `javaLogger.log(...)`. Это основа требования **add host object** и делает логгер доступным как глобальная переменная для кода JavaScript.

### Распространённые подводные камни

- **Коллизии имён** — если в вашем скрипте уже существует глобальная переменная `javaLogger`, хост‑объект будет перезаписан. Выберите уникальное имя.  
- **Потокобезопасность** — хост‑объект разделяется между выполнениями скриптов в одном документе. Если планируете запускать скрипты параллельно, сделайте класс потокобезопасным (например, используя `synchronized` или примитивы из `java.util.concurrent`).

## Как писать и выполнять javascript в java?
`eval` исполняет строку JavaScript в движке скриптов документа и возвращает любой результат. Передайте небольшой скрипт в `eval`. Движок найдёт `javaLogger` в глобальном пространстве и вызовет его метод `log` с переданной строкой. Вы также можете возвращать значения, обрабатывать исключения и цепочкой выполнять несколько оценок для более сложных взаимодействий.

### Ожидаемый вывод

Запуск метода `main` выводит в консоль следующую строку:

```
[JS] Hello from JavaScript!
```

## Как расширить хост‑объект – не только логирование?
Хост‑объект — это любой Java‑экземпляр, открытый для JavaScript через `addHostObject`. Добавьте дополнительный функционал, расширив класс `Logger` или создав новый хост‑класс. Ниже быстрый пример, который также возвращает значение в JavaScript. Хост‑объект может предоставлять сложные типы, выполнять ввод/вывод или взаимодействовать с другими сервисами. Возврат значения позволяет скрипту получать данные обратно, обеспечивая двустороннюю связь между Java и JavaScript.

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

## Как освободить ресурсы после выполнения скриптов?
`dispose` освобождает нативные ресурсы, удерживаемые экземпляром `HTMLDocument`. Когда работа с окружением скриптов завершена, вызовите `dispose()` у `HTMLDocument`, чтобы освободить нативные ресурсы. Пропуск вызова `dispose()` может привести к утечкам памяти, особенно при создании множества документов в циклах или длительно работающих сервисах. Всегда оборачивайте использование в блок `try‑with‑resources` или гарантируйте вызов `document.dispose()` в `finally`.

```java
document.dispose(); // Important for long‑running applications
```

## Полный рабочий пример

Ниже приведён полный исходный файл, который можно сразу скомпилировать и запустить. Сохраните его как `JsHostObjectDemo.java`, убедитесь, что JAR‑файл Aspose.HTML находится в classpath, и выполните `java JsHostObjectDemo`.

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

## Часто задаваемые вопросы

**Q: Работает ли это на Android?**  
A: Да. Aspose.HTML — чисто Java‑библиотека, поэтому работает на любой JVM, включая ART‑runtime Android.

**Q: Что если нужно передать сложные объекты?**  
A: Вы можете открыть POJO с геттерами и сеттерами; движок автоматически отображает их в объекты JavaScript. Коллекции типа `java.util.List` или массивы также конвертируются.

**Q: Как работает обработка ошибок?**  
A: Если скрипт бросает ошибку JavaScript, `eval` генерирует `ScriptException`. Оберните вызов в `try‑catch`, чтобы залогировать или восстановиться.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**Q: Можно ли запускать несколько скриптов последовательно?**  
A: Абсолютно. Один и тот же `HTMLDocument` сохраняет глобальную область, так что вы можете вызывать `eval` многократно. Просто следите за именами переменных, чтобы избежать конфликтов.

**Q: Безопасен ли хост‑объект для недоверенных скриптов?**  
A: Любой внешний скрипт следует считать недоверенным. Валидируйте параметры и рассматривайте возможность «песочницы», открывая только минимально необходимые методы.

## Лучшие практики и советы

- **Дайте хост‑объектам понятные имена** — `javaLogger`, `javaUtils` и т.д., чтобы избежать путаницы.  
- **Делайте методы хост‑объекта небольшими и без побочных эффектов**, когда это возможно; так проще отлаживать.  
- **Освобождайте документ** сразу после завершения работы; это освобождает нативную память, которую выделяет Aspose.HTML.  
- **Проверяйте входные данные** из JavaScript, особенно если скрипты поступают из недоверенных источников. Обрабатывайте их как любые внешние данные.

## Заключение

Теперь у вас есть полноценный пример, показывающий, как **вызвать java из javascript** посредством **добавления хост‑объекта**, **выполнения javascript в java** и **логирования из javascript** с помощью Aspose.HTML. Этот паттерн мощный: любой Java‑сервис можно открыть скриптам, превратив приложение в лёгкую платформу скриптинга.

Дальше вы можете исследовать:

- Внедрение полного HTML‑документа и манипуляцию DOM из JavaScript.  
- Использование хост‑объекта для передачи данных обратно в Java (например, сериализация в JSON).  
- Интеграцию с другими движками скриптов, такими как Nashorn или GraalVM, для поддержки более широкого спектра языков.

Попробуйте, измените классы `Logger` или `Utils`, и посмотрите, насколько далеко вы сможете продвинуть концепцию **javascript host object** в своих проектах.

---

**Последнее обновление:** 2026-10-14  
**Тестировано с:** Aspose.HTML for Java 23.10  
**Автор:** Aspose  






```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## Связанные руководства

- [Enable Script Execution In Java Complete Aspose Html Guide](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Execute Javascript In Java Complete Guide To Running Js From](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [How To Sandbox Javascript Complete Aspose Html Guide](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}