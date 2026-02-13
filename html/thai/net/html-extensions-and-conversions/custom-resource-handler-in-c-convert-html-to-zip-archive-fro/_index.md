---
category: general
date: 2026-02-13
description: เรียนรู้วิธีสร้างตัวจัดการทรัพยากรแบบกำหนดเองใน C# เพื่อแปลง HTML เป็นไฟล์
  ZIP โดยสร้างไฟล์ ZIP จากหน่วยความจำด้วย Aspose.HTML – คู่มือทีละขั้นตอน
draft: false
keywords:
- custom resource handler
- convert html zip archive
- create zip from memory
- Aspose HTML
- in‑memory streaming
- C# zip compression
language: th
og_description: ค้นพบโซลูชัน C# ครบชุดสำหรับการใช้ตัวจัดการทรัพยากรแบบกำหนดเองเพื่อแปลง
  HTML เป็นไฟล์ ZIP โดยตรงในหน่วยความจำ
og_title: ตัวจัดการทรัพยากรแบบกำหนดเอง – แปลง HTML เป็น ZIP จากหน่วยความจำ
tags:
- C#
- Aspose.HTML
- ZipArchive
- MemoryStream
title: ตัวจัดการทรัพยากรแบบกำหนดเองใน C# – แปลง HTML เป็นไฟล์ ZIP จากหน่วยความจำ
url: /th/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-archive-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตัวจัดการทรัพยากรแบบกำหนดเอง – แปลง HTML เป็นไฟล์ ZIP จากหน่วยความจำ

เคยต้องการ **custom resource handler** เพื่อดึงรูปภาพ, ไฟล์ CSS หรือสคริปต์ทั้งหมดที่หน้า HTML เรียกใช้, แล้วบีบอัดทั้งหมดโดยไม่ต้องเขียนลงดิสก์หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายสถานการณ์ของการทำเว็บ‑อัตโนมัติหรือการเทมเพลตอีเมล คุณต้องการให้หน้าทั้งหมดถูกบรรจุเป็นแพ็คเกจเดียวที่พกพาได้, และคุณอยากเก็บทุกอย่างใน RAM เพื่อความเร็วและความปลอดภัย.

ในบทแนะนำนี้ เราจะเดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งจะแสดงให้คุณเห็นอย่างชัดเจนว่า **convert HTML zip archive** อย่างไรโดยใช้ **custom resource handler** แล้ว **create zip from memory** ด้วย .NET's `System.IO.Compression`. เมื่อจบคุณจะมีเมธอดที่เป็นอิสระซึ่งสามารถนำไปใช้ในโปรเจค C# ใด ๆ ที่ใช้ Aspose.HTML.

## สิ่งที่คุณต้องการ

- .NET 6+ (หรือ .NET Framework 4.7.2+)  
- Aspose.HTML for .NET (แพคเกจ NuGet `Aspose.HTML`)  
- ความคุ้นเคยพื้นฐานกับ streams และคลาส `ZipArchive`

ไม่มีเครื่องมือภายนอก, ไม่มีไฟล์ชั่วคราว, เพียงการประมวลผลในหน่วยความจำเท่านั้น.

## ขั้นตอนที่ 1: กำหนด Custom Resource Handler

หัวใจของวิธีแก้คือคลาสที่สืบทอดจาก `Aspose.Html.ResourceHandler`. งานของมันคือให้ `Stream` ใหม่สำหรับแต่ละทรัพยากรภายนอกที่เอนจิน HTML เรียกขอ. โดยการคืนค่า `MemoryStream` ใหม่ทุกครั้ง เราจะทำให้ข้อมูลแยกจากกันและพร้อมสำหรับการบรรจุภายหลัง.

