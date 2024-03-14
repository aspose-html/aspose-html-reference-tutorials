---
title: การสร้างเอกสาร HTML ใน .NET ด้วย Aspose.HTML
linktitle: การสร้างเอกสาร HTML ใน .NET
second_title: Aspose.HTML .NET API การจัดการ HTML
description: เรียนรู้วิธีสร้างเอกสาร HTML ใน .NET โดยใช้ Aspose.HTML ตั้งแต่เริ่มต้นหรือจาก URL บทช่วยสอนที่ครอบคลุมสำหรับนักพัฒนาเว็บ
type: docs
weight: 10
url: /th/net/working-with-html-documents/creating-a-document/
---

ในขอบเขตของการพัฒนาเว็บและการจัดการข้อมูล การมีเครื่องมือที่มีประสิทธิภาพในการสร้าง แก้ไข และทำงานกับเอกสาร HTML เป็นสิ่งที่ขาดไม่ได้ Aspose.HTML สำหรับ .NET เป็นหนึ่งในเครื่องมือที่ช่วยให้งานที่เกี่ยวข้องกับ HTML ของคุณง่ายขึ้น ในบทช่วยสอนที่ครอบคลุมนี้ เราจะสำรวจวิธีสร้างเอกสาร HTML โดยใช้ Aspose.HTML สำหรับ .NET ทีละขั้นตอน ก่อนที่เราจะเจาะลึกตัวอย่าง เรามากล่าวถึงข้อกำหนดเบื้องต้นบางประการกันก่อน

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มต้นการเดินทางนี้ ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio บนระบบของคุณ

2.  Aspose.HTML สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารี Aspose.HTML สำหรับ .NET คุณสามารถค้นหาลิงค์ดาวน์โหลด[ที่นี่](https://releases.aspose.com/html/net/).

3. ความรู้พื้นฐานของ C#: ทำความคุ้นเคยกับพื้นฐานภาษาการเขียนโปรแกรม C#

ตอนนี้เราได้ครอบคลุมข้อกำหนดเบื้องต้นแล้ว เรามาเริ่มต้นสร้างเอกสาร HTML กันดีกว่า

## การนำเข้าเนมสเปซ

ขั้นแรก คุณต้องนำเข้าเนมสเปซที่จำเป็นเพื่อใช้ Aspose.HTML ในโปรเจ็กต์ C# ของคุณ เพิ่มคำสั่งการใช้ต่อไปนี้ลงในไฟล์โค้ดของคุณ:

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## การสร้างเอกสาร SVG

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
    {
        // ดำเนินการกับเอกสาร SVG ที่นี่...
    }
}
```

 ในตัวอย่างนี้ เราสร้างเอกสาร SVG โดยระบุเนื้อหา SVG และ URL พื้นฐาน ที่`SVGDocument`คลาสจาก Aspose.HTML สำหรับ .NET ช่วยให้คุณสามารถจัดการเอกสาร SVG ได้อย่างง่ายดาย

## การสร้างเอกสาร HTML ตั้งแต่เริ่มต้น

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        // ดำเนินการกับเอกสาร HTML ที่นี่...
    }
}
```

 ตัวอย่างนี้สาธิตวิธีการสร้างเอกสาร HTML ตั้งแต่เริ่มต้น ที่`HTMLDocument` class จัดเตรียมพื้นที่ว่างสำหรับเนื้อหา HTML ของคุณ

## การสร้างเอกสาร HTML จากไฟล์ในเครื่อง

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        // ดำเนินการกับเอกสาร HTML ที่นี่...
    }
}
```

 หากคุณมีไฟล์ HTML ที่มีอยู่ในระบบภายในของคุณ คุณสามารถโหลดได้โดยใช้ไฟล์`HTMLDocument` คลาสดังที่แสดงในตัวอย่างนี้

## การสร้างเอกสาร HTML จาก URL ระยะไกล

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://your.site.com/"))
    {
        // ดำเนินการกับเอกสาร HTML ที่นี่...
    }
}
```

บางครั้งคุณอาจต้องทำงานกับเนื้อหา HTML ที่โฮสต์บนเซิร์ฟเวอร์ระยะไกล ตัวอย่างนี้สาธิตวิธีการสร้างเอกสาร HTML จาก URL ระยะไกล

