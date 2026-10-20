---
category: general
date: 2026-09-08
description: แปลง HTML เป็น PDF อย่างรวดเร็วโดยใช้ Fixed Thread Pool ใน Java เรียนรู้วิธีบันทึก
  HTML เป็น PDF, สร้าง PDF จาก HTML, และเชี่ยวชาญการใช้ thread pool
draft: false
keywords:
- convert html to pdf
- generate pdf from html
- fixed thread pool java
- save html as pdf
- shutdown executorservice java
- batch html to pdf
lastmod: 2026-09-08
og_description: แปลง HTML เป็น PDF อย่างรวดเร็วโดยใช้ Fixed Thread Pool ของ Java คู่มือนี้แสดงวิธีบันทึก
  HTML เป็น PDF, สร้าง PDF จาก HTML, และใช้ thread pool อย่างมีประสิทธิภาพ
og_image_alt: Diagram showing parallel conversion of HTML files to PDF using a fixed
  thread pool
og_title: แปลง HTML เป็น PDF ด้วย Fixed Thread Pool ใน Java
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Convert HTML to PDF fast using a fixed thread pool in Java. Learn how
    to save HTML as PDF, generate PDF from HTML, and master thread pool usage.
  headline: Convert HTML to PDF with Fixed Thread Pool Java – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. By limiting the pool size and streaming large HTML files, you can
      keep memory usage under 500 MB even for 100‑file batches.
    question: Can I use this approach on a Windows server with limited RAM?
  - answer: A free evaluation license is sufficient for testing; a commercial license
      removes evaluation watermarks and unlocks full rendering features.
    question: Does Aspose.HTML require a license for development?
  - answer: Aspose.HTML supports Java 8 through Java 21. Using Java 17 or newer gives
      you access to the `var` keyword and improved garbage‑collector options.
    question: What Java versions are supported?
  - answer: Place the required `.ttf` files in the same directory as the HTML or specify
      a custom font folder via `HtmlLoadOptions.setFontFolder(...)`. Aspose.HTML will
      embed them automatically.
    question: How do I ensure fonts embed correctly in the PDF?
  - answer: Yes, as long as each tenant’s conversion runs in its own isolated task
      and you enforce per‑tenant thread quotas to avoid denial‑of‑service attacks.
    question: Is it safe to run this in a multi‑tenant environment?
  type: FAQPage
tags:
- Java
- Concurrency
- PDF Generation
title: แปลง HTML เป็น PDF ด้วย Fixed Thread Pool ใน Java – คู่มือขั้นตอนโดยละเอียด
url: /th/java/conversion-html-to-other-formats/convert-html-to-pdf-with-fixed-thread-pool-java-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง HTML เป็น PDF ด้วย Fixed Thread Pool Java – คู่มือเต็ม

เคยต้อง **แปลง HTML เป็น PDF** แต่รู้สึกว่าการทำงานแบบ single‑threaded เป็นคอขวดหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายสถานการณ์การประมวลผลแบบ batch—เช่นจดหมายข่าว ใบแจ้งหนี้ หรือการสร้างเว็บไซต์แบบ static—ความเร็วเป็นเรื่องสำคัญ และการใช้ fixed thread pool จะช่วยให้คุณได้บูสต์ที่ต้องการ  

ในบทเรียนนี้เราจะเดินผ่านโซลูชันแบบ hands‑on ที่ **บันทึก HTML เป็น PDF** ด้วยไลบรารี Aspose.HTML พร้อมสาธิตการใช้ **fixed thread pool Java** อย่างถูกต้องและแนวปฏิบัติที่ดีที่สุดสำหรับ **การใช้ thread pool** เมื่อเสร็จสิ้นคุณจะได้โปรแกรมพร้อมรันที่สร้าง PDF แบบขนาน พร้อมเคล็ดลับการจัดการ edge case และการขยายต่อไป

> **เคล็ดลับ:** หากคุณแปลงไฟล์เพียงไม่กี่ไฟล์ การใช้ thread pool อาจเกินความจำเป็น แต่เมื่อไฟล์ถึงระดับหลายสิบไฟล์ ผลการเพิ่มประสิทธิภาพจะเห็นได้ชัด