```csharp
using System.IO;
using Aspose.Html;

// Step 1 – Custom handler that stores resources in memory
class MemoryResourceHandler : ResourceHandler
{
    // The framework calls this method for every external resource (images, CSS, etc.)
    public override Stream HandleResource(Resource resource)
    {
        // We give the engine an empty stream; later we’ll fill it with the actual bytes.
        // Using MemoryStream means everything stays in RAM.
        return new MemoryStream();
    }
}
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
หากคุณให้ Aspose.HTML เขียนทรัพยากรลงดิสก์ คุณจะต้องทำความสะอาดภายหลัง. ตัวจัดการในหน่วยความจำจะขจัดภาระ I/O และทำให้โค้ดปลอดภัยสำหรับสภาพแวดล้อมแบบ sandbox (เช่น Azure Functions).

## ขั้นตอนที่ 2: โหลดเอกสาร HTML ของคุณ

ต่อไป, ให้ Aspose.HTML ชี้ไปที่ไฟล์ HTML ที่คุณต้องการบรรจุ. เอกสารอาจอยู่บนดิสก์, URL, หรือแม้แต่สตริงดิบ. ที่นี่เราใช้เส้นทางไฟล์เพื่อความง่าย.

```csharp
using Aspose.Html;

// Step 2 – Load the source HTML
HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/input.html");
```

> **เคล็ดลับ:** หาก HTML ของคุณอ้างอิงทรัพยากรแบบ relative, ตรวจสอบให้แน่ใจว่า `input.html` อยู่ในโฟลเดอร์เดียวกับแอสเซทเหล่านั้น, ไม่เช่นนั้นตัวจัดการจะไม่สามารถค้นหาได้.

## ขั้นตอนที่ 3: เชื่อมต่อ Handler และบันทึกลง MemoryStream

ตอนนี้เราจะสร้างอินสแตนซ์ของ handler และบอก Aspose.HTML ให้ใช้มันผ่าน `HtmlSaveOptions.OutputStorage`. HTML ที่ได้ (รวมถึง URL ของทรัพยากรที่เขียนใหม่) จะถูกเก็บไว้ใน `MemoryStream`.

```csharp
using Aspose.Html.Saving;
using System.IO;

// Step 3 – Prepare the handler and an in‑memory buffer for the final HTML
var resourceHandler = new MemoryResourceHandler();

