---
category: general
date: 2026-03-26
description: Создайте PDF произвольного размера из HTML с помощью Aspose.HTML для
  Java. Узнайте, как преобразовать HTML в PDF и установить размер страницы PDF за
  несколько простых шагов.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: ru
og_description: Создайте PDF пользовательского размера из HTML с помощью Aspose. Это
  руководство покажет, как конвертировать HTML в PDF, изменить размер страницы PDF
  и установить размер страницы PDF без усилий.
og_title: Создайте PDF нестандартного размера – Краткое руководство по конвертации
  HTML в PDF
tags:
- aspose
- java
- pdf
- html
title: Создать PDF пользовательского размера – конвертировать HTML в PDF с помощью
  Aspose
url: /ru/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PDF пользовательского размера – Конвертация HTML в PDF с помощью Aspose

Когда‑нибудь нужно было **создать PDF пользовательского размера** из HTML‑файла? В этом руководстве мы покажем, как **конвертировать HTML в PDF** и задать размер страницы PDF, используя Aspose.HTML for Java.  

Если вы создаёте счета, отчёты или электронные книги, точные размеры страницы имеют значение — иначе ваш макет будет смещён или обрезан.  

Мы пройдём каждый шаг: от загрузки исходного HTML до настройки полей, и закончим готовым PDF. Никаких расплывчатых ссылок, только полный, готовый к запуску пример, который можно скопировать‑вставить уже сегодня.

## Что понадобится

- **Java 17** (или любой современный JDK).  
- **Aspose.HTML for Java** JAR‑ы — их последнюю версию можно взять из Maven‑репозитория или с сайта Aspose.  
- Простой файл `input.html`, размещённый в папке, которой вы управляете.  
- IDE или текстовый редактор по вашему выбору; я обычно работаю в IntelliJ IDEA, но Eclipse тоже отлично подходит.

Наличие этих предварительных условий избавит вас от ошибок «class not found» в середине работы.  

А теперь давайте начнём.

![Пример создания PDF пользовательского размера](/images/create-pdf-custom-size.png "Скриншот, показывающий PDF, сгенерированный с пользовательским размером страницы и полями – create pdf custom size")

## Создание PDF пользовательского размера – Основные шаги

Ниже представлен полный Java‑программный код, который у вас получится. Скопируйте его в файл `ConvertHtmlToPdfCustomPage.java` и запустите после добавления зависимостей Aspose в ваш проект.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### Шаг 1 – Конвертация HTML в PDF: загрузка документа

Первое, что мы делаем, — **загружаем HTML**, который хотим превратить в PDF.  
`HTMLDocument` читает файл, разрешает относительные ссылки и строит DOM, который Aspose может отрисовать.  

> **Почему это важно:** Если HTML ссылается на CSS или изображения, Aspose получит их относительно пути к файлу. Использование абсолютного пути (`YOUR_DIRECTORY/input.html`) избавит от неожиданностей «file not found».

### Шаг 2 – Изменение размера страницы PDF: настройка параметров

Здесь мы создаём объект `PdfConversionOptions`.  
- `setPageSize(PageSize.A4)` указывает Aspose использовать стандартный размер A4 (210 × 297 mm).  
- `setPageOrientation(...)` меняет ориентацию страницы, если нужен альбомный вид.  
- `setMargins(new Margin(20, 20, 20, 20))` задаёт поле в 20 поинтов со всех сторон.

Вы можете заменить `PageSize.A4` на `PageSize.LETTER` или даже **пользовательский размер**, передав объект `SizeF`, например:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **Полезный совет:** Один поинт = 1/72 дюйма. Если вам удобнее работать в миллиметрах, умножьте значение на 2.83465, чтобы получить поинты.

### Шаг 3 – Генерация PDF из HTML: запуск конвертации

`Converter.convertHTML` делает всю тяжёлую работу. Он принимает загруженный `HTMLDocument`, путь к выходному файлу и только что настроенные параметры.  

Если нужно **задать размер страницы PDF** динамически в зависимости от содержимого, вы можете вычислить требуемые размеры перед этим шагом и скорректировать `pdfOptions` соответственно.

### Шаг 4 – Проверка результата

Строка `System.out.println` необязательна, но даёт быстрый отклик при запуске программы из консоли. После выполнения откройте `custom_page.pdf` — вы должны увидеть PDF формата A4 в портретной ориентации с равномерными полями в 20 поинтов, точно как мы указали.

## Конвертация HTML в PDF – Распространённые варианты

### Использование потока вместо пути к файлу

Иногда физического файла нет; HTML может приходить из базы данных или API. В этом случае оберните строку в `ByteArrayInputStream`:

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

Второй аргумент — базовый URL для разрешения относительных ресурсов.

### Смена ориентации страницы

Если ваш отчёт широкий, переключитесь на альбомный режим:

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### Точная настройка полей

Поля принимают значения с плавающей точкой, так что можно задать, например, 0.5 pt для тонкой границы:

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### Обработка больших HTML‑файлов

Для массивных документов рассмотрите включение **потоковой обработки с экономией памяти**:

```java
pdfOptions.setUseMemoryCache(true);
```

Это заставит Aspose записывать промежуточные данные во временные файлы вместо того, чтобы держать всё в ОЗУ.

## Установка размера страницы PDF – Пограничные случаи и подводные камни

- **Отсутствие шрифтов:** Если ваш HTML использует пользовательский шрифт, не установленный на сервере, PDF перейдёт к шрифту по умолчанию. Встроить шрифт можно с помощью `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);`.  
- **Масштабирование изображений:** Высококачественные изображения могут раздувать PDF. Используйте `pdfOptions.setImageResolution(150);`, чтобы уменьшить разрешение, сохранив приемлемое качество.  
- **Совместимость CSS:** Не все свойства CSS полностью поддерживаются. Оставайтесь на стандартных техниках верстки (flexbox работает, а grid может иметь нюансы).  
- **Разрешения путей:** Убедитесь, что процесс имеет права записи в `YOUR_DIRECTORY`. Иначе будет выброшено `IOException`.

## Ожидаемый результат

Запуск программы создаёт PDF, выглядящий примерно так (концептуальная иллюстрация):

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- Размер страницы: **A4** (210 × 297 mm).  
- Ориентация: **Портрет**.  
- Поля: **20 pt** со всех сторон.  

Откройте файл в любом PDF‑просмотрщике (Adobe Reader, Chrome и т.д.), чтобы убедиться.

## Итоги

Теперь вы знаете, как **создать PDF пользовательского размера** из HTML‑источника с помощью Aspose.HTML for Java. Руководство охватило весь конвейер: **конвертация HTML в PDF**, **изменение размера страницы PDF**, **установка размера страницы PDF** и **генерацию PDF из HTML** с пользовательскими полями.  

Экспериментируйте — меняйте `PageSize.LETTER` на юридический размер, подстраивайте поля или встраивайте свои шрифты. Далее можно изучить **добавление водяных знаков**, **шифрование PDF** или **пакетную обработку нескольких HTML‑файлов**. Все эти темы опираются на те же базовые концепции, которые мы только что разобрали.

Есть вопрос о конкретном пограничном случае? Оставьте комментарий ниже, и я помогу разобраться. Счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}