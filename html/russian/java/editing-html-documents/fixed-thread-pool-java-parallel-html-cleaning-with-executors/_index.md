---
category: general
date: 2026-01-01
description: Узнайте, как использовать фиксированный пул потоков в Java для удаления
  тегов `script` из HTML‑файлов. Этот пример с `ExecutorService` на Java демонстрирует
  эффективную загрузку HTML‑документов.
draft: false
keywords:
- fixed thread pool java
- remove script tags
- remove javascript html
- executorservice example java
- load html document
language: ru
og_description: Освойте фиксированный пул потоков в Java для удаления тегов `script`
  из HTML‑файлов. Полный пример ExecutorService в Java с шагами загрузки HTML‑документа.
og_title: Фиксированный пул потоков Java – Руководство по параллельной очистке HTML
tags:
- Java concurrency
- HTML processing
- Aspose.HTML
title: Фиксированный пул потоков Java – Параллельная очистка HTML с помощью ExecutorService
url: /ru/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fixed thread pool java – Параллельная очистка HTML с помощью ExecutorService

Когда‑то вам нужен **fixed thread pool java**, чтобы ускорить массовую обработку HTML? Вы не одиноки. Если у вас десятки — а то и сотни — HTML‑файлов, заваленных элементами `<script>`, последовательная обработка ощущается, как наблюдение за высыхающей краской.  

В этом руководстве мы покажем, как создать **fixed thread pool java**, загрузить каждый HTML‑документ, удалить весь JavaScript (`<script>`‑теги) и сохранить очищенные файлы — все это параллельно с помощью **executorservice example java**. К концу вы получите готовую к запуску программу, эффективно удаляющую script‑теги, и поймёте, почему фиксированный пул потоков часто является оптимальным решением для CPU‑ограниченных задач.

## Что вы получите

- Настроите `ExecutorService` с фиксированным числом потоков.  
- Загрузите HTML‑файлы с помощью `HTMLDocument` из Aspose.HTML.  
- С помощью CSS‑селектора **удалите script‑теги** (или любые другие нежелательные элементы).  
- Сохраните очищенный результат, используя понятную схему именования.  
- Обработаете завершение работы и корректное завершение пула потоков.

Никаких внешних систем сборки, никаких скрытых трюков — только чистый Java 8+ и Aspose.HTML.

---

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

| Требование | Почему это важно |
|-------------|----------------|
| **Java 8 или новее** | Необходима для лямбда‑выражений и API `ExecutorService`. |
| **Aspose.HTML for Java** (скачать с <https://products.aspose.com/html/java/>) | Предоставляет класс `HTMLDocument` для загрузки и манипуляций HTML. |
| **Папка с образцами HTML‑файлов** | Демонстрация обрабатывает файлы вроде `input1.html`, `input2.html` и т.д. |
| **IDE или инструмент сборки** (IntelliJ, Eclipse, Maven, Gradle) | Для компиляции и запуска кода. |

Если вы ещё не добавили Aspose.HTML в проект, поместите JAR‑файл в папку `libs` и добавьте его в classpath, либо объявите Maven‑зависимость:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

---

## Шаг 1: Создайте Fixed Thread Pool java

**Fixed thread pool java** предоставляет предсказуемое количество рабочих потоков, которые живут на протяжении всей задачи. Это избавляет от накладных расходов на постоянное создание и уничтожение потоков, что особенно полезно, когда каждая задача короткоживущая, например загрузка и очистка отдельного HTML‑файла.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

public class ParallelProcessingDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
        // ...
    }
}
```

> **Совет:** Выбирайте размер пула, исходя из количества ядер CPU (`Runtime.getRuntime().availableProcessors()`) плюс небольшой резерв, если задачи включают ввод‑вывод.

---

## Шаг 2: Список HTML‑файлов для обработки

Можно сканировать каталог динамически, но для наглядности мы зафиксируем массив. Замените `"YOUR_DIRECTORY"` на реальный путь к папке на вашем компьютере.

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/input1.html",
    "YOUR_DIRECTORY/input2.html",
    "YOUR_DIRECTORY/input3.html",
    "YOUR_DIRECTORY/input4.html"
};
```

Если предпочитаете динамический подход, `Files.list(Paths.get("YOUR_DIRECTORY"))` может автоматически заполнить массив.

---

## Шаг 3: Отправьте задачу очистки для каждого файла

Каждому файлу соответствует собственная задача **executorservice example java**. Внутри лямбда‑выражения мы:

1. Открываем файл с помощью `HTMLDocument`.  
2. **Удаляем script‑теги** с помощью CSS‑селектора (`"script"`).  
3. Сохраняем очищенную версию с суффиксом `_clean.html`.

```java
for (String htmlFile : htmlFiles) {
    executor.submit(() -> {
        // Load the document (each thread works with its own instance)
        try (HTMLDocument doc = new HTMLDocument(htmlFile)) {
            // Remove all <script> elements from the document
            doc.querySelectorAll("script")
               .forEach(node -> node.getParentNode().removeChild(node));

            // Save the cleaned document with a new name
            doc.save(htmlFile.replace(".html", "_clean.html"));
        } catch (Exception e) {
            System.err.println("Failed to process " + htmlFile + ": " + e.getMessage());
        }
    });
}
```