using (MemoryStream htmlMemoryStream = new MemoryStream())
{
    document.Save(htmlMemoryStream, new HtmlSaveOptions
    {
        OutputStorage = resourceHandler // redirects all resources to the handler
    });

    // At this point htmlMemoryStream contains the full HTML file,
    // while each external resource resides in the streams returned by the handler.
```

**กำลังเกิดอะไรขึ้นเบื้องหลัง?**  
เมื่อ `document.Save` ทำงาน, Aspose.HTML จะขอ `MemoryResourceHandler` ให้สตรีมสำหรับแต่ละทรัพยากร. เนื่องจากเราส่งคืน `MemoryStream` ว่าง, เอนจินจะเขียนไบต์ดิบโดยตรงลงในหน่วยความจำ. ไม่มีไฟล์ชั่วคราวถูกสร้าง.

## ขั้นตอนที่ 4: ประกอบไฟล์ ZIP อย่างสมบูรณ์ในหน่วยความจำ

ตอนนี้มาถึงส่วนที่สนุก: เราจะสร้าง `ZipArchive` ที่อยู่ภายใน `MemoryStream` อีกอันหนึ่ง. สิ่งนี้ทำให้เราสามารถ **create zip from memory** โดยไม่ต้องสัมผัสระบบไฟล์.

```csharp
    // Step 4 – Build the ZIP archive in memory
    using (MemoryStream zipMemoryStream = new MemoryStream())
    using (var zipArchive = new ZipArchive(zipMemoryStream, ZipArchiveMode.Create, leaveOpen: true))
    {
        // 4a – Add the main HTML file
        var htmlEntry = zipArchive.CreateEntry("index.html");
        using (var entryStream = htmlEntry.Open())
        {
            // Reset the position of the HTML stream before copying
            htmlMemoryStream.Position = 0;
            htmlMemoryStream.CopyTo(entryStream);
        }

        // 4b – Add each resource that the handler captured
        // The handler stored each resource in a fresh MemoryStream, which we can enumerate.
        // For demonstration, assume we kept a list of those streams (you could store them in a dictionary).
        // Example placeholder – replace with your actual collection:
        // foreach (var kvp in capturedResources)
        // {
        //     var resourceEntry = zipArchive.CreateEntry(kvp.Key); // kvp.Key = relative path
        //     using var entry = resourceEntry.Open();
        //     kvp.Value.Position = 0;
        //     kvp.Value.CopyTo(entry);
        // }

        // When we’re done, flush everything
        zipArchive.Dispose(); // optional because of using, but makes intent clear
    }

    // At this stage zipMemoryStream holds the complete ZIP file.
    // You can return it, write it to a response stream, or save it to disk if you wish.
}
```

> **หมายเหตุ:** ส่วนที่ถูกคอมเมนต์แสดงว่าคุณอาจเก็บสตรีมภายใน `MemoryResourceHandler` อย่างไร. ในสถานการณ์การผลิตคุณจะเก็บแต่ละ `MemoryStream` ในดิกชันนารีโดยใช้ URL ของทรัพยากรต้นฉบับเป็นคีย์, แล้ววนลูปที่นี่เพื่อเพิ่มลงในอาร์ไคฟ์.

**ทำไมต้องเก็บ ZIP ในหน่วยความจำ?**  
การเก็บอาร์ไคฟ์ใน `MemoryStream` ทำให้ส่งตรงไปยังไคลเอนต์ HTTP (`FileResult` ใน ASP.NET Core) หรืออัปโหลดไปยังคลาวด์สตอเรจโดยไม่มีไฟล์กลางเป็นเรื่องง่าย.

## ขั้นตอนที่ 5: (ทางเลือก) บันทึก ZIP ลงดิสก์

หากคุณยังต้องการไฟล์จริง—อาจเพื่อการดีบัก—เพียงเขียน `zipMemoryStream` ลงดิสก์:

```csharp
// Optional: write the in‑memory ZIP to a file for inspection
File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipMemoryStream.ToArray());
```

## ตัวอย่างทำงานเต็มรูปแบบ

เมื่อนำทุกอย่างมารวมกัน, นี่คือโปรแกรมเดียวที่พร้อมคัดลอก‑วางที่ **converts HTML to a ZIP archive** อย่างสมบูรณ์ในหน่วยความจำ.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class MemoryResourceHandler : ResourceHandler
{
    // Capture each resource in a dictionary for later retrieval
    public static readonly System.Collections.Generic.Dictionary<string, MemoryStream> Captured = new();

    public override Stream HandleResource(Resource resource)
    {
        var ms = new MemoryStream();
        // Store the stream using the resource's absolute URL as the key
        Captured[resource.Uri.AbsoluteUri] = ms;
        return ms;
    }
}

class Program
{
    static void Main()
    {
        // Load the HTML file
        HtmlDocument doc = new HtmlDocument("YOUR_DIRECTORY/input.html");

        // Attach the custom handler
        var handler = new MemoryResourceHandler();

        // Save HTML + resources to memory
        using var htmlStream = new MemoryStream();
        doc.Save(htmlStream, new HtmlSaveOptions { OutputStorage = handler });

        // Create the ZIP archive in memory
        using var zipStream = new MemoryStream();
        using (var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            // Add the HTML file
            var htmlEntry = zip.CreateEntry("index.html");
            using (var entry = htmlEntry.Open())
            {
                htmlStream.Position = 0;
                htmlStream.CopyTo(entry);
            }

            // Add each captured resource
            foreach (var kvp in MemoryResourceHandler.Captured)
            {
                // Derive a sane relative path from the URL
                var uri = new Uri(kvp.Key);
                var relativePath = uri.AbsolutePath.TrimStart('/');
                var resEntry = zip.CreateEntry(relativePath);
                using var entry = resEntry.Open();
                kvp.Value.Position = 0;
                kvp.Value.CopyTo(entry);
            }
        }

        // The ZIP is ready – write it out or return it from a web API
        File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipStream.ToArray());

        Console.WriteLine("HTML successfully packaged into output.zip");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะสร้าง `output.zip` ที่มี:

- `index.html` – HTML ที่เขียนใหม่ซึ่งชี้ไปยังทรัพยากรที่บรรจุไว้.  
- รูปภาพ, CSS, และไฟล์ JavaScript ทั้งหมดที่หน้าเดิมอ้างอิง, ถูกเก็บโดยใช้เส้นทาง relative ดั้งเดิม.

เปิด `index.html` จาก ZIP ในเบราว์เซอร์ใดก็ได้และคุณจะเห็นหน้าตรงกับที่แสดงเมื่ออยู่บนระบบไฟล์.

## คำถามทั่วไป & กรณีขอบ

| Question | Answer |
|----------|--------|
| **ถ้าทรัพยากรมีขนาดใหญ่ (เช่น วิดีโอ)?** | เนื่องจากทุกอย่างอยู่ในหน่วยความจำ ไฟล์ขนาดใหญ่มากอาจทำให้เกิด `OutOfMemoryException`. ในกรณีนั้น ให้สตรีมโดยตรงไปยังไฟล์ชั่วคราวหรือจำกัดขนาดที่รับได้. |
| **ต้องจัดการ URL ของทรัพยากรที่ซ้ำกันหรือไม่?** | ดิกชันนารีของ handler จะเขียนทับรายการที่ซ้ำกัน. หากต้องการเก็บเพียงสำเนาเดียว, ตรวจสอบ `Captured.ContainsKey` ก่อนเพิ่ม. |
| **สามารถใช้ในคอนโทรลเลอร์ ASP.NET Core ได้หรือไม่?** | ได้เลย. คืนค่า `File(zipStream.ToArray(), "application/zip", "page.zip")` จากเมธอดแอคชัน. |
| **จะทำอย่างไรกับทรัพยากร HTTPS?** | Aspose.HTML จะดาวน์โหลดโดยอัตโนมัติตราบใดที่ runtime เชื่อถือใบรับรอง SSL. สำหรับใบรับรอง self‑signed, ให้กำหนดค่า `ServicePointManager.ServerCertificateValidationCallback`. |
| **ตัวจัดการแบบกำหนดเองปลอดภัยต่อการทำงานหลายเธรดหรือไม่?** | ตัวอย่างใช้ดิกชันนารีแบบ static, ซึ่ง *ไม่* ปลอดภัยต่อหลายเธรด. ควรห่อการเข้าถึงด้วย lock หรือใช้ `ConcurrentDictionary` หากต้องประมวลผลหลายเอกสารพร้อมกัน. |

## เคล็ดลับสำหรับการใช้งานในโปรดักชัน

- **Reuse the handler** เฉพาะสำหรับเอกสารเดียว; สร้างอินสแตนซ์ใหม่ต่อคำขอเพื่อหลีกเลี่ยงการสื่อสารข้ามผู้ใช้.  
- **Dispose streams** อย่างรวดเร็ว. แม้ว่า `using` blocks จะจัดการส่วนใหญ่, สตรีมที่เก็บในดิกชันนารีใด ๆ ควรทำการ dispose หลังจากสร้าง ZIP เสร็จ.  
- **Validate the HTML** ก่อนประมวลผลเพื่อจับ markup ที่ผิดรูปแบบซึ่งอาจทำให้ handler ขอทรัพยากรที่ไม่คาดคิด.  
- **Compress aggressively** โดยตั้งค่า `ZipArchiveEntry.CompressionLevel = CompressionLevel.Optimal` หากขนาดไฟล์สำคัญ.  

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **custom resource handler** ผ่านหน้า HTML, จับทุกแอสเซทที่เชื่อมโยง, และ **create zip from memory** โดยไม่ต้องสัมผัสดิสก์. รูปแบบที่แสดงนี้ยืดหยุ่นพอสำหรับสถานการณ์เว็บ‑เซอร์วิส, งานเบื้องหลัง, หรือแม้แต่ยูทิลิตี้เดสก์ท็อปที่ต้องส่งมอบบันเดิล HTML ที่เป็นอิสระ.

ลองใช้ดู—เปลี่ยน `YOUR_DIRECTORY/input.html` เป็นหน้าใดก็ได้ที่คุณต้องการ, ปรับแต่ง handler ให้เก็บทรัพยากรใน `ConcurrentDictionary`, แล้วคุณจะมี pipeline HTML‑to‑ZIP ในหน่วยความจำที่แข็งแรงพร้อมสำหรับการผลิต.

*พร้อมจะก้าวต่อไหม?* ต่อไปสำรวจวิธี **convert HTML to PDF** ด้วย Aspose.HTML, หรือทดลองเข้ารหัส ZIP เพื่อความปลอดภัยเพิ่ม. ไม่มีขีดจำกัดเมื่อคุณเชี่ยวชาญการสตรีมในหน่วยความจำด้วย C#. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}