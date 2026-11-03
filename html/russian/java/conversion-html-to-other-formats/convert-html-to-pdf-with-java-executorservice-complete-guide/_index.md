---
category: general
date: 2026-04-19
description: Быстро преобразуйте HTML в PDF, используя пример Java ExecutorService.
  Изучите шаблон фиксированного пула потоков в Java для генерации PDF из HTML и безопасного
  завершения ExecutorService.
draft: false
keywords:
- convert html to pdf
- java executorservice example
- fixed thread pool java
- generate pdf from html
- shutdown executor service
language: ru
og_description: Эффективно преобразуйте HTML в PDF, используя подход с фиксированным
  пулом потоков в Java. В этом руководстве показан полный пример java ExecutorService,
  как генерировать PDF из HTML и как правильно завершать работу ExecutorService.
og_title: Конвертировать HTML в PDF с помощью Java ExecutorService – пошагово
tags:
- Java
- Concurrency
- PDF Generation
title: Конвертация HTML в PDF с помощью Java ExecutorService – Полное руководство
url: /ru/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-executorservice-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование HTML в PDF с помощью Java ExecutorService – Полное руководство

Когда‑то вам нужно **преобразовать HTML в PDF**, но вы беспокоитесь о скорости при наличии десятков файлов? Вы не одиноки. Во многих конвейерах пакетной обработки однопоточный подход становится узким местом, особенно когда сама библиотека конвертации ограничена вводом‑выводом.

Хорошая новость в том, что `ExecutorService` в Java позволяет создать **фиксированный пул потоков** и выполнять множество конвертаций параллельно, при этом сохраняя чистый код и контролируя ресурсы. В этом руководстве мы пройдём через **пример java executorservice**, который **генерирует PDF из HTML**, объяснит, почему фиксированный пул потоков — оптимальный вариант, и покажет правильный способ **завершения executor service** после завершения всех задач.

К концу этого руководства у вас будет готовая к запуску программа, которая принимает список HTML‑файлов, конвертирует каждый в PDF с помощью Aspose.HTML и корректно завершает работу — без «осиротевших» потоков и утечек памяти.

---

## Что вы создадите

- Java‑класс `ParallelBatch`, который читает массив путей к HTML‑файлам.  
- **Фиксированный пул потоков** (`Executors.newFixedThreadPool`), обрабатывающий каждую конвертацию одновременно.  
- Чистое управление жизненным циклом executor‑а с помощью `shutdown()` и `awaitTermination`.  
- Вывод в консоль, подтверждающий создание каждого PDF‑файла.

**Требования**

