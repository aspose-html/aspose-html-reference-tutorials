---
category: general
date: 2026-03-29
description: วิธีฝังรูปภาพขณะแปลง MHTML เป็น PDF ด้วย Aspose HTML. ลดขนาดไฟล์ PDF
  และเชี่ยวชาญเทคนิคการแปลง Aspose HTML เป็น PDF ในไม่กี่นาที.
draft: false
keywords:
- how to embed images
- convert mhtml to pdf
- reduce pdf file size
- aspose html to pdf
- reduce pdf size
language: th
og_description: วิธีฝังรูปภาพขณะแปลง MHTML เป็น PDF ด้วย Aspose HTML. เรียนรู้การลดขนาดไฟล์
  PDF และใช้ประโยชน์สูงสุดจาก Aspose HTML to PDF.
og_title: วิธีฝังรูปภาพเมื่อแปลง MHTML เป็น PDF – คู่มือของ Aspose
tags:
- Aspose
- Java
- PDF
- MHTML
title: วิธีฝังรูปภาพเมื่อแปลง MHTML เป็น PDF – คู่มือ Aspose
url: /th/java/conversion-html-to-other-formats/how-to-embed-images-when-converting-mhtml-to-pdf-aspose-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีฝังรูปภาพเมื่อแปลง MHTML เป็น PDF – คู่มือ Aspose

เคยสงสัย **วิธีฝังรูปภาพ** ระหว่างการแปลง MHTML‑to‑PDF และทำให้ไฟล์ที่ได้มีขนาดเบาไหม? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจอปัญหาเมื่อ PDF ของพวกเขาใหญ่ขึ้นอย่างรวดเร็วเพราะทุกทรัพยากร—ฟอนต์, สคริปต์, แม้แต่ไอคอนขนาดเล็ก—ถูกฝังเข้าไป ข่าวดีคือ? ด้วย Aspose.HTML for Java คุณสามารถบอกให้ตัวแปลงฝัง **เฉพาะรูปภาพ** เท่านั้น ปล่อยให้ส่วนอื่นเป็นการอ้างอิงภายนอก การปรับแต่งเดียวนี้มักทำให้ขนาด PDF ลดลงอย่างมาก

ในบทแนะนำนี้เราจะเดินผ่านการแปลงรายงาน MHTML เป็น PDF, เน้นที่ **วิธีฝังรูปภาพ**, และเพิ่มเคล็ดลับเพิ่มเติมบางอย่างเพื่อ **ลดขนาดไฟล์ PDF**. เมื่อจบคุณจะมีคลาส Java ที่พร้อมรัน, เข้าใจว่าทำไมการฝังเฉพาะรูปภาพจึงสำคัญ, และรู้ว่าจะไปที่ไหนหากในภายหลังต้องการฝังฟอนต์หรือทรัพยากรอื่น ๆ ไม่ใช่การอ้างอิงแบบกว้าง ๆ “ดูเอกสาร” — เพียงโซลูชันที่สมบูรณ์พร้อมคัดลอกและวาง

## สิ่งที่คุณจะได้เรียนรู้

- คำสั่ง API ที่ต้องใช้เพื่อ **แปลง MHTML เป็น PDF** ด้วย Aspose.HTML.
- วิธีตั้งค่า `PdfConversionOptions` เพื่อให้ตัวแปลง **ฝังเฉพาะรูปภาพ**.
- ทำไมการฝังเฉพาะรูปภาพช่วย **ลดขนาด PDF** และเมื่อใดที่คุณอาจต้องการการตั้งค่าอื่น.
- ตัวอย่าง Java ที่สมบูรณ์และสามารถรันได้ ซึ่งคุณสามารถนำไปใส่ในโปรเจกต์ Maven/Gradle ใดก็ได้.
- ข้อผิดพลาดทั่วไป (ทรัพยากรหาย, เส้นทางไฟล์ผิด) และวิธีแก้ไขอย่างรวดเร็ว.

### ข้อกำหนดเบื้องต้น

- ติดตั้ง Java 8 หรือใหม่กว่า.
- Maven หรือ Gradle เพื่อจัดการ dependencies (เราจะแสดงตัวอย่าง Maven).
- ไลบรารี Aspose.HTML for Java (คุณสามารถดาวน์โหลดรุ่นทดลองฟรีจากเว็บไซต์ของ Aspose).
- ไฟล์ MHTML ที่คุณต้องการแปลงเป็น PDF (ตัวอย่างใช้ `report.mhtml`).

> **เคล็ดลับมืออาชีพ:** เก็บไฟล์ MHTML และ PDF ผลลัพธ์ไว้ในโฟลเดอร์เดียวกันระหว่างการทดสอบ; การใช้เส้นทางสัมพันธ์ช่วยให้จัดการง่าย.

---

## ขั้นตอนที่ 1 – เพิ่ม Aspose.HTML ไปยังโปรเจกต์ของคุณ

