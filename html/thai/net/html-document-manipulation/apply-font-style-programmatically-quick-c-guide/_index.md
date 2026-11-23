---
category: general
date: 2026-04-23
description: ใช้สไตล์ฟอนต์แบบโปรแกรมและเรียนรู้วิธีลบขีดเส้นใต้จากข้อความ, เปลี่ยนสไตล์ข้อความ,
  และตั้งข้อความเป็นตัวหนาแบบโปรแกรมในบทแนะนำสั้น ๆ
draft: false
keywords:
- apply font style
- remove underline from text
- change text style
- text formatting tutorial
- set bold text programmatically
language: th
og_description: ใช้สไตล์ฟอนต์แบบโปรแกรมเมติกและค้นหาวิธีลบขีดเส้นใต้จากข้อความ, เปลี่ยนสไตล์ข้อความ,
  และตั้งข้อความเป็นตัวหนาแบบโปรแกรมเมติกในบทแนะนำสั้น ๆ ที่ใช้งานได้จริง.
og_title: ใช้สไตล์ฟอนต์โดยโปรแกรม – คู่มือ C# อย่างรวดเร็ว
tags:
- csharp
- ui
- text-formatting
- programming
title: ใช้สไตล์ฟอนต์แบบโปรแกรม – คู่มือ C# อย่างรวดเร็ว
url: /th/net/html-document-manipulation/apply-font-style-programmatically-quick-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ใช้สไตล์ฟอนต์แบบโปรแกรมเมติก – คู่มือสั้น C#

เคยต้อง **ใช้สไตล์ฟอนต์** กับองค์ประกอบ UI แต่ไม่รู้ว่าจะเริ่มจากตรงไหนหรือเปล่า? คุณไม่ได้เป็นคนเดียว—นักพัฒนาส่วนใหญ่มักเจอปัญหานี้เมื่อลองทำการจัดรูปแบบข้อความแบบไดนามิก ข่าวดีคือในไม่กี่นาทีคุณจะรู้วิธีเปลี่ยนลักษณะของ label, ลบเส้นขีดใต้จากข้อความ, และตั้งค่าข้อความหนาแบบโปรแกรมเมติกโดยไม่ต้องค้นหาเอกสารยาว ๆ

ใน **บทแนะนำการจัดรูปแบบข้อความ** นี้เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบ, อธิบาย “ทำไม” ของแต่ละบรรทัด, และให้เคล็ดลับที่คุณสามารถคัดลอก‑วางไปใช้ในโปรเจกต์ WinForms หรือ WPF ใดก็ได้ ไม่มีส่วนเกิน เพียงสิ่งที่ทำให้งานสำเร็จ

---

## สิ่งที่คุณจะได้เรียน

- วิธี **ใช้สไตล์ฟอนต์** ด้วยคลาสช่วยเหลือขนาดเล็ก  
- ขั้นตอนที่แม่นยำในการ **ลบเส้นขีดใต้จากข้อความ** ขณะยังคงรักษาสไตล์อื่นไว้  
- วิธี **เปลี่ยนสไตล์ข้อความ** (หนา, เอียง, ขีดใต้) อย่างรวดเร็ว  
- ชิ้นส่วนโค้ดเต็มพร้อมคัดลอกที่ **ตั้งค่าข้อความหนาแบบโปรแกรมเมติก**  
- ข้อผิดพลาดทั่วไปและการจัดการกรณีขอบ เพื่อให้คุณไม่เจอปัญหาในภายหลัง  

**ข้อกำหนดเบื้องต้น:** .NET 6+ (หรือ .NET Framework เวอร์ชันใหม่), ความรู้พื้นฐาน C#, และ IDE ที่คุณชอบ (Visual Studio, Rider, หรือ VS Code) เพียงเท่านี้—ไม่ต้องติดตั้ง NuGet แพคเกจเพิ่มเติม

---

## ขั้นตอนที่ 1 – ใช้สไตล์ฟอนต์กับคอนโทรลของคุณ

หัวใจของการ **ใช้สไตล์ฟอนต์** ใด ๆ คือ enum `FontStyle` ที่รวมกับอ็อบเจกต์ `Font` เพื่อให้โค้ดดูเรียบร้อย เราจะห่อหุ้มตรรกะของ enum นี้ไว้ในคลาสเล็ก ๆ ชื่อ `WebFontStyle` คลาสนี้สะท้อนคุณสมบัติที่คุณเห็นในโค้ดต้นฉบับ (`Bold`, `Italic`, `Underline`) และสร้างค่า `FontStyle` ที่คุณสามารถส่งให้ `Font` ได้

