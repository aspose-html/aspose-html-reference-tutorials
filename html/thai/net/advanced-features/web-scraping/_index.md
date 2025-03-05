---
title: การขูดเว็บใน .NET ด้วย Aspose.HTML
linktitle: การขูดเว็บใน .NET
second_title: API การจัดการ HTML ของ Aspose.HTML .NET
description: เรียนรู้การจัดการเอกสาร HTML ใน .NET ด้วย Aspose.HTML นำทาง กรอง ค้นหา และเลือกองค์ประกอบอย่างมีประสิทธิภาพเพื่อการพัฒนาเว็บที่มีประสิทธิภาพยิ่งขึ้น
type: docs
weight: 13
url: /th/net/advanced-features/web-scraping/
---

ในยุคดิจิทัลทุกวันนี้ การจัดการและดึงข้อมูลจากเอกสาร HTML เป็นงานทั่วไปสำหรับนักพัฒนา Aspose.HTML สำหรับ .NET เป็นเครื่องมืออันทรงพลังที่ช่วยลดความซับซ้อนของการประมวลผลและการจัดการ HTML ในแอปพลิเคชัน .NET ในบทช่วยสอนนี้ เราจะสำรวจแง่มุมต่างๆ ของ Aspose.HTML สำหรับ .NET รวมถึงข้อกำหนดเบื้องต้น เนมสเปซ และตัวอย่างทีละขั้นตอนเพื่อช่วยให้คุณใช้ประโยชน์จากศักยภาพทั้งหมดได้

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเข้าสู่โลกของ Aspose.HTML สำหรับ .NET คุณต้องมีข้อกำหนดเบื้องต้นบางประการ:

1. สภาพแวดล้อมการพัฒนา: ตรวจสอบให้แน่ใจว่าคุณมีสภาพแวดล้อมการพัฒนาที่ใช้งานได้ตั้งค่าด้วย Visual Studio หรือ IDE อื่นที่เข้ากันได้สำหรับการพัฒนา .NET

2.  Aspose.HTML สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารี Aspose.HTML สำหรับ .NET จาก[ลิงค์ดาวน์โหลด](https://releases.aspose.com/html/net/)คุณสามารถเลือกได้ระหว่างเวอร์ชันทดลองใช้งานฟรีหรือเวอร์ชันที่มีลิขสิทธิ์ตามความต้องการของคุณ

3. ความรู้พื้นฐานเกี่ยวกับ HTML: ความคุ้นเคยกับโครงสร้างและองค์ประกอบ HTML ถือเป็นสิ่งสำคัญเพื่อใช้ Aspose.HTML สำหรับ .NET ได้อย่างมีประสิทธิภาพ

## การนำเข้าเนมสเปซ

ในการเริ่มต้น คุณต้องนำเข้าเนมสเปซที่จำเป็นในโปรเจ็กต์ C# ของคุณ เนมสเปซเหล่านี้ให้สิทธิ์ในการเข้าถึงคลาสและฟังก์ชัน Aspose.HTML สำหรับ .NET:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

เมื่อมีข้อกำหนดเบื้องต้นและนำเข้าเนมสเปซแล้ว เรามาดูตัวอย่างสำคัญ ๆ ทีละขั้นตอนเพื่อแสดงให้เห็นวิธีการใช้ Aspose.HTML สำหรับ .NET อย่างมีประสิทธิภาพ

## การนำทางผ่าน HTML

ในตัวอย่างนี้ เราจะนำทางผ่านเอกสาร HTML และเข้าถึงองค์ประกอบต่างๆ ทีละขั้นตอน

```csharp
public static void NavigateThroughHTML()
{
    // เตรียมโค้ด HTML
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // เริ่มต้นเอกสารจากโค้ดที่เตรียมไว้
    using (var document = new HTMLDocument(html_code, "."))
    {
        // รับการอ้างอิงถึงลูกคนแรก (SPAN แรก) ของ BODY
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // เอาท์พุต : สวัสดี

        // รับการอ้างอิงถึงช่องว่างระหว่างองค์ประกอบ HTML
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // เอาท์พุต: ' '

        // รับการอ้างอิงถึงองค์ประกอบ SPAN ที่สอง
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // เอาท์พุท: โลก!
    }
}
```

 ในตัวอย่างนี้ เราสร้างเอกสาร HTML เข้าถึงเอกสารย่อยแรกของเอกสาร (`SPAN` องค์ประกอบ), ช่องว่างระหว่างองค์ประกอบ และองค์ประกอบที่สอง`SPAN` องค์ประกอบที่แสดงการนำทางขั้นพื้นฐาน

## การใช้ตัวกรองโหนด

ตัวกรองโหนดช่วยให้คุณประมวลผลองค์ประกอบเฉพาะต่างๆ ภายในเอกสาร HTML ได้อย่างเลือกสรร

```csharp
public static void NodeFilterUsageExample()
{
    // เตรียมโค้ด HTML
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // สร้างเอกสารเริ่มต้นจากโค้ดที่เตรียมไว้
    using (var document = new HTMLDocument(code, "."))
    {
        // สร้าง TreeWalker ด้วยฟิลเตอร์แบบกำหนดเองสำหรับองค์ประกอบรูปภาพ
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // ผลลัพธ์: image1.png
                // ผลลัพธ์: image2.png
            }
        }
    }
}
```

 ตัวอย่างนี้สาธิตวิธีใช้ตัวกรองโหนดแบบกำหนดเองเพื่อแยกองค์ประกอบเฉพาะ (ในกรณีนี้`IMG` องค์ประกอบ) จากเอกสาร HTML

## แบบสอบถาม XPath

แบบสอบถาม XPath ช่วยให้คุณสามารถค้นหาองค์ประกอบในเอกสาร HTML ตามเงื่อนไขเฉพาะเจาะจง

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
    
    // สร้างเอกสารเริ่มต้นจากโค้ดที่เตรียมไว้
    using (var document = new HTMLDocument(code, "."))
    {
        // ประเมินนิพจน์ XPath เพื่อเลือกองค์ประกอบเฉพาะ
        var result = document.Evaluate("//*[@class='มีความสุข']//ช่วง",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // ทำซ้ำผ่านโหนดที่ได้ผลลัพธ์
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // เอาท์พุต : สวัสดี
            // เอาท์พุท: โลก!
        }
    }
}
```

ตัวอย่างนี้แสดงให้เห็นการใช้แบบสอบถาม XPath เพื่อค้นหาองค์ประกอบในเอกสาร HTML ตามแอตทริบิวต์และโครงสร้าง

## ตัวเลือก CSS

ตัวเลือก CSS ให้ทางเลือกในการเลือกองค์ประกอบในเอกสาร HTML คล้ายกับวิธีที่สไตล์ชีต CSS กำหนดเป้าหมายองค์ประกอบ

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
    
    // สร้างเอกสารเริ่มต้นจากโค้ดที่เตรียมไว้
    using (var document = new HTMLDocument(code, "."))
    {
        //ใช้ตัวเลือก CSS เพื่อแยกองค์ประกอบตามคลาสและลำดับชั้น
        var elements = document.QuerySelectorAll(".happy span");
        
        // ทำซ้ำผ่านรายการองค์ประกอบที่ได้ผลลัพธ์
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // เอาท์พุต : สวัสดี
            // เอาท์พุท: โลก!
        }
    }
}
```

