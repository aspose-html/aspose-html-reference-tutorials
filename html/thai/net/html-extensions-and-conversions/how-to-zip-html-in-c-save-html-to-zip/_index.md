---
category: general
date: 2025-12-29
description: วิธีบีบอัด HTML ใน C# อย่างรวดเร็วด้วย Aspose.HTML – บันทึก HTML เป็นไฟล์
  zip ด้วย ZipResourceHandler ที่กำหนดเอง เรียนรู้ขั้นตอนโดยละเอียด
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: th
og_description: วิธีบีบอัด HTML ใน C# อย่างรวดเร็วด้วย Aspose.HTML. ทำตามคำแนะนำนี้เพื่อบันทึก
  HTML เป็นไฟล์ zip และสร้างไฟล์ zip พร้อมการจัดการทรัพยากรแบบกำหนดเอง.
og_title: วิธีบีบอัด HTML เป็น Zip ใน C# – บันทึก HTML เป็น Zip
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: วิธีบีบอัด HTML เป็น Zip ใน C# – บันทึก HTML เป็น Zip
url: /th/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีบีบอัด HTML เป็น Zip ใน C# – บันทึก HTML ไปยัง Zip

การบีบอัด HTML เป็น Zip ใน C# เป็นความต้องการทั่วไปเมื่อคุณต้องการจัดเก็บหน้าเว็บสำหรับการใช้งานออฟไลน์ ไม่ว่าคุณจะบรรจุหน้าเดียวพร้อมรูปภาพหรือส่งออกทั้งเว็บไซต์ **การบันทึก HTML ไปยัง zip** จะช่วยให้ทุกอย่างเป็นระเบียบและพกพาได้ง่าย ในบทเรียนนี้เราจะเดินผ่านโซลูชันที่พร้อมใช้งานครบชุด ซึ่งไม่เพียงแค่บีบอัด markup ของ HTML แต่ยังสตรีมทรัพยากรที่อ้างอิงทั้งหมดโดยตรงเข้าไปในไฟล์ archive

คุณจะได้เรียนรู้วิธี:

* สร้างไฟล์ zip อย่างโปรแกรมเมติกด้วย `System.IO.Compression` ของ .NET
* เชื่อม `ResourceHandler` แบบกำหนดเองเข้าไปใน Aspose.HTML เพื่อให้ทรัพยากรไหลตรงเข้าสู่ zip
* จัดการกรณีขอบเขตเช่นไฟล์ zip ที่มีอยู่แล้วและไฟล์ไบนารีขนาดใหญ่

ไม่ต้องใช้เครื่องมือภายนอก—แค่ C#, Aspose.HTML, และไม่กี่บรรทัดของโค้ด

## สิ่งที่คุณต้องมี

ก่อนที่เราจะดำเนินการต่อ ให้ตรวจสอบว่าคุณมี:

* **.NET 6+** (โค้ดนี้ทำงานบน .NET Framework 4.6.2 ขึ้นไปด้วย)
* **Aspose.HTML for .NET** – คุณสามารถดาวน์โหลดเวอร์ชันทดลองฟรีจากเว็บไซต์ Aspose หรือใช้สำเนาที่มีลิขสิทธิ์
* สภาพแวดล้อมการพัฒนา (Visual Studio, VS Code, Rider—อะไรก็ตามที่คุณชอบ)

เท่านี้เอง ไม่ต้องเพิ่ม NuGet package ใด ๆ นอกจาก `System.IO.Compression` (รวมมาใน .NET) และ `Aspose.HTML`

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และนำเข้า

สร้างโปรเจกต์คอนโซลใหม่ (หรือวางโค้ดลงในโปรเจกต์ที่มีอยู่) แล้วเพิ่ม `using` directives ที่จำเป็นไว้ด้านบนของไฟล์ของคุณ:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **เคล็ดลับ:** หากคุณใช้ Visual Studio IDE จะเสนอให้เพิ่ม NuGet package ที่ขาดหายสำหรับ `Aspose.Html` ให้ยอมรับ แล้วคุณก็พร้อมใช้งาน

## ขั้นตอนที่ 2: สร้าง Custom ZipResourceHandler

