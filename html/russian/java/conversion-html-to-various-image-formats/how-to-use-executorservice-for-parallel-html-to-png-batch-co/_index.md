---
category: general
date: 2026-02-21
description: Как использовать ExecutorService для быстрой конвертации HTML в PNG.
  Узнайте, как пакетно преобразовывать HTML‑файлы с помощью параллельных задач в Java.
draft: false
keywords:
- how to use executorservice
- convert html to png
- how to run parallel tasks
- how to convert html to png
- batch convert html files
language: ru
og_description: Как использовать ExecutorService для пакетного преобразования HTML‑файлов
  в PNG. Пошаговое руководство с полным примером на Java.
og_title: Как использовать ExecutorService для параллельного преобразования HTML в
  PNG
tags:
- Java
- concurrency
- Aspose.HTML
- image‑conversion
title: Как использовать ExecutorService для параллельного пакетного преобразования
  HTML в PNG
url: /ru/java/conversion-html-to-various-image-formats/how-to-use-executorservice-for-parallel-html-to-png-batch-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать ExecutorService для параллельного пакетного преобразования HTML‑to‑PNG

Когда‑нибудь задавались вопросом **как использовать ExecutorService**, когда у вас есть папка, полная HTML‑страниц, которые нужно превратить в PNG‑изображения? Вы не одиноки — многие разработчики сталкиваются с этим, когда их конвейер веб‑отчётности зависает в однопоточном цикле преобразования.  

Хорошие новости? С несколькими строками Java и мощным Aspose.HTML `Converter` вы можете создать пул рабочих потоков, передать каждый HTML‑файл конвертеру и наблюдать, как изображения появляются параллельно. В этом руководстве мы также коснёмся основ **convert html to png**, покажем, как **run parallel tasks**, и предоставим готовый к запуску скрипт **batch convert html files**.

## Требования

- Java 17 или новее (код использует современный API `java.nio.file`).  
- Библиотека Aspose.HTML for Java в вашем classpath. Вы можете получить её из Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

- Каталог, содержащий исходные файлы `.html`, и пустая папка вывода.  
- Умеренное количество ОЗУ — каждая конверсия выполняется в отдельном потоке, поэтому размер пула должен соответствовать количеству ядер CPU.

> **Pro tip:** Если вы работаете на машине с гиперпоточностью, `Runtime.getRuntime().availableProcessors()` обычно возвращает оптимальное количество ядер.

## Шаг 1 — Определение путей ввода и вывода

Сначала нам нужно указать Java, где находятся HTML‑файлы и куда сохранять PNG‑изображения. Использование объектов `Path` делает код независимым от платформы.

```java
import java.nio.file.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Input folder containing .html files
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        // Output folder for the generated .png files
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");

        // Ensure the output folder exists
        Files.createDirectories(outputDir);
```

> **Почему это важно:** Создание каталога вывода заранее предотвращает `FileNotFoundException`, когда первый рабочий поток пытается записать файл.

## Шаг 2 — Создание фиксированного пула потоков

Суть **how to use ExecutorService** заключается в создании пула, соответствующего вашему оборудованию. *Фиксированный* пул гарантирует, что мы не создадим больше потоков, чем можем реально запустить.

```java
        // Create a thread pool sized to the number of available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());
```

> **Объяснение:** `ExecutorService` абстрагирует низкоуровневое управление потоками. Используя `newFixedThreadPool`, мы позволяем JVM переиспользовать потоки, что уменьшает накладные расходы на их постоянное создание и уничтожение.

## Шаг 3 — Отправка одной задачи конвертации на каждый HTML‑файл

Теперь мы проходим по входному каталогу, выбираем каждый файл `*.html` и передаём его в пул. Каждая задача — небольшая лямбда, вызывающая `Converter.convert`.

```java
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        // Build the output filename by swapping .html for .png
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();

                        // Perform the actual conversion
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }
```

### Что происходит под капотом?

1. **DirectoryStream** лениво читает имена файлов, поэтому использование памяти остаётся низким даже при тысячах файлов.  
2. Лямбда захватывает `htmlFile` и `outputDir` — нет необходимости в отдельном классе `Runnable`.  
3. `Converter.convert` — блокирующий вызов, который читает HTML, рендерит его и записывает PNG. Поскольку каждый вызов выполняется в отдельном потоке, несколько файлов обрабатываются одновременно — именно то поведение, которое вы ожидаете при **run parallel tasks**.

