---
category: general
date: 2026-10-09
description: สร้างอินสแตนซ์ของ ImageRenderingOptions เพื่อเปิดใช้งานการทำแอนตี้เอเลียสและปรับปรุงคุณภาพการเรนเดอร์กราฟิกในแอปพลิเคชัน
  .NET
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create imagerenderingoptions instance
- ImageRenderingOptions
- antialiasing
- SmoothingMode
- graphics rendering
language: th
lastmod: 2026-10-09
og_description: สร้างอินสแตนซ์ของ ImageRenderingOptions เพื่อเปิดใช้งานการแอนตี้เอเลียซิ่งและทำให้การเรนเดอร์กราฟิกใน
  .NET ราบรื่นยิ่งขึ้น ตามคู่มือขั้นตอนต่อขั้นตอน
og_image_alt: Screenshot showing smooth edges after enabling antialiasing with ImageRenderingOptions
og_title: สร้างอินสแตนซ์ ImageRenderingOptions – เพิ่มคุณภาพกราฟิกใน .NET
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  headline: Create imagerenderingoptions instance for high‑quality graphics rendering
  type: TechArticle
- description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  name: Create imagerenderingoptions instance for high‑quality graphics rendering
  steps:
  - name: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
    text: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
  - name: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
    text: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
  - name: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
    text: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
  type: HowTo
tags:
- .NET
- C#
- rendering
title: สร้างอินสแตนซ์ imagerenderingoptions สำหรับการเรนเดอร์กราฟิกคุณภาพสูง
url: /th/net/canvas-and-image-manipulation/create-imagerenderingoptions-instance-for-high-quality-graph/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างอินสแตนซ์ imagerenderingoptions สำหรับการเรนเดอร์กราฟิกคุณภาพสูง

หากคุณต้องการ **สร้างอินสแตนซ์ imagerenderingoptions** เพื่อสร้างกราฟิกที่เรียบเนียนขึ้น คู่มือนี้จะแสดงวิธีทำอย่างละเอียด โดยการกำหนดค่า antialiasing คุณจะกำจัดขอบหยักและได้ผลลัพธ์ระดับมืออาชีพโดยไม่ต้องใช้ไลบรารีเพิ่มเติม

คุณจะได้เรียนรู้วิธีสร้างอินสแตนซ์ `ImageRenderingOptions` เปิดใช้งาน antialiasing และแนบตัวเลือกเหล่านี้ไปยังเอนจินการเรนเดอร์ เช่น Aspose.Slides หรือ System.Drawing บทเรียนนี้สมมติว่าคุณคุ้นเคยกับไวยากรณ์พื้นฐานของ C# และมีสภาพแวดล้อมการพัฒนา .NET พร้อมใช้งาน

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (API มีให้ใช้ใน .NET Standard 2.0+)
- การอ้างอิงไปยัง assembly ที่มี `ImageRenderingOptions` (เช่น `Aspose.Slides.NET`)
- IDE เช่น Visual Studio 2022 หรือ VS Code พร้อมส่วนขยาย C#
- ความเข้าใจพื้นฐานเกี่ยวกับ pipeline การเรนเดอร์กราฟิก

## ขั้นตอนที่ 1: สร้างอินสแตนซ์ imagerenderingoptions

การดำเนินการแรกคือการจัดสรรอ็อบเจ็กต์ `ImageRenderingOptions` ใหม่ ซึ่งอ็อบเจ็กต์นี้ทำหน้าที่เป็นคอนเทนเนอร์สำหรับแฟล็กทั้งหมดที่เกี่ยวข้องกับการเรนเดอร์

```csharp
using Aspose.Slides;          // Replace with the appropriate namespace
using Aspose.Slides.Export;   // Needed for ImageRenderingOptions

// Step 1: Create the ImageRenderingOptions instance
ImageRenderingOptions imgOptions = new ImageRenderingOptions();
```

การสร้างอินสแตนซ์นี้ให้คุณควบคุมเต็มที่ว่ากราฟิกเวกเตอร์จะถูกแปลงเป็นแรสเตอร์อย่างไร คุณสามารถเปิดหรือปิดฟีเจอร์เฉพาะได้ในภายหลัง เช่น antialiasing, โหมดการเรนเดอร์ข้อความ หรือการบีบอัดภาพ

