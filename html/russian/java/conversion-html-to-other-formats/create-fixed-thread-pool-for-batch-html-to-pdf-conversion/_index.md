---
category: general
date: 2026-02-22
description: Создайте фиксированный пул потоков для эффективного пакетного преобразования
  HTML в PDF на Java. Изучите пример пула потоков в Java, который быстро сохраняет
  HTML в PDF.
draft: false
keywords:
- create fixed thread pool
- convert html to pdf
- batch html to pdf
- thread pool java example
- save html as pdf
language: ru
og_description: Создайте фиксированный пул потоков для пакетного преобразования HTML
  в PDF. Это руководство проведёт вас через пример пула потоков на Java, который эффективно
  сохраняет HTML в PDF.
og_title: Создать фиксированный пул потоков для пакетного преобразования HTML в PDF
tags:
- Java
- Concurrency
- PDF Generation
title: Создать фиксированный пул потоков для пакетного преобразования HTML в PDF
url: /ru/java/conversion-html-to-other-formats/create-fixed-thread-pool-for-batch-html-to-pdf-conversion/
---

must keep them.

Now produce final output with translated Russian text.

Be careful with markdown formatting.

Let's write translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание фиксированного пула потоков для пакетного преобразования HTML в PDF

Задумывались ли вы когда‑нибудь, как **создать фиксированный пул потоков**, который превращает кучу HTML‑файлов в PDF без перегрузки процессора? Вы не одиноки. Когда у вас десятки — а иногда и сотни — страниц для обработки, выполнять их по одной — это утомительно, но запуск неограниченного пула потоков может быстро исчерпать память.  

В этом руководстве мы решим эту проблему, показав **пример Java с пулом потоков**, который **пакетно преобразует HTML в PDF**, сохраняет каждый результат и корректно завершает работу. К концу вы сможете **конвертировать HTML в PDF** параллельно и поймёте, почему фиксированный пул потоков — оптимальный вариант для большинства пакетных задач.

## Что вы получите

- Полную, готовую к запуску программу на Java, которая создает фиксированный пул потоков.  
- Пошаговое объяснение каждой строки, чтобы вы знали **почему** делаем именно так.  
- Руководство по выбору библиотеки PDF (чтобы вы могли **сохранять HTML как PDF** без поиска фрагментов кода).  
- Советы по обработке ошибок, настройке размера пула и расширению решения для больших пакетов.

**Prerequisites** – установлен Java 8+, базовая IDE (IntelliJ, Eclipse или VS Code) и библиотека конвертации PDF в вашем classpath (в примере мы используем *OpenHTMLtoPDF*). Другие фреймворки не требуются.

---

## Создание фиксированного пула потоков – почему это важно

Когда вы **создаёте фиксированный пул потоков**, вы говорите JVM, сколько именно рабочих потоков может работать одновременно. Это предотвращает «бури» создания потоков, делает использование памяти предсказуемым и позволяет ОС эффективно планировать работу.  

Представьте себе кассу в продуктовом магазине: вы открываете определённое количество касс, позволяете клиентам выстраиваться в очередь и закрываете кассы, когда очередь исчезает. `FixedThreadPool` работает точно так же — задачи ждут своей очереди, но дополнительные потоки не создаются «на лету».

```java
// Step 1: Build a fixed‑size thread pool with 4 workers
ExecutorService threadPool = Executors.newFixedThreadPool(4);
```

Число `4` — хорошая отправная точка для ноутбука с четырёхъядерным процессором; вы можете изменить его в зависимости от количества ядер CPU и характеристик ввода‑вывода.

## Пакетное преобразование HTML в PDF: конвертация каждой страницы

Теперь, когда пул существует, нам нужно передать ему задачи, которые **конвертируют HTML в PDF**. Каждая задача будет:

1. Загружать HTML‑документ с диска.  
2. Передавать его библиотеке PDF.  
3. Записывать полученный PDF обратно в тот же каталог.

Поскольку работа в основном связана с вводом‑выводом (чтение файлов, запись PDF), небольшой пул часто превосходит более крупный, который просто простаивает, ожидая диск.

```java
// Step 2: Submit a conversion job for every HTML file you have
for (int i = 0; i < 4; i++) {
    final int pageIndex = i;               // capture loop variable for the lambda
    threadPool.submit(() -> {
        // Load the HTML file
        Path htmlPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".html");
        String html = Files.readString(htmlPath, StandardCharsets.UTF_8);

        // Convert and save as PDF
        Path pdfPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".pdf");
        convertHtmlToPdf(html, pdfPath);
    });
}
```

> **Pro tip:** Если у вас более четырёх страниц, просто увеличьте границу цикла или считывайте список файлов динамически — `Files.list(Paths.get("YOUR_DIRECTORY")).filter(p -> p.toString().endsWith(".html"))` делает это без усилий.

## Пример Java с пулом потоков, объяснённый построчно

Разберём **пример Java с пулом потоков** строка за строкой, чтобы вы не просто копировали код, а действительно понимали поток выполнения.

