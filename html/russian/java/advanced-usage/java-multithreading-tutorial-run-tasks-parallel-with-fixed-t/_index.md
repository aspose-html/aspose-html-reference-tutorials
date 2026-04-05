---
category: general
date: 2026-04-05
description: Учебник по многопоточности в Java, показывающий, как выполнять задачи
  параллельно с помощью фиксированного пула потоков и безопасно завершать ExecutorService.
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: ru
og_description: Учебник по многопоточности в Java, который пошагово показывает, как
  выполнять задачи параллельно, создавать фиксированный пул потоков, выводить имя
  потока и корректно завершать ExecutorService.
og_title: Учебник по многопоточности в Java – параллельное выполнение с фиксированным
  пулом потоков
tags:
- Java
- Concurrency
- ExecutorService
title: 'Учебник по многопоточности в Java: запуск задач параллельно с фиксированным
  пулом потоков'
url: /ru/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – Параллельное выполнение просто

Когда‑нибудь задавались вопросом, как **run tasks parallel** в Java без утопления в низкоуровневом управлении потоками? В этом **java multithreading tutorial** мы подробно покажем, как это сделать: используя **fixed thread pool java**, выводя имя каждого потока и корректно **shutdown executorservice**, когда работа завершена.  

Если вы когда‑либо писали цикл, блокирующийся на сетевом вводе‑выводе, или вам нужно одновременно собрать несколько веб‑страниц, шаблон, который мы рассмотрим ниже, сэкономит вам и время, и нервные клетки.  

Мы охватим всё, что вам нужно — без внешних документов, только чистый Java‑код, который вы можете скопировать, вставить, запустить и увидеть результаты. К концу вы поймёте, почему фиксированный пул потоков часто является оптимальным решением для ограниченного параллелизма, как безопасно его завершать и как сделать ваши логи более читаемыми, выводя имя потока.  

> **Prerequisites**: Java 8+ (пакет `java.util.concurrent` стабилен уже несколько лет), IDE или простая командная строка `javac`/`java`, а также базовое понимание ООП. Дополнительные библиотеки не требуются, кроме jar‑файла Aspose HTML for Java, который у вас уже есть.

---

![Диаграмма java multithreading tutorial, показывающая пул потоков, распределяющий задачи](https://example.com/images/java-multithreading-tutorial.png "Диаграмма java multithreading tutorial")

## java multithreading tutorial – Настройка фиксированного пула потоков

**Fixed thread pool** ограничивает количество одновременно работающих потоков, предотвращая создание вашим приложением слишком большого числа потоков ОС и исчерпание ресурсов. Здесь мы создаём пул из четырёх рабочих:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Почему именно четыре?* Это соответствует количеству URL, которые мы будем получать, но вы можете настроить это число в зависимости от количества ядер CPU, интенсивности ввода‑вывода или ограничений памяти. Фабрика `Executors` защищает вас от низкоуровневого конструктора `Thread` и предоставляет чистую ссылку `ExecutorService`, которую вы позже **shutdown executorservice**.

## Подготовка URL и определение параллельных задач

Далее мы перечисляем страницы, которые хотим обработать. В реальном скрейпере вы, вероятно, будете читать их из файла или базы данных, но статический массив делает пример автономным:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

Теперь переходим к части **run tasks parallel**. Для каждого URL мы отправляем лямбда‑выражение, которое загружает документ и выводит его заголовок. Обратите внимание на использование `Thread.currentThread().getName()` — это наш приём **print thread name**, который значительно упрощает отладку:

```java
        // Step 3: Submit a task for each URL that loads the document and prints its title
        for (String url : pageUrls) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(url)) {
                    String title = doc.getTitle();
                    // Print the thread name alongside the title
                    System.out.println(Thread.currentThread().getName() + " – " + title);
                } catch (Exception e) {
                    System.err.println(Thread.currentThread().getName() + " failed: " + e.getMessage());
                }
            });
        }
```

> **Pro tip**: Оборачивание `HTMLDocument` в блок try‑with‑resources гарантирует закрытие базового потока, даже если загрузка страницы не удалась.

## Корректное завершение ExecutorService

Оставление пула потоков живым после завершения его работы может привести к зависанию JVM. Правильный способ — **shutdown executorservice**, а затем ожидать завершения:

```java
        // Step 4: Shut down the pool and wait for all tasks to finish
        executor.shutdown();                         // No new tasks will be accepted
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            // Force shutdown if tasks exceed the timeout
            executor.shutdownNow();
        }
    }
}
```

*Почему нужен тайм‑аут?* Он защищает вас от «злостной» задачи, которая никогда не возвращается (например, зависший сетевой вызов). Если пул не завершится за одну минуту, мы вызываем `shutdownNow()`, чтобы прервать оставшиеся потоки.

### Ожидаемый вывод

Запуск программы выводит что‑то похожее на:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

Точный порядок может различаться — в конце концов задачи действительно параллельные. Постоянным остаётся префикс **print thread name**, который точно указывает, какой рабочий обработал каждый URL.

---

## Распространённые варианты и граничные случаи

| Ситуация | Что изменить | Причина |
|-----------|----------------|--------|
| **Больше URL, чем потоков** | Оставить тот же размер пула; лишние задачи автоматически ставятся в очередь. | Фиксированный пул обрабатывает back‑pressure за вас. |
| **CPU‑зависимая работа** | Установить размер пула в `Runtime.getRuntime().availableProcessors()` вместо жёстко заданных 4. | Максимизирует использование CPU без переизбытка. |
| **Необходимо отменить конкретную задачу** | Сохранить ссылку `Future<?>` из `executor.submit()` и вызвать `future.cancel(true)`. | Предоставляет тонкий контроль над отдельными задачами. |
| **Обработка больших файлов** | Увеличить размер пула умеренно *или* переключиться на `newCachedThreadPool()`, если ожидаются всплески. | Кешированные пулы создают потоки по требованию, но будьте осторожны с неограниченным ростом. |

---

## Заключение

Теперь у вас есть надёжный **java multithreading tutorial**, демонстрирующий, как **run tasks parallel** с помощью **fixed thread pool java**, использовать **print thread name** для ясного логирования и корректно **shutdown executorservice**. Полный, исполняемый код находится в одном классе, поэтому вы можете добавить его в любой проект и сразу начать масштабировать вашу I/O‑зависимую работу.  

Что дальше? Попробуйте заменить `HTMLDocument` на ваш собственный HTTP‑клиент, поэкспериментировать с различными размерами пула или интегрировать `CompletionService` для сбора результатов по мере их завершения. Вы также можете изучить `java.util.concurrent.Flow` для реактивных потоков, если вам требуется управление back‑pressure, выходящее за рамки простой очереди.  

Удачной разработки, и помните: с правильной стратегией пула потоков конкуренция становится *пустяком*, а не источником ошибок. Если у вас есть вопросы, смело оставляйте комментарий — я всегда рад обсудить Java‑конкурентность!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}