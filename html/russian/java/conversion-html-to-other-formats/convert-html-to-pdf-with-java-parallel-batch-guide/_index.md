---
category: general
date: 2026-06-07
description: Преобразуйте HTML в PDF с помощью ExecutorService в Java. Узнайте, как
  пакетно конвертировать HTML‑файлы, сохранять HTML‑документ в PDF и корректно завершать
  работу ExecutorService.
draft: false
keywords:
- convert html to pdf
- save html document as pdf
- shutdown executorservice gracefully
- batch convert html to pdf
language: ru
og_description: Преобразуйте HTML в PDF с помощью ExecutorService в Java. Овладейте
  пакетным преобразованием, сохранением HTML‑документа в PDF и корректным завершением
  работы ExecutorService.
og_title: Конвертация HTML в PDF с помощью Java – Параллельное пакетное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  headline: Convert HTML to PDF with Java – Parallel Batch Guide
  type: TechArticle
- description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  name: Convert HTML to PDF with Java – Parallel Batch Guide
  steps:
  - name: The HTML file is read into a string.
    text: The HTML file is read into a string.
  - name: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
    text: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
  - name: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
    text: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
  type: HowTo
tags:
- Java
- Concurrency
- PDF Generation
title: Конвертировать HTML в PDF с помощью Java — Параллельное пакетное руководство
url: /ru/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-parallel-batch-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование HTML в PDF с помощью Java – Параллельное пакетное руководство

Когда‑нибудь вам нужно было **convert HTML to PDF**, но вы застряли, пытаясь справиться с десятками файлов? Вы не одиноки — многие разработчики сталкиваются с этой проблемой при создании генераторов отчетов или экспортеров счетов. Хорошая новость? С несколькими строками Java и умным пулом потоков вы можете **batch convert HTML to PDF** в один момент, **save HTML document as PDF**, и даже **shutdown ExecutorService gracefully**, когда работа завершена.

В этом руководстве мы пройдем полный, готовый к запуску пример. Вы увидите, почему пул потоков фиксированного размера — оптимальное решение для параллельного преобразования, как выглядит код конвертации, и какие точные шаги нужны для чистого завершения executor’а. К концу у вас будет автономная программа, которую можно добавить в любой проект — без недостающих частей, без неопределённых ссылок «см. документацию».

## Что вы создадите

- Java‑консольное приложение, которое читает список локальных HTML‑файлов.  
- Каждый файл передаётся рабочему потоку, который создаёт PDF‑версию.  
- Приложение использует **ExecutorService** для параллельного выполнения конвертаций.  
- После того как все задачи поставлены в очередь, пул **shutdown gracefully**, гарантируя, что ни один поток не останется висеть.

**Prerequisites**  
- Java 17 (или любой современный JDK).  
- PDF‑библиотека, способная рендерить HTML, например **OpenHTMLtoPDF**, **iText** или **Flying Saucer**. В коде мы будем ссылаться на заглушку `HTMLDocument`; замените её API вашей библиотеки.  
- Базовые знания о конкуренции в Java (ничего сложного).

![Diagram showing batch conversion of HTML files to PDF using ExecutorService](batch-convert-diagram.png "Преобразование HTML в PDF параллельно с помощью ExecutorService")

*Alt text: Диаграмма, показывающая пакетное преобразование HTML‑файлов в PDF с использованием ExecutorService.*

## Преобразование HTML в PDF параллельно (Batch Convert HTML to PDF)

Когда у вас есть десятки — а иногда и тысячи — HTML‑файлов, их последовательное преобразование в главном потоке становится узким местом. Пул потоков фиксированного размера позволяет JVM переиспользовать заданное количество рабочих потоков, поддерживая высокую загрузку CPU без перегрузки системы.

