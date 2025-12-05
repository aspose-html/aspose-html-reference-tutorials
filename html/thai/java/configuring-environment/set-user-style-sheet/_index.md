---
date: 2025-12-05
description: เรียนรู้วิธีสร้าง PDF จาก HTML โดยการตั้งค่า stylesheet ของผู้ใช้แบบกำหนดเองใน
  Aspose.HTML สำหรับ Java และแปลง HTML เป็น PDF ได้อย่างง่ายดายด้วยบริการตัวแทนผู้ใช้
language: th
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: สร้าง PDF จาก HTML – ตั้งค่าแผ่นสไตล์ผู้ใช้ใน Aspose.HTML สำหรับ Java
url: /java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF จาก HTML – ตั้งค่า User Style Sheet ใน Aspose.HTML สำหรับ Java

## Introduction
ในบทแนะนำนี้คุณจะได้เรียนรู้วิธี **สร้าง PDF จาก HTML** ด้วย Aspose.HTML สำหรับ Java พร้อมการใช้สไตล์ชีตผู้ใช้แบบกำหนดเอง  
เคยต้องการปรับแต่งลักษณะของเอกสาร HTML ของคุณด้วยสไตล์ที่เป็นเอกลักษณ์ของคุณหรือไม่? ลองนึกภาพว่าคุณกำลังสร้างหน้าเว็บและต้องการให้หัวเรื่องเด่นด้วยสีเฉพาะหรือย่อหน้ามีลักษณะสม่ำเสมอข้ามอุปกรณ์ นั่นคือจุดที่ *user stylesheet* และ **User Agent Service** เข้ามาช่วย เราจะเดินผ่านทุกขั้นตอน—from การเขียนไฟล์ HTML ง่าย ๆ, การกำหนดค่า user agent, จนถึง **แปลง HTML เป็น PDF**—เพื่อให้คุณเห็นผลลัพธ์ทันที

## Quick Answers
- **“สร้าง PDF จาก HTML” หมายถึงอะไร?** หมายถึงการเรนเดอร์เอกสาร HTML (พร้อม CSS, รูปภาพ, ฟอนต์ ฯลฯ) แล้วบันทึกผลลัพธ์เป็นไฟล์ PDF  
- **ต้องใช้คอมโพเนนต์ Aspose ใด?** ไลบรารี Aspose.HTML สำหรับ Java ให้เครื่องมือแปลงและ User Agent Service  
- **ต้องมีลิขสิทธิ์สำหรับการทดสอบหรือไม่?** สามารถใช้รุ่นทดลองฟรีสำหรับการพัฒนา; ต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง  
- **สามารถใช้ไฟล์ CSS ภายนอกได้หรือไม่?** ได้ – คุณสามารถลิงก์สไตล์ชีตภายนอกได้เช่นเดียวกับในเบราว์เซอร์ทั่วไป  
- **การแปลงใช้เวลานานแค่ไหน?** สำหรับเอกสารง่าย ๆ อย่างในคู่มือนี้ การแปลงเสร็จภายในไม่ถึงหนึ่งวินาที

## Prerequisites
ก่อนที่เราจะลงลึกในโค้ด โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

