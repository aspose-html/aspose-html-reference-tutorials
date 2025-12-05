---
date: 2025-12-05
description: เรียนรู้วิธีตั้งค่าขอบหน้าของ HTML ด้วย Java โดยใช้ Aspose.HTML และเพิ่มหมายเลขหน้าและหัวเรื่องลงในเอกสารของคุณ
language: th
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: วิธีตั้งค่าขอบหน้ากระดาษ HTML ด้วย Java และ Aspose.HTML
url: /java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตั้งค่าขอบหน้า HTML ด้วย Java และ Aspose.HTML

ในบทแนะนำนี้คุณจะได้เรียนรู้ **วิธีตั้งค่าขอบหน้า HTML ด้วย Java** โดยใช้ Aspose.HTML สำหรับ Java เราจะอธิบายขั้นตอนการสร้างขอบหน้าที่กำหนดเอง การแทรกหมายเลขหน้า และการเพิ่มชื่อเอกสาร — ทั้งหมดด้วยโค้ดที่ชัดเจนและทำตามขั้นตอนซึ่งคุณสามารถคัดลอกไปใช้ในโปรเจกต์ของคุณได้

## คำตอบอย่างรวดเร็ว
- **ต้องใช้ไลบรารีอะไร?** Aspose.HTML for Java  
- **ฉันสามารถควบคุมขอบหน้าโดยโปรแกรมได้หรือไม่?** ใช่ ผ่านกฎ CSS `@page` ใน user‑style sheet  
- **รูปแบบเอาต์พุตใดบ้างที่รองรับขอบหน้า?** XPS, PDF, และรูปแบบ raster อื่น ๆ  
- **ต้องการใบอนุญาตสำหรับการใช้งานในผลิตภัณฑ์หรือไม่?** จำเป็นต้องมีใบอนุญาต Aspose.HTML ที่ถูกต้องสำหรับการใช้งานที่ไม่ใช่รุ่นทดลอง  
- **รองรับ Java 11+ หรือไม่?** แน่นอน — ไลบรารีทำงานกับเวอร์ชัน Java สมัยใหม่  

## การ “ตั้งค่าขอบหน้า HTML ด้วย Java” คืออะไร?
การตั้งค่าขอบหน้า HTML ด้วย Java หมายถึงการกำหนดค่าเอนจินการแสดงผล (ที่ให้โดย Aspose.HTML) ให้ใช้คุณสมบัติ CSS page‑box ก่อนที่เอกสารจะถูกแปลงเป็นรูปแบบที่สามารถพิมพ์ได้ เช่น XPS หรือ PDF โดยการกำหนดกฎ `@page` แบบกำหนดเอง คุณจะควบคุมพื้นที่ที่พิมพ์ได้, หมายเลขหน้า, และเนื้อหา header/footer

## ทำไมต้องใช้ Aspose.HTML สำหรับการควบคุมขอบหน้า?
- **การจัดวางที่แม่นยำ** – CSS `@page` ให้การควบคุมขอบ, header, และ footer อย่างพิกเซลที่สมบูรณ์แบบ  
- **ความสอดคล้องข้ามรูปแบบ** – คำกำหนดขอบเดียวกันทำงานกับ XPS, PDF, และเอาต์พุตรูปภาพ  
- **ไม่มีการพึ่งพาเบราว์เซอร์** – การแสดงผลทำบนเซิร์ฟเวอร์ ดังนั้นคุณไม่จำเป็นต้องใช้ headless browser  

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม โปรดตรวจสอบว่าคุณได้เตรียมข้อกำหนดต่อไปนี้ไว้แล้ว:

