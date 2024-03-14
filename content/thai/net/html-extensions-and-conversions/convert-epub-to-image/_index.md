---
title: แปลง EPUB เป็นรูปภาพใน .NET ด้วย Aspose.HTML
linktitle: แปลง EPUB เป็นรูปภาพใน .NET
second_title: Aspose.HTML .NET API การจัดการ HTML
description: เรียนรู้วิธีแปลง EPUB เป็นรูปภาพโดยใช้ Aspose.HTML สำหรับ .NET บทช่วยสอนทีละขั้นตอนพร้อมตัวอย่างโค้ดและตัวเลือกที่ปรับแต่งได้
type: docs
weight: 11
url: /th/net/html-extensions-and-conversions/convert-epub-to-image/
---

ในยุคดิจิทัลปัจจุบัน ความสามารถในการจัดการและแปลงรูปแบบเอกสารต่างๆ ถือเป็นทักษะที่มีคุณค่า Aspose.HTML สำหรับ .NET เป็นเครื่องมืออันทรงพลังที่ช่วยให้นักพัฒนาทำงานกับเอกสาร HTML และ EPUB ได้อย่างง่ายดาย ในบทช่วยสอนนี้ เราจะเจาะลึกโลกของ Aspose.HTML สำหรับ .NET และแนะนำคุณตลอดกระบวนการแปลงเอกสาร EPUB เป็นรูปแบบรูปภาพต่างๆ เราจะแบ่งแต่ละตัวอย่างออกเป็นหลายขั้นตอน โดยอธิบายทุกขั้นตอนตลอดการทำงาน

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะดำดิ่งสู่โลกของ Aspose.HTML สำหรับ .NET คุณควรตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio ในระบบของคุณ คุณสามารถดาวน์โหลดได้จากเว็บไซต์