Aspose.HTML จะเรียก `ResourceHandler` ทุกครั้งที่ต้องเขียนทรัพยากร (เช่นรูปภาพ, ไฟล์ CSS, หรือสคริปต์) โดยการโอเวอร์ไรด์ `HandleResource` เราสามารถกำหนดได้ว่าทรัพยากรแต่ละรายการจะไปอยู่ที่ไหน ตัวจัดการด้านล่างนี้สร้าง zip entry ที่สะท้อนเส้นทางตรรกะของทรัพยากร แล้วคืนสตรีมที่เขียนได้โดยตรงไปยัง entry นั้น

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**ทำไมเรื่องนี้สำคัญ:**  
แทนที่จะเขียนทรัพยากรลงในโฟลเดอร์ชั่วคราวแล้วค่อยบีบอัดโฟลเดอร์นี้ ตัวจัดการนี้สตรีมข้อมูลแบบเรียลไทม์ ลดการอ่าน/เขียนบนดิสก์และใช้หน่วยความจำน้อยลง อีกทั้งยังทำให้โครงสร้างโฟลเดอร์ภายใน zip ตรงกับเส้นทางสัมพันธ์ของ HTML ซึ่งเบราว์เซอร์ต้องการเมื่อคุณแตกไฟล์และเปิดหน้า

## ขั้นตอนที่ 3: เตรียม Zip Archive

ต่อไปเราจะเปิด (หรือสร้าง) ไฟล์ zip ปลายทาง ฟลัก `FileMode.Create` จะเขียนทับไฟล์ที่มีอยู่—เหมาะสำหรับการสร้างซ้ำ หากคุณต้องการเก็บไฟล์ archive ที่มีอยู่แล้ว ให้เปลี่ยนเป็น `FileMode.OpenOrCreate` แล้วจัดการกับ entry ที่ซ้ำกันตามต้องการ

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **กรณีขอบเขต:** หากกระบวนการล่มก่อนที่บล็อก `using` จะทำการ dispose archive คุณอาจได้ไฟล์ zip ที่เสียหาย การรันโค้ดภายใน `try/catch` แล้วลบไฟล์ที่สร้างขึ้นบางส่วนเมื่อเกิดข้อผิดพลาดเป็นวิธีป้องกันง่าย ๆ

## ขั้นตอนที่ 4: สร้าง HTML Document พร้อมทรัพยากรฝังตัว

เพื่อเป็นตัวอย่าง เราจะสร้างหน้า HTML ขนาดเล็กที่อ้างอิงรูปภาพชื่อ `image.png` ในสถานการณ์จริงคุณอาจโหลด HTML จากไฟล์หรือสตริงที่มาจากฐานข้อมูล

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

หากคุณมีไฟล์รูปภาพจริงบนดิสก์ คุณสามารถเพิ่มไฟล์เหล่านั้นลงใน zip ด้วยตนเองก่อนบันทึก HTML, หรือให้ Aspose.HTML ดึงไฟล์เหล่านั้นผ่านตัวจัดการ (เช่นจาก URL) ตัวจัดการที่เราเขียนทำงานได้ทั้งกับเส้นทางโลคัลและ URL ระยะไกล

## ขั้นตอนที่ 5: ตั้งค่า Save Options ให้ใช้ ZipResourceHandler

ตอนนี้เราบอก Aspose.HTML ให้ใช้ตัวจัดการแบบกำหนดเองของเราเมื่อเขียนทรัพยากร `HTMLSaveOptions` ยังให้คุณระบุชื่อไฟล์ผลลัพธ์ภายใน zip (ค่าเริ่มต้นคือ `index.html`)

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## ขั้นตอนที่ 6: บันทึก Document – ทุกอย่างสตรีมเข้า Zip

สุดท้ายเรียก `Save` Aspose.HTML จะวิเคราะห์ markup, ค้นหาแท็ก `<img>`, เรียก `HandleResource` สำหรับ `image.png` และเขียนทั้งไฟล์ HTML และรูปภาพเข้าไปใน archive เดียวกัน

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

เมื่อบล็อก `using` สิ้นสุด `ZipArchive` จะทำการสรุปไฟล์ ทำให้พร้อมสำหรับการแจกจ่าย

### ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมทั้งหมดที่ประกอบรวมไว้ด้วยกัน คัดลอก‑วางลงใน `Program.cs` แล้วรัน—ไม่ต้องแก้ไขเพิ่มเติม

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** หลังจากรันเสร็จ `output.zip` จะมีสอง entry:

```
index.html
image.png
```

หากคุณแตกไฟล์และเปิด `index.html` ในเบราว์เซอร์ รูปภาพจะแสดงอย่างถูกต้องเพราะเส้นทางสัมพันธ์ถูกเก็บไว้

## คำถามที่พบบ่อย

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}