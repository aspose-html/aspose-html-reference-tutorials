---
title: ปรับแต่งตัวแปลงใน .NET ด้วย Aspose.HTML
linktitle: การปรับแต่งตัวแปลงใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: เรียนรู้วิธีการแปลง HTML เป็น PDF, XPS และรูปภาพด้วย Aspose.HTML สำหรับ .NET บทช่วยสอนแบบทีละขั้นตอนพร้อมตัวอย่างโค้ดและคำถามที่พบบ่อย
weight: 16
url: /th/net/advanced-features/fine-tuning-converters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ปรับแต่งตัวแปลงใน .NET ด้วย Aspose.HTML


## การแนะนำ

Aspose.HTML สำหรับ .NET เป็นไลบรารีอันทรงพลังที่ช่วยให้นักพัฒนาสามารถจัดการและแปลงเอกสาร HTML ในรูปแบบต่างๆ ไม่ว่าคุณจะต้องแปลง HTML เป็น PDF, XPS หรือรูปภาพ หรือดำเนินการงานอื่นๆ ที่เกี่ยวข้องกับ HTML Aspose.HTML ก็มีชุดเครื่องมืออันแข็งแกร่งที่จะช่วยให้คุณทำงานสำเร็จลุล่วงได้

ในบทช่วยสอนนี้ เราจะมาสำรวจฟีเจอร์สำคัญบางอย่างของ Aspose.HTML สำหรับ .NET และให้คำอธิบายทีละขั้นตอนสำหรับแต่ละตัวอย่าง เมื่ออ่านบทช่วยสอนนี้จบ คุณจะเข้าใจอย่างถ่องแท้ว่าจะใช้ Aspose.HTML สำหรับ .NET ในแอปพลิเคชัน .NET ของคุณอย่างไร

## ข้อกำหนดเบื้องต้น

ก่อนที่จะไปดูตัวอย่าง ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

