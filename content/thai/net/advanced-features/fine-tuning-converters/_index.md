---
title: การปรับแต่งตัวแปลงอย่างละเอียดใน .NET ด้วย Aspose.HTML
linktitle: ตัวแปลงการปรับแต่งแบบละเอียดใน .NET
second_title: Aspose.HTML .NET API การจัดการ HTML
description: เรียนรู้วิธีแปลง HTML เป็น PDF, XPS และรูปภาพด้วย Aspose.HTML สำหรับ .NET บทช่วยสอนทีละขั้นตอนพร้อมตัวอย่างโค้ดและคำถามที่พบบ่อย
type: docs
weight: 16
url: /th/net/advanced-features/fine-tuning-converters/
---

## การแนะนำ

Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยให้นักพัฒนาสามารถจัดการและแปลงเอกสาร HTML ในรูปแบบต่างๆ ได้ ไม่ว่าคุณจะต้องแปลง HTML เป็น PDF, XPS หรือรูปภาพ หรือทำงานอื่นๆ ที่เกี่ยวข้องกับ HTML Aspose.HTML ก็มีชุดเครื่องมือที่มีประสิทธิภาพเพื่อช่วยให้คุณทำงานสำเร็จได้

ในบทช่วยสอนนี้ เราจะสำรวจคุณสมบัติที่สำคัญบางประการของ Aspose.HTML สำหรับ .NET และให้คำอธิบายทีละขั้นตอนสำหรับแต่ละตัวอย่าง เมื่อสิ้นสุดบทช่วยสอนนี้ คุณจะมีความเข้าใจที่ชัดเจนเกี่ยวกับวิธีการใช้ Aspose.HTML สำหรับ .NET ในแอปพลิเคชัน .NET ของคุณ

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกตัวอย่างต่างๆ ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

