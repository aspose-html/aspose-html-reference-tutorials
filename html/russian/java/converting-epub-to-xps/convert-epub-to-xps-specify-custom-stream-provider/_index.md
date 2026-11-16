---
date: 2026-03-29
description: Узнайте, как легко конвертировать EPUB в XPS с помощью Aspose.HTML для
  Java. Следуйте этому пошаговому руководству для беспроблемного процесса конвертации.
linktitle: How to Convert EPUB to XPS with a Custom Stream Provider
second_title: Java HTML Processing with Aspose.HTML
title: Как конвертировать EPUB в XPS с помощью пользовательского поставщика потоков
url: /ru/java/converting-epub-to-xps/convert-epub-to-xps-specify-custom-stream-provider/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как конвертировать EPUB в XPS с помощью пользовательского провайдера потоков

В современном мире цифрового издательства **как конвертировать EPUB в XPS** является распространённой задачей — будь то необходимость фиксированного представления для печати, архивирования или обмена между устройствами Windows. Aspose.HTML for Java делает эту конвертацию простой, а использование пользовательского провайдера памяти позволяет держать весь процесс в памяти, что идеально подходит для облачных или высокопроизводительных сценариев. Ниже вы найдёте всё необходимое для начала, от предварительных требований до полного, готового к запуску примера.

## Быстрые ответы
- **Что создает конвертация?** XPS‑документ, сохраняющий макет и шрифты.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для тестирования; для продакшн‑использования требуется коммерческая лицензия.  
- **Можно ли запускать в контейнере?** Да — записи в файловую систему не требуются, если всё хранится в памяти.  
- **Какая версия Java поддерживается?** Java 8 или выше.  
- **Обязательно ли использовать пользовательский провайдер потоков?** Нет, но он даёт полный контроль над использованием памяти и обработкой вывода.

## Как конвертировать EPUB в XPS
Прежде чем перейти к коду, уточним, что именно делает конвертация и почему может потребоваться хранить всё в памяти.

### Что такое «конвертация EPUB в XPS»?
Конвертация файла EPUB в XPS преобразует переflow‑able формат электронной книги в документ фиксированного макета, независимый от устройства. XPS (XML Paper Specification) — аналог PDF от Microsoft, идеален для сценариев, где требуется точное визуальное представление, не меняющееся на разных платформах.

### Зачем использовать пользовательский провайдер потоков?
Пользовательский `MemoryStreamProvider` позволяет хранить результат конвертации в ОЗУ вместо записи временного файла на диск. Этот подход:
- Снижает нагрузку ввода‑вывода.  
- Повышает производительность в безсерверных или микросервисных архитектурах.  
- Обеспечивает гибкость потоковой передачи результата напрямую клиенту, облачному хранилищу или другому API.

## Предварительные требования

Чтобы успешно **конвертировать EPUB в XPS**, убедитесь, что выполнены следующие предварительные требования:

### 1. Библиотека Aspose.HTML for Java

