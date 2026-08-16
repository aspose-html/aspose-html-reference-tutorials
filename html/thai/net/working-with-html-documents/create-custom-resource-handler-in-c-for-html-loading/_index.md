---
category: general
date: 2026-08-15
description: สร้างตัวจัดการทรัพยากรแบบกำหนดเองใน C# เพื่อจัดการทรัพยากร HTML เช่น
  รูปภาพและ CSS เรียนรู้ HTMLLoadOptions, memory streams, และการโหลด HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: th
lastmod: 2026-08-15
og_description: สร้างตัวจัดการทรัพยากรแบบกำหนดเองใน C# เพื่อควบคุมการสตรีมทรัพยากร
  HTML บทเรียนนี้แสดงการตั้งค่า HTMLLoadOptions การจัดการ Memory Stream และการโหลด
  HTMLDocument ด้วยตรรกะแบบกำหนดเอง
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: สร้างตัวจัดการทรัพยากรแบบกำหนดเองใน C# – คู่มือเต็มสำหรับการจัดการทรัพยากร
  HTML
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: สร้างตัวจัดการทรัพยากรแบบกำหนดเองใน C# สำหรับการโหลด HTML
url: /th/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างตัวจัดการทรัพยากรแบบกำหนดเองใน C# สำหรับการโหลด HTML

หากคุณต้องการ **create custom resource handler** สำหรับไฟล์ HTML คำแนะนำนี้จะแสดงให้คุณเห็นอย่างละเอียด คุณจะได้เรียนรู้การดักจับรูปภาพ, CSS, และทรัพยากรอื่น ๆ ขณะโหลดเอกสาร HTML โดยใช้ `HTMLLoadOptions` และสตรีมที่อยู่ในหน่วยความจำ

บทแนะนำนี้ครอบคลุมทุกอย่างที่จำเป็นสำหรับการสร้างตัวจัดการที่ใช้ซ้ำได้, การกำหนดค่า load options, และการตรวจสอบว่าทรัพยากรถูกจับได้อย่างถูกต้อง ไม่ต้องอ้างอิงเอกสารภายนอก—เพียงโค้ดด้านล่างและคำอธิบายเท่านั้น

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า
- ความคุ้นเคยพื้นฐานกับ C#
- การอ้างอิงไลบรารีการประมวลผล HTML ที่ให้ `HTMLDocument`, `HtmlLoadOptions`, และ `ResourceHandler` (เช่น GroupDocs.Viewer for .NET)

## ภาพรวมของวิธีแก้

เราจะทำดังนี้:

1. **Create a custom resource handler** โดยสืบทอดจาก `ResourceHandler`
2. กำหนดค่า `HTMLLoadOptions` ให้ใช้ตัวจัดการนี้
3. โหลดไฟล์ HTML ด้วย `HTMLDocument` ขณะตัวจัดการให้สตรีมสำหรับแต่ละทรัพยากร
4. (ทางเลือก) เก็บทรัพยากรที่ได้รับลงดิสก์เพื่อยืนยันผล

แต่ละขั้นตอนจะมีโค้ดเต็มรูปแบบและเหตุผลที่อยู่เบื้องหลัง

## ขั้นตอนที่ 1: กำหนดคลาสตัวจัดการทรัพยากรแบบกำหนดเอง

การสร้างตัวจัดการแบบกำหนดเองหมายถึงการเขียนทับ `HandleResource` เพื่อให้ไลบรารีสามารถเขียนไบต์ของทรัพยากรลงสตรีมที่คุณควบคุมได้ การใช้ `MemoryStream` ทำให้ข้อมูลอยู่ในหน่วยความจำ ซึ่งเหมาะสำหรับการทดสอบหรือการประมวลผลต่อไป

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**ทำไมจึงสำคัญ:**  
การเขียนทับ `HandleResource` ให้คุณควบคุมเต็มที่ว่าข้อมูลทรัพยากรจะไปที่ไหน หากภายหลังคุณต้องแคชรูปภาพ, แปลง CSS, หรือบันทึกการใช้ทรัพยากร คุณสามารถเปลี่ยน `MemoryStream` เป็นสตรีมแบบกำหนดเองใด ๆ ก็ได้

## ขั้นตอนที่ 2: กำหนดค่า `HTMLLoadOptions` ให้ใช้ตัวจัดการ

`HTMLLoadOptions` ให้คุณเชื่อมต่อตัวจัดการเข้ากับ pipeline การโหลด การตั้งค่า `ResourceHandler` จะบอก viewer ให้เรียก `MyHandler` สำหรับทุก asset ภายนอก

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**ทำไมจึงสำคัญ:**  
หากไม่ได้กำหนด `ResourceHandler` viewer จะเขียนทรัพยากรไปยังตำแหน่งเริ่มต้น (มักเป็นโฟลเดอร์ชั่วคราว) การระบุตัวจัดการของคุณเองทำให้คุณ **create custom resource handler** พฤติกรรมที่สอดคล้องกับกลยุทธ์การจัดเก็บของแอปพลิเคชัน

