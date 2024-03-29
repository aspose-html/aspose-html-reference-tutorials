---
title: แสดงผล EPUB เป็น XPS ใน .NET ด้วย Aspose.HTML
linktitle: แสดงผล EPUB เป็น XPS ใน .NET
second_title: Aspose.HTML .NET API การจัดการ HTML
description: เรียนรู้วิธีสร้างและเรนเดอร์เอกสาร HTML ด้วย Aspose.HTML สำหรับ .NET ในบทช่วยสอนที่ครอบคลุมนี้ ดำดิ่งสู่โลกแห่งการจัดการ HTML การขูดเว็บ และอื่นๆ อีกมากมาย
type: docs
weight: 11
url: /th/net/rendering-html-documents/render-epub-as-xps/
---

## การแนะนำ

ยินดีต้อนรับสู่บทช่วยสอนที่ครอบคลุมเกี่ยวกับการใช้ Aspose.HTML สำหรับ .NET เพื่อสร้างและเรนเดอร์เอกสาร HTML Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยให้นักพัฒนาสามารถทำงานกับไฟล์ HTML โดยทางโปรแกรม ทำให้เป็นเครื่องมือที่มีค่าสำหรับแอปพลิเคชันที่หลากหลาย ตั้งแต่การขูดเว็บไปจนถึงการสร้างรายงาน

ในบทช่วยสอนนี้ เราจะครอบคลุมหัวข้อต่อไปนี้:
- วิชาบังคับก่อน: สิ่งที่คุณต้องมีในการเริ่มต้น
- นำเข้าเนมสเปซ: เนมสเปซที่จำเป็นเพื่อรวมไว้ในโปรเจ็กต์ของคุณ
- การสร้างและการแสดงผลเอกสาร HTML: เราจะแบ่งตัวอย่างโค้ดที่ให้มาออกเป็นหลายขั้นตอน และอธิบายแต่ละขั้นตอนอย่างละเอียด
- สรุป: สรุปโดยย่อของสิ่งที่เราได้เรียนรู้
- คำถามที่พบบ่อย (FAQ): คำตอบสำหรับคำถามทั่วไป
- คำอธิบายที่ปรับให้เหมาะสมกับเครื่องมือค้นหา: คำอธิบายโดยย่อสำหรับ SEO

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเจาะลึก Aspose.HTML สำหรับ .NET คุณจะต้องแน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

1. สภาพแวดล้อมการพัฒนา: ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าสภาพแวดล้อมการพัฒนา .NET บนเครื่องของคุณ คุณสามารถดาวน์โหลดและติดตั้ง Visual Studio หรือใช้ Visual Studio Code เพื่อการพัฒนาได้