```csharp
using System;
using System.Drawing;

/// <summary>
/// Simple helper that mimics the original WebFontStyle API.
/// It lets you toggle Bold, Italic, and Underline flags and
/// converts the result into a System.Drawing.FontStyle value.
/// </summary>
public class WebFontStyle
{
    public bool Bold { get; set; } = false;
    public bool Italic { get; set; } = false;
    public bool Underline { get; set; } = false;

    /// <summary>
    /// Returns a FontStyle that combines the selected flags.
    /// </summary>
    public FontStyle ToFontStyle()
    {
        FontStyle style = FontStyle.Regular;
        if (Bold)      style |= FontStyle.Bold;
        if (Italic)    style |= FontStyle.Italic;
        if (Underline) style |= FontStyle.Underline;
        return style;
    }

    /// <summary>
    /// Creates a new Font based on an existing one but with the
    /// updated style. Handy for UI controls that already have a font.
    /// </summary>
    public Font ToFont(Font baseFont)
    {
        return new Font(baseFont, ToFontStyle());
    }
}
```

**ทำไมถึงสำคัญ:**  
โดยการแยกตรรกะการสร้างแฟล็กออกจาก UI คุณจะหลีกเลี่ยงการกระจายการใช้ `|` แบบบิตไวด์ทั่วโค้ด ทำให้อ่านง่ายขึ้น, ทดสอบง่ายขึ้น, และ—ที่สำคัญที่สุด—ทำให้เจตนาของ **ใช้สไตล์ฟอนต์** ชัดเจนเป็นผลลัพธ์

---

## ขั้นตอนที่ 2 – ลบเส้นขีดใต้จากข้อความ (และรักษาสไตล์อื่นไว้)

สมมติว่าคุณได้รับมรดกจาก label ที่มีเส้นขีดใต้แล้ว แต่การออกแบบต้องการข้อความหนาแบบธรรมดา คุณไม่ต้องการสูญเสียความหนาเมื่อเอาเส้นขีดใต้ออก ที่นี่ `WebFontStyle` จะช่วยได้

```csharp
// Assume we already have a Label named lblSample.
var fontStyle = new WebFontStyle
{
    Bold = true,          // Keep bold on.
    Italic = false,      // No italic needed.
    Underline = false    // This line **removes underline**.
};

// Apply the new Font to the label.
lblSample.Font = fontStyle.ToFont(lblSample.Font);
```

**จุดสำคัญ:** การตั้งค่า `Underline = false` อย่างชัดเจนบอกให้ตัวช่วย *ไม่* รวมแฟล็กเส้นขีดใต้ หากคุณละเว้นบรรทัดนี้ เส้นขีดใต้เดิมจะคงอยู่ ซึ่งเป็นแหล่งที่มาของบั๊กบ่อยครั้งเมื่อผู้พัฒนาเพียงแค่สลับคุณสมบัติ `Bold`

---

## ขั้นตอนที่ 3 – เปลี่ยนสไตล์ข้อความ: หนา, เอียง, และอื่น ๆ

คุณอาจสงสัยว่า “ถ้าต้องการสลับเอียงด้วยล่ะ?” อ็อบเจกต์เดียวกันทำงานได้กับการผสมใด ๆ ด้านล่างเป็นเมทริกซ์สั้น ๆ ที่คุณสามารถอ้างอิงขณะเขียนโค้ด

| สไตล์ที่ต้องการ | `Bold` | `Italic` | `Underline` |
|------------------|--------|----------|-------------|
| **หนาเท่านั้น** | true   | false    | false       |
| *เอียงเท่านั้น* | false  | true     | false       |
| **หนา + เอียง** | true   | true     | false       |
| **หนา + ขีดใต้** | true   | false    | true        |

เพียงตั้งค่าคุณสมบัติที่ต้องการและเรียก `ToFont` ตัวช่วยจะทำงานหนักให้คุณ เพื่อให้คุณโฟกัสที่ตรรกะ UI

---

## ตัวอย่างเต็ม – ตั้งค่าข้อความหนาแบบโปรแกรมเมติก

ด้านล่างเป็นตัวอย่าง **WinForms ที่ทำงานได้เต็มรูปแบบ** ซึ่งสาธิตทุกอย่างที่เราได้พูดถึงแล้ว คัดลอกไปวางในโปรเจกต์ WinForms แบบ console‑style ใหม่และกด **F5**

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

namespace FontStyleDemo
{
    static class Program
    {
        [STAThread]
        static void Main()
        {
            ApplicationConfiguration.Initialize(); // .NET 6+ boilerplate
            Application.Run(new DemoForm());
        }
    }

    public class DemoForm : Form
    {
        private readonly Label _sampleLabel;

