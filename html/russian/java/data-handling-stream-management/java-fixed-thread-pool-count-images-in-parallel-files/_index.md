---
category: general
date: 2026-02-10
description: Узнайте, как использовать фиксированный пул потоков Java для подсчёта
  изображений в HTML‑файлах, запускать задачи параллельно и правильно завершать службу
  исполнителя.
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: ru
og_description: Освоил использование фиксированного пула потоков в Java для подсчёта
  изображений, параллельной обработки файлов и безопасного завершения ExecutorService.
og_title: 'Java фиксированный пул потоков: подсчёт изображений в параллельных файлах'
tags:
- Java
- Concurrency
- Aspose.HTML
title: 'Java фиксированный пул потоков: подсчёт изображений в параллельных файлах'
url: /ru/java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – Параллельный подсчёт изображений

Задумывались ли вы когда‑нибудь, как **java fixed thread pool** пройтись по десяткам HTML‑файлов и быстро посчитать изображения? Может быть, вы смотрели на каталог страниц, думали «Мне нужно знать, сколько тегов `<img>` в каждом файле», а затем поняли, что однопоточный цикл займет вечность.  

Хорошая новость в том, что вам не нужно писать собственный менеджер потоков или возиться с низкоуровневыми объектами `Thread`. В этом руководстве мы покажем, **как посчитать изображения** с помощью *java fixed thread pool*, запускать задачи параллельно java и корректно **shutdown executor service**, когда работа завершена.  

Мы охватим всё: от настройки пула, подготовки списка файлов, отправки параллельных задач, обработки граничных случаев, до проверки вывода. К концу вы получите готовую к запуску программу, демонстрирующую **java parallel file processing** чистым и поддерживаемым способом.  

## Prerequisites

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

- Java 17 или новее (в коде используется ключевое слово `var` для краткости, но при необходимости можно понизить версию).
- Aspose.HTML for Java в classpath – его можно получить из Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- Пара HTML‑файлов, которые вы хотите проанализировать (в руководстве предполагается, что они находятся в `YOUR_DIRECTORY/`).
- IDE или система сборки, с которой вам удобно работать – IntelliJ IDEA, VS Code или простой `javac` подойдут.

И всё. Никаких дополнительных серверов, Docker не нужен, только чистый Java и небольшая сторонняя библиотека.

## Step 1: Create a java fixed thread pool

*java fixed thread pool* предоставляет ограниченный набор рабочих потоков, которые переиспользуются для каждой отправленной задачи. Это избавляет от накладных расходов на постоянное создание новых потоков и ограничивает уровень параллелизма, что критично при чтении файлов с диска.

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**Почему 4?** Если у вас ноутбук с четырёхъядерным процессором, четыре потока загружают каждый ядро без переизбытка. На сервере с большим количеством ядер число можно увеличить, но помните, что каждый поток открывает файловый дескриптор, поэтому слишком много потоков могут исчерпать лимиты ОС.

## Step 2: List the HTML files you want to analyse

Следующий шаг **java parallel file processing** – просто собрать массив (или `List`) путей к файлам. В реальном проекте вы, вероятно, будете рекурсивно обходить каталог, фильтровать по расширению или читать пути из базы данных. Здесь показан простой подход:

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

Если нужен динамический набор, замените статический массив, например, на:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

Этот фрагмент демонстрирует **java parallel file processing** для любого количества файлов без изменения остального кода.

## Step 3: Submit tasks to **run tasks concurrently java**

Теперь к сердцу руководства – мы **run tasks concurrently java** отправляя лямбду для каждого файла. Каждая задача загружает HTML‑документ с помощью Aspose.HTML, выбирает все элементы `<img>` и выводит их количество.

```java
import com.aspose.html.HTMLDocument;

public static void main(String[] args) throws InterruptedException {
    for (String filePath : htmlFiles) {
        executor.submit(() -> {
            // Load the document – Aspose.HTML does the heavy lifting
            HTMLDocument document = new HTMLDocument(filePath);
            // querySelectorAll returns a NodeList; its length is the image count
            int imageCount = document.querySelectorAll("img").length;
            System.out.println(filePath + " contains " + imageCount + " images.");
        });
    }

    // Step 4 is next – gracefully shut down the pool
    shutdownAndAwaitTermination();
}
```

**Зачем лямбда?** Она делает код лаконичным и избавляет от необходимости создавать отдельный класс `Runnable`. Лямбда автоматически захватывает `filePath`, поэтому каждая задача работает со своим файлом.

### How to **count images** efficiently

Aspose.HTML парсит файл один раз, строит DOM, а затем `querySelectorAll("img")` работает за O(n), где *n* – количество узлов. Для большинства HTML‑страниц это пренебрежимо. Если нужен более быстрый, только‑потоковый подход (например, для файлов гигабайтного размера), можно переключиться на SAX‑парсер, но это усложнит код, от чего мы отказываемся.

## Step 4: Properly **shutdown executor service**

