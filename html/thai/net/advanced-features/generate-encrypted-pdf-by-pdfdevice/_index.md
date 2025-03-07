---
title: สร้าง PDF เข้ารหัสโดย PdfDevice ใน .NET ด้วย Aspose.HTML
linktitle: สร้าง PDF เข้ารหัสโดย PdfDevice ใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: แปลง HTML เป็น PDF แบบไดนามิกด้วย Aspose.HTML สำหรับ .NET บูรณาการได้ง่าย มีตัวเลือกที่ปรับแต่งได้ และประสิทธิภาพที่มั่นคง
weight: 15
url: /th/net/advanced-features/generate-encrypted-pdf-by-pdfdevice/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF เข้ารหัสโดย PdfDevice ใน .NET ด้วย Aspose.HTML


ในโลกของการพัฒนาเว็บที่เปลี่ยนแปลงอย่างรวดเร็ว ความจำเป็นในการแปลง HTML เป็น PDF แบบไดนามิกได้กลายมาเป็นความต้องการทั่วไป ไม่ว่าคุณต้องการสร้างรายงาน ใบแจ้งหนี้ หรือเพียงแค่เก็บถาวรเนื้อหาเว็บ Aspose.HTML สำหรับ .NET เป็นเครื่องมืออันทรงพลังที่สามารถทำให้กระบวนการนี้ราบรื่นขึ้นได้ ในบทช่วยสอนนี้ เราจะแนะนำคุณเกี่ยวกับขั้นตอนต่างๆ ในการแปลง HTML เป็น PDF แบบไดนามิกโดยใช้ Aspose.HTML สำหรับ .NET

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกโค้ด เรามาตรวจสอบกันก่อนว่าคุณมีทุกสิ่งที่คุณต้องการ:

### 1. การติดตั้ง

 ขั้นแรก คุณต้องดาวน์โหลดและติดตั้ง Aspose.HTML สำหรับ .NET คุณสามารถดูลิงก์ดาวน์โหลด[ที่นี่](https://releases.aspose.com/html/net/).

### 2. การนำเข้าเนมสเปซ

ในการเริ่มต้น ให้ใส่เนมสเปซที่จำเป็นไว้ที่จุดเริ่มต้นของโค้ดของคุณ เนมสเปซเหล่านี้มีความจำเป็นสำหรับการเข้าถึงฟังก์ชันการทำงานของ Aspose.HTML สำหรับ .NET

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Pdf.Paging;
using Aspose.Html.Saving;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using System;
using System.Drawing;
```

ตอนนี้ มาแบ่งโค้ดตัวอย่างที่คุณให้ไว้ออกเป็นขั้นตอนต่างๆ และอธิบายแต่ละขั้นตอนกัน

## การพังทลาย

### ขั้นตอนที่ 1: เริ่มต้นเอกสาร HTML

```csharp
using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
```

 ในขั้นตอนนี้เราจะสร้างอินสแตนซ์ของ`HTMLDocument` คลาสที่แสดงเนื้อหา HTML ที่คุณต้องการแปลง คุณสามารถส่งเนื้อหา HTML ของคุณเป็นสตริงได้ ตรวจสอบให้แน่ใจว่าคุณระบุเส้นทางที่ถูกต้องสำหรับไดเร็กทอรีการทำงานของคุณ

### ขั้นตอนที่ 2: กำหนดค่าตัวเลือกการแสดงผล PDF

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(new Size(500, 500), new Margin(50, 50, 50, 50))
    },
    Encryption = new PdfEncryptionInfo("user", "p@wd", PdfPermissions.PrintDocument, PdfEncryptionAlgorithm.RC4_128)
};
```

 ในขั้นตอนนี้เราจะสร้างอินสแตนซ์ของ`PdfRenderingOptions`ช่วยให้คุณสามารถกำหนดค่าการตั้งค่าต่างๆ สำหรับการแปลง PDF ได้ ในตัวอย่างนี้ เราจะตั้งค่าขนาดหน้าและระยะขอบ และระบุการตั้งค่าการเข้ารหัสสำหรับผลลัพธ์ PDF

### ขั้นตอนที่ 3: เรนเดอร์ HTML เป็น PDF

```csharp
using (PdfDevice device = new PdfDevice(options, dataDir + @"document_out.pdf"))
{
    document.RenderTo(device);
}
```

 ในขั้นตอนสุดท้ายนี้เราใช้`RenderTo` วิธีการแปลงเอกสาร HTML เป็น PDF เราส่ง`PdfDevice` อินสแตนซ์และเส้นทางไฟล์เอาท์พุตที่ต้องการ เนื้อหา HTML จะถูกแปลงเป็นเอกสาร PDF ด้วยการตั้งค่าที่ระบุ

ขอแสดงความยินดี! คุณได้แปลง HTML เป็น PDF แบบไดนามิกโดยใช้ Aspose.HTML สำหรับ .NET สำเร็จแล้ว ตอนนี้คุณสามารถรวมโค้ดนี้ลงในแอปพลิเคชันหรือโปรเจ็กต์เว็บของคุณตามต้องการ

## บทสรุป

Aspose.HTML สำหรับ .NET ทำให้กระบวนการแปลง HTML เป็น PDF แบบไดนามิกง่ายขึ้น ทำให้เป็นเครื่องมือที่มีประโยชน์สำหรับนักพัฒนาเว็บ เมื่อทำตามขั้นตอนที่ระบุไว้ในบทช่วยสอนนี้ คุณก็สามารถสร้างเอกสาร PDF จากเนื้อหา HTML ได้อย่างง่ายดาย พร้อมทั้งปรับแต่งผลลัพธ์ให้ตรงตามความต้องการเฉพาะของคุณได้

## คำถามที่พบบ่อย

### คำถามที่ 1 Aspose.HTML สำหรับ .NET เข้ากันได้กับ HTML เวอร์ชันต่างๆ หรือไม่

A1: ใช่ Aspose.HTML สำหรับ .NET ได้รับการออกแบบมาเพื่อรองรับ HTML เวอร์ชันต่างๆ เพื่อให้มั่นใจว่ามีความเข้ากันได้กับเนื้อหาเว็บที่หลากหลาย

### คำถามที่ 2 ฉันสามารถปรับแต่งเอาต์พุต PDF เพิ่มเติมได้หรือไม่

A2: แน่นอน! คุณสามารถปรับเปลี่ยนตัวเลือกการแสดงผลเพื่อกำหนดขนาดหน้า ขอบ การเข้ารหัส และการตั้งค่าเฉพาะ PDF อื่นๆ ให้เหมาะกับความต้องการของคุณได้

### คำถามที่ 3 Aspose.HTML สำหรับ .NET รองรับรูปแบบเอาต์พุตอื่น ๆ หรือไม่

A3: ใช่ นอกเหนือจาก PDF แล้ว Aspose.HTML สำหรับ .NET ยังรองรับรูปแบบเอาต์พุตอื่นๆ อีกมากมาย รวมถึงรูปแบบภาพอย่าง PNG และ JPEG

### คำถามที่ 4. มีรุ่นทดลองใช้งานฟรีหรือไม่?

A4: ใช่ คุณสามารถทดลองใช้ Aspose.HTML สำหรับ .NET ได้ฟรี เริ่มต้นใช้งาน[ที่นี่](https://releases.aspose.com/).

### คำถามที่ 5 ฉันจะได้รับความช่วยเหลือและการสนับสนุนได้จากที่ไหน

 A5: หากมีคำถามหรือปัญหาใดๆ คุณสามารถไปที่ฟอรัม Aspose เพื่อรับการสนับสนุนและการสนทนา:[สนับสนุน](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