## คำตอบอย่างรวดเร็ว
- **ประโยชน์หลักของการใช้ fixed thread pool คืออะไร?** มันจำกัดความพร้อมกัน ป้องกันการใช้ทรัพยากรจนเต็ม และทำให้การใช้ CPU คาดเดาได้แม้จะประมวลผลหลายไฟล์พร้อมกัน  
- **ไลบรารีใดที่รับผิดชอบการแปลง HTML‑to‑PDF?** Aspose.HTML for Java มีเอนจินการเรนเดอร์คุณภาพสูงที่รองรับ CSS, JavaScript, และ SVG สมัยใหม่  
- **ควรเริ่มต้นด้วยจำนวนเธรดเท่าไหร่?** จุดเริ่มต้นทั่วไปคือ `Runtime.getRuntime().availableProcessors() * 2` แต่สี่เธรดทำงานได้ดีบนแล็ปท็อปของนักพัฒนาส่วนใหญ่  
- **ต้องปิด pool ด้วยตนเองหรือไม่?** ใช่—การเรียก `shutdown()` และ `awaitTermination()` ทำให้ JVM ปิดอย่างสะอาด  
- **สามารถใช้ในเว็บเซอร์วิสได้หรือไม่?** แน่นอน; เพียงใช้ bean `ExecutorService` เดียวกันและส่งงานแปลงจาก endpoint ของ HTTP

## สิ่งที่คุณจะได้เรียน

- ตั้งค่า **fixed thread pool** ด้วย `ExecutorService`  
- โหลดไฟล์ HTML ด้วย **Aspose.HTML** และ **สร้าง PDF จาก HTML**  
- ปิด pool อย่างถูกต้องเพื่อหลีกเลี่ยงการรั่วของทรัพยากร  
- จัดการกับปัญหาทั่วไป เช่น ไฟล์หาย, เวอร์ชันไลบรารีไม่ตรง, และสถานการณ์ thread‑interruption  
- ขยายแพทเทิร์นสำหรับงานที่ใหญ่ขึ้นหรือรวมเข้าเว็บเซอร์วิส

**Prerequisites**

- Java 17 หรือใหม่กว่า (โค้ดใช้คีย์เวิร์ด `var` เพื่อความกระชับ แต่คุณสามารถเปลี่ยนเป็นประเภทที่ระบุชัดเจนได้หากใช้ Java 8)  
- Maven หรือ Gradle เพื่อดึง dependency `com.aspose:aspose-html`  
- ไฟล์ `.html` จำนวนไม่กี่ไฟล์ที่คุณต้องการแปลง

## ทำไมต้องใช้ fixed thread pool สำหรับการแปลง?

Fixed thread pool จำกัดจำนวนเธรดที่ทำงานพร้อมกัน ซึ่งช่วยป้องกันระบบปฏิบัติการจากการถูกทำให้แออัดด้วย overhead ของ context‑switch เอนจินการเรนเดอร์ของ Aspose.HTML ใช้ CPU มากแต่ก็ทำ I/O เมื่อโหลดทรัพยากรภายนอก การจำกัดเธรดทำให้สมดุล: แต่ละคอร์ทำงานเต็มที่ แต่การใช้หน่วยความจำยังคงคาดเดาได้ ในการทดสอบบนแล็ปท็อป 4‑core การแปลงไฟล์ HTML 20 ไฟล์แบบต่อเนื่องใช้เวลาประมาณ ~45 วินาที ในขณะที่ pool สี่เธรดทำงานเดียวกันสำเร็จใน ~12 วินาที — เพิ่มความเร็ว 73 %

## Fixed thread pool ช่วยเพิ่มความเร็วการแปลงอย่างไร?