-  Aspose.HTML สำหรับ .NET: คุณควรติดตั้งไลบรารี Aspose.HTML สำหรับ .NET คุณสามารถดาวน์โหลดได้จาก[ลิ้งค์ดาวน์โหลด](https://releases.aspose.com/html/net/).

- ใบอนุญาตชั่วคราว (ไม่บังคับ): หากคุณไม่มีใบอนุญาตที่ถูกต้อง คุณสามารถขอรับใบอนุญาตชั่วคราวได้จาก[ที่นี่](https://purchase.aspose.com/temporary-license/).

ตอนนี้ เรามาสำรวจกรณีการใช้งานทั่วไปบางส่วนกับ Aspose.HTML สำหรับ .NET กัน

## นำเข้าเนมสเปซ

ในโค้ด C# ของคุณ ให้เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็น:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## แปลง HTML เป็น PDF

### ขั้นตอนที่ 1: เตรียมโค้ด HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ขั้นตอนที่ 3: สร้างอุปกรณ์ PDF และระบุไฟล์เอาต์พุต

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### ขั้นตอนที่ 4: เรนเดอร์ HTML เป็น PDF

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้จะแปลงข้อมูลโค้ด HTML ให้เป็นเอกสาร PDF คุณสามารถปรับแต่งโค้ด HTML และไฟล์เอาท์พุตได้ตามต้องการ

## ตั้งค่าขนาดหน้าแบบกำหนดเอง

### ขั้นตอนที่ 1: เตรียมโค้ด HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ขั้นตอนที่ 3: สร้างตัวเลือกการเรนเดอร์ PDF

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และระบุตัวเลือกและไฟล์เอาต์พุต

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้สาธิตวิธีการตั้งค่าขนาดหน้าแบบกำหนดเองสำหรับเอกสาร PDF ที่ได้

## ปรับความละเอียด

### ขั้นตอนที่ 1: เตรียมโค้ด HTML และบันทึกเป็นไฟล์

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### ขั้นตอนที่ 3: สร้างตัวเลือกการเรนเดอร์ PDF สำหรับความละเอียดต่ำ

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และระบุตัวเลือกและไฟล์เอาต์พุตสำหรับความละเอียดต่ำ

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF สำหรับความละเอียดต่ำ

```csharp
document.RenderTo(device);
```

### ขั้นตอนที่ 6: สร้างตัวเลือกการเรนเดอร์ PDF สำหรับความละเอียดสูง

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### ขั้นตอนที่ 7: สร้างอุปกรณ์ PDF และระบุตัวเลือกและไฟล์เอาต์พุตสำหรับความละเอียดสูง

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### ขั้นตอนที่ 8: เรนเดอร์ HTML เป็น PDF เพื่อความละเอียดสูง

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้แสดงวิธีการปรับความละเอียดเมื่อเรนเดอร์ HTML เป็น PDF โดยพิจารณาทั้งหน้าจอที่มีความละเอียดสูงและต่ำ

## ระบุสีพื้นหลัง

### ขั้นตอนที่ 1: เตรียมโค้ด HTML และบันทึกเป็นไฟล์

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### ขั้นตอนที่ 3: เริ่มต้นตัวเลือกการเรนเดอร์ PDF ด้วยสีพื้นหลัง

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และระบุตัวเลือกและไฟล์เอาต์พุต

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้สาธิตวิธีการระบุสีพื้นหลังเมื่อแปลง HTML เป็น PDF

## ตั้งค่าขนาดหน้าซ้ายและขวา

### ขั้นตอนที่ 1: เตรียมโค้ด HTML

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ขั้นตอนที่ 3: สร้างตัวเลือกการเรนเดอร์ PDF ด้วยขนาดหน้าซ้ายและขวา

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และระบุตัวเลือกและไฟล์เอาต์พุต

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้แสดงวิธีตั้งค่าขนาดหน้าที่แตกต่างกันสำหรับหน้าซ้ายและขวาเมื่อแปลง HTML เป็น PDF

## ปรับขนาดหน้าเป็นเนื้อหา

### ขั้นตอนที่ 1: เตรียมโค้ด HTML

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ขั้นตอนที่ 3: สร้างตัวเลือกการเรนเดอร์ PDF

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และระบุตัวเลือกและไฟล์เอาต์พุต

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้สาธิตวิธีการปรับขนาดหน้าให้เป็นเนื้อหาที่กว้างที่สุดเมื่อแปลง HTML เป็น PDF

## ระบุการอนุญาต PDF

### ขั้นตอนที่ 1: เตรียมโค้ด HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ขั้นตอนที่ 3: สร้างตัวเลือกการเรนเดอร์ PDF พร้อมสิทธิ์

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และระบุตัวเลือกและไฟล์เอาต์พุต

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้สาธิตวิธีการระบุสิทธิ์และการเข้ารหัสเมื่อแปลง HTML เป็น PDF ที่มีการป้องกัน

## ระบุตัวเลือกเฉพาะรูปภาพ

### ขั้นตอนที่ 1: เตรียมโค้ด HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ขั้นตอนที่ 3: สร้างตัวเลือกการแสดงภาพ

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์รูปภาพและระบุตัวเลือกและไฟล์เอาต์พุต

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็นรูปภาพ

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้สาธิตวิธีการแปลง HTML เป็นรูปภาพด้วยตัวเลือกการเรนเดอร์เฉพาะ เช่น รูปแบบ ความละเอียด และโหมดการปรับให้เรียบ

## ระบุตัวเลือกการแสดงผล XPS

### ขั้นตอนที่ 1: เตรียมโค้ด HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ขั้นตอนที่ 3: สร้างตัวเลือกการแสดงผล XPS ด้วยขนาดหน้า

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ XPS และระบุตัวเลือกและไฟล์เอาต์พุต

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น XPS

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้แสดงวิธีแปลง HTML เป็น XPS ด้วยขนาดหน้าที่กำหนดเองและตัวเลือกการแสดงผล

## รวมเอกสาร HTML หลายรายการเป็น PDF

### ขั้นตอนที่ 1: เตรียมโค้ด HTML สำหรับเอกสารหลายชุด

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### ขั้นตอนที่ 2: สร้างเอกสาร HTML ที่จะรวม

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### ขั้นตอนที่ 3: เริ่มต้น HTML Renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF สำหรับเอาต์พุตที่ผสาน

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### ขั้นตอนที่ 5: รวมเอกสาร HTML ให้เป็น PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

ตัวอย่างนี้สาธิตวิธีการรวมเอกสาร HTML หลายชุดให้เป็นไฟล์ PDF ไฟล์เดียวโดยใช้ Aspose.HTML สำหรับ .NET

## ตั้งค่าการหมดเวลาการแสดงผล

### ขั้นตอนที่ 1: เตรียมโค้ด HTML ด้วย JavaScript

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ขั้นตอนที่ 3: เริ่มต้น HTML Renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และตั้งค่าการหมดเวลาการเรนเดอร์

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF ด้วยการหมดเวลา

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

ตัวอย่างนี้สาธิตวิธีตั้งค่าการหมดเวลาการเรนเดอร์เมื่อแปลง HTML เป็น PDF ซึ่งจะมีประโยชน์เมื่อต้องจัดการกับเนื้อหาไดนามิกหรือสคริปต์ที่ใช้เวลานาน

## บทสรุป

Aspose.HTML สำหรับ .NET เป็นไลบรารีอเนกประสงค์ที่ช่วยให้นักพัฒนาสามารถทำงานกับเอกสาร HTML ได้อย่างมีประสิทธิภาพ ในบทช่วยสอนนี้ เราได้กล่าวถึงตัวอย่างต่างๆ ตั้งแต่การแปลง HTML พื้นฐานเป็น PDF ไปจนถึงคุณลักษณะขั้นสูงเพิ่มเติม เช่น ขนาดหน้าที่กำหนดเอง ความละเอียด และการอนุญาต ด้วยการทำตามตัวอย่างเหล่านี้ คุณจะสามารถควบคุมศักยภาพของ Aspose.HTML สำหรับ .NET ในแอปพลิเคชัน .NET ของคุณได้อย่างเต็มที่

 หากคุณมีคำถามหรือต้องการความช่วยเหลือเพิ่มเติม อย่าลังเลที่จะเยี่ยมชม[Aspose.HTML ฟอรั่ม](https://forum.aspose.com/) สำหรับการสนับสนุนและคำแนะนำ

## คำถามที่พบบ่อย

### ไตรมาสที่ 1 Aspose.HTML สำหรับ .NET คืออะไร
   
คำตอบ 1: Aspose.HTML สำหรับ .NET คือไลบรารี .NET ที่ช่วยให้นักพัฒนาสามารถจัดการและแปลงเอกสาร HTML โดยทางโปรแกรม โดยนำเสนอคุณสมบัติที่หลากหลายสำหรับการทำงานกับเนื้อหา HTML รวมถึง HTML เป็น PDF, XPS และการแปลงรูปภาพ รวมถึงตัวเลือกการเรนเดอร์ขั้นสูง

### ไตรมาสที่ 2 ฉันจะดาวน์โหลด Aspose.HTML สำหรับ .NET ได้ที่ไหน

 A2: คุณสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้จากไฟล์[ลิ้งค์ดาวน์โหลด](https://releases.aspose.com/html/net/).

### ไตรมาสที่ 3 ฉันต้องมีใบอนุญาตเพื่อใช้ Aspose.HTML สำหรับ .NET หรือไม่

ตอบ 3: แม้ว่าคุณสามารถใช้ Aspose.HTML สำหรับ .NET ได้โดยไม่ต้องมีใบอนุญาต แต่ขอแนะนำให้ขอรับใบอนุญาตสำหรับการใช้งานจริงเพื่อปลดล็อกคุณลักษณะทั้งหมดและลบลายน้ำหรือข้อจำกัดใดๆ

### ไตรมาสที่ 4 ฉันจะป้องกันไฟล์ PDF ที่สร้างด้วย Aspose.HTML สำหรับ .NET ได้อย่างไร

A4: คุณสามารถระบุการอนุญาต PDF และการตั้งค่าการเข้ารหัสเมื่อแสดงผล HTML เป็น PDF โดยใช้ Aspose.HTML สำหรับ .NET สิ่งนี้ช่วยให้คุณควบคุมได้ว่าใครสามารถเข้าถึงและแก้ไขไฟล์ PDF ที่ได้

### คำถามที่ 5 ฉันสามารถแปลง HTML เป็นรูปแบบอื่น เช่น XPS หรือรูปภาพได้หรือไม่

A5: ใช่ Aspose.HTML สำหรับ .NET รองรับการแปลง HTML เป็นรูปแบบต่างๆ รวมถึง PDF, XPS และรูปภาพ (เช่น JPEG) คุณสามารถปรับแต่งการตั้งค่าการแปลงให้ตรงตามความต้องการเฉพาะของคุณได้