1. **Aspose.HTML สำหรับ Java** – ดาวน์โหลด JAR ล่าสุดจาก [หน้า releases ของ Aspose](https://releases.aspose.com/html/java/)  
2. **Java Development Kit (JDK) 8+** – ตรวจสอบว่า `java -version` แสดงเวอร์ชัน 8 หรือสูงกว่า  
3. **IDE** – IntelliJ IDEA, Eclipse หรือ NetBeans ก็ใช้ได้ดี  
4. **ความรู้พื้นฐาน HTML/CSS** – มีประโยชน์แต่ไม่จำเป็นต้องมีขั้นสูง

## Import Packages
เริ่มต้นด้วยการนำเข้าคลาส Java ที่จำเป็น การนำเข้าที่ต้องระบุโดยตรงสำหรับตัวอย่างนี้มีเพียง `java.io.IOException` เท่านั้น; คลาสของ Aspose จะอ้างอิงด้วยชื่อเต็มในโค้ดต่อไป

```java
import java.io.IOException;
```

## Step 1: Create a Simple HTML Document
ขั้นแรก เราจะเขียนไฟล์ HTML ขั้นต่ำ (`document.html`) ที่จะเป็นแหล่งข้อมูลสำหรับการแปลง PDF

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** เก็บไฟล์ HTML ไว้ในโฟลเดอร์เดียวกับโค้ด Java ของคุณเพื่อหลีกเลี่ยงปัญหาเกี่ยวกับเส้นทางไฟล์

## Step 2: Set Up Aspose.HTML Configuration
สร้างอ็อบเจ็กต์ `Configuration` ซึ่งทำหน้าที่เป็นคอนเทนเนอร์สำหรับบริการทั้งหมด (รวมถึง User Agent Service) ที่คุณจะใช้ต่อไป

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Step 3: Access the User Agent Service  
**User Agent Service** ช่วยให้คุณสามารถแทรกสไตล์ชีตแบบกำหนดเอง, ตั้งค่า charset เริ่มต้น, และควบคุมตัวเลือกการเรนเดอร์อื่น ๆ

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Step 4: Define and Apply the User Stylesheet  
ต่อไปเราจะกำหนดกฎ CSS ที่จะใช้สไตล์ให้กับ HTML ขณะเรนเดอร์ นี่คือขั้นตอนที่ **ใช้ user agent service** เพื่อตั้งค่าสไตล์ชีต

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Why this matters:** การใส่สไตล์ชีตระดับ user‑agent ทำให้สไตล์ถูกนำไปใช้แม้ว่า HTML ดั้งเดิมจะไม่ได้อ้างอิงไฟล์ CSS ใด ๆ

## Step 5: Load the HTML Document with the Custom Configuration  
ส่งทั้งเส้นทางไฟล์และอ็อบเจ็กต์ `Configuration` ไปยังคอนสตรัคเตอร์ของ `HTMLDocument` การทำเช่นนี้จะผูกสไตล์ชีตผู้ใช้กับเอกสาร

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Step 6: Convert HTML to PDF  
เมื่อเอกสารถูกสไตล์อย่างเต็มที่แล้ว ให้เรียกเมธอดสแตติก `convertHTML` เพื่อ **แปลง HTML เป็น PDF** อ็อบเจ็กต์ `PdfSaveOptions` ช่วยให้คุณปรับแต่งผลลัพธ์ (เช่น ขนาดหน้า, การบีบอัด)

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Result:** `user-agent-stylesheet_out.pdf` จะมีหัวเรื่องเป็นสีสีน้ำตาลและย่อหน้าพื้นหลัง GhostWhite ตามที่กำหนดในสไตล์ชีต

## Step 7: Clean Up Resources  
ควรทำการ dispose อ็อบเจ็กต์ของ Aspose เสมอเพื่อคืนหน่วยความจำเนทีฟ

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## Common Issues & Solutions
| Issue | Cause | Fix |
|-------|-------|-----|
| **Blank PDF output** | ไม่ได้ใส่สไตล์ชีตหรือไม่ได้โหลดเอกสารด้วย configuration | ตรวจสอบให้แน่ใจว่าได้ส่ง `configuration` ไปยัง `HTMLDocument` และเรียก `setUserStyleSheet` ก่อนโหลด |
| **Unsupported CSS property warning** | Aspose.HTML ไม่รองรับคุณสมบัติ CSS ขั้นสูงบางอย่าง | ใช้เฉพาะคุณสมบัติ CSS ที่ระบุในเอกสาร Aspose.HTML หรือเลือกใช้สไตล์ที่ง่ายกว่า |
| **FileNotFoundException** | เส้นทางไปยัง `document.html` ผิด | ใช้เส้นทางแบบ absolute หรือวางไฟล์ HTML ไว้ที่โฟลเดอร์รากของโปรเจกต์ |

## Frequently Asked Questions

**Q: สามารถกำหนดสไตล์ที่แตกต่างกันให้กับองค์ประกอบ HTML ต่าง ๆ ได้หรือไม่?**  
A: ได้เลย! คุณสามารถกำหนดกฎ CSS ได้ตามต้องการภายในสไตล์ชีตผู้ใช้  

**Q: ถ้าต้องการเปลี่ยนสไตล์ชีตแบบไดนามิกทำอย่างไร?**  
A: เรียก `setUserStyleSheet` อีกครั้งก่อนสร้างอินสแตนซ์ `HTMLDocument` ใหม่; สไตล์ใหม่จะถูกนำไปใช้ในการแปลงครั้งต่อไป  

**Q: สามารถใช้ไฟล์ CSS ภายนอกกับ Aspose.HTML สำหรับ Java ได้หรือไม่?**  
A: ใช่ – คุณสามารถลิงก์สไตล์ชีตภายนอกใน HTML หรือโหลดเนื้อหาแล้วส่งให้ `setUserStyleSheet`  

**Q: Aspose.HTML จัดการกับคุณสมบัติ CSS ที่ไม่รองรับอย่างไร?**  
A: คุณสมบัติที่ไม่รองรับจะถูกละเว้น ทำให้ส่วนที่เหลือของสไตล์ชีตยังคงเรนเดอร์ได้โดยไม่มีข้อผิดพลาด  

**Q: สามารถแปลง HTML ไปเป็นรูปแบบอื่นนอกจาก PDF ได้หรือไม่?**  
A: ได้, Aspose.HTML รองรับการแปลงเป็น XPS, TIFF, PNG, JPEG และรูปแบบอื่น ๆ ผ่านคลาส `SaveOptions` ที่เหมาะสม  

## Conclusion
คุณได้เรียนรู้วิธี **สร้าง PDF จาก HTML** โดยตั้งค่าสไตล์ชีตผู้ใช้แบบกำหนดเองด้วย Aspose.HTML สำหรับ Java เวิร์กโฟลว์นี้ให้คุณควบคุมลักษณะการแสดงผลของ PDF ที่สร้างได้อย่างเต็มที่ เหมาะสำหรับการสร้างรายงานอัตโนมัติ, ใบแจ้งหนี้, หรือสถานการณ์ใด ๆ ที่ต้องการสไตล์ที่สม่ำเสมอ อย่าลังเลที่จะทดลองใช้ CSS ที่ซับซ้อนขึ้น, ฟอนต์ภายนอก, หรือรูปแบบการแปลงเพิ่มเติมเพื่อขยายพื้นฐานนี้ต่อไป

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML สำหรับ Java 24.11 (ล่าสุด ณ เวลาที่เขียน)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}