Никогда не забывайте завершать пул, иначе ваш JVM будет работать вечно. Ниже показан рекомендованный способ **shutdown executor service** с ожиданием завершения всех задач:

```java
private static void shutdownAndAwaitTermination() {
    executor.shutdown(); // Disable new tasks from being submitted
    try {
        // Wait a while for existing tasks to terminate
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            executor.shutdownNow(); // Cancel currently executing tasks
            // Wait a second for tasks to respond to being cancelled
            if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                System.err.println("Pool did not terminate");
        }
    } catch (InterruptedException ie) {
        // (Re-)Cancel if current thread also interrupted
        executor.shutdownNow();
        // Preserve interrupt status
        Thread.currentThread().interrupt();
    }
}
```

**Что если задача зависнет?** Вызов `shutdownNow()` пытается прервать работающие потоки. Если ваша логика подсчёта изображений поддерживает прерывание (Aspose.HTML не блокирует ввод‑вывод), пул завершится корректно. Этот шаблон считается золотым стандартом для любого использования **java fixed thread pool**.

## Step 5: Verify the output

Запустите программу из IDE или через командную строку:

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

Обычный вывод выглядит так:

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

Если вы видите подсчёты в произвольном порядке, это ожидаемо – потоки завершаются в разное время. Главное, чтобы каждый файл был обработан и программа корректно завершилась после процедуры shutdown.

## Full Working Example (Copy‑Paste Ready)

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelImageCounter {
    // 1️⃣ Fixed thread pool – change size based on your hardware
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);

    public static void main(String[] args) throws InterruptedException {
        // 2️⃣ List of HTML files – replace with your own directory
        String[] htmlFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // 3️⃣ Submit a counting task for each file
        for (String filePath : htmlFiles) {
            executor.submit(() -> {
                HTMLDocument document = new HTMLDocument(filePath);
                int imageCount = document.querySelectorAll("img").length;
                System.out.println(filePath + " contains " + imageCount + " images.");
            });
        }

        // 4️⃣ Gracefully shut down the pool
        shutdownAndAwaitTermination();
    }

    // 5️⃣ Helper method to cleanly stop the executor
    private static void shutdownAndAwaitTermination() {
        executor.shutdown(); // Disable new tasks
        try {
            if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
                executor.shutdownNow(); // Cancel currently executing tasks
                if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                    System.err.println("Pool did not terminate");
            }
        } catch (InterruptedException ie) {
            executor.shutdownNow();
            Thread.currentThread().interrupt();
        }
    }
}
```

### Expected Result

Запуск фрагмента выводит путь к каждому файлу и количество тегов `<img>` в нём, после чего JVM завершается. Никаких «залипающих» потоков, никаких утечек памяти.

## Common Pitfalls & Pro Tips

- **Pitfall:** Использовать `newCachedThreadPool()` вместо *fixed* пула. Это создаёт неограниченное количество потоков, что может исчерпать файловые дескрипторы при больших партиях. Оставайтесь на `newFixedThreadPool`.
- **Pro tip:** Если ваши HTML‑файлы огромные, рассмотрите увеличение кучи (`-Xmx2g`) или переход на потоковый парсер. Для большинства маркетинговых страниц стандартный размер кучи достаточен.
- **Pitfall:** Забыть вызвать `shutdown()` – приложение «зависнет» после вывода результатов. Метод `shutdownAndAwaitTermination`, показанный выше, решает эту проблему надёжно.
- **Pro tip:** Логируйте время начала и окончания каждой задачи, если нужны метрики производительности. Простой `System.nanoTime()` до и после создания `HTMLDocument` покажет, сколько занял парсинг.
- **Pitfall:** Жёстко задавать количество потоков. Лучше использовать `Runtime.getRuntime().availableProcessors()` для выбора разумного значения по умолчанию:

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## Related Topics You Might Explore Next

- **run tasks concurrently java** с `CompletableFuture` для более выразительных конвейеров.
- Сохранение подсчётов изображений в базе данных для аналитических панелей.
- Использование **java parallel file processing** с API `java.nio.file.Files.walk` в сочетании со стримами.
- Реализация собственного `ThreadFactory` для присвоения потокам осмысленных имён (упрощает отладку).

## Conclusion

Мы только что прошли полный, автономный пример, показывающий, как **java fixed thread pool** можно использовать для **how to count images** в нескольких HTML‑файлах, одновременно демонстрируя правильный способ **shutdown executor service**. Шаблон масштабируется – замените массив файлов на динамический список, увеличьте размер пула, и у вас будет надёжное решение для любой нагрузки **java parallel file processing**.  

Попробуйте, поиграйте с количеством потоков и, возможно, добавьте экспорт результатов в CSV. Возможности безграничны, когда у вас есть прочный фундамент конкурентности и удобная библиотека, такая как Aspose.HTML. Happy coding!  

![java fixed thread pool diagram](image.png){alt="java fixed thread pool diagram"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}