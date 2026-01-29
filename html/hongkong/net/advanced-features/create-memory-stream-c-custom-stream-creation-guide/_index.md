---
category: general
date: 2025-12-27
description: 快速使用一步一步指南建立 C# 記憶體串流。了解如何建立串流、處理資源，以及在 .NET 中實作自訂串流的建立。
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: zh-hant
og_description: 在秒內建立 C# 記憶體串流。本教學示範如何建立串流、處理資源，以及使用現代 .NET API 建構自訂串流。
og_title: 建立記憶體串流 C# – 完整自訂串流指南
tags:
- stream
- csharp
- .net
- resource-handling
title: 建立記憶體串流 C# – 自訂串流建立指南
url: /zh-hant/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 memory stream c# – 自訂串流建立指南

有沒有曾經需要 **create memory stream c#** 但不確定該選哪個 API？你並非唯一遇到這個問題的人。在許多舊有專案中會看到 `IOutputStorage`，而較新的程式碼庫則偏好使用 `ResourceHandler`。不論哪種方式，目標都相同：產生一個可供你的框架使用的 `Stream`。

在本教學中，你將學會 **how to create stream** 物件、**how to handle resources** 的安全處理方式，並精通針對 24.2 之前與 24.2 以上版本的函式庫的 **custom stream creation**。完成後，你將擁有一個可直接放入任何 .NET 解決方案的可執行範例——不需要神祕的參考，只要純粹的 C#。

## 你將學到的內容

- 清楚比較舊有的 `IOutputStorage` 模式與現代的 `ResourceHandler` 方法。  
- 完整、可直接複製貼上的程式碼，能編譯於 .NET 6+（或更早版本，視需求而定）。  
- 針對邊緣案例的技巧，例如釋放串流、處理大型負載，以及測試你的自訂串流。  

> **專業提示：** 若你的目標是 .NET 8，較新的 `ResourceHandler` 內建 async 支援，能在高吞吐量情境下節省毫秒級的時間。

## 建立 memory stream c# – 傳統做法（pre‑24.2）

當你被迫使用舊版函式庫時，需要符合的合約是 `IOutputStorage`。此介面僅要求提供一個方法，回傳給定資源名稱的 `Stream`。

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

### 為何這樣可行

- **介面合約** – 框架在需要寫入輸出時會呼叫 `CreateStream`。  
- **彈性** – 因為你回傳的是 `Stream`，之後可以將 `MemoryStream` 換成 `FileStream`，甚至自訂的緩衝串流，而不必修改其他程式碼。  
- **資源安全** – 呼叫端負責釋放回傳的串流，這也是我們在方法內不呼叫 `Dispose` 的原因。  

### 常見陷阱

| 問題 | 會發生什麼 | 解決方式 |
|------|------------|----------|
| 回傳已關閉的串流 | 使用者在寫入時會拋出 `ObjectDisposedException`。 | 確保在交付時串流是 **開啟** 的。 |
| 寫入後忘記將 `Position = 0` | 之後讀取時資料顯示為空。 | 若事先填入資料，返回前請呼叫 `stream.Seek(0, SeekOrigin.Begin)`。 |
| 對大型檔案使用巨大的 `MemoryStream` | 導致記憶體不足而當機。 | 改用暫存的 `FileStream` 或自訂緩衝串流。 |

## 建立 memory stream c# – 現代做法（24.2+）

自 24.2 版起，函式庫引入了 `ResourceHandler`。不再使用介面，而是繼承自基底類別並覆寫單一方法。這提供了更簡潔、支援 async 的入口點。

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

### 為何偏好 `ResourceHandler`

- **非同步支援** – `HandleResourceAsync` 方法讓你在不阻塞執行緒的情況下執行 I/O。  
- **內建錯誤處理** – 基底類別會捕捉例外並轉換為框架特定的錯誤代碼。  
- **未來保證** – 新版會加入掛鉤（例如日誌、遙測），僅能於 handler 模式使用。  

### 邊緣案例處理

1. **釋放** – 框架在使用完畢後會釋放串流，但若你包裝了其他可釋放物件（例如 `FileStream`），應在方法內使用 `using` 區塊，並回傳一個轉發 `Dispose` 的包裝器。  
2. **大型負載** – 若預期負載超過 100 MB，請將 `MemoryStream` 換成指向暫存檔的 `FileStream`。範例：  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```

3. **測試** – 若基底類別從 DI 取得服務，可透過注入 mock `IServiceProvider` 來單元測試你的 handler。確認 `HandleResource` 回傳的串流可寫入且可讀取。

## 如何建立串流 – 快速速查表

| 情境 | 推薦 API | 範例程式碼 |
|------|----------|------------|
| 簡單的記憶體資料 | `MemoryStream` | `new MemoryStream()` |
| 大型暫存檔 | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| 基於網路的來源 | `NetworkStream` | `new NetworkStream(socket)` |
| 自訂緩衝 | Derive from `Stream` | See [Microsoft docs] for custom stream implementation |

> **注意：** 若事先填入資料，返回前務必設定 `stream.Position = 0`；否則下游讀取者會認為串流是空的。

## 圖片說明

![顯示建立 memory stream c# 流程的圖示](https://example.com/images/create-memory-stream-diagram.png)

*替代文字：* 顯示建立 memory stream c# 流程的圖示

## 完整可執行範例

以下是一個最小的主控台應用程式，示範舊版與新版兩種做法。你可以直接複製貼上到新的 .NET 6 主控台專案並直接執行。

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

**預期輸出**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

程式展示了三種 **how to create stream** 的方式：舊的 `IOutputStorage`、新的同步 `HandleResource`，以及非同步的 `HandleResourceAsync`。三者皆回傳 `MemoryStream`，證明自訂串流建立在任何目標版本下皆可運作。

## 常見問題 (FAQ)

**Q: 我需要對取得的串流呼叫 `Dispose` 嗎？**  
A: 框架（或呼叫端程式碼）負責釋放。若你在回傳的串流內包裝了其他可釋放物件，請確保它會傳遞 `Dispose` 呼叫。

**Q: 我可以回傳唯讀串流嗎？**  
A: 可以，但合約通常預期可寫入的串流。若僅需讀取，請實作 `CanWrite => false` 並在文件中說明此限制。

**Q: 若我的資料大於可用記憶體該怎麼辦？**  
A: 改用以暫存檔為基礎的 `FileStream`，或實作會分段寫入磁碟的自訂緩衝串流。

**Q: 兩種做法在效能上有差異嗎？**  
A: 現代的 `ResourceHandler` 會因額外的基底類別邏輯產生少量開銷，但非同步版本在高併發情況下可顯著提升吞吐量。

## 結語

我們剛剛從各個可能遇到的角度說明了 **create memory stream c#**。現在你已了解如何使用舊版的 `IOutputStorage` 模式與新版的 `ResourceHandler` 類別來 **how to create stream**，同時也掌握了負責任地 **how to handle resources** 的實用技巧，並能以 **custom stream creation** 方式擴充至大型檔案或非同步情境。

Ready for

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}