---
category: general
date: 2026-03-31
description: สร้าง memory stream ใน C# และเรียนรู้การแปลง HTML เป็น PNG, ใช้ตัวจัดการทรัพยากรแบบกำหนดเอง,
  บันทึก HTML เป็นไฟล์ ZIP, และตั้งค่าแบบอักษรโดยโปรแกรม—ทั้งหมดในบทเรียนเดียว
draft: false
keywords:
- create memory stream
- render html to png
- custom resource handler
- save html to zip
- set font style programmatically
language: th
og_description: สร้าง memory stream ใน C# และเรนเดอร์ HTML เป็น PNG ทันที, ใช้ตัวจัดการทรัพยากรแบบกำหนดเอง,
  บันทึก HTML เป็น ZIP, และตั้งค่าแบบอักษรโดยโปรแกรม
og_title: สร้าง Memory Stream ใน C# – คู่มือการเขียนโปรแกรมฉบับสมบูรณ์
tags:
- C#
- HTML rendering
- Streams
- ZIP archives
- Image processing
title: สร้าง Memory Stream ใน C# – คู่มือเต็มกับการแสดงผล HTML และการส่งออกเป็น ZIP
url: /th/net/rendering-html-documents/create-memory-stream-in-c-full-guide-with-html-rendering-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Memory Stream ใน C# – คู่มือเต็มพร้อมการเรนเดอร์ HTML & การส่งออก ZIP

เคยสงสัยไหมว่า **create memory stream** ใน C# แล้วแปลงเอกสาร HTML ให้เป็นภาพ PNG, ไฟล์ ZIP, หรือแม้กระทั่งเปลี่ยนสไตล์ฟอนต์แบบเรียลไทม์? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อต้องการตัวแทนเอกสารในหน่วยความจำโดยไม่ต้องสัมผัสระบบไฟล์  

ในบทเรียนนี้เราจะเดินผ่านโซลูชันแบบครบวงจร: เราจะสร้าง custom resource handler, ส่ง HTML เข้า `MemoryStream`, บีบอัดเอกสารเดียวกันเป็น ZIP, และสุดท้ายเรนเดอร์เป็นภาพพร้อม antialiasing. เมื่อเสร็จคุณจะสามารถ **render HTML to PNG**, **save HTML to ZIP**, และ **set font style programmatically** โดยไม่ต้องเขียนไฟล์ชั่วคราวลงดิสก์เลย

## Prerequisites

- .NET 6.0 หรือใหม่กว่า (API มีความเสถียรข้ามเวอร์ชันล่าสุด)  
- การอ้างอิงไลบรารี HTML‑to‑image ที่ให้ `HTMLDocument`, `ImageRenderer` และประเภทที่เกี่ยวข้อง – ตัวอย่างเช่น **HtmlRenderer.Core** (เปลี่ยนเป็นแพ็กเกจที่คุณใช้จริง)  
- ความคุ้นเคยพื้นฐานกับ streams, คำสั่ง `using`, และรูปแบบการเขียนแบบ object‑oriented ของ C#

> **Pro tip:** หากคุณใช้ Visual Studio ให้เปิดใช้ **nullable reference types** (`<Nullable>enable</Nullable>`) เพื่อจับบั๊กละเอียดได้ตั้งแต่ต้น

## Step 1: Create a Memory Stream with a Custom Resource Handler

สิ่งแรกที่เราต้องการคือ handler ที่บอก engine ของ HTML *ว่าจะเขียน* resource แต่ละอย่าง (รูปภาพ, CSS, ฯลฯ) ไปที่ไหน. โดยสืบทอดจาก `ResourceHandler` เราสามารถส่งออกทุกอย่างเข้า `MemoryStream` เดียวได้

```csharp
using System;
using System.IO;

// Step 1: Define a handler that writes resources to an in‑memory stream
class MemoryResourceHandler : ResourceHandler
{
    // The stream lives for the whole lifetime of the handler
    public MemoryStream OutputStream = new MemoryStream();

    // The engine calls this for every resource it needs to write
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
`MemoryStream` ทำงานทั้งหมดใน RAM, ไม่ต้องทำ I/O กับดิสก์, เหมาะอย่างยิ่งกับสถานการณ์ที่ต้องการประสิทธิภาพสูงเช่นเว็บเซอร์วิสหรือ unit test. Handler นี้ยังทำให้ API พอใจเพราะ engine คาดหวัง `Stream` สำหรับแต่ละ resource

## Step 2: Load the HTML Document and Save It to the Memory Stream

ต่อไปเราจะโหลดไฟล์ HTML ที่มีอยู่ (หรือสตริง) แล้วบอกให้ใช้ `MemoryResourceHandler` ของเรา. หลังจากเรียก `Save` แล้ว `OutputStream` จะมี payload HTML เต็มรูปแบบ

```csharp
using System.IO;