2.  Aspose.HTML สำหรับ .NET: คุณสามารถรับไลบรารีได้จากเว็บไซต์ Aspose[ที่นี่](https://releases.aspose.com/html/net/).

3. ไดเร็กทอรีข้อมูลของคุณ: เตรียมไดเร็กทอรีที่คุณจัดเก็บไฟล์ EPUB และตำแหน่งที่จะบันทึกอิมเมจเอาต์พุต

4. ความรู้พื้นฐานของ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# เป็นสิ่งสำคัญในการทำความเข้าใจและนำตัวอย่างโค้ดที่ให้ไว้ในบทช่วยสอนนี้ไปใช้

## การนำเข้าเนมสเปซที่จำเป็น

ก่อนที่เราจะเริ่มทำงานกับ Aspose.HTML สำหรับ .NET คุณต้องนำเข้าเนมสเปซที่จำเป็นลงในโค้ด C# ของคุณ เนมสเปซเหล่านี้ให้การเข้าถึงคุณสมบัติ Aspose.HTML สำหรับ .NET

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

ตอนนี้เรามีข้อกำหนดเบื้องต้นและเนมสเปซแล้ว มาดูตัวอย่างทีละขั้นตอนกันดีกว่า

## แปลง EPUB เป็น JPEG

```csharp
    string dataDir = "Your Data Directory";
    // เปิดไฟล์ EPUB ที่มีอยู่เพื่ออ่าน
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // เรียกใช้เมธอด ConvertEPUB เพื่อแปลงไฟล์ EPUB เป็นรูปภาพ
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### ขั้นตอน

1. ระบุเส้นทางไปยังไฟล์ EPUB ของคุณในตัวแปร dataDir
2. เปิดไฟล์ EPUB เพื่ออ่านโดยใช้ FileStream
3. เรียกใช้เมธอด ConvertEPUB โดยส่งสตรีม EPUB, ImageSaveOptions ที่ระบุรูปแบบเอาต์พุต (JPEG) และชื่อไฟล์เอาต์พุต ("output.jpg")
5. ไฟล์ EPUB จะถูกแปลงเป็นภาพ JPEG

ในตัวอย่างนี้ เราเปิดไฟล์ EPUB อ่านเนื้อหา และแปลงเป็นรูปแบบภาพ JPEG รูปภาพเอาต์พุตจะถูกบันทึกเป็น "output.jpg"

## แปลง EPUB เป็น PNG

คุณสามารถแปลงไฟล์ EPUB เป็นรูปแบบภาพต่างๆ เช่น PNG, BMP, GIF และ TIFF ได้อย่างง่ายดายโดยใช้โครงสร้างโค้ดที่คล้ายกัน นี่คือตัวอย่างสำหรับการแปลงเป็น PNG:

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### ขั้นตอน
1. เปิดไฟล์ EPUB เพื่ออ่านโดยใช้ FileStream
2. เริ่มต้นวัตถุ ImageSaveOptions ด้วยรูปแบบเอาต์พุตที่ต้องการ (ในกรณีนี้คือ PNG)
3. เรียกใช้เมธอด ConvertEPUB โดยส่งกระแสข้อมูล EPUB ตัวเลือกการบันทึกรูปภาพ และชื่อไฟล์เอาต์พุต
4. ไฟล์ EPUB จะถูกแปลงเป็นรูปแบบภาพที่ระบุ

## ระบุตัวเลือกการบันทึกรูปภาพ

คุณสามารถปรับแต่งเอาท์พุตรูปภาพได้โดยการระบุตัวเลือก เช่น ขนาดหน้าและสีพื้นหลัง นี่คือตัวอย่าง:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### ขั้นตอน

1.  ระบุเส้นทางไปยังไฟล์ EPUB ของคุณในรูปแบบ`dataDir` ตัวแปร.
2.  เปิดไฟล์ EPUB เพื่ออ่านโดยใช้ไฟล์`FileStream`.
3.  สร้าง`ImageSaveOptions` object และระบุรูปแบบเอาต์พุตที่ต้องการ (JPEG)
4. ปรับแต่งขนาดหน้าและสีพื้นหลังหากจำเป็น
5.  โทรหา`ConvertEPUB`วิธีการส่งสตรีม EPUB ตัวเลือกการบันทึกรูปภาพ และชื่อไฟล์เอาต์พุต
6. ไฟล์ EPUB จะถูกแปลงเป็นรูปภาพด้วยตัวเลือกที่ระบุ

## ระบุผู้ให้บริการสตรีมแบบกำหนดเอง

หากคุณต้องการจัดการสตรีมเอาต์พุต คุณสามารถใช้ผู้ให้บริการสตรีมแบบกำหนดเองได้ นี่คือตัวอย่าง:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
ซอร์สโค้ดคลาส MemoryStreamProvider

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

### ขั้นตอน
1.  ระบุเส้นทางไปยังไฟล์ EPUB ของคุณในรูปแบบ`dataDir` ตัวแปร.
2.  เปิดไฟล์ EPUB เพื่ออ่านโดยใช้ไฟล์`FileStream`.
3.  สร้างก`MemoryStreamProvider` เพื่อจัดการสตรีมเอาต์พุตแบบกำหนดเอง
4.  โทรหา`ConvertEPUB` วิธีการส่งผ่านสตรีม EPUB ตัวเลือกการบันทึกรูปภาพ (JPEG) และผู้ให้บริการสตรีมแบบกำหนดเอง
5. วนซ้ำสตรีมหน่วยความจำในผู้ให้บริการแบบกำหนดเอง บันทึกลงในไฟล์แต่ละไฟล์
6. ตัวอย่างนี้ช่วยให้คุณสามารถจัดการและบันทึกสตรีมเอาต์พุตหลายรายการได้ตามต้องการ

## บทสรุป

Aspose.HTML สำหรับ .NET เป็นไลบรารีอเนกประสงค์ที่ช่วยลดความยุ่งยากในการทำงานกับเอกสาร EPUB และ HTML ด้วยความสามารถในการแปลงเอกสาร EPUB เป็นรูปแบบภาพต่างๆ และตัวเลือกที่ปรับแต่งได้ ทำให้มีแอพพลิเคชั่นมากมายสำหรับนักพัฒนา

---

## คำถามที่พบบ่อย

### 1. ฉันจะดาวน์โหลด Aspose.HTML สำหรับ .NET ได้ที่ไหน

 คุณสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้จากหน้าเผยแพร่[ที่นี่](https://releases.aspose.com/html/net/).

### 2. ฉันจะรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET ได้อย่างไร

 หากต้องการขอรับใบอนุญาตชั่วคราว โปรดไปที่หน้าใบอนุญาตชั่วคราว[ที่นี่](https://purchase.aspose.com/temporary-license/).

### 3. ฉันจะรับการสนับสนุนเพิ่มเติมสำหรับ Aspose.HTML สำหรับ .NET ได้ที่ไหน

 หากมีคำถามหรือปัญหา คุณสามารถขอความช่วยเหลือจากชุมชน Aspose บนฟอรัมการสนับสนุน[ที่นี่](https://forum.aspose.com/).

### 4. ฉันสามารถแปลงเอกสาร EPUB เป็นรูปแบบอื่น เช่น PDF หรือ XPS ได้หรือไม่

ได้ คุณสามารถใช้ Aspose.HTML สำหรับ .NET เพื่อแปลงเอกสาร EPUB เป็นรูปแบบต่างๆ รวมถึง PDF และ XPS

### 5. Aspose.HTML สำหรับ .NET เหมาะสำหรับโครงการทั้งขนาดเล็กและขนาดใหญ่หรือไม่

อย่างแน่นอน! Aspose.HTML สำหรับ .NET ได้รับการออกแบบมาให้สามารถปรับขนาดได้ ทำให้เป็นตัวเลือกที่ยอดเยี่ยมสำหรับโครงการทุกขนาด
