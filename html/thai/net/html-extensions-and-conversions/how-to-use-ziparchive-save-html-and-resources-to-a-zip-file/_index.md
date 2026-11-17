---
category: general
date: 2026-03-29
description: เรียนรู้วิธีใช้ ZipArchive ใน C# เพื่อแปลง HTML เป็น ZIP, บันทึก HTML
  เป็น ZIP และบีบอัดรูปภาพใน HTML—ทั้งหมดในบทเรียนที่ชัดเจนหนึ่งเดียว
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: th
og_description: ค้นพบวิธีใช้ ZipArchive ใน C# เพื่อแปลง HTML เป็น ZIP, บันทึก HTML
  เป็น ZIP, และบีบอัดรูปภาพใน HTML พร้อมตัวอย่างที่สมบูรณ์และสามารถรันได้
og_title: วิธีใช้ ZipArchive – บันทึก HTML และทรัพยากรเป็นไฟล์ ZIP
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: วิธีใช้ ZipArchive – บันทึก HTML และทรัพยากรเป็นไฟล์ ZIP
url: /th/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ ZipArchive – บันทึก HTML และทรัพยากรเป็นไฟล์ ZIP

เคยสงสัย **how to use ZipArchive** ว่าจะรวมหน้า HTML กับรูปภาพ, CSS, และทรัพยากรอื่น ๆ อย่างไรไหม? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อจำเป็นต้องจัดส่งแพ็กเกจ HTML ที่เป็นอิสระ, โดยเฉพาะเมื่อหน้ามีการอ้างอิงทรัพยากรภายนอก ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ C# และ Aspose.HTML คุณสามารถ **convert HTML to ZIP**, **save HTML to ZIP**, และแม้แต่ **compress HTML images** ได้โดยไม่ต้องออกจาก IDE.

ในบทแนะนำนี้ เราจะเดินผ่านกระบวนการทั้งหมด—ตั้งแต่การสร้าง `HTMLDocument` อย่างง่ายจนถึงการจัดการทรัพยากรที่เชื่อมโยงทั้งหมดผ่าน `ResourceHandler` แบบกำหนดเอง. เมื่อเสร็จคุณจะมีไฟล์ ZIP พร้อมใช้งานที่สามารถวางลงบนเว็บเซิร์ฟเวอร์ใดก็ได้หรือแนบในอีเมล. ไม่มีสคริปต์ภายนอก, ไม่มีการคัดลอกด้วยมือ—เพียง .NET แท้.

## ข้อกำหนดเบื้องต้น

- **.NET 6+** (หรือ .NET Framework 4.6+). API ที่ใช้เป็นส่วนหนึ่งของ `System.IO.Compression`.
- **Aspose.HTML for .NET** ติดตั้งแล้ว (แพ็กเกจ NuGet `Aspose.Html`).
- ความเข้าใจพื้นฐานเกี่ยวกับไวยากรณ์ C#.
- IDE เช่น Visual Studio หรือ VS Code.

เท่านี้เอง. ไม่มีเครื่องมือเพิ่มเติม, ไม่มียูทิลิตี้ zip ของบุคคลที่สาม. พร้อมหรือยัง? มาเริ่มกัน.

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และเพิ่ม Dependencies

สร้างโปรเจกต์คอนโซลใหม่:

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

แพ็กเกจ `Aspose.Html` ให้คลาส `HTMLDocument` และคลาสฐาน `ResourceHandler` ที่เราจะขยายในภายหลัง. เนมสเปซในตัว `System.IO.Compression` ให้ `ZipArchive` และ `ZipArchiveEntry`.

> **Pro tip:** หากคุณตั้งเป้าหมายเป็น .NET 6, คุณสามารถใช้ top‑level statements เพื่อทำให้เมธอด `Main` ดูเรียบร้อย. โค้ดด้านล่างใช้คลาส `Program` แบบคลาสสิกเพื่อความชัดเจน.

## ขั้นตอนที่ 2: สร้าง Custom Resource Handler

