---
category: general
date: 2026-04-19
description: Извлекайте HTML из MHTML быстро с помощью Java. Узнайте, как конвертировать
  MHTML в HTML, извлекать тело письма, записывать строку в файл и обрабатывать конверсию
  MHT.
draft: false
keywords:
- extract html from mhtml
- convert mhtml to html
- extract email body
- write string to file
- convert mht to html
language: ru
og_description: Извлечение HTML из MHTML в Java. Это руководство показывает, как преобразовать
  MHTML в HTML, извлечь тело письма и записать строку в файл.
og_title: Извлечение HTML из MHTML – пошаговое руководство по Java
tags:
- Java
- Aspose.HTML
- Email Processing
title: Извлечение HTML из MHTML – Полное руководство по Java
url: /ru/java/creating-managing-html-documents/extract-html-from-mhtml-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение HTML из MHTML – Полное руководство по Java

Когда‑нибудь вам нужно было **извлечь HTML из MHTML**, но вы не знали, с чего начать? Возможно, вы получили архивированное письмо (`.mht`) и хотите получить чистое тело для веб‑просмотра, или вы создаёте скрипт миграции, который преобразует устаревшие архивы в современные HTML‑страницы. В любом случае проблема одна: у вас есть однопоточный веб‑архив, и вам нужен сырой HTML‑разметка из него.

Хорошие новости? С несколькими строками кода на Java и библиотекой Aspose.HTML вы можете **конвертировать MHTML в HTML**, извлечь тело письма и даже записать эту строку в файл — всё это не покидая вашу IDE. В этом руководстве мы пройдём весь процесс, объясним, почему каждый шаг важен, и покажем, как справляться с типичными краевыми случаями, такими как отсутствие ресурсов или кодировки, отличные от UTF‑8.

> **Краткое резюме:** К концу этого руководства вы сможете **извлечь тело письма**, **конвертировать MHTML в HTML** и **записать строку в файл** с помощью чистого, переиспользуемого фрагмента кода, который работает с любым `.mht` или `.mhtml`, который вы ему передадите.

---

## Что понадобится

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

