---
category: general
date: 2026-06-19
description: Как запустить поток в Java с переиспользуемым Runnable, запустить несколько
  потоков, вывести имя потока и парсить HTML с помощью Java. Пошаговый пример.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: ru
og_description: Как запустить поток в Java с помощью Runnable, запустить несколько
  потоков, вывести имя потока и разобрать HTML на Java в едином, исполняемом примере.
og_title: Как запустить поток в Java – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: Как запустить поток в Java – Полное руководство
url: /ru/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как запустить поток в Java – Полное руководство

Когда‑нибудь задумывались **как запустить поток** в Java, не утопая в шаблонном коде? Вы не одиноки. Будь то веб‑краулер, обновление UI или просто необходимость вынести тяжёлый расчёт в отдельный поток — умение создавать потоки обязательно для любого Java‑разработчика.

В этом руководстве мы пройдём практический пример: **разобрать HTML с помощью Java**, вывести имя текущего потока и **запустить несколько потоков**, использующих одну и ту же логику. К концу вы будете знать **как использовать Runnable**, запустить несколько воркеров и увидеть ожидаемый вывод — всё в самодостаточном примере, который можно скопировать‑вставить прямо сейчас.

## Что вы узнаете

- Точные шаги **как запустить поток** с помощью класса `Thread` и `Runnable`.
- Как **запустить несколько потоков**, выполняющих одну задачу без дублирования кода.
- Самый простой способ **вывести имя потока** рядом с результатами обработки.
- Чистый метод **разбора HTML с помощью Java** с использованием лёгкого помощника `HTMLDocument` (или любого парсера, который вам нравится).
- Почему **как использовать runnable** важно для переиспользуемого, тестируемого кода.

Для базового примера внешние библиотеки не требуются, но мы укажем, где можно заменить их на Jsoup или другой парсер, если понадобится больше возможностей.

---

## Шаг 1: Определите переиспользуемую задачу – **как использовать runnable**

Первое, что нужно знать **как использовать runnable**, — это инкапсулировать работу, которую каждый поток будет выполнять. `Runnable` — это просто функциональный интерфейс с единственным методом `run()`, что делает его идеальным для лямбда‑выражений.

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**Почему это важно:** Держая логику внутри `Runnable`, вы можете передать её любому количеству объектов `Thread`, пулу потоков или даже сервису‑исполнителю позже. Это делает ваш код DRY и тестируемым.

---

## Шаг 2: **Как запустить поток** – создаём первого воркера

Теперь, когда у нас есть `Runnable`, запуск потока так же прост, как вызов конструктора `Thread`. Вопрос **как запустить поток** решается одной строкой:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

Обратите внимание на второй аргумент, `"Worker-1"`. Это имя появится, когда мы позже **выведем имя потока**, делая отладку гораздо менее загадочной.

---

## Шаг 3: **Запустить несколько потоков** – переиспользуем тот же Runnable

Хотите обрабатывать несколько HTML‑файлов одновременно? Просто создайте ещё один `Thread` с тем же `Runnable`. Это демонстрирует **запуск нескольких потоков** без копирования кода задачи:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

Оба потока — `Worker-1` и `Worker-2` — будут выполнять блок, определённый в `extractTextLength`, одновременно. Поскольку задача без состояния (она только читает файл), гонок нет.

---

## Шаг 4: **Вывести имя потока** во время разбора HTML

Внутри `Runnable` мы уже вызываем `Thread.currentThread().getName()`. Это канонический способ **вывести имя потока**. Вывод будет выглядеть примерно так (при условии, что тело HTML содержит 1 234 символа):

```
Worker-1: 1234
Worker-2: 1234
```

Если запустить программу на более крупном файле, каждая строка покажет одинаковую длину, потому что оба потока читают один и тот же файл. Измените путь или передайте имя файла как параметр, чтобы увидеть разные результаты.

---

## Шаг 5: Полный, runnable‑пример — от импорта до выполнения

Ниже полностью **самодостаточная** программа, которую можно поместить в файл `HtmlThreadDemo.java`. В ней есть небольшой заглушка `HTMLDocument`, чтобы код компилировался даже без реального парсера. Замените заглушку на Jsoup или любую другую библиотеку для продакшн‑использования.

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### Ожидаемый вывод

Если `page.html` содержит 2 567 символов внутри тега `<body>`, вы увидите примерно следующее:

```
Worker-1: 2567
Worker-2: 2567
```

Если файл не удаётся прочитать, будет выведен стек трассировки — благодаря блоку `catch`.

---

## Частые ошибки и профессиональные советы

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| **File not found** | Путь `"YOUR_DIRECTORY/page.html"` относительный к месту запуска JVM. | Используйте абсолютный путь или `Paths.get("").toAbsolutePath()` для отладки. |
| **Гонки** | Если `Runnable` изменяет общие данные, потоки могут конфликтовать. | Делайте задачу без состояния или синхронизируйте доступ к общим объектам. |
| **Слишком много потоков** | Создание десятков `Thread` может исчерпать ресурсы ОС. | Перейдите на `ExecutorService` с ограниченным пулом после освоения основ. |
| **Некорректный разбор HTML** | Заглушка `HTMLDocument` упрощённая; сложные страницы ломаются. | Замените её на Jsoup: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## Расширение примера

Теперь, когда вы знаете **как запустить поток**, вы можете:

- **Разбирать разные файлы**, передавая имя файла в `Runnable` (через конструктор или лямбду, захватывающую переменную).
- **Собирать результаты** в `ConcurrentLinkedQueue<Integer>` вместо простого вывода.
- **Использовать пул потоков** (`Executors.newFixedThreadPool(4)`) для лучшей масштабируемости.
- **Заменить парсер** на Jsoup, HtmlUnit или любую библиотеку, подходящую вашему проекту.

Все эти шаги всё равно опираются на ядро идеи: определить переиспользуемую задачу, передать её одному или нескольким потокам и наблюдать, какой поток работает, с помощью **вывода имени потока**.

---

## Заключение

Мы рассмотрели **как запустить поток** в Java, продемонстрировали **как использовать runnable** для переиспользуемой работы, показали, как **запустить несколько потоков**, и иллюстрировали простой способ **разбора HTML с помощью Java**, одновременно **выводя имя потока** для каждого воркера. Полный код выше готов к запуску, а концепции масштабируются до более сложных, производственных приложений.

Экспериментируйте: меняйте путь к файлу, увеличивайте количество воркеров или подключайте реальный HTML‑парсер. Основы остаются теми же, и теперь у вас прочный фундамент для любого многопоточного проекта на Java.

Есть вопросы о потокобезопасности, сервисах‑исполнителях или библиотеках парсинга HTML? Оставляйте комментарий ниже, и удачной разработки!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}