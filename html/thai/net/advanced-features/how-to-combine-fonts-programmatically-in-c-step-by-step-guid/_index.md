---
category: general
date: 2025-12-26
description: วิธีรวมฟอนต์ใน C# ด้วยตัวดำเนินการบิต – เรียนรู้การตั้งค่าสไตล์ฟอนต์แบบโปรแกรมและการใช้หลายสไตล์ฟอนต์อย่างมีประสิทธิภาพ
draft: false
keywords:
- how to combine fonts
- set font style programmatically
- how to set font
- combine font styles
- apply multiple font styles
language: th
og_description: วิธีรวมฟอนต์ใน C# อย่างรวดเร็ว คู่มือนี้จะแสดงวิธีตั้งค่ารูปแบบฟอนต์โดยโปรแกรมและใช้หลายรูปแบบฟอนต์พร้อมตัวอย่างที่ชัดเจน
og_title: วิธีรวมฟอนต์ใน C# – คู่มือการเขียนโปรแกรมครบถ้วน
tags:
- C#
- graphics
- typography
title: วิธีรวมฟอนต์โดยใช้โปรแกรมใน C# – คู่มือขั้นตอนโดยละเอียด
url: /th/net/advanced-features/how-to-combine-fonts-programmatically-in-c-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีรวมฟอนต์โดยโปรแกรมใน C#

เคยสงสัย **วิธีรวมฟอนต์** ในบรรทัดเดียวของโค้ด C# ไหม? บางทีคุณอาจกำลังสร้างเว็บ‑เอดิเตอร์, ตัวสร้าง PDF, หรือ UI ของเกม, และต้องการข้อความที่ **หนา** *และ* *เอียง* พร้อมกัน ข่าวดีคือคุณไม่ต้องเขียนหลายคำสั่ง—แค่เทคนิคบิตไวส์เล็ก ๆ แล้วคุณก็พร้อมใช้งาน

ในบทเรียนนี้เราจะอธิบาย **วิธีตั้งค่าแบบอักษร** ผ่านโปรแกรม, สำรวจตัวดำเนินการ `|` (bitwise OR) สำหรับการรวมแฟล็ก `WebFontStyle`, และแสดงวิธี **ใช้หลายสไตล์ฟอนต์** โดยไม่สับสนกับ overloads ต่าง ๆ เมื่อจบคุณจะได้ตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งคุณสามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้

> **สรุปสั้น:** ใช้ `WebFontStyle.Bold | WebFontStyle.Italic` (หรือการผสมใด ๆ) แล้วกำหนดผลลัพธ์ให้กับ `GraphicContext.FontStyle` เพียงเท่านี้ก็ **รวมสไตล์ฟอนต์** ได้แล้ว

---

## สิ่งที่คุณต้องเตรียม

ก่อนที่เราจะลงลึก, ตรวจสอบให้แน่ใจว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า (API ที่เราใช้เป็นส่วนหนึ่งของไลบรารีกราฟิกสมมติ, แต่รูปแบบนี้ทำงานกับ `Flags` enum ใดก็ได้)
* สภาพแวดล้อมการพัฒนา—Visual Studio, Rider, หรือ VS Code ก็ได้
* ความคุ้นเคยพื้นฐานกับ enum ของ C# และตัวดำเนินการบิตไวส์

ไม่ต้องติดตั้ง NuGet แพคเกจเพิ่มเติมสำหรับตัวอย่างหลัก; เราจะใช้คลาส stub `GraphicContext` แบบ minimal เพื่อให้ทุกอย่างอยู่ในไฟล์เดียว

---

## วิธีรวมฟอนต์ใน C# – แนวคิดหลัก

หัวใจของ **วิธีรวมฟอนต์** อยู่ที่การที่ `WebFontStyle` ถูกกำหนดด้วยแอตทริบิวต์ `[Flags]` ซึ่งบอก CLR ว่าแต่ละค่า enum แทนบิตเดียว, และคุณสามารถผสานมันด้วยตัวดำเนินการ bitwise OR (`|`) ได้อย่างปลอดภัย ผลลัพธ์คือจำนวนเต็มหนึ่งค่า ที่บิตแต่ละบิตสื่อถึงสไตล์ที่เลือก

```csharp
// Define the enum – each value occupies a distinct bit.
[Flags]
public enum WebFontStyle
{
    Regular = 0,
    Bold    = 1 << 0,   // 0001
    Italic  = 1 << 1,   // 0010
    Underline = 1 << 2 // 0100
    // Add more styles as needed
}
```

เมื่อคุณเขียน `WebFontStyle.Bold | WebFontStyle.Italic` คอมไพเลอร์จะสร้างค่าที่มีการแสดงผลเป็นไบนารี `0011`. คลาส `GraphicContext` จะอ่านบิตเหล่านี้และเรนเดอร์ข้อความตามสไตล์ที่กำหนด

