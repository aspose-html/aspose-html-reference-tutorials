---
date: 2026-01-02
description: เรียนรู้วิธีแปลง EPUB เป็น PDF ด้วย Java และ Aspose.HTML พร้อมตั้งค่าขนาดหน้ากระดาษ
  PDF แบบกำหนดเองและตัวเลือกการบันทึก PDF อื่น ๆ
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'ขนาดหน้ากระดาษ PDF แบบกำหนดเอง - การระบุตัวเลือกการบันทึก PDF สำหรับการแปลง
  EPUB เป็น PDF'
url: /th/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ขนาดหน้ากระดาษ PDF แบบกำหนดเอง: การระบุ PDF Save Options สำหรับการแปลง EPUB เป็น PDF

## การแนะนำ

Aspose.HTML for Java ไม่ได้การการ **แปลง EPUB เป็น PDF** เป็นเรื่องง่ายและให้คุณควบคุมผลลัพธ์ได้ในส่วนนี้ **ขนาดหน้า PDF แบบกำหนดเอง** ด้วยในคู่มือแบบขั้นตอนนี้เราจะพาคุณผ่านทุกอย่างที่ต้องดำเนินการ—จากการเตรียมการที่สามารถนำมาใช้ได้ `PdfSaveOptions` สำหรับ PDF ครั้งแรกในขนาดหน้าของครั้งแรก นวัตกรรมสร้างไปป์ไลน์การเผยแพร่, แพลตฟอร์ม e-learning, หรือเพียงแค่ต้องการอัตโนมัติสำหรับเอกสารเป็นครั้งแรกเทคนิคที่สามารถนำมาใช้ได้

## คำตอบด่วน
- **จุดประสงค์หลักของบทช่วยสอนนี้คืออะไร** แปลงไฟล์ EPUB เป็น PDF พร้อมใช้ขนาดหน้ากระดาษ PDF เอเธนส์
- **ใช้ไลบรารีใด** Aspose.HTML สำหรับ Java
- **ฉันจำเป็นต้องมีใบอนุญาตหรือไม่** มีรุ่นทดลองฟรี; ต้องมีลิขสิทธิ์เรื่องนี้เป็นหลัก
- **ฉันสามารถเปลี่ยนสีพื้นหลังได้หรือไม่** ได้แล้ว ใช้ `PdfSaveOptions`
- **รองรับ Java 8+ หรือไม่** แน่นอน—Java runtime รุ่นใหม่ทั้งหมดทำงานได้

## ขนาดหน้า PDF ที่กำหนดเองคืออะไร

ขนาดหน้ากระดาษ PDF ช่วยให้สามารถระบุความสูงและความสูงที่แน่นอนของแต่ละหน้าใน PDF ได้ แทนการใช้ขนาดมาตรฐานเช่น A4 หรือ Letter ที่เหมาะสำหรับ e-books, แผ่นพับ, หรือสถานการณ์ใด ๆ ที่ต้องการวางภาพความละเอียดสูงการออกแบบเฉพาะ

## เหตุใดจึงต้องใช้ Aspose.HTML สำหรับการแปลง EPUB เป็น PDF

- **ความเที่ยงตรงสูง:** รักษาไลเนอร์เอาต์, ฟอนต์, และรูปภาพได้อย่างครบถ้วน
- **การควบคุมแบบละเอียด:** ติดตามหน้า, คอสเพลย์, ระยะขอบ, อ่านผ่านทุกอย่าง `PdfSaveOptions`
- **ข้ามแพลตฟอร์ม:** ทำงานบน Windows, Linux, และ macOS ด้วยโค้ด Java เดียวกัน
- **Performance:** มีเอนจินเรนเดอร์ที่ปรับให้เร็วสำหรับการปรับปรุง

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มต้นขั้นตอน, ระบบควบคุมคุณ:

