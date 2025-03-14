---
title: แปลง HTML เป็น PNG ใน .NET ด้วย Aspose.HTML
linktitle: แปลง HTML เป็น PNG ใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: ค้นพบวิธีใช้ Aspose.HTML สำหรับ .NET เพื่อจัดการและแปลงเอกสาร HTML คำแนะนำทีละขั้นตอนสำหรับการพัฒนา .NET ที่มีประสิทธิภาพ
weight: 20
url: /th/net/html-extensions-and-conversions/convert-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง HTML เป็น PNG ใน .NET ด้วย Aspose.HTML


## การแนะนำ

Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพที่ช่วยให้คุณทำงานกับเอกสาร HTML ในแอปพลิเคชัน .NET ของคุณได้ ไม่ว่าคุณจะต้องแปลง HTML เป็นรูปแบบอื่น จัดการเอกสาร HTML หรือดึงข้อมูลจากเอกสารเหล่านั้น Aspose.HTML มีฟังก์ชันต่างๆ มากมายที่จะช่วยให้คุณทำงานได้ง่ายขึ้น ในคู่มือฉบับสมบูรณ์นี้ เราจะแบ่งการใช้งาน Aspose.HTML สำหรับ .NET ออกเป็นชุดตัวอย่างทีละขั้นตอน ซึ่งจะช่วยให้คุณเข้าใจถึงวิธีการใช้ประโยชน์จากศักยภาพทั้งหมดของไลบรารีนี้ในโครงการของคุณ

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเริ่มใช้ Aspose.HTML สำหรับ .NET โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

### 1. ติดตั้ง Aspose.HTML สำหรับ .NET

 ในการเริ่มต้น คุณต้องติดตั้ง Aspose.HTML สำหรับ .NET คุณสามารถดาวน์โหลดไลบรารีได้จากเว็บไซต์[ที่นี่](https://releases.aspose.com/html/net/)ปฏิบัติตามคำแนะนำในการติดตั้งที่ให้ไว้เพื่อตั้งค่า Aspose.HTML ในโครงการ .NET ของคุณ

### 2. นำเข้าเนมสเปซที่จำเป็น

ในโปรเจ็กต์ .NET ของคุณ คุณต้องนำเข้าเนมสเปซ Aspose.HTML เพื่อเข้าถึงคลาสและวิธีการของมัน คุณสามารถทำได้โดยเพิ่มบรรทัดโค้ดต่อไปนี้ที่ด้านบนของไฟล์ C#:

```csharp
using Aspose.Html;
```

เมื่อมีข้อกำหนดเบื้องต้นแล้ว เรามาแบ่งตัวอย่างแต่ละตัวอย่างออกเป็นขั้นตอนต่างๆ กัน:

## แปลง HTML เป็น PNG ใน .NET

### ขั้นตอนที่ 1: เริ่มต้นตัวแปร

ขั้นแรก คุณต้องตั้งค่าตัวแปรที่จำเป็น ในตัวอย่างนี้ เราจะแปลงเอกสาร HTML เป็นรูปภาพ PNG

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Data Directory";
```

### ขั้นตอนที่ 2: โหลดเอกสาร HTML

ในการดำเนินการแปลง คุณจะต้องโหลดเอกสาร HTML ที่คุณต้องการแปลง 

```csharp
// แหล่งที่มาเอกสาร HTML
HTMLDocument htmlDocument = new HTMLDocument(dataDir + "input.html");
```

### ขั้นตอนที่ 3: กำหนดค่าตัวเลือกการแปลง

ระบุตัวเลือกการแปลง ในกรณีนี้ เราจะแปลง HTML เป็นรูปแบบภาพ PNG

```csharp
// เริ่มต้น ImageSaveOptions
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Png);
```

### ขั้นตอนที่ 4: กำหนดเส้นทางไฟล์เอาท์พุต

กำหนดเส้นทางที่คุณต้องการบันทึกไฟล์ PNG ที่แปลงแล้ว

```csharp
// เส้นทางไฟล์เอาท์พุต
string outputFile = dataDir + "HTMLtoPNG_Output.png";
```

### ขั้นตอนที่ 5: ดำเนินการแปลง

 สุดท้ายให้ดำเนินการแปลงโดยใช้`Converter` ระดับ.

```csharp
// แปลง HTML เป็น PNG
Converter.ConvertHTML(htmlDocument, options, outputFile);
```

ด้วยขั้นตอนเหล่านี้ คุณจะสามารถแปลงเอกสาร HTML เป็นภาพ PNG โดยใช้ Aspose.HTML สำหรับ .NET ได้สำเร็จ

## บทสรุป

Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีความยืดหยุ่นซึ่งช่วยลดความซับซ้อนในการทำงานกับเอกสาร HTML ในแอปพลิเคชัน .NET ด้วยตัวอย่างและข้อกำหนดเบื้องต้นแบบทีละขั้นตอนที่มีให้ คุณก็จะสามารถใช้งานไลบรารีนี้ในโครงการของคุณได้อย่างมีประสิทธิภาพ ใช้ประโยชน์จากพลังของ Aspose.HTML เพื่อสร้าง จัดการ และแปลงเอกสาร HTML ได้อย่างราบรื่น

## คำถามที่พบบ่อย

### Aspose.HTML สำหรับ .NET ใช้ได้ฟรีหรือไม่?
 Aspose.HTML สำหรับ .NET ไม่ใช่ไลบรารีฟรี คุณสามารถตรวจสอบราคาและตัวเลือกใบอนุญาตได้[ที่นี่](https://purchase.aspose.com/buy).

### ฉันสามารถหาเอกสารเพิ่มเติมสำหรับ Aspose.HTML สำหรับ .NET ได้จากที่ใด
 คุณสามารถดูเอกสารประกอบได้[ที่นี่](https://reference.aspose.com/html/net/) เพื่อข้อมูลเชิงลึกและตัวอย่าง

### ฉันสามารถทดลองใช้ Aspose.HTML สำหรับ .NET ก่อนซื้อได้หรือไม่?
 ใช่ คุณสามารถทดลองใช้เวอร์ชันทดลองใช้งานฟรีได้[ที่นี่](https://releases.aspose.com/) เพื่อประเมินคุณสมบัติและความสามารถของมัน

### ฉันจะได้รับการสนับสนุนสำหรับ Aspose.HTML สำหรับ .NET ได้อย่างไร
 หากคุณมีคำถามหรือต้องการความช่วยเหลือ คุณสามารถเยี่ยมชมฟอรัม Aspose ได้[ที่นี่](https://forum.aspose.com/) เพื่อรับความช่วยเหลือจากชุมชนและผู้เชี่ยวชาญ

### ฉันสามารถแปลง HTML เป็นรูปแบบใดได้บ้างโดยใช้ Aspose.HTML สำหรับ .NET?
Aspose.HTML สำหรับ .NET รองรับการแปลง HTML เป็นรูปแบบต่างๆ รวมถึง PDF, PNG, JPEG, BMP และอื่นๆ อีกมากมาย
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