---

## การทำงานทีละขั้นตอน

ด้านล่างเป็น **โปรแกรมที่ทำงานได้เต็มรูปแบบ** ที่แสดงขั้นตอนทั้งหมด—from การสร้าง graphics context ไปจนถึง **การตั้งค่าสไตล์ฟอนต์โดยโปรแกรม** และสุดท้าย **การใช้หลายสไตล์ฟอนต์** กับข้อความหนึ่งบรรทัด

### 1️⃣ สร้าง Graphic Context ขั้นพื้นฐาน

ก่อนอื่นเราต้องมีพื้นผิวสำหรับวาด ในโปรเจกต์จริงคุณอาจใช้ `System.Drawing.Graphics` หรือ canvas ของบุคคลที่สาม, แต่เพื่อความชัดเจนเราจะ stub คลาสง่าย ๆ

```csharp
using System;

public class GraphicContext
{
    // The FontStyle property accepts a combination of WebFontStyle flags.
    public WebFontStyle FontStyle { get; set; } = WebFontStyle.Regular;

    // Simulated draw method – in a real app this would render to screen or PDF.
    public void DrawString(string text)
    {
        Console.WriteLine($"Drawing text: \"{text}\" with style: {FontStyle}");
        // Here you would normally pass FontStyle to the underlying rendering engine.
    }
}
```

### 2️⃣ รวมสไตล์ที่ต้องการ

ต่อไปเราจะ **รวมสไตล์ฟอนต์** จริง ๆ นี่คือส่วนที่ตอบคำถาม “วิธีรวมฟอนต์” โดยตรง

```csharp
// Combine Bold and Italic using the bitwise OR operator.
WebFontStyle combinedStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

คุณสามารถเพิ่มแฟล็กอื่น ๆ หากต้องการขีดเส้นใต้, เส้นขีดฆ่า, หรือสไตล์กำหนดเองที่ไลบรารีของคุณรองรับ:

```csharp
WebFontStyle fancyStyle = WebFontStyle.Bold | WebFontStyle.Italic | WebFontStyle.Underline;
```

### 3️⃣ นำสไตล์ที่รวมแล้วไปใช้กับ Context

สุดท้ายกำหนดค่าที่รวมแล้วให้กับ `GraphicContext` แล้ววาดอะไรสักอย่าง

```csharp
GraphicContext graphicContext = new GraphicContext();

// Apply the combined style.
graphicContext.FontStyle = combinedStyle;

// Render a sample string.
graphicContext.DrawString("Hello, combined fonts!");
```

### 4️⃣ โปรแกรมเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน, นี่คือไฟล์ซอร์สทั้งหมดที่คุณสามารถคัดลอก, วาง, และรันได้:

```csharp
using System;

[Flags]
public enum WebFontStyle
{
    Regular   = 0,
    Bold      = 1 << 0,   // 0001
    Italic    = 1 << 1,   // 0010
    Underline = 1 << 2    // 0100
    // Extend with more styles as needed.
}

public class GraphicContext
{
    public WebFontStyle FontStyle { get; set; } = WebFontStyle.Regular;

    public void DrawString(string text)
    {
        // In a real graphics library you would pass FontStyle to the renderer.
        Console.WriteLine($"Drawing text: \"{text}\" with style: {FontStyle}");
    }
}

