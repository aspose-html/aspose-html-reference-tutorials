---
category: general
date: 2026-08-15
description: Создайте пользовательский обработчик ресурсов на C# для управления HTML‑ресурсами,
  такими как изображения и CSS. Изучите HTMLLoadOptions, потоки памяти и загрузку
  HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: ru
lastmod: 2026-08-15
og_description: Создайте пользовательский обработчик ресурсов на C# для контроля того,
  как передаются HTML‑ресурсы. В этом руководстве показана настройка HTMLLoadOptions,
  работа с потоками памяти и загрузка HTMLDocument с пользовательской логикой.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Создайте пользовательский обработчик ресурсов в C# – полное руководство
  по управлению HTML‑ресурсами
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Создать пользовательский обработчик ресурсов на C# для загрузки HTML
url: /ru/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание пользовательского обработчика ресурсов в C# для загрузки HTML

Если вам нужно **создать пользовательский обработчик ресурсов** для HTML‑файлов, это руководство покажет, как это сделать. Вы научитесь перехватывать изображения, CSS и другие активы при загрузке HTML‑документа, используя `HTMLLoadOptions` и поток, основанный на памяти.

В руководстве рассматривается всё, что требуется для реализации переиспользуемого обработчика, настройки параметров загрузки и проверки корректного захвата ресурсов. Никакой внешней документации не требуется — только код ниже и пояснения.

## Предварительные требования

- .NET 6.0 или новее
- Базовые знания C#
- Ссылка на библиотеку обработки HTML, предоставляющую `HTMLDocument`, `HtmlLoadOptions` и `ResourceHandler` (например, GroupDocs.Viewer for .NET)

## Обзор решения

Мы будем:

1. **Создавать пользовательский обработчик ресурсов**, наследуясь от `ResourceHandler`.
2. Настраивать `HTMLLoadOptions` для использования этого обработчика.
3. Загружать HTML‑файл с помощью `HTMLDocument`, при этом обработчик будет предоставлять поток для каждого ресурса.
4. (Опционально) Сохранять полученные ресурсы на диск для проверки.

Каждый шаг включает полный исходный код и объяснение логики.

## Шаг 1: Определите класс пользовательского обработчика ресурсов

Создание собственного обработчика подразумевает переопределение `HandleResource`, чтобы библиотека могла записывать байты ресурса в поток, которым вы управляете. Использование `MemoryStream` сохраняет данные в памяти, что удобно для тестирования или дальнейшей обработки.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Почему это важно:**  
Переопределяя `HandleResource`, вы получаете полный контроль над тем, куда направляются данные ресурса. Если позже понадобится кэшировать изображения, трансформировать CSS или вести журнал использования ресурсов, вы можете заменить `MemoryStream` любой другой реализацией потока.

## Шаг 2: Настройте `HTMLLoadOptions` для использования обработчика

`HTMLLoadOptions` позволяет подключить обработчик к конвейеру загрузки. Установка свойства `ResourceHandler` указывает просмотрщику вызывать `MyHandler` для каждого внешнего актива.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Почему это важно:**  
Без назначения `ResourceHandler` просмотрщик записывал бы ресурсы в место по умолчанию (обычно во временную папку). Указав собственный обработчик, вы **создаёте пользовательский обработчик ресурсов**, который соответствует стратегии хранения вашего приложения.

## Шаг 3: Загрузите HTML‑документ с настроенными параметрами

Теперь загрузите HTML‑файл. Просмотрщик вызовет `MyHandler.HandleResource` для каждого найденного ресурса.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

На этом этапе HTML‑контент разобран, а все внешние ресурсы переданы в буферы памяти, предоставленные `MyHandler`.

## Шаг 4 (опционально): Доступ к захваченным ресурсам

Если необходимо проанализировать или сохранить ресурсы, вы можете изменить `MyHandler`, чтобы сохранять каждый `MemoryStream` в словарь, ключом которого будет имя ресурса.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

После загрузки можно пройтись по `handler.Resources` и записать каждый элемент на диск:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Почему это важно:**  
Сохранение ресурсов позволяет выполнять постобработку, такую как оптимизация изображений, минификация CSS или архивирование. Это также даёт наглядную проверку того, что логика **создания пользовательского обработчика ресурсов** работает корректно.

## Шаг 5: Очистка

И `HTMLDocument`, и любые потоки следует освобождать, чтобы освободить неуправляемые ресурсы.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Полный рабочий пример

Ниже представлена автономная программа, демонстрирующая все шаги от определения класса до извлечения ресурсов.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Ожидаемый вывод**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

Консоль выводит каждый ресурс, который просмотрщик передал вашему пользовательскому обработчику, подтверждая успешное выполнение рабочего процесса **создания пользовательского обработчика ресурсов**.

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| *Что делать, если ресурс большой (например, изображение высокого разрешения)?* | Замените `MemoryStream` на `FileStream`, указывающий на временную папку. Это предотвратит чрезмерное потребление памяти. |
| *Можно ли фильтровать ресурсы по типу?* | Внутри `HandleResource` проверяйте `info.MimeType` или `info.Extension` и возвращайте `null` для нежелательных типов. Возврат `null` сообщает просмотрщику пропустить ресурс. |
| *Нужна ли потокобезопасность?* | Если один экземпляр обработчика используется в нескольких одновременных загрузках, защитите словарь `Resources` блокировкой или используйте конкурентную коллекцию. |
| *Как поддерживать относительные URL?* | `ResourceInfo` содержит оригинальный URL; вы можете объединить его с базовым путём HTML‑файла для разрешения относительных ссылок перед сохранением. |

## Заключение

Теперь вы знаете, как **создать пользовательский обработчик ресурсов** в C# для загрузки HTML, настроить `HTMLLoadOptions`, захватывать передаваемые активы и корректно освобождать ресурсы. Этот шаблон даёт полный контроль над управлением ресурсами, позволяя реализовывать такие сценарии, как обработка изображений «на лету», пере‑запись CSS или безопасное хранение.

Далее изучайте связанные темы, такие как **загрузка HTMLDocument** с различными параметрами рендеринга, или расширяйте обработчик до **C# resource handler** реализаций, записывающих данные напрямую в облачное хранилище. Экспериментируйте с методом `HandleResource` вашего обработчика, чтобы он соответствовал специфическому рабочему процессу вашего проекта.

## Что изучать дальше?

Следующие руководства охватывают близкие темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}