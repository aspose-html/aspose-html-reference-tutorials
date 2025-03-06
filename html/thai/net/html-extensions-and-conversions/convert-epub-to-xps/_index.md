---
title: แปลง EPUB เป็น XPS ใน .NET ด้วย Aspose.HTML
linktitle: แปลง EPUB เป็น XPS ใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: เรียนรู้วิธีการแปลง EPUB เป็น XPS ใน .NET โดยใช้ Aspose.HTML สำหรับ .NET ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อการแปลงที่ง่ายดาย
weight: 13
url: /th/net/html-extensions-and-conversions/convert-epub-to-xps/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง EPUB เป็น XPS ใน .NET ด้วย Aspose.HTML


คุณกำลังมองหาวิธีแปลงไฟล์ EPUB เป็นรูปแบบ XPS ในแอปพลิเคชัน .NET ของคุณอย่างราบรื่นอยู่หรือไม่ Aspose.HTML สำหรับ .NET นำเสนอโซลูชันอันทรงพลังที่ช่วยให้คุณบรรลุเป้าหมายดังกล่าวได้อย่างง่ายดาย ในคู่มือทีละขั้นตอนนี้ เราจะแนะนำคุณเกี่ยวกับกระบวนการแปลง EPUB เป็น XPS โดยใช้ Aspose.HTML มาเริ่มกันเลย!

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มกระบวนการแปลง EPUB เป็น XPS คุณต้องแน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

### 1. Aspose.HTML สำหรับไลบรารี .NET

 ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Aspose.HTML สำหรับ .NET ไว้ในโปรเจ็กต์ของคุณแล้ว หากยังไม่ได้ติดตั้ง คุณสามารถดาวน์โหลดได้จาก[หน้าดาวน์โหลด Aspose.HTML สำหรับ .NET](https://releases.aspose.com/html/net/).

### 2. อินพุตไฟล์ EPUB

คุณจะต้องมีไฟล์ EPUB ที่ต้องการแปลงเป็น XPS ตรวจสอบว่าคุณมีไฟล์ EPUB ที่พร้อมสำหรับการแปลงหรือไม่

### 3. สภาพแวดล้อมการพัฒนา .NET

คู่มือนี้จะถือว่าคุณมีการตั้งค่าสภาพแวดล้อมการพัฒนา .NET ที่ทำงานอยู่บนเครื่องของคุณแล้ว

## นำเข้าเนมสเปซ

ในการเริ่มต้น คุณควรนำเข้าเนมสเปซที่จำเป็นสำหรับ Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## แปลง EPUB เป็น XPS

มาแบ่งขั้นตอนการแปลงไฟล์ EPUB เป็นรูปแบบ XPS ออกเป็นหลายขั้นตอนกัน

### ขั้นตอนที่ 1.1: เปิดไฟล์ EPUB

ขั้นแรก เปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่านโดยใช้ FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // ดำเนินการต่อด้วยกระบวนการแปลง
}
```

### ขั้นตอนที่ 1.2: สร้าง XpsSaveOptions

สร้างอินสแตนซ์ของ XpsSaveOptions ขั้นตอนนี้มีความสำคัญต่อการกำหนดค่าเอาต์พุต XPS:

```csharp
var options = new XpsSaveOptions();
```

### ขั้นตอนที่ 1.3: แปลง EPUB เป็น XPS

ตอนนี้เรามาเรียกใช้เมธอด ConvertEPUB เพื่อแปลง EPUB เป็น XPS กัน:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## ระบุตัวเลือก XPS ที่กำหนดเอง

คุณสามารถปรับแต่งเอาต์พุต XPS เพิ่มเติมได้โดยระบุตัวเลือกที่กำหนดเอง เช่น ขนาดหน้าและสีพื้นหลัง

### ขั้นตอนที่ 2.1: ขนาดหน้าที่กำหนดเองและสีพื้นหลัง

สร้างอินสแตนซ์ของ XpsSaveOptions ด้วยขนาดหน้าและสีพื้นหลังแบบกำหนดเอง:

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

### ขั้นตอนที่ 2.2: แปลง EPUB เป็น XPS ด้วยตัวเลือกที่กำหนดเอง

ตอนนี้เรียกใช้เมธอด ConvertEPUB เพื่อแปลง EPUB เป็น XPS ด้วยตัวเลือกแบบกำหนดเอง:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## ใช้ผู้ให้บริการสตรีมแบบกำหนดเอง

ในขั้นตอนนี้ เราจะแปลง EPUB เป็น XPS โดยใช้ผู้ให้บริการสตรีมแบบกำหนดเอง ทำให้คุณสามารถจัดการข้อมูลที่ได้

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

ดึงข้อมูลสตรีมหน่วยความจำที่มีข้อมูลที่แปลงแล้วและบันทึกลงในไฟล์เอาต์พุต:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

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
ขอแสดงความยินดี! คุณได้แปลงไฟล์ EPUB เป็นรูปแบบ XPS โดยใช้ Aspose.HTML สำหรับ .NET สำเร็จแล้ว

## บทสรุป

ในบทช่วยสอนที่ครอบคลุมนี้ เราได้สำรวจวิธีใช้ประโยชน์จาก Aspose.HTML สำหรับ .NET เพื่อแปลงไฟล์ EPUB เป็นรูปแบบ XPS ด้วยตัวเลือกการปรับแต่งต่างๆ ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น Aspose.HTML จะทำให้กระบวนการนี้ง่ายขึ้น ช่วยให้คุณจัดการการแปลง EPUB เป็น XPS ได้อย่างง่ายดาย

 มีคำถามหรือพบปัญหาหรือไม่? ลองดู[เอกสารประกอบ Aspose.HTML](https://reference.aspose.com/html/net/) หากต้องการข้อมูลเชิงลึกเพิ่มเติมหรือขอความช่วยเหลือจาก[ฟอรั่มชุมชน Aspose.HTML](https://forum.aspose.com/).

## คำถามที่พบบ่อย

### Aspose.HTML สำหรับ .NET คืออะไร?
Aspose.HTML สำหรับ .NET เป็นไลบรารีอันทรงพลังที่ช่วยให้นักพัฒนาสามารถทำงานกับเอกสาร HTML, EPUB และ XPS ในแอปพลิเคชัน .NET ได้

### ฉันสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้ที่ไหน
 คุณสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้จาก[หน้าดาวน์โหลด](https://releases.aspose.com/html/net/).

### มี Aspose.HTML สำหรับ .NET ให้ทดลองใช้งานฟรีหรือไม่
 ใช่ คุณสามารถรับการทดลองใช้ฟรีได้จาก[ที่นี่](https://releases.aspose.com/).

### ฉันจะรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET ได้อย่างไร
 หากต้องการรับใบอนุญาตชั่วคราว โปรดไปที่[หน้าใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/).

### ฉันสามารถหาบทช่วยสอนและเอกสารประกอบเพิ่มเติมสำหรับ Aspose.HTML สำหรับ .NET ได้จากที่ไหน
 สำรวจบทช่วยสอนที่หลากหลายและเอกสารรายละเอียดเกี่ยวกับ[เอกสารประกอบ Aspose.HTML](https://reference.aspose.com/html/net/) หน้าหนังสือ.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
