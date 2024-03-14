---
title: การใช้เทมเพลต HTML ใน .NET กับ Aspose.HTML
linktitle: การใช้เทมเพลต HTML ใน .NET
second_title: Aspose.HTML .NET API การจัดการ HTML
description: เรียนรู้วิธีใช้ Aspose.HTML สำหรับ .NET เพื่อสร้างเอกสาร HTML แบบไดนามิกจากข้อมูล JSON ควบคุมพลังของการจัดการ HTML ในแอปพลิเคชัน .NET ของคุณ
type: docs
weight: 17
url: /th/net/advanced-features/using-html-templates/
---

หากคุณต้องการทำงานกับเอกสารและเทมเพลต HTML ในแอปพลิเคชัน .NET คุณมาถูกที่แล้ว! Aspose.HTML สำหรับ .NET เป็นไลบรารีอเนกประสงค์ที่ช่วยให้นักพัฒนาจัดการเอกสารและเทมเพลต HTML ได้อย่างง่ายดาย ในบทช่วยสอนนี้ เราจะเจาะลึกถึงสิ่งสำคัญของการใช้ Aspose.HTML สำหรับ .NET โดยแจกแจงรายละเอียดแต่ละขั้นตอนและให้คำอธิบายที่ชัดเจนไปพร้อมกัน

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกรายละเอียดสำคัญของ Aspose.HTML สำหรับ .NET ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio บนเครื่องของคุณแล้ว คุณสามารถดาวน์โหลดได้จากเว็บไซต์หากคุณยังไม่มี

2.  Aspose.HTML สำหรับ .NET: คุณต้องมี Aspose.HTML สำหรับ .NET ติดตั้งอยู่ในโครงการ Visual Studio ของคุณ คุณสามารถรับได้จาก[เอกสารประกอบ](https://reference.aspose.com/html/net/).

3. ข้อมูล JSON: เตรียมแหล่งข้อมูล JSON ที่คุณต้องการใช้สำหรับเติมเทมเพลต HTML ของคุณ สำหรับบทช่วยสอนนี้ เราจะใช้ข้อมูล JSON ต่อไปนี้:

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

4. เทมเพลต HTML: สร้างเทมเพลต HTML ที่คุณต้องการเติมด้วยข้อมูล JSON นี่เป็นตัวอย่างง่ายๆ:

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

ก่อนอื่น มานำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ .NET ของคุณกันก่อน:

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Loading;
```

ตอนนี้เราได้ครอบคลุมข้อกำหนดเบื้องต้นและนำเข้าเนมสเปซที่จำเป็นแล้ว เรามาดูรายละเอียดแต่ละขั้นตอนกันดีกว่า

## ขั้นตอนที่ 1: เตรียมแหล่งข้อมูล JSON

เริ่มต้นด้วยการสร้างแหล่งข้อมูล JSON ที่เก็บข้อมูลที่คุณต้องการแทรกลงในเทมเพลต HTML ของคุณ ในตัวอย่างนี้ เราได้เตรียมแหล่งข้อมูล JSON ตามที่กล่าวไว้ในข้อกำหนดเบื้องต้นแล้ว บันทึกลงในไฟล์ เช่น "data-source.json"

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

ข้อมูลโค้ดนี้จะอ่านข้อมูล JSON และเขียนลงในไฟล์ชื่อ "data-source.json"

## ขั้นตอนที่ 2: เตรียมเทมเพลต HTML

ตอนนี้ เรามาสร้างเทมเพลต HTML ที่คุณต้องการเติมข้อมูล JSON กัน บันทึกเทมเพลตนี้ลงในไฟล์ เช่น "template.html"

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

 เทมเพลต HTML นี้มีตัวยึดตำแหน่งเช่น`{{FirstName}}`, `{{LastName}}`, `{{Address.Street}}`, `{{Address.Number}}` และ`{{Address.City}}`ซึ่งเราจะแทนที่ด้วยข้อมูลจริง

## ขั้นตอนที่ 3: เติมเทมเพลต HTML

 สุดท้ายให้เรียกใช้`Converter.ConvertTemplate` วิธีการเติมเทมเพลต HTML ของคุณด้วยข้อมูลจากแหล่ง JSON

```csharp
Aspose.Html.Converters.Converter.ConvertTemplate(
"template.html", new Aspose.Html.Converters.TemplateData("data-source.json"), new Aspose.Html.Loading.TemplateLoadOptions(), "document.html"
);
```

โค้ดนี้ใช้ไฟล์ "template.html" แทนที่ตัวยึดตำแหน่งด้วยค่า JSON ที่เกี่ยวข้อง และบันทึกผลลัพธ์ใน "document.html"

ยินดีด้วย! คุณได้ควบคุมพลังของ Aspose.HTML สำหรับ .NET เพื่อสร้างเอกสาร HTML แบบไดนามิกจากข้อมูล JSON สำเร็จแล้ว

## บทสรุป

ในบทช่วยสอนนี้ เราได้สำรวจพื้นฐานของการใช้ Aspose.HTML สำหรับ .NET เพื่อสร้างเอกสาร HTML แบบไดนามิก เราครอบคลุมข้อกำหนดเบื้องต้น การนำเข้าเนมสเปซ และแจกแจงรายละเอียดแต่ละขั้นตอนโดยละเอียด ด้วยการทำตามขั้นตอนเหล่านี้ คุณสามารถรวมการสร้างเอกสาร HTML เข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างราบรื่น

## คำถามที่พบบ่อย

### ไตรมาสที่ 1 Aspose.HTML สำหรับ .NET คืออะไร

คำตอบ 1: Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีประสิทธิภาพซึ่งช่วยให้นักพัฒนา .NET สามารถทำงานกับเอกสารและเทมเพลต HTML โดยทางโปรแกรม มันทำให้งานต่างๆ เช่น การสร้าง HTML, การแปลง และการจัดการง่ายขึ้น

### ไตรมาสที่ 2 ฉันจะหาเอกสารสำหรับ Aspose.HTML สำหรับ .NET ได้ที่ไหน

 A2: คุณสามารถเข้าถึงเอกสารประกอบสำหรับ Aspose.HTML สำหรับ .NET ได้[ที่นี่](https://reference.aspose.com/html/net/). โดยให้ข้อมูลที่ครอบคลุม รวมถึงการอ้างอิง API และตัวอย่างโค้ด

### ไตรมาสที่ 3 ฉันจะดาวน์โหลด Aspose.HTML สำหรับ .NET ได้อย่างไร

A3: คุณสามารถดาวน์โหลด Aspose.HTML สำหรับ .NET ได้จากหน้าดาวน์โหลด[ที่นี่](https://releases.aspose.com/html/net/).

### ไตรมาสที่ 4 มีการทดลองใช้ฟรีสำหรับ Aspose.HTML สำหรับ .NET หรือไม่

 A4: ได้ คุณสามารถลองใช้ Aspose.HTML สำหรับ .NET ได้โดยการดาวน์โหลดเวอร์ชันทดลองใช้ฟรีจาก[ที่นี่](https://releases.aspose.com/).

### คำถามที่ 5 ฉันจำเป็นต้องมีใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET หรือไม่

 A5: หากคุณต้องการใบอนุญาตชั่วคราวเพื่อวัตถุประสงค์ในการประเมิน คุณสามารถขอรับใบอนุญาตได้จาก[ที่นี่](https://purchase.aspose.com/temporary-license/).