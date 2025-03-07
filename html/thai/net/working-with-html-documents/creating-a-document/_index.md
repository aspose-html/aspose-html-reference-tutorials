---
title: การสร้างเอกสาร HTML ใน .NET ด้วย Aspose.HTML
linktitle: การสร้างเอกสาร HTML ใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: เรียนรู้วิธีการสร้างเอกสาร HTML ใน .NET โดยใช้ Aspose.HTML ตั้งแต่ต้นหรือจาก URL บทช่วยสอนที่ครอบคลุมสำหรับนักพัฒนาเว็บ
weight: 10
url: /th/net/working-with-html-documents/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การสร้างเอกสาร HTML ใน .NET ด้วย Aspose.HTML


ในด้านการพัฒนาเว็บและการจัดการข้อมูล การมีเครื่องมืออันทรงพลังในการสร้าง แก้ไข และทำงานกับเอกสาร HTML ถือเป็นสิ่งจำเป็น Aspose.HTML สำหรับ .NET เป็นเครื่องมือหนึ่งที่ช่วยลดความซับซ้อนของงานที่เกี่ยวข้องกับ HTML ในบทช่วยสอนที่ครอบคลุมนี้ เราจะมาสำรวจวิธีการสร้างเอกสาร HTML โดยใช้ Aspose.HTML สำหรับ .NET ทีละขั้นตอน ก่อนที่เราจะเจาะลึกในตัวอย่าง เรามาทำความเข้าใจข้อกำหนดเบื้องต้นกันก่อน

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่มการเดินทางครั้งนี้ โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio ไว้ในระบบของคุณแล้ว

2. Aspose.HTML สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารี Aspose.HTML สำหรับ .NET คุณสามารถค้นหาลิงก์ดาวน์โหลด[ที่นี่](https://releases.aspose.com/html/net/).

3. ความรู้พื้นฐานเกี่ยวกับ C#: ทำความคุ้นเคยกับพื้นฐานภาษาการเขียนโปรแกรม C#

ตอนนี้เราได้ครอบคลุมข้อกำหนดเบื้องต้นแล้ว เรามาเริ่มต้นสร้างเอกสาร HTML กันเลย

## การนำเข้าเนมสเปซ

ขั้นแรก คุณต้องนำเข้าเนมสเปซที่จำเป็นสำหรับการใช้ Aspose.HTML ในโปรเจ็กต์ C# ของคุณ เพิ่มคำสั่ง using ต่อไปนี้ลงในไฟล์โค้ดของคุณ:

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## การสร้างเอกสาร SVG

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "เกี่ยวกับ:ว่างเปล่า"))
    {
        // ดำเนินการกับเอกสาร SVG ที่นี่...
    }
}
```

 ในตัวอย่างนี้ เราสร้างเอกสาร SVG โดยระบุเนื้อหา SVG และ URL ฐาน`SVGDocument` คลาสจาก Aspose.HTML สำหรับ .NET ช่วยให้คุณสามารถจัดการเอกสาร SVG ได้อย่างง่ายดาย

## การสร้างเอกสาร HTML จากเริ่มต้น

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        // ดำเนินการกับเอกสาร HTML ที่นี่...
    }
}
```

 ตัวอย่างนี้สาธิตวิธีการสร้างเอกสาร HTML ตั้งแต่เริ่มต้น`HTMLDocument`คลาสนี้มอบพื้นที่ว่างสำหรับเนื้อหา HTML ของคุณ

## การสร้างเอกสาร HTML จากไฟล์ภายในเครื่อง

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

 หากคุณมีไฟล์ HTML อยู่แล้วในระบบภายในเครื่อง คุณสามารถโหลดได้โดยใช้`HTMLDocument` คลาสตามที่แสดงในตัวอย่างนี้

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

แนวทางทางเลือกนี้ยังแสดงวิธีการสร้างเอกสาร HTML จาก URL ระยะไกลโดยใช้ตัวสร้างที่แตกต่างกันอีกด้วย

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

หากคุณมีเนื้อหา HTML ในรูปแบบสตริง คุณสามารถสร้างเอกสาร HTML ด้วยเนื้อหานั้นได้ ดังที่แสดงในตัวอย่างนี้

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

ในตัวอย่างนี้ เราจะแสดงวิธีสร้างเอกสาร HTML จากข้อมูลในสตรีมหน่วยความจำ ซึ่งอาจมีประโยชน์ในกรณีที่คุณมีเนื้อหา HTML ในสตรีมและต้องการจัดการเนื้อหาดังกล่าว

## บทสรุป

Aspose.HTML สำหรับ .NET มอบชุดเครื่องมืออันทรงพลังสำหรับการสร้างและทำงานกับเอกสาร HTML ในแอปพลิเคชัน .NET ของคุณ ด้วยตัวอย่างที่ให้ไว้ในบทช่วยสอนนี้ คุณสามารถเริ่มต้นสร้างเอกสาร HTML ได้อย่างง่ายดาย ไม่ว่าจะจากศูนย์ ไฟล์ในเครื่อง URL ระยะไกล หรือเนื้อหา HTML ที่มีอยู่

 มีคำถามหรือต้องการความช่วยเหลือหรือไม่ เยี่ยมชมฟอรัมชุมชน Aspose.HTML เพื่อรับการสนับสนุนได้ที่[https://forum.aspose.com/](https://forum.aspose.com/).

## คำถามที่พบบ่อย

### คำถามที่ 1: สามารถใช้ Aspose.HTML สำหรับ .NET ได้ฟรีหรือไม่?
 A1: Aspose.HTML สำหรับ .NET นำเสนอรุ่นทดลองใช้งานฟรี แต่หากต้องการใช้งานเต็มรูปแบบ คุณจะต้องซื้อใบอนุญาต คุณสามารถดูรายละเอียดเพิ่มเติมได้ที่[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### คำถามที่ 2: ฉันจะได้รับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET ได้อย่างไร
 A2: หากคุณต้องการใบอนุญาตชั่วคราว คุณสามารถขอรับได้ที่[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### คำถามที่ 3: ฉันสามารถหาเอกสารสำหรับ Aspose.HTML สำหรับ .NET ได้จากที่ใด
A3: สามารถดูเอกสารได้ที่[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### คำถามที่ 4: มีไลบรารี Aspose อื่นสำหรับการพัฒนา .NET หรือไม่
 A4: ใช่ Aspose มีไลบรารีต่างๆ มากมายสำหรับรูปแบบไฟล์และงานจัดการเอกสาร ลองดูข้อเสนอของเราได้ที่[https://products.aspose.com/](https://products.aspose.com/).

### คำถามที่ 5: ฉันสามารถใช้ Aspose.HTML สำหรับ .NET ในแอปพลิเคชันเว็บของฉันได้หรือไม่
A5: ใช่ Aspose.HTML สำหรับ .NET เข้ากันได้กับแอพพลิเคชันเว็บ ทำให้เป็นตัวเลือกที่หลากหลายสำหรับทั้งโปรเจ็กต์บนเดสก์ท็อปและบนเว็บ

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
