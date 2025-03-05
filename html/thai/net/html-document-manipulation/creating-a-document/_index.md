---
title: การสร้างเอกสารใน .NET ด้วย Aspose.HTML
linktitle: การสร้างเอกสารใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: ปลดปล่อยพลังของ Aspose.HTML สำหรับ .NET เรียนรู้การสร้าง จัดการ และเพิ่มประสิทธิภาพเอกสาร HTML และ SVG ได้อย่างง่ายดาย สำรวจตัวอย่างทีละขั้นตอนและคำถามที่พบบ่อย
type: docs
weight: 14
url: /th/net/html-document-manipulation/creating-a-document/
---

ในโลกของการพัฒนาเว็บที่เปลี่ยนแปลงอยู่ตลอดเวลา การก้าวไปข้างหน้าถือเป็นสิ่งสำคัญ Aspose.HTML สำหรับ .NET มอบชุดเครื่องมืออันแข็งแกร่งให้กับนักพัฒนาเพื่อทำงานกับเอกสาร HTML ไม่ว่าคุณจะเริ่มต้นจากศูนย์ โหลดจากไฟล์ ดึงข้อมูลจาก URL หรือจัดการเอกสาร SVG ไลบรารีนี้มอบความคล่องตัวที่คุณต้องการ

ในคู่มือทีละขั้นตอนนี้ เราจะเจาะลึกถึงหลักพื้นฐานของการใช้ Aspose.HTML สำหรับ .NET เพื่อให้แน่ใจว่าคุณมีอุปกรณ์ครบครันเพื่อใช้เครื่องมืออันทรงพลังนี้ในโครงการพัฒนาเว็บของคุณ ก่อนที่เราจะเจาะลึกในรายละเอียด มาดูข้อกำหนดเบื้องต้นและเนมสเปซที่จำเป็นเพื่อเริ่มต้นการเดินทางของคุณกันก่อน

## ข้อกำหนดเบื้องต้น

หากต้องการทำตามบทช่วยสอนนี้และใช้พลังของ Aspose.HTML สำหรับ .NET ได้สำเร็จ คุณจะต้องมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

- เครื่อง Windows ที่มีการติดตั้ง .NET Framework หรือ .NET Core
- โปรแกรมแก้ไขโค้ดเช่น Visual Studio
- ความรู้พื้นฐานในการเขียนโปรแกรม C#

ตอนนี้คุณมีข้อกำหนดเบื้องต้นแล้ว มาเริ่มกันเลย

## การนำเข้าเนมสเปซ

ก่อนที่คุณจะเริ่มใช้ Aspose.HTML สำหรับ .NET คุณต้องนำเข้าเนมสเปซที่จำเป็นก่อน เนมสเปซเหล่านี้ประกอบด้วยคลาสและเมธอดที่สำคัญสำหรับการทำงานกับเอกสาร HTML ด้านล่างนี้คือรายการเนมสเปซที่คุณควรนำเข้า:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

เมื่อนำเนมสเปซเหล่านี้เข้ามาแล้ว คุณก็พร้อมที่จะเจาะลึกตัวอย่างทีละขั้นตอนได้แล้ว

## การสร้างเอกสาร HTML จากเริ่มต้น

### ขั้นตอนที่ 1: สร้างเอกสาร HTML ที่ว่างเปล่า

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

ในตัวอย่างนี้ เราจะเริ่มต้นด้วยการสร้างเอกสาร HTML เปล่าและเพิ่มข้อความ "Hello World!" ลงไป จากนั้นเราจะบันทึกเอกสารลงในไฟล์

## การสร้างเอกสาร HTML จากไฟล์

### ขั้นตอนที่ 1: เตรียมไฟล์ 'document.html'

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### ขั้นตอนที่ 2: โหลดจากไฟล์ 'document.html'

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // เขียนเนื้อหาเอกสารลงในสตรีมเอาต์พุต
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

ที่นี่ เราเตรียมไฟล์ที่มีเนื้อหา "Hello World!" แล้วโหลดเป็นเอกสาร HTML จากนั้นพิมพ์เนื้อหาของเอกสารไปยังคอนโซล

## การสร้างเอกสาร HTML จาก URL

### ขั้นตอนที่ 1: โหลดเอกสารจากหน้าเว็บ

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // เขียนเนื้อหาเอกสารลงในสตรีมเอาต์พุต
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

ในตัวอย่างนี้ เราโหลดเอกสาร HTML โดยตรงจากเว็บเพจและแสดงเนื้อหาของเอกสารนั้น

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

ที่นี่เราสร้างเอกสาร HTML จากตัวแปรสตริงและบันทึกลงในไฟล์

## การสร้างเอกสาร HTML จาก MemoryStream