```java
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * Simple demo that batch converts HTML files to PDF using a fixed thread pool.
 * Replace HTMLDocument with the actual class from your chosen PDF library.
 */
public class HtmlToPdfBatch {

    public static void main(String[] args) {
        // 1️⃣ Prepare a list of HTML files to convert
        List<String> htmlPaths = List.of(
            "src/main/resources/page1.html",
            "src/main/resources/page2.html",
            "src/main/resources/page3.html"
        );

        // 2️⃣ Create a fixed‑size thread pool – 4 workers is a good starting point
        ExecutorService pool = Executors.newFixedThreadPool(4);

        // 3️⃣ Submit a conversion task for each HTML file
        for (String htmlPath : htmlPaths) {
            pool.submit(() -> convertAndSave(htmlPath));
        }

        // 4️⃣ Shutdown ExecutorService gracefully – no new tasks, wait for running ones
        shutdownGracefully(pool);
    }

    /**
     * Core conversion logic – this is where we **save HTML document as PDF**.
     */
    private static void convertAndSave(String htmlPath) {
        try {
            // Imagine HTMLDocument is from OpenHTMLtoPDF, iText, etc.
            HTMLDocument doc = new HTMLDocument(htmlPath);
            String pdfPath = htmlPath.replace(".html", ".pdf");
            doc.save(pdfPath);
            System.out.println("✅ Converted: " + htmlPath + " → " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Failed to convert " + htmlPath + ": " + e.getMessage());
        }
    }

    /**
     * Helper that **shutdowns ExecutorService gracefully**.
     */
    private static void shutdownGracefully(ExecutorService executor) {
        executor.shutdown(); // stop accepting new tasks
        try {
            // Wait a maximum of 60 seconds for existing tasks to finish
            if (!executor.awaitTermination(60, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("⚠️ Pool didn’t terminate in time – forcing shutdown");
                executor.shutdownNow(); // cancel currently executing tasks
            } else {
                System.out.println("🛑 All tasks completed – executor shut down cleanly.");
            }
        } catch (InterruptedException ie) {
            // Preserve interrupt status & force shutdown
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }
}
```

### Почему это работает

- **Parallelism**: Каждый вызов `submit` передаёт конвертацию рабочему потоку, поэтому четыре файла могут обрабатываться одновременно на четырёхъядерной машине.  
- **Isolation**: Метод `convertAndSave` содержит всю логику, необходимую для **save HTML document as PDF**, что упрощает замену базовой библиотеки позже.  
- **Graceful termination**: Сначала вызывая `shutdown()`, мы говорим пулу «больше нет задач, пожалуйста, завершите текущие». Цикл `awaitTermination` даёт потокам шанс закончить работу, и только если они упорствуют, мы вызываем `shutdownNow()`. Этот шаблон — рекомендованный способ **shutdown ExecutorService gracefully**.

## Сохранение HTML‑документа как PDF — Основная логика конвертации

Сердцем любого **convert HTML to PDF** рабочего процесса является библиотека конвертации. Хотя пример использует заглушку `HTMLDocument`, вот быстрый взгляд на то, как это можно сделать с помощью **OpenHTMLtoPDF**:

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

public class HTMLDocument {
    private final String htmlPath;

    public HTMLDocument(String htmlPath) {
        this.htmlPath = htmlPath;
    }

    public void save(String pdfPath) throws IOException {
        try (OutputStream os = new FileOutputStream(pdfPath);
             InputStream is = new FileInputStream(htmlPath)) {

            PdfRendererBuilder builder = new PdfRendererBuilder();
            builder.withHtmlContent(new String(is.readAllBytes()), null);
            builder.toStream(os);
            builder.run();
        }
    }
}
```

**Что происходит?**  
1. HTML‑файл читается в строку.  
2. `PdfRendererBuilder` разбирает разметку, применяет CSS и передаёт результат в PDF‑файл.  
3. Любой `IOException` поднимается до `convertAndSave`, где мы регистрируем успех или ошибку.

Не стесняйтесь заменить этот фрагмент на `HtmlConverter.convertToPdf` из iText или `ITextRenderer` из Flying Saucer. Код, управляющий пулом потоков, остаётся точно таким же, поэтому мы выделили **save HTML document as PDF** как отдельную задачу.

## Корректное завершение ExecutorService — Лучшие практики

Распространённая ошибка — вызвать `shutdownNow()` сразу после отправки задач. Это резко прерывает потоки, что может привести к появлению неполных PDF‑файлов на диске. Шаблон, который мы использовали — `shutdown()` → `awaitTermination()` → опциональный `shutdownNow()` — гарантирует:

- **No new tasks** не принимаются после того, как вы поставили все задачи в очередь.  
- **Running tasks** получают шанс завершиться корректно.  
- **Blocked threads** прерываются только если превышают разумный тайм‑аут (здесь 60 секунд).  

Если вы ожидаете очень большие PDF‑файлы или медленный движок рендеринга, увеличьте тайм‑аут или используйте `executor.invokeAll(tasks, timeout, unit)` для более строгого контроля.

## Полный рабочий пример (Все части вместе)

Ниже представлен весь код программы, который вы можете скопировать в один файл `HtmlToPdfBatch.java`. Просто добавьте зависимость OpenHTMLtoPDF (или вашу предпочтительную библиотеку) в `pom.xml` или Gradle‑скрипт, и всё готово.



## Что следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как конвертировать HTML в PDF Java — используя Aspose.HTML для Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Конвертировать HTML в PDF Java — настройка окружения в Aspose.HTML](/html/english/java/configuring-environment/)
- [Конвертировать HTML в PDF в Java — пошаговое руководство с настройками размеров страниц](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}