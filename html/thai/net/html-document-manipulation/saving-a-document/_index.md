---
title: การบันทึกเอกสารใน .NET ด้วย Aspose.HTML
linktitle: การบันทึกเอกสารใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: ปลดล็อกพลังของ Aspose.HTML สำหรับ .NET ด้วยคู่มือทีละขั้นตอนของเรา เรียนรู้การสร้าง จัดการ และแปลงเอกสาร HTML และ SVG
weight: 16
url: /th/net/html-document-manipulation/saving-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การบันทึกเอกสารใน .NET ด้วย Aspose.HTML


ในยุคดิจิทัลทุกวันนี้ การสร้างและจัดการเอกสาร HTML และ SVG ถือเป็นสิ่งจำเป็นสำหรับนักพัฒนาซอฟต์แวร์และธุรกิจต่างๆ Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยลดความซับซ้อนของงานเหล่านี้ โดยมีฟังก์ชันต่างๆ มากมายสำหรับทำงานกับ HTML, SVG และอื่นๆ ในคู่มือฉบับสมบูรณ์นี้ เราจะเจาะลึกถึงสิ่งสำคัญของ Aspose.HTML สำหรับ .NET โดยแบ่งตัวอย่างแต่ละตัวอย่างออกเป็นขั้นตอนที่ทำตามได้ง่าย ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น คุณจะพบว่าคู่มือนี้มีประโยชน์อย่างยิ่งสำหรับการใช้ประโยชน์จากความสามารถของ Aspose.HTML

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มต้นการเดินทางครั้งนี้ เรามาตรวจสอบกันก่อนว่าคุณมีทุกสิ่งที่คุณต้องการ:

- สภาพแวดล้อมการพัฒนา: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio หรือสภาพแวดล้อมการพัฒนา .NET อื่น ๆ บนคอมพิวเตอร์ของคุณแล้ว

- Aspose.HTML สำหรับ .NET: คุณต้องได้รับไลบรารี Aspose.HTML สำหรับ .NET คุณสามารถดาวน์โหลดได้จาก[ที่นี่](https://releases.aspose.com/html/net/).

- ความรู้เกี่ยวกับ C#: ความคุ้นเคยกับภาษาการเขียนโปรแกรม C# เป็นประโยชน์แต่ไม่จำเป็น คู่มือนี้ได้รับการออกแบบมาให้เหมาะกับผู้เริ่มต้น

## นำเข้าเนมสเปซ

หากต้องการเริ่มใช้ Aspose.HTML สำหรับ .NET คุณจะต้องนำเข้าเนมสเปซที่จำเป็นลงในโปรเจ็กต์ของคุณ ในโค้ด C# ให้ใส่เนมสเปซต่อไปนี้:

### ขั้นตอนที่ 1: นำเข้าเนมสเปซ Aspose.HTML
```csharp
using Aspose.Html;
```

เนมสเปซนี้จะทำให้คุณสามารถเข้าถึงความสามารถในการจัดการ HTML และ SVG ต่าง ๆ ได้

## HTML เป็นไฟล์

### ขั้นตอนที่ 1: สร้างเอกสาร HTML ที่ว่างเปล่า
```csharp
// เริ่มต้นเอกสาร HTML ที่ว่างเปล่า
using (var document = new Aspose.Html.HTMLDocument())
{
    // สร้างองค์ประกอบข้อความและเพิ่มลงในเอกสาร
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // บันทึก HTML ลงในไฟล์บนดิสก์
    document.Save("document.html");
}
```

ในตัวอย่างนี้ เราสร้างเอกสาร HTML และเพิ่มข้อความ "Hello World!" ลงไป จากนั้นจึงบันทึก HTML ลงในไฟล์บนดิสก์

## HTML ที่ไม่มีไฟล์เชื่อมโยง

### ขั้นตอนที่ 1: เตรียมไฟล์ HTML ง่ายๆ
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

ที่นี่เราจะสร้างไฟล์ HTML พื้นฐานพร้อมลิงก์ยึดไปยังไฟล์อื่น

### ขั้นตอนที่ 2: โหลด 'document.html' ลงในหน่วยความจำ
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // สร้างอินสแตนซ์ตัวเลือกการบันทึก
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //ตั้งค่าความลึกในการจัดการสูงสุดเป็น 0 เพื่อตัดไฟล์ HTML ที่เชื่อมโยง
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // บันทึกเอกสาร
    document.Save(@".\html-to-file-example\document.html", options);
}
```

ในตัวอย่างนี้ เราโหลดเอกสาร HTML เข้าไปในหน่วยความจำ ตั้งค่าความลึกในการจัดการสูงสุดเพื่อตัดไฟล์ที่เชื่อมโยง และบันทึกเอกสาร 

## HTML เป็น MHTML

### ขั้นตอนที่ 1: เตรียมไฟล์ HTML ง่ายๆ
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

เช่นเดียวกับในตัวอย่างที่ 2 เราจะสร้างไฟล์ HTML พื้นฐานโดยมีลิงก์ยึดไปยังไฟล์อื่น

### ขั้นตอนที่ 2: โหลด 'document.html' ลงในหน่วยความจำและบันทึกเป็น MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // บันทึกเอกสารเป็น MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

ที่นี่เราโหลดเอกสาร HTML ลงในหน่วยความจำและบันทึกในรูปแบบ MHTML

## HTML เป็นมาร์กดาวน์

### ขั้นตอนที่ 1: เตรียมโค้ด HTML
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 ในขั้นตอนนี้ เราจะกำหนดโค้ด HTML ที่ประกอบด้วย`<H2>` องค์ประกอบ.

### ขั้นตอนที่ 2: เริ่มต้นเอกสารจากโค้ด HTML และบันทึกเป็นมาร์กดาวน์
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // บันทึกเอกสารเป็นไฟล์ Markdown
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

เราสร้างเอกสาร HTML จากชิ้นส่วนโค้ดและบันทึกเป็นไฟล์ Markdown

## SVG เป็นไฟล์

### ขั้นตอนที่ 1: เตรียมรหัส SVG
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' ความสูง='80' ความกว้าง='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

ที่นี่ เราสร้างโค้ด SVG ที่วาดกราฟิกที่เรียบง่ายและมีสีสัน

### ขั้นตอนที่ 2: เริ่มต้นเอกสาร SVG จากรหัสและบันทึกลงในดิสก์
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // บันทึกไฟล์ SVG ลงในดิสก์
    document.Save("document.svg");
}
```

