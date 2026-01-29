---
category: general
date: 2025-12-27
description: สร้าง Memory Stream ใน C# อย่างรวดเร็วด้วยคู่มือขั้นตอนต่อขั้นตอน เรียนรู้วิธีสร้างสตรีม
  การจัดการทรัพยากร และการสร้างสตรีมแบบกำหนดเองใน .NET
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: th
og_description: สร้าง MemoryStream ด้วย C# ในไม่กี่วินาที บทเรียนนี้แสดงวิธีสร้างสตรีม,
  จัดการทรัพยากร, และสร้างสตรีมแบบกำหนดเองด้วย API .NET สมัยใหม่
og_title: สร้าง Memory Stream ใน C# – คู่มือการสร้าง Stream แบบกำหนดเองอย่างครบถ้วน
tags:
- stream
- csharp
- .net
- resource-handling
title: สร้าง Memory Stream C# – คู่มือการสร้างสตรีมแบบกำหนดเอง
url: /th/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง memory stream c# – คู่มือการสร้างสตรีมแบบกำหนดเอง

เคยต้องการ **create memory stream c#** แต่ไม่แน่ใจว่าจะเลือก API ไหนไหม? คุณไม่ได้เป็นคนเดียว ในหลายโครงการเก่า ๆ คุณจะพบ `IOutputStorage` ในขณะที่โค้ดใหม่ ๆ นิยมใช้ `ResourceHandler` ไม่ว่าอย่างไรก็ตาม เป้าหมายคือเดียวกัน: สร้าง `Stream` ที่เฟรมเวิร์กของคุณสามารถใช้ได้

ในบทแนะนำนี้ คุณจะได้เรียนรู้ **how to create stream** objects, **how to handle resources** อย่างปลอดภัย, และเชี่ยวชาญ **custom stream creation** สำหรับทั้งเวอร์ชันก่อน‑24.2 และ 24.2+ ของไลบรารี เมื่อจบคุณจะมีตัวอย่างที่ทำงานได้ซึ่งสามารถนำไปใส่ในโซลูชัน .NET ใดก็ได้—ไม่มีการอ้างอิงที่ซับซ้อน เพียงแค่ C# แท้ ๆ

## สิ่งที่คุณจะได้เรียนรู้

- การเปรียบเทียบที่ชัดเจนระหว่างรูปแบบ `IOutputStorage` แบบเก่า กับแนวทาง `ResourceHandler` แบบใหม่
- โค้ดที่สมบูรณ์พร้อมคัดลอก‑วางที่คอมไพล์ได้กับ .NET 6+ (หรือเวอร์ชันก่อนหน้า หากคุณต้องการ)
- เคล็ดลับสำหรับกรณีขอบเช่นการทำลายสตรีม, การจัดการข้อมูลขนาดใหญ่, และการทดสอบสตรีมแบบกำหนดเองของคุณ

> **เคล็ดลับพิเศษ:** หากคุณกำหนดเป้าหมายเป็น .NET 8, `ResourceHandler` รุ่นใหม่จะให้การสนับสนุน async ในตัว ซึ่งสามารถลดมิลลิวินาทีในสถานการณ์ที่ต้องการ throughput สูงได้

## สร้าง memory stream c# – วิธีแบบเก่า (pre‑24.2)

เมื่อคุณติดอยู่กับเวอร์ชันเก่าของไลบรารี สัญญาที่คุณต้องปฏิบัติตามคือ `IOutputStorage` อินเทอร์เฟซนี้ต้องการเพียงเมธอดที่คืนค่า `Stream` สำหรับชื่อทรัพยากรที่ระบุ

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

### ทำไมวิธีนี้ถึงได้ผล

