---
category: general
date: 2025-12-27
description: Tạo memory stream C# nhanh chóng với hướng dẫn từng bước. Tìm hiểu cách
  tạo stream, quản lý tài nguyên và triển khai tạo stream tùy chỉnh trong .NET.
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: vi
og_description: Tạo MemoryStream trong C# trong vài giây. Hướng dẫn này cho thấy cách
  tạo stream, quản lý tài nguyên và xây dựng việc tạo stream tùy chỉnh với các API
  .NET hiện đại.
og_title: Tạo memory stream C# – Hướng dẫn đầy đủ về Stream tùy chỉnh
tags:
- stream
- csharp
- .net
- resource-handling
title: Tạo memory stream C# – Hướng dẫn tạo stream tùy chỉnh
url: /vi/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo memory stream c# – Hướng dẫn tạo stream tùy chỉnh

Bạn đã bao giờ cần **create memory stream c#** nhưng không chắc nên chọn API nào? Bạn không phải là người duy nhất. Trong nhiều dự án legacy, bạn sẽ thấy `IOutputStorage`, trong khi các codebase mới hơn ưu tiên `ResourceHandler`. Dù sao, mục tiêu vẫn giống nhau: tạo ra một `Stream` mà framework của bạn có thể sử dụng.

Trong hướng dẫn này, bạn sẽ học **how to create stream** objects, **how to handle resources** một cách an toàn, và làm chủ **custom stream creation** cho cả các phiên bản trước‑24.2 và 24.2+ của thư viện. Kết thúc, bạn sẽ có một ví dụ hoạt động mà bạn có thể chèn vào bất kỳ giải pháp .NET nào—không có tham chiếu bí ẩn, chỉ C# thuần túy.

## Bạn sẽ nhận được gì

- So sánh rõ ràng giữa mẫu `IOutputStorage` legacy và cách tiếp cận `ResourceHandler` hiện đại.  
- Mã hoàn chỉnh, sẵn sàng copy‑paste, biên dịch trên .NET 6+ (hoặc phiên bản cũ hơn, nếu bạn cần).  
- Mẹo cho các trường hợp biên như việc giải phóng stream, xử lý payload lớn, và kiểm thử stream tùy chỉnh.  

> **Pro tip:** Nếu bạn đang nhắm tới .NET 8, `ResourceHandler` mới hơn cung cấp hỗ trợ async tích hợp, có thể giảm vài mili giây trong các kịch bản thông lượng cao.

## Tạo memory stream c# – Cách tiếp cận Legacy (pre‑24.2)

Khi bạn bị kẹt ở phiên bản cũ của thư viện, hợp đồng bạn phải đáp ứng là `IOutputStorage`. Giao diện chỉ yêu cầu một phương thức trả về `Stream` cho một tên tài nguyên nhất định.

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

### Tại sao cách này hoạt động

- **Interface contract** – Framework sẽ gọi `CreateStream` bất cứ khi nào cần ghi output.  
- **Flexibility** – Vì bạn trả về một `Stream`, bạn có thể thay `MemoryStream` bằng `FileStream` hoặc thậm chí một stream bộ đệm tùy chỉnh sau này mà không cần chạm vào phần còn lại của mã.  
- **Resource safety** – Người gọi chịu trách nhiệm giải phóng stream trả về, vì vậy chúng ta không gọi `Dispose` bên trong phương thức.  

### Những sai lầm thường gặp

| Issue | What happens | Fix |
|-------|--------------|-----|
| Trả về stream đã đóng | Người tiêu dùng sẽ nhận `ObjectDisposedException` khi ghi. | Đảm bảo stream **mở** khi bạn chuyển giao. |
| Quên đặt `Position = 0` sau khi ghi | Dữ liệu xuất hiện trống khi đọc sau. | Gọi `stream.Seek(0, SeekOrigin.Begin)` trước khi trả về nếu bạn đã điền trước. |
| Sử dụng `MemoryStream` lớn cho các tệp lớn | Sập do hết bộ nhớ. | Chuyển sang `FileStream` tạm thời hoặc một stream bộ đệm tùy chỉnh. |

## Tạo memory stream c# – Cách tiếp cận Modern (24.2+)

Bắt đầu từ phiên bản 24.2, thư viện đã giới thiệu `ResourceHandler`. Thay vì một giao diện, bạn bây giờ kế thừa từ một lớp cơ sở và ghi đè một phương thức duy nhất. Điều này cung cấp cho bạn một điểm vào sạch hơn, thân thiện với async.

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

### Tại sao nên ưu tiên `ResourceHandler`

