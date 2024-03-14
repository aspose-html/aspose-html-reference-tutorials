---
title: แปลง EPUB เป็น XPS ใน .NET ด้วย Aspose.HTML
linktitle: แปลง EPUB เป็น XPS ใน .NET
second_title: Aspose.HTML .NET API การจัดการ HTML
description: เรียนรู้วิธีแปลง EPUB เป็น XPS ใน .NET โดยใช้ Aspose.HTML สำหรับ .NET ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อการแปลงที่ง่ายดาย
type: docs
weight: 13
url: /th/net/html-extensions-and-conversions/convert-epub-to-xps/
---

คุณกำลังมองหาวิธีที่ราบรื่นในการแปลงไฟล์ EPUB เป็นรูปแบบ XPS ในแอปพลิเคชัน .NET ของคุณหรือไม่? Aspose.HTML สำหรับ .NET มอบโซลูชันที่มีประสิทธิภาพเพื่อให้บรรลุเป้าหมายนี้ได้อย่างง่ายดาย ในคำแนะนำทีละขั้นตอนนี้ เราจะแนะนำคุณตลอดขั้นตอนการแปลง EPUB เป็น XPS โดยใช้ Aspose.HTML มาเริ่มกันเลย!

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเจาะลึกกระบวนการแปลง EPUB เป็น XPS คุณจะต้องแน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

### 1. Aspose.HTML สำหรับ .NET Library

 ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Aspose.HTML สำหรับ .NET ในโปรเจ็กต์ของคุณ หากคุณยังไม่ได้ดำเนินการ คุณสามารถขอรับได้จาก[Aspose.HTML สำหรับหน้าดาวน์โหลด .NET](https://releases.aspose.com/html/net/).

### 2. อินพุตไฟล์ EPUB

คุณจะต้องมีไฟล์ EPUB ที่ต้องการแปลงเป็น XPS ตรวจสอบให้แน่ใจว่าคุณมีไฟล์ EPUB ที่พร้อมสำหรับการแปลง

### 3. สภาพแวดล้อมการพัฒนา .NET

คู่มือนี้ถือว่าคุณได้ตั้งค่าสภาพแวดล้อมการพัฒนา .NET ที่ใช้งานได้บนเครื่องของคุณ

## นำเข้าเนมสเปซ

ในการเริ่มต้น คุณควรนำเข้าเนมสเปซที่จำเป็นสำหรับ Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## แปลง EPUB เป็น XPS

เรามาแจกแจงขั้นตอนการแปลงไฟล์ EPUB เป็นรูปแบบ XPS ออกเป็นหลายขั้นตอนกัน

### ขั้นตอนที่ 1.1: เปิดไฟล์ EPUB

ขั้นแรก ให้เปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่านโดยใช้ FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // ดำเนินการต่อด้วยกระบวนการแปลง
}
```

### ขั้นตอนที่ 1.2: สร้าง XpsSaveOptions

สร้างอินสแตนซ์ของ XpsSaveOptions ขั้นตอนนี้มีความสำคัญอย่างยิ่งในการกำหนดค่าเอาต์พุต XPS:

```csharp
var options = new XpsSaveOptions();
```

### ขั้นตอนที่ 1.3: แปลง EPUB เป็น XPS

ตอนนี้ เรามาเรียกเมธอด ConvertEPUB เพื่อแปลง EPUB เป็น XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## ระบุตัวเลือก XPS แบบกำหนดเอง

คุณสามารถปรับแต่งเอาต์พุต XPS เพิ่มเติมได้โดยการระบุตัวเลือกแบบกำหนดเอง เช่น ขนาดหน้าและสีพื้นหลัง

### ขั้นตอนที่ 2.1: ขนาดหน้าแบบกำหนดเองและสีพื้นหลัง

สร้างอินสแตนซ์ของ XpsSaveOptions ด้วยขนาดหน้าและสีพื้นหลังที่กำหนดเอง:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### ขั้นตอนที่ 2.2: แปลง EPUB เป็น XPS ด้วยตัวเลือกแบบกำหนดเอง

ตอนนี้ ให้เรียกใช้เมธอด ConvertEPUB เพื่อแปลง EPUB เป็น XPS ด้วยตัวเลือกที่กำหนดเอง:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## ใช้ผู้ให้บริการสตรีมแบบกำหนดเอง

ในขั้นตอนนี้ เราจะแปลง EPUB เป็น XPS โดยใช้ผู้ให้บริการสตรีมแบบกำหนดเอง ซึ่งช่วยให้คุณสามารถจัดการข้อมูลผลลัพธ์ได้

### ขั้นตอนที่ 3.1: สร้าง MemoryStreamProvider

สร้างอินสแตนซ์ของ MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // ดำเนินการต่อด้วยกระบวนการแปลง
}
```

### ขั้นตอนที่ 3.2: แปลง EPUB เป็น XPS ด้วย Stream Provider

แปลง EPUB เป็น XPS โดยใช้ MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### ขั้นตอนที่ 3.3: เข้าถึงและบันทึกผลลัพธ์

ดึงสตรีมหน่วยความจำที่มีข้อมูลที่แปลงแล้วและบันทึกลงในไฟล์เอาต์พุต:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

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
ยินดีด้วย! คุณได้แปลงไฟล์ EPUB เป็นรูปแบบ XPS โดยใช้ Aspose.HTML สำหรับ .NET เรียบร้อยแล้ว

## บทสรุป

ในบทช่วยสอนที่ครอบคลุมนี้ เราได้สำรวจวิธีใช้ประโยชน์จาก Aspose.HTML สำหรับ .NET เพื่อแปลงไฟล์ EPUB เป็นรูปแบบ XPS ด้วยตัวเลือกการปรับแต่งที่หลากหลาย ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น Aspose.HTML จะทำให้กระบวนการง่ายขึ้น ช่วยให้คุณสามารถจัดการการแปลง EPUB เป็น XPS ได้อย่างง่ายดาย

 มีคำถามหรือพบปัญหาหรือไม่? ตรวจสอบ[เอกสาร Aspose.HTML](https://reference.aspose.com/html/net/) สำหรับข้อมูลเชิงลึกเพิ่มเติมหรือขอความช่วยเหลือจาก[ฟอรั่มชุมชน Aspose.HTML](https://forum.aspose.com/).

## คำถามที่พบบ่อย

### Aspose.HTML สำหรับ .NET คืออะไร
Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยให้นักพัฒนาสามารถทำงานกับเอกสาร HTML, EPUB และ XPS ในแอปพลิเคชัน .NET

### ฉันจะดาวน์โหลด Aspose.HTML สำหรับ .NET ได้ที่ไหน
 คุณสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้จาก[หน้าดาวน์โหลด](https://releases.aspose.com/html/net/).

### มีการทดลองใช้ฟรีสำหรับ Aspose.HTML สำหรับ .NET หรือไม่
 ใช่ คุณสามารถทดลองใช้ฟรีได้จาก[ที่นี่](https://releases.aspose.com/).

### ฉันจะขอรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET ได้อย่างไร
 หากต้องการรับใบอนุญาตชั่วคราว โปรดไปที่[หน้าใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/).

### ฉันจะหาบทช่วยสอนและเอกสารประกอบเพิ่มเติมสำหรับ Aspose.HTML สำหรับ .NET ได้ที่ไหน
 สำรวจบทช่วยสอนที่หลากหลายและเอกสารประกอบโดยละเอียดเกี่ยวกับ[เอกสาร Aspose.HTML](https://reference.aspose.com/html/net/) หน้าหนังสือ.