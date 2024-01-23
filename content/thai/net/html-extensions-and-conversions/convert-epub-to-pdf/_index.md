---
title: แปลง EPUB เป็น PDF ใน .NET ด้วย Aspose.HTML
linktitle: แปลง EPUB เป็น PDF ใน .NET
second_title: Aspose.HTML .NET API การจัดการ HTML
description: เรียนรู้วิธีแปลง EPUB เป็น PDF โดยใช้ Aspose.HTML สำหรับ .NET คำแนะนำทีละขั้นตอนนี้ครอบคลุมตัวเลือกการปรับแต่ง คำถามที่พบบ่อย และอื่นๆ อีกมากมายสำหรับการแปลงเอกสารได้อย่างราบรื่น
type: docs
weight: 12
url: /th/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

ในบทช่วยสอนนี้ เราจะสำรวจวิธีใช้ Aspose.HTML สำหรับ .NET เพื่อแปลงไฟล์ EPUB เป็น PDF Aspose.HTML เป็นไลบรารี .NET ที่ทรงพลังซึ่งมีฟังก์ชันการทำงานที่หลากหลายสำหรับการทำงานกับเอกสาร HTML และ EPUB เราจะครอบคลุมข้อกำหนดเบื้องต้น นำเข้าเนมสเปซที่จำเป็น และแจกแจงตัวอย่างหลายรายการ โดยอธิบายแต่ละขั้นตอนโดยละเอียด

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

1. Aspose.HTML สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Aspose.HTML สำหรับ .NET ในโปรเจ็กต์ .NET ของคุณ คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.aspose.com/html/net/).

2. ไดเร็กทอรีข้อมูลของคุณ: คุณจะต้องมีไดเร็กทอรีข้อมูลที่จัดเก็บไฟล์ EPUB ของคุณ

ตอนนี้ เรามาเจาะลึกกระบวนการทีละขั้นตอนในการแปลง EPUB เป็น PDF โดยใช้ Aspose.HTML สำหรับ .NET

## แปลง EPUB เป็น PDF

### ขั้นตอนที่ 1: เริ่มต้นโครงการของคุณ

ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าโปรเจ็กต์ .NET และติดตั้ง Aspose.HTML สำหรับ .NET แล้ว

### ขั้นตอนที่ 2: นำเข้าเนมสเปซที่จำเป็น

ในไฟล์โค้ด C# ของคุณ ให้นำเข้าเนมสเปซที่จำเป็น:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### ขั้นตอนที่ 3: เปิดไฟล์ EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // ไปยังขั้นตอนต่อไป...
}
```

-  แทนที่`"Your Data Directory"` ด้วยไดเร็กทอรีจริงที่มีไฟล์ EPUB ของคุณอยู่
- รหัสนี้จะเปิดไฟล์ EPUB เพื่ออ่าน

### ขั้นตอนที่ 4: ตั้งค่าตัวเลือก PDF และทำการแปลง

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  สร้างอินสแตนซ์ของ`PdfSaveOptions` เพื่อระบุการตั้งค่าการแปลง PDF
-  ใช้`Converter.ConvertEPUB` วิธีการแปลง EPUB เป็น PDF ด้วยตัวเลือกที่กำหนด
- บันทึก PDF ที่ได้เป็น "output.pdf"

## ระบุตัวเลือกการบันทึก PDF

### ขั้นตอนที่ 1: เริ่มต้นโครงการของคุณ

ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าโปรเจ็กต์ .NET และติดตั้ง Aspose.HTML สำหรับ .NET แล้ว

### ขั้นตอนที่ 2: นำเข้าเนมสเปซที่จำเป็น

นำเข้าเนมสเปซที่จำเป็นในรหัส C# ของคุณ:

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
    // ไปยังขั้นตอนต่อไป...
}
```

-  แทนที่`"Your Data Directory"` ด้วยไดเร็กทอรีที่แท้จริงของไฟล์ EPUB ของคุณ
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
- ในตัวอย่างนี้ เราตั้งค่าขนาดหน้าเป็นความกว้าง 3000 พิกเซลและความสูง 1,000 พิกเซล และสีพื้นหลังเป็น Alice Blue

### ขั้นตอนที่ 5: ทำการแปลง

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  ใช้`Converter.ConvertEPUB` วิธีการแปลง EPUB เป็น PDF ด้วยตัวเลือกที่กำหนดเอง
- บันทึก PDF ที่ได้เป็น "output.pdf"

## ใช้ผู้ให้บริการสตรีมแบบกำหนดเอง

### ขั้นตอนที่ 1: เริ่มต้นโครงการของคุณ

ตั้งค่าโครงการ .NET และติดตั้ง Aspose.HTML สำหรับ .NET

### ขั้นตอนที่ 2: นำเข้าเนมสเปซที่จำเป็น