// Assume the HTML file lives under YOUR_DIRECTORY
HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

// Instantiate the memory handler
MemoryResourceHandler memoryHandler = new MemoryResourceHandler();

// Save the document – all resources flow into the same MemoryStream
htmlDoc.Save(memoryHandler);
```

ในขั้นตอนนี้ตำแหน่งของ stream อยู่ที่ท้ายไฟล์, ดังนั้นเราต้องรีวินด์ก่อนจึงจะอ่านเนื้อหาได้

```csharp
// Reset the stream position to the beginning
memoryHandler.OutputStream.Position = 0;

// Quick verification (optional)
// string htmlContent = new StreamReader(memoryHandler.OutputStream).ReadToEnd();
// Console.WriteLine(htmlContent);
```

> **Note:** บรรทัด `ReadToEnd` ด้านบนถูกคอมเมนต์ไว้เพราะในสภาพแวดล้อมการผลิตคุณอาจส่ง stream ไปยังคอมโพเนนต์อื่นแทนการพิมพ์ออก

## Step 3: Zip the Same HTML Using a Custom ZIP Resource Handler

บางครั้งคุณต้องส่ง HTML พร้อมกับ assets ของมัน. Handler แบบกำหนดเองตัวที่สองสามารถสร้าง entry ของ ZIP สำหรับแต่ละ resource ได้ทันที

```csharp
using System.IO.Compression;

// Step 4: Define a handler that writes each resource into a ZIP archive
class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(string zipPath)
    {
        // Open (or create) the archive in write mode
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);
    }

    // The engine calls this for each resource; we create a ZIP entry with the same name
    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    // Proper disposal of the underlying ZipArchive
    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}
```

ต่อไปเราจะใช้ instance ของ `htmlDoc` เดิมและเขียนลงไฟล์ ZIP

```csharp
// Step 5: Save the HTML document into a ZIP file
using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
{
    htmlDoc.Save(zipHandler);
}
```

**เคล็ดลับกรณีขอบ:** หาก HTML อ้างอิงรูปเดียวกันหลายครั้ง, ZIP handler จะสร้าง entry ซ้ำ. เพื่อหลีกเลี่ยง, คุณสามารถเก็บ `HashSet<string>` ของชื่อที่เพิ่มแล้วและคืน stream ของ entry ที่มีอยู่แทน

## Step 4: Programmatically Set Font Style on the Default Stylesheet

การเปลี่ยนลุคของเอกสารโดยไม่แก้ไข HTML ต้นฉบับเป็นเรื่องสะดวก—เช่นเมื่อต้องสร้าง preview PDF ที่หัวข้อเป็นตัวหนา. ไลบรารีเปิดเผย `DefaultViewStyleSheet` ที่คุณสามารถปรับได้

```csharp
// Step 6: Apply bold and italic styling to the default view stylesheet
htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

คุณสามารถรวม flag ใด ๆ ที่กำหนดใน `WebFontStyle`. การเปลี่ยนแปลงจะมีผลทันทีและส่งผลต่อการเรนเดอร์หรือการบันทึกต่อไป

## Step 5: Render the HTML Document to a PNG Image

สุดท้าย, เราจะเปลี่ยน HTML ให้เป็นภาพ raster. การเปิดใช้งาน antialiasing และ hinting จะทำให้ข้อความคมชัดและขอบเรียบเนียน

```csharp
using System.Drawing; // For ImageRenderingOptions if needed

// Step 7: Render the document to an image with antialiasing and hinting
var renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    UseHinting = true
};

new ImageRenderer(renderingOptions).Render(htmlDoc, "YOUR_DIRECTORY/out.png");
```

**สิ่งที่คุณจะเห็น:** ไฟล์ PNG ชื่อ `out.png` อยู่ใน `YOUR_DIRECTORY` ที่ดูเหมือนกับการเรนเดอร์ของเบราว์เซอร์, พร้อมสไตล์ bold‑italic ที่ตั้งค่าไว้ก่อนหน้า

![ภาพหน้าจอของผลลัพธ์การสร้าง memory stream](placeholder-image.png "ตัวอย่างการสร้าง memory stream")

