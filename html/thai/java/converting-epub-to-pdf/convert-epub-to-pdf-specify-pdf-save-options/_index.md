---
date: 2026-01-02
description: เรียนรู้วิธีแปลง EPUB เป็น PDF ด้วย Java และ Aspose.HTML พร้อมตั้งค่าขนาดหน้ากระดาษ
  PDF แบบกำหนดเองและตัวเลือกการบันทึก PDF อื่น ๆ
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'ขนาดหน้ากระดาษ PDF แบบกำหนดเอง: การระบุตัวเลือกการบันทึก PDF สำหรับการแปลง
  EPUB เป็น PDF'
url: /th/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ขนาดหน้ากระดาษ PDF แบบกำหนดเอง: การระบุ PDF Save Options สำหรับการแปลง EPUB เป็น PDF

## Introduction

Aspose.HTML for Java ทำให้การ **convert EPUB to PDF** เป็นเรื่องง่ายและให้คุณควบคุมผลลัพธ์ได้อย่างเต็มที่ รวมถึงการตั้งค่า **custom PDF page size** ด้วย ในคู่มือแบบขั้นตอนนี้เราจะพาคุณผ่านทุกอย่างที่ต้องทำ—from การเตรียมสภาพแวดล้อมจนถึงการปรับ `PdfSaveOptions` เพื่อให้ PDF ที่สร้างขึ้นตรงกับขนาดหน้าที่คุณต้องการ ไม่ว่าคุณจะสร้าง pipeline การเผยแพร่, แพลตฟอร์ม e‑learning, หรือแค่ต้องการอัตโนมัติการแปลงเอกสาร คุณจะพบเทคนิคเหล่านี้มีประโยชน์

## Quick Answers
- **What is the primary purpose of this tutorial?** แปลงไฟล์ EPUB เป็น PDF พร้อมใช้ขนาดหน้ากระดาษ PDF แบบกำหนดเอง  
- **Which library is used?** Aspose.HTML for Java  
- **Do I need a license?** มีรุ่นทดลองฟรี; ต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง  
- **Can I change background color?** ได้, ใช้ `PdfSaveOptions`  
- **Is Java 8+ supported?** แน่นอน—Java runtime รุ่นใหม่ทั้งหมดทำงานได้

## What is a custom PDF page size?

ขนาดหน้ากระดาษ PDF แบบกำหนดเองช่วยให้คุณระบุความกว้างและความสูงที่แน่นอนของแต่ละหน้าใน PDF ที่สร้างขึ้น แทนการใช้ขนาดมาตรฐานเช่น A4 หรือ Letter ซึ่งเหมาะสำหรับ e‑books, แผ่นพับ, หรือสถานการณ์ใด ๆ ที่ต้องการให้การจัดวางภาพตรงกับการออกแบบเฉพาะ

## Why use Aspose.HTML for EPUB to PDF conversion?

- **High fidelity:** รักษาเลย์เอาต์ซับซ้อน, ฟอนต์, และรูปภาพได้อย่างครบถ้วน  
- **Fine‑grained control:** ปรับขนาดหน้า, พื้นหลัง, ระยะขอบ, และอื่น ๆ ผ่าน `PdfSaveOptions`  
- **Cross‑platform:** ทำงานบน Windows, Linux, และ macOS ด้วยโค้ด Java เดียวกัน  
- **Performance:** มีเอนจินเรนเดอร์ที่ปรับให้เร็วสำหรับการแปลงที่มีประสิทธิภาพ

## Prerequisites

ก่อนเริ่มทำตามขั้นตอน, ตรวจสอบว่าคุณมี:

- **Java Development Environment:** JDK 8 หรือใหม่กว่า ติดตั้งและกำหนดค่าเรียบร้อย  
- **Aspose.HTML for Java:** ดาวน์โหลด JAR ล่าสุดจาก [website](https://releases.aspose.com/html/java/)  
- **EPUB File:** ไฟล์ `.epub` ที่ต้องการแปลง  

เมื่อทุกอย่างพร้อมแล้ว, ไปสู่ขั้นตอนการแปลงจริง

## Step 1: Open the EPUB File

ก่อนอื่นเราต้องเปิดไฟล์ EPUB ด้วย `FileInputStream` ซึ่งสตรีมนี้จะถูกส่งต่อให้ตัวแปลงในขั้นตอนต่อไป

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## Step 2: Define PDF Save Options

ที่นี่เราตั้งค่า **custom PDF page size** และสีพื้นหลัง (ถ้าต้องการ) ปรับค่าพิกเซลให้ตรงกับขนาดที่คุณต้องการ

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

### Pro tip:
- **Pixels vs. Points:** `Length.fromPixels` แปลงพิกเซลหน้าจอเป็น PDF points (1 point = 1/72 นิ้ว) เลือกค่าที่สะท้อนขนาดการพิมพ์สุดท้ายที่ต้องการ

## Step 3: Convert EPUB to PDF

เมื่อมีสตรีมอินพุตและตัวเลือกที่กำหนดแล้ว, เรียกใช้ตัวแปลง ผลลัพธ์ PDF จะถูกบันทึกลงในตำแหน่งที่คุณระบุ

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## Complete Source Code

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Common Issues and Solutions

| Issue | Cause | Fix |
|-------|-------|-----|
| **PDF pages are blank** | Input stream closed before conversion | Keep the `try‑with‑resources` block open until after `convertEPUB`. |
| **Incorrect page dimensions** | Using pixels that don’t map to desired print size | Convert desired inches to points (`1 inch = 72 points`) and then to pixels using `Length.fromPixels`. |
| **Missing fonts** | Fonts not embedded in EPUB | Ensure the fonts are packaged inside the EPUB or install them on the host machine. |

## Frequently Asked Questions (FAQs)

### Is Aspose.HTML for Java a free library?
Aspose.HTML for Java เป็นไลบรารีเชิงพาณิชย์, แต่คุณสามารถดาวน์โหลดรุ่นทดลองฟรีจาก [website](https://releases.aspose.com/) ได้

### What EPUB formats are supported for conversion?
Aspose.HTML for Java รองรับการแปลงรูปแบบ EPUB หลากหลาย, ทำให้เข้ากันได้กับเอกสาร EPUB ส่วนใหญ่

### Can I customize the PDF output further?
ได้, คุณสามารถปรับแต่งผลลัพธ์ PDF เพิ่มเติมได้โดยการตั้งค่า page setup, สีพื้นหลัง, และการตั้งค่าอื่น ๆ ใน `PdfSaveOptions`

### Are there any limitations to the trial version of Aspose.HTML for Java?
รุ่นทดลองอาจมีข้อจำกัดบางประการ, ควรตรวจสอบเอกสารเพื่อดูรายละเอียด

### Where can I get support for Aspose.HTML for Java?
คุณสามารถค้นหาคำตอบและขอรับการสนับสนุนได้ที่ [Aspose.HTML forum](https://forum.aspose.com/)

---

**Last Updated:** 2026-01-02  
**Tested With:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}