-  Aspose.HTML สำหรับ .NET: คุณควรติดตั้งไลบรารี Aspose.HTML สำหรับ .NET คุณสามารถดาวน์โหลดได้จาก[ลิงค์ดาวน์โหลด](https://releases.aspose.com/html/net/).

-  ใบอนุญาตชั่วคราว (ทางเลือก): หากคุณไม่มีใบอนุญาตที่ถูกต้อง คุณสามารถขอใบอนุญาตชั่วคราวได้จาก[ที่นี่](https://purchase.aspose.com/temporary-license/).

ตอนนี้เราลองมาสำรวจกรณีการใช้งานทั่วไปบางกรณีด้วย Aspose.HTML สำหรับ .NET กัน

## นำเข้าเนมสเปซ

ในโค้ด C# ของคุณ เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็น:

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

ตัวอย่างนี้จะแปลงโค้ด HTML เป็นเอกสาร PDF คุณสามารถปรับแต่งโค้ด HTML และไฟล์เอาท์พุตตามต้องการ

## ตั้งค่าขนาดหน้ากระดาษแบบกำหนดเอง

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

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และระบุตัวเลือกและไฟล์เอาท์พุต

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้สาธิตวิธีการตั้งค่าขนาดหน้าแบบกำหนดเองให้กับเอกสาร PDF ที่ได้

## ปรับความละเอียด

### ขั้นตอนที่ 1: เตรียมโค้ด HTML และบันทึกลงในไฟล์

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

ตัวอย่างนี้แสดงให้เห็นวิธีปรับความละเอียดเมื่อเรนเดอร์ HTML เป็น PDF โดยพิจารณาถึงหน้าจอที่มีความละเอียดต่ำและความละเอียดสูง

## ระบุสีพื้นหลัง

### ขั้นตอนที่ 1: เตรียมโค้ด HTML และบันทึกลงในไฟล์

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

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และระบุตัวเลือกและไฟล์เอาท์พุต

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้สาธิตวิธีการระบุสีพื้นหลังเมื่อแปลง HTML เป็น PDF

## ตั้งค่าขนาดหน้ากระดาษด้านซ้ายและขวา

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

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และระบุตัวเลือกและไฟล์เอาท์พุต

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้แสดงวิธีตั้งค่าขนาดหน้าต่างๆ สำหรับหน้าซ้ายและขวาเมื่อแปลง HTML เป็น PDF

## ปรับขนาดหน้าให้เข้ากับเนื้อหา

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

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และระบุตัวเลือกและไฟล์เอาท์พุต

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้สาธิตวิธีปรับขนาดหน้าให้มีเนื้อหาที่กว้างที่สุดเมื่อแปลง HTML เป็น PDF

## ระบุสิทธิ์การเข้าถึง PDF

### ขั้นตอนที่ 1: เตรียมโค้ด HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ขั้นตอนที่ 3: สร้างตัวเลือกการเรนเดอร์ PDF พร้อมสิทธิ์อนุญาต

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และระบุตัวเลือกและไฟล์เอาท์พุต

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้สาธิตวิธีระบุการอนุญาตและการเข้ารหัสเมื่อแปลง HTML เป็น PDF ที่ได้รับการป้องกัน

## ระบุตัวเลือกเฉพาะรูปภาพ

### ขั้นตอนที่ 1: เตรียมโค้ด HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ขั้นตอนที่ 3: สร้างตัวเลือกการแสดงผลภาพ

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ภาพและระบุตัวเลือกและไฟล์เอาท์พุต

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML ลงในรูปภาพ

```csharp
document.RenderTo(device);
```

ตัวอย่างนี้สาธิตวิธีการแปลง HTML เป็นรูปภาพด้วยตัวเลือกการเรนเดอร์เฉพาะ เช่น รูปแบบ ความละเอียด และโหมดการปรับให้เรียบ

## ระบุตัวเลือกการเรนเดอร์ XPS

### ขั้นตอนที่ 1: เตรียมโค้ด HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### ขั้นตอนที่ 3: สร้างตัวเลือกการเรนเดอร์ XPS พร้อมขนาดหน้ากระดาษ

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

ตัวอย่างนี้แสดงวิธีการแปลง HTML เป็น XPS ด้วยขนาดหน้าแบบกำหนดเองและตัวเลือกการแสดงผล

## รวมเอกสาร HTML หลายฉบับเป็น PDF

### ขั้นตอนที่ 1: เตรียมโค้ด HTML สำหรับเอกสารหลายฉบับ

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### ขั้นตอนที่ 2: สร้างเอกสาร HTML ที่จะรวมเข้าด้วยกัน

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### ขั้นตอนที่ 3: เริ่มต้นโปรแกรมแสดงผล HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF สำหรับผลลัพธ์รวม

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### ขั้นตอนที่ 5: รวมเอกสาร HTML ลงใน PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

ตัวอย่างนี้สาธิตวิธีการรวมเอกสาร HTML หลายฉบับเป็นไฟล์ PDF เดียวโดยใช้ Aspose.HTML สำหรับ .NET

## ตั้งค่าการหมดเวลาการเรนเดอร์

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

### ขั้นตอนที่ 3: เริ่มต้นโปรแกรมแสดงผล HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### ขั้นตอนที่ 4: สร้างอุปกรณ์ PDF และตั้งเวลาการเรนเดอร์

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### ขั้นตอนที่ 5: เรนเดอร์ HTML เป็น PDF พร้อมหมดเวลา

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

ตัวอย่างนี้สาธิตวิธีการตั้งค่าเวลาหมดเวลาการเรนเดอร์เมื่อแปลง HTML เป็น PDF ซึ่งอาจเป็นประโยชน์เมื่อต้องจัดการกับเนื้อหาแบบไดนามิกหรือสคริปต์ที่รันเป็นเวลานาน

## บทสรุป

Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีความยืดหยุ่นซึ่งช่วยให้นักพัฒนาสามารถทำงานกับเอกสาร HTML ได้อย่างมีประสิทธิภาพ ในบทช่วยสอนนี้ เราได้กล่าวถึงตัวอย่างต่างๆ ตั้งแต่การแปลง HTML ขั้นพื้นฐานเป็น PDF ไปจนถึงฟีเจอร์ขั้นสูง เช่น ขนาดหน้าแบบกำหนดเอง ความละเอียด และการอนุญาตต่างๆ หากทำตามตัวอย่างเหล่านี้ คุณจะสามารถใช้ศักยภาพทั้งหมดของ Aspose.HTML สำหรับ .NET ในแอปพลิเคชัน .NET ของคุณได้

 หากคุณมีคำถามหรือต้องการความช่วยเหลือเพิ่มเติม โปรดอย่าลังเลที่จะเยี่ยมชม[ฟอรั่ม Aspose.HTML](https://forum.aspose.com/) เพื่อการสนับสนุนและคำแนะนำ

## คำถามที่พบบ่อย

### คำถามที่ 1 Aspose.HTML สำหรับ .NET คืออะไร
   
A1: Aspose.HTML สำหรับ .NET เป็นไลบรารี .NET ที่ช่วยให้นักพัฒนาสามารถจัดการและแปลงเอกสาร HTML ด้วยโปรแกรมได้ ไลบรารีนี้มีฟีเจอร์มากมายสำหรับการทำงานกับเนื้อหา HTML รวมถึงการแปลง HTML เป็น PDF, XPS และการแปลงรูปภาพ รวมถึงตัวเลือกการเรนเดอร์ขั้นสูง

### คำถามที่ 2 ฉันสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้ที่ไหน

 A2: คุณสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้จาก[ลิงค์ดาวน์โหลด](https://releases.aspose.com/html/net/).

### คำถามที่ 3 ฉันต้องมีใบอนุญาตเพื่อใช้ Aspose.HTML สำหรับ .NET หรือไม่?

A3: แม้ว่าคุณจะใช้ Aspose.HTML สำหรับ .NET ได้โดยไม่ต้องมีใบอนุญาต แต่ขอแนะนำให้รับใบอนุญาตสำหรับการใช้งานจริงเพื่อปลดล็อกคุณลักษณะทั้งหมดและลบลายน้ำหรือข้อจำกัดใดๆ

### คำถามที่ 4 ฉันจะปกป้องไฟล์ PDF ที่สร้างด้วย Aspose.HTML สำหรับ .NET ได้อย่างไร

A4: คุณสามารถระบุสิทธิ์ PDF และการตั้งค่าการเข้ารหัสเมื่อเรนเดอร์ HTML เป็น PDF โดยใช้ Aspose.HTML สำหรับ .NET ซึ่งจะช่วยให้คุณควบคุมได้ว่าใครสามารถเข้าถึงและแก้ไขไฟล์ PDF ที่ได้

### คำถามที่ 5 ฉันสามารถแปลง HTML เป็นรูปแบบอื่นเช่น XPS หรือรูปภาพได้หรือไม่

A5: ใช่ Aspose.HTML สำหรับ .NET รองรับการแปลง HTML เป็นรูปแบบต่างๆ รวมถึง PDF, XPS และรูปภาพ (เช่น JPEG) คุณสามารถปรับแต่งการตั้งค่าการแปลงเพื่อให้ตรงตามความต้องการเฉพาะของคุณได้
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
