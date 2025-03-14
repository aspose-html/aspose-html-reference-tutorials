---
title: แปลง HTML เป็น Markdown ใน .NET ด้วย Aspose.HTML
linktitle: แปลง HTML เป็น Markdown ใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: เรียนรู้วิธีการแปลง HTML เป็น Markdown ใน .NET โดยใช้ Aspose.HTML เพื่อการจัดการเนื้อหาอย่างมีประสิทธิภาพ รับคำแนะนำทีละขั้นตอนเพื่อกระบวนการแปลงที่ราบรื่น
weight: 18
url: /th/net/html-extensions-and-conversions/convert-html-to-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง HTML เป็น Markdown ใน .NET ด้วย Aspose.HTML


## การแนะนำ

ในยุคดิจิทัลทุกวันนี้ เนื้อหาบนเว็บมีความสำคัญมาก และความสามารถในการจัดการและแปลงเนื้อหาอย่างมีประสิทธิภาพก็มีความสำคัญเช่นกัน Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยลดความซับซ้อนในการประมวลผลเอกสาร HTML ช่วยให้คุณสามารถแปลงเนื้อหา HTML เป็นรูปแบบต่างๆ ได้อย่างง่ายดาย คำแนะนำทีละขั้นตอนนี้จะแนะนำคุณเกี่ยวกับขั้นตอนการใช้ Aspose.HTML สำหรับ .NET เพื่อแปลง HTML เป็นรูปแบบ Markdown

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเริ่มลงลึกในบทช่วยสอนนี้ ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