ที่นี่ เราจะสาธิตวิธีการใช้ตัวเลือก CSS เพื่อกำหนดเป้าหมายไปที่องค์ประกอบเฉพาะในเอกสาร HTML

จากตัวอย่างเหล่านี้ คุณจะเข้าใจพื้นฐานเกี่ยวกับการนำทาง การกรอง การสอบถาม และเลือกองค์ประกอบในเอกสาร HTML โดยใช้ Aspose.HTML สำหรับ .NET

## บทสรุป

 Aspose.HTML สำหรับ .NET เป็นไลบรารีที่มีความยืดหยุ่นซึ่งช่วยให้นักพัฒนา .NET สามารถทำงานกับเอกสาร HTML ได้อย่างมีประสิทธิภาพ ด้วยคุณสมบัติอันทรงพลังสำหรับการนำทาง การกรอง การสอบถาม และการเลือกองค์ประกอบ คุณสามารถจัดการงานประมวลผล HTML ต่างๆ ได้อย่างราบรื่น โดยทำตามบทช่วยสอนนี้และสำรวจเอกสารประกอบที่[เอกสาร Aspose.HTML สำหรับ .NET](https://reference.aspose.com/html/net/)คุณสามารถปลดล็อคศักยภาพทั้งหมดของเครื่องมือนี้สำหรับแอปพลิเคชัน .NET ของคุณได้

## คำถามที่พบบ่อย

### คำถามที่ 1. สามารถใช้ Aspose.HTML สำหรับ .NET ได้ฟรีหรือไม่?

A1: Aspose.HTML สำหรับ .NET นำเสนอเวอร์ชันทดลองใช้งานฟรี แต่สำหรับการใช้งานจริง คุณจะต้องซื้อใบอนุญาต คุณสามารถดูรายละเอียดและตัวเลือกใบอนุญาตได้ที่[Aspose.HTML การซื้อ](https://purchase.aspose.com/buy).

### คำถามที่ 2 ฉันจะได้รับใบอนุญาตชั่วคราวสำหรับ Aspose.HTML สำหรับ .NET ได้อย่างไร

 A2: คุณสามารถขอใบอนุญาตชั่วคราวเพื่อวัตถุประสงค์การทดสอบได้จาก[ใบอนุญาตชั่วคราว Aspose.HTML](https://purchase.aspose.com/temporary-license/).

### คำถามที่ 3 ฉันสามารถขอความช่วยเหลือหรือการสนับสนุนสำหรับ Aspose.HTML สำหรับ .NET ได้จากที่ไหน

 A3: หากคุณพบปัญหาหรือมีคำถามใดๆ คุณสามารถเยี่ยมชม[ฟอรั่ม Aspose.HTML](https://forum.aspose.com/) เพื่อความช่วยเหลือและการสนับสนุนจากชุมชน

### คำถามที่ 4 มีแหล่งข้อมูลเพิ่มเติมสำหรับการเรียนรู้ Aspose.HTML สำหรับ .NET หรือไม่

 A4: นอกจากบทช่วยสอนนี้แล้ว คุณยังสามารถสำรวจบทช่วยสอนและเอกสารประกอบเพิ่มเติมได้[หน้าเอกสาร Aspose.HTML สำหรับ .NET](https://reference.aspose.com/html/net/).

### คำถามที่ 5 Aspose.HTML สำหรับ .NET เข้ากันได้กับเวอร์ชัน .NET ล่าสุดหรือไม่

A5: Aspose.HTML สำหรับ .NET ได้รับการอัปเดตเป็นประจำเพื่อให้แน่ใจถึงความเข้ากันได้กับเวอร์ชันและเทคโนโลยี .NET ล่าสุด