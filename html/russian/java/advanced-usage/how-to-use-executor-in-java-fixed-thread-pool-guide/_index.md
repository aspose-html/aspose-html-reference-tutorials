---
category: general
date: 2026-05-28
description: как использовать executor в Java с фиксированным пулом потоков, извлекать
  текст из HTML и ускорять обработку – полный пример пула потоков Java.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: ru
og_description: как использовать executor в Java с фиксированным пулом потоков. Изучите
  полный пример пула потоков Java, который эффективно извлекает текст из HTML‑файлов.
og_title: Как использовать Executor в Java – руководство по фиксированному пулу потоков
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: Как использовать Executor в Java – руководство по фиксированному пулу потоков
url: /ru/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать Executor в Java – Руководство по фиксированному пулу потоков

Когда‑нибудь задавались вопросом **как использовать executor**, чтобы запустить множество задач одновременно, не переполняя память? Вы не одиноки. Во многих реальных приложениях вам понадобится просканировать папку с HTML‑файлами, извлечь текст тела и сделать это быстро — именно такой сценарий решает этот учебник.

Мы пройдем через реализацию **fixed thread pool java**, которая извлекает текст из HTML, выводит количество символов в каждом файле и корректно завершает работу. К концу у вас будет автономный **java thread pool example**, который можно добавить в любой проект, а также несколько советов по настройке размера пула и обработке крайних случаев.

> **Что понадобится**  
> * Java 17 (или любой современный JDK)  
> * Небольшая библиотека для парсинга HTML — мы будем использовать *jsoup*, потому что она проверена в боевых условиях и не требует конфигурации.  
> * Небольшой набор примерных файлов *.html* в директории по вашему выбору.

---

## Как использовать Executor с фиксированным пулом потоков

Сердцем любой программы на Java с интенсивной параллельностью является `ExecutorService`. Создавая **fixed thread pool**, мы говорим JVM поддерживать ровно N рабочих потоков, что предотвращает накладные расходы на создание потоков и ограничивает использование ресурсов.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Почему это важно:*  
Если бы вы запускали новый `Thread` для каждого HTML‑файла, ОС пришлось бы планировать десятки потоков на скромном ноутбуке, что приводило бы к частой смене контекста. Фиксированный пул переиспользует одни и те же четыре потока, обеспечивая предсказуемую загрузку CPU.

---

## Определение HTML‑файлов для обработки — Fixed Thread Pool Java

Далее мы перечисляем файлы, которые хотим передать в пул. В реальном приложении вы, вероятно, будете обходить дерево каталогов; здесь мы упростим задачу.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Подсказка:* `List.of` возвращает неизменяемый список, который безопасно использовать в нескольких потоках без дополнительной синхронизации.

---

## Отправка отдельной задачи для каждого HTML‑файла

Теперь мы передаем каждый путь исполнителю. Лямбда, которую мы отправляем, будет выполняться **параллельно** на одном из четырёх рабочих потоков.

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**Почему мы оборачиваем логику в метод** (`extractBodyText`), станет ясно в следующем разделе — это делает лямбду аккуратной и позволяет переиспользовать код извлечения в других местах.

---

## Извлечение текста из HTML — основная логика

Вот переиспользуемый вспомогательный метод, который действительно **extracts text from html** с помощью Jsoup. Он открывает файл, парсит DOM и возвращает чистый текст тела.

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*Почему Jsoup?* Он лёгкий, корректно обрабатывает некорректную разметку и не требует полноценного браузерного движка. Метод бросает `IOException`, чтобы вызывающий код мог решить, как логировать или восстанавливать работу — идеально для сценария с пулом потоков, где вы не хотите, чтобы один плохой файл завершал работу всего executor.

---

## Корректное завершение работы Executor — создание фиксированного пула потоков

После того как мы отправили все задачи, необходимо сообщить пулу прекратить принимать новую работу и завершить уже поставленные в очередь.

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*Объяснение:* `shutdown()` предотвращает новые отправки, а `awaitTermination` блокирует выполнение до завершения всех задач парсинга (или истечения тайм‑аута). Если что‑то зависает, `shutdownNow()` пытается отменить запущенные задачи. Этот шаблон — рекомендованный способ **create fixed thread pool** безопасно.

---

## Полный, исполняемый пример

Объединив всё вместе, представляем один файл, который можно скомпилировать и запустить. Он содержит необходимые импорты, метод `main` и вспомогательный метод, описанный выше.

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**Ожидаемый вывод** (при условии, что каждый файл содержит примерно 1 200 символов текста тела):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Если какой‑то файл отсутствует или повреждён, вы увидите трассировку стека, выведенную в `stderr`, но остальные задачи продолжат работу без влияния — именно то, что должен делать корректный **java thread pool example**.

---

## Часто задаваемые вопросы и крайние случаи

| Вопрос | Ответ |
|----------|--------|
| *Что если у меня более четырёх файлов?* | Пул поставит лишние задачи в очередь и выполнит их, как только освободится поток. Дополнительный код не требуется. |
| *Стоит ли вместо этого использовать `newCachedThreadPool`?* | `newCachedThreadPool` создаёт потоки по требованию и может расти без ограничений, что рискованно для задач с интенсивным вводом‑выводом. **fixed thread pool** обеспечивает предсказуемое использование памяти и CPU. |
| *Как изменить размер пула в зависимости от количества ядер CPU?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` — распространённый шаблон. |
| *Что если парсинг одного файла завершится ошибкой?* | `catch (IOException e)` внутри лямбды изолирует ошибку, записывает её в лог и позволяет остальному пулу продолжать работу. |
| *Могу ли я вернуть извлечённый текст вызывающему коду?* | Да — используйте `Future<String>` вместо `submit(Runnable)`. Код будет выглядеть так: `Future<String> f = executor.submit(() -> extractBodyText(path));` и позже `String result = f.get();`. |

---

## Заключение

Мы рассмотрели **how to use executor**, чтобы создать **fixed thread pool java**, который обрабатывает набор HTML‑файлов параллельно, извлекает их текст тела и выводит количество символов. Полный **java thread pool example** демонстрирует правильное управление ресурсами, обработку ошибок и переиспользуемый метод извлечения.

Что дальше? Попробуйте заменить реализацию `extractBodyText` на более продвинутый скраппер, поэкспериментировать с большим размером пула или передать результаты в базу данных. Вы также можете изучить `CompletionService` для получения результатов сразу после их готовности, что удобно, когда размеры файлов сильно различаются.

Не стесняйтесь менять путь к директории, добавлять больше файлов или интегрировать этот фрагмент в более крупный фреймворк обхода. Основной шаблон — создать пул, отправить независимые задачи и корректно завершить работу — остаётся тем же, независимо от сложности нагрузки.

Удачной разработки, и пусть ваши потоки всегда живут (до тех пор, пока вы их не завершите, конечно)!

## Связанные руководства

- [Fixed thread pool java – Параллельная очистка HTML с ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Query HTML in Java – Полный учебник](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Use Aspose.HTML for Java — Мастерство рендеринга HTML5 Canvas](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}