หากคุณใช้ Maven ให้วางโค้ดต่อไปนี้ลงในไฟล์ `pom.xml` ของคุณ เวอร์ชันที่แสดงเป็นเวอร์ชันล่าสุด ณ เดือนมีนาคม 2026; ตรวจสอบรีโพของ Aspose เพื่อดูเวอร์ชันที่ใหม่กว่า.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

สำหรับ Gradle, รูปแบบที่เทียบเท่าคือ:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

เมื่อ dependency ถูกดึงมาเรียบร้อย คุณพร้อมที่จะนำเข้าคลาสที่เราต้องใช้.

## ขั้นตอนที่ 2 – สร้างตัวเลือกการแปลงและตั้งค่าโหมดการฝัง

หัวใจของ **วิธีฝังรูปภาพ** อยู่ใน `PdfConversionOptions`. โดยค่าเริ่มต้น Aspose จะฝัง *ทุก* ทรัพยากร (ฟอนต์, CSS, รูปภาพ). เราจะเปลี่ยนเป็น `EMBED_IMAGES_ONLY`.

```java
// Step 2: Prepare conversion options – embed only images
PdfConversionOptions options = new PdfConversionOptions();
options.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);
```

ทำไมเรื่องนี้ถึงสำคัญ? ลองนึกถึงรายงานองค์กรที่อ้างอิงฟอนต์ขององค์กรที่เก็บไว้บนแชร์เครือข่าย การฝังฟอนต์นั้นทำให้ PDF เพิ่มขนาดหลายร้อยกิโลไบต์แม้ว่าผู้ชมจะสามารถดึงฟอนต์จากระยะไกลได้ การฝังเฉพาะรูปภาพทำให้ PDF รักษาความคมชัดของภาพที่ต้องการในขณะที่ยังคงเบาอยู่.

## ขั้นตอนที่ 3 – ดำเนินการแปลง

ตอนนี้เราจะเรียก `Converter.convert` โดยส่งพาธของไฟล์ MHTML ต้นทาง, พาธของไฟล์ PDF ปลายทาง, และตัวเลือกที่เราตั้งค่าไว้.

```java
// Step 3: Convert MHTML to PDF using the options above
String sourcePath = "YOUR_DIRECTORY/report.mhtml";
String targetPath = "YOUR_DIRECTORY/report.pdf";

Converter.convert(sourcePath, targetPath, options);
```

หากทุกอย่างตั้งค่าอย่างถูกต้อง คุณจะเห็นไฟล์ `report.pdf` ปรากฏข้างไฟล์ MHTML ของคุณ เปิดไฟล์นั้น—รูปภาพทุกภาพจากรายงานต้นฉบับควรอยู่ครบ, ส่วนฟอนต์และ CSS จะยังคงเป็นการอ้างอิงภายนอก.

## ขั้นตอนที่ 4 – ตรวจสอบการลดขนาด PDF

การตรวจสอบอย่างรวดเร็วช่วยยืนยันว่าคุณ **ลดขนาด PDF** จริง ๆ เปรียบเทียบขนาดไฟล์ก่อนและหลังเปลี่ยนโหมดการฝัง:

```java
File before = new File("YOUR_DIRECTORY/report_full.pdf"); // generated with default settings
File after  = new File(targetPath); // our image‑only PDF

System.out.println("Full embed size: " + before.length() / 1024 + " KB");
System.out.println("Images‑only size: " + after.length() / 1024 + " KB");
```

ในหลาย ๆ กรณีคุณจะเห็นการลดลงประมาณ 30‑70 % ขึ้นอยู่กับจำนวนฟอนต์หรือไฟล์ CSS ที่ฝังไว้เดิม นั่นเป็นการชนะที่สำคัญสำหรับผู้ที่ส่ง PDF ผ่านเว็บหรือเก็บไว้ในคลาวด์บัคเก็ต.

## ขั้นตอนที่ 5 – ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นคลาส Java ทั้งหมดที่คุณสามารถคัดลอกไปยัง IDE ของคุณ แทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางโฟลเดอร์จริงที่ไฟล์ `report.mhtml` อยู่.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.converters.ResourceEmbeddingMode;

import java.io.File;

public class MhtmlToPdf {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define source and destination ----------
        String sourcePath = "YOUR_DIRECTORY/report.mhtml";
        String targetPath = "YOUR_DIRECTORY/report.pdf";

        // ---------- Step 2: Set conversion options (embed only images) ----------
        PdfConversionOptions conversionOptions = new PdfConversionOptions();
        conversionOptions.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);

        // ---------- Step 3: Run the conversion ----------
        Converter.convert(sourcePath, targetPath, conversionOptions);
        System.out.println("Conversion complete! PDF saved to: " + targetPath);

        // ---------- Step 4: (Optional) Show size reduction ----------
        File outputPdf = new File(targetPath);
        System.out.println("Resulting PDF size: " + outputPdf.length() / 1024 + " KB");
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (บนคอนโซล):

```
Conversion complete! PDF saved to: YOUR_DIRECTORY/report.pdf
Resulting PDF size: 842 KB
```

