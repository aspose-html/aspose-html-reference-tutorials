---
title: แปลง EPUB เป็น PDF ใน .NET ด้วย Aspose.HTML
linktitle: แปลง EPUB เป็น PDF ใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: เรียนรู้วิธีการแปลง EPUB เป็น PDF โดยใช้ Aspose.HTML สำหรับ .NET คำแนะนำทีละขั้นตอนนี้ครอบคลุมตัวเลือกการปรับแต่ง คำถามที่พบบ่อย และอื่นๆ สำหรับการแปลงเอกสารอย่างราบรื่น
weight: 12
url: /th/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง EPUB เป็น PDF ใน .NET ด้วย Aspose.HTML


ในบทช่วยสอนนี้ เราจะมาเรียนรู้วิธีใช้ Aspose.HTML สำหรับ .NET เพื่อแปลงไฟล์ EPUB เป็น PDF Aspose.HTML เป็นไลบรารี .NET ที่ทรงพลังซึ่งมีฟังก์ชันต่างๆ มากมายสำหรับการทำงานกับเอกสาร HTML และ EPUB เราจะครอบคลุมข้อกำหนดเบื้องต้น นำเข้าเนมสเปซที่จำเป็น และแยกตัวอย่างต่างๆ ออกมา พร้อมอธิบายแต่ละขั้นตอนอย่างละเอียด

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มต้น โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. Aspose.HTML สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Aspose.HTML สำหรับ .NET ไว้ในโปรเจ็กต์ .NET ของคุณแล้ว คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.aspose.com/html/net/).

2. ไดเร็กทอรีข้อมูลของคุณ: คุณจะต้องมีไดเร็กทอรีข้อมูลที่ใช้จัดเก็บไฟล์ EPUB ของคุณ

ตอนนี้เรามาดูกระบวนการทีละขั้นตอนในการแปลง EPUB เป็น PDF โดยใช้ Aspose.HTML สำหรับ .NET กัน

## แปลง EPUB เป็น PDF

### ขั้นตอนที่ 1: เริ่มต้นโครงการของคุณ

ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าโครงการ .NET และติดตั้ง Aspose.HTML สำหรับ .NET แล้ว

### ขั้นตอนที่ 2: นำเข้าเนมสเปซที่จำเป็น

ในไฟล์โค้ด C# ของคุณ ให้โหลดเนมสเปซที่จำเป็น:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### ขั้นตอนที่ 3: เปิดไฟล์ EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // ไปยังขั้นตอนถัดไป...
}
```

-  แทนที่`"Your Data Directory"` ด้วยไดเร็กทอรีจริงที่ไฟล์ EPUB ของคุณตั้งอยู่
- โค้ดนี้จะเปิดไฟล์ EPUB เพื่อการอ่าน

### ขั้นตอนที่ 4: ตั้งค่าตัวเลือก PDF และดำเนินการแปลง

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  สร้างอินสแตนซ์ของ`PdfSaveOptions` เพื่อระบุการตั้งค่าการแปลง PDF
-  ใช้`Converter.ConvertEPUB` วิธีการแปลง EPUB เป็น PDF ด้วยตัวเลือกที่กำหนดให้
- บันทึกไฟล์ PDF ผลลัพธ์เป็น "output.pdf"

## ระบุตัวเลือกการบันทึก PDF

### ขั้นตอนที่ 1: เริ่มต้นโครงการของคุณ

ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าโครงการ .NET และติดตั้ง Aspose.HTML สำหรับ .NET แล้ว

### ขั้นตอนที่ 2: นำเข้าเนมสเปซที่จำเป็น

นำเข้าเนมสเปซที่จำเป็นในโค้ด C# ของคุณ:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### ขั้นตอนที่ 3: เปิดไฟล์ EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // ไปยังขั้นตอนถัดไป...
}
```

-  แทนที่`"Your Data Directory"` ด้วยไดเร็กทอรีจริงของไฟล์ EPUB ของคุณ
- เปิดไฟล์ EPUB เพื่ออ่าน

### ขั้นตอนที่ 4: ปรับแต่งตัวเลือก PDF

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  สร้างอินสแตนซ์ของ`PdfSaveOptions` และปรับแต่งตามความต้องการของคุณ
- ในตัวอย่างนี้ เราตั้งค่าขนาดหน้าเป็นความกว้าง 3,000 พิกเซล และความสูง 1,000 พิกเซล และสีพื้นหลังเป็น Alice Blue

### ขั้นตอนที่ 5: ดำเนินการแปลง

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  ใช้`Converter.ConvertEPUB` วิธีการแปลง EPUB เป็น PDF ด้วยตัวเลือกแบบกำหนดเอง
- บันทึกไฟล์ PDF ผลลัพธ์เป็น "output.pdf"

## ใช้ผู้ให้บริการสตรีมแบบกำหนดเอง

### ขั้นตอนที่ 1: เริ่มต้นโครงการของคุณ

ตั้งค่าโครงการ .NET และติดตั้ง Aspose.HTML สำหรับ .NET

### ขั้นตอนที่ 2: นำเข้าเนมสเปซที่จำเป็น