เมื่อ Aspose.HTML บันทึกเอกสาร, มันจะเรียก `ResourceHandler` ให้จัดหา `Stream` สำหรับไฟล์ภายนอกแต่ละไฟล์ (รูปภาพ, CSS, ฟอนต์, ฯลฯ). โดยการ override `HandleResource` เราสามารถส่งทรัพยากรทุกอย่างตรงเข้า zip entry ได้.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Writes each HTML resource (image, CSS, etc.) directly into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        // Ensure a folder hierarchy inside the zip (optional but tidy)
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open(); // Aspose streams the content into this entry.
    }
}
```

**Why this matters:** แทนที่จะเขียนทรัพยากรลงดิสก์ก่อนแล้วจึง zip, ตัว handler จะ stream โดยตรง, ซึ่งลดภาระ I/O และรับประกันว่า zip จะสอดคล้องกับเนื้อหา HTML.

## ขั้นตอนที่ 3: สร้าง HTML Document

เพื่อการสาธิต, เราจะฝัง snippet HTML เล็ก ๆ ที่อ้างอิงรูปภาพภายนอกชื่อ `logo.png`. ในโปรเจกต์จริงคุณอาจโหลด HTML จากไฟล์หรือฐานข้อมูล.

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

หากคุณต้องการ **compress HTML images**, เพียงตรวจสอบให้ไฟล์รูปภาพอยู่ใกล้กับไฟล์ executable (หรือฝังเป็น resource). `ZipResourceHandler` จะเพิ่มรูปภาพลงใน archive โดยอัตโนมัติ.

## ขั้นตอนที่ 4: เปิด (หรือสร้าง) ไฟล์ ZIP และบันทึก

ตอนนี้เราจะเชื่อมทุกอย่างเข้าด้วยกัน. เราเปิด `FileStream` สำหรับ zip ผลลัพธ์, สร้างอินสแตนซ์ `ZipArchive` ในโหมด *Update*, และส่ง handler ที่กำหนดเองของเราให้กับ `HTMLDocument.Save`.

```csharp
using (var fileStream = new FileStream("output.zip", FileMode.Create))
using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
{
    // Initialise the handler with the open ZipArchive.
    var zipHandler = new ZipResourceHandler(zipArchive);

    // Save the HTML document; the handler writes HTML, images, CSS, etc. into the zip.
    htmlDocument.Save(zipHandler);
}
```

เมื่อบล็อก `using` สิ้นสุด, zip จะถูกสรุปและปิดโดยอัตโนมัติ. `output.zip` ที่ได้จะประกอบด้วย:

- `index.html` (เอกสาร HTML ที่ถูก serialize)
- `logo.png` (รูปภาพที่อ้างอิงใน HTML)

คุณสามารถตรวจสอบเนื้อหาโดยเปิด zip ในไฟล์เอ็กซ์พลอเรอร์ใดก็ได้.

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์ (ทางเลือก)

เป็นความคิดที่ดีเสมอที่จะตรวจสอบว่า zip ทำงานจริงหรือไม่. นี่คือ snippet สั้น ๆ ที่คุณสามารถรันหลังจากโค้ดก่อนหน้าเพื่อแสดงรายการ entry:

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

คุณควรเห็นอะไรประมาณนี้:

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

เปิด `index.html` จากโฟลเดอร์ที่แตกไฟล์ออก, คุณจะเห็นรูปภาพแสดงผลอย่างถูกต้อง—เป็นหลักฐานว่า **save HTML to ZIP** ทำงานตามที่ตั้งใจ.

## ความแปรผันทั่วไป & กรณีขอบ

### 1. ใช้ชื่อ Entry ที่แตกต่างสำหรับไฟล์ HTML

โดยค่าเริ่มต้น Aspose จะเขียน HTML ไปที่ `index.html`. หากต้องการชื่อที่กำหนดเอง, คุณสามารถตั้งค่า `htmlDocument.FileName` ก่อนบันทึกได้:

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. เพิ่มไฟล์เพิ่มเติมด้วยตนเอง

บางครั้งคุณอาจต้องการรวมไฟล์เพิ่มเติม (เช่น README). คุณสามารถเพิ่มไฟล์เหล่านั้นโดยตรงลงใน `ZipArchive` ก่อนเรียก `htmlDocument.Save` ได้:

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. จัดการรูปภาพขนาดใหญ่อย่างมีประสิทธิภาพ

หาก HTML ของคุณอ้างอิงรูปภาพขนาดใหญ่มาก, ควรปรับขนาดล่วงหน้าเพื่อให้ขนาด zip อยู่ในระดับที่สมเหตุสมผล. แพ็กเกจ `System.Drawing.Common` สามารถช่วยได้:

```csharp
// Example: Resize logo.png to a max width of 800px before zipping.
using (var img = System.Drawing.Image.FromFile("logo.png"))
{
    int maxWidth = 800;
    if (img.Width > maxWidth)
    {
        var ratio = (double)maxWidth / img.Width;
        var newHeight = (int)(img.Height * ratio);
        using var thumb = img.GetThumbnailImage(maxWidth, newHeight, () => false, IntPtr.Zero);
        thumb.Save("logo_resized.png");
    }
}
```

จากนั้นให้ชี้ `<img src='logo_resized.png'>` ใน HTML ของคุณ.

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงใน `Program.cs`. มันคอมไพล์และรันได้โดยตรง, สมมติว่าคุณได้ติดตั้งแพ็กเกจ NuGet ของ Aspose.HTML แล้ว.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Custom handler that streams each resource into a zip entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create an HTML document that references an external image.
        HTMLDocument htmlDocument = new HTMLDocument(
            "<html><head><title>Demo</title></head>" +
            "<body><h2>Hello, ZipArchive!</h2>" +
            "<img src='logo.png' alt='Demo logo'></body></html>"
        );

        // 2️⃣ Open (or create) the output zip file.
        using (var fileStream = new FileStream("output.zip", FileMode.Create))
        using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Initialise the custom handler.
            var zipHandler = new ZipResourceHandler(zipArchive);

            // 4️⃣ Save the HTML; resources get streamed into the zip.
            htmlDocument.Save(zipHandler);
        }

        Console.WriteLine("✅ HTML document and its resources have been saved to output.zip");
    }
}
```