        public DemoForm()
        {
            Text = "Apply Font Style Demo";
            Size = new Size(400, 200);
            StartPosition = FormStartPosition.CenterScreen;

            _sampleLabel = new Label
            {
                Text = "Hello, world!",
                AutoSize = true,
                Location = new Point(20, 30)
            };
            Controls.Add(_sampleLabel);

            // STEP: instantiate WebFontStyle and configure it
            var fontStyle = new WebFontStyle
            {
                Bold = true,          // set bold text programmatically
                Italic = false,      // no italic
                Underline = false    // remove underline from text
            };

            // Apply the new style to the label
            _sampleLabel.Font = fontStyle.ToFont(_sampleLabel.Font);
        }
    }

    // ---- WebFontStyle class from Step 1 (included for completeness) ----
    public class WebFontStyle
    {
        public bool Bold { get; set; } = false;
        public bool Italic { get; set; } = false;
        public bool Underline { get; set; } = false;

        public FontStyle ToFontStyle()
        {
            FontStyle style = FontStyle.Regular;
            if (Bold)      style |= FontStyle.Bold;
            if (Italic)    style |= FontStyle.Italic;
            if (Underline) style |= FontStyle.Underline;
            return style;
        }

        public Font ToFont(Font baseFont)
        {
            return new Font(baseFont, ToFontStyle());
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณรันโปรแกรม หน้าต่างจะปรากฏพร้อมข้อความ **“Hello, world!”** ที่แสดงเป็น **หนา**, **ไม่เอียง**, และ **ไม่มีเส้นขีดใต้** การยืนยันด้วยภาพนี้บอกว่าตรรกะ **ใช้สไตล์ฟอนต์** ทำงานได้อย่างสมบูรณ์

---

## เคล็ดลับระดับมืออาชีพ & กรณีขอบ

- **อัปเดตแบบไดนามิก:** หากต้องการเปลี่ยนสไตล์หลังจากฟอร์มแสดง (เช่น ตอบสนองต่อเช็คบ็อกซ์) เพียงสร้างอินสแตนซ์ `WebFontStyle` ใหม่หรือแก้ไขคุณสมบัติแล้วกำหนดค่า `lbl.Font` ใหม่ UI จะอัปเดตทันที  
- **พิจารณา High‑DPI:** เมื่อคุณแทนที่อ็อบเจกต์ `Font` Windows จะสเกลอัตโนมัติตาม DPI ปัจจุบัน ไม่ต้องเขียนโค้ดเพิ่มเติม เว้นแต่คุณจัดการสเกลด้วยตนเอง  
- **เทียบเท่า WPF:** ใน WPF คุณจะผูก `FontWeight`, `FontStyle`, และ `TextDecorations` แทนการสลับอ็อบเจกต์ `Font` การแยกตรรกะสไตล์ออกจากเลเยอร์วิวยังคงใช้ได้เช่นกัน  
- **หลีกเลี่ยง memory leak:** การกำหนดค่า `Label.Font` ใหม่จะสร้างอ็อบเจกต์ `Font` ตัวใหม่ ควร Dispose อ็อบเจกต์เก่าเมื่อสลับสไตล์บ่อย ๆ: `var oldFont = lbl.Font; lbl.Font = newFont; oldFont.Dispose();`

---

## สรุป

ตอนนี้คุณรู้วิธี **ใช้สไตล์ฟอนต์** กับคอนโทรล .NET ใด ๆ, **ลบเส้นขีดใต้จากข้อความ**, และ **เปลี่ยนสไตล์ข้อความ** อย่างรวดเร็ว—ทั้งหมดนี้โดยรักษาโค้ดให้สะอาดและนำกลับมาใช้ใหม่ได้ ตัวช่วย `WebFontStyle` ขนาดเล็กทำให้การจัดการบูลีนหลายค่าเป็นคอมโพเนนต์ที่ทดสอบได้, และตัวอย่างเต็มพิสูจน์ว่าคุณสามารถ **ตั้งค่าข้อความหนาแบบโปรแกรมเมติก** ได้ในไม่กี่บรรทัด

ต่อไปทำอะไรดี? ลองผสานวิธีนี้กับการตั้งค่าที่ผู้ใช้กำหนด, หรือทดลองใช้แฟล็ก `FontStyle` อื่น ๆ เช่น `Strikeout` คุณอาจสร้างพาเนล UI เล็ก ๆ ที่ให้ผู้ใช้ที่ไม่ใช่นักพัฒนาเลือกหนา, เอียง, หรือขีดใต้ได้ในขณะรัน—ไม่ต้องคอมไพล์ใหม่

หากคุณพบว่า **บทแนะนำการจัดรูปแบบข้อความ** นี้เป็นประโยชน์ อย่าลังเลที่จะแสดงความคิดเห็นหรือแชร์วิธีของคุณเอง ขอให้เขียนโค้ดอย่างสนุกสนานและ UI ของคุณดูตรงตามที่คุณต้องการเสมอ!

---

![Screenshot showing how to apply font style to a label in C#](https://example.com/images/apply-font-style.png

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}