2.  Aspose.HTML สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารี Aspose.HTML สำหรับ .NET จาก[ที่นี่](https://releases.aspose.com/html/net/) . คุณยังสามารถทดลองใช้ฟรีหรือซื้อใบอนุญาตได้จาก[ที่นี่](https://purchase.aspose.com/buy).

3. ไดเร็กทอรีข้อมูล: เตรียมไดเร็กทอรีที่คุณจะจัดเก็บไฟล์ HTML ของคุณ เช่น "ไดเร็กทอรีข้อมูลของคุณ" ที่กล่าวถึงในตัวอย่างโค้ด

## นำเข้าเนมสเปซ

หากต้องการทำงานกับ Aspose.HTML สำหรับ .NET คุณต้องนำเข้าเนมสเปซต่อไปนี้ในโปรเจ็กต์ของคุณ:

```csharp
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.EpubRenderer;
using System.IO;
```

เนมสเปซเหล่านี้ให้การเข้าถึงความสามารถในการเรนเดอร์ของ Aspose.HTML สำหรับ .NET และช่วยให้คุณสามารถจัดการเอกสาร HTML และ EPUB ได้

## การสร้างและแสดงผลเอกสาร HTML

ตอนนี้ เรามาแบ่งตัวอย่างโค้ดที่ให้มาออกเป็นหลายขั้นตอนและอธิบายแต่ละขั้นตอน:

```csharp
string dataDir = "Your Data Directory";

// ขั้นตอนที่ 1: เปิดเอกสาร EPUB เพื่ออ่าน
using (var fs = File.OpenRead(dataDir + "document.epub"))

// ขั้นตอนที่ 2: สร้างอุปกรณ์เรนเดอร์ XPS
using (var device = new XpsDevice(dataDir + "document_out.xps"))

// ขั้นตอนที่ 3: สร้างตัวเรนเดอร์ EPUB
using (var renderer = new EpubRenderer())
{
    // ขั้นตอนที่ 4: เรนเดอร์เอกสาร EPUB เป็นรูปแบบ XPS
    renderer.Render(device, fs);
}
```

1.  เปิดเอกสาร EPUB เพื่ออ่าน: ในขั้นตอนนี้ เราจะเปิดเอกสาร EPUB (ระบุโดยเส้นทางของไฟล์) เพื่ออ่านโดยใช้`FileStream`. เอกสารนี้จะเป็นแหล่งสำหรับการเรนเดอร์

2.  สร้างอุปกรณ์เรนเดอร์ XPS: เราสร้างอุปกรณ์เรนเดอร์ XPS โดยใช้`XpsDevice` ระดับ. อุปกรณ์นี้จะใช้ในการเรนเดอร์เนื้อหาจากเอกสาร EPUB เป็นรูปแบบ XPS

3.  สร้างตัวเรนเดอร์ EPUB: เราสร้างอินสแตนซ์ของ`EpubRenderer` ระดับ. คลาสนี้มีความสามารถในการเรนเดอร์ที่ปรับแต่งมาโดยเฉพาะสำหรับเอกสาร EPUB

4.  เรนเดอร์เอกสาร EPUB เป็นรูปแบบ XPS: สุดท้ายนี้ เราเรียกไฟล์`Render` วิธีการของ`EpubRenderer` คลาสเพื่อทำการเรนเดอร์ เอาต์พุตที่แสดงผลจะถูกบันทึกเป็นไฟล์ XPS ในตำแหน่งที่ระบุ

ยินดีด้วย! คุณสร้างและเรนเดอร์เอกสาร HTML โดยใช้ Aspose.HTML สำหรับ .NET สำเร็จแล้ว

## บทสรุป

ในบทช่วยสอนนี้ เราได้สำรวจขั้นตอนสำคัญในการสร้างและเรนเดอร์เอกสาร HTML โดยใช้ Aspose.HTML สำหรับ .NET ด้วยการทำตามขั้นตอนเหล่านี้และนำเข้าเนมสเปซที่จำเป็น คุณจะสามารถควบคุมประสิทธิภาพของ Aspose.HTML สำหรับ .NET ในแอปพลิเคชัน .NET ของคุณได้

## คำถามที่พบบ่อย (FAQ)

### 1. ฉันสามารถใช้ Aspose.HTML สำหรับ .NET สำหรับการขูดเว็บได้หรือไม่

ใช่ Aspose.HTML สำหรับ .NET สามารถใช้สำหรับงานขูดเว็บได้โดยการโหลดเนื้อหา HTML จากหน้าเว็บและจัดการโดยทางโปรแกรม

### 2. Aspose.HTML สำหรับ .NET รองรับรูปแบบเอาต์พุตอื่นๆ นอกเหนือจาก XPS หรือไม่

ใช่ Aspose.HTML สำหรับ .NET รองรับรูปแบบเอาต์พุตที่หลากหลาย รวมถึง PDF รูปแบบรูปภาพ และอื่นๆ คุณสามารถสำรวจเอกสารประกอบเพื่อดูข้อมูลโดยละเอียด

### 3. มีการทดลองใช้ฟรีหรือไม่?

 ใช่ คุณสามารถขอรับ Aspose.HTML สำหรับ .NET รุ่นทดลองใช้ฟรีได้จาก[ที่นี่](https://releases.aspose.com/).

### 4. ฉันจะขอความช่วยเหลือหรือแบ่งปันประสบการณ์กับห้องสมุดได้ที่ไหน?

คุณสามารถเข้าร่วมชุมชน Aspose และขอความช่วยเหลือหรือแบ่งปันประสบการณ์ของคุณบน[ฟอรั่ม Aspose](https://forum.aspose.com/).

### 5. ฉันสามารถใช้ Aspose.HTML สำหรับ .NET ในโครงการเชิงพาณิชย์ได้หรือไม่

 ได้ คุณสามารถใช้ Aspose.HTML สำหรับ .NET ในโครงการเชิงพาณิชย์ได้โดยการซื้อใบอนุญาตจาก[ที่นี่](https://purchase.aspose.com/buy).

