---
date: 2026-03-29
description: Узнайте, как использовать Aspose.HTML для Java, чтобы указать параметры
  сохранения XPS, конвертировать EPUB в XPS и управлять лицензированием.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Как использовать параметры сохранения Aspose HTML для EPUB в XPS
url: /ru/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать параметры сохранения Aspose HTML для EPUB в XPS

В этом руководстве мы покажем, **как использовать Aspose** HTML Save Options для конвертации документа EPUB в XPS с полным контролем над размерами страниц, цветом фона и вопросами лицензирования. Независимо от того, создаёте ли вы конвейер пакетной обработки или одноразовый инструмент конвертации, эти шаги помогут вам быстро получить надёжные результаты.

## Быстрые ответы
- **Что делает Aspose HTML Save Options?** Он позволяет настраивать размер страницы, цвет фона и другие параметры рендеринга при сохранении в такие форматы, как XPS.  
- **Какая библиотека требуется?** Aspose.HTML for Java (последняя версия).  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для оценки; коммерческая лицензия требуется для продакшна.  
- **Можно ли изменить размеры страницы?** Да — вы можете задать любую ширину и высоту через `PageSetup`.  
- **Быстра ли конверсия?** Для типичных файлов EPUB конверсия завершается за секунды на современном JVM.

## Что означает «how to use aspose» в данном контексте?
Фраза **как использовать Aspose** относится к практическим шагам по использованию библиотеки Aspose.HTML для манипуляции и конвертации веб‑документов. В этом руководстве мы сосредотачиваемся на **aspose html save options**, которые позволяют точно настроить вывод при **конвертации EPUB в XPS**.

## Зачем использовать Aspose.HTML для Java для конвертации EPUB в XPS?
- **Высокая точность** — сохраняет сложные макеты, шрифты и векторную графику.  
- **Программный контроль** — автоматизировать пакетные конвертации внутри Java‑приложений.  
- **Отсутствие внешних зависимостей** — чистая Java‑библиотека, без нативных компонентов.  
- **Настраиваемый вывод** — благодаря параметрам сохранения вы можете адаптировать XPS под свои точные требования, например **указать размеры страницы** или задать пользовательский фон.  

## Требования
Прежде чем погрузиться в код, убедитесь, что у вас есть следующее:

1. **Среда разработки Java** — установлен JDK 8 или новее.  
2. **Библиотека Aspose.HTML for Java** — скачайте её по [download link](https://releases.aspose.com/html/java/).  
3. **Файл EPUB** — исходный EPUB, который вы хотите **конвертировать EPUB в XPS**.  

Наличие этих элементов позволит вам следовать шагам без прерываний.

## Импорт пакетов
First, import the required classes. Place the imports at the top of your Java source file:

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

Эти импорты дают вам доступ к движку конвертации и **Aspose HTML Save Options**, необходимым для точной настройки.

## Открытие файла EPUB
Next, open the EPUB you want to convert. The `Resources.input` helper loads a file from the demo resources folder:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Использование блока try‑with‑resources гарантирует автоматическое закрытие потока.

## Создание XPS Save Options (Настройка размера страницы и фона)
Now we create an `XpsSaveOptions` instance and customize it. This is where the **save options** really shine:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Размер страницы** — установлен в 3000 × 1000 пикселей в этом примере; настройте под нужный размер бумаги или используйте `Length.fromInches`, чтобы **указать размеры страницы** в дюймах.  
- **Цвет фона** — `AliceBlue` демонстрирует, как изменить фон холста; вы можете выбрать любой `Color`.  

Эти настройки являются частью **aspose html save options**, влияющих на конечный документ XPS.

## Конвертация EPUB в XPS
Finally, invoke the converter with the stream, the configured options, and an output path:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Когда эта строка выполнится, Aspose.HTML прочитает EPUB, применит заданные параметры страницы и цвет фона, и запишет полностью совместимый файл XPS.

## Распространённые проблемы и советы
- **Неправильные размеры страницы** — убедитесь, что размеры указаны в пикселях (или используйте `Length.fromInches`).  
- **Отсутствие шрифтов** — внедрите необходимые шрифты в EPUB или установите их на хосте JVM, чтобы избежать подстановки.  
- **Большие файлы** — для очень больших EPUB увеличьте размер кучи JVM (`-Xmx`), чтобы предотвратить `OutOfMemoryError`.  
- **Лицензирование Aspose HTML** — убедитесь, что перед конвертацией загружена действующая лицензия; иначе появится водяной знак пробной версии.

## Заключение
Используя **Aspose HTML Save Options**, вы получаете точный контроль над тем, как EPUB преобразуется в XPS. Приведённые выше шаги показывают, как **конвертировать EPUB**, задать **размеры страницы**, изменить фон и выполнить конверсию всего несколькими строками кода Java. Интегрируйте этот шаблон в ваши конвейеры пакетной обработки для эффективной автоматизации задач публикации.

## Часто задаваемые вопросы

**Q: Что такое Aspose.HTML for Java?**  
A: Это Java‑библиотека, позволяющая разработчикам создавать, редактировать, рендерить и конвертировать HTML, EPUB и другие веб‑документы без необходимости браузера.

**Q: Можно ли использовать её в коммерческом проекте?**  
A: Да. Для продакшн‑использования требуется действующая лицензия. Приобрести её можно на [purchase page](https://purchase.aspose.com/buy).

**Q: Доступна ли бесплатная пробная версия?**  
A: Конечно. Скачайте пробную версию [здесь](https://releases.aspose.com/).

**Q: Где я могу получить поддержку?**  
A: Сообщества и официальная поддержка доступны через форумы Aspose по адресу [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: Каковы системные требования?**  
A: Java Development Kit (JDK) 8+ и операционная система, поддерживаемая средой выполнения Aspose. Убедитесь, что ваша среда соответствует перечисленным выше требованиям.

---

**Последнее обновление:** 2026-03-29  
**Тестировано с:** Aspose.HTML for Java 24.12  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}