---
title: เรนเดอร์ HTML เป็น PNG ใน .NET ด้วย Aspose.HTML
linktitle: เรนเดอร์ HTML เป็น PNG ใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: เรียนรู้การใช้งาน Aspose.HTML สำหรับ .NET จัดการ HTML แปลงเป็นรูปแบบต่างๆ และอื่นๆ อีกมากมาย เจาะลึกบทช่วยสอนที่ครอบคลุมนี้!
weight: 10
url: /th/net/rendering-html-documents/render-html-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เรนเดอร์ HTML เป็น PNG ใน .NET ด้วย Aspose.HTML


ในบทช่วยสอนนี้ เราจะเจาะลึกเข้าไปในโลกของ Aspose.HTML สำหรับ .NET ซึ่งเป็นเครื่องมืออันทรงพลังสำหรับการทำงานกับเอกสาร HTML ด้วยการเขียนโปรแกรม ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้นเส้นทางในโลกแห่งการเขียนโปรแกรม .NET บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับสิ่งสำคัญของ Aspose.HTML ตั้งแต่การนำเข้าเนมสเปซไปจนถึงการแยกย่อยตัวอย่างในทางปฏิบัติ

## การแนะนำ

Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีความยืดหยุ่นซึ่งช่วยให้นักพัฒนาสามารถจัดการเอกสาร HTML ได้อย่างง่ายดาย ไม่ว่าคุณจะต้องแปลง HTML เป็นรูปแบบอื่น ดึงข้อมูลจากเอกสาร HTML หรือสร้างเนื้อหา HTML แบบไดนามิก Aspose.HTML ก็ช่วยคุณได้ ในบทช่วยสอนนี้ เราจะมาสำรวจความสามารถของมันทีละขั้นตอน

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกตัวอย่างโค้ด คุณต้องมีข้อกำหนดเบื้องต้นบางประการ:

1. Visual Studio: ให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio แล้ว เนื่องจากเราจะเขียนโค้ด .NET

