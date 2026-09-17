---
category: general
date: 2026-02-13
description: Сделайте текст полужирным курсивом программно с помощью C#. Научитесь
  использовать GetElementsByTagName, задавать стиль шрифта, загружать HTML‑документ
  и получать первый элемент абзаца.
draft: false
keywords:
- make text bold italic
- use getelementsbytagname
- set font style programmatically
- load html document c#
- get first paragraph element
language: ru
og_description: Сделайте текст полужирным курсивом в C# мгновенно. Этот учебник показывает,
  как использовать GetElementsByTagName, программно установить стиль шрифта, загрузить
  HTML‑документ и получить первый элемент абзаца.
og_title: Сделать текст полужирным и курсивным в C# – быстрое стилирование в коде
tags:
- C#
- Aspose.Html
- HTML manipulation
title: Сделайте текст полужирным и курсивом в C# – Краткое руководство по стилизации
  HTML
url: /ru/net/html-document-manipulation/make-text-bold-italic-in-c-quick-guide-to-styling-html/
---

"Make Text Bold Italic in C# – Quick Guide to Styling HTML" etc.

Let's produce final content.

Be careful with "Aspose.HTML", "HTML", "C#", keep as is.

Translate sentences naturally.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Сделать текст полужирным курсивом в C# – Быстрое руководство по стилизации HTML

Когда‑нибудь нужно **сделать текст полужирным курсивом** в HTML‑файле из приложения на C#? Вы не одиноки; это частый запрос при генерации отчетов, писем или динамических веб‑фрагментов. Хорошая новость? Это можно выполнить всего в несколько строк с помощью Aspose.HTML.

В этом руководстве мы пройдем процесс загрузки HTML‑документа, поиска первого элемента `<p>` с помощью `GetElementsByTagName`, а затем **программно зададим стиль шрифта**, чтобы текст стал одновременно полужирным и курсивным. К концу вы получите полностью готовый, исполняемый фрагмент кода и уверенное понимание используемого API.

## Что понадобится

- **Aspose.HTML for .NET** (любая актуальная версия; используемый API работает с .NET 6+)
- Базовая среда разработки C# (Visual Studio, Rider или VS Code)
- HTML‑файл с именем `sample.html`, размещенный в папке, к которой у вас есть доступ  
  (будем ссылаться на него как `YOUR_DIRECTORY/sample.html`)

Дополнительные пакеты NuGet не требуются, кроме Aspose.HTML, а код работает на Windows, Linux и macOS.

---

## Шаг 1: Загрузка HTML‑документа в C#

Первое, что нужно сделать — загрузить HTML‑файл в память. Класс `HtmlDocument` из Aspose.HTML выполняет всю тяжелую работу.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;

// Replace YOUR_DIRECTORY with the actual path where sample.html lives
string htmlPath = Path.Combine("YOUR_DIRECTORY", "sample.html");

// Load the HTML document from the file system
HtmlDocument htmlDoc = new HtmlDocument(htmlPath);
```

**Почему это важно:**  
Загрузка документа предоставляет вам объектную модель, похожую на DOM, которую можно запрашивать и изменять. Это фундамент для любой последующей работы со стилями.

> **Pro tip:** Если файл может отсутствовать, оберните загрузку в `try/catch` и корректно обработайте `FileNotFoundException`.

---

## Шаг 2: Поиск первого элемента `<p>` с помощью `GetElementsByTagName`

Чтобы изменить стиль конкретного абзаца, нам нужна ссылка на этот узел. `GetElementsByTagName` возвращает «живую» коллекцию; получение первого элемента простое.

```csharp
// Get all <p> elements and pick the first one
var paragraphs = htmlDoc.GetElementsByTagName("p");

// Safety check – ensure at least one <p> exists
if (paragraphs.Length == 0)
{
    Console.WriteLine("No <p> elements found in the document.");
    return;
}

// This is the element we will style
var firstParagraph = paragraphs[0];
```

**Почему использовать `GetElementsByTagName`?**  
Это знакомый, стандартный метод DOM, который работает независимо от сложности документа. Можно также использовать CSS‑селекторы, но `GetElementsByTagName` предельно ясен для задачи «получить первый элемент абзаца».

---

## Шаг 3: Применение комбинированного стиля полужирный и курсив с `WebFontStyle`

Aspose.HTML предоставляет перечисление `WebFontStyle`, позволяющее комбинировать стили побитовым ИЛИ. Чтобы сделать текст **полужирным курсивом**, объединяем два флага.

```csharp
// Apply both Bold and Italic styles at once
firstParagraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

Под капотом это задает CSS‑свойства `font-weight: bold; font-style: italic;`. Перечисление делает код типобезопасным и избавляет от опечаток в строковых значениях.

---

## Шаг 4: Сохранение изменённого документа (по желанию)

