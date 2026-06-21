---
category: general
date: 2026-03-04
description: Вызов Java из JavaScript с помощью Aspose.HTML, выполнение асинхронного
  JavaScript и получение JSON в Java с простым примером. Узнайте, как эффективно использовать
  движок JavaScript.
draft: false
keywords:
- call java from javascript
- run async javascript
- fetch json in java
- asynchronous fetch api
- execute javascript engine
language: ru
og_description: Вызов Java из JavaScript с помощью Aspose.HTML, запуск асинхронного
  JavaScript и получение JSON в Java. Полный код, объяснения и советы включены.
og_title: Вызов Java из JavaScript – пошаговое руководство по асинхронному fetch.
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: Вызов Java из JavaScript — Полное руководство по асинхронному fetch и выполнению
  движка JS
url: /ru/java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Вызов Java из JavaScript – Полный учебник с асинхронным Fetch API

Когда‑нибудь задумывались, как **вызвать Java из JavaScript** не покидая ваше Java‑приложение? Возможно, вы создаёте серверный HTML‑рендерер, или вам нужно открыть некоторую Java‑логику скрипту, который работает внутри документа. Хорошая новость в том, что Aspose.HTML делает это проще простого. В этом руководстве мы не только покажем, как *запускать асинхронный JavaScript* внутри Java‑документа, но и как **получать JSON в Java** с помощью современного **асинхронного fetch API** и, наконец, безопасно выполнять вызовы **JavaScript engine**.

Короче говоря, вы получите полностью готовый пример, который получает JSON‑полезную нагрузку с публичного эндпоинта, передаёт её Java‑хост‑объекту и выводит результат в консоль. Никаких внешних веб‑серверов, никаких дополнительных библиотек — только чистый Java и Aspose.HTML.

## Что вы узнаете

- Как создать пустой HTML‑документ с помощью Aspose.HTML.  
- Как получить и **execute JavaScript engine** из Java.  
- Как зарегистрировать Java‑хост‑объект, который может вызываться из JavaScript.  
- Как написать **asynchronous JavaScript** функцию, использующую **asynchronous fetch API**.  
- Как обработать полученные данные в Java с помощью чистого callback‑а.  
- Ожидаемый вывод и советы по устранению неполадок.

### Требования

- Java 17 или новее (код также компилируется на JDK 11).  
- Aspose.HTML for Java 23.7 (или последняя версия на момент написания).  
- Базовое знакомство с Java и обещаниями JavaScript (promises).  
- Доступ в Интернет для демонстрационного запроса к `jsonplaceholder`.

Если что‑то из перечисленного вам незнакомо, не паникуйте — каждый шаг объяснён простым английским, и вы точно увидите, почему делаем именно так.

---

## Шаг 1 – Создать пустой HTML‑документ и получить его JavaScript‑движок

Первое, что нам нужно, — это пустой документ, предоставляющий изолированную среду JavaScript. Класс `Document` из Aspose.HTML делает именно это.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Create an empty HTML document
        Document document = new Document();

        // Obtain the JavaScript engine associated with the document's window
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();
```

**Почему это важно:** Объект `Document` имитирует окно браузера, а его `JavaScriptEngine` позволяет запускать скрипты точно так же, как в браузере. Это фундамент для **call java from javascript** — движок выступает в роли моста.

---

## Шаг 2 – Зарегистрировать хост‑объект, чтобы JavaScript мог вызывать Java

Aspose.HTML позволяет открыть любой Java‑объект для скриптового мира. Мы создадим анонимный класс с единственным методом `onResult`, который просто выводит любой полученный JSON.

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**Explanation:**  
- `addHostObject` привязывает имя `javaCallback` к анонимному Java‑объекту.  
- Внутри JavaScript мы будем вызывать `javaCallback.onResult(...)`.  
- Это ядро **call java from javascript** — скрипт «запрыгивает» в Java, а Java реагирует.

> **Pro tip:** Делайте методы хост‑объекта `public` и простыми; сложные объекты могут вызвать проблемы сериализации.

---

## Шаг 3 – Написать асинхронную JavaScript‑функцию с использованием асинхронного Fetch API

Теперь самая интересная часть: небольшой скрипт, который получает JSON с удалённого эндпоинта. Мы используем `async/await`, что является современным способом **run async JavaScript**.

```java
        // Asynchronous script that fetches JSON and passes it to the Java host object
        String asyncScript =
            "async function fetchData() {" +
            "  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "  const json = await response.json();" +
            "  javaCallback.onResult(JSON.stringify(json));" +
            "}" +
            "fetchData();";
