---
category: general
date: 2026-10-21
description: Узнайте, как сохранять HTML в виде ZIP с помощью Aspose.HTML, конвертировать
  HTML в ZIP и удалять ресурсы для получения чистого пакета.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save html as zip
- convert html to zip
- how to omit resources
- how to strip resources
- create html zip
language: ru
lastmod: 2026-10-21
og_description: Сохраняйте HTML в ZIP с Aspose.HTML, узнайте, как конвертировать HTML
  в ZIP и удалить ресурсы для лёгкого архива.
og_image_alt: Screenshot showing the save html as zip process with resources omitted
og_title: Сохранить HTML в ZIP с Aspose.HTML – исключить ресурсы за один шаг
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to save HTML as ZIP using Aspose.HTML, convert HTML to ZIP,
    and strip resources for a clean package.
  headline: How to save HTML as ZIP with Aspose.HTML and omit resources
  type: TechArticle
tags:
- Aspose.HTML
- C#
- ZIP archive
- HTML conversion
- Resource handling
title: Как сохранить HTML в виде ZIP с помощью Aspose.HTML и исключить ресурсы
url: /ru/net/html-extensions-and-conversions/how-to-save-html-as-zip-with-aspose-html-and-omit-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить HTML в ZIP с Aspose.HTML и исключить ресурсы

Если вам нужно **сохранить HTML в ZIP**, удаляя внешние файлы, это руководство показывает полное, готовое к запуску решение. К концу урока вы сможете **конвертировать HTML в ZIP**, управлять тем, какие ресурсы сохраняются, и создать чистый архив, содержащий только основную разметку.

Во многих сценариях веб‑автоматизации требуется упаковать страницу для офлайн‑использования, вложения в email или архивного хранения. Включение изображений, шрифтов или скриптов часто ненужно увеличивает размер архива. Ниже приведённые шаги объясняют **как исключать ресурсы** и **как удалять ресурсы** из вывода, чтобы полученный ZIP оставался лёгким.

## Требования

- .NET 6.0 или новее установлен  
- Лицензия Aspose.HTML for .NET (или бесплатная оценочная версия)  
- Базовая среда разработки C# (Visual Studio, VS Code или Rider)  

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Html`.

## Шаг 1: Создать пользовательский обработчик ресурсов

Суть **как исключать ресурсы** заключается в подклассе `ResourceHandler`. Aspose.HTML вызывает этот обработчик для каждого внешнего ресурса (изображения, CSS, скрипты). Возвращая пустой поток, вы фактически говорите конвертеру пропустить ресурс.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Prevents external resources from being written to the output package.
/// </summary>
class CustomResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning an empty MemoryStream strips the resource from the ZIP.
        return new MemoryStream();
    }
}
```

**Почему это важно:** Поведение по умолчанию копирует каждый связанный файл в ZIP, что может удвоить или утроить размер файла. Переопределяя `HandleResource`, вы получаете тонкий контроль без изменения исходного HTML.

## Шаг 2: Загрузить HTML‑документ

Загрузите исходный файл с помощью `HTMLDocument`. Конструктор принимает путь к файлу, URL или поток. В этом примере мы читаем локальный файл с именем `input.html`.