## Шаг 4 — Корректное завершение работы пула

После того как все задачи поставлены в очередь, мы сообщаем пулу прекратить принимать новую работу и ждём завершения всех задач. Если что‑то зависнет, тайм‑аут прервет процесс через час, что достаточно для большинства пакетных заданий.

```java
        // No more tasks will be submitted
        pool.shutdown();

        // Wait up to 1 hour for all conversions to complete
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }

        System.out.println("All conversions completed.");
    }
}
```

> **Особый случай:** Если у вас есть чрезвычайно большие HTML‑файлы, возможно, потребуется увеличить тайм‑аут или контролировать использование памяти. Добавление `pool.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy())` заставляет вызывающий поток выполнять лишние задачи, предотвращая `RejectedExecutionException`.

## Полный готовый к запуску пример

Ниже представлен весь код программы, готовый к копированию в один файл `ParallelBatchConversion.java`.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.*;
import java.util.concurrent.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Step 1: Define source and destination folders
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");
        Files.createDirectories(outputDir);

        // Step 2: Create a thread pool sized to the available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());

        // Step 3: Submit a conversion task for each HTML file found
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }

        // Step 4: Shut down the pool and wait for all conversions to finish
        pool.shutdown();
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }
        System.out.println("All conversions completed.");
    }
}
```

### Ожидаемый вывод

Запуск программы выводит строку для каждой успешно выполненной конвертации:

```
Converted: report1.html
Converted: dashboard.html
Converted: summary.html
All conversions completed.
```

Если файл не удалось обработать, вы увидите строку ошибки с сообщением исключения, что упрощает отладку.

## Как расширить этот шаблон

- **Different image formats:** Замените расширение `.png` на `.jpg` или `.bmp` и соответственно настройте параметры конвертации Aspose.  
- **Dynamic thread count:** Для задач, ограниченных вводом‑выводом, вы можете увеличить размер пула (`availableProcessors() * 2`).  
- **Progress monitoring:** Замените `System.out.println` на потокобезопасную библиотеку индикатора прогресса, например `jline`, или выводите в файл.  
- **Error handling:** Собирать пути неудачных файлов в `List<Path>` и повторять попытку после завершения основного цикла.

## Часто задаваемые вопросы

**Q: Работает ли это на Windows и Linux?**  
A: Да. `java.nio.file` абстрагирует файловую систему, поэтому один и тот же код работает без изменений на любой ОС, поддерживающей Java.

**Q: Что если у меня более 10 000 HTML‑файлов?**  
A: Итератор `DirectoryStream` читает записи лениво, поэтому потребление памяти остаётся низким. Просто убедитесь, что на диске достаточно свободного места для PNG‑вывода.

**Q: Можно ли ограничить память, используемую каждой конвертацией?**  
A: Aspose.HTML позволяет настроить движок рендеринга через `HtmlLoadOptions` и `ImageSaveOptions`. Можно задать максимальный размер битмапа или включить рендеринг низкого качества, чтобы контролировать потребление ОЗУ.

## Заключение

Мы прошли процесс **how to use ExecutorService** для **batch convert html files** в PNG‑изображения, объяснили, почему фиксированный пул — оптимальный вариант для CPU‑зависимого рендеринга, и предоставили полностью готовую к копированию Java‑программу. Следуя описанным шагам, вы превратите медленный однопоточный цикл в быстрый масштабируемый конвейер, способный обрабатывать тысячи файлов одной командой.

Готовы к следующему вызову? Попробуйте заменить `Converter.convert` на экспорт PDF в Aspose для **convert html to pdf**, либо интегрировать эту логику в микросервис Spring Boot, принимающий запросы загрузки‑и‑конвертации. Основная идея — использование `ExecutorService` для **run parallel tasks** — остаётся той же, и вы найдёте её полезной во множестве сценариев пакетной обработки.

Счастливого кодинга, и пусть ваши потоки всегда живут! 

![how to use executorservice diagram](placeholder.png "Diagram illustrating the thread pool workflow for parallel HTML‑to‑PNG conversion")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}