## การสร้างเอกสาร HTML จาก URL ระยะไกล (ทางเลือก)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://your.site.com/")))
    {
        // ดำเนินการกับเอกสาร HTML ที่นี่...
    }
}
```

วิธีทางเลือกนี้ยังแสดงวิธีสร้างเอกสาร HTML จาก URL ระยะไกลโดยใช้ตัวสร้างอื่น

## การสร้างเอกสาร HTML จากเนื้อหา HTML

```csharp
static void FromHTML()
{
    using (var document = new HTMLDocument("<p>my first paragraph</p>", "."))
    {
        // ดำเนินการกับเอกสาร HTML ที่นี่...
    }
}
```

หากคุณมีเนื้อหา HTML ในรูปแบบสตริง คุณสามารถสร้างเอกสาร HTML ได้ ดังที่แสดงในตัวอย่างนี้

## การสร้างเอกสาร HTML จากสตรีม

```csharp
static void FromStream()
{
    using (MemoryStream mem = new MemoryStream())
    using (StreamWriter sw = new StreamWriter(mem))
    {
        sw.Write("<p>my first paragraph</p>");
        sw.Flush();
        mem.Seek(0, SeekOrigin.Begin);
        using (var document = new HTMLDocument(mem, "about:blank"))
        {
            // ดำเนินการกับเอกสาร HTML ที่นี่...
        }
    }
}
```

ในตัวอย่างนี้ เราจะแสดงวิธีการสร้างเอกสาร HTML จากข้อมูลในสตรีมหน่วยความจำ สิ่งนี้มีประโยชน์เมื่อคุณมีเนื้อหา HTML ในสตรีมและต้องการจัดการมัน

## บทสรุป

Aspose.HTML สำหรับ .NET มอบชุดเครื่องมืออันทรงพลังสำหรับการสร้างและทำงานกับเอกสาร HTML ในแอปพลิเคชัน .NET ของคุณ ด้วยตัวอย่างที่ให้ไว้ในบทช่วยสอนนี้ คุณสามารถเริ่มต้นสร้างเอกสาร HTML ได้อย่างง่ายดาย ไม่ว่าจะเป็นตั้งแต่ต้น ไฟล์ในเครื่อง URL ระยะไกล หรือเนื้อหา HTML ที่มีอยู่

 มีคำถามหรือต้องการความช่วยเหลือ? เยี่ยมชมฟอรั่มชุมชน Aspose.HTML เพื่อรับการสนับสนุนที่[https://forum.aspose.com/](https://forum.aspose.com/).

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.HTML สำหรับ .NET ใช้งานได้ฟรีหรือไม่
 ตอบ 1: Aspose.HTML สำหรับ .NET ให้ทดลองใช้ฟรี แต่สำหรับการใช้งานเต็มรูปแบบ คุณจะต้องซื้อใบอนุญาต สามารถดูรายละเอียดเพิ่มเติมได้ที่[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### คำถามที่ 2: ฉันจะรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET ได้อย่างไร
A2: หากคุณต้องการใบอนุญาตชั่วคราว คุณสามารถขอรับได้ที่[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### คำถามที่ 3: ฉันจะหาเอกสารสำหรับ Aspose.HTML สำหรับ .NET ได้ที่ไหน
 A3: สามารถดูเอกสารได้ที่[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### คำถามที่ 4: มีไลบรารี Aspose อื่น ๆ สำหรับการพัฒนา .NET หรือไม่
 ตอบ 4: ใช่ Aspose มีไลบรารีมากมายสำหรับรูปแบบไฟล์ต่างๆ และงานจัดการเอกสาร ตรวจสอบข้อเสนอของพวกเขาได้ที่[https://products.aspose.com/](https://products.aspose.com/).

### คำถามที่ 5: ฉันสามารถใช้ Aspose.HTML สำหรับ .NET ในเว็บแอปพลิเคชันของฉันได้หรือไม่
A5: ใช่ Aspose.HTML สำหรับ .NET เข้ากันได้กับเว็บแอปพลิเคชัน ทำให้เป็นตัวเลือกที่หลากหลายสำหรับทั้งโปรเจ็กต์บนเดสก์ท็อปและบนเว็บ