*ข้อความ alt ของรูปภาพรวมคีย์เวิร์ดหลักเพื่อรองรับ SEO*

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| **Can I reuse the same `HTMLDocument` after saving to a ZIP?** | ใช่. วัตถุ document ยังคงอยู่ในหน่วยความจำ; คุณสามารถเรียก `Save` หลายครั้งด้วย handler ที่ต่างกันได้ |
| **What if the HTML contains large binary assets?** | `MemoryStream` จะขยายตามขนาดนั้น. สำหรับไฟล์ขนาดใหญ่มาก ควร stream ตรงไปไฟล์หรือใช้ `BufferedStream` |
| **Do I need to call `Dispose` on `MemoryResourceHandler`?** | ไม่จำเป็นอย่างเคร่งครัดเพราะมันถือแค่ `MemoryStream` ที่จะถูกทำลายเมื่อ handler ถูก garbage‑collected. อย่างไรก็ตามการเรียก `Dispose` ถือเป็นนิสัยที่ดี |
| **How do I change the image format (e.g., JPEG instead of PNG)?** | ส่งส่วนขยายไฟล์ที่ต่างออกไปให้ `ImageRenderer.Render`, หรือใช้ `ImageRenderer.RenderToBitmap` แล้วบันทึกด้วย `bitmap.Save("out.jpg", ImageFormat.Jpeg)` |
| **Is the ZIP handler thread‑safe?** | ไม่. `ZipArchive` ไม่ปลอดภัยต่อหลายเธรด, ดังนั้นควรจัดลำดับการเข้าถึงหรือสร้าง handler แยกสำหรับแต่ละเธรด |

## Full Working Example

ด้านล่างเป็นโปรแกรมพร้อมคัดลอก‑วางที่สาธิตทุกขั้นตอนที่กล่าวมา. แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริงบนเครื่องของคุณ

```csharp
// FullExample.cs
using System;
using System.IO;
using System.IO.Compression;

// Assume these types come from your HTML rendering library
using HtmlRendering; // placeholder namespace

class MemoryResourceHandler : ResourceHandler
{
    public MemoryStream OutputStream = new MemoryStream();
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}

class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(string zipPath) =>
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);

    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load HTML
        var htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

        // 2️⃣ Write to a memory stream
        var memHandler = new MemoryResourceHandler();
        htmlDoc.Save(memHandler);
        memHandler.OutputStream.Position = 0;
        // Optional: verify content
        // Console.WriteLine(new StreamReader(memHandler.OutputStream).ReadToEnd());

        // 3️⃣ Zip the same document
        using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
        {
            htmlDoc.Save(zipHandler);
        }

        // 4️⃣ Change font style programmatically
        htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // 5️⃣ Render to PNG with antialiasing & hinting
        var renderOpts = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            UseHinting = true
        };
        new ImageRenderer(renderOpts).Render(htmlDoc, "YOUR_DIRECTORY/out.png");

        Console.WriteLine("All operations completed successfully.");
    }
}
```

เมื่อคุณรันโปรแกรมนี้คุณจะได้สามผลลัพธ์:

1. **In‑memory HTML** ที่เก็บอยู่ใน `memHandler.OutputStream`  
2. **`output.zip`** ที่บรรจุ HTML และ resource ทั้งหมดที่เชื่อมโยง  
3. **`out.png`** – ภาพที่เรนเดอร์โดยคำนึงถึงสไตล์ bold‑italic

## Conclusion

เราได้แสดงวิธี **create memory stream** ใน C# และผสานรวมกับการเรนเดอร์ HTML, การบีบอัดเป็น ZIP, และการสร้างภาพ. สิ่งสำคัญคือ `HTMLDocument` เดียวสามารถบันทึกได้หลายรูปแบบ—เข้า `MemoryStream`, เข้า ZIP archive, หรือเข้าไฟล์ PNG—โดยการสลับ `ResourceHandler` เท่านั้น  

ถ้าคุณพร้อมจะต่อยอด, ลอง:

- **Render to PDF** ด้วย PDF renderer ที่รับ `Stream`  
- **Compress the memory stream** ก่อนส่งผ่านเครือข่าย (เช่น `GZipStream`)  
- **Combine multiple HTML pages** เป็น ZIP เดียวสำหรับการส่งออกเป็นกลุ่ม

ทดลองเล่นได้ตามสบาย, และอย่าลังเลที่จะคอมเมนต์หากเจออุปสรรค. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}