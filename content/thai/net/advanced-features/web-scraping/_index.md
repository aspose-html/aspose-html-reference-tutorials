---
title: การขูดเว็บใน .NET ด้วย Aspose.HTML
linktitle: การขูดเว็บใน .NET
second_title: Aspose.HTML .NET API การจัดการ HTML
description: เรียนรู้การจัดการเอกสาร HTML ใน .NET ด้วย Aspose.HTML นำทาง กรอง ค้นหา และเลือกองค์ประกอบอย่างมีประสิทธิภาพเพื่อการพัฒนาเว็บที่ได้รับการปรับปรุง
type: docs
weight: 13
url: /th/net/advanced-features/web-scraping/
---

ในยุคดิจิทัลปัจจุบัน การจัดการและดึงข้อมูลจากเอกสาร HTML ถือเป็นงานทั่วไปสำหรับนักพัฒนา Aspose.HTML สำหรับ .NET เป็นเครื่องมืออันทรงพลังที่ทำให้การประมวลผลและการจัดการ HTML ในแอปพลิเคชัน .NET ง่ายขึ้น ในบทช่วยสอนนี้ เราจะสำรวจแง่มุมต่างๆ ของ Aspose.HTML สำหรับ .NET รวมถึงข้อกำหนดเบื้องต้น เนมสเปซ และตัวอย่างทีละขั้นตอนเพื่อช่วยให้คุณควบคุมศักยภาพของสิ่งนี้ได้อย่างเต็มที่

## ข้อกำหนดเบื้องต้น

ก่อนที่จะดำดิ่งสู่โลกของ Aspose.HTML สำหรับ .NET คุณจะต้องมีข้อกำหนดเบื้องต้นบางประการ:

1. สภาพแวดล้อมการพัฒนา: ตรวจสอบให้แน่ใจว่าคุณมีสภาพแวดล้อมการพัฒนาการทำงานที่ตั้งค่าด้วย Visual Studio หรือ IDE อื่น ๆ ที่เข้ากันได้สำหรับการพัฒนา .NET

