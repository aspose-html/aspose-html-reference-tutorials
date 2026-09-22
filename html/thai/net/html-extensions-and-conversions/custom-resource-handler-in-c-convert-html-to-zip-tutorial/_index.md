---
category: general
date: 2026-02-10
description: ตัวจัดการทรัพยากรแบบกำหนดเองช่วยให้คุณแปลง HTML เป็น ZIP ด้วย C# เรียนรู้วิธีบันทึก
  HTML เป็น ZIP และสตรีมทรัพยากร HTML อย่างมีประสิทธิภาพ
draft: false
keywords:
- custom resource handler
- convert html to zip
- save html as zip
- create zip with html
- stream html resources
language: th
og_description: ตัวจัดการทรัพยากรแบบกำหนดเองช่วยให้คุณแปลง HTML เป็น ZIP ใน C# ทำตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อบันทึก
  HTML เป็น zip และสตรีมทรัพยากร HTML
og_title: ตัวจัดการทรัพยากรแบบกำหนดเองใน C# – แปลง HTML เป็น ZIP
tags:
- Aspose.HTML
- C#
- ZIP archive
- file streaming
title: การจัดการทรัพยากรแบบกำหนดเองใน C# – สอนแปลง HTML เป็น ZIP
url: /th/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/
---

all shortcodes unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตัวจัดการทรัพยากรแบบกำหนดเอง – แปลง HTML เป็น ZIP ใน C#

เคยสงสัยไหมว่า **custom resource handler** จะทำให้คุณแปลง HTML ดิบให้เป็นไฟล์ ZIP ได้อย่างไร? คุณไม่ได้เป็นคนเดียวที่เจออุปสรรค นักพัฒนาจำนวนมากเจอปัญหาเมื่อจำเป็นต้องบรรจุหน้า HTML พร้อมกับทรัพยากรของมันโดยไม่ทิ้งไฟล์ชั่วคราวบนดิสก์ ข่าวดีคือ? ด้วย Aspose.HTML คุณสามารถทำทั้งหมดในหน่วยความจำได้ และเคล็ดลับอยู่ที่ตัวจัดการทรัพยากรแบบกำหนดเอง

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งจะแสดงให้คุณเห็นวิธี **convert HTML to ZIP**, **save HTML as ZIP**, และ **stream HTML resources** แบบเรียลไทม์ เมื่อจบคุณจะมีเมธอดเดียวที่รับสตริง HTML แล้วสร้างไฟล์ `result.zip` พร้อมดาวน์โหลดที่มีหน้าเว็บและทรัพยากรที่เชื่อมโยงทั้งหมด

> **Prerequisites** – .NET 6+ (หรือ .NET Framework 4.6+), Aspose.HTML สำหรับ .NET ติดตั้งแล้ว, และมีความเข้าใจพื้นฐานเกี่ยวกับ streams. ไม่ต้องใช้เครื่องมือภายนอก

---

## ตัวจัดการทรัพยากรแบบกำหนดเอง – แนวคิดหลัก

*resource handler* ใน Aspose.HTML คืออ็อบเจกต์ที่ตัดสินใจ **ว่า** ส่วนต่าง ๆ ของเอกสารจะถูกบันทึกไปที่ไหน—ไม่ว่าจะเป็นไฟล์บนดิสก์, บัฟเฟอร์ในหน่วยความจำ, หรืออย่างที่เราจะแสดง, รายการภายในไฟล์ ZIP โดยการสืบทอด `ResourceHandler` คุณจะได้การควบคุมเต็มรูปแบบต่อปลายทางของไฟล์ HTML หลัก **และ** ทุกทรัพยากรเสริม (CSS, รูปภาพ, ฟอนต์ ฯลฯ)

คิดว่ามันเป็นเจ้าหน้าที่จราจรสำหรับทรัพยากรของเอกสารของคุณ: เมธอด `HandleResource` จะให้ `Stream` สำหรับ HTML หลัก, ส่วนเหตุการณ์ `ResourceSaving` จะให้คุณดักจับไฟล์ที่พึ่งพาแต่ละไฟล์ก่อนที่มันจะถูกเขียน

## ขั้นตอนที่ 1: สร้างตัวจัดการทรัพยากรแบบกำหนดเอง

แรกเริ่มสร้างคลาสที่สืบทอดจาก `ResourceHandler` เราจะโอเวอร์ไรด์ `HandleResource` เพื่อให้ Aspose ได้รับ `MemoryStream` ใหม่สำหรับผลลัพธ์ HTML หลัก สำหรับทรัพยากรที่เชื่อมโยงเราจะเชื่อมต่อกับ `ResourceSaving` ต่อไป

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System.IO;