- **Java 17+** (код использует шаблон try‑with‑resources, доступный с Java 7, но Java 17 — текущий LTS).
- **Aspose.HTML for Java** JAR‑файлы в вашем classpath. Их можно скачать с [сайта Aspose](https://products.aspose.com/html/java/) или подключить через Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- Пример файла **`.mht` или `.mhtml`**, который вы хотите обработать. Для демонстрации будем использовать `email.mht` и разместим его в `YOUR_DIRECTORY`.

Вот и всё — никаких дополнительных фреймворков, никаких тяжёлых парсеров. Просто чистый Java и одна хорошо документированная библиотека.

---

## Шаг 1 – Открыть файл MHTML как поток

Первое, что мы делаем, — открываем архивированное письмо как `InputStream`. Использование потока снижает потребление памяти, особенно для больших файлов `.mht`, которые могут содержать встроенные изображения или CSS.

```java
// Step 1: Open the MHTML file as a stream
try (InputStream mhtmlStream = new FileInputStream("YOUR_DIRECTORY/email.mht")) {
    // Subsequent steps go inside this block
}
```

**Почему поток?**  
Поток позволяет `MhtmlDocument` читать данные «на лету», что значит, вы не получите `OutOfMemoryError`, даже если архив весит несколько мегабайт. Кроме того, это даёт гибкость чтения из других источников позже (например, `ByteArrayInputStream` из базы данных).

---

## Шаг 2 – Загрузить документ MHTML из потока

Теперь передаём поток классу `MhtmlDocument` от Aspose. Этот класс парсит MIME‑закодированный архив и строит DOM‑подобное представление встроенного HTML.

```java
// Step 2: Load the MHTML document from the stream
MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);
```

**Что происходит за кулисами:**  
Aspose извлекает каждую часть MIME (HTML, изображения, CSS) и собирает их внутри себя. Поэтому позже вы можете запросить только HTML‑часть, не беспокоясь о встроенных ресурсах.

---

## Шаг 3 – Получить основной HTML‑контент

После загрузки документа получение сырого HTML — это однострочник. Метод `getHtmlContent()` возвращает тело в виде `String`, сохраняя оригинальную разметку.

```java
// Step 3: Retrieve the main HTML content as a string
String htmlContent = mhtmlDoc.getHtmlContent();
```

**Что вы получаете:**  
`htmlContent` содержит полную HTML‑страницу — включая теги `<head>` и `<body>` — точно так, как она выглядела при сохранении письма. Если нужен только видимый контент, позже можно распарсить его с помощью Jsoup и убрать `<head>`.

---

## Шаг 4 – Записать извлечённый HTML в отдельный файл

Сохранить строку на диск просто с помощью API `java.nio.file`. Этот шаг демонстрирует шаблон **write string to file**, который работает на любой платформе.

```java
// Step 4: Save the extracted HTML to a separate file
Files.writeString(Path.of("YOUR_DIRECTORY/email_body.html"), htmlContent);
```

**Подсказка:**  
Если нужен определённый набор символов, используйте `Files.writeString(Path, CharSequence, Charset)`. По умолчанию — UTF‑8, что подходит для большинства современных писем.

---

## Шаг 5 – Подтвердить извлечение

Быстрый `System.out.println` позволяет убедиться, что всё выполнено без исключений. В продакшн‑задаче вы замените его на proper logging.

```java
// Step 5: Indicate successful extraction
System.out.println("HTML extracted.");
```

При запуске программы в консоли вы должны увидеть `HTML extracted.`, а файл `email_body.html` появится в `YOUR_DIRECTORY`.

---

## Полный готовый к запуску пример

Собрав всё вместе, получаем полностью автономный Java‑класс. Смело копируйте‑вставляйте его в IDE и нажимайте **Run**.

```java
import com.aspose.html.MhtmlDocument;
import java.io.FileInputStream;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;

public class MhtmlToHtmlConverter {

    public static void main(String[] args) {
        // Adjust the path to point to your .mht/.mhtml file
        String sourcePath = "YOUR_DIRECTORY/email.mht";
        String targetPath = "YOUR_DIRECTORY/email_body.html";

        // Try-with-resources ensures the stream is closed automatically
        try (InputStream mhtmlStream = new FileInputStream(sourcePath)) {

            // Load the MHTML document
            MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);

            // Extract the HTML content
            String htmlContent = mhtmlDoc.getHtmlContent();

            // Write the HTML string to a new file
            Files.writeString(Path.of(targetPath), htmlContent);

            // Simple confirmation output
            System.out.println("HTML extracted to " + targetPath);
        } catch (Exception e) {
            // In real code you might want to log this instead of printing
            System.err.println("Failed to extract HTML: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Ожидаемый вывод

При запуске программа выводит что‑то вроде:

```
HTML extracted to YOUR_DIRECTORY/email_body.html
```

А `email_body.html` будет содержать полный HTML‑исходник оригинального письма. Откройте его в браузере — вы увидите то же визуальное отображение, что и в оригинальном архивированном сообщении (за исключением внешних ресурсов, которые не были включены).

---

## Обработка типичных краевых случаев

### 1. Отсутствующие встроенные ресурсы

Иногда файл MHTML ссылается на внешние изображения, которые не были сохранены внутри архива. В таких случаях `getHtmlContent()` всё равно возвращает разметку `<img src="...">`, но URL‑адреса будут указывать на оригинальное веб‑место. Если нужен полностью автономный HTML‑файл, можно:

- Использовать `MhtmlDocument.save(Path, SaveFormat.HTML)`, чтобы Aspose извлекла все ресурсы в папку.
- Или пост‑обработать HTML с помощью библиотеки **Jsoup**, заменив удалённые URL‑ы на data‑URI в формате base64.

### 2. Кодировки, отличные от UTF‑8

Если письмо было сохранено в другой кодировке (например, `windows-1252`), полученная строка может содержать «кракозябры». Можно принудительно задать нужную кодировку при записи:

```java
Files.writeString(
    Path.of(targetPath),
    htmlContent,
    StandardCharsets.ISO_8859_1
);
```

### 3. Большие файлы

Для архивов более нескольких сотен мегабайт рассмотрите возможность потоковой записи HTML‑вывода напрямую в `BufferedWriter`, вместо загрузки всей строки в память. Aspose также предлагает метод **`save`**, который пишет сразу в файл, обходя промежуточный `String`.

---

## Профессиональные советы и лучшие практики

- **Повторно используйте объект `MhtmlDocument`**, если нужно извлечь несколько частей (например, CSS, изображения). Он парсит архив только один раз.
- **Проверяйте вывод** с помощью HTML‑валидатора (W3C validator или `jsoup.isValid()`), если планируете передавать HTML в другую систему.
- **Логируйте, а не печатайте** в продакшене. Замените `System.out.println` на фреймворк логирования, например SLF4J, чтобы фиксировать метки времени и уровни важности.
- **Контролируйте версии зависимостей.** Aspose часто выпускает обновления; зафиксируйте версию в `pom.xml`, чтобы избежать неожиданного поломания.

---

## Заключение

Мы только что прошли практическое, сквозное решение для **извлечения HTML из MHTML** с помощью Java. Открыв архив как поток, загрузив его через Aspose.HTML, получив строку HTML и **записав строку в файл**, вы теперь имеете надёжный способ **конвертировать MHTML в HTML**, **извлекать тело письма** и даже **конвертировать MHT в HTML** для последующей обработки.

Не стесняйтесь адаптировать фрагмент: замените `FileInputStream` на `ByteArrayInputStream`, если ваши архивы хранятся в базе данных, или интегрируйте код в более крупную пакетную задачу, обрабатывающую десятки писем за раз. Основная идея остаётся прежней — позвольте специализированной библиотеке выполнить тяжёлую работу, а затем работайте с полученным текстом как вам нужно.

**Следующие шаги**, которые можно изучить:

- Использовать Jsoup для **очистки извлечённого HTML** (удаление трекинговых пикселей, инлайн‑CSS и т.д.).
- Автоматизировать **массовую конверсию**, перебирая каталог файлов `.mht`.
- Скомбинировать это с **Apache POI**, чтобы внедрять очищенный HTML в документы Word или PDF.

Есть вопросы по конкретному краевому случаю или хотите поделиться, как расширили скрипт? Оставляйте комментарий ниже — счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}