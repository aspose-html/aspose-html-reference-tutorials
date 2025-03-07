---
title: แปลง EPUB เป็นรูปภาพใน .NET ด้วย Aspose.HTML
linktitle: แปลง EPUB เป็นรูปภาพใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: เรียนรู้วิธีการแปลง EPUB เป็นรูปภาพโดยใช้ Aspose.HTML สำหรับ .NET บทช่วยสอนแบบทีละขั้นตอนพร้อมตัวอย่างโค้ดและตัวเลือกที่ปรับแต่งได้
weight: 11
url: /th/net/html-extensions-and-conversions/convert-epub-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง EPUB เป็นรูปภาพใน .NET ด้วย Aspose.HTML


ในยุคดิจิทัลทุกวันนี้ ความสามารถในการจัดการและแปลงเอกสารในรูปแบบต่างๆ ถือเป็นทักษะที่มีค่า Aspose.HTML สำหรับ .NET เป็นเครื่องมืออันทรงพลังที่ช่วยให้นักพัฒนาสามารถทำงานกับเอกสาร HTML และ EPUB ได้อย่างง่ายดาย ในบทช่วยสอนนี้ เราจะเจาะลึกเข้าไปในโลกของ Aspose.HTML สำหรับ .NET และแนะนำคุณตลอดกระบวนการแปลงเอกสาร EPUB เป็นรูปแบบภาพต่างๆ เราจะแบ่งตัวอย่างแต่ละตัวอย่างออกเป็นหลายขั้นตอน และอธิบายแต่ละขั้นตอนไปพร้อมกัน

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกเข้าสู่โลกของ Aspose.HTML สำหรับ .NET คุณควรแน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio ไว้ในระบบของคุณแล้ว คุณสามารถดาวน์โหลดได้จากเว็บไซต์