```csharp
// Load the source HTML file from the local file system.
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

Если ваш HTML находится в памяти или приходит из веб‑запроса, вы можете передать вместо этого `MemoryStream` или строку URL. API работает так же.

## Шаг 3: Настроить параметры сохранения

Создайте экземпляр `HtmlSaveOptions` и назначьте пользовательский обработчик, созданный на Шаге 1. Это указывает Aspose.HTML использовать обработчик каждый раз, когда он встречает ресурс.

```csharp
// Prepare save options and attach the custom resource handler.
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // The ResourceHandler property is what enables resource stripping.
    ResourceHandler = new CustomResourceHandler()
};
```

Вы также можете настроить другие параметры, например `CompressImages = false`, если хотите сохранить данные изображений, но всё равно исключать другие ресурсы. В примере сохраняются настройки сжатия по умолчанию.

## Шаг 4: Сохранить документ в виде ZIP‑архива

Наконец, вызовите `Save`, указав путь назначения и настроенные параметры. Выходной файл будет `.zip`, содержащий `index.html` (или оригинальное имя файла) и **без внешних ресурсов**.

```csharp
// Save the HTML document as a ZIP file. The archive will contain only the HTML markup.
document.Save("YOUR_DIRECTORY/output.zip", saveOptions);
```

### Ожидаемый результат

- `output.zip` → содержит один файл `index.html`.  
- Все изображения, CSS‑файлы и ссылки на JavaScript исключены, потому что пользовательский обработчик возвращал пустой поток для каждого.  

Вы можете проверить архив, открыв его в любом ZIP‑просмотрщике. HTML‑страница всё ещё будет ссылаться на оригинальные URL, но эти файлы отсутствуют в архиве, что сохраняет пакет минимальным.

## Полный, готовый к запуску пример

Ниже приведена полная программа, которую вы можете скопировать, вставить и запустить. Замените `YOUR_DIRECTORY` реальным путём к папке на вашем компьютере.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

class Program
{
    static void Main()
    {
        // Step 1: Define a custom resource handler to control how external resources are saved.
        class CustomResourceHandler : ResourceHandler
        {
            public override Stream HandleResource(ResourceInfo info)
            {
                // Returning an empty stream strips the resource from the ZIP output.
                return new MemoryStream();
            }
        }

        // Step 2: Load an HTML document from a file.
        string inputPath = "YOUR_DIRECTORY/input.html";
        HTMLDocument document = new HTMLDocument(inputPath);

        // Step 3: Create HTML save options and assign the custom handler.
        HtmlSaveOptions saveOptions = new HtmlSaveOptions
        {
            ResourceHandler = new CustomResourceHandler()
        };

        // Step 4: Save the document as a ZIP archive containing the HTML and (now omitted) resources.
        string outputPath = "YOUR_DIRECTORY/output.zip";
        document.Save(outputPath, saveOptions);

        Console.WriteLine($"HTML has been saved as ZIP at: {outputPath}");
    }
}
```

Запуск этой программы создаёт ZIP‑файл, описанный выше. Теперь вы можете распространять HTML‑страницу без включения ненужных ресурсов.

## Общие варианты и граничные случаи

| Сценарий | Корректировка |
|----------|---------------|
| **Сохранить изображения, но удалить CSS/JS** | В `CustomResourceHandler` проверьте `info.MimeType`. Возвращайте `MemoryStream` только для `text/css` и `application/javascript`. |
| **Сохранить внешние шрифты** | Возвращайте оригинальный поток для MIME‑типа `font/woff2`, иначе возвращайте пустой поток. |
| **Создать ZIP с пользовательским именем записи** | Используйте перегрузку `HtmlSaveOptions` `Save(string path, SaveOptions options, string entryName)`, чтобы указать другое имя корневого файла. |
| **Конвертировать несколько HTML‑файлов в один ZIP** | Пройдитесь по каждому файлу в цикле, создайте отдельный `HTMLDocument` и вручную добавьте каждый в один `ZipArchive` с помощью `System.IO.Compression`. |

Эти варианты демонстрируют **как избирательно удалять ресурсы**, предоставляя вам полный контроль над окончательным размером архива.

## Профессиональные советы

- **Проверьте результат**: После сохранения откройте ZIP и загрузите `index.html` в браузере. Отсутствующие ресурсы отобразятся как битые ссылки, подтверждая работу обработчика.  
- **Производительность**: Возврат пустого `MemoryStream` дешёв, но если у вас тысячи ресурсов, рассмотрите кэширование решения (например, `HashSet<string>` MIME‑типов для пропуска).  
- **Лицензирование**: Бесплатная оценочная версия Aspose.HTML добавляет комментарий‑водяной знак в HTML. Разверните лицензированную версию, чтобы удалить его для продакшн‑использования.  

## Заключение

Теперь вы знаете, как **сохранить HTML в ZIP**, **конвертировать HTML в ZIP** и **удалять ресурсы** с помощью Aspose.HTML для .NET. Реализовав пользовательский `ResourceHandler`, вы можете исключать нежелательные файлы и сохранять архив лёгким. Экспериментируйте с логикой обработчика, чтобы оставлять только действительно нужные ресурсы, и интегрируйте этот подход в более крупные автоматизационные конвейеры.

---

**Следующие шаги**

- Исследуйте другие возможности `HtmlSaveOptions`, такие как `EmbedImages`, для встраивания изображений непосредственно в HTML.  
- Скомбинируйте этот подход с `Aspose.PDF`, чтобы после создания ZIP конвертировать тот же HTML в PDF.  
- Рассмотрите серверные сценарии, где вы генерируете ZIP по запросу и передаёте его клиенту в потоковом режиме без записи на диск.  

Удачной разработки!

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как использовать ZipArchive – Сохранить HTML и ресурсы в ZIP‑файл](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [Как сохранить HTML в C# – Пользовательские обработчики ресурсов и ZIP](/html/english/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/)
- [Как сохранить HTML в ZIP в C# – Полное руководство по Aspose.HTML](/html/english/net/html-extensions-and-conversions/how-to-save-html-as-zip-in-c-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}