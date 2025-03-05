---
title: Конвертируйте EPUB в XPS в .NET с помощью Aspose.HTML
linktitle: Конвертировать EPUB в XPS в .NET
second_title: API манипуляции HTML Aspose.HTML .NET
description: Узнайте, как конвертировать EPUB в XPS в .NET с помощью Aspose.HTML для .NET. Следуйте нашему пошаговому руководству для легкой конвертации.
type: docs
weight: 13
url: /ru/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Вы ищете простой способ конвертировать файлы EPUB в формат XPS в ваших приложениях .NET? Aspose.HTML для .NET предоставляет мощное решение для достижения этой цели без усилий. В этом пошаговом руководстве мы проведем вас через процесс конвертации EPUB в XPS с помощью Aspose.HTML. Давайте начнем!

## Предпосылки

Прежде чем приступить к процессу конвертации EPUB в XPS, вам необходимо убедиться в наличии следующих предварительных условий:

### 1. Библиотека Aspose.HTML для .NET

 Убедитесь, что в вашем проекте установлена библиотека Aspose.HTML for .NET. Если вы этого еще не сделали, вы можете получить ее из[Страница загрузки Aspose.HTML для .NET](https://releases.aspose.com/html/net/).

### 2. Входной файл EPUB

Вам понадобится файл EPUB, который вы хотите преобразовать в XPS. Убедитесь, что у вас есть файл EPUB, доступный для преобразования.

### 3. Среда разработки .NET

В этом руководстве предполагается, что на вашем компьютере установлена рабочая среда разработки .NET.

## Импорт пространства имен

Для начала вам следует импортировать необходимое пространство имен для Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Конвертировать EPUB в XPS

Давайте разберем процесс преобразования файла EPUB в формат XPS на несколько этапов.

### Шаг 1.1: Откройте файл EPUB

Сначала откройте существующий файл EPUB для чтения с помощью FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Продолжить процесс конвертации
}
```

### Шаг 1.2: Создание XpsSaveOptions

Создайте экземпляр XpsSaveOptions. Этот шаг имеет решающее значение для настройки вывода XPS:

```csharp
var options = new XpsSaveOptions();
```

### Шаг 1.3: Конвертация EPUB в XPS

Теперь вызовем метод ConvertEPUB для преобразования EPUB в XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Укажите пользовательские параметры XPS

Вы можете дополнительно настроить вывод XPS, указав специальные параметры, такие как размер страницы и цвет фона.

### Шаг 2.1: Пользовательский размер страницы и цвет фона

Создайте экземпляр XpsSaveOptions с пользовательским размером страницы и цветом фона:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### Шаг 2.2: Конвертируйте EPUB в XPS с помощью пользовательских параметров

Теперь вызовите метод ConvertEPUB, чтобы преобразовать EPUB в XPS с пользовательскими параметрами:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Использовать пользовательский поставщик потоковой передачи

На этом этапе мы преобразуем EPUB в XPS с помощью пользовательского поставщика потоковой передачи, что позволит вам манипулировать полученными данными.

### Шаг 3.1: Создание MemoryStreamProvider

Создайте экземпляр MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Продолжить процесс конвертации
}
```

### Шаг 3.2: Конвертируйте EPUB в XPS с помощью Stream Provider

Конвертируйте EPUB в XPS с помощью MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Шаг 3.3: Доступ и сохранение результата

Извлеките поток памяти, содержащий преобразованные данные, и сохраните его в выходном файле:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Исходный код класса MemoryStreamProvider

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Список объектов MemoryStream, созданных во время рендеринга документа
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Этот метод вызывается, когда требуется только один выходной поток, например, для форматов XPS, PDF или TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Этот метод вызывается, когда требуется создание нескольких выходных потоков. Например, во время рендеринга HTML в список файлов изображений (JPG, PNG и т. д.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Здесь вы можете освободить поток, заполненный данными, и, например, сбросить его на жесткий диск.
            }
            public void Dispose()
            {
                // Освобождение ресурсов
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Поздравляем! Вы успешно преобразовали файл EPUB в формат XPS с помощью Aspose.HTML для .NET.

## Заключение

В этом всеобъемлющем руководстве мы изучили, как использовать Aspose.HTML для .NET для преобразования файлов EPUB в формат XPS с различными параметрами настройки. Независимо от того, являетесь ли вы опытным разработчиком или только начинаете, Aspose.HTML упрощает процесс, позволяя вам легко обрабатывать преобразования EPUB в XPS.

 Есть вопросы или возникли проблемы? Посмотрите[Документация Aspose.HTML](https://reference.aspose.com/html/net/) для получения дополнительной информации или обратитесь за помощью к[Форум сообщества Aspose.HTML](https://forum.aspose.com/).

## Часто задаваемые вопросы

### Что такое Aspose.HTML для .NET?
Aspose.HTML для .NET — мощная библиотека, которая позволяет разработчикам работать с документами HTML, EPUB и XPS в приложениях .NET.

### Где можно скачать Aspose.HTML для .NET?
 Вы можете загрузить Aspose.HTML для .NET с сайта[страница загрузки](https://releases.aspose.com/html/net/).

### Существует ли бесплатная пробная версия Aspose.HTML для .NET?
 Да, вы можете получить бесплатную пробную версию[здесь](https://releases.aspose.com/).

### Как получить временную лицензию на Aspose.HTML для .NET?
 Чтобы получить временную лицензию, посетите[временная страница лицензии](https://purchase.aspose.com/temporary-license/).

### Где я могу найти больше руководств и документации по Aspose.HTML для .NET?
 Изучите широкий спектр учебных пособий и подробную документацию по[Документация Aspose.HTML](https://reference.aspose.com/html/net/) страница.