/// <summary>
/// Supplies a stream for every resource the HTML document needs to save.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a new stream for the main HTML content.
    /// </summary>
    public override Stream HandleResource(ResourceInfo info)
    {
        // In real life you might return a FileStream or a ZipEntry stream.
        // Here we just hand back a clean MemoryStream.
        return new MemoryStream();
    }
}
```

**Why this matters:** การคืนค่า `MemoryStream` ใหม่หมายความว่า HTML จะไม่สัมผัสกับระบบไฟล์ นี่คือพื้นฐานสำหรับการสร้าง ZIP ในหน่วยความจำที่สะอาดต่อไป

## ขั้นตอนที่ 2: บันทึก HTML ลงใน MemoryStream เดียว

ตอนนี้เรามีตัวจัดการแล้ว เราสามารถสร้างเอกสาร HTML และเก็บไว้ทั้งหมดในหน่วยความจำ ขั้นตอนนี้เป็นออปชันหากคุณต้องการเพียง ZIP เท่านั้น แต่ช่วยแสดงให้เห็นว่าตัวจัดการทำงานอย่างไรในแบบแยกส่วน

```csharp
using Aspose.Html;

// Sample HTML – replace with your own markup or load from a file.
string htmlContent = "<html><head><title>Demo</title></head><body>Hello world!</body></html>";

// Create the document from a string.
HTMLDocument htmlDocument = new HTMLDocument(htmlContent);

// Instantiate our custom handler.
MyHandler memoryHandler = new MyHandler();

using (MemoryStream htmlStream = new MemoryStream())
{
    // Save triggers HandleResource and writes the HTML into htmlStream.
    htmlDocument.Save(htmlStream, memoryHandler);

    // Reset position for potential reading.
    htmlStream.Position = 0;

    // For demo purposes, dump the HTML to console.
    using (StreamReader reader = new StreamReader(htmlStream))
    {
        Console.WriteLine("Generated HTML:");
        Console.WriteLine(reader.ReadToEnd());
    }
}
```

**Expected output** (formatted for readability):

```
Generated HTML:
<html><head><title>Demo</title></head><body>Hello world!</body></html>
```

หากคุณรันสคริปต์นี้คุณจะเห็นว่า HTML อยู่เฉพาะใน RAM—ไม่มีไฟล์ชั่วคราวใด ๆ ถูกสร้าง

## ขั้นตอนที่ 3: แพ็ค HTML และทรัพยากรลงในไฟล์ ZIP

ตอนนี้มาถึงส่วนที่น่าสนใจ: การบรรจุ HTML **และ** ทุกทรัพยากรที่อ้างอิงลงในไฟล์ ZIP โดยไม่ต้องเขียนไฟล์กลางลงดิสก์ เราจะใช้ `System.IO.Compression.ZipArchive` ร่วมกับเหตุการณ์ `ResourceSaving`

```csharp
using Aspose.Html;
using System.IO;
using System.IO.Compression;

// Re‑use the same HTMLDocument from the previous step.
HTMLDocument htmlDocument = new HTMLDocument("<html><body>Hello world!</body></html>");

// Path where the final ZIP will be written.
string zipPath = Path.Combine(Environment.CurrentDirectory, "result.zip");

// Open a FileStream for the ZIP file.
using (FileStream zipFile = new FileStream(zipPath, FileMode.Create))
using (ZipArchive zipArchive = new ZipArchive(zipFile, ZipArchiveMode.Update))
{
    // Create a fresh handler for the ZIP operation.
    MyHandler zipHandler = new MyHandler();

    // Hook the ResourceSaving event – this fires for every resource.
    zipHandler.ResourceSaving += (sender, e) =>
    {
        // Ensure we don't create leading folder entries like "/css/style.css".
        string entryName = e.ResourceInfo.Path.TrimStart('/');

        // Create a new entry inside the ZIP.
        ZipArchiveEntry entry = zipArchive.CreateEntry(entryName);

        // Provide the stream that Aspose will write into.
        e.Stream = entry.Open();
    };

    // Save the document; the handler will fill the ZIP for us.
    htmlDocument.Save(zipHandler);
}