Если необходимо сохранить изменения, просто вызовите `Save`. Вы можете вывести результат в другой HTML‑файл или даже в PDF, в зависимости от последующих требований.

```csharp
// Save the updated HTML to a new file
string outputPath = Path.Combine("YOUR_DIRECTORY", "sample_modified.html");
htmlDoc.Save(outputPath);

Console.WriteLine($"Document saved to {outputPath}");
```

**Ожидаемый результат:**  
Откройте `sample_modified.html` в любом браузере, и первый абзац будет отображаться **полужирным курсивом**. Всё остальное останется без изменений.

---

## Полный рабочий пример

Объединив всё вместе, получаем полную программу, которую можно скопировать в консольное приложение:

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the HTML document
        string htmlPath = Path.Combine("YOUR_DIRECTORY", "sample.html");
        HtmlDocument htmlDoc = new HtmlDocument(htmlPath);

        // 2️⃣ Locate the first <p> element
        var paragraphs = htmlDoc.GetElementsByTagName("p");
        if (paragraphs.Length == 0)
        {
            Console.WriteLine("No <p> elements found.");
            return;
        }
        var firstParagraph = paragraphs[0];

        // 3️⃣ Make text bold italic
        firstParagraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // 4️⃣ Save the result (optional)
        string outputPath = Path.Combine("YOUR_DIRECTORY", "sample_modified.html");
        htmlDoc.Save(outputPath);

        Console.WriteLine($"Successfully made text bold italic and saved to {outputPath}");
    }
}
```

**Ожидаемый вывод в консоли:**

```
Successfully made text bold italic and saved to YOUR_DIRECTORY\sample_modified.html
```

Откройте сохранённый файл и убедитесь, что первый абзац выглядит так:

> *This is the first paragraph – it should be **bold italic**.*

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если в HTML нет тегов `<p>`?
Проверка безопасности в Шаге 2 уже выводит дружеское сообщение и завершает работу. В продакшене можно создать новый элемент `<p>` вместо прерывания.

### Можно ли стилизовать сразу несколько абзацев?
Конечно. Пройдитесь в цикле по `paragraphs` и примените тот же `FontStyle`:

```csharp
foreach (var p in paragraphs)
{
    p.Style.FontWeight = FontWeight.Bold;
    p.Style.FontStyle = FontStyle.Italic;
}
```

### Как добавить другие стили, например, подчёркивание?
`WebFontStyle` охватывает только толщину и наклон. Для подчёркивания задайте CSS‑свойство `text-decoration`:

```csharp
firstParagraph.Style.TextDecoration = TextDecoration.Underline;
```

### Работает ли это с HTML5‑тегами, такими как `<section>`?
`GetElementsByTagName` работает с любым именем тега, поэтому можно так же легко обращаться к `<section>`, `<div>` или пользовательским тегам.

### Отразится ли изменение в браузерах, не поддерживающих CSS?
Поскольку API записывает стандартные CSS‑свойства, любой современный браузер корректно отобразит полужирный курсив. Старые браузеры, игнорирующие `font-weight` или `font-style`, крайне редки и обычно не учитываются в проектах .NET.

---

## Полезные советы и распространённые подводные камни

- **Не забудьте импортировать пространства имён.** Отсутствие `using Aspose.Html.Drawing;` приводит к ошибке компиляции для `WebFontStyle`.
- **Работа с путями:** используйте `Path.Combine`, чтобы избежать жёстко заданных разделителей; это делает код кроссплатформенным.
- **Производительность:** для огромных документов используйте `GetElementsByTagName` экономно. Если нужен только первый абзац, можно выйти из цикла после его нахождения.
- **Формат сохранения:** если позже понадобится PDF, замените `htmlDoc.Save(outputPath);` на `htmlDoc.Save(outputPath, SaveFormat.Pdf);` (требуется дополнение PDF).

---

## Заключение

Теперь вы знаете, как **сделать текст полужирным курсивом** в HTML‑файле с помощью C#. Загрузив документ, используя `GetElementsByTagName` для **получения первого элемента абзаца** и **задания стиля шрифта программно**, вы получаете тонкий контроль над любым HTML‑контентом.  

Дальше вы можете экспериментировать с другими вариантами стилизации, обрабатывать несколько узлов или даже конвертировать стилизованный HTML в PDF для отчётности. Один и тот же шаблон — загрузить, найти, стилизовать, сохранить — подходит практически для любой задачи манипуляции DOM в Aspose.HTML.

Есть дополнительные вопросы по работе с HTML в C#? Исследуйте связанные темы, такие как *load html document c#*, *use GetElementsByTagName* или *set font style programmatically* для более глубокого погружения. Приятного кодинга!

---

![make text bold italic example](image.png "Screenshot showing a paragraph rendered bold and italic after applying the style")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}