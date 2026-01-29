---
category: general
date: 2025-12-27
description: Быстро создайте MemoryStream в C# с пошаговым руководством. Узнайте,
  как создавать поток, управлять ресурсами и реализовывать пользовательское создание
  потоков в .NET.
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: ru
og_description: Создайте MemoryStream в C# за секунды. Этот учебник показывает, как
  создать поток, управлять ресурсами и создавать пользовательские потоки с помощью
  современных API .NET.
og_title: Создание MemoryStream в C# — Полное руководство по пользовательским потокам
tags:
- stream
- csharp
- .net
- resource-handling
title: Создание MemoryStream в C# – Руководство по созданию пользовательского потока
url: /ru/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание memory stream c# – Руководство по пользовательскому созданию потоков

Когда‑нибудь вам нужно было **создать memory stream c#**, но вы не знали, какой API выбрать? Вы не одиноки. Во многих устаревших проектах вы найдете `IOutputStorage`, в то время как более новые кодовые базы предпочитают `ResourceHandler`. В любом случае цель одна: получить `Stream`, который может использовать ваш фреймворк.

В этом руководстве вы узнаете **как создавать объекты stream**, **как безопасно работать с ресурсами** и освоите **пользовательское создание потоков** как для версий до 24.2, так и для 24.2+. К концу вы получите рабочий пример, который можно вставить в любое решение .NET — без загадочных зависимостей, только чистый C#.

## Что вы получите

- Чёткое сравнение устаревшего шаблона `IOutputStorage` и современного подхода `ResourceHandler`.  
- Полный готовый к копированию код, компилируемый под .NET 6+ (или более ранние версии, если нужно).  
- Советы по крайним случаям, таким как освобождение потоков, работа с большими нагрузками и тестирование вашего пользовательского потока.  

> **Pro tip:** Если вы нацелены на .NET 8, новый `ResourceHandler` предоставляет встроенную поддержку async, что может сэкономить миллисекунды в сценариях с высоким пропускным способностью.

## Создание memory stream c# – Устаревший подход (pre‑24.2)

Когда вы застряли на более старой версии библиотеки, контракт, который нужно выполнить, — `IOutputStorage`. Интерфейс требует лишь метод, возвращающий `Stream` для заданного имени ресурса.

```csharp
using System;
using System.IO;

// Step 1: Implement the old IOutputStorage contract.
public class MyStorage : IOutputStorage
{
    /// <summary>
    /// Returns a stream for the requested resource name.
    /// In a real app you might open a file, a network socket,
    /// or generate data on the fly.
    /// </summary>
    /// <param name="name">Logical name of the resource.</param>
    /// <returns>A writable Stream instance.</returns>
    public Stream CreateStream(string name)
    {
        // Custom stream creation logic.
        // Here we simply return an in‑memory stream.
        // You could also wrap a FileStream if you prefer.
        return new MemoryStream();
    }
}
```

### Почему это работает

- **Interface contract** – Фреймворк вызовет `CreateStream`, когда понадобится записать вывод.  
- **Flexibility** – Поскольку вы возвращаете `Stream`, позже можно заменить `MemoryStream` на `FileStream` или даже на пользовательский буферизованный поток, не меняя остального кода.  
- **Resource safety** – Вызывающая сторона отвечает за освобождение возвращённого потока, поэтому мы не вызываем `Dispose` внутри метода.

### Распространённые подводные камни

| Issue | What happens | Fix |
|-------|--------------|-----|
| Returning a closed stream | Consumers will get `ObjectDisposedException` on write. | Ensure the stream is **open** when you hand it off. |
| Forgetting to set `Position = 0` after writing | Data appears empty when read later. | Call `stream.Seek(0, SeekOrigin.Begin)` before returning if you pre‑populate it. |
| Using a huge `MemoryStream` for large files | Out‑of‑memory crashes. | Switch to a temporary `FileStream` or a custom buffered stream. |

## Создание memory stream c# – Современный подход (24.2+)

Начиная с версии 24.2 библиотека представила `ResourceHandler`. Вместо интерфейса теперь наследуете базовый класс и переопределяете один метод. Это даёт более чистую, async‑дружелюбную точку входа.

```csharp
using System;
using System.IO;

// Step 2: Inherit from the new ResourceHandler base class.
public class MyHandler : ResourceHandler
{
    /// <summary>
    /// Called by the framework to obtain a stream for a resource.
    /// </summary>
    /// <param name="name">The logical name of the resource.</param>
    /// <returns>A writable Stream instance.</returns>
    public override Stream HandleResource(string name)
    {
        // Your custom stream creation logic goes here.
        // For demonstration we use a MemoryStream.
        return new MemoryStream();
    }

    // Optional async version (available in 24.2+)
    public override async Task<Stream> HandleResourceAsync(string name, CancellationToken ct = default)
    {
        // Simulate async work, e.g., fetching data from a service.
        await Task.Delay(10, ct);
        return new MemoryStream();
    }
}
```

### Почему стоит предпочесть `ResourceHandler`

- **Async support** – Метод `HandleResourceAsync` позволяет выполнять I/O без блокировки потоков.  
- **Built‑in error handling** – Базовый класс перехватывает исключения и преобразует их в коды ошибок, специфичные для фреймворка.  
- **Future‑proof** – В новых релизах добавляются хуки (например, логирование, телеметрия), которые работают только с шаблоном обработчика.