### ขั้นตอนที่ 1: สร้างวัตถุสตรีมหน่วยความจำ

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // เขียนโค้ด HTML ลงในอ็อบเจ็กต์หน่วยความจำ
    sw.Write("<p>Hello World!</p>");
    // ตั้งค่าตำแหน่งไว้ที่จุดเริ่มต้น
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // เริ่มต้นเอกสารจากสตรีมหน่วยความจำ
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // บันทึกเอกสารลงดิสก์
        document.Save("document.html");
    }
}
```

ในตัวอย่างนี้ เราจะสร้างเอกสาร HTML จากสตรีมหน่วยความจำและบันทึกลงในไฟล์

## การทำงานกับเอกสาร SVG

### ขั้นตอนที่ 1: เริ่มต้นเอกสาร SVG จากสตริง

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // เขียนเนื้อหาเอกสารลงในสตรีมเอาต์พุต
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

ที่นี่ เราสร้างและแสดงเอกสาร SVG จากสตริง

## การโหลดเอกสาร HTML แบบอะซิงโครนัส

### ขั้นตอนที่ 1: สร้างอินสแตนซ์ของเอกสาร HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### ขั้นตอนที่ 2: สมัครรับเหตุการณ์ 'ReadyStateChange'

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    // ตรวจสอบค่าคุณสมบัติ 'ReadyState'
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

ในตัวอย่างนี้ เราโหลดเอกสาร HTML แบบอะซิงโครนัสและจัดการเหตุการณ์ 'ReadyStateChange' เพื่อแสดงเนื้อหาเมื่อการโหลดเสร็จสิ้น

## การจัดการเหตุการณ์ 'OnLoad'

### ขั้นตอนที่ 1: สร้างอินสแตนซ์ของเอกสาร HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### ขั้นตอนที่ 2: สมัครรับข่าวสาร 'OnLoad'

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

ตัวอย่างนี้สาธิตการโหลดเอกสาร HTML แบบอะซิงโครนัสและการจัดการเหตุการณ์ 'OnLoad' เพื่อแสดงเนื้อหาเมื่อเสร็จสมบูรณ์

## สรุปแล้ว

ในโลกของการพัฒนาเว็บที่เปลี่ยนแปลงตลอดเวลา การมีเครื่องมือที่เหมาะสมถือเป็นสิ่งสำคัญ Aspose.HTML สำหรับ .NET ช่วยให้คุณสร้าง จัดการ และประมวลผลเอกสาร HTML และ SVG ได้อย่างมีประสิทธิภาพ คู่มือฉบับสมบูรณ์นี้จะแนะนำคุณเกี่ยวกับสิ่งสำคัญต่างๆ เพื่อให้แน่ใจว่าคุณสามารถใช้ Aspose.HTML สำหรับ .NET ในโครงการของคุณได้อย่างเต็มที่

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.HTML สำหรับ .NET คืออะไร?

A1: Aspose.HTML สำหรับ .NET เป็นไลบรารี .NET ที่ทรงพลังซึ่งช่วยให้นักพัฒนาสามารถทำงานกับเอกสาร HTML และ SVG ได้ โดยมีคุณสมบัติมากมายตั้งแต่การสร้างเอกสารตั้งแต่ต้นจนถึงการแยกวิเคราะห์และจัดการไฟล์ HTML และ SVG ที่มีอยู่

### คำถามที่ 2: ฉันสามารถใช้ Aspose.HTML สำหรับ .NET กับ .NET Core ได้หรือไม่

A2: ใช่ Aspose.HTML สำหรับ .NET เข้ากันได้กับทั้ง .NET Framework และ .NET Core ทำให้เป็นตัวเลือกที่หลากหลายสำหรับแอปพลิเคชัน .NET สมัยใหม่

### คำถามที่ 3: Aspose.HTML สำหรับ .NET เหมาะกับการสแกนและแยกวิเคราะห์เว็บหรือไม่

A3: อย่างแน่นอน! Aspose.HTML สำหรับ .NET เป็นตัวเลือกที่ยอดเยี่ยมสำหรับงานการขูดข้อมูลและการแยกวิเคราะห์เว็บ เนื่องจากสามารถโหลดเอกสาร HTML จาก URL และสตริงได้ คุณสามารถดึงข้อมูล ดำเนินการวิเคราะห์ และอื่นๆ อีกมากมาย

### คำถามที่ 4: ฉันสามารถเข้าถึงการสนับสนุน Aspose.HTML สำหรับ .NET ได้อย่างไร

 A4: หากคุณพบปัญหาหรือมีคำถามขณะใช้ Aspose.HTML สำหรับ .NET คุณสามารถไปที่[ฟอรั่ม Aspose](https://forum.aspose.com/) เพื่อรับการสนับสนุนและความช่วยเหลือจากชุมชนและผู้เชี่ยวชาญ Aspose

### A5: ฉันสามารถหาเอกสารรายละเอียดและตัวเลือกการดาวน์โหลดได้ที่ไหน

A5: สำหรับเอกสารประกอบที่ครอบคลุมและการเข้าถึงตัวเลือกการดาวน์โหลด คุณสามารถดูได้จากลิงก์ต่อไปนี้:

- [เอกสารประกอบ](https://reference.aspose.com/html/net/)
- [ดาวน์โหลด](https://releases.aspose.com/html/net/)
- [ซื้อ](https://purchase.aspose.com/buy)
- [ทดลองใช้งานฟรี](https://releases.aspose.com/)
- [ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/)