2.  Aspose.HTML สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารี Aspose.HTML สำหรับ .NET จาก[ลิงค์นี้](https://releases.aspose.com/html/net/) คุณสามารถเลือกได้ระหว่างการทดลองใช้ฟรีหรือซื้อใบอนุญาต[ที่นี่](https://purchase.aspose.com/buy).

3. .NET Framework หรือ .NET Core: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET Framework หรือ .NET Core ไว้ในเครื่องพัฒนาของคุณแล้ว ขึ้นอยู่กับข้อกำหนดของโครงการของคุณ

4. โปรแกรมแก้ไขโค้ด: คุณสามารถใช้ Visual Studio หรือโปรแกรมแก้ไขโค้ดอื่น ๆ ตามที่คุณต้องการ

## การนำเข้าเนมสเปซ

ในการเริ่มต้นใช้งาน Aspose.HTML สำหรับ .NET ก่อนอื่นเราต้องนำเข้าเนมสเปซที่จำเป็น เปิดโปรเจ็กต์ของคุณใน Visual Studio สร้างคลาส C# ใหม่ และนำเข้าเนมสเปซต่อไปนี้:

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;
```

เนมสเปซเหล่านี้ให้สิทธิ์ในการเข้าถึงคลาสและวิธีการต่าง ๆ ที่จำเป็นสำหรับการทำงานกับเอกสาร HTML ด้วยโปรแกรม

## ตัวอย่างการเรนเดอร์ HTML เป็น PNG

มาดูตัวอย่างโค้ดที่คุณให้มาโดยละเอียดและแบ่งมันออกเป็นขั้นตอนต่างๆ ดังต่อไปนี้:

```csharp
// เรนเดอร์ HTML เป็น PNG ใน .NET ด้วย Aspose.HTML
string dataDir = "Your Data Directory";

// ขั้นตอนที่ 1: สร้างวัตถุเอกสาร HTML
using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
{
    // ขั้นตอนที่ 2: สร้างโปรแกรมเรนเดอร์ HTML
    using (HtmlRenderer renderer = new HtmlRenderer())
    using (ImageDevice device = new ImageDevice(dataDir + @"document_out.png"))
    {
        // ขั้นตอนที่ 3: เรนเดอร์เอกสาร HTML เป็น PNG
        renderer.Render(device, document);
    }
}
```

### ขั้นตอนที่ 1: สร้างวัตถุเอกสาร HTML

 ในขั้นตอนนี้เราจะสร้าง`HTMLDocument` วัตถุซึ่งแสดงถึงเอกสาร HTML คุณสามารถส่งเนื้อหา HTML เป็นสตริงไปยังคอนสตรัคเตอร์ และคุณยังสามารถระบุเส้นทางฐานสำหรับการแก้ไขเส้นทางสัมพันธ์กันได้อีกด้วย

### ขั้นตอนที่ 2: สร้างโปรแกรมเรนเดอร์ HTML

 ที่นี่เราสร้าง`HtmlRenderer` วัตถุ นี่คือส่วนประกอบหลักที่รับผิดชอบในการแสดงเนื้อหา HTML 

### ขั้นตอนที่ 3: เรนเดอร์เอกสาร HTML เป็น PNG

 ในที่สุดเราจะเรนเดอร์เอกสาร HTML เป็นภาพ PNG โดยใช้`HtmlRenderer` และ`ImageDevice` รูปภาพ PNG ที่ได้จะถูกบันทึกในตำแหน่งที่ตั้งที่ระบุ`dataDir`.

## บทสรุป

ในบทช่วยสอนนี้ เราจะแนะนำ Aspose.HTML สำหรับ .NET และแจกแจงรายละเอียดของโค้ดตัวอย่าง นี่เป็นเพียงจุดเริ่มต้นของสิ่งที่คุณสามารถทำได้ด้วยไลบรารีอันทรงพลังนี้ คุณสามารถสำรวจเอกสารประกอบที่ครอบคลุมได้[ที่นี่](https://reference.aspose.com/html/net/) และเข้าถึงทรัพยากรและการสนับสนุนเพิ่มเติมบน[ฟอรั่ม Aspose](https://forum.aspose.com/).

หากคุณมีคำถามหรือต้องการความช่วยเหลือเกี่ยวกับ Aspose.HTML สำหรับ .NET โปรดติดต่อชุมชน Aspose หรือศึกษาเอกสารเพื่อขอคำแนะนำเพิ่มเติม

## คำถามที่พบบ่อย (FAQs)

### Aspose.HTML สำหรับ .NET คืออะไร?
   Aspose.HTML สำหรับ .NET เป็นไลบรารีที่ช่วยให้นักพัฒนาสามารถจัดการและแปลงเอกสาร HTML ด้วยโปรแกรมในแอปพลิเคชัน .NET

### ฉันจะรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET ได้อย่างไร
    คุณสามารถรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET ได้[ที่นี่](https://purchase.aspose.com/temporary-license/).

### ฉันสามารถแปลง HTML เป็นรูปแบบอื่นโดยใช้ Aspose.HTML สำหรับ .NET ได้หรือไม่
   ใช่ Aspose.HTML สำหรับ .NET มีตัวแปลงต่างๆ เพื่อแปลง HTML เป็นรูปแบบเช่น PDF, XPS และรูปภาพ

### มี Aspose.HTML สำหรับ .NET ให้ทดลองใช้งานฟรีหรือไม่
    ใช่ คุณสามารถดาวน์โหลดรุ่นทดลองใช้งานฟรีของ Aspose.HTML สำหรับ .NET ได้[ที่นี่](https://releases.aspose.com/).

### ฉันสามารถหาบทช่วยสอนและเอกสารเพิ่มเติมได้ที่ไหน
   คุณสามารถสำรวจเอกสารและบทช่วยสอนที่ครอบคลุมบน[หน้าเอกสาร Aspose.HTML สำหรับ .NET](https://reference.aspose.com/html/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
