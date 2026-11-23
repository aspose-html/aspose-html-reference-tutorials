---
category: general
date: 2026-02-16
description: Узнайте, как запускать JavaScript в Java с использованием CompletableFuture,
  задерживать JS и выполнять асинхронный код. Полное пошаговое руководство по асинхронной
  оценке JavaScript.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: ru
og_description: Освойте, как запускать JavaScript из Java, откладывать выполнение
  JS и оценивать асинхронный код с помощью CompletableFuture в этом полном руководстве.
og_title: Как выполнить JavaScript асинхронно с помощью CompletableFuture
tags:
- javascript
- java
- asynchronous
- completablefuture
title: Как выполнить JavaScript асинхронно с помощью CompletableFuture
url: /ru/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять JavaScript асинхронно с помощью CompletableFuture

Вы когда‑нибудь задавались вопросом **how to run JavaScript** внутри Java‑приложения без блокировки основного потока? Возможно, вам нужно вызвать небольшой скрипт, который получает данные, но вы не хотите, чтобы ваш UI завис. Хорошая новость в том, что современные Java‑библиотеки позволяют выполнять JavaScript **asynchronously**, и вы даже можете вводить задержки так же, как в браузере. В этом руководстве мы покажем вам полный, готовый к запуску пример, использующий `ScriptEngine` из Aspose HTML вместе с `CompletableFuture`, чтобы **how to run javascript** и получить результат обратно в Java.

Мы также рассмотрим **how to use CompletableFuture**, **how to delay JS**, и **how to evaluate async** код, чтобы вы могли **evaluate JavaScript asynchronously** в любом Java‑проекте. К концу у вас будет надёжный шаблон, который можно скопировать‑вставить, настроить и встроить в более крупные системы.

---

## Что вы узнаете

- Настроить Java `ScriptEngine`, способный выполнять современный JavaScript ES2022.
- Написать `async` функцию, включающую задержку (`how to delay js`).
- Вызвать `evaluateAsync` и получить `CompletableFuture` (`how to use completablefuture`).
- Получить результат после разрешения JavaScript‑promise (`how to evaluate async`).
- Советы по обработке ошибок, управлению потоками и расширению шаблона.

Никакие внешние инструменты сборки не требуются, кроме JAR‑файла Aspose HTML for Java, который можно добавить в classpath. Давайте начнём.

---

## Шаг 1: How to Run JavaScript – Инициализация движка скриптов

Сначала самое главное. Библиотека Aspose HTML предоставляет класс `ScriptEngine`, который может выполнять код JavaScript. Представьте его как крошечный движок Chromium, работающий внутри вашей JVM.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Почему это важно:** При создании экземпляра `ScriptEngine` мы получаем изолированную среду, где современный JavaScript (включая `async/await`) работает сразу же. Нет необходимости запускать внешний процесс Node.

---

## Шаг 2: How to Delay JS – Написание async‑функции с таймером на основе Promise

`setTimeout` в JavaScript — классический способ приостановить выполнение. В современном коде мы оборачиваем его в `Promise`, чтобы можно было `await` его. Именно это мы сделаем в строке скрипта.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **How to delay js:** Помощник `delay` создаёт promise, который завершается через `ms` миллисекунд. При `await`‑е функция приостанавливается без блокировки Java‑потока.

---

## Шаг 3: How to Evaluate Async – Выполнение скрипта и получение CompletableFuture

Вместо синхронного метода `evaluate` мы вызываем `evaluateAsync`. Он сразу возвращает `CompletableFuture<Object>`, который будет завершён, когда JavaScript‑promise разрешится.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **How to evaluate async:** `evaluateAsync` соединяет цикл событий JavaScript с `CompletableFuture` в Java. Это ядро **evaluate javascript asynchronously**.

---

## Шаг 4: How to Use CompletableFuture – Привязка обратного вызова и блокировка для демонстрации

Теперь мы привязываем обратный вызов с помощью `thenAccept`, чтобы вывести результат, и блокируем основной поток достаточно долго, чтобы демонстрация завершилась.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Почему мы вызываем `get()`:** В реальном приложении вы, вероятно, продолжите обработку где‑то ещё. Здесь мы блокируем, чтобы пример был автономным.

---

## Визуальный обзор

![Диаграмма, показывающая, как выполнять JavaScript асинхронно с помощью CompletableFuture](https://example.com/diagram.png "Как выполнять JavaScript – Асинхронный поток")

*Alt text:* **Диаграмма, показывающая, как выполнять JavaScript асинхронно с помощью CompletableFuture** – изображение иллюстрирует поток от Java к движку скриптов, асинхронную задержку и завершение CompletableFuture.

---

## Распространённые подводные камни и лучшие практики (How to Evaluate Async Safely)

| Подводный камень | Что происходит | Исправление |
|------------------|----------------|-------------|
| Забыть вернуть promise | `evaluateAsync` сразу разрешается со значением `undefined` | Убедитесь, что последняя строка скрипта — это promise (`fetchMessage();`) |
| Использование блокирующего `Thread.sleep` в JS | Блокирует цикл событий движка, разрушает асинхронность | Используйте шаблон `delay` promise (как показано) |
| Игнорирование исключений | Future завершается с исключением, но вы его не видите | Присоедините `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| Не закрывать движок | Утечка ресурсов в длительно работающих приложениях | Вызовите `scriptEngine.dispose()` после завершения |

---

## Расширение шаблона (How to Use CompletableFuture in Real Projects)

Вы можете цепочкой вызывать несколько async‑вызовов JavaScript, комбинировать их с другими futures или даже запускать их на пользовательском `Executor`. Вот быстрый набросок:

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **How to use CompletableFuture:** Передавая `Executor`, вы контролируете пул потоков, поддерживая отзывчивость UI и избегая нехватки потоков.

---

## Ожидаемый вывод

Запустите класс `JsAsyncDemo`, и вы должны увидеть:

```
JS result: Hello from async JS!
```

Пауза в 500 мс не видна в консоли, но при желании можно добавить метки времени, чтобы проверить задержку.

---

## Итоги – How to Run JavaScript with CompletableFuture

Мы начали с **how to run javascript** внутри Java, написали `async` функцию, которая **how to delay js**, выполнили её с помощью `evaluateAsync` (**how to evaluate async**) и получили результат, используя **how to use completablefuture**. Весь процесс демонстрирует **evaluate javascript asynchronously** в чистом, переиспользуемом шаблоне.

---

## Что дальше?

- **Integrate with HTTP clients:** Получать данные из REST‑конечного пункта внутри async‑JS и возвращать их в Java.
- **Use multiple scripts:** Связывать несколько вызовов `evaluateAsync` для сложных конвейеров.
- **Swap engines:** Тот же шаблон работает с Nashorn, GraalVM или другими JavaScript‑рантаймами — просто замените `ScriptEngine`.

Не стесняйтесь экспериментировать с более длительными задержками, скриптами, генерирующими ошибки, или даже модулями WebAssembly. Возможности безграничны, когда вы комбинируете примитивы конкурентности Java с современным JavaScript.

### Есть вопросы?

Если что‑то непонятно — возможно, вы задаётесь вопросом, как обработать отклонённый promise или как передать переменные из Java в скрипт — оставьте комментарий ниже. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}