> **Почему это работает:** `querySelectorAll("script")` возвращает живую коллекцию всех элементов `<script>`. Цикл `forEach` затем отсоединяет каждый узел от родителя, эффективно **remove javascript html** из исходного кода.

---

## Шаг 4: Завершите работу пула и дождитесь окончания

Корректное завершение критично; не хочется оставлять «заблудившиеся» потоки после завершения задачи.

```java
// Step 4: Shut down the pool and wait for all tasks to finish
executor.shutdown();
if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
    System.err.println("Some tasks did not finish within the timeout.");
    executor.shutdownNow(); // Force shutdown if needed
}
System.out.println("All HTML files have been cleaned.");
```

Если файлов много или документы крупные, увеличьте значение тайм‑аута.

---

## Полный рабочий пример

Объединив всё вместе, получаем полную программу, которую можно скопировать в `ParallelProcessingDemo.java` и запустить.

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelProcessingDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ List the HTML files to be processed
        String[] htmlFiles = {
            "YOUR_DIRECTORY/input1.html",
            "YOUR_DIRECTORY/input2.html",
            "YOUR_DIRECTORY/input3.html",
            "YOUR_DIRECTORY/input4.html"
        };

        // 3️⃣ Submit a cleaning task for each file
        for (String htmlFile : htmlFiles) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(htmlFile)) {
                    // 🌟 Remove all <script> elements (remove script tags)
                    doc.querySelectorAll("script")
                       .forEach(node -> node.getParentNode().removeChild(node));

                    // Save cleaned version
                    doc.save(htmlFile.replace(".html", "_clean.html"));
                } catch (Exception e) {
                    System.err.println("Error processing " + htmlFile + ": " + e.getMessage());
                }
            });
        }

        // 4️⃣ Shut down the pool and wait for completion
        executor.shutdown();
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            System.err.println("Timeout reached before all tasks finished.");
            executor.shutdownNow();
        } else {
            System.out.println("All files cleaned successfully!");
        }
    }
}
```

### Ожидаемый вывод

При запуске вы увидите сообщения в консоли, например:

```
All files cleaned successfully!
```

А в вашей папке появятся:

- `input1_clean.html`
- `input2_clean.html`
- `input3_clean.html`
- `input4_clean.html`

Каждый файл `_clean.html` будет идентичен оригиналу, за исключением всех блоков `<script>`.

---

## Часто задаваемые вопросы (FAQ)

**В: Можно ли изменить размер пула потоков во время выполнения?**  
О: Да. Используйте `Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() + 1)` для динамического размера, основанного на характеристиках хоста.

**В: Что если мои HTML‑файлы содержат встроенные обработчики событий (`onclick`, `onload`)?**  
О: Текущий селектор удаляет только теги `<script>`. Чтобы избавиться от встроенных обработчиков, придётся пройтись по всем элементам и очистить атрибуты, начинающиеся с `on`. Это хорошее расширение для будущего урока.

**В: Является ли Aspose.HTML единственной библиотекой, поддерживающей `querySelectorAll`?**  
О: Нет. Библиотеки вроде jsoup тоже предлагают CSS‑селекторы, но Aspose.HTML предоставляет полноценный DOM‑API, максимально приближённый к поведению браузера, что удобно для сложных задач очистки.

**В: Как обрабатывать очень большие HTML‑файлы, которые могут не помещаться в памяти?**  
О: Для массивных файлов рассмотрите потоковые парсеры (например, Saxon для XML) или обработку файла кусками. Паттерн фиксированного пула потоков остаётся применимым; просто замените `HTMLDocument` на потоковое решение.

---

## Следующие шаги и смежные темы

- **Remove JavaScript HTML with jsoup** – лёгкая альтернатива, если вам не нужен полный DOM.  
- **Dynamic thread pool sizing** – изучите `ThreadPoolExecutor` для более тонкой настройки.  
- **Batch processing with `CompletableFuture`** – комбинируйте futures для более сложных конвейеров.  
- **HTML‑санитизация помимо скриптов** – удаляйте стили, iframes или небезопасные атрибуты.  

Все эти темы опираются на ту же основу **executorservice example java**, которую мы построили здесь.

---

## Заключение

Теперь у вас есть надёжный, готовый к продакшену пример использования **fixed thread pool java** для **remove script tags** из пакета HTML‑файлов. Благодаря `ExecutorService` каждый файл обрабатывается параллельно, что значительно сокращает общее время выполнения. Подход модульный, легко расширяется и работает с любой Java‑совместимой HTML‑библиотекой, предоставляющей возможность **load html document**.

Попробуйте, поиграйте с размером пула или добавьте новые правила очистки — ваше следующее приключение в обработке HTML всего в нескольких строках кода.

---

![Fixed thread pool java illustration](https://example.com/fixed-thread-pool-java.png "Fixed thread pool java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}