เปิด `report.pdf` ด้วยโปรแกรมดูใดก็ได้; คุณควรเห็นรูปภาพทั้งหมดจากต้นฉบับแสดงอย่างถูกต้อง หากพบรูปภาพหาย ให้ตรวจสอบอีกครั้งว่า URL ของรูปใน MHTML เป็นแบบ absolute หรือไฟล์สามารถเข้าถึงได้จากเครื่องที่ทำการแปลง.

## คำถามทั่วไป & การจัดการกรณีขอบ

### ถ้าฉัน *ต้องการ* ฝังฟอนต์ล่ะ?

เปลี่ยน `ResourceEmbeddingMode` เป็น `EMBED_ALL` หรือ `EMBED_FONTS_ONLY`. enum นี้มีสี่ตัวเลือก:

| Mode                     | สิ่งที่ถูกฝัง |
|--------------------------|--------------------|
| `EMBED_ALL`              | รูปภาพ, ฟอนต์, CSS |
| `EMBED_IMAGES_ONLY`      | เฉพาะรูปภาพ (ค่าเริ่มต้นของเรา) |
| `EMBED_FONTS_ONLY`       | เฉพาะฟอนต์ |
| `EMBED_NONE`             | ไม่มี (อ้างอิงภายนอกเท่านั้น) |

### MHTML ของฉันมี CSS ภายนอกที่ส่งผลต่อการจัดวาง—PDF จะเสียรูปหรือไม่?

เนื่องจากเราไม่ได้ฝัง CSS ตัวแปลงจะยังคงดาวน์โหลดมันในระหว่างการแปลง หาก CSS โฮสต์บนอินทราเน็ตที่เซิร์ฟเวอร์แปลงไม่สามารถเข้าถึงได้ การจัดวางอาจกลับไปใช้ค่าเริ่มต้น ในกรณีนั้น ให้ฝัง CSS (`EMBED_ALL`) หรือคัดลอกสไตล์ชีตไปยังเครื่องโลคัลและปรับ MHTML ให้ชี้ไปที่ไฟล์โลคัล

### ฉันสามารถประมวลผลหลายไฟล์ MHTML ในโฟลเดอร์ได้หรือไม่?

ได้เลย. ห่อหุ้มตรรกะการแปลงในลูปที่วนผ่าน `File.listFiles()` และเปลี่ยนชื่อไฟล์เป้าหมายตามนั้น เพียงจำไว้ว่าให้ใช้อินสแตนซ์ `PdfConversionOptions` ตัวเดียวเพื่อประสิทธิภาพ.

### แล้วเรื่องการใช้หน่วยความจำสำหรับเอกสารขนาดใหญ่ล่ะ?

Aspose.HTML ทำการสตรีมเนื้อหา ทำให้การใช้หน่วยความจำค่อนข้างต่ำ อย่างไรก็ตามรูปภาพขนาดใหญ่อาจทำให้เกิดการเพิ่มขึ้นอย่างฉับพลัน หากคุณเจอ `OutOfMemoryError` ให้พิจารณาลดความละเอียดของรูปก่อนฝัง—Aspose มี `ImageConversionOptions` สำหรับเรื่องนี้ แต่เป็นหัวข้อของบทแนะนำอื่น.

---

## สรุป

ตอนนี้คุณรู้ **วิธีฝังรูปภาพ** เมื่อแปลง MHTML เป็น PDF ด้วย Aspose.HTML แล้ว และคุณได้เห็นว่าการตั้งค่านี้แม้เล็กน้อยสามารถ **ลดขนาดไฟล์ PDF** ได้อย่างมาก ตัวอย่าง Java ที่เต็มรูปแบบพร้อมคัดลอกและวางแสดงกระบวนการทั้งหมด—from การเพิ่ม dependency ของ Maven ไปจนถึงการพิมพ์ขนาดไฟล์สุดท้าย.

ต่อจากนี้คุณอาจ:
- ทดลองใช้ `EMBED_FONTS_ONLY` หาก PDF ของคุณต้องการเป็นแบบ self‑contained อย่างสมบูรณ์.
- อัตโนมัติการแปลงเป็นชุดสำหรับโฟลเดอร์รายงานทั้งหมด.
- รวมเทคนิคนี้กับ API การปรับแต่ง PDF ของ Aspose เพื่อให้ไฟล์เล็กยิ่งขึ้น.

ไม่ว่าคุณจะสร้างบริการรายงาน, pipeline แปลงอีเมลเป็น PDF, หรือแค่ทำความสะอาดหน้าเว็บที่เก็บไว้, การควบคุมสิ่งที่ถูกฝังเป็นตัวควบคุมสำคัญสำหรับประสิทธิภาพและต้นทุน ลองใช้ ปรับแต่งตัวเลือก แล้วให้ PDF ของคุณคงความบางที่สุดเท่าที่จะเป็นไปได้.

*เขียนโค้ดให้สนุก!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}