---
category: general
date: 2026-05-31
description: ปิดการใช้งานรูปภาพภายนอกเมื่อคุณแปลงหน้าเว็บเป็น PNG ใน Java ด้วย Aspose
  HTML. เรียนรู้วิธีโหลดหน้าเว็บใน sandbox อย่างปลอดภัยและบันทึกเอกสาร HTML เป็น PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: th
og_description: ปิดการใช้งานรูปภาพภายนอกเมื่อเรนเดอร์หน้าเว็บเป็น PNG ใน Java คู่มือขั้นตอนต่อขั้นตอนนี้แสดงวิธีโหลดหน้าเว็บใน
  sandbox และบันทึกเอกสาร HTML เป็น PNG.
og_title: ปิดการใช้งานรูปภาพภายนอกขณะเรนเดอร์หน้าเว็บเป็น PNG ใน Java
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: ปิดการใช้งานรูปภาพภายนอกขณะเรนเดอร์หน้าเว็บเป็น PNG ด้วย Java
url: /th/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ปิดการใช้งานรูปภาพภายนอกขณะเรนเดอร์หน้าเว็บเป็น PNG ใน Java

เคยต้อง **ปิดการใช้งานรูปภาพภายนอก** เมื่อคุณเรนเดอร์หน้าเว็บเป็น PNG ด้วย Java หรือไม่? บางทีคุณอาจกำลังสร้างบริการสร้างภาพย่อที่ต้องแยกออกจากอินเทอร์เน็ตสาธารณะ หรือคุณแค่ต้องการรับประกันว่าไม่มีรูปภาพของบุคคลที่สามรั่วไหลระหว่างการแปลง ไม่ว่ากรณีใด คุณมาถูกที่แล้ว

ในบทเรียนนี้เราจะอธิบายขั้นตอนการโหลดหน้าเว็บใน sandbox, ปิดการดึงรูปภาพภายนอก, และสุดท้ายบันทึกเอกสาร HTML เป็นไฟล์ PNG—ทั้งหมดด้วย Aspose.HTML for Java. เมื่อเสร็จคุณจะได้ตัวอย่างที่พร้อมรัน พร้อมเคล็ดลับปฏิบัติที่ช่วยหลีกเลี่ยงปัญหาที่พบบ่อย

## สิ่งที่คุณจะได้เรียนรู้

- **วิธีเรนเดอร์ HTML เป็นภาพใน Java** ด้วย `Converter` ของ Aspose.HTML
- ขั้นตอนที่แม่นยำในการ **โหลดหน้าเว็บใน sandbox** พร้อม viewport และ DPI ที่กำหนดเอง
- การตั้งค่าที่จำเป็นเพื่อ **ปิดการใช้งานรูปภาพภายนอก** ขณะยังคงเรนเดอร์หน้าเว็บได้
- วิธี **บันทึกเอกสาร HTML เป็น PNG** (หรือรูปแบบที่รองรับอื่น) ลงดิสก์
- การจัดการกรณีขอบ, เคล็ดลับประสิทธิภาพ, และคำแนะนำการแก้ไขปัญหา

### ข้อกำหนดเบื้องต้น

- ติดตั้ง Java 8 หรือใหม่กว่า (โค้ดทำงานได้กับ JDK 11+ ด้วย)
- มี Maven หรือ Gradle เพื่อดึงไลบรารี Aspose.HTML for Java
- มีความคุ้นเคยพื้นฐานกับไวยากรณ์ Java และการจัดการข้อยกเว้น
- มีการเชื่อมต่ออินเทอร์เน็ตสำหรับการโหลดหน้าเว็บครั้งแรก (ยกเว้นคุณให้บริการ HTML ภายในเครื่อง)

> **เคล็ดลับ:** หากคุณทำงานอยู่หลังพร็อกซีขององค์กร ให้ตั้งค่าคุณสมบัติ JVM `http.proxyHost` และ `http.proxyPort` ก่อนรันตัวอย่าง

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และเพิ่ม Aspose.HTML

เริ่มแรก—เพิ่ม dependency ของ Aspose.HTML หากคุณใช้ Maven ให้ใส่โค้ดนี้ลงในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

สำหรับ Gradle ให้ใช้โค้ดที่เทียบเท่า:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

เมื่อไลบรารีอยู่ใน classpath แล้ว คุณก็พร้อมเริ่มเขียนโค้ด

---

