---
category: general
date: 2025-12-27
description: 快速创建 C# 内存流的分步指南。学习如何创建流、处理资源以及在 .NET 中实现自定义流的创建。
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: zh
og_description: 在几秒钟内创建 C# 内存流。本教程展示了如何创建流、处理资源，以及使用现代 .NET API 构建自定义流。
og_title: 创建内存流 C# – 完整自定义流指南
tags:
- stream
- csharp
- .net
- resource-handling
title: 创建内存流 C# – 自定义流创建指南
url: /zh/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建内存流 c# – 自定义流创建指南

是否曾经需要**create memory stream c#**但不确定该选择哪个 API？你并不是唯一遇到这种情况的人。在许多旧项目中，你会看到 `IOutputStorage`，而较新的代码库更倾向于使用 `ResourceHandler`。无论哪种方式，目标都是相同的：生成一个你的框架可以使用的 `Stream`。

在本教程中，你将学习**how to create stream**对象，**how to handle resources**的安全处理，并掌握针对库的 pre‑24.2 和 24.2+ 版本的**custom stream creation**。完成后，你将拥有一个可直接放入任何 .NET 解决方案的可运行示例——无需神秘引用，纯粹的 C#。

## 你将收获的内容

- 对传统 `IOutputStorage` 模式与现代 `ResourceHandler` 方法进行清晰对比。  
- 完整的、可直接复制粘贴的代码，能够在 .NET 6+（或更早版本，如有需要）上编译。  
- 针对边缘情况的技巧，如释放流、处理大容量负载以及测试自定义流。  

> **专业提示：**如果你针对 .NET 8，更新的 `ResourceHandler` 提供内置的异步支持，可在高吞吐场景中节省毫秒级时间。

## 创建内存流 c# – 传统方法（pre‑24.2）

当你被迫使用库的旧版本时，需要满足的契约是 `IOutputStorage`。该接口仅要求提供一个方法，返回给定资源名称对应的 `Stream`。

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

### 为什么这样可行

- **接口契约** – 框架在需要写入输出时会调用 `CreateStream`。  
- **灵活性** – 因为返回的是 `Stream`，你可以在以后将 `MemoryStream` 替换为 `FileStream`，甚至自定义缓冲流，而无需修改其他代码。  
- **资源安全** – 调用方负责释放返回的流，这也是我们在方法内部不调用 `Dispose` 的原因。  

### 常见陷阱

| 问题 | 会发生什么 | 解决方案 |
|------|------------|----------|
| 返回已关闭的流 | 消费者在写入时会收到 `ObjectDisposedException`。 | 确保在交付时流是**打开**的。 |
| 写入后忘记设置 `Position = 0` | 随后读取时数据为空。 | 如果预先填充数据，在返回前调用 `stream.Seek(0, SeekOrigin.Begin)`。 |
| 对大文件使用巨大的 `MemoryStream` | 导致内存不足崩溃。 | 改用临时 `FileStream` 或自定义缓冲流。 |

## 创建内存流 c# – 现代方法（24.2+）

从 24.2 版本开始，库引入了 `ResourceHandler`。不再使用接口，而是继承自基类并重写单个方法。这为你提供了更简洁、支持异步的入口点。

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

### 为什么更倾向于 `ResourceHandler`

- **异步支持** – `HandleResourceAsync` 方法让你在不阻塞线程的情况下执行 I/O。  
- **内置错误处理** – 基类捕获异常并将其转换为框架特定的错误码。  
- **面向未来** – 新版本会添加仅在处理器模式下可用的钩子（例如日志、遥测）。  

### 边缘情况处理

1. **释放** – 框架在完成后会释放流，但如果你包装了其他可释放对象（如 `FileStream`），应在方法内部使用 `using` 块，并返回一个转发 `Dispose` 的包装器。  
2. **大负载** – 如果预计负载超过 100 MB，建议用指向临时文件的 `FileStream` 替代 `MemoryStream`。示例：  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```
3. **测试** – 如果基类从 DI 中获取服务，可通过注入模拟的 `IServiceProvider` 对处理器进行单元测试。验证 `HandleResource` 返回的流既可写入也可读取。  

## 如何创建流 – 快速速查表

| 场景 | 推荐 API | 示例代码 |
|------|----------|----------|
| 简单的内存数据 | `MemoryStream` | `new MemoryStream()` |
| 大型临时文件 | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| 基于网络的来源 | `NetworkStream` | `new NetworkStream(socket)` |
| 自定义缓冲 | Derive from `Stream` | 请参阅 [Microsoft docs] 了解自定义流实现 |

> **注意：**如果预先填充流，请在返回前始终设置 `stream.Position = 0`；否则下游读取器会认为流为空。

## 图片说明

![显示创建内存流 c# 过程的图示](https://example.com/images/create-memory-stream-diagram.png)

*Alt text:* 显示创建内存流 c# 过程的图示

## 完整可运行示例

下面是一个最小的控制台应用程序，演示传统和现代两种方法。你可以将其复制粘贴到新的 .NET 6 控制台项目中直接运行。

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

**预期输出**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

该程序展示了三种**how to create stream**方式：旧的 `IOutputStorage`、新的同步 `HandleResource`，以及异步的 `HandleResourceAsync`。这三者都返回 `MemoryStream`，证明自定义流创建在任何目标版本下都能工作。

## 常见问题 (FAQ)

**Q: 我需要对返回的流调用 `Dispose` 吗？**  
A: 框架（或你的调用代码）负责释放。如果在返回的流中包装了其他可释放对象，请确保它传播 `Dispose` 调用。

**Q: 我可以返回只读流吗？**  
A: 可以，但契约通常期望可写流。如果只需要读取，请实现 `CanWrite => false` 并在文档中说明限制。

**Q: 如果我的数据大于可用内存怎么办？**  
A: 改用基于临时文件的 `FileStream`，或实现将数据分块写入磁盘的自定义缓冲流。

**Q: 两种方法之间是否存在性能差异？**  
A: 现代的 `ResourceHandler` 因额外的基类逻辑会有轻微开销，但异步版本在高并发下可以显著提升吞吐量。

## 总结

我们已经从各个可能遇到的角度完整讲解了**create memory stream c#**。现在你了解了使用传统 `IOutputStorage` 模式和新版 `ResourceHandler` 类的**how to create stream**方法，并掌握了负责任地**how to handle resources**的实用技巧，以及针对大文件或异步场景的**custom stream creation**扩展方式。Ready for

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}