- Java 17 или новее (в коде используется синтаксис лямбда).  
- Библиотека Aspose.HTML for Java в classpath (скачайте с [aspose.com/html/java](https://products.aspose.com/html/java/)).  
- Папка с несколькими образцами `.html`‑файлов.

Никаких внешних систем сборки не требуется; можно компилировать `javac` и запускать `java`. Если предпочитаете Maven или Gradle, просто добавьте зависимость Aspose.HTML соответствующим образом.

---

## Шаг 1: Настройка проекта и зависимостей

### Почему это важно

Прежде чем любой код выполнится, JVM должна найти классы Aspose.HTML. Отсутствие jar‑файлов приводит к `ClassNotFoundException`, что является частой проблемой у новичков.

### Как сделать

1. **Создайте папку** `pdf‑converter`.  
2. **Скачайте** `aspose-html-<version>.jar` и поместите её в подпапку `libs`.  
3. **Организуйте** исходный файл так:

```
pdf-converter/
├─ libs/
│  └─ aspose-html-23.10.jar
└─ src/
   └─ ParallelBatch.java
```

Скомпилировать можно так:

```bash
javac -cp "libs/*" src/ParallelBatch.java -d out
```

И запустить:

```bash
java -cp "out:libs/*" ParallelBatch
```

*(В Windows замените `:` на `;` в classpath.)*

---

## Шаг 2: Список HTML‑файлов для конвертации

### Обоснование

Жёстко прописанный список файлов подходит для демонстрации, но в продакшене вы, скорее всего, будете сканировать каталог. Для простоты оставим массив; это демонстрирует основную логику без отвлечения на код ввода‑вывода.

### Код

```java
// Step 2: Define the source HTML files
String[] htmlFiles = {
    "YOUR_DIRECTORY/1.html",
    "YOUR_DIRECTORY/2.html",
    "YOUR_DIRECTORY/3.html"
};
```

Замените `YOUR_DIRECTORY` на абсолютный или относительный путь к папке с вашими HTML‑файлами.

---

## Шаг 3: Создание фиксированного пула потоков

### Почему фиксированный пул?

**Фиксированный пул потоков** (`newFixedThreadPool`) даёт предсказуемое количество рабочих потоков. Слишком много потоков могут исчерпать CPU или память, а слишком мало — недоиспользовать систему. Для CPU‑зависимых задач обычно берут `availableProcessors()`, но для I/O‑зависимой конвертации часто достаточно 3‑5 потоков для максимальной пропускной способности.

### Код

```java
// Step 3: Initialise a fixed‑size thread pool (3 threads in this example)
ExecutorService executor = Executors.newFixedThreadPool(3);
```

При необходимости подгоните размер пула под ваше оборудование и размер HTML‑файлов.

---

## Шаг 4: Отправка задачи конвертации для каждого HTML‑файла

### Как это работает

Каждая задача — это лямбда, которая:

1. Формирует имя PDF‑файла (`replace(".html", ".pdf")`).  
2. Вызывает `Conversion.convert` из Aspose.HTML.  
3. Печатает строку‑подтверждение.

Использование `executor.submit` гарантирует, что задача выполнится в одном из потоков пула.

### Код

```java
// Step 4: Enqueue conversion jobs
for (String htmlFilePath : htmlFiles) {
    executor.submit(() -> {
        // Derive the PDF output path
        String pdfFilePath = htmlFilePath.replace(".html", ".pdf");
        // Perform the conversion
        Conversion.convert(htmlFilePath, pdfFilePath);
        // Log the result
        System.out.println(pdfFilePath + " generated.");
    });
}
```

**Подсказка:** Если конвертация падает, Aspose бросает `Exception`. Оберните тело в `try‑catch`, чтобы логировать ошибки, не останавливая весь пул.

```java
executor.submit(() -> {
    try {
        String pdfFilePath = htmlFilePath.replace(".html", ".pdf");
        Conversion.convert(htmlFilePath, pdfFilePath);
        System.out.println(pdfFilePath + " generated.");
    } catch (Exception e) {
        System.err.println("Failed to convert " + htmlFilePath + ": " + e.getMessage());
    }
});
```

---

## Шаг 5: Корректное завершение Executor Service

### Почему корректное завершение?

Вызов `shutdown()` запрещает прием новых задач. `awaitTermination` блокирует поток, пока все поставленные в очередь задачи не завершатся **или** не истечёт тайм‑аут. Такой шаблон гарантирует, что приложение не завершится, пока фоновые потоки ещё работают, что часто приводит к обрезанным PDF‑файлам.

### Код

```java
// Step 5: Shut down the pool and wait for completion
executor.shutdown();                       // No new tasks
boolean finished = executor.awaitTermination(5, TimeUnit.MINUTES);

if (finished) {
    System.out.println("All PDFs generated successfully.");
} else {
    System.err.println("Timeout reached before all tasks finished.");
}
```

При необходимости увеличьте тайм‑аут, если ожидаете очень большие документы.

---

## Полный рабочий пример

Ниже полностью самодостаточная программа. Скопируйте её в `src/ParallelBatch.java`, поправьте пути к файлам и запустите, как описано в Шаге 1.

```java
import com.aspose.html.Conversion;
import java.util.concurrent.*;

public class ParallelBatch {
    public static void main(String[] args) throws Exception {
        // Step 1: List the HTML files that will be converted to PDF
        String[] htmlFiles = {
            "YOUR_DIRECTORY/1.html",
            "YOUR_DIRECTORY/2.html",
            "YOUR_DIRECTORY/3.html"
        };

        // Step 2: Create a fixed‑size thread pool to run conversions in parallel
        ExecutorService executor = Executors.newFixedThreadPool(3);

        // Step 3: For each HTML file, submit a conversion task to the pool
        for (String htmlFilePath : htmlFiles) {
            executor.submit(() -> {
                try {
                    String pdfFilePath = htmlFilePath.replace(".html", ".pdf");
                    // Convert HTML to PDF using Aspose.HTML
                    Conversion.convert(htmlFilePath, pdfFilePath);
                    System.out.println(pdfFilePath + " generated.");
                } catch (Exception e) {
                    System.err.println("Error converting " + htmlFilePath + ": " + e.getMessage());
                }
            });
        }

        // Step 4: Shut down the executor and wait for all tasks to finish
        executor.shutdown(); // stop accepting new tasks
        boolean terminated = executor.awaitTermination(5, TimeUnit.MINUTES);

        if (terminated) {
            System.out.println("All conversions completed.");
        } else {
            System.err.println("Some tasks did not finish within the timeout.");
        }
    }
}
```

**Ожидаемый вывод в консоль** (порядок может различаться из‑за параллелизма):

```
YOUR_DIRECTORY/1.pdf generated.
YOUR_DIRECTORY/2.pdf generated.
YOUR_DIRECTORY/3.pdf generated.
All conversions completed.
```

Если какая‑то конвертация завершится с ошибкой, вы увидите строку‑сообщение с причиной, но остальные задачи продолжат работу.

---

## Часто задаваемые вопросы и особые случаи

### 1. *Что делать, если у меня сотни HTML‑файлов?*

Увеличьте размер пула умеренно (например, `Runtime.getRuntime().availableProcessors()`) и рассмотрите чтение списка файлов из каталога:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
try (Stream<Path> stream = Files.list(dir)) {
    List<String> files = stream
        .filter(p -> p.toString().endsWith(".html"))
        .map(Path::toString)
        .collect(Collectors.toList());
    // feed `files` into the executor loop
}
```

### 2. *Можно ли ограничить потребление памяти?*

Aspose.HTML потоково читает исходный файл, но при работе с очень большими страницами можно задать пользовательские `ConversionOptions` с более низким параметром `MaxMemory`. В документации API указаны точные имена свойств.

### 3. *Что если конвертация «зависает»?*

Обёрните задачу в `Future` и используйте `future.get(timeout, TimeUnit.SECONDS)`. При истечении тайм‑аута отменяйте задачу:

```java
Future<?> future = executor.submit(task);
try {
    future.get(2, TimeUnit.MINUTES);
} catch (TimeoutException te) {
    future.cancel(true);
    System.err.println("Conversion timed out for " + htmlFilePath);
}
```

### 4. *Работает ли это на Windows и Linux?*

Да — `ExecutorService` и Aspose.HTML платформенно‑независимы. Просто убедитесь, что нативные библиотеки (если есть) доступны через `java.library.path`.

---

## Профессиональные советы и подводные камни

- **Совет:** Переиспользуйте один экземпляр `Conversion`, если библиотека это позволяет; это может снизить накладные расходы на создание объектов.  
- **Осторожно:** Жёстко прописанные пути с пробелами. Окружайте их кавычками или используйте объекты `Path`, чтобы избежать `FileNotFoundException`.  
- **Логирование:** Замените `System.out.println` на полноценный фреймворк логирования (SLF4J, Log4j) для продакшн‑видимости.  
- **Корректное завершение:** Всегда вызывайте `shutdown()` *даже* при возникновении исключения; блок `try‑finally` гарантирует очистку пула.

---

## Заключение

Мы только что **преобразовали HTML в PDF** с помощью **java executorservice example**, использующего **fixed thread pool java**. Код демонстрирует, как **генерировать PDF из HTML**, обрабатывать ошибки и правильно **завершать executor service** после выполнения всех задач.

Такой подход масштабируется от трёх файлов до тысяч, оставаясь отзывчивым и экономным по ресурсам. Дальше вы можете изучить:

- Добавление **мониторинга прогресса** через `CompletionService`.  
- Использование **динамических пулов** (`newCachedThreadPool`) для непредсказуемой нагрузки.  
- Интеграцию конвертера в **REST API**, чтобы другие сервисы могли инициировать генерацию PDF по запросу.

Попробуйте, поиграйте с размером пула и посмотрите, насколько ускорятся ваши пакетные конвертации. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}