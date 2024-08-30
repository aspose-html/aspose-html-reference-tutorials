---
title: การใช้เทมเพลต HTML ใน .NET ด้วย Aspose.HTML
linktitle: การใช้เทมเพลต HTML ใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: เรียนรู้วิธีใช้ Aspose.HTML สำหรับ .NET เพื่อสร้างเอกสาร HTML แบบไดนามิกจากข้อมูล JSON ใช้ประโยชน์จากพลังของการจัดการ HTML ในแอปพลิเคชัน .NET ของคุณ
type: docs
weight: 17
url: /th/net/advanced-features/using-html-templates/
---

หากคุณกำลังมองหาวิธีทำงานกับเอกสารและเทมเพลต HTML ในแอปพลิเคชัน .NET คุณมาถูกที่แล้ว! Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีความยืดหยุ่นซึ่งช่วยให้นักพัฒนาสามารถจัดการเอกสารและเทมเพลต HTML ได้อย่างง่ายดาย ในบทช่วยสอนนี้ เราจะเจาะลึกถึงสิ่งสำคัญในการใช้ Aspose.HTML สำหรับ .NET โดยจะแบ่งขั้นตอนแต่ละขั้นตอนและให้คำอธิบายที่ชัดเจนตลอดขั้นตอน

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกถึงรายละเอียดของ Aspose.HTML สำหรับ .NET โปรดตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio ไว้ในเครื่องของคุณแล้ว คุณสามารถดาวน์โหลดได้จากเว็บไซต์หากยังไม่มี

2.  Aspose.HTML สำหรับ .NET: คุณต้องติดตั้ง Aspose.HTML สำหรับ .NET ไว้ในโปรเจ็กต์ Visual Studio ของคุณ คุณสามารถรับได้จาก[เอกสารประกอบ](https://reference.aspose.com/html/net/).

3. ข้อมูล JSON: เตรียมแหล่งข้อมูล JSON ที่คุณต้องการใช้ในการเพิ่มเทมเพลต HTML สำหรับบทช่วยสอนนี้ เราจะใช้ข้อมูล JSON ต่อไปนี้:

```json
{
    'FirstName': 'John',
    'LastName': 'Smith',
    'Address': {
        'City': 'Dallas',
        'Street': 'Austin rd.',
        'Number': '200'
    }
}
```

4. เทมเพลต HTML: สร้างเทมเพลต HTML ที่คุณต้องการเติมข้อมูล JSON นี่คือตัวอย่างง่ายๆ:

```html
<table border=1>
    <tr>
        <th>Person</th>
        <th>Address</th>
    </tr>
    <tr>
        <td>{{FirstName}} {{LastName}}</td>
        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
    </tr>
</table>
```

## การนำเข้าเนมสเปซ

ขั้นแรกเลย เราจะนำเข้าเนมสเปซที่จำเป็นลงในโครงการ .NET ของคุณ:

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Loading;
```

ตอนนี้เราได้ครอบคลุมข้อกำหนดเบื้องต้นและนำเข้าเนมสเปซที่จำเป็นแล้ว มาแบ่งแต่ละขั้นตอนโดยละเอียดกัน

## ขั้นตอนที่ 1: เตรียมแหล่งข้อมูล JSON

เริ่มต้นด้วยการสร้างแหล่งข้อมูล JSON ที่เก็บข้อมูลที่คุณต้องการแทรกลงในเทมเพลต HTML ในตัวอย่างนี้ เราได้เตรียมแหล่งข้อมูล JSON ไว้แล้วตามที่ได้กล่าวไว้ในข้อกำหนดเบื้องต้น บันทึกลงในไฟล์ เช่น "data-source.json"

```csharp
var data = @"{
    'FirstName': 'John',
    'LastName': 'Smith',
    'Address': {
        'City': 'Dallas',
        'Street': 'Austin rd.',
        'Number': '200'
    }
}";
System.IO.File.WriteAllText("data-source.json", data);
```

โค้ดตัวอย่างนี้จะอ่านข้อมูล JSON และเขียนลงในไฟล์ชื่อ "data-source.json"

## ขั้นตอนที่ 2: เตรียมเทมเพลต HTML

ตอนนี้เรามาสร้างเทมเพลต HTML ที่คุณต้องการเพิ่มข้อมูล JSON กัน บันทึกเทมเพลตนี้ลงในไฟล์ เช่น "template.html"

```csharp
var template = @"
<table border=1>
    <tr>
        <th>Person</th>
        <th>Address</th>
    </tr>
    <tr>
        <td>{{FirstName}} {{LastName}}</td>
        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
    </tr>