**Expected output:** คอนโซลจะแสดงข้อความสำเร็จ, และ `output.zip` จะปรากฏในโฟลเดอร์โปรเจกต์ที่มี `index.html` และ `logo.png`.

## คำถามที่พบบ่อย

- **Does this work on .NET Core?**  
  ใช่. `System.IO.Compression.ZipArchive` เป็นส่วนหนึ่งของ .NET Standard, ดังนั้นโค้ดเดียวกันทำงานบน .NET 5, .NET 6, และ .NET 7.

- **What if I need to **compress HTML images** more aggressively?**  
  คุณสามารถทำการประมวลผลล่วงหน้าภาพ (ปรับขนาด, เปลี่ยนรูปแบบเป็น WebP, ฯลฯ) ก่อนที่จะเพิ่มลงใน zip. ตัว handler เองจะ stream ข้อมูลที่ได้รับเท่านั้น.

- **Can I encrypt the zip?**  
  `ZipArchive` รองรับการเข้ารหัส AES เฉพาะผ่านไลบรารีของบุคคลที่สาม (เช่น `SharpZipLib`). หากคุณต้องการการเข้ารหัส, สร้าง zip ด้วยไลบรารีนั้นแล้วจึงส่งสตรีมให้ Aspose เป็น `ResourceHandler` แบบกำหนดเอง.

- **Is there a way to set the root folder inside the zip?**  
  ใช่—เพิ่มชื่อโฟลเดอร์ก่อน `resourceName` ภายใน `HandleResource`, เช่น `var entry = _zipArchive.CreateEntry($"site/{resourceName}", ...)`.

## สรุป

ตอนนี้คุณรู้แล้วว่า **how to use ZipArchive** ใน C# เพื่อ **convert HTML to ZIP**, **save HTML to ZIP**, และ **compress HTML images** ทั้งหมดในเวิร์กโฟลว์เดียวที่เรียบง่าย. ด้วยการขยาย `ResourceHandler` เราเลี่ยงไฟล์ชั่วคราวและทำให้กระบวนการใช้หน่วยความจำอย่างมีประสิทธิภาพ. รูปแบบนี้ขยายได้ดี: เพียงวาง zip ที่สร้างขึ้นบนเว็บเซิร์ฟเวอร์, ส่งอีเมล, หรือเก็บไว้ในคลาวด์สตอเรจ.

ขั้นตอนต่อไปที่คุณอาจสำรวจ:

- **Create ZIP archives programmatically** สำหรับโฟลเดอร์เว็บไซต์ทั้งหมด (`create zip archive c#`).
- **Add PDF or DOCX conversions** ก่อนทำการ zip เพื่อให้ได้แพ็กเกจเอกสารที่สมบูรณ์ขึ้น.
- **Integrate with ASP.NET Core** เพื่อ stream zip โดยตรงไปยังเบราว์เซอร์ของผู้ใช้ (`FileStreamResult`).

มีคำถามเพิ่มเติมเกี่ยวกับการ zip HTML, การจัดการฟอนต์, หรือการเพิ่มประสิทธิภาพขนาดภาพ? แสดงความคิดเห็นหรือทักมาใน Stack Overflow. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}