## ขั้นตอนที่ 2: เปิดใช้งาน antialiasing เพื่อปรับปรุงการเรนเดอร์กราฟิก

Antialiasing ทำให้การเปลี่ยนแปลงสีพิกเซลราบรื่นขึ้น ลดเอฟเฟกต์ขั้นบันไดบนเส้นทแยงหรือเส้นโค้ง คุณสมบัติ `SmoothingMode` รุ่นเก่าได้ถูกยกเลิกแล้ว; `UseAntialiasing` เป็นวิธีสมัยใหม่ที่แนะนำ

```csharp
// Step 2: Turn on antialiasing for smoother output
imgOptions.UseAntialiasing = true;
```

การตั้งค่า `UseAntialiasing` เป็น `true` จะบอกเอนจินการเรนเดอร์ให้ใช้ฟิลเตอร์คุณภาพสูงระหว่างการแปลงเป็นแรสเตอร์ แฟล็กนี้ทำงานกับรูปทรงเวกเตอร์และข้อความทั้งสองประเภท เพื่อให้ความคมชัดของภาพสอดคล้องกันทั่วทั้งสไลด์

### ทำไมไม่ใช้ SmoothingMode?

`SmoothingMode` เป็นของ `System.Drawing.Graphics` และมีผลต่อการวาดด้วย GDI+ เท่านั้น เมื่อคุณเรนเดอร์สไลด์หรือ PDF ผ่าน Aspose.Slides, `ImageRenderingOptions.UseAntialiasing` จะเป็นแฟล็กเดียวที่ไลบรารียอมรับ การใช้คุณสมบัติใหม่นี้รับประกันความเข้ากันได้ในอนาคตและกำจัดพฤติกรรมที่ไม่คาดคิดบนแพลตฟอร์มที่ไม่ใช่ Windows

## ขั้นตอนที่ 3: นำตัวเลือกไปใช้กับการดำเนินการเรนเดอร์

เมื่ออินสแตนซ์ `ImageRenderingOptions` ถูกกำหนดค่าแล้ว ให้นำไปส่งให้เมธอดที่ทำการเรนเดอร์จริง ตัวอย่างต่อไปนี้เป็นโค้ดที่สมบูรณ์และสามารถรันได้ ซึ่งโหลดงานนำเสนอ, เรนเดอร์สไลด์แรกเป็น PNG, และบันทึกภาพพร้อมเปิดใช้งาน antialiasing

```csharp
using System;
using Aspose.Slides;
using Aspose.Slides.Export;

class Program
{
    static void Main()
    {
        // Load a sample presentation
        using Presentation pres = new Presentation("sample.pptx");

        // Create and configure ImageRenderingOptions
        ImageRenderingOptions imgOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true   // Enable antialiasing
        };

        // Render the first slide to a PNG file
        Slide slide = pres.Slides[0];
        slide.GetThumbnail(2f, 2f, imgOptions)   // 2x scale for higher resolution
            .Save("slide1_antialiased.png", Export.SaveFormat.Png);

        Console.WriteLine("Slide rendered with antialiasing.");
    }
}
```

**คำอธิบายบรรทัดสำคัญ**

- `new Presentation("sample.pptx")` โหลดไฟล์ต้นฉบับ  
- `GetThumbnail(2f, 2f, imgOptions)` สร้างบิตแมพของสไลด์ที่ความละเอียดสองเท่าของ DPI เริ่มต้น พร้อมใช้ตัวเลือกการเรนเดอร์ที่คุณกำหนด  
- PNG ที่ได้ (`slide1_antialiased.png`) แสดงเส้นโค้งและข้อความที่ราบรื่นด้วย `UseAntialiasing = true`

### ผลลัพธ์ที่คาดหวัง

เปิด `slide1_antialiased.png` ด้วยโปรแกรมดูภาพใดก็ได้ เมื่อเทียบกับการเรนเดอร์ที่ไม่มี antialiasing คุณจะสังเกตเห็นว่า:

- มุมโค้งของรูปทรงปรากฏโดยไม่มีขั้นบันไดหยัก  
- ขอบข้อความคมชัดแต่มีความนุ่มนวล ลดอาการพิกเซลเป็นจุด  
- คุณภาพภาพโดยรวมตรงกับที่คุณเห็นในมุมมอง PowerPoint ดั้งเดิม