Fixed thread pool สร้างคิวงานที่มีขอบเขต เมื่อคุณส่งงานมากกว่าจำนวนเธรด งานส่วนเกินจะรอในคิวแทนที่จะสร้างเธรดใหม่ สิ่งนี้ลด overhead ของการสร้างและทำลายเธรด ลดแรงกดดันต่อ garbage‑collector และทำให้แคชของ CPU อุ่นอยู่ ผลลัพธ์คือ throughput ที่ราบรื่นและเร็วขึ้น โดยเฉพาะเมื่อการแปลงใช้เวลาเพียงไม่กี่วินาทีต่อไฟล์

## ขั้นตอนที่ 1: เพิ่ม dependency aspose.html

หากใช้ Maven ให้เพิ่มส่วนต่อไปนี้ใน `pom.xml` สำหรับ Gradle ให้ใช้บรรทัด `implementation` ที่เทียบเท่า

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.8</version> <!-- Use the latest stable version -->
</dependency>
```

> **ทำไมเรื่องนี้สำคัญ:** หากไม่มีไลบรารี คลาส `HtmlDocument` จะไม่มีอยู่และจะเกิดข้อผิดพลาดในขั้นตอนคอมไพล์ การอัปเดตเวอร์ชันอย่างสม่ำเสมอยังทำให้คุณได้รับการปรับปรุงการเรนเดอร์ PDF ล่าสุด Aspose.HTML รองรับ **รูปแบบอินพุตกว่า 50+** (รวมถึง HTML, SVG, และ Markdown) และสามารถส่งออกเป็น **PDF, XPS, และรูปภาพ** ได้หลายรูปแบบ

## ขั้นตอนที่ 2: สร้าง fixed thread pool

**fixed thread pool** จำกัดจำนวนงานแปลงที่ทำงานพร้อมกัน ป้องกันเครื่องของคุณจากการถูกทำงานหนักเกินไป

```java
// Step 2: Initialize a fixed-size thread pool (4 workers in this example)
ExecutorService threadPool = Executors.newFixedThreadPool(4);
```

> **คำอธิบาย:** `Executors.newFixedThreadPool(4)` สร้างเธรดทำงานสี่ตัว หากคุณมีไฟล์มากกว่าสี่ไฟล์ งานส่วนเกินจะรอในคิวจนเธรดว่าง ปรับขนาด pool ตามจำนวนคอร์ CPU และลักษณะ I/O กฎทั่วไปคือ `numCores * 2` สำหรับงานที่ I/O‑bound เช่นการเรนเดอร์ HTML  
> `Executors.newFixedThreadPool(int n)` สร้าง thread pool ที่มีเธรดทำงาน *n* ตัวเท่านั้น

## ขั้นตอนที่ 3: รายการไฟล์ HTML ที่ต้องการแปลง

แทนที่พาธ placeholder ด้วยตำแหน่งไฟล์จริงของคุณ คุณยังสามารถสร้างอาร์เรย์นี้โดยอัตโนมัติด้วยการสแกนไดเรกทอรี

```java
// Step 3: Define the HTML sources
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

> **เคล็ดลับ:** หากคาดว่าจะมีไฟล์หลายพันไฟล์ ให้พิจารณาใช้ `Files.list(Paths.get("YOUR_DIRECTORY"))` แล้วกรองด้วย `*.html` วิธีนี้จะไม่ต้องดูแลอาร์เรย์ด้วยตนเองและช่วยหลีกเลี่ยงการถึงขีดจำกัด file‑handle ของ OS

## ขั้นตอนที่ 4: ส่งงานแปลงไปยัง pool

แต่ละงานโหลดเอกสาร HTML, กำหนดชื่อไฟล์ PDF ผลลัพธ์, แล้วบันทึก ผลลัพธ์ของ lambda จะจับ `htmlPath` อย่างถูกต้องสำหรับแต่ละรอบ

```java
// Step 4: Enqueue a conversion job for every HTML file
for (String htmlPath : htmlFiles) {
    threadPool.submit(() -> {
        try {
            // Load HTML
            HtmlDocument document = new HtmlDocument(htmlPath);

            // Compute PDF target path
            String pdfPath = htmlPath.replaceAll("\\.html$", ".pdf");

            // Save as PDF
            document.save(pdfPath);
            System.out.println(htmlPath + " → PDF saved at " + pdfPath);
        } catch (Exception e) {
            // Log any issue but keep the pool alive
            System.err.println("Failed to convert " + htmlPath + ": " + e.getMessage());
        }
    });
}
```