### Обработка крайних случаев

1. **Disposal** – Фреймворк освобождает поток после завершения работы, но если вы оборачиваете другой disposable (например, `FileStream`), следует использовать `using` внутри метода и вернуть обёртку, которая переадресует `Dispose`.  
2. **Large payloads** – Если ожидаются нагрузки > 100 MB, замените `MemoryStream` на `FileStream`, указывающий на временный файл. Пример:  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```

3. **Testing** – Юнит‑тестируйте обработчик, внедряя мок `IServiceProvider`, если базовый класс получает сервисы из DI. Убедитесь, что `HandleResource` возвращает поток, в который можно писать и из которого можно читать.

## Как создать поток – Быстрая шпаргалка

| Scenario | Recommended API | Sample Code |
|----------|----------------|-------------|
| Simple in‑memory data | `MemoryStream` | `new MemoryStream()` |
| Large temporary files | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| Network‑based source | `NetworkStream` | `new NetworkStream(socket)` |
| Custom buffering | Derive from `Stream` | See [Документация Microsoft] for custom stream implementation |

> **Note:** Always set `stream.Position = 0` before returning if you pre‑populate the stream; otherwise downstream readers will think the stream is empty.

## Иллюстрация

![Диаграмма, показывающая процесс создания memory stream c# process](https://example.com/images/create-memory-stream-diagram.png)

*Alt text:* диаграмма, показывающая процесс создания memory stream c# process

## Полный исполняемый пример

Ниже представлен минимальный консольный приложение, демонстрирующее как устаревший, так и современный подходы. Вы можете скопировать‑вставить его в новый проект консоли .NET 6 и запустить без изменений.

```csharp
using System;
using System.IO;
using System.Threading;
using System.Threading.Tasks;

// -------------------------------------------------
// Legacy implementation (pre‑24.2)
// -------------------------------------------------
public class MyStorage : IOutputStorage
{
    public Stream CreateStream(string name) => new MemoryStream();
}

// -------------------------------------------------
// Modern implementation (24.2+)
// -------------------------------------------------
public class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string name) => new MemoryStream();

    public override async Task<Stream> HandleResourceAsync(string name, CancellationToken ct = default)
    {
        await Task.Delay(10, ct); // simulate async work
        return new MemoryStream();
    }
}

// -------------------------------------------------
// Demo program
// -------------------------------------------------
class Program
{
    static async Task Main()
    {
        // Legacy usage
        IOutputStorage legacy = new MyStorage();
        using (var legacyStream = legacy.CreateStream("legacy"))
        using (var writer = new StreamWriter(legacyStream))
        {
            writer.Write("Hello from legacy API!");
            writer.Flush();
            legacyStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(new StreamReader(legacyStream).ReadToEnd());
        }

        // Modern sync usage
        var handler = new MyHandler();
        using (var modernStream = handler.HandleResource("modern"))
        using (var writer = new StreamWriter(modernStream))
        {
            writer.Write("Hello from modern API!");
            writer.Flush();
            modernStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(new StreamReader(modernStream).ReadToEnd());
        }

        // Modern async usage
        using (var asyncStream = await handler.HandleResourceAsync("async"))
        using (var writer = new StreamWriter(asyncStream))
        {
            await writer.WriteAsync("Hello from async API!");
            await writer.FlushAsync();
            asyncStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(await new StreamReader(asyncStream).ReadToEndAsync());
        }
    }
}
```

**Ожидаемый вывод**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

Программа показывает три способа **как создавать поток**: старый `IOutputStorage`, новый синхронный `HandleResource` и асинхронный `HandleResourceAsync`. Все три возвращают `MemoryStream`, подтверждая, что пользовательское создание потоков работает независимо от целевой версии.

## Часто задаваемые вопросы (FAQ)

**Q: Нужно ли вызывать `Dispose` у потока, который я получаю?**  
A: Фреймворк (или ваш вызывающий код) отвечает за освобождение. Если вы оборачиваете внутри возвращаемого потока другой disposable, убедитесь, что он передаёт вызов `Dispose`.

**Q: Можно ли вернуть поток только для чтения?**  
A: Да, но контракт обычно ожидает поток с возможностью записи. Если нужен только чтение, реализуйте `CanWrite => false` и задокументируйте ограничение.

**Q: Что делать, если мои данные больше доступной ОЗУ?**  
A: Перейдите на `FileStream`, основанный на временном файле, или реализуйте пользовательский буферизованный поток, который пишет на диск кусками.

**Q: Есть ли различия в производительности между двумя подходами?**  
A: Современный `ResourceHandler` добавляет небольшие накладные расходы из‑за дополнительной логики базового класса, но async‑версия может значительно повысить пропускную способность при высокой конкуренции.

## Итоги

Мы только что рассмотрели **create memory stream c#** со всех сторон, с которыми вы можете столкнуться в реальных проектах. Теперь вы знаете **как создавать поток** с использованием как устаревшего шаблона `IOutputStorage`, так и нового класса `ResourceHandler`, а также получили практические советы по **как работать с ресурсами** ответственно и расширять шаблон с помощью **пользовательского создания потоков** для больших файлов или async‑сценариев.

Ready for

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}