2.  Aspose.HTML สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารี Aspose.HTML สำหรับ .NET จากไฟล์[ลิ้งค์ดาวน์โหลด](https://releases.aspose.com/html/net/). คุณสามารถเลือกระหว่างเวอร์ชันทดลองใช้ฟรีหรือเวอร์ชันลิขสิทธิ์ได้ตามความต้องการของคุณ

3. ความรู้พื้นฐานเกี่ยวกับ HTML: ความคุ้นเคยกับโครงสร้างและองค์ประกอบ HTML เป็นสิ่งสำคัญต่อการใช้ Aspose.HTML สำหรับ .NET ได้อย่างมีประสิทธิภาพ

## การนำเข้าเนมสเปซ

ในการเริ่มต้น คุณต้องนำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ C# ของคุณ เนมสเปซเหล่านี้ให้การเข้าถึง Aspose.HTML สำหรับคลาสและฟังก์ชัน .NET:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

เมื่อมีข้อกำหนดเบื้องต้นและนำเข้าเนมสเปซแล้ว เราจะมาแจกแจงตัวอย่างสำคัญบางส่วนทีละขั้นตอนเพื่อแสดงวิธีใช้ Aspose.HTML สำหรับ .NET อย่างมีประสิทธิภาพ

## การนำทางผ่าน HTML

ในตัวอย่างนี้ เราจะนำทางผ่านเอกสาร HTML และเข้าถึงองค์ประกอบต่างๆ ทีละขั้นตอน

```csharp
public static void NavigateThroughHTML()
{
    // เตรียมโค้ด HTML
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // เริ่มต้นเอกสารจากรหัสที่เตรียมไว้
    using (var document = new HTMLDocument(html_code, "."))
    {
        // รับการอ้างอิงถึงลูกคนแรก (SPAN แรก) ของ BODY
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // เอาท์พุต: สวัสดี

        // รับการอ้างอิงถึงช่องว่างระหว่างองค์ประกอบ HTML
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // เอาท์พุต: ''

        // รับการอ้างอิงถึงองค์ประกอบ SPAN ที่สอง
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // เอาท์พุต: โลก!
    }
}
```

 ในตัวอย่างนี้ เราสร้างเอกสาร HTML เข้าถึงรายการลูกคนแรก (a`SPAN` องค์ประกอบ) ช่องว่างระหว่างองค์ประกอบ และส่วนที่สอง`SPAN` องค์ประกอบสาธิตการนำทางขั้นพื้นฐาน

## การใช้ตัวกรองโหนด

ตัวกรองโหนดช่วยให้คุณสามารถเลือกประมวลผลองค์ประกอบเฉพาะภายในเอกสาร HTML ได้

```csharp
public static void NodeFilterUsageExample()
{
    // เตรียมโค้ด HTML
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // เริ่มต้นเอกสารตามรหัสที่เตรียมไว้
    using (var document = new HTMLDocument(code, "."))
    {
        // สร้าง TreeWalker ด้วยฟิลเตอร์แบบกำหนดเองสำหรับองค์ประกอบรูปภาพ
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // เอาท์พุต: image1.png
                // เอาท์พุต: image2.png
            }
        }
    }
}
```

 ตัวอย่างนี้สาธิตวิธีใช้ตัวกรองโหนดที่กำหนดเองเพื่อแยกองค์ประกอบเฉพาะ (ในกรณีนี้`IMG` องค์ประกอบ) จากเอกสาร HTML

## แบบสอบถาม XPath

ข้อความค้นหา XPath ช่วยให้คุณสามารถค้นหาองค์ประกอบในเอกสาร HTML ตามเกณฑ์เฉพาะได้

```csharp
public static void XPathQueryUsageExample()
{
    // เตรียมโค้ด HTML
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello!</span>
            </div>
        </div>
        <p class='happy'>
            <span>World</span>
        </p>
    ";
    
    // เริ่มต้นเอกสารตามรหัสที่เตรียมไว้
    using (var document = new HTMLDocument(code, "."))
    {
        // ประเมินนิพจน์ XPath เพื่อเลือกองค์ประกอบเฉพาะ
        var result = document.Evaluate("//*[@class='happy']//span",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // วนซ้ำโหนดผลลัพธ์
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // เอาท์พุต: สวัสดี
            // เอาท์พุต: โลก!
        }
    }
}
```

ตัวอย่างนี้แสดงการใช้แบบสอบถาม XPath เพื่อค้นหาองค์ประกอบในเอกสาร HTML ตามคุณลักษณะและโครงสร้าง

## ตัวเลือก CSS

ตัวเลือก CSS เป็นทางเลือกในการเลือกองค์ประกอบในเอกสาร HTML คล้ายกับวิธีที่ CSS สไตล์ชีตกำหนดเป้าหมายองค์ประกอบ

```csharp
public static void CSSSelectorUsageExample()
{
    // เตรียมโค้ด HTML
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello</span>
            </div>
        </div>
        <p class='happy'>
            <span>World!</span>
        </p>
    ";
    
    // เริ่มต้นเอกสารตามรหัสที่เตรียมไว้
    using (var document = new HTMLDocument(code, "."))
    {
        //ใช้ตัวเลือก CSS เพื่อแยกองค์ประกอบตามคลาสและลำดับชั้น
        var elements = document.QuerySelectorAll(".happy span");
        
        // วนซ้ำรายการองค์ประกอบผลลัพธ์
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // เอาท์พุต: สวัสดี
            // เอาท์พุต: โลก!
        }
    }
}
```

ที่นี่ เราจะสาธิตวิธีการใช้ตัวเลือก CSS เพื่อกำหนดเป้าหมายองค์ประกอบเฉพาะในเอกสาร HTML

จากตัวอย่างเหล่านี้ คุณได้รับความเข้าใจพื้นฐานเกี่ยวกับวิธีการนำทาง กรอง สืบค้น และเลือกองค์ประกอบในเอกสาร HTML โดยใช้ Aspose.HTML สำหรับ .NET

## บทสรุป

 Aspose.HTML สำหรับ .NET เป็นไลบรารีอเนกประสงค์ที่ช่วยให้นักพัฒนา .NET สามารถทำงานกับเอกสาร HTML ได้อย่างมีประสิทธิภาพ ด้วยคุณสมบัติอันทรงพลังสำหรับการนำทาง การกรอง การสืบค้น และการเลือกองค์ประกอบ คุณสามารถจัดการงานการประมวลผล HTML ต่างๆ ได้อย่างราบรื่น โดยทำตามบทช่วยสอนนี้และสำรวจเอกสารประกอบที่[Aspose.HTML สำหรับเอกสารประกอบ .NET](https://reference.aspose.com/html/net/)คุณสามารถปลดล็อกศักยภาพสูงสุดของเครื่องมือนี้สำหรับแอปพลิเคชัน .NET ของคุณได้

## คำถามที่พบบ่อย

### ไตรมาสที่ 1 Aspose.HTML สำหรับ .NET ใช้งานได้ฟรีหรือไม่

ตอบ 1: Aspose.HTML สำหรับ .NET มีเวอร์ชันทดลองใช้ฟรี แต่สำหรับการใช้งานจริง คุณจะต้องซื้อใบอนุญาต คุณสามารถดูรายละเอียดใบอนุญาตและตัวเลือกต่างๆ ได้ที่[Aspose.HTML ซื้อ](https://purchase.aspose.com/buy).

### ไตรมาสที่ 2 ฉันจะรับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET ได้อย่างไร

 A2: คุณสามารถขอรับใบอนุญาตชั่วคราวเพื่อการทดสอบได้จาก[Aspose.HTML ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/).

### ไตรมาสที่ 3 ฉันจะขอความช่วยเหลือหรือสนับสนุน Aspose.HTML สำหรับ .NET ได้ที่ไหน

 A3: หากคุณพบปัญหาใด ๆ หรือมีคำถาม คุณสามารถไปที่[Aspose.HTML ฟอรั่ม](https://forum.aspose.com/) เพื่อช่วยเหลือและสนับสนุนชุมชน

### ไตรมาสที่ 4 มีแหล่งข้อมูลเพิ่มเติมสำหรับการเรียนรู้ Aspose.HTML สำหรับ .NET หรือไม่

 A4: นอกจากบทช่วยสอนนี้แล้ว คุณยังสามารถสำรวจบทช่วยสอนและเอกสารประกอบเพิ่มเติมเกี่ยวกับ[หน้าเอกสารประกอบ Aspose.HTML สำหรับ .NET](https://reference.aspose.com/html/net/).

### คำถามที่ 5 Aspose.HTML สำหรับ .NET เข้ากันได้กับ .NET เวอร์ชันล่าสุดหรือไม่

A5: Aspose.HTML สำหรับ .NET ได้รับการอัปเดตเป็นประจำเพื่อให้มั่นใจว่าสามารถใช้งานร่วมกับ .NET เวอร์ชันและเทคโนโลยีล่าสุดได้