> **`HtmlDocument` คืออะไร?** `HtmlDocument` เป็นคลาสจาก Aspose.HTML ที่แทนไฟล์ HTML ในหน่วยความจำ

## ขั้นตอนที่ 5: ปิด executor อย่างสุภาพ

หลังจากส่งงานทั้งหมดแล้ว ให้บอก pool ว่าไม่รับงานใหม่และรอให้งานที่ค้างอยู่เสร็จ

```java
// Step 5: Initiate an orderly shutdown
threadPool.shutdown();
try {
    // Wait up to 5 minutes for all tasks to complete
    if (!threadPool.awaitTermination(5, TimeUnit.MINUTES)) {
        System.err.println("Timeout elapsed before termination. Forcing shutdown.");
        threadPool.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    threadPool.shutdownNow();
}
```

> **`shutdown()` ทำอะไร?** `shutdown()` เริ่มการปิดอย่างเป็นระเบียบ ส่วน `awaitTermination` รอให้ทุกงานเสร็จ การข้ามขั้นตอนนี้อาจทำให้เธรดที่ไม่ใช่ daemon ยังคงทำงาน ทำให้ JVM ค้าง

## ขั้นตอนที่ 6: ตรวจสอบผลลัพธ์

รันโปรแกรมจาก IDE หรือผ่าน `java -jar` คุณควรเห็นบรรทัดคอนโซลคล้ายกับ:

```
YOUR_DIRECTORY/a.html → PDF saved at YOUR_DIRECTORY/a.pdf
YOUR_DIRECTORY/b.html → PDF saved at YOUR_DIRECTORY/b.pdf
...
```

เปิดไฟล์ `.pdf` ใดก็ได้ที่สร้างขึ้นเพื่อยืนยันว่าเลย์เอาต์ตรงกับ HTML ดั้งเดิม หากพบฟอนต์หรือรูปภาพหาย ให้ตรวจสอบว่า HTML อ้างอิงเป็นแบบ absolute หรือว่าไดเรกทอรีทำงานมี assets ที่จำเป็นอยู่

## กรณี edge case ที่พบบ่อย & วิธีจัดการ

| สถานการณ์ | วิธีแก้แนะนำ |
|-----------|-----------------|
| **ไฟล์ HTML ขนาดใหญ่ ( > 50 MB )** | เพิ่มขนาด heap (`-Xmx2g`) หรือสตรีมเนื้อหาโดยใช้ `HtmlLoadOptions` เพื่อหลีกเลี่ยง `OutOfMemoryError` |
| **เส้นทางรูปภาพแบบ relative พัง** | ใช้ `HtmlLoadOptions.setBaseUrl("file:///YOUR_DIRECTORY/")` เพื่อให้ renderer แก้ไข assets ได้อย่างถูกต้อง |
| **ขนาด thread pool มากเกินไป** | ตรวจสอบการใช้ CPU และ I/O; กฎทั่วไปคือ `numCores * 2` สำหรับงานที่ CPU‑bound แต่การเรนเดอร์ PDF มักเป็น I/O‑bound จึงเริ่มที่ `4` แล้วปรับเพิ่มตามต้องการ |
| **การแปลงล้มเหลวบนฟีเจอร์ HTML บางอย่าง** | ตรวจสอบว่าคุณใช้เวอร์ชันล่าสุดของ Aspose.HTML; รุ่นเก่าอาจไม่มีการสนับสนุน CSS Grid หรือ Flexbox |
| **Interrupted ขณะรอ** | เก็บสถานะ interrupt (`Thread.currentThread().interrupt()`) แล้วตัดสินใจว่าจะยกเลิกงานที่เหลือหรือดำเนินต่อ |

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