Необходимо установить и настроить библиотеку Aspose.HTML for Java в вашей среде Java. Если вы ещё этого не сделали, можете скачать библиотеку по [ссылке для загрузки](https://releases.aspose.com/html/java/).

### 2. Входной файл EPUB

Вам нужен существующий файл EPUB, который вы хотите конвертировать в XPS. Убедитесь, что файл готов к процессу конвертации.

Теперь, когда все предварительные требования выполнены, пройдём процесс конвертации шаг за шагом.

## Импорт пакетов

Прежде чем начать, убедитесь, что импортированы необходимые пакеты Aspose.HTML for Java для использования её функций.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.saving.MemoryStreamProvider;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## Открытие файла EPUB

Сначала необходимо открыть существующий файл EPUB для чтения. На этом этапе мы используем `FileInputStream` для доступа к файлу EPUB.

```java
try (FileInputStream fileInputStream = new FileInputStream("path/to/your/input.epub")) {
    // Your code for Step 1
}
```

## Создание MemoryStreamProvider

Далее создайте экземпляр `MemoryStreamProvider`. Этот объект будет хранить результат конвертации в памяти.

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code for Step 2
}
```

## Конвертация EPUB в XPS

Теперь конвертируйте файл EPUB в XPS с помощью метода `Converter.convertEPUB`. `MemoryStreamProvider` предоставляет целевой поток.

```java
Converter.convertEPUB(
    fileInputStream,
    new XpsSaveOptions(),
    streamProvider.getStream().findFirst().get()
);
```

## Получение полученных данных

После завершения конвертации получите поток памяти, содержащий данные XPS.

```java
InputStream inputStream = streamProvider.getStream().findFirst().get();
```

## Сохранение результата (необязательно)

Если нужен физический файл — возможно для отладки или офлайн‑просмотра — запишите поток памяти на диск. В большинстве продакшн‑сценариев можно пропустить этот шаг и передавать данные напрямую клиенту.

```java
try (FileOutputStream fileOutputStream = new FileOutputStream("path/to/your/output.xps")) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## Полный исходный код

Ниже приведён полный готовый к запуску пример, объединяющий все части. Смело копируйте, вставляйте и адаптируйте его под свой проект.

```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of MemoryStreamProvider
            try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
                // Convert EPUB to XPS by using the MemoryStreamProvider
                com.aspose.html.converters.Converter.convertEPUB(
                        fileInputStream,
                        new com.aspose.html.saving.XpsSaveOptions(),
                        streamProvider.lStream
                );
                // Get access to the memory stream that contains the resulted data
                java.io.InputStream inputStream = streamProvider.lStream.stream().findFirst().get();
                // Flush the result data to the output file
                try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("output.xps"))) {
                    byte[] buffer = new byte[inputStream.available()];
                    inputStream.read(buffer);
                    fileOutputStream.write(buffer);
                }
            }
        }
```

## Распространённые проблемы и решения

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **`java.lang.OutOfMemoryError`** | Большие файлы EPUB могут превысить размер кучи по умолчанию, если они полностью находятся в памяти. | Увеличьте размер кучи JVM (`-Xmx`) или, если возможно, обрабатывайте EPUB частями. |
| Отсутствие шрифтов в XPS | Шрифты, не встроенные в EPUB, недоступны на машине конвертации. | Убедитесь, что необходимые шрифты установлены на сервере или встроены в EPUB. |
| `UnsupportedOperationException` от `MemoryStreamProvider` | Используется устаревшая версия Aspose.HTML. | Обновите до последней версии Aspose.HTML for Java. |

## Часто задаваемые вопросы

### 1. Что такое EPUB?

EPUB, сокращённо Electronic Publication, — широко используемый файловый формат для электронных книг. Он разработан для удобного чтения на различных устройствах, таких как электронные ридеры, планшеты и смартфоны.

### 2. Что такое XPS?

XPS расшифровывается как XML Paper Specification, документный формат, созданный Microsoft. Он используется для обмена и архивирования документов с единым внешним видом и макетом.

### 3. Зачем использовать Aspose.HTML for Java?

Aspose.HTML for Java — мощная библиотека, упрощающая задачи по работе с документами, их конвертации и рендерингу. Она предоставляет обширные возможности и поддержку различных форматов документов, делая её ценным инструментом для разработчиков.

### 4. Можно ли конвертировать другие форматы документов с помощью Aspose.HTML for Java?

Да, Aspose.HTML for Java поддерживает конвертацию различных форматов документов, включая HTML, EPUB, XPS и другие. Это универсальный инструмент для управления документами.

### 5. Где можно найти дополнительные ресурсы и поддержку?

Для документации и поддержки посетите [документацию Aspose.HTML for Java](https://reference.aspose.com/html/java/) и [форум поддержки](https://forum.aspose.com/).

---

**Последнее обновление:** 2026-03-29  
**Тестировано с:** Aspose.HTML for Java 24.12 (последняя версия на момент написания)  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}