class Program
{
    static void Main()
    {
        // Step 1: Obtain a graphic context.
        GraphicContext graphicContext = new GraphicContext();

        // Step 2: Combine the desired font styles using the bitwise OR operator.
        // This creates a single value that represents both Bold and Italic.
        WebFontStyle combinedStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Step 3: Apply the combined style to the graphic context.
        graphicContext.FontStyle = combinedStyle;

        // Step 4: Draw something to verify the result.
        graphicContext.DrawString("Hello, combined fonts!");

        // Bonus: Show how to add underline as well.
        WebFontStyle fancy = WebFontStyle.Bold | WebFontStyle.Italic | WebFontStyle.Underline;
        graphicContext.FontStyle = fancy;
        graphicContext.DrawString("Now with underline!");
    }
}
```

**ผลลัพธ์ที่คาดหวัง**

```
Drawing text: "Hello, combined fonts!" with style: Bold, Italic
Drawing text: "Now with underline!" with style: Bold, Italic, Underline
```

หากคุณรันในคอนโซล, จะเห็นสองบรรทัดที่ยืนยันว่าการรวมสไตล์ทำงานถูกต้อง. ใน UI จริงคุณจะเห็นข้อความ **หนา‑เอียง** (และอาจมีขีดเส้นใต้) แสดงบนหน้าจอ

---

## คำถามที่พบบ่อย & กรณีขอบ

### ถ้าต้องการ **ลบ** สไตล์ภายหลังทำอย่างไร?

คุณสามารถใช้ bitwise AND กับคอมพลีเมนต์ (`& ~`) เพื่อลบแฟล็ก:

```csharp
// Remove Italic while keeping Bold.
graphicContext.FontStyle &= ~WebFontStyle.Italic;
```

### ทำงานกับ **ฟอนต์ครอบครัวแบบกำหนดเอง** ได้ไหม?

ได้เลย. วิธีการใช้แฟล็กนี้เกี่ยวกับ *สไตล์* (bold, italic ฯลฯ) เท่านั้น. ฟอนต์ครอบครัวจริง (เช่น `"Arial"` หรือ `"Open Sans"`) มักตั้งผ่าน property แยกอย่าง `FontFamily`. คุณสามารถผสานได้ตามต้องการ

### จำเป็นต้องมีแอตทริบิวต์ `Flags` หรือไม่?

ต้อง. หากไม่มี `[Flags]` enum จะยังคอมไพล์ได้, แต่การแสดงผลเป็นสตริง (`ToString()`) จะไม่เป็นมิตรและการผสานบิตอาจอ่านยาก. ไลบรารีกราฟิกส่วนใหญ่ที่เปิดให้ใช้ enum สไตล์จะตั้ง `[Flags]` ไว้แล้ว

### สามารถใช้รูปแบบนี้กับ **WPF** หรือ **WinForms** ได้หรือไม่?

ทั้งสองเฟรมเวิร์กมี enum แบบแฟล็กคล้ายกัน (`FontStyle` ใน WinForms, `FontWeight`/`FontStyle` ใน WPF). หลักการเดียวกัน: ผสานค่า enum ด้วย `|`. ตัวอย่างใน WinForms:

```csharp
myLabel.Font = new Font(myLabel.Font, FontStyle.Bold | FontStyle.Italic);
```

---

## เคล็ดลับระดับมืออาชีพสำหรับการตั้งค่าสไตล์ฟอนต์โดยโปรแกรม

* **ตรวจสอบก่อนนำไปใช้** – บาง engine ปฏิเสธการผสานที่ไม่รองรับ (เช่น `Bold | Italic` บนฟอนต์ที่มีแค่ regular) ตรวจสอบ `CanApplyStyle` หาก API มีให้
* **แคชสไตล์ที่รวมแล้ว** – หากคุณวาดข้อความหลายพันสตริง, คำนวณค่า enum ที่รวมแล้วล่วงหน้าแล้วใช้ซ้ำ
* **คำนึงถึงวัฒนธรรม** – ภาษาบางภาษาอาจมีการพิมพ์แบบพิเศษ; ทดสอบผลลัพธ์ในโลคัลเป้าหมายเสมอ
* **บันทึกประสิทธิภาพ** – การทำงานบิตไวส์แทบไม่มีค่าใช้จ่าย; คอขวดมักอยู่ที่การเรนเดอร์จริง ไม่ใช่การรวมสไตล์

---

## สรุปภาพรวม

![Diagram showing how bitwise OR merges font style flags](/images/combine-fonts-diagram.png "how to combine fonts example")

*ข้อความแทนภาพ:* *ภาพตัวอย่างการรวมฟอนต์โดยใช้ bitwise OR ของแฟล็ก Bold และ Italic.*

---

## บทสรุป

เราได้ครอบคลุม **วิธีรวมฟอนต์** ใน C# ตั้งแต่การกำหนด enum `[Flags]`, การผสานสไตล์ด้วยตัวดำเนินการ `|`, ไปจนถึง **การตั้งค่าสไตล์ฟอนต์โดยโปรแกรม** บน graphics context. ตัวอย่างโค้ดเต็มแสดงให้เห็นว่าคุณสามารถ **ใช้หลายสไตล์ฟอนต์** เพียงสองสามบรรทัด, และเคล็ดลับเพิ่มเติมช่วยให้หลีกเลี่ยงข้อผิดพลาดทั่วไป

ตอนนี้คุณรู้เทคนิคแล้ว, ลองเพิ่มขีดเส้นใต้, เส้นขีดฆ่า, หรือแม้แต่แฟล็กกำหนดเองสำหรับเงาหรือเอมบอส. รูปแบบนี้ขยายได้อย่างสวยงาม, ทำให้โค้ด UI ของคุณสะอาดและอ่านง่าย

หากคุณพบว่าคู่มือฉบับนี้มีประโยชน์, อย่าลืมแชร์ให้ทีมงานหรือกดสตาร์ที่รีโพซิทอรีที่คุณเก็บยูทิลิตี้กราฟิกของคุณ. Happy coding, และขอให้ข้อความของคุณดูสวยตามที่คุณจินตนาการ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}