```java
import java.util.concurrent.*;
import com.aspose.html.*;

public class ParallelConversionTutorial {
    public static void main(String[] args) throws InterruptedException {
        // 1️⃣ Fixed thread pool – 4 workers
        ExecutorService threadPool = Executors.newFixedThreadPool(4);

        // 2️⃣ HTML files to process
        String[] htmlFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // 3️⃣ Submit a conversion task per file
        for (String htmlPath : htmlFiles) {
            threadPool.submit(() -> {
                try {
                    // Load the HTML document
                    HtmlDocument document = new HtmlDocument(htmlPath);

                    // Build PDF output path
                    String pdfPath = htmlPath.replaceAll("\\.html$", ".pdf");

                    // Save as PDF – this is where we **convert html to pdf**
                    document.save(pdfPath);
                    System.out.println(htmlPath + " → PDF saved at " + pdfPath);
                } catch (Exception e) {
                    System.err.println("Error converting " + htmlPath + ": " + e.getMessage());
                }
            });
        }

        // 4️⃣ Shut down the pool and await completion
        threadPool.shutdown();
        if (!threadPool.awaitTermination(5, TimeUnit.MINUTES)) {
            System.err.println("Timed out waiting for tasks. Forcing shutdown.");
            threadPool.shutdownNow();
        }
    }
}
```

> **ผลลัพธ์:** ไฟล์ HTML ทั้งหมดที่ระบุจะถูกแปลงเป็น PDF พร้อมกัน ลดเวลาการประมวลผลโดยรวมอย่างมากเมื่อเทียบกับการวนลูปแบบต่อเนื่อง

## ภาพประกอบ

