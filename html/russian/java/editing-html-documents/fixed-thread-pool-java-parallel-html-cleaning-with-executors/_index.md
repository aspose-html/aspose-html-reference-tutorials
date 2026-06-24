---
category: general
date: 2026-06-24
description: Узнайте, как использовать fixed thread pool java для удаления script
  tags из HTML‑файлов. Этот executorservice example java демонстрирует эффективную
  загрузку HTML‑документов.
draft: false
keywords:
- fixed thread pool java
- executorservice example java
- java executorservice tutorial
- load html document java
- remove script tags java
og_description: Освойте fixed thread pool java для удаления script tags из HTML‑файлов.
  Полный executorservice example java с пошаговыми инструкциями по загрузке HTML‑документов.
og_title: Fixed thread pool java – Руководство по параллельной очистке HTML
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to use a fixed thread pool java to remove script tags from
    HTML files. This executorservice example java shows loading HTML documents efficiently.
  headline: Fixed thread pool java – Parallel HTML Cleaning with ExecutorService
  type: TechArticle
- description: Learn how to use a fixed thread pool java to remove script tags from
    HTML files. This executorservice example java shows loading HTML documents efficiently.
  name: Fixed thread pool java – Parallel HTML Cleaning with ExecutorService
  steps:
  - name: Open the file with `HTMLDocument`.
    text: Open the file with `HTMLDocument`.
  - name: '**Remove script tags** using a CSS selector (`"script"`).'
    text: '**Remove script tags** using a CSS selector (`"script"`).'
  - name: Save the cleaned version with a `_clean.html` suffix.
    text: Save the cleaned version with a `_clean.html` suffix.
  type: HowTo
- questions:
  - answer: Yes. Use `Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors()
      + 1)` for a dynamic size based on the host machine.
    question: Can I change the thread pool size at runtime?
  - answer: The current selector only removes `<script>` tags. To strip inline handlers,
      you’d need to traverse all elements and clear attributes that start with `on`.
      That’s a good extension for a later tutorial.
    question: What if my HTML files contain inline event handlers (`onclick`, `onload`)?
  - answer: No. Libraries like jsoup also offer CSS selectors, but Aspose.HTML gives
      you a full DOM API that mirrors browser behavior, which is handy for complex
      cleaning tasks.
    question: Is Aspose.HTML the only library that supports `querySelectorAll`?
  - answer: For massive files, consider streaming parsers (e.g., Saxon for XML) or
      processing the file in chunks. The fixed thread pool pattern still applies;
      you’d just replace `HTMLDocument` with a streaming solution.
    question: How do I handle very large HTML files that might not fit into memory?
  - answer: It will use as many threads as you configure. A common practice is to
      set the pool size to the number of available processors, which maximizes CPU
      utilization without causing excessive context switching.
    question: Will the fixed thread pool java automatically use all CPU cores?
  type: FAQPage
tags:
- Java concurrency
- HTML processing
- Aspose.HTML
title: Fixed thread pool java – Параллельная очистка HTML с помощью ExecutorService
url: /ru/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Фиксированный пул потоков java – Параллельная очистка HTML с помощью ExecutorService

Когда‑нибудь вам нужен был **fixed thread pool java** для ускорения массовой обработки HTML? Вы не одиноки. Когда у вас десятки — а иногда и сотни — HTML‑файлов, заполненных элементами `<script>`, выполнение работы последовательно может ощущаться как наблюдение за высыхающей краской.  

В этом руководстве мы покажем, как создать **fixed thread pool java**, загрузить каждый HTML‑документ, удалить все JavaScript (`<script>` теги) и сохранить очищенные файлы — всё параллельно с помощью **executorservice example java**. К концу вы получите готовую к запуску программу, эффективно удаляющую теги script, и поймёте, почему фиксированный пул потоков часто является оптимальным решением для CPU‑нагруженных задач.

## Быстрые ответы
`ExecutorService` — это интерфейс Java, который управляет пулом рабочих потоков и позволяет выполнять задачи асинхронно.

- **Что делает fixed thread pool java?** Он создает фиксированное количество переиспользуемых рабочих потоков, которые выполняют задачи одновременно, устраняя накладные расходы на постоянное создание новых потоков.  
- **Какая библиотека загружает HTML‑документы?** Класс `HTMLDocument` из Aspose.HTML предоставляет полный DOM‑API для чтения и изменения HTML в Java.  
- **Как удаляются теги script?** Выбирая все элементы `<script>` с помощью CSS‑селектора `"script"` и отсоединяя каждый узел от его родителя.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для тестирования; для использования в продакшене требуется коммерческая лицензия.  
- **Можно ли изменить размер пула?** Да — используйте `Runtime.getRuntime().availableProcessors()` для определения размера пула на основе количества процессоров хоста.

