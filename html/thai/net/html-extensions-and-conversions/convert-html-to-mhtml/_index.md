---
title: แปลง HTML เป็น MHTML ใน .NET ด้วย Aspose.HTML
linktitle: แปลง HTML เป็น MHTML ใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: แปลง HTML เป็น MHTML ใน .NET ด้วย Aspose.HTML - คำแนะนำทีละขั้นตอนสำหรับการเก็บถาวรเนื้อหาเว็บอย่างมีประสิทธิภาพ เรียนรู้วิธีใช้ Aspose.HTML สำหรับ .NET เพื่อสร้างไฟล์เก็บถาวร MHTML
weight: 19
url: /th/net/html-extensions-and-conversions/convert-html-to-mhtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง HTML เป็น MHTML ใน .NET ด้วย Aspose.HTML


ในโลกของการพัฒนาเว็บ การแปลงเอกสารอย่างมีประสิทธิภาพถือเป็นสิ่งสำคัญ ไลบรารี Aspose.HTML สำหรับ .NET เป็นเครื่องมืออันทรงพลังที่ช่วยลดความซับซ้อนในการแปลงเอกสาร HTML เป็นรูปแบบต่างๆ รวมถึง MHTML MHTML ย่อมาจาก "MIME HTML" เป็นรูปแบบไฟล์เก็บถาวรของเว็บเพจที่ให้คุณบันทึกเว็บเพจและทรัพยากรของเว็บเพจนั้นไว้ในไฟล์เดียว ในคู่มือทีละขั้นตอนนี้ เราจะแนะนำคุณเกี่ยวกับกระบวนการแปลงเอกสาร HTML เป็น MHTML โดยใช้ Aspose.HTML สำหรับ .NET

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเริ่มกระบวนการแปลง โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