| Line | What It Does | Why It’s Important |
|------|--------------|--------------------|
| `ExecutorService threadPool = Executors.newFixedThreadPool(4);` | Создаёт пул ровно из четырёх потоков. | Гарантирует ограниченное количество одновременных конвертаций, избегая ошибок «Out‑of‑Memory». |
| `for (int i = 0; i < 4; i++) { … }` | Проходит по страницам, которые нужно обработать. | Цикл отвечает за создание задач; статическую границу можно заменить динамическим списком. |
| `final int pageIndex = i;` | Захватывает индекс цикла для использования внутри лямбда‑выражения. | Без `final` (или эффективно final) лямбда увидит меняющуюся переменную, что приведёт к неверным именам файлов. |
| `threadPool.submit(() -> { … });` | Передаёт `Runnable` в пул для асинхронного выполнения. | Пул планирует runnable на свободном рабочем потоке, освобождая главный поток для дальнейшего добавления задач. |
| `Files.readString(htmlPath, …);` | Считывает HTML‑файл в `String`. | Необходимо, потому что большинство PDF‑библиотек принимают HTML в виде строки или потока. |
| `convertHtmlToPdf(html, pdfPath);` | Вызывает вспомогательный метод, который делает реальную конвертацию. | Делает лямбда‑выражение компактным и изолирует код, зависящий от конкретной библиотеки. |

Ниже полная вспомогательная функция, использующая **OpenHTMLtoPDF**, лёгкую библиотеку, которая **сохраняет HTML как PDF** одним вызовом.

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

private static void convertHtmlToPdf(String html, Path outputPdf) throws IOException {
    try (OutputStream os = Files.newOutputStream(outputPdf)) {
        PdfRendererBuilder builder = new PdfRendererBuilder();
        builder.withHtmlContent(html, null);     // base URI is null because we use absolute paths
        builder.toStream(os);
        builder.run();                           // blocks until PDF is written
    } catch (Exception e) {
        // Wrap any checked exception as an unchecked one so the lambda can compile
        throw new RuntimeException("Failed to convert HTML to PDF for " + outputPdf, e);
    }
}
```

> **Why OpenHTMLtoPDF?** Это чистый Java, без нативных зависимостей, и он учитывает CSS, благодаря чему полученные PDF почти полностью соответствуют оригинальным веб‑страницам. Если вы предпочитаете iText или Flying Saucer, просто замените реализацию внутри `convertHtmlToPdf`.

## Сохранение HTML как PDF – выбор библиотеки

Вы можете спросить: «Какую библиотеку лучше **конвертировать HTML в PDF**?» Ниже краткое сравнение:

| Library | Maven Coordinates | Pros | Cons |
|---------|-------------------|------|------|
| OpenHTMLtoPDF | `com.openhtmltopdf:openhtmltopdf-pdfbox:1.0.10` | Чистый Java, хорошая поддержка CSS, лёгкая | Ограниченные продвинутые функции PDF (например, шифрование) |
| iText 7 + html2pdf | `com.itextpdf:html2pdf:3.0.6` | Богатый набор функций, коммерческая поддержка | Требуется платная лицензия для многих сценариев |
| Flying Saucer | `org.xhtmlrenderer:flying-saucer-pdf:9.1.22` | Зрелая, работает со старыми версиями Java | Медленнее на больших документах, менее полная поддержка CSS |

Выберите ту, что соответствует требованиям вашего проекта. Для **пакетного преобразования HTML в PDF** OpenHTMLtoPDF обычно попадает в «золотую середину»: быстро, просто и бесплатно.

## Корректное завершение и обработка ошибок

Если оставить исполнитель работающим, JVM может не завершиться, а непойманные исключения в потоке трудно отследить. Следующий шаблон обеспечивает аккуратное завершение:

```java
// Step 5: Initiate an orderly shutdown after all tasks are queued
threadPool.shutdown();                     // No new tasks accepted
try {
    // Wait up to 60 seconds for existing tasks to finish
    if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
        threadPool.shutdownNow();          // Force shutdown if tasks linger
    }
} catch (InterruptedException ex) {
    threadPool.shutdownNow();              // Preserve interrupt status
    Thread.currentThread().interrupt();
}
```

- `shutdown()` сообщает пулу завершить текущие задачи, но отклонять новые.  
- `awaitTermination` блокирует поток, пока либо всё не завершится, либо не истечёт тайм‑аут.  
- `shutdownNow()` пытается отменить запущенные задачи — полезно для принудительной остановки.

Если какая‑то конвертация завершится с ошибкой, `RuntimeException`, который мы бросаем, поднимается до исполнителя и по умолчанию выводится в консоль. В продакшене стоит подключить собственный `ThreadPoolExecutor` с переопределённым методом `afterExecute` для записи в файл или систему мониторинга.

## Полный рабочий пример

Собрав всё вместе, представляем автономный Java‑класс, который можно скопировать‑вставить в `src/main/java/com/example/BatchPdfConverter.java`. Убедитесь, что зависимость OpenHTMLtoPDF находится в вашем classpath.

```java
package com.example;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;
import java.util.concurrent.*;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;

/**
 * Demonstrates how to create a fixed thread pool to batch HTML to PDF conversion.
 * Adjust POOL_SIZE and DIRECTORY constants to fit your environment.
 */
public class BatchPdfConverter {

    private static final int POOL_SIZE = 4;                     // Number of parallel workers
    private static final Path DIRECTORY = Paths.get("YOUR_DIRECTORY"); // Change to your folder

    public static void main(String[] args) {
        ExecutorService threadPool = Executors.newFixedThreadPool(POOL_SIZE);

        // Discover all *.html files in the target directory
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(DIRECTORY, "*.html")) {
            for (Path htmlPath : stream) {
                threadPool.submit(() -> processFile(htmlPath));
            }
        } catch (IOException e) {
            System.err.println("Failed to list HTML files: " + e.getMessage());
        }

        // Graceful shutdown
        thread

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}