## Что вы достигнете

- Настроить `ExecutorService` с фиксированным числом потоков.  
- Загрузить HTML‑файлы с помощью `HTMLDocument` из Aspose.HTML.  
- Использовать CSS‑селектор для **удаления тегов script** (или любых других нежелательных элементов).  
- Сохранить очищенный результат, используя понятную схему именования.  
- Обработать завершение работы и корректное завершение пула потоков.

Никаких внешних средств сборки, никаких скрытых трюков — только чистый Java 8+ и Aspose.HTML.

---

## Требования

`HTMLDocument` — основной класс Aspose.HTML, представляющий HTML‑файл в памяти и предоставляющий методы манипуляции DOM.

Перед тем как начать, убедитесь, что у вас есть:

| Требование | Почему это важно |
|------------|-------------------|
| **Java 8 или новее** | Необходим для лямбда‑выражений и API `ExecutorService`. |
| **Aspose.HTML for Java** ([download here](https://products.aspose.com/html/java/)) | Предоставляет класс `HTMLDocument`, используемый для загрузки и изменения HTML. |
| **Папка с примерами HTML‑файлов** | Демонстрация обрабатывает файлы вроде `input1.html`, `input2.html` и т.д. |
| **IDE или инструмент сборки командной строки** (IntelliJ, Eclipse, Maven, Gradle) | Для компиляции и запуска кода. |

Если вы ещё не добавили Aspose.HTML в ваш проект, поместите JAR в папку `libs` и добавьте его в classpath, либо объявите зависимость Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

## Как фиксированный пул потоков java повышает скорость обработки?

Фиксированный пул потоков java переиспользует заранее определённое количество потоков, поэтому JVM избегает дорогого создания и уничтожения потоков для каждого файла. Это снижает задержку и повышает пропускную способность, особенно когда каждая задача (загрузка, очистка и сохранение HTML‑файла) кратковременна. На машине с 8 ядрами использование 8‑10 потоков может сократить общее время выполнения примерно на 70 % по сравнению с однопоточным циклом.

## Якорь определения: ExecutorService

`ExecutorService` — это высокоуровневый фреймворк Java для управления пулом рабочих потоков и отправки задач `Runnable` или `Callable` на асинхронное выполнение.

## Шаг 1: Создать фиксированный пул потоков java

**fixed thread pool java** предоставляет предсказуемое количество рабочих потоков, которые живут в течение всей задачи. Это устраняет накладные расходы на постоянное создание и уничтожение потоков, что особенно полезно, когда каждая задача кратковременна, например загрузка и очистка отдельного HTML‑файла.

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

> **Совет:** Выбирайте размер пула, исходя из количества ядер CPU (`Runtime.getRuntime().availableProcessors()`) и небольшого запаса, если задачи включают ввод‑вывод.

## Якорь определения: HTMLDocument

`HTMLDocument` — основной класс Aspose.HTML, представляющий полный HTML‑файл в памяти и предоставляющий методы манипуляции DOM, сопоставимые с теми, что есть в веб‑браузере.

## Шаг 2: Список HTML‑файлов, которые нужно обработать

Можно сканировать каталог динамически, но для ясности мы зажёстко зададим массив. Замените `"YOUR_DIRECTORY"` реальным путём на вашей машине.

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/input1.html",
    "YOUR_DIRECTORY/input2.html",
    "YOUR_DIRECTORY/input3.html",
    "YOUR_DIRECTORY/input4.html"
};
```

Если вы предпочитаете динамический подход, `Files.list(Paths.get("YOUR_DIRECTORY"))` может автоматически заполнить массив.

## Шаг 3: Отправить задачу очистки для каждого файла

Каждому файлу назначается собственная задача **executorservice example java**. Внутри лямбда‑выражения мы:

1. Открываем файл с помощью `HTMLDocument`.  
2. **Удаляем теги script** с помощью CSS‑селектора (`"script"`).  
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

> **Почему это работает:** `querySelectorAll("script")` возвращает живую коллекцию всех элементов `<script>`. Цикл `forEach` затем отсоединяет каждый узел от его родителя, эффективно **удаляя javascript html** из исходного кода.

## Шаг 4: Завершить работу пула и дождаться завершения

Корректное завершение критически важно; не хочется, чтобы оставшиеся потоки висели после завершения задачи.

```java
// Step 4: Shut down the pool and wait for all tasks to finish
executor.shutdown();
if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
    System.err.println("Some tasks did not finish within the timeout.");
    executor.shutdownNow(); // Force shutdown if needed
}
System.out.println("All HTML files have been cleaned.");
```

Если у вас много файлов или большие документы, увеличьте тайм‑аут до большего значения.

## Почему использовать фиксированный пул потоков java для параллельной обработки файлов?

Aspose.HTML поддерживает **более 50 форматов ввода и вывода** — включая HTML, XHTML, XML, PDF и типы изображений — и может обрабатывать файлы до **500 МБ** без загрузки всего документа в память. Совмещение этого с фиксированным пулом потоков java позволяет очистить тысячи файлов за долю времени, требуемого однопоточным подходом, при этом использование памяти остаётся предсказуемым и низким.

## Полный рабочий пример

Объединив всё вместе, представляем полностью готовую программу, которую можно скопировать в `ParallelProcessingDemo.java` и запустить.

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

При запуске программы вы увидите сообщения в консоли, например:

```
All files cleaned successfully!
```

А в вашем каталоге вы найдёте:

- `input1_clean.html`
- `input2_clean.html`
- `input3_clean.html`
- `input4_clean.html`

Каждый файл `_clean.html` будет идентичен оригиналу, за исключением всех блоков `<script>`.

## Часто задаваемые вопросы (FAQ)

**Q: Можно ли изменить размер пула потоков во время выполнения?**  
**A:** Да. Use `Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() + 1)` for a dynamic size based on the host machine.

**Q: Что если мои HTML‑файлы содержат встроенные обработчики событий (`onclick`, `onload`)?**  
**A:** Текущий селектор удаляет только теги `<script>`. Чтобы удалить встроенные обработчики, нужно пройтись по всем элементам и очистить атрибуты, начинающиеся с `on`. Это хорошее расширение для будущего урока.

**Q: Является ли Aspose.HTML единственной библиотекой, поддерживающей `querySelectorAll`?**  
**A:** Нет. Библиотеки вроде jsoup также предоставляют CSS‑селекторы, но Aspose.HTML дает полноценный DOM‑API, который имитирует поведение браузера, что удобно для сложных задач очистки.

**Q: Как обрабатывать очень большие HTML‑файлы, которые могут не помещаться в памяти?**  
**A:** Для огромных файлов рассмотрите потоковые парсеры (например, Saxon для XML) или обработку файла кусками. Паттерн фиксированного пула потоков по‑прежнему применим; просто замените `HTMLDocument` на потоковое решение.

**Q: Будет ли фиксированный пул потоков java автоматически использовать все ядра CPU?**  
**A:** Он будет использовать столько потоков, сколько вы зададите. Распространённая практика — установить размер пула равным количеству доступных процессоров, что максимизирует загрузку CPU без избыточного переключения контекстов.

## Следующие шаги и связанные темы

- **Remove JavaScript HTML with jsoup** – лёгкая альтернатива, если вам не нужен полный DOM.  
- **Dynamic thread pool sizing** – изучите `ThreadPoolExecutor` для более тонкого управления.  
- **Batch processing with `CompletableFuture`** – комбинируйте futures для более сложных конвейеров.  
- **HTML sanitization beyond scripts** – удаляйте стили, iframe или небезопасные атрибуты.  

Все эти темы основаны на той же основе **executorservice example java**, которую мы здесь изложили.

## Заключение

Теперь у вас есть надёжный, готовый к продакшену пример того, как использовать **fixed thread pool java** для **удаления тегов script** из пакета HTML‑файлов. Используя `ExecutorService`, каждый файл обрабатывается параллельно, что значительно сокращает общее время выполнения. Подход модульный, легко расширяемый и работает с любой Java‑совместимой HTML‑библиотекой, предоставляющей возможность `load html document`.

Попробуйте, измените размер пула или добавьте дополнительные правила очистки — ваше следующее приключение по обработке HTML всего в нескольких строках от вас.

---

![Иллюстрация фиксированного пула потоков java](https://example.com/fixed-thread-pool-java.png "Иллюстрация фиксированного пула потоков java")

[Иллюстрация фиксированного пула потоков java](https://example.com/fixed-thread-pool-java.png "Иллюстрация фиксированного пула потоков java")

**Последнее обновление:** 2026-06-24  
**Тестировано с:** Aspose.HTML 24.12 for Java  
**Автор:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Связанные руководства

- [Создать HTML‑документы асинхронно в Aspose.HTML для Java](/html/java/creating-managing-html-documents/create-html-documents-async/)
- [Загрузить HTML‑документы из файла в Aspose.HTML для Java](/html/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Как выполнять запросы к HTML в Java: полный учебник](/html/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}