## ขั้นตอนที่ 4: การปรับแต่งเพิ่มเติมสำหรับการเรนเดอร์กราฟิกขั้นสูง

แม้ว่า antialiasing จะเป็นแฟล็กที่ใช้บ่อยที่สุด `ImageRenderingOptions` ยังมีการควบคุมเพิ่มเติม:

| Property | วัตถุประสงค์ | ค่าที่มักใช้ |
|----------|--------------|------------|
| `UseHighQualityRendering` | เปิดใช้งานการเรนเดอร์ระดับ sub‑pixel สำหรับข้อความ | `true` |
| `PixelFormat` | กำหนดความลึกสีของบิตแมพผลลัพธ์ | `PixelFormat.Format32bppArgb` |
| `ImageFormat` | ตั้งค่าฟอร์แมตของภาพเป้าหมาย (PNG, JPEG ฯลฯ) | `Export.SaveFormat.Png` |

คุณสามารถเชื่อมต่อการตั้งค่าเหล่านี้ได้:

```csharp
imgOptions.UseHighQualityRendering = true;
imgOptions.PixelFormat = System.Drawing.Imaging.PixelFormat.Format32bppArgb;
```

**เคล็ดลับ:** เมื่อสร้าง PDF ขนาดใหญ่หรือ PNG ความละเอียดสูง ให้เปิด `UseAntialiasing` ไว้แต่ควรตรวจสอบการใช้หน่วยความจำ Antialiasing จะเพิ่มภาระการประมวลผลเพิ่มเติม ซึ่งอาจสังเกตได้บนเครื่องที่สเปคต่ำ

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

1. **ลืมส่งตัวเลือก** – เมธอดการเรนเดอร์ที่รับ `ImageRenderingOptions` จะละเลย antialiasing หากคุณเรียก overload โดยไม่ส่งพารามิเตอร์ตัวเลือก ควรใช้ `GetThumbnail` แบบสามพารามิเตอร์หรือเมธอดที่เทียบเท่าเสมอ  
2. **ผสมผสาน SmoothingMode กับ ImageRenderingOptions** – การตั้งค่า `Graphics.SmoothingMode` ไม่มีผลต่อการเรนเดอร์ของ Aspose.Slides ควรพึ่งพา `UseAntialiasing` เท่านั้น  
3. **ใช้ไลบรารีเวอร์ชันเก่า** – `ImageRenderingOptions` ถูกเพิ่มใน Aspose.Slides 20.5 ตรวจสอบให้แน่ใจว่าแพคเกจ NuGet ของคุณเป็นเวอร์ชันล่าสุด มิฉะนั้นคลาสอาจไม่มีหรือไม่มีคุณสมบัติ `UseAntialiasing`

## สรุป

ตอนนี้คุณรู้วิธี **สร้างอินสแตนซ์ imagerenderingoptions**, เปิดใช้งาน antialiasing, และรวมตัวเลือกเหล่านี้เข้าในกระบวนการเรนเดอร์ วิธีนี้รับประกันการเรนเดอร์กราฟิกที่ราบรื่นขึ้น, แทนที่การตั้งค่า `SmoothingMode` แบบเก่า, และทำงานอย่างสม่ำเสมอบนแพลตฟอร์ม .NET ทั้งหมด

จากนี้คุณสามารถสำรวจแฟล็กการเรนเดอร์เพิ่มเติม, ทดลองสเกล DPI ต่าง ๆ, หรือผสานเทคนิคนี้กับการส่งออก PDF เพื่อสร้างสินทรัพย์คุณภาพพิมพ์ การเชี่ยวชาญ `ImageRenderingOptions` เป็นพื้นฐานสำคัญของการเขียนโปรแกรมกราฟิก .NET คุณภาพสูง

---

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญคุณลักษณะ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโครงการของคุณ

- [Create PNG from HTML – Full C# Rendering Guide](/html/english/net/rendering-html-documents/create-png-from-html-full-c-rendering-guide/)
- [Create image from HTML in C# – Complete Step‑by‑Step Guide](/html/english/net/rendering-html-documents/create-image-from-html-in-c-complete-step-by-step-guide/)
- [Create canvas text – Full Guide to Rendering Text on Images](/html/english/net/canvas-and-image-manipulation/create-canvas-text-full-guide-to-rendering-text-on-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}