2.  Aspose.HTML สำหรับ .NET: คุณสามารถรับไลบรารีได้จากเว็บไซต์ Aspose[ที่นี่](https://releases.aspose.com/html/net/).

3. ไดเร็กทอรีข้อมูลของคุณ: เตรียมไดเร็กทอรีที่คุณใช้จัดเก็บไฟล์ EPUB และที่ที่จะบันทึกรูปภาพเอาต์พุต

4. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# ถือเป็นสิ่งสำคัญในการทำความเข้าใจและนำตัวอย่างโค้ดที่ให้ไว้ในบทช่วยสอนนี้ไปใช้งาน

## การนำเข้าเนมสเปซที่จำเป็น

ก่อนที่เราจะเริ่มทำงานกับ Aspose.HTML สำหรับ .NET คุณต้องนำเข้าเนมสเปซที่จำเป็นลงในโค้ด C# ของคุณก่อน เนมสเปซเหล่านี้ช่วยให้เข้าถึงฟีเจอร์ Aspose.HTML สำหรับ .NET ได้

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

ตอนนี้เรามีข้อกำหนดเบื้องต้นและเนมสเปซแล้ว มาดูตัวอย่างทีละขั้นตอนกัน

## การแปลง EPUB เป็น JPEG

```csharp
    string dataDir = "Your Data Directory";
    // เปิดไฟล์ EPUB ที่มีอยู่เพื่อการอ่าน
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // เรียกใช้เมธอด ConvertEPUB เพื่อแปลงไฟล์ EPUB เป็นรูปภาพ
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### ขั้นตอน

1. ระบุเส้นทางไปยังไฟล์ EPUB ของคุณในตัวแปร dataDir
2. เปิดไฟล์ EPUB เพื่ออ่านโดยใช้ FileStream
3. เรียกใช้เมธอด ConvertEPUB โดยส่งสตรีม EPUB, ImageSaveOptions พร้อมระบุรูปแบบเอาต์พุต (JPEG) และชื่อไฟล์เอาต์พุต ("output.jpg")
5. ไฟล์ EPUB จะถูกแปลงเป็นภาพ JPEG

ในตัวอย่างนี้ เราจะเปิดไฟล์ EPUB อ่านเนื้อหา และแปลงไฟล์เป็นรูปแบบภาพ JPEG รูปภาพเอาต์พุตจะถูกบันทึกเป็น "output.jpg"

## การแปลง EPUB เป็น PNG

คุณสามารถแปลงไฟล์ EPUB เป็นรูปแบบภาพต่างๆ เช่น PNG, BMP, GIF และ TIFF ได้อย่างง่ายดายโดยใช้โครงสร้างโค้ดที่คล้ายกัน นี่คือตัวอย่างการแปลงเป็น PNG:

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
3. เรียกใช้เมธอด ConvertEPUB โดยส่งสตรีม EPUB ตัวเลือกการบันทึกภาพ และชื่อไฟล์เอาต์พุต
4. ไฟล์ EPUB จะถูกแปลงเป็นรูปแบบภาพที่ระบุ

## ระบุตัวเลือกการบันทึกภาพ

คุณสามารถปรับแต่งผลลัพธ์ของภาพได้โดยระบุตัวเลือกต่างๆ เช่น ขนาดหน้าและสีพื้นหลัง นี่คือตัวอย่าง:

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

1.  ระบุเส้นทางไปยังไฟล์ EPUB ของคุณใน`dataDir` ตัวแปร.
2.  เปิดไฟล์ EPUB เพื่ออ่านโดยใช้`FileStream`.
3.  สร้าง`ImageSaveOptions` วัตถุและระบุรูปแบบเอาต์พุตที่ต้องการ (JPEG)
4. ปรับแต่งขนาดหน้าและสีพื้นหลังหากจำเป็น
5.  โทรหา`ConvertEPUB`วิธีการส่งสตรีม EPUB ตัวเลือกการบันทึกภาพ และชื่อไฟล์เอาต์พุต
6. ไฟล์ EPUB จะถูกแปลงเป็นรูปภาพที่มีตัวเลือกตามที่ระบุ

## ระบุผู้ให้บริการสตรีมแบบกำหนดเอง

หากคุณจำเป็นต้องจัดการสตรีมเอาต์พุต คุณสามารถใช้ผู้ให้บริการสตรีมแบบกำหนดเองได้ นี่คือตัวอย่าง:

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
โค้ดต้นฉบับของคลาส MemoryStreamProvider

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

### ขั้นตอน
1.  ระบุเส้นทางไปยังไฟล์ EPUB ของคุณใน`dataDir` ตัวแปร.
2.  เปิดไฟล์ EPUB เพื่ออ่านโดยใช้`FileStream`.
3.  สร้าง`MemoryStreamProvider` เพื่อจัดการกับสตรีมเอาท์พุตแบบกำหนดเอง
4.  โทรหา`ConvertEPUB` วิธีการส่งสตรีม EPUB ตัวเลือกการบันทึกภาพ (JPEG) และผู้ให้บริการสตรีมแบบกำหนดเอง
5. ทำซ้ำผ่านสตรีมหน่วยความจำในผู้ให้บริการแบบกำหนดเอง บันทึกลงในไฟล์แต่ละรายการ
6. ตัวอย่างนี้ช่วยให้คุณสามารถจัดการและบันทึกสตรีมเอาต์พุตหลายรายการตามต้องการ

## บทสรุป

Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีความยืดหยุ่นสูงซึ่งช่วยลดความซับซ้อนในการทำงานกับเอกสาร EPUB และ HTML ด้วยความสามารถในการแปลงเอกสาร EPUB เป็นรูปแบบภาพต่างๆ และตัวเลือกที่ปรับแต่งได้ จึงทำให้มีแอปพลิเคชันมากมายสำหรับนักพัฒนา

---

## คำถามที่พบบ่อย

### 1. ฉันสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้ที่ไหน

 คุณสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้จากหน้าเผยแพร่[ที่นี่](https://releases.aspose.com/html/net/).

### 2. ฉันจะได้รับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET ได้อย่างไร

 หากต้องการรับใบอนุญาตชั่วคราว โปรดไปที่หน้าใบอนุญาตชั่วคราว[ที่นี่](https://purchase.aspose.com/temporary-license/).

### 3. ฉันสามารถค้นหาการสนับสนุนเพิ่มเติมสำหรับ Aspose.HTML สำหรับ .NET ได้จากที่ใด

 หากมีคำถามหรือปัญหาใดๆ คุณสามารถขอความช่วยเหลือจากชุมชน Aspose บนฟอรัมสนับสนุนได้[ที่นี่](https://forum.aspose.com/).

### 4. ฉันสามารถแปลงเอกสาร EPUB เป็นรูปแบบอื่นเช่น PDF หรือ XPS ได้หรือไม่

ใช่ คุณสามารถใช้ Aspose.HTML สำหรับ .NET เพื่อแปลงเอกสาร EPUB เป็นรูปแบบต่างๆ รวมทั้ง PDF และ XPS

### 5. Aspose.HTML สำหรับ .NET เหมาะกับโปรเจ็กต์ขนาดเล็กและขนาดใหญ่หรือไม่

แน่นอน! Aspose.HTML สำหรับ .NET ได้รับการออกแบบมาให้ปรับขนาดได้ ทำให้เป็นตัวเลือกที่ยอดเยี่ยมสำหรับโปรเจ็กต์ทุกขนาด

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