ในขั้นตอนนี้ เราจะสร้างเอกสาร SVG จากโค้ดและบันทึกเป็นไฟล์ SVG

## บทสรุป

Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีความยืดหยุ่นสูงซึ่งช่วยลดความซับซ้อนในการจัดการเอกสาร HTML และ SVG ในแอปพลิเคชัน .NET ของคุณ ในคู่มือนี้ เราได้ครอบคลุมตัวอย่างที่สำคัญ 5 ตัวอย่าง โดยแบ่งแต่ละตัวอย่างออกเป็นคำแนะนำทีละขั้นตอน ไม่ว่าคุณจะกำลังสร้าง แก้ไข หรือแปลงเอกสาร Aspose.HTML ก็ช่วยคุณได้ เพียงทำตามขั้นตอนเหล่านี้ คุณก็พร้อมที่จะเชี่ยวชาญเครื่องมืออันทรงพลังนี้แล้ว

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.HTML สำหรับ .NET คืออะไร?

A1: Aspose.HTML สำหรับ .NET เป็นไลบรารี .NET ที่ให้คุณลักษณะมากมายสำหรับการทำงานกับเอกสาร HTML และ SVG รวมถึงการสร้าง การจัดการ และการแปลง

### คำถามที่ 2: ฉันสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้ที่ไหน

 A2: คุณสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้จาก[ที่นี่](https://releases.aspose.com/html/net/).

### คำถามที่ 3: Aspose.HTML สำหรับ .NET เหมาะสำหรับผู้เริ่มต้นหรือไม่

A3: ใช่ Aspose.HTML สำหรับ .NET สามารถใช้งานได้ทั้งโดยผู้เริ่มต้นและนักพัฒนาที่มีประสบการณ์ ตัวอย่างในคู่มือนี้ได้รับการออกแบบมาให้เหมาะกับผู้เริ่มต้น

### คำถามที่ 4: ฉันสามารถแปลง HTML เป็นรูปแบบอื่นโดยใช้ Aspose.HTML สำหรับ .NET ได้หรือไม่

A4: ใช่ Aspose.HTML สำหรับ .NET รองรับการแปลงเป็นรูปแบบต่างๆ รวมถึง MHTML และ Markdown ดังที่แสดงในตัวอย่าง

### คำถามที่ 5: ฉันจะได้รับการสนับสนุนสำหรับ Aspose.HTML สำหรับ .NET ได้จากที่ไหน

 A5: คุณสามารถค้นหาการสนับสนุนและคำตอบสำหรับคำถามของคุณได้ในฟอรัมชุมชน Aspose.HTML[ที่นี่](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