- **สัญญาอินเทอร์เฟซ** – เฟรมเวิร์กจะเรียก `CreateStream` ทุกครั้งที่ต้องการเขียนผลลัพธ์  
- **ความยืดหยุ่น** – เนื่องจากคุณคืนค่า `Stream` คุณสามารถสลับ `MemoryStream` เป็น `FileStream` หรือแม้กระทั่งสตรีมบัฟเฟอร์แบบกำหนดเองในภายหลังโดยไม่ต้องแก้ไขโค้ดส่วนอื่น  
- **ความปลอดภัยของทรัพยากร** – ผู้เรียกเป็นผู้รับผิดชอบในการทำลายสตรีมที่คืนค่า ซึ่งเป็นเหตุผลที่เราไม่เรียก `Dispose` ภายในเมธอด  

### ข้อผิดพลาดทั่วไป

| ปัญหา | สิ่งที่เกิดขึ้น | วิธีแก้ |
|-------|----------------|--------|
| การคืนสตรีมที่ปิดแล้ว | ผู้ใช้จะได้รับ `ObjectDisposedException` เมื่อเขียน | ตรวจสอบให้แน่ใจว่าสตรีม **เปิด** อยู่เมื่อส่งต่อ |
| ลืมตั้งค่า `Position = 0` หลังการเขียน | ข้อมูลดูเหมือนว่างเปล่าเมื่ออ่านต่อไป | เรียก `stream.Seek(0, SeekOrigin.Begin)` ก่อนคืนค่า หากคุณได้เติมข้อมูลล่วงหน้า |
| ใช้ `MemoryStream` ขนาดใหญ่สำหรับไฟล์ใหญ่ | เกิดการล่มจากหน่วยความจำไม่พอ | เปลี่ยนเป็น `FileStream` ชั่วคราวหรือสตรีมบัฟเฟอร์แบบกำหนดเอง |

## สร้าง memory stream c# – วิธีสมัยใหม่ (24.2+)

ตั้งแต่เวอร์ชัน 24.2 ไลบรารีได้แนะนำ `ResourceHandler` แทนการใช้อินเทอร์เฟซ คุณจะสืบทอดจากคลาสฐานและเขียนทับเมธอดเดียว ซึ่งทำให้จุดเริ่มต้นสะอาดขึ้นและรองรับ async

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

### ทำไมควรเลือก `ResourceHandler`

- **รองรับ Async** – เมธอด `HandleResourceAsync` ให้คุณทำ I/O โดยไม่บล็อกเธรด  
- **จัดการข้อผิดพลาดในตัว** – คลาสฐานจะจับข้อยกเว้นและแปลงเป็นรหัสข้อผิดพลาดเฉพาะเฟรมเวิร์ก  
- **พร้อมอนาคต** – เวอร์ชันใหม่เพิ่ม hook (เช่น logging, telemetry) ที่ทำงานได้เฉพาะกับรูปแบบ handler  

### การจัดการกรณีขอบ