ในโค้ด C# ของคุณ ให้นำเข้าเนมสเปซที่จำเป็น:

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
    // ไปยังขั้นตอนต่อไป...
}
```

-  แทนที่`"Your Data Directory"` ด้วยไดเร็กทอรีที่แท้จริงของไฟล์ EPUB ของคุณ
- เปิดไฟล์ EPUB เพื่ออ่าน

### ขั้นตอนที่ 4: ใช้ผู้ให้บริการสตรีมแบบกำหนดเอง

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // ไปยังขั้นตอนต่อไป...
}
```

-  สร้างก`MemoryStreamProvider` เพื่อจัดการผลลัพธ์การแปลงเป็นสตรีมหน่วยความจำ
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
- สร้างไฟล์ PDF เอาท์พุตและคัดลอกเนื้อหาจากสตรีมหน่วยความจำไปยังไฟล์นั้น

### ซอร์สโค้ด Class MemoryStreamProvider 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // รายการออบเจ็กต์ MemoryStream ที่สร้างขึ้นระหว่างการเรนเดอร์เอกสาร
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // วิธีการนี้เรียกว่าเมื่อจำเป็นต้องใช้สตรีมเอาต์พุตเพียงรายการเดียว เช่น สำหรับรูปแบบ XPS, PDF หรือ TIFF
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // วิธีการนี้เรียกว่าเมื่อจำเป็นต้องมีการสร้างสตรีมเอาต์พุตหลายรายการ ตัวอย่างเช่นในระหว่างการเรนเดอร์ HTML ไปยังรายการไฟล์รูปภาพ (JPG, PNG ฯลฯ )
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // ที่นี่ คุณสามารถปล่อยสตรีมที่เต็มไปด้วยข้อมูลและล้างข้อมูลไปยังฮาร์ดไดรฟ์ได้
            }
            public void Dispose()
            {
                // การปล่อยทรัพยากร
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
ตอนนี้ คุณได้เรียนรู้วิธีแปลงไฟล์ EPUB เป็น PDF โดยใช้ Aspose.HTML สำหรับ .NET พร้อมด้วยตัวเลือกและการปรับแต่งที่หลากหลาย Aspose.HTML ทำให้กระบวนการง่ายขึ้น โดยให้ความยืดหยุ่นและควบคุมการแปลงเอกสารของคุณ

## บทสรุป

Aspose.HTML สำหรับ .NET เป็นเครื่องมืออเนกประสงค์สำหรับการแปลงไฟล์ EPUB เป็น PDF โดยเสนอตัวเลือกการปรับแต่งเพื่อปรับแต่งเอกสาร PDF ที่ได้ให้ตรงตามความต้องการของคุณ ไม่ว่าคุณจะต้องการการแปลงแบบธรรมดาหรือการปรับแต่งขั้นสูง Aspose.HTML ก็ครอบคลุมไว้แล้ว

 หากคุณยังไม่ได้ดาวน์โหลด คุณสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้จาก[เว็บไซต์](https://releases.aspose.com/html/net/) และเริ่มใช้งานในแอปพลิเคชัน .NET ของคุณวันนี้

---

## คำถามที่พบบ่อย

### Aspose.HTML สำหรับ .NET ใช้งานได้ฟรีหรือไม่
    Aspose.HTML สำหรับ .NET เป็นผลิตภัณฑ์เชิงพาณิชย์ แต่สามารถทดลองใช้ฟรีได้[ที่นี่](https://releases.aspose.com/).

### ฉันสามารถปรับแต่งลักษณะที่ปรากฏของ PDF ที่แปลงแล้วได้หรือไม่
   ได้ คุณสามารถปรับแต่งลักษณะที่ปรากฏของ PDF ได้โดยการปรับตัวเลือก เช่น ขนาดหน้าและสีพื้นหลัง ดังที่แสดงในตัวอย่างที่ 2

### ฉันจะรับการสนับสนุน Aspose.HTML สำหรับ .NET ได้อย่างไร
    คุณสามารถค้นหาการสนับสนุนและแหล่งข้อมูลได้ที่[ฟอรั่ม Aspose.HTML](https://forum.aspose.com/).

### มีรูปแบบอื่นที่ฉันสามารถแปลงด้วย Aspose.HTML สำหรับ .NET ได้หรือไม่
   ใช่ Aspose.HTML สำหรับ .NET รองรับรูปแบบเอกสารที่หลากหลาย รวมถึง HTML, EPUB และอื่นๆ

### Aspose.HTML สำหรับ ..NET เหมาะสำหรับการแปลงเอกสารขนาดใหญ่หรือไม่
   Aspose.HTML สำหรับ .NET ได้รับการออกแบบมาเพื่อรองรับการแปลงเอกสารขนาดใหญ่อย่างมีประสิทธิภาพ ทำให้เหมาะสำหรับแอปพลิเคชันที่หลากหลาย

