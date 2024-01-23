---
title: การสร้างเอกสารใน .NET ด้วย Aspose.HTML
linktitle: การสร้างเอกสารใน .NET
second_title: Aspose.HTML .NET API การจัดการ HTML
description: ปลดปล่อยพลังของ Aspose.HTML สำหรับ .NET เรียนรู้การสร้าง จัดการ และเพิ่มประสิทธิภาพเอกสาร HTML และ SVG ได้อย่างง่ายดาย สำรวจตัวอย่างและคำถามที่พบบ่อยทีละขั้นตอน
type: docs
weight: 14
url: /th/net/html-document-manipulation/creating-a-document/
---

ในโลกของการพัฒนาเว็บที่มีการพัฒนาอยู่ตลอดเวลา การก้าวนำหน้าเป็นสิ่งสำคัญ Aspose.HTML สำหรับ .NET ช่วยให้นักพัฒนามีชุดเครื่องมือที่มีประสิทธิภาพในการทำงานกับเอกสาร HTML ไม่ว่าคุณจะเริ่มต้นใหม่ทั้งหมด โหลดจากไฟล์ ดึงจาก URL หรือจัดการเอกสาร SVG ไลบรารีนี้มอบความสามารถรอบด้านที่คุณต้องการ

ในคำแนะนำทีละขั้นตอนนี้ เราจะเจาะลึกถึงพื้นฐานของการใช้ Aspose.HTML สำหรับ .NET เพื่อให้มั่นใจว่าคุณมีความพร้อมในการใช้เครื่องมืออันทรงพลังนี้ในโครงการพัฒนาเว็บของคุณ ก่อนที่เราจะเจาะลึกรายละเอียด เรามาดูข้อกำหนดเบื้องต้นและเนมสเปซที่จำเป็นเพื่อเริ่มต้นการเดินทางของคุณกันก่อน

## ข้อกำหนดเบื้องต้น

หากต้องการปฏิบัติตามบทช่วยสอนนี้ให้ประสบความสำเร็จและควบคุมประสิทธิภาพของ Aspose.HTML สำหรับ .NET คุณจะต้องมีข้อกำหนดเบื้องต้นต่อไปนี้:

- เครื่อง Windows ที่ติดตั้ง .NET Framework หรือ .NET Core
- โปรแกรมแก้ไขโค้ดเช่น Visual Studio
- ความรู้พื้นฐานเกี่ยวกับการเขียนโปรแกรม C#

ตอนนี้คุณมีข้อกำหนดเบื้องต้นแล้ว เรามาเริ่มต้นกัน

## การนำเข้าเนมสเปซ

ก่อนที่คุณจะเริ่มใช้ Aspose.HTML สำหรับ .NET คุณต้องนำเข้าเนมสเปซที่จำเป็นก่อน เนมสเปซเหล่านี้ประกอบด้วยคลาสและวิธีการที่สำคัญสำหรับการทำงานกับเอกสาร HTML ด้านล่างนี้คือรายการเนมสเปซที่คุณควรนำเข้า:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

เมื่อนำเข้าเนมสเปซเหล่านี้แล้ว คุณก็พร้อมที่จะเจาะลึกตัวอย่างทีละขั้นตอนแล้ว

## การสร้างเอกสาร HTML ตั้งแต่เริ่มต้น

### ขั้นตอนที่ 1: เริ่มต้นเอกสาร HTML ที่ว่างเปล่า

```csharp
// เริ่มต้นเอกสาร HTML ที่ว่างเปล่า
using (var document = new Aspose.Html.HTMLDocument())
{
    // สร้างองค์ประกอบข้อความและเพิ่มลงในเอกสาร
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // บันทึกเอกสารลงดิสก์
    document.Save("document.html");
}
```

ในตัวอย่างนี้ เราเริ่มต้นด้วยการสร้างเอกสาร HTML เปล่าๆ และเพิ่ม "Hello World!" ส่งข้อความถึงมัน จากนั้นเราจะบันทึกเอกสารเป็นไฟล์

## การสร้างเอกสาร HTML จากไฟล์

### ขั้นตอนที่ 1: เตรียมไฟล์ 'document.html'

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### ขั้นตอนที่ 2: โหลดจากไฟล์ 'document.html'

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // เขียนเนื้อหาเอกสารไปยังเอาท์พุตสตรีม
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

ที่นี่เราเตรียมไฟล์ที่มีคำว่า "Hello World!" เนื้อหาแล้วโหลดเป็นเอกสาร HTML เราพิมพ์เนื้อหาของเอกสารไปยังคอนโซล

## การสร้างเอกสาร HTML จาก URL

### ขั้นตอนที่ 1: โหลดเอกสารจากหน้าเว็บ

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // เขียนเนื้อหาเอกสารไปยังเอาท์พุตสตรีม
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

ในตัวอย่างนี้ เราโหลดเอกสาร HTML โดยตรงจากหน้าเว็บและแสดงเนื้อหา

## การสร้างเอกสาร HTML จากสตริง

### ขั้นตอนที่ 1: เตรียมโค้ด HTML

```csharp
var html_code = "<p>Hello World!</p>";
```

### ขั้นตอนที่ 2: เริ่มต้นเอกสารจากตัวแปรสตริง

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // บันทึกเอกสารลงดิสก์
    document.Save("document.html");
}
```

ที่นี่ เราสร้างเอกสาร HTML จากตัวแปรสตริงและบันทึกลงในไฟล์

## การสร้างเอกสาร HTML จาก MemoryStream

### ขั้นตอนที่ 1: สร้างวัตถุสตรีมหน่วยความจำ

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // เขียนโค้ด HTML ลงในวัตถุหน่วยความจำ
    sw.Write("<p>Hello World!</p>");
    // กำหนดตำแหน่งเป็นจุดเริ่มต้น
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // เตรียมใช้งานเอกสารจากสตรีมหน่วยความจำ
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // บันทึกเอกสารลงดิสก์
        document.Save("document.html");
    }
}
```