- **Async support** – Phương thức `HandleResourceAsync` cho phép bạn thực hiện I/O mà không chặn các luồng.  
- **Built‑in error handling** – Lớp cơ sở bắt các ngoại lệ và chuyển chúng thành mã lỗi riêng của framework.  
- **Future‑proof** – Các phiên bản mới hơn thêm các hook (ví dụ: logging, telemetry) chỉ hoạt động với mẫu handler.  

### Xử lý các trường hợp biên

1. **Disposal** – Framework sẽ giải phóng stream sau khi hoàn thành, nhưng nếu bạn bọc một đối tượng disposable khác (như `FileStream`) bạn nên triển khai một khối `using` bên trong phương thức và trả về một wrapper chuyển tiếp `Dispose`.  
2. **Large payloads** – Nếu bạn dự đoán payload > 100 MB, thay `MemoryStream` bằng `FileStream` trỏ tới một tệp tạm. Ví dụ:  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```

3. **Testing** – Kiểm thử đơn vị handler của bạn bằng cách tiêm một mock `IServiceProvider` nếu lớp cơ sở lấy dịch vụ từ DI. Xác minh rằng `HandleResource` trả về một stream có thể ghi và đọc.

## Cách tạo stream – Bảng cheat sheet nhanh

| Scenario | Recommended API | Sample Code |
|----------|----------------|-------------|
| Dữ liệu trong bộ nhớ đơn giản | `MemoryStream` | `new MemoryStream()` |
| Tệp tạm thời lớn | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| Nguồn dựa trên mạng | `NetworkStream` | `new NetworkStream(socket)` |
| Bộ đệm tùy chỉnh | Derive from `Stream` | Xem [Microsoft docs] để biết cách triển khai stream tùy chỉnh |

> **Note:** Luôn đặt `stream.Position = 0` trước khi trả về nếu bạn đã điền trước stream; nếu không, các trình đọc phía dưới sẽ nghĩ stream là trống.

## Minh họa hình ảnh

![Diagram showing create memory stream c# process](https://example.com/images/create-memory-stream-diagram.png)

*Alt text:* sơ đồ mô tả quy trình tạo memory stream c#

## Ví dụ chạy đầy đủ

Dưới đây là một ứng dụng console tối thiểu minh họa cả hai cách tiếp cận legacy và modern. Bạn có thể copy‑paste nó vào một dự án console .NET 6 mới và chạy ngay.

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

**Kết quả mong đợi**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

Chương trình hiển thị ba cách để **how to create stream**: `IOutputStorage` cũ, `HandleResource` đồng bộ mới, và `HandleResourceAsync` bất đồng bộ. Cả ba đều trả về một `MemoryStream`, chứng minh rằng việc tạo stream tùy chỉnh hoạt động bất kể bạn nhắm tới phiên bản nào.

## Câu hỏi thường gặp (FAQ)

**Q: Tôi có cần gọi `Dispose` trên stream mà tôi nhận được không?**  
A: Framework (hoặc mã gọi của bạn) chịu trách nhiệm giải phóng. Nếu bạn bọc một đối tượng disposable khác bên trong stream trả về, hãy chắc chắn nó truyền gọi `Dispose`.

**Q: Tôi có thể trả về một stream chỉ đọc không?**  
A: Có, nhưng hợp đồng thường mong đợi một stream có thể ghi. Nếu bạn chỉ cần đọc, triển khai `CanWrite => false` và ghi chú giới hạn.

**Q: Nếu dữ liệu của tôi lớn hơn RAM có sẵn thì sao?**  
A: Chuyển sang `FileStream` dựa trên tệp tạm thời, hoặc triển khai một stream bộ đệm tùy chỉnh ghi vào đĩa theo từng khối.

**Q: Có sự khác biệt về hiệu năng giữa hai cách tiếp cận không?**  
A: `ResourceHandler` hiện đại thêm một chút overhead cho logic lớp cơ sở, nhưng phiên bản async có thể cải thiện đáng kể thông lượng trong môi trường đồng thời cao.

## Kết luận

Chúng tôi vừa đề cập đến **create memory stream c#** từ mọi góc độ bạn có thể gặp trong thực tế. Bây giờ bạn biết **how to create stream** bằng cả mẫu `IOutputStorage` legacy và lớp `ResourceHandler` mới hơn, cùng với các mẹo thực tế về **how to handle resources** một cách có trách nhiệm và mở rộng mẫu với **custom stream creation** cho các tệp lớn hoặc kịch bản async.

Sẵn sàng cho

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}