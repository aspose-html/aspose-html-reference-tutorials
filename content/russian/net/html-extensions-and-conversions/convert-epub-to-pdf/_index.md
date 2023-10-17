---
title: Конвертируйте EPUB в PDF в .NET с помощью Aspose.HTML
linktitle: Конвертируйте EPUB в PDF в .NET
second_title: Aspose.HTML .NET API манипулирования HTML
description: Узнайте, как конвертировать EPUB в PDF с помощью Aspose.HTML для .NET. В этом пошаговом руководстве описаны параметры настройки, часто задаваемые вопросы и многое другое для беспрепятственного преобразования документов.
type: docs
weight: 12
url: /ru/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

В этом уроке мы рассмотрим, как использовать Aspose.HTML для .NET для преобразования файлов EPUB в PDF. Aspose.HTML — это мощная библиотека .NET, предоставляющая различные функции для работы с документами HTML и EPUB. Мы рассмотрим предварительные условия, импортируем необходимые пространства имен и разберем несколько примеров, подробно объясняя каждый шаг.

## Предварительные условия

Прежде чем начать, убедитесь, что у вас есть следующие предварительные условия:

1.  Aspose.HTML for .NET: убедитесь, что в вашем проекте .NET установлен Aspose.HTML for .NET. Вы можете скачать его с[здесь](https://releases.aspose.com/html/net/).

2. Ваш каталог данных: вам понадобится каталог данных, в котором хранятся ваши файлы EPUB.

Теперь давайте углубимся в пошаговый процесс преобразования EPUB в PDF с помощью Aspose.HTML для .NET.

## Конвертировать EPUB в PDF

### Шаг 1. Инициализируйте свой проект

Убедитесь, что у вас настроен проект .NET и установлен Aspose.HTML for .NET.

### Шаг 2. Импортируйте необходимые пространства имен

В файл кода C# импортируйте необходимые пространства имен:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Шаг 3. Откройте файл EPUB.

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Перейдите к следующему шагу...
}
```

-  Заменять`"Your Data Directory"` с фактическим каталогом, в котором находится ваш файл EPUB.
- Этот код открывает файл EPUB для чтения.

### Шаг 4. Установите параметры PDF и выполните преобразование

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Создайте экземпляр`PdfSaveOptions` чтобы указать настройки преобразования PDF.
-  Использовать`Converter.ConvertEPUB`метод преобразования EPUB в PDF с заданными параметрами.
- Сохраните полученный PDF-файл как «output.pdf».

## Укажите параметры сохранения PDF

### Шаг 1. Инициализируйте свой проект

Убедитесь, что у вас настроен проект .NET и установлен Aspose.HTML for .NET.

### Шаг 2. Импортируйте необходимые пространства имен

Импортируйте необходимые пространства имен в свой код C#:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Шаг 3. Откройте файл EPUB.

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Перейдите к следующему шагу...
}
```

-  Заменять`"Your Data Directory"` с фактическим каталогом вашего файла EPUB.
- Откройте файл EPUB для чтения.

### Шаг 4. Настройте параметры PDF

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Создайте экземпляр`PdfSaveOptions` и настроить его в соответствии с вашими требованиями.
- В этом примере мы установили размер страницы 3000 пикселей в ширину и 1000 пикселей в высоту, а цвет фона — Alice Blue.

### Шаг 5. Выполните преобразование

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Использовать`Converter.ConvertEPUB` метод преобразования EPUB в PDF с настраиваемыми параметрами.
- Сохраните полученный PDF-файл как «output.pdf».

## Использовать поставщика пользовательского потока

### Шаг 1. Инициализируйте свой проект

Настройте проект .NET и установите Aspose.HTML для .NET.

### Шаг 2. Импортируйте необходимые пространства имен

В коде C# импортируйте необходимые пространства имен:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Шаг 3. Откройте файл EPUB.

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Перейдите к следующему шагу...
}
```

-  Заменять`"Your Data Directory"` с фактическим каталогом вашего файла EPUB.
- Откройте файл EPUB для чтения.

### Шаг 4. Используйте собственного поставщика потоков

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Перейдите к следующему шагу...
}
```

-  Создать`MemoryStreamProvider` для управления результатом преобразования как потоком памяти.
-  Использовать`Converter.ConvertEPUB` метод с пользовательским поставщиком потока.

### Шаг 5: сохраните результат

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Получите доступ к потоку памяти, содержащему преобразованные данные.
- Установите позицию потока в начало.
- Создайте выходной PDF-файл и скопируйте в него содержимое из потока памяти.

### Исходный код класса MemoryStreamProvider. 

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
                // Этот метод вызывается, когда требуется создание нескольких выходных потоков. Например, во время рендеринга HTML в список файлов изображений (JPG, PNG и т. д.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Здесь Вы можете освободить поток, наполненный данными, и, например, сбросить его на жесткий диск.
            }
            public void Dispose()
            {
                // Освобождение ресурсов
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Теперь вы узнали, как конвертировать файлы EPUB в PDF с помощью Aspose.HTML для .NET с различными параметрами и возможностями настройки. Aspose.HTML упрощает процесс, обеспечивая гибкость и контроль над преобразованием документов.

## Заключение

Aspose.HTML for .NET — это универсальный инструмент для преобразования файлов EPUB в PDF, предлагающий возможности настройки для адаптации полученного PDF-документа к вашим потребностям. Если вам нужны простые преобразования или расширенная настройка, Aspose.HTML поможет вам.

 Если вы еще этого не сделали, вы можете загрузить Aspose.HTML для .NET с сайта[Веб-сайт](https://releases.aspose.com/html/net/) и начните использовать его в своих .NET-приложениях уже сегодня.

---

## Часто задаваемые вопросы

### Можно ли использовать Aspose.HTML для .NET бесплатно?
    Aspose.HTML for .NET — коммерческий продукт, но доступна бесплатная пробная версия.[здесь](https://releases.aspose.com/).

### Могу ли я настроить внешний вид преобразованного PDF-файла?
   Да, вы можете настроить внешний вид PDF-файла, настроив такие параметры, как размер страницы и цвет фона, как показано в примере 2.

### Как я могу получить поддержку Aspose.HTML для .NET?
    Вы можете найти поддержку и ресурсы на[Форум Aspose.HTML](https://forum.aspose.com/).

### Существуют ли другие форматы, которые я могу конвертировать с помощью Aspose.HTML для .NET?
   Да, Aspose.HTML for .NET поддерживает различные форматы документов, включая HTML, EPUB и другие.

### Подходит ли Aspose.HTML для ..NET для крупномасштабного преобразования документов?
   Aspose.HTML for .NET предназначен для эффективной обработки крупномасштабных преобразований документов, что делает его пригодным для широкого спектра приложений.