## ขั้นตอนที่ 2: **ปิดการใช้งานรูปภาพภายนอก** ด้วยสภาพแวดล้อม Sandbox

หัวใจของวิธีแก้คือ `DocumentSandbox` โดยส่งค่า `false` ให้กับพารามิเตอร์ *allowExternalImages* เราจะบอก Aspose.HTML ให้ละเลยแท็ก `<img>` ที่ชี้ไปยัง URL ภายนอก นี่คือกลไกที่ **ปิดการใช้งานรูปภาพภายนอก** อย่างแม่นยำ

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **ทำไมต้องทำเช่นนี้:** หากไม่มี sandbox ตัวเรนเดอร์จะพยายามดาวน์โหลดรูปภาพทุกภาพที่หน้าเว็บอ้างอิง ซึ่งอาจทำให้ช้า ไม่เสถียร หรือเสี่ยงต่อความปลอดภัย การตั้งค่าสถานะเป็น `false` จะรับประกันการเรนเดอร์ที่สะอาดและเป็นอิสระจากแหล่งภายนอก

---

## ขั้นตอนที่ 3: **โหลดหน้าเว็บใน Sandbox**  

ต่อไปเราจะชี้ Aspose.HTML ไปยัง URL ที่ต้องการจับภาพ ตัวสร้าง `HTMLDocument` รับอินสแตนซ์ sandbox เป็นพารามิเตอร์และจะใช้ข้อจำกัดที่เรากำหนดโดยอัตโนมัติ

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

หากหน้าเว็บพึ่งพา script ภายนอกอย่างหนักเพื่อจัดวางคุณอาจพบว่าเนื้อหาบางส่วนหายไป เพราะเรายังได้ปิดการใช้งานสคริปต์ด้วย ในกรณีนั้นให้สลับค่า `allowExternalScripts` เป็น `true` แต่คง `allowExternalImages` เป็น `false`

---

## ขั้นตอนที่ 4: **เรนเดอร์หน้าเว็บเป็น PNG**  

เมื่อเอกสารถูกโหลดแล้ว การแปลงเป็นภาพทำได้ด้วยบรรทัดเดียวผ่าน `Converter.convert` ตัวเลือก `ImageSaveOptions` ให้คุณเลือกฟอร์แมตของไฟล์ผลลัพธ์; ที่นี่เราเลือก PNG

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

ไฟล์ที่ได้ `sandboxed.png` จะเป็นภาพสแนปช็อตของหน้าเว็บ **โดยไม่มีรูปภาพภายนอก**—เหลือเพียง SVG ฝังในตัวหรือกราฟิกที่เข้ารหัสเป็น base64 หากมี

---

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์และแก้ไขปัญหาที่พบบ่อย

หลังจากรันโปรแกรมแล้ว เปิดไฟล์ `sandboxed.png` ด้วยโปรแกรมดูภาพใดก็ได้ คุณควรเห็นเลย์เอาต์ของหน้า, ข้อความ, และสไตล์ CSS, แต่ทุก `<img src="http://…">` จะเป็นช่องว่าง (มักแสดงเป็นสี่เหลี่ยมสีขาวหรือถูกละเว้นทั้งหมด)

### ปัญหาที่พบบ่อยและวิธีแก้

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---|---|---|
| หน้าเปล่า | URL ปลายทางบล็อกคำขอ (เช่น Cloudflare) | เพิ่ม header ที่เหมาะสมให้กับ user‑agent ของ sandbox หรือใช้พร็อกซี |
| ฟอนต์หาย | ไฟล์ฟอนต์โฮสต์อยู่ภายนอก | ติดตั้งฟอนต์ในเครื่องหรือฝังเป็น `@font-face` ด้วย data URI |
| เลย์เอาต์เปลี่ยน | CSS อ้างอิง stylesheet ภายนอกที่ถูกบล็อก | ตั้งค่า `allowExternalScripts` เป็น `true` *เฉพาะ* สำหรับการโหลด CSS แล้วรันใหม่ |
| `java.lang.OutOfMemoryError` | เรนเดอร์หน้าใหญ่ที่ DPI สูง | ลดขนาด viewport หรือ DPI, หรือเพิ่ม heap ของ JVM (`-Xmx2g`) |

---

## ขั้นตอนที่ 6: ขยายตัวอย่าง – บันทึกเป็นฟอร์แมตอื่น