## ขั้นตอนที่ 3: โหลดเอกสาร HTML ด้วยตัวเลือกที่กำหนดค่าแล้ว

ตอนนี้โหลดไฟล์ HTML ตัว viewer จะเรียก `MyHandler.HandleResource` สำหรับแต่ละทรัพยากรที่พบ

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

ในขั้นตอนนี้เนื้อหา HTML ถูกพาร์สและทรัพยากรภายนอกทั้งหมดถูกสตรีมเข้าสู่บัฟเฟอร์หน่วยความจำที่ `MyHandler` จัดหาให้

## ขั้นตอนที่ 4 (ทางเลือก): เข้าถึงทรัพยากรที่จับได้

หากต้องการตรวจสอบหรือบันทึกทรัพยากร คุณสามารถแก้ไข `MyHandler` ให้เก็บ `MemoryStream` แต่ละอันในดิกชันนารีโดยใช้ชื่อทรัพยากรเป็นคีย์

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

หลังจากโหลดเสร็จ คุณสามารถวนลูป `handler.Resources` และเขียนแต่ละไฟล์ลงดิสก์ได้:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**ทำไมจึงสำคัญ:**  
การเก็บทรัพยากรช่วยให้ทำการประมวลผลต่อ เช่น การเพิ่มประสิทธิภาพรูปภาพ, การย่อ CSS, หรือการเก็บสำรอง นอกจากนี้ยังเป็นการยืนยันอย่างเป็นรูปธรรมว่า logic **create custom resource handler** ทำงานตามที่คาดหวัง

## ขั้นตอนที่ 5: ทำความสะอาด

ทั้ง `HTMLDocument` และสตรีมใด ๆ ควรทำการ dispose เพื่อปล่อยทรัพยากรที่ไม่ได้จัดการ

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมที่รวมทุกขั้นตอนตั้งแต่การกำหนดคลาสจนถึงการสกัดทรัพยากร

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

คอนโซลจะแสดงรายการทรัพยากรแต่ละรายการที่ viewer สตรีมผ่านตัวจัดการของคุณ ยืนยันว่า workflow **create custom resource handler** สำเร็จ

## คำถามที่พบบ่อยและกรณีขอบ

| Question | Answer |
|----------|--------|
| *What if a resource is large (e.g., high‑resolution image)?* | แทนที่ `MemoryStream` ด้วย `FileStream` ที่ชี้ไปยังโฟลเดอร์ชั่วคราว เพื่อป้องกันการใช้หน่วยความจำมากเกินไป |
| *Can I filter resources by type?* | ภายใน `HandleResource` ตรวจสอบ `info.MimeType` หรือ `info.Extension` แล้วคืนค่า `null` สำหรับประเภทที่ไม่ต้องการ การคืนค่า `null` จะบอก viewer ให้ข้ามทรัพยากรนั้น |
| *Is thread safety required?* | หากใช้ instance ของตัวจัดการเดียวกันในหลายการโหลดพร้อมกัน ควรปกป้องดิกชันนารี `Resources` ด้วย lock หรือใช้คอลเลกชันแบบ concurrent |
| *How do I support relative URLs?* | `ResourceInfo` มี URL ดั้งเดิม คุณสามารถผสานกับ base path ของไฟล์ HTML เพื่อแก้ไข URL แบบ relative ก่อนบันทึก |

## สรุป

คุณได้เรียนรู้วิธี **create custom resource handler** ใน C# สำหรับการโหลด HTML, การกำหนดค่า `HTMLLoadOptions`, การจับทรัพยากรที่สตรีม, และการทำความสะอาดอย่างรับผิดชอบ รูปแบบนี้ให้คุณควบคุมการจัดการทรัพยากรได้เต็มที่ รองรับสถานการณ์เช่น การประมวลผลรูปภาพแบบเรียลไทม์, การเขียนทับ CSS, หรือการจัดเก็บอย่างปลอดภัย

ต่อไปให้สำรวจหัวข้อที่เกี่ยวข้องเช่น **HTMLDocument loading** ด้วยตัวเลือกการเรนเดอร์ต่าง ๆ, หรือขยายตัวจัดการให้เป็น **C# resource handler** ที่เขียนโดยตรงไปยังคลาวด์สตอเรจ ทดลองใช้เมธอด `HandleResource` ของตัวจัดการเพื่อให้ตรงกับ workflow ของโครงการของคุณ

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}