```

**Why we choose `fetch` over older XHR:**  
- `fetch` возвращает `Promise`, делая код чище.  
- Он работает нативно с `await`, поэтому поток читается сверху вниз — идеально для демонстраций **asynchronous fetch api**.  
- API «будущее‑защищённый»; большинство браузеров и движков (включая Aspose) поддерживают его из коробки.

---

## Шаг 4 – Выполнить скрипт внутри JavaScript‑движка документа

Наконец, передаём скрипт движку. Движок запустит крошечный цикл событий, разрешит `fetch`‑промис и вызовет обратный вызов в Java, когда всё будет готово.

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

Когда вы запустите класс `AsyncJsTutorial`, вы должны увидеть примерно следующее:

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Этот вывод подтверждает три вещи:

1. **asynchronous fetch API** успешно получил данные.  
2. JSON был сериализован и передан в Java.  
3. Наш вызов **execute javascript engine** завершился без взаимных блокировок.

---

## Шаг 5 – Обработка ошибок и крайних случаев (опциональные улучшения)

В реальном коде всё редко работает идеально каждый раз. Ниже перечислены распространённые подводные камни и способы их избежать.

### 5.1 Сетевые сбои

Если удалённый сервер недоступен, `fetch` бросает исключение. Оберните вызов в блок `try/catch`:

```java
String asyncScript =
    "async function fetchData() {" +
    "  try {" +
    "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
    "    if (!response.ok) throw new Error('Network response was not ok');" +
    "    const json = await response.json();" +
    "    javaCallback.onResult(JSON.stringify(json));" +
    "  } catch (e) {" +
    "    javaCallback.onResult('Error: ' + e.message);" +
    "  }" +
    "}" +
    "fetchData();";
```

Теперь Java‑сторона получит сообщение об ошибке вместо зависания.

### 5.2 Тайм‑ауты

Движок Aspose не предоставляет нативный тайм‑аут для `fetch`, но вы можете реализовать его в JavaScript:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 Множественные вызовы

Если нужно получить несколько ресурсов, просто выполните цикл или `map` по массиву URL‑ов. Хост‑объект можно расширить, чтобы принимать идентификатор и сопоставлять ответы.

---

## Полный рабочий пример

Ниже представлен **полный исходный файл**, который можно скопировать‑вставить в свою IDE. Нет скрытых зависимостей, только JAR Aspose.HTML в classpath.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty HTML document and obtain its JavaScript engine
        Document document = new Document();
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();

        // Step 2: Register a host object that JavaScript can call back into Java
        jsEngine.addHostObject("javaCallback", new Object() {
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });

        // Step 3: Write an async function that uses the asynchronous fetch API
        String asyncScript =
            "async function fetchData() {" +
            "  try {" +
            "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "    if (!response.ok) throw new Error('Network error');" +
            "    const json = await response.json();" +
            "    javaCallback.onResult(JSON.stringify(json));" +
            "  } catch (e) {" +
            "    javaCallback.onResult('Error: ' + e.message);" +
            "  }" +
            "}" +
            "fetchData();";

        // Step 4: Execute the script inside the document's JavaScript engine
        jsEngine.execute(asyncScript);
    }
}
```

**Expected console output**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Если вы видите строку ошибки, начинающуюся с `Error:`, значит что‑то пошло не так — скорее всего, сетевой сбой.

---

## Визуальный обзор

![Диаграмма, показывающая, как Java вызывает JavaScript и получает результаты асинхронного fetch – call java from javascript](/images/java-js-async.png)

*На изображении показан поток: Java → JavaScriptEngine → async fetch → JavaCallback.*

---

## Часто задаваемые вопросы

**Можно ли использовать этот подход с другими JavaScript‑движками?**  
Да, любой движок, предоставляющий механизм хост‑объекта (например, Nashorn, GraalVM), может работать, но Aspose.HTML даёт полностью укомплектованную браузероподобную среду с встроенным `fetch`.

**Что если мне нужно вернуть сложный Java‑объект вместо строки?**  
Вы можете сериализовать объект в JSON на стороне Java и дать JavaScript его распарсить, либо открыть несколько методов в хост‑объекте для получения отдельных полей.

**Является ли реализация `fetch` полностью соответствующей стандарту?**  
Aspose.HTML реализует WHATWG Fetch Standard, поэтому вы получаете корректную обработку редиректов, CORS и потоков.

**Блокирует ли это Java‑поток во время ожидания сети?**  
Нет. Вызов `execute` возвращается сразу, а внутренний движок обрабатывает промис асинхронно. Однако главный поток будет жив до завершения скрипта или пока вы явно не остановите движок.

---

## Заключение

Мы только что прошли практический сценарий, позволяющий **вызвать Java из JavaScript**, **запускать async JavaScript** и **получать JSON в Java** с помощью **asynchronous fetch API**. Создав хост‑объект, написав аккуратную `async`‑функцию и выполнив её через **JavaScript engine** Aspose.HTML, вы получаете чистый, неблокирующий мост между двумя средами выполнения.

Попробуйте, измените URL или добавьте больше обратных вызовов — ваша фантазия единственное ограничение. Дальше вы можете исследовать:

- **Executing JavaScript engine** с несколькими одновременно работающими скриптами.  
- Использование **run async javascript** для параллельной обработки больших наборов данных.  
- Интеграцию этого паттерна в веб‑сервис, который динамически рендерит HTML «на лету».

Экспериментируйте, и не стесняйтесь оставить комментарий, если столкнётесь с неожиданной проблемой. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}