</table>
";
System.IO.File.WriteAllText("template.html", template);
```

 เทมเพลต HTML นี้ประกอบด้วยตัวแทน เช่น`{{FirstName}}`, `{{LastName}}`, `{{Address.Street}}`, `{{Address.Number}}` และ`{{Address.City}}`ซึ่งเราจะแทนที่ด้วยข้อมูลจริง

## ขั้นตอนที่ 3: เติมข้อมูลในเทมเพลต HTML

 สุดท้ายให้เรียกใช้`Converter.ConvertTemplate` วิธีการในการเติมเทมเพลต HTML ของคุณด้วยข้อมูลจากแหล่ง JSON

```csharp
Aspose.Html.Converters.Converter.ConvertTemplate(
"template.html", new Aspose.Html.Converters.TemplateData("data-source.json"), new Aspose.Html.Loading.TemplateLoadOptions(), "document.html"
);
```

โค้ดนี้ใช้ไฟล์ "template.html" แทนที่ตัวแทนด้วยค่า JSON ที่สอดคล้องกัน และบันทึกผลลัพธ์ใน "document.html"

ขอแสดงความยินดี! คุณได้ใช้ความสามารถของ Aspose.HTML สำหรับ .NET เพื่อสร้างเอกสาร HTML แบบไดนามิกจากข้อมูล JSON สำเร็จแล้ว

## บทสรุป

ในบทช่วยสอนนี้ เราได้ศึกษาหลักพื้นฐานของการใช้ Aspose.HTML สำหรับ .NET เพื่อสร้างเอกสาร HTML แบบไดนามิก เราได้ครอบคลุมข้อกำหนดเบื้องต้น การนำเข้าเนมสเปซ และการแบ่งแต่ละขั้นตอนอย่างละเอียด หากทำตามขั้นตอนเหล่านี้ คุณจะสามารถผสานการสร้างเอกสาร HTML เข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างราบรื่น

## คำถามที่พบบ่อย

### คำถามที่ 1 Aspose.HTML สำหรับ .NET คืออะไร

A1: Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพที่ช่วยให้ผู้พัฒนา .NET สามารถทำงานกับเอกสารและเทมเพลต HTML ได้ด้วยการเขียนโปรแกรม ไลบรารีนี้ช่วยลดความยุ่งยากของงานต่างๆ เช่น การสร้าง การแปลง และการจัดการ HTML

### คำถามที่ 2 ฉันสามารถหาเอกสารประกอบสำหรับ Aspose.HTML สำหรับ .NET ได้ที่ไหน

 A2: คุณสามารถเข้าถึงเอกสารสำหรับ Aspose.HTML สำหรับ .NET ได้[ที่นี่](https://reference.aspose.com/html/net/). ให้ข้อมูลที่ครอบคลุม รวมถึงข้อมูลอ้างอิง API และตัวอย่างโค้ด

### คำถามที่ 3 ฉันสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้อย่างไร

A3: คุณสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้จากหน้าดาวน์โหลด[ที่นี่](https://releases.aspose.com/html/net/).

### คำถามที่ 4 มีรุ่นทดลองใช้งานฟรีสำหรับ Aspose.HTML สำหรับ .NET หรือไม่

 A4: ใช่ คุณสามารถลองใช้ Aspose.HTML สำหรับ .NET ได้โดยดาวน์โหลดเวอร์ชันทดลองใช้งานฟรีจาก[ที่นี่](https://releases.aspose.com/).

### คำถามที่ 5 ฉันต้องมีใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET หรือไม่?

 A5: หากคุณต้องการใบอนุญาตชั่วคราวเพื่อวัตถุประสงค์ในการประเมินผล คุณสามารถขอรับได้จาก[ที่นี่](https://purchase.aspose.com/temporary-license/).