1.  Aspose.HTML สำหรับไลบรารี .NET: ดาวน์โหลดและติดตั้งไลบรารี Aspose.HTML สำหรับ .NET จาก[เว็บไซต์](https://releases.aspose.com/html/net/)คุณจะต้องมีไลบรารีนี้เพื่อดำเนินการตามตัวอย่าง

2. สภาพแวดล้อมการพัฒนา: ให้แน่ใจว่าคุณมีการตั้งค่าสภาพแวดล้อมการพัฒนา .NET ไว้แล้ว รวมถึง Visual Studio หรือตัวแก้ไขโค้ดที่เหมาะสมอื่น ๆ

3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# จะเป็นประโยชน์ในการทำความเข้าใจและการนำตัวอย่างไปใช้

## นำเข้าเนมสเปซ

ในการเริ่มต้น คุณต้องนำเข้าเนมสเปซ Aspose.HTML เข้าสู่โปรเจ็กต์ C# ของคุณ ซึ่งจะช่วยให้คุณสามารถเข้าถึงคลาสและวิธีการที่จำเป็นสำหรับการแปลง HTML เป็น Markdown ได้

### ขั้นตอนที่ 1: นำเข้าเนมสเปซ Aspose.HTML

```csharp
using Aspose.Html;
```

เมื่อนำเนมสเปซเข้ามาแล้ว คุณสามารถดำเนินการแปลง HTML เป็น Markdown ได้

## แปลง HTML เป็น Markdown ใน .NET ด้วย Aspose.HTML

ในตัวอย่างนี้ เราจะสาธิตวิธีการแปลงเอกสาร HTML เป็น Markdown โดยใช้ Aspose.HTML สำหรับ .NET 

### ขั้นตอนที่ 1: สร้าง HTMLDocument

เริ่มต้นด้วยการสร้างเอกสาร HTML โดยใช้ Aspose.HTML ในตัวอย่างนี้ เรามีเนื้อหา HTML ง่ายๆ ที่มีความยาวสองย่อหน้า

```csharp
string dataDir = "Your Data Directory";
using (var document = new Aspose.Html.HTMLDocument("<p>my first paragraph</p>" +
"<p>my second paragraph</p>", dataDir))
{
    // โค้ดของคุณจะอยู่ที่นี่
}
```

### ขั้นตอนที่ 2: บันทึกเป็นมาร์กดาวน์

 ตอนนี้เรามาบันทึกเนื้อหา HTML เป็น Markdown กัน ในขั้นตอนนี้เราจะใช้`Saving.HTMLSaveFormat.Markdown` ตัวเลือกสำหรับระบุรูปแบบ

```csharp
document.Save(dataDir + "Markdown.md", Saving.HTMLSaveFormat.Markdown);
```

ขอแสดงความยินดี! คุณได้แปลงเอกสาร HTML เป็น Markdown โดยใช้ Aspose.HTML สำหรับ .NET สำเร็จแล้ว

## กำหนดกฎการแปลงมาร์กดาวน์

บางครั้งคุณอาจต้องการปรับแต่งกฎการแปลง Markdown เพื่อรวมหรือไม่รวมองค์ประกอบ HTML เฉพาะ ในตัวอย่างนี้ เราจะกำหนดกฎสำหรับการแปลงเฉพาะองค์ประกอบที่เลือกเท่านั้น

### ขั้นตอนที่ 1: กำหนดกฎมาร์กดาวน์

 ขั้นแรก ให้สร้างเอกสาร HTML ตามที่แสดงในตัวอย่างก่อนหน้า จากนั้นสร้าง`MarkdownSaveOptions` วัตถุที่จะระบุข้อกำหนดการแปลง

```csharp
string dataDir = "Your Data Directory";
using (var document = new Aspose.Html.HTMLDocument("<p>my first paragraph</p>", dataDir))
{
    var options = new Aspose.Html.Saving.MarkdownSaveOptions();
    
    // กำหนดกฎ: มีเพียงองค์ประกอบ <a>, <img> และ <p> เท่านั้นที่จะถูกแปลงเป็นมาร์กดาวน์
    options.Features = MarkdownFeatures.Link | MarkdownFeatures.Image | MarkdownFeatures.AutomaticParagraph;
    
    document.Save(dataDir + "Markdown.md", options);
}
```

เมื่อทำตามขั้นตอนนี้ คุณจะควบคุมองค์ประกอบ HTML เฉพาะที่จะถูกแปลงเป็น Markdown ได้

## บทสรุป

 Aspose.HTML สำหรับ .NET ช่วยให้การแปลง HTML เป็น Markdown ง่ายขึ้นด้วยแนวทางที่ตรงไปตรงมา ด้วยตัวอย่างที่ให้มาและคำแนะนำทีละขั้นตอน ตอนนี้คุณมีเครื่องมือในการจัดการและแปลงเนื้อหา HTML เป็น Markdown อย่างมีประสิทธิภาพแล้ว สำรวจเอกสาร Aspose.HTML สำหรับ .NET[ที่นี่](https://reference.aspose.com/html/net/) สำหรับคุณสมบัติและตัวเลือกขั้นสูงเพิ่มเติม

## คำถามที่พบบ่อย

### 1. สามารถใช้ Aspose.HTML สำหรับ .NET ได้ฟรีหรือไม่?

ไม่ Aspose.HTML สำหรับ .NET เป็นไลบรารีเชิงพาณิชย์ และคุณจะต้องมีใบอนุญาตที่ถูกต้องจึงจะใช้ในโปรเจ็กต์ของคุณได้ คุณสามารถขอใบอนุญาตชั่วคราวสำหรับการทดสอบได้จาก[ที่นี่](https://purchase.aspose.com/temporary-license/).

### 2. ฉันสามารถแปลงเอกสาร HTML ที่ซับซ้อนเป็น Markdown ได้หรือไม่

ใช่ Aspose.HTML สำหรับ .NET สามารถจัดการเอกสาร HTML ที่ซับซ้อน รวมถึงสไตล์ CSS รูปภาพ และลิงก์ ในระหว่างกระบวนการแปลงได้

### 3. มีการสนับสนุนด้านเทคนิคสำหรับ Aspose.HTML สำหรับ .NET หรือไม่

 ใช่ คุณสามารถรับการสนับสนุนด้านเทคนิคและความช่วยเหลือจากชุมชน Aspose.HTML ได้[ฟอรั่ม](https://forum.aspose.com/).

### 4. มีรูปแบบเอาต์พุตอื่น ๆ ที่รองรับนอกเหนือจาก Markdown หรือไม่

ใช่ Aspose.HTML สำหรับ .NET รองรับรูปแบบเอาต์พุตต่างๆ รวมถึง PDF, XPS, EPUB และอื่นๆ อีกมากมาย โปรดดูเอกสารประกอบเพื่อดูรายการรูปแบบที่รองรับอย่างครบถ้วน

### 5. ฉันสามารถทดลองใช้ Aspose.HTML สำหรับ .NET ก่อนซื้อได้หรือไม่

 แน่นอน! คุณสามารถดาวน์โหลด Aspose.HTML รุ่นทดลองใช้งานฟรีสำหรับ .NET ได้จาก[ที่นี่](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