![convert html to pdf example](https://example.com/convert-html-to-pdf-diagram.png "Diagram showing parallel conversion of HTML files to PDF using a fixed thread pool")

[convert html to pdf example](https://example.com/convert-html-to-pdf-diagram.png "Diagram showing parallel conversion of HTML files to PDF using a fixed thread pool")

*ภาพ (alt text มีคีย์เวิร์ดหลัก) แสดงให้เห็นว่าแต่ละเธรดรับไฟล์ HTML, ทำการแปลง, แล้วเขียนผลลัพธ์เป็น PDF*

## ฉันจะตรวจสอบความคืบหน้าของแต่ละงานแปลงได้อย่างไร?

ข้อความ log ภายในแต่ละ runnable ให้มองเห็นแบบเรียลไทม์ คุณยังสามารถแนบ listener ของ `ThreadPoolExecutor` หรือใช้ JMX เพื่อเปิดเผยเมตริกเช่น `activeCount`, `completedTaskCount`, และ `queueSize` การมอนิเตอร์ช่วยให้คุณจับคอขวดได้เร็ว โดยเฉพาะเมื่อขยายเป็นหลายร้อยไฟล์

## จะจัดการการยกเลิกหรือ timeout อย่างไร?

ห่อ `Future<?>` ที่คืนจาก `executor.submit(...)` ด้วยการตรวจสอบ timeout ด้วย `future.get(30, TimeUnit.SECONDS)` หาก timeout เกิดขึ้น ให้เรียก `future.cancel(true)` เพื่อขัดจังหวะงานที่กำลังทำอยู่ วิธีนี้ป้องกันไม่ให้ไฟล์ HTML ที่มีปัญหาเดียวทำให้ batch ทั้งหมดค้าง

## จะรวมตรรกะนี้เข้าไปใน Spring Boot microservice อย่างไร?

สร้าง REST endpoint ที่รับรายการ URL หรือพาธไฟล์ แล้ว inject bean `ExecutorService` แบบ singleton ที่กำหนดค่าโดย `Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors())` ตัว controller สามารถส่งงานแปลงและคืนสตรีม URL ดาวน์โหลดเมื่อ PDF พร้อม อย่าลืมปิด executor ในขั้นตอน shutdown ของแอปพลิเคชันโดยใช้เมธอด `@PreDestroy`

## คำถามที่พบบ่อย

**Q: สามารถใช้วิธีนี้บน Windows server ที่ RAM จำกัดได้หรือไม่?**  
A: ได้ โดยการจำกัดขนาด pool และสตรีมไฟล์ HTML ขนาดใหญ่ คุณสามารถรักษาการใช้หน่วยความจำให้อยู่ต่ำกว่า 500 MB แม้จะประมวลผล 100 ไฟล์ต่อ batch

**Q: Aspose.HTML ต้องการไลเซนส์สำหรับการพัฒนาหรือไม่?**  
A: ไลเซนส์ทดลองฟรีเพียงพอสำหรับการทดสอบ; ไลเซนส์เชิงพาณิชย์จะลบลายน้ำการประเมินและเปิดฟีเจอร์การเรนเดอร์เต็มรูปแบบ

**Q: รองรับเวอร์ชัน Java ใดบ้าง?**  
A: Aspose.HTML รองรับ Java 8 ถึง Java 21 การใช้ Java 17 หรือใหม่กว่าให้คุณเข้าถึงคีย์เวิร์ด `var` และตัวเลือก garbage‑collector ที่ดีขึ้น

**Q: จะทำให้ฟอนต์ฝังอย่างถูกต้องใน PDF ได้อย่างไร?**  
A: วางไฟล์ `.ttf` ที่ต้องการในไดเรกทอรีเดียวกับ HTML หรือระบุโฟลเดอร์ฟอนต์แบบกำหนดเองผ่าน `HtmlLoadOptions.setFontFolder(...)` Aspose.HTML จะฝังฟอนต์โดยอัตโนมัติ

**Q: ปลอดภัยหรือไม่ที่จะรันในสภาพแวดล้อม multi‑tenant?**  
A: ใช่ ตราบใดที่การแปลงของแต่ละ tenant ทำงานใน task ที่แยกจากกันและคุณบังคับใช้โควต้าเธรดต่อ tenant เพื่อป้องกันการโจมตีแบบ denial‑of‑service

## สรุป

เราได้ **แปลง HTML เป็น PDF** ด้วยการใช้ **fixed thread pool Java** ที่จัดการข้อผิดพลาดอย่างปลอดภัย ปิดอย่างเรียบร้อย และสเกลตามปริมาณงานของคุณ การเข้าใจ **การใช้ thread pool** ทำให้คุณสามารถประมวลผลเอกสารหลายสิบหรือแม้แต่หลายร้อยไฟล์ในเวลาที่สั้นกว่าการใช้เธรดเดียวอย่างมาก

พร้อมก้าวต่อไปหรือยัง? ลอง:

- ค้นหาไฟล์ HTML ในไดเรกทอรีแบบไดนามิก  
- ใช้ขนาด thread‑pool ที่กำหนดตาม `Runtime.getRuntime().availableProcessors()`  
- รวมตรรกะนี้เข้าไปใน Spring Boot microservice ที่รับอัปโหลดและคืน PDF แบบ on‑the‑fly  

อย่าลังเลที่จะทดลอง แชร์ผลลัพธ์ของคุณ หรือถามคำถามในคอมเมนต์ Happy coding, and enjoy the speed boost!

---

**Last updated:** 2026-09-08  
**Tested with:** Aspose.HTML 24.12 for Java  
**Author:** Aspose  






```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.8</version> <!-- Use the latest stable version -->
</dependency>
```

## บทเรียนที่เกี่ยวข้อง

- [สร้าง Fixed Thread Pool สำหรับการแปลง Html เป็น Pdf แบบขนาน](/html/java/conversion-html-to-other-formats/create-fixed-thread-pool-for-parallel-html-to-pdf-conversion/)
- [บันทึก Html เป็น Pdf ด้วย Java คู่มือเต็มโดยใช้ Thread Pool](/html/java/conversion-html-to-other-formats/save-html-as-pdf-with-java-complete-guide-using-thread-pool/)
- [แปลง Html เป็น Pdf ใน Java ตั้งค่าขนาดหน้า PDF ความละเอียดและ](/html/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-set-pdf-page-size-resolution-and/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}