ในโค้ด C# ของคุณ ให้โหลดเนมสเปซที่จำเป็น:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### ขั้นตอนที่ 3: เปิดไฟล์ EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // ไปยังขั้นตอนถัดไป...
}
```

-  แทนที่`"Your Data Directory"` ด้วยไดเร็กทอรีจริงของไฟล์ EPUB ของคุณ
- เปิดไฟล์ EPUB เพื่ออ่าน

### ขั้นตอนที่ 4: ใช้ผู้ให้บริการสตรีมแบบกำหนดเอง

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // ไปยังขั้นตอนถัดไป...
}
```

-  สร้าง`MemoryStreamProvider` เพื่อจัดการผลการแปลงเป็นสตรีมหน่วยความจำ
-  ใช้`Converter.ConvertEPUB` วิธีการกับผู้ให้บริการสตรีมแบบกำหนดเอง

### ขั้นตอนที่ 5: บันทึกผลลัพธ์

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- เข้าถึงสตรีมหน่วยความจำที่มีข้อมูลที่แปลงแล้ว
- ตั้งค่าตำแหน่งสตรีมไปที่จุดเริ่มต้น
- สร้างไฟล์ PDF เอาท์พุตและคัดลอกเนื้อหาจากสตรีมหน่วยความจำลงไป

### โค้ดต้นฉบับของคลาส MemoryStreamProvider 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // รายการของวัตถุ MemoryStream ที่ถูกสร้างระหว่างการเรนเดอร์เอกสาร
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // วิธีการนี้ถูกเรียกใช้เมื่อต้องการสตรีมเอาต์พุตเพียงสตรีมเดียว เช่น สำหรับรูปแบบ XPS, PDF หรือ TIFF
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // วิธีการนี้จะถูกเรียกใช้เมื่อจำเป็นต้องสร้างสตรีมเอาต์พุตหลายสตรีม เช่น ในระหว่างการเรนเดอร์ HTML ลงในรายการไฟล์รูปภาพ (JPG, PNG เป็นต้น)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // ที่นี่ คุณสามารถปล่อยสตรีมที่เต็มไปด้วยข้อมูลและล้างไปยังฮาร์ดไดรฟ์ได้
            }
            public void Dispose()
            {
                // การปล่อยทรัพยากร
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
ตอนนี้ คุณได้เรียนรู้วิธีการแปลงไฟล์ EPUB เป็น PDF โดยใช้ Aspose.HTML สำหรับ .NET พร้อมตัวเลือกและความสามารถในการปรับแต่งต่างๆ แล้ว Aspose.HTML ช่วยลดความยุ่งยากของกระบวนการ มอบความยืดหยุ่นและการควบคุมในการแปลงเอกสารของคุณ

## บทสรุป

Aspose.HTML สำหรับ .NET เป็นเครื่องมืออเนกประสงค์สำหรับการแปลงไฟล์ EPUB เป็น PDF โดยมีตัวเลือกการปรับแต่งเพื่อปรับแต่งเอกสาร PDF ที่ได้ให้เหมาะกับความต้องการของคุณ ไม่ว่าคุณจะต้องการการแปลงแบบง่ายๆ หรือการปรับแต่งขั้นสูง Aspose.HTML ก็ตอบโจทย์คุณได้

 หากคุณยังไม่ได้ดาวน์โหลด Aspose.HTML สำหรับ .NET ได้จาก[เว็บไซต์](https://releases.aspose.com/html/net/) และเริ่มใช้งานในแอพพลิเคชั่น .NET ของคุณวันนี้

---

## คำถามที่พบบ่อย

### Aspose.HTML สำหรับ .NET ใช้ได้ฟรีหรือไม่?
    Aspose.HTML สำหรับ .NET เป็นผลิตภัณฑ์เชิงพาณิชย์แต่มีรุ่นทดลองใช้งานฟรี[ที่นี่](https://releases.aspose.com/).

### ฉันสามารถปรับแต่งลักษณะที่ปรากฏของ PDF ที่แปลงแล้วได้หรือไม่
   ใช่ คุณสามารถปรับแต่งลักษณะที่ปรากฏของ PDF ได้โดยการปรับเปลี่ยนตัวเลือกเช่นขนาดหน้าและสีพื้นหลัง ดังที่แสดงในตัวอย่างที่ 2

### ฉันจะได้รับการสนับสนุนสำหรับ Aspose.HTML สำหรับ .NET ได้อย่างไร
    คุณสามารถค้นหาการสนับสนุนและทรัพยากรได้ที่[ฟอรั่ม Aspose.HTML](https://forum.aspose.com/).

### มีรูปแบบอื่นที่ฉันสามารถแปลงโดยใช้ Aspose.HTML สำหรับ .NET ได้หรือไม่
   ใช่ Aspose.HTML สำหรับ .NET รองรับรูปแบบเอกสารต่างๆ รวมถึง HTML, EPUB และอื่นๆ อีกมากมาย

### Aspose.HTML สำหรับ ..NET เหมาะสำหรับการแปลงเอกสารขนาดใหญ่หรือไม่
   Aspose.HTML สำหรับ .NET ได้รับการออกแบบมาเพื่อรองรับการแปลงเอกสารขนาดใหญ่อย่างมีประสิทธิภาพ จึงเหมาะกับแอพพลิเคชั่นที่หลากหลาย


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