โค้ดเดียวกันทำงานได้กับ JPEG, BMP หรือแม้แต่ PDF เพียงเปลี่ยนค่า enum `SaveFormat`:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

หากต้องการ PDF ให้แทนที่ `ImageSaveOptions` ด้วย `PdfSaveOptions` แล้วปรับนามสกุลไฟล์ให้สอดคล้อง

---

## ตัวอย่างทำงานเต็มรูปแบบ (คัดลอก‑วางได้)

ด้านล่างเป็น **โปรแกรมที่สมบูรณ์และพร้อมรัน** สร้างคลาส Java ใหม่, วางโค้ดนี้, ตรวจสอบให้โฟลเดอร์ `output` มีอยู่, แล้วรัน

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (คอนโซล):

```
PNG image saved to: output/sandboxed.png
```

เปิด `sandboxed.png` – คุณจะเห็นหน้าเว็บที่เรนเดอร์ **โดยไม่มีรูปภาพภายนอก** เลย

---

## คำถามที่พบบ่อย

**ถาม: ยังสามารถแสดงรูปภาพที่ฝังอยู่ใน HTML ได้หรือไม่?**  
ตอบ: ได้. URI แบบ `data:` หรือรูปภาพที่เข้ารหัสเป็น base64 ถือเป็นส่วนหนึ่งของเอกสารและจะปรากฏใน PNG

**ถาม: ถ้าต้องการเก็บรูปภาพภายนอกบางส่วนไว้แต่บล็อกส่วนอื่นทำอย่างไร?**  
ตอบ: Sandbox ทำงานแบบเปิดหรือปิดทั้งหมด สำหรับการควบคุมระดับละเอียด ให้ดาวน์โหลดรูปภาพที่อนุญาตเอง, ฝังเป็น data URI, แล้วจึงเรนเดอร์

**ถาม: วิธีนี้ทำงานบนเซิร์ฟเวอร์แบบ headless ได้หรือไม่?**  
ตอบ: ได้เลย. Aspose.HTML เป็นไลบรารี pure‑Java; ไม่ต้องการเซิร์ฟเวอร์แสดงผลหรือเอนจินเบราว์เซอร์

**ถาม: แตกต่างจากการใช้ Selenium หรือ Puppeteer อย่างไร?**  
ตอบ: Selenium ควบคุมเบราว์เซอร์จริงซึ่งหนักและยากต่อการ sandbox ส่วน Aspose.HTML เรนเดอร์ HTML ภายในหน่วยความจำโดยตรง ให้ประสิทธิภาพคาดเดาได้และควบคุมความปลอดภัยง่ายกว่า เช่น **ปิดการใช้งานรูปภาพภายนอก**

---

## สรุป

ตอนนี้คุณมีสูตรครบวงจรสำหรับ **การปิดการใช้งานรูปภาพภายนอกขณะเรนเดอร์หน้าเว็บเป็น PNG ใน Java** ด้วย `DocumentSandbox` คุณจะได้การควบคุมที่แน่นหนาต่อทรัพยากรภายนอก, ทำให้ระบบปลอดภัยและผลลัพธ์สอดคล้องกัน จากนี้คุณสามารถทดลองเปลี่ยนขนาด viewport, DPI, หรือฟอร์แมตผลลัพธ์—แต่ละการปรับแต่งเปิดโอกาสใหม่สำหรับการสร้างภาพย่อ, ตัวอย่างพรีวิว, หรือการเก็บสำเนาแบบถาวร

พร้อมรับความท้าทายต่อไปหรือยัง? ลองเรนเดอร์หลาย URL พร้อมกันแบบขนาน, หรือผสานโลจิกนี้เข้าไปใน microservice ของ Spring Boot ที่ให้บริการ PNG ตามคำขอ ความเป็นไปไม่มีขีดจำกัดเมื่อคุณรวมความยืดหยุ่นของ Aspose.HTML กับเครื่องมือคอนคอร์เรนซีของ Java

Happy coding, และอย่าลืมแชร์เรื่องราวความสำเร็จของคุณในคอมเมนต์!

## สิ่งที่ควรเรียนต่อ

- [วิธีใช้ Aspose เพื่อเรนเดอร์ HTML เป็น PNG – คู่มือขั้นตอน](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [วิธีเรนเดอร์ HTML เป็น PNG ด้วย Aspose – คู่มือฉบับสมบูรณ์](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [วิธีแก้ไข CSS - การแก้ไข CSS ภายนอกขั้นสูงด้วย Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}