1. **การทำลาย** – เฟรมเวิร์กจะทำลายสตรีมหลังจากใช้งานเสร็จ แต่หากคุณห่อหุ้มวัตถุที่ทำลายได้อื่น (เช่น `FileStream`) ควรใช้บล็อก `using` ภายในเมธอดและคืน wrapper ที่ส่งต่อ `Dispose`  
2. **ข้อมูลขนาดใหญ่** – หากคาดว่าจะมี payload มากกว่า 100 MB ให้เปลี่ยนจาก `MemoryStream` เป็น `FileStream` ที่ชี้ไปยังไฟล์ชั่วคราว ตัวอย่าง:  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```
3. **การทดสอบ** – ทดสอบหน่วยของ handler โดยฉีด `IServiceProvider` จำลอง หากคลาสฐานดึงบริการจาก DI ตรวจสอบว่า `HandleResource` คืนสตรีมที่สามารถเขียนและอ่านได้  

## วิธีสร้างสตรีม – ชีตสรุปเร็ว

| สถานการณ์ | API ที่แนะนำ | ตัวอย่างโค้ด |
|-----------|--------------|--------------|
| ข้อมูลในหน่วยความจำแบบง่าย | `MemoryStream` | `new MemoryStream()` |
| ไฟล์ชั่วคราวขนาดใหญ่ | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| แหล่งข้อมูลแบบเครือข่าย | `NetworkStream` | `new NetworkStream(socket)` |
| การบัฟเฟอร์แบบกำหนดเอง | สืบทอดจาก `Stream` | ดู [Microsoft docs] สำหรับการทำ custom stream implementation |

> **หมายเหตุ:** ควรตั้งค่า `stream.Position = 0` ก่อนคืนค่า หากคุณเติมข้อมูลล่วงหน้า มิฉะนั้นผู้อ่านต่อไปจะคิดว่าสตรีมว่างเปล่า

## ภาพประกอบ

![แผนภาพแสดงกระบวนการสร้าง memory stream c#](https://example.com/images/create-memory-stream-diagram.png)

*ข้อความแทนภาพ:* แผนภาพแสดงกระบวนการสร้าง memory stream c#

## ตัวอย่างที่สามารถรันได้เต็มรูปแบบ

ด้านล่างเป็นแอปคอนโซลขนาดเล็กที่แสดงวิธีทั้งแบบเก่าและแบบใหม่ คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซล .NET 6 ใหม่และรันได้ทันที

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

**ผลลัพธ์ที่คาดหวัง**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

โปรแกรมนี้แสดงสามวิธีในการ **how to create stream**: `IOutputStorage` แบบเก่า, `HandleResource` แบบซิงโครนัสใหม่, และ `HandleResourceAsync` แบบอะซิงโครนัส ทั้งสามคืนค่า `MemoryStream` แสดงให้เห็นว่าการสร้างสตรีมแบบกำหนดเองทำงานได้ไม่ว่าคุณจะใช้เวอร์ชันใด

## คำถามที่พบบ่อย (FAQ)

**ถาม: ฉันต้องเรียก `Dispose` บนสตรีมที่ได้รับกลับมาหรือไม่?**  
**ตอบ:** เฟรมเวิร์ก (หรือโค้ดที่เรียก) เป็นผู้รับผิดชอบการทำลาย หากคุณห่อหุ้มวัตถุที่ทำลายได้อื่นภายในสตรีมที่คืนค่า ควรให้มันส่งต่อการเรียก `Dispose` ด้วย  

**ถาม: ฉันสามารถคืนสตรีมแบบอ่าน‑อย่างเดียวได้หรือไม่?**  
**ตอบ:** ได้ แต่สัญญามักคาดหวังสตรีมที่เขียนได้ หากคุณต้องการอ่านเท่านั้น ให้เขียน `CanWrite => false` และระบุข้อจำกัดในเอกสาร  

**ถาม: ถ้าข้อมูลของฉันใหญ่กว่าหน่วยความจำที่มี?**  
**ตอบ:** เปลี่ยนเป็น `FileStream` ที่อิงไฟล์ชั่วคราว หรือสร้างสตรีมบัฟเฟอร์แบบกำหนดเองที่เขียนลงดิสก์เป็นชิ้นส่วน  

**ถาม: มีความแตกต่างด้านประสิทธิภาพระหว่างสองวิธีหรือไม่?**  
**ตอบ:** `ResourceHandler` รุ่นใหม่เพิ่มภาระเล็กน้อยจากตรรกะของคลาสฐานเพิ่มเติม แต่เวอร์ชัน async สามารถเพิ่ม throughput อย่างมากในสภาวะความพร้อมใช้งานสูง  

## สรุป

เราได้ครอบคลุม **create memory stream c#** จากทุกมุมที่คุณอาจเจอในโลกจริง คุณตอนนี้รู้ **how to create stream** ด้วยทั้งรูปแบบ `IOutputStorage` แบบเก่าและคลาส `ResourceHandler` รุ่นใหม่ พร้อมกับเคล็ดลับการ **how to handle resources** อย่างรับผิดชอบและการขยายรูปแบบด้วย **custom stream creation** สำหรับไฟล์ขนาดใหญ่หรือสถานการณ์ async  

Ready for

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}