// Verify the ZIP exists.
Console.WriteLine($"ZIP created at: {zipPath}");
```

### สิ่งที่เกิดขึ้นภายใน

1. **`ResourceSaving` fires** สำหรับไฟล์ HTML หลักและแต่ละทรัพยากรที่เชื่อมโยง
2. Lambda ของเราสร้างรายการที่สอดคล้อง (`CreateEntry`) ภายใน ZIP ที่เปิดอยู่
3. โดยการกำหนด `e.Stream = entry.Open()` เราให้ Aspose เขียนโดยตรงลงในรายการ ZIP
4. เมื่อ `htmlDocument.Save` เสร็จสิ้น ZIP จะมีหน้า HTML ที่สมบูรณ์พร้อม CSS, รูปภาพ หรือฟอนต์ที่อ้างอิงใน markup

**Result:** ไฟล์ `result.zip` เดียวที่คุณสามารถให้บริการแก่เบราว์เซอร์, แนบในอีเมล, หรือเก็บใน blob storage—ไม่มีไฟล์ชั่วคราวเหลืออยู่

## โบนัส: การใช้ ZIP ใน Web API

หากคุณกำลังสร้าง endpoint ของ ASP.NET Core ที่ส่งคืน ZIP ตามคำขอเดียวกันก็ใช้ตรรกะเดียวกัน นี่คือตัวอย่าง action ของคอนโทรลเลอร์แบบกระชับ

```csharp
[ApiController]
[Route("api/[controller]")]
public class HtmlZipController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult DownloadZip()
    {
        // Build the document (could be loaded from a DB, etc.).
        var html = "<html><body><h1>Dynamic report</h1></body></html>";
        var doc = new HTMLDocument(html);
        var handler = new MyHandler();

        // Prepare an in‑memory ZIP.
        using var zipStream = new MemoryStream();
        using (var archive = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            handler.ResourceSaving += (s, e) =>
            {
                var entry = archive.CreateEntry(e.ResourceInfo.Path.TrimStart('/'));
                e.Stream = entry.Open();
            };
            doc.Save(handler);
        }

        zipStream.Position = 0;
        return File(zipStream, "application/zip", "report.zip");
    }
}
```

ตอนนี้การร้องขอ GET ไปที่ `/api/HtmlZip/download` จะสตรีม ZIP ที่สร้างขึ้นโดยตรงไปยังไคลเอนต์—เหมาะสำหรับรายงานแบบเรียลไทม์

## ข้อผิดพลาดทั่วไป & เคล็ดลับระดับมืออาชีพ

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Empty folders in the ZIP** | `ResourceInfo.Path` starts with `/` causing an entry like `/` | Use `TrimStart('/')` as shown in the event handler. |
| **Missing images** | Images referenced with absolute URLs aren’t fetched automatically | Set `htmlDocument.Options.ResourceLoading = ResourceLoadingMode.Stream` and supply a custom `ResourceHandler` that downloads remote assets. |
| **Large files cause memory pressure** | All streams are kept in memory until the ZIP is closed | Switch `ZipArchiveMode.Update` to `Create` and write each entry directly without buffering, or stream from disk if size exceeds RAM. |
| **Exception “The stream does not support seeking”** | Trying to reuse a non‑seekable stream for multiple resources | Always provide a fresh `MemoryStream` or `entry.Open()` for each resource. |

## สรุป

เราได้แสดงให้เห็นว่า **custom resource handler** ทำให้คุณ **convert HTML to ZIP**, **save HTML as ZIP**, และ **stream HTML resources** ได้โดยไม่ต้องสัมผัสระบบไฟล์ โดยการโอเวอร์ไรด์ `HandleResource` และใช้เหตุการณ์ `ResourceSaving` คุณจะได้การควบคุมระดับไบต์ที่ออกจาก Aspose.HTML อย่างละเอียด

รูปแบบนี้สามารถขยายได้: เปลี่ยน `MemoryStream` ในหน่วยความจำเป็นสตรีมของคลาวด์บล็อบ, เพิ่มการตั้งค่าการบีบอัด, หรือเชื่อมต่อเลเยอร์การบันทึกเพื่อ audit ว่าอุปกรณ์ใดบ้างที่ถูกบรรจุ ไม่จำกัดอะไรเลยเมื่อคุณเป็นเจ้าของ pipeline ของทรัพยากร

พร้อมก้าวต่อไปหรือยัง? ลองฝัง CSS และรูปภาพใน HTML ของคุณ, ทดลองโหลดทรัพยากรระยะไกล, หรือผสานกระบวนการนี้เข้าใน Azure Function ที่คืนค่า ZIP ตามคำขอ. Happy coding!

--- 

![การทำงานของตัวจัดการทรัพยากรแบบกำหนดเอง](https://example.com/placeholder-image.png "การทำงานของตัวจัดการทรัพยากรแบบกำหนดเอง")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}