ในตัวอย่างนี้ เราสร้างเอกสาร HTML จากสตรีมหน่วยความจำและบันทึกลงในไฟล์

## การทำงานกับเอกสาร SVG

### ขั้นตอนที่ 1: เริ่มต้นเอกสาร SVG จากสตริง

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // เขียนเนื้อหาเอกสารไปยังเอาท์พุตสตรีม
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

ที่นี่ เราสร้างและแสดงเอกสาร SVG จากสตริง

## กำลังโหลดเอกสาร HTML แบบอะซิงโครนัส

### ขั้นตอนที่ 1: สร้างอินสแตนซ์ของเอกสาร HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### ขั้นตอนที่ 2: สมัครสมาชิกกิจกรรม 'ReadyStateChange'

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //ตรวจสอบค่าของคุณสมบัติ 'ReadyState'
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### ขั้นตอนที่ 3: นำทางแบบอะซิงโครนัสที่ Uri ที่ระบุ

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

ในตัวอย่างนี้ เราโหลดเอกสาร HTML แบบอะซิงโครนัสและจัดการเหตุการณ์ 'ReadyStateChange' เพื่อแสดงเนื้อหาเมื่อการโหลดเสร็จสมบูรณ์

## การจัดการเหตุการณ์ 'OnLoad'

### ขั้นตอนที่ 1: สร้างอินสแตนซ์ของเอกสาร HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### ขั้นตอนที่ 2: สมัครสมาชิกกิจกรรม 'OnLoad'

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### ขั้นตอนที่ 3: นำทางแบบอะซิงโครนัสที่ Uri ที่ระบุ

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

ตัวอย่างนี้สาธิตการโหลดเอกสาร HTML แบบอะซิงโครนัสและการจัดการเหตุการณ์ 'OnLoad' เพื่อแสดงเนื้อหาเมื่อเสร็จสิ้น

## สรุปแล้ว

ในโลกของการพัฒนาเว็บไซต์แบบไดนามิก การมีเครื่องมือที่เหมาะสมเป็นสิ่งสำคัญ Aspose.HTML สำหรับ .NET ช่วยให้คุณสร้าง จัดการ และประมวลผลเอกสาร HTML และ SVG ได้อย่างมีประสิทธิภาพ คู่มือที่ครอบคลุมนี้ได้อธิบายสิ่งสำคัญต่างๆ ให้คุณทราบ เพื่อให้มั่นใจว่าคุณจะสามารถควบคุมพลังของ Aspose.HTML สำหรับ .NET ในโปรเจ็กต์ของคุณได้

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.HTML สำหรับ .NET คืออะไร

คำตอบ 1: Aspose.HTML สำหรับ .NET เป็นไลบรารี .NET ที่ทรงพลังซึ่งช่วยให้นักพัฒนาสามารถทำงานกับเอกสาร HTML และ SVG ได้ โดยมีคุณสมบัติที่หลากหลาย ตั้งแต่การสร้างเอกสารตั้งแต่เริ่มต้นไปจนถึงการแยกวิเคราะห์และจัดการไฟล์ HTML และ SVG ที่มีอยู่

### คำถามที่ 2: ฉันสามารถใช้ Aspose.HTML สำหรับ .NET กับ .NET Core ได้หรือไม่

ตอบ 2: ใช่ Aspose.HTML สำหรับ .NET เข้ากันได้กับทั้ง .NET Framework และ .NET Core ทำให้เป็นตัวเลือกที่หลากหลายสำหรับแอปพลิเคชัน .NET สมัยใหม่

### คำถามที่ 3: Aspose.HTML สำหรับ .NET เหมาะสำหรับการขูดและแยกวิเคราะห์เว็บหรือไม่

A3: แน่นอน! Aspose.HTML สำหรับ .NET เป็นตัวเลือกที่ยอดเยี่ยมสำหรับงานขูดเว็บและแยกวิเคราะห์ เนื่องจากความสามารถในการโหลดเอกสาร HTML จาก URL และสตริง คุณสามารถดึงข้อมูล ทำการวิเคราะห์ และอื่นๆ อีกมากมาย

### คำถามที่ 4: ฉันจะเข้าถึงการสนับสนุน Aspose.HTML สำหรับ .NET ได้อย่างไร

 A4: หากคุณพบปัญหาใดๆ หรือมีคำถามขณะใช้ Aspose.HTML สำหรับ .NET คุณสามารถไปที่[ตั้งฟอรั่ม](https://forum.aspose.com/) สำหรับการสนับสนุนและความช่วยเหลือจากชุมชนและผู้เชี่ยวชาญของ Aspose

### A5: ฉันจะหาเอกสารโดยละเอียดและตัวเลือกการดาวน์โหลดได้จากที่ไหน?

A5: สำหรับเอกสารประกอบที่ครอบคลุมและการเข้าถึงตัวเลือกการดาวน์โหลด คุณสามารถดูได้จากลิงก์ต่อไปนี้:

- [เอกสารประกอบ](https://reference.aspose.com/html/net/)
- [ดาวน์โหลด](https://releases.aspose.com/html/net/)
- [ซื้อ](https://purchase.aspose.com/buy)
- [ทดลองฟรี](https://releases.aspose.com/)
- [ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/)