### 1. Aspose.HTML สำหรับไลบรารี .NET

 คุณต้องติดตั้งไลบรารี Aspose.HTML สำหรับ .NET หากคุณยังไม่ได้ติดตั้ง คุณสามารถดาวน์โหลดจากเว็บไซต์ได้[ที่นี่](https://releases.aspose.com/html/net/). ทำตามคำแนะนำการติดตั้งที่ให้ไว้ในเว็บไซต์

### 2. ตัวอย่างเอกสาร HTML

หากต้องการทำการแปลง คุณจะต้องมีเอกสาร HTML เพื่อใช้งาน โปรดเตรียมไฟล์ตัวอย่าง HTML ให้พร้อม คุณสามารถใช้เอกสาร HTML ของคุณเองหรือดาวน์โหลดตัวอย่างจาก[เอกสาร Aspose.HTML](https://reference.aspose.com/html/net/).

ตอนนี้คุณมีข้อกำหนดเบื้องต้นแล้ว มาดำเนินการแปลงกันเลย

## นำเข้าเนมสเปซ

ขั้นแรก คุณต้องนำเข้าเนมสเปซที่จำเป็นลงในโค้ด C# ของคุณ ซึ่งถือเป็นสิ่งสำคัญในการเข้าถึงคลาสและเมธอดที่จัดเตรียมไว้โดยไลบรารี Aspose.HTML

### นำเข้าเนมสเปซที่จำเป็น

```csharp
using Aspose.Html;
```

ตอนนี้คุณได้นำเข้าเนมสเปซที่จำเป็นแล้ว คุณสามารถดำเนินการตามกระบวนการแปลงจริงได้

เพื่อความชัดเจน เราจะแบ่งขั้นตอนการแปลงเอกสาร HTML เป็น MHTML ออกเป็นหลายขั้นตอน

## โหลดเอกสาร HTML

```csharp
string dataDir = "Your Data Directory"; // ระบุไดเรกทอรีข้อมูลของคุณ
HTMLDocument htmlDocument = new HTMLDocument(dataDir + "input.html"); // โหลดเอกสาร HTML
```

ในขั้นตอนนี้ คุณต้องระบุเส้นทางไปยังเอกสาร HTML ของคุณ Aspose.HTML จะโหลดไฟล์ HTML ทำให้พร้อมสำหรับการแปลง

## เริ่มต้น MHTMLSaveOptions

```csharp
MHTMLSaveOptions options = new MHTMLSaveOptions();
```

 ที่นี่คุณเริ่มต้น`MHTMLSaveOptions` คลาสซึ่งให้ตัวเลือกสำหรับการแปลง MHTML

## กำหนดกฎการจัดการทรัพยากร

```csharp
options.ResourceHandlingOptions.MaxHandlingDepth = 1;
```

คุณสามารถกำหนดกฎการจัดการทรัพยากรตามความต้องการของคุณได้ ในตัวอย่างนี้ เราจำกัดความลึกในการจัดการสูงสุดไว้ที่ 1 ซึ่งหมายความว่าจะรวมเฉพาะเอกสาร HTML หลักและทรัพยากรโดยตรงเท่านั้นในไฟล์ MHTML

## ระบุเส้นทางเอาต์พุต

```csharp
string outputMHTML = dataDir + "HTMLtoMHTML_Output.mht"; // ระบุเส้นทางไฟล์เอาท์พุต
```

ในขั้นตอนนี้ คุณต้องระบุเส้นทางสำหรับไฟล์ MHTML ที่ได้ นี่คือที่ที่เอกสาร MHTML ที่แปลงแล้วจะถูกบันทึก

## ดำเนินการแปลง

```csharp
Converter.ConvertHTML(htmlDocument, options, outputMHTML);
```

 ตอนนี้ถึงเวลาแปลงเอกสาร HTML เป็น MHTML แล้ว`ConvertHTML` วิธีนี้จะนำเอกสาร HTML ที่โหลด ตัวเลือกที่คุณตั้งค่า และเส้นทางไฟล์เอาท์พุตเป็นพารามิเตอร์

ขอแสดงความยินดี! คุณได้แปลงเอกสาร HTML เป็น MHTML โดยใช้ Aspose.HTML สำหรับ .NET สำเร็จแล้ว ขณะนี้คุณสามารถเข้าถึงไฟล์ MHTML ได้จากเส้นทางเอาต์พุตที่ระบุ

## บทสรุป

การแปลงเอกสาร HTML เป็นรูปแบบ MHTML อย่างมีประสิทธิภาพถือเป็นทักษะอันมีค่าสำหรับนักพัฒนาเว็บและผู้สร้างเนื้อหา Aspose.HTML สำหรับ .NET ช่วยลดความซับซ้อนของกระบวนการนี้ ทำให้เข้าถึงได้และเป็นมิตรต่อผู้ใช้ คุณสามารถสร้างไฟล์ MHTML สำหรับเนื้อหาเว็บของคุณได้อย่างง่ายดายโดยปฏิบัติตามคำแนะนำทีละขั้นตอนที่ระบุไว้ข้างต้น

ตอนนี้ มาตอบคำถามที่พบบ่อย (FAQ) กันเพื่อให้เข้าใจหัวข้อนี้ชัดเจนยิ่งขึ้น

## คำถามที่พบบ่อย

### MHTML คืออะไร และทำไมจึงใช้?

MHTML ย่อมาจาก "MIME HTML" เป็นรูปแบบไฟล์เก็บถาวรของเว็บเพจที่ให้คุณบันทึกเว็บเพจและทรัพยากรในไฟล์เดียว โดยทั่วไปแล้ว MHTML จะใช้เก็บถาวรเนื้อหาเว็บ แชร์เว็บเพจเป็นไฟล์เดียว และรับรองว่าทรัพยากรทั้งหมด (รูปภาพ สไตล์ชีต ฯลฯ) รวมอยู่ในไฟล์เดียวกัน แม้ว่าจะโฮสต์อยู่บนเซิร์ฟเวอร์ที่แตกต่างกันก็ตาม

### ฉันสามารถปรับแต่งการจัดการทรัพยากรเมื่อแปลงเป็น MHTML ได้หรือไม่

 ใช่ คุณสามารถทำได้ ตามที่แสดงในตัวอย่าง คุณสามารถกำหนดกฎการจัดการทรัพยากรโดยใช้`ResourceHandlingOptions` ของ`MHTMLSaveOptions`คลาส คุณสามารถควบคุมความลึกของทรัพยากรที่จะรวมอยู่ในไฟล์ MHTML ได้

### ฉันสามารถหาทรัพยากรและเอกสารเพิ่มเติมสำหรับ Aspose.HTML สำหรับ .NET ได้จากที่ไหน

 คุณสามารถสำรวจได้[เอกสาร Aspose.HTML](https://reference.aspose.com/html/net/) สำหรับข้อมูลเชิงลึก บทช่วยสอน และเอกสารอ้างอิง API นอกจากนี้[ฟอรั่ม Aspose.HTML](https://forum.aspose.com/) เป็นสถานที่ที่ดีในการขอความช่วยเหลือและหารือเกี่ยวกับปัญหาหรือคำถามต่างๆ ที่คุณอาจมี

### มี Aspose.HTML สำหรับ .NET ให้ทดลองใช้งานฟรีหรือไม่

 ใช่ คุณสามารถทดลองใช้ Aspose.HTML สำหรับ .NET ได้ฟรีโดยเข้าไปที่[ลิงค์นี้](https://releases.aspose.com/)เวอร์ชันทดลองใช้ช่วยให้คุณสามารถสำรวจคุณลักษณะของไลบรารีก่อนตัดสินใจซื้อ

### ฉันจะขอใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET ได้อย่างไร

 หากคุณต้องการใบอนุญาตชั่วคราว คุณสามารถขอได้จาก[เว็บไซต์ซื้อ Aspose](https://purchase.aspose.com/temporary-license/)ใบอนุญาตชั่วคราวนี้จะทำให้คุณสามารถเข้าถึงฟังก์ชันต่างๆ ของห้องสมุดได้อย่างครบถ้วนในระยะเวลาจำกัด


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