1. **สภาพแวดล้อมการพัฒนา Java** – ติดตั้ง JDK 11 หรือใหม่กว่า  
2. **Aspose.HTML for Java** – ดาวน์โหลดและติดตั้งไลบรารีจาก [here](https://releases.aspose.com/html/java/).  

## นำเข้าแพ็กเกจ

เพื่อเริ่มต้น ให้นำเข้าคลาส Aspose.HTML ที่จำเป็น:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## วิธีตั้งค่าขอบหน้า HTML ด้วย Java – คู่มือขั้นตอนโดยละเอียด

### ขั้นตอนที่ 1: เริ่มต้น Configuration และกำหนดขอบหน้าที่กำหนดเอง

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

ในบล็อกนี้ เราจะสร้างอ็อบเจ็กต์ `Configuration` รับบริการ `IUserAgentService` และแทรกกฎ CSS `@page` ที่กำหนดขอบ, ตัวนับหน้าที่อยู่ด้านล่าง‑ขวา, และชื่อเอกสารที่อยู่ด้านบน‑กลาง

### ขั้นตอนที่ 2: สร้างเอกสาร HTML

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

ที่นี่ เราจะสร้างอินสแตนซ์ของ `HTMLDocument` ด้วยโค้ดสั้น “Hello World” การกำหนดค่าเดียวกันจากขั้นตอนที่ 1 จะถูกนำไปใช้ ดังนั้นขอบที่กำหนดเองจะถูกเคารพเมื่อเอกสารถูกแสดงผล

### ขั้นตอนที่ 3: เรนเดอร์เป็นไฟล์ XPS (หรือเอาต์พุตที่รองรับอื่นใด)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

ขั้นตอนนี้จะสร้าง `XpsDevice` ที่เขียนหน้าที่เรนเดอร์ลงใน `output.xps`. ขอบ, หมายเลขหน้า, และชื่อที่คุณกำหนดไว้ก่อนหน้านี้จะปรากฏในไฟล์สุดท้าย

## ปัญหาที่พบบ่อยและเคล็ดลับ
- **ขอบไม่เปลี่ยนแปลง** – ตรวจสอบให้แน่ใจว่ากฎ `@page` ไม่ถูกเขียนทับโดยสไตล์ชีตอื่น ๆ การเรียก `setUserStyleSheet` จะบังคับให้มีลำดับความสำคัญสูงสุด  
- **หมายเลขหน้าปรากฏเป็น “NaN”** – ตรวจสอบว่าคุณใช้ Aspose.HTML เวอร์ชัน 23.10 หรือใหม่กว่า; เวอร์ชันเก่าจะไม่มีฟังก์ชัน `currentPageNumber()`  
- **ไฟล์เอาต์พุตเป็นไฟล์เปล่า** – ยืนยันว่าเส้นทาง `Resources.output` แก้ไขได้อย่างถูกต้องและคุณมีสิทธิ์เขียน  

## คำถามที่พบบ่อย

### Q1: Aspose.HTML for Java คืออะไร?
**A:** Aspose.HTML for Java เป็นไลบรารี Java ที่ให้เครื่องมือที่ทรงพลังสำหรับการทำงานกับเอกสาร HTML ในแอปพลิเคชัน Java รวมถึงการแปลง, การเรนเดอร์, และการจัดการ  

### Q2: ฉันสามารถปรับแต่งขอบหน้าเพิ่มเติมได้หรือไม่?
**A:** ได้, เพียงแก้ไข CSS ภายใน `setUserStyleSheet`. คุณสามารถเปลี่ยนค่า `margin-*` ใด ๆ หรือเพิ่มกล่อง `@top-*` / `@bottom-*` เพิ่มเติม  

### Q3: ฉันจะเพิ่มเนื้อหาเพิ่มเติมในเอกสาร HTML ได้อย่างไร?
**A:** แทนที่สตริงใน `new HTMLDocument("<div>Hello World!!!</div>", …)` ด้วยมาร์กอัป HTML ของคุณเอง, หรือโหลดไฟล์ภายนอกโดยใช้คอนสตรัคเตอร์ `HTMLDocument(String url, …)`  

### Q4: Aspose.HTML for Java รองรับรูปแบบเอกสารอื่น ๆ หรือไม่?
**A:** แน่นอน. `HTMLDocument` เดียวกันสามารถเรนเดอร์เป็น PDF, XPS, รูปภาพ, หรือแม้แต่ EPUB โดยการสลับอุปกรณ์เอาต์พุต (เช่น `PdfDevice`, `PngDevice`)  

### Q5: ฉันต้องการใบอนุญาตสำหรับการใช้ Aspose.HTML for Java หรือไม่?
**A:** ใช่, จำเป็นต้องมีใบอนุญาตสำหรับการใช้งานในผลิตภัณฑ์ คุณสามารถรับรุ่นทดลองหรือซื้อใบอนุญาตได้จาก [here](https://purchase.aspose.com/buy) หรือ [here](https://releases.aspose.com/)  

### Q6: ฉันจะตั้งค่าขอบที่แตกต่างสำหรับหน้าคี่และหน้าเลขคู่อย่างไร?
**A:** ใช้ pseudo‑class `@page :left` และ `@page :right` ในสไตล์ชีตของคุณเพื่อกำหนดขอบที่แตกต่างสำหรับหน้าซ้าย (เลขคู) และหน้าขวา (เลขคี่)  

### Q7: ฉันสามารถฝังฟอนต์ที่กำหนดเองในเอกสารที่เรนเดอร์ได้หรือไม่?
**A:** ได้. เพิ่มกฎ `@font-face` ลงใน user style sheet และอ้างอิงฟอนต์ในเนื้อหา HTML ของคุณ  

## สรุป

คุณได้เรียนรู้ **วิธีตั้งค่าขอบหน้า HTML ด้วย Java** ด้วย Aspose.HTML แล้ว และคุณรู้วิธีเพิ่มหมายเลขหน้าและชื่อเอกสารเพื่อทำให้เอกสารของคุณดูเป็นมืออาชีพ อย่าลังเลที่จะทดลองใช้กล่อง `@page` เพิ่มเติม, ฟอนต์ที่กำหนดเอง, หรือรูปแบบเอาต์พุตต่าง ๆ เพื่อให้เหมาะกับความต้องการของโครงการของคุณ

หากคุณพบปัญหาใด ๆ เอกสารอย่างเป็นทางการของ [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/) และ [Aspose support forum](https://forum.aspose.com/) เป็นแหล่งข้อมูลที่ยอดเยี่ยมสำหรับการขอความช่วยเหลือ

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 23.12  
**Author:** Aspose  

---