- **Java Development Environment:** JDK 8 หรือใหม่กว่าที่จำเป็นและไม่จำเป็นต้องใช้
- **Aspose.HTML สำหรับ Java:** ดาวน์โหลด JAR ล่าสุดจาก [เว็บไซต์](https://releases.aspose.com/html/java/)
- **ไฟล์ EPUB:** และ `.epub` ต้องการแปลง

เมื่อทุกอย่างพร้อมแล้ว โปรดดูขั้นตอนการควบคุมจริง

## ขั้นตอนที่ 1: เปิดไฟล์ EPUB

เรื่องเราต้องเปิดไฟล์ EPUB ด้วย `FileInputStream` ซึ่งจะมีการสตรีมนี้ต่อไปในขั้นตอนต่อไป

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## ขั้นตอนที่ 2: กำหนดตัวเลือกการบันทึก PDF

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

### เคล็ดลับมือโปร:
- **Pixels vs. Points:** `Length.fromPixels` แปลงหน้าจอเป็น PDF point (1 point = 1/72 นิ้ว) เลือกค่าที่สะท้อนขนาดการพิมพ์สุดท้ายที่ต้องการ

## ขั้นตอนที่ 3: แปลง EPUB เป็น PDF

เมื่อมีสตรีมอินพุตและตัวเลือกที่กำหนดแล้ว, เรียกใช้ตัวแปลง ผลลัพธ์ PDF จะถูกบันทึกลงในตำแหน่งที่คุณระบุ

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## ซอร์สโค้ดฉบับสมบูรณ์

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

## ปัญหาและวิธีแก้ไขที่พบบ่อย

| ปัญหา | สาเหตุ | วิธีแก้ไข |

|-------|-------|-----|

| **หน้า PDF ว่างเปล่า** | สตรีมอินพุตถูกปิดก่อนการแปลง | เปิดบล็อก `try‑with‑resources` ไว้จนกว่าจะเสร็จสิ้น `convertEPUB` |

| **ขนาดหน้าไม่ถูกต้อง** | ใช้พิกเซลที่ไม่ตรงกับขนาดการพิมพ์ที่ต้องการ | แปลงหน่วยนิ้วที่ต้องการเป็นพอยต์ (`1 นิ้ว = 72 พอยต์`) แล้วแปลงเป็นพิกเซลโดยใช้ `Length.fromPixels` |

| **ฟอนต์หายไป** | ฟอนต์ไม่ได้ฝังอยู่ใน EPUB | ตรวจสอบให้แน่ใจว่าฟอนต์ถูกบรรจุอยู่ภายใน EPUB หรือติดตั้งฟอนต์บนเครื่องโฮสต์ |

## คำถามที่พบบ่อย (FAQs)

### Aspose.HTML สำหรับ Java เป็นไลบรารีฟรีหรือไม่?

Aspose.HTML for Java เป็นไลบรารีเป็นตัวอย่าง,ไม่เชื่อรุ่นทดลองฟรีจาก [เว็บไซต์](https://releases.aspose.com/) ได้อีกต่อไป

### รูปแบบ EPUB ใดบ้างที่รองรับสำหรับการแปลง
Aspose.HTML สำหรับ Java ที่รองรับรูปแบบ EPUB หลาย, เพิ่มเติมเอกสาร EPUB โดยตรง

### ฉันสามารถปรับแต่งเอาต์พุต PDF เพิ่มเติมได้หรือไม่
ได้, ไม่เคยปรับแต่งผลลัพธ์ PDF มากนัก ส่วนใหญ่การตั้งค่าหน้า, สีความเชื่อ, และหลายอย่างอื่นๆ ใน `PdfSaveOptions`

### มีข้อจำกัดใดๆ สำหรับ Aspose.HTML สำหรับ Java เวอร์ชันทดลองหรือไม่
รุ่นทดลองอาจมีการควบคุมอีกครั้ง, โปรดดูเอกสารเพื่อดูรายละเอียด

### ฉันจะรับการสนับสนุนสำหรับ Aspose.HTML สำหรับ Java ได้ที่ไหน
เพื่อรับคำตอบและขอรับได้ที่ [Aspose.HTML forum](https://forum.aspose.com/)

---

**อัปเดตล่าสุด:** 2026-01-02
**ทดสอบด้วย:** Aspose.HTML สำหรับ Java 24.11 (ล่าสุด ณ เวลาที่เขียน)
**ผู้เขียน:** สมมติ  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}