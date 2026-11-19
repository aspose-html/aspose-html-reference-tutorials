---
category: general
date: 2026-06-07
description: แปลง HTML เป็น PDF ด้วย ExecutorService ของ Java. เรียนรู้วิธีแปลงไฟล์
  HTML เป็นชุด, บันทึกเอกสาร HTML เป็น PDF, และปิด ExecutorService อย่างราบรื่น.
draft: false
keywords:
- convert html to pdf
- save html document as pdf
- shutdown executorservice gracefully
- batch convert html to pdf
language: th
og_description: แปลง HTML เป็น PDF ด้วย ExecutorService ของ Java. ควบคุมการแปลงแบบกลุ่ม,
  บันทึกเอกสาร HTML เป็น PDF, และปิด ExecutorService อย่างราบรื่น.
og_title: แปลง HTML เป็น PDF ด้วย Java – คู่มือการทำงานแบบแบตช์ขนาน
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  headline: Convert HTML to PDF with Java – Parallel Batch Guide
  type: TechArticle
- description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  name: Convert HTML to PDF with Java – Parallel Batch Guide
  steps:
  - name: The HTML file is read into a string.
    text: The HTML file is read into a string.
  - name: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
    text: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
  - name: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
    text: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
  type: HowTo
tags:
- Java
- Concurrency
- PDF Generation
title: แปลง HTML เป็น PDF ด้วย Java – คู่มือการทำงานแบบแบตช์ขนาน
url: /th/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-parallel-batch-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลง HTML เป็น PDF ด้วย Java – คู่มือการประมวลผลแบบขนาน (Batch)

เคยต้อง **convert HTML to PDF** แต่รู้สึกติดขัดกับการจัดการไฟล์หลายสิบไฟล์หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาจำนวนมากเจออุปสรรคนี้เมื่อต้องสร้างตัวสร้างรายงานหรือผู้ส่งออกใบแจ้งหนี้ ข่าวดีคือ ด้วยเพียงไม่กี่บรรทัดของ Java และ thread pool ที่ฉลาด คุณสามารถ **batch convert HTML to PDF** ได้อย่างรวดเร็ว, **save HTML document as PDF**, และแม้กระทั่ง **shutdown ExecutorService gracefully** เมื่อทำงานเสร็จ

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่พร้อม‑run อย่างครบถ้วน คุณจะได้เห็นว่าทำไม fixed‑size thread pool จึงเป็นจุดที่ลงตัวสำหรับการแปลงแบบขนาน, โค้ดการแปลงเป็นอย่างไร, และขั้นตอนที่แน่นอนในการปิด executor อย่างสะอาด สุดท้ายคุณจะได้โปรแกรมที่สามารถนำไปใส่ในโปรเจกต์ใดก็ได้—ไม่มีส่วนที่หายไป, ไม่มีลิงก์ “ดูเอกสาร” ที่คลุมเครือ

---

## สิ่งที่คุณจะสร้าง

- แอปคอนโซล Java ที่อ่านรายการไฟล์ HTML ในเครื่อง  
- แต่ละไฟล์จะถูกส่งต่อให้ worker thread เพื่อสร้างเวอร์ชัน PDF  
- แอปใช้ **ExecutorService** เพื่อรันการแปลงแบบขนาน  
- เมื่อทุกงานถูกคิวแล้ว pool จะ **shutdown gracefully**, เพื่อให้แน่ใจว่าไม่มี thread ใดค้างอยู่

**Prerequisites**  
- Java 17 (หรือ JDK รุ่นใหม่ใดก็ได้)  
- ไลบรารี PDF ที่สามารถเรนเดอร์ HTML ได้ เช่น **OpenHTMLtoPDF**, **iText**, หรือ **Flying Saucer** ในโค้ดเราจะอ้างอิงคลาส placeholder `HTMLDocument`; เปลี่ยนเป็น API ของไลบรารีที่คุณใช้  
- ความรู้พื้นฐานเกี่ยวกับการทำงานพร้อมกันของ Java (ไม่มีอะไรซับซ้อน)

---

![Diagram showing batch conversion of HTML files to PDF using ExecutorService](batch-convert-diagram.png "Convert HTML to PDF in parallel with ExecutorService")

*Alt text: Diagram illustrating how to convert HTML to PDF using a thread pool for batch processing.*

---

## Convert HTML to PDF in Parallel (Batch Convert HTML to PDF)

เมื่อคุณมีไฟล์ HTML หลายสิบหรือแม้แต่หลายพันไฟล์ การแปลงทีละไฟล์บน main thread จะเป็นคอขวด Fixed‑size thread pool ช่วยให้ JVM ใช้ worker threads จำนวนที่กำหนดซ้ำได้ ทำให้การใช้ CPU สูงโดยไม่ทำให้ระบบล้น

```java
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * Simple demo that batch converts HTML files to PDF using a fixed thread pool.
 * Replace HTMLDocument with the actual class from your chosen PDF library.
 */
public class HtmlToPdfBatch {

    public static void main(String[] args) {
        // 1️⃣ Prepare a list of HTML files to convert
        List<String> htmlPaths = List.of(
            "src/main/resources/page1.html",
            "src/main/resources/page2.html",
            "src/main/resources/page3.html"
        );

        // 2️⃣ Create a fixed‑size thread pool – 4 workers is a good starting point
        ExecutorService pool = Executors.newFixedThreadPool(4);

        // 3️⃣ Submit a conversion task for each HTML file
        for (String htmlPath : htmlPaths) {
            pool.submit(() -> convertAndSave(htmlPath));
        }

        // 4️⃣ Shutdown ExecutorService gracefully – no new tasks, wait for running ones
        shutdownGracefully(pool);
    }

    /**
     * Core conversion logic – this is where we **save HTML document as PDF**.
     */
    private static void convertAndSave(String htmlPath) {
        try {
            // Imagine HTMLDocument is from OpenHTMLtoPDF, iText, etc.
            HTMLDocument doc = new HTMLDocument(htmlPath);
            String pdfPath = htmlPath.replace(".html", ".pdf");
            doc.save(pdfPath);
            System.out.println("✅ Converted: " + htmlPath + " → " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Failed to convert " + htmlPath + ": " + e.getMessage());
        }
    }

    /**
     * Helper that **shutdowns ExecutorService gracefully**.
     */
    private static void shutdownGracefully(ExecutorService executor) {
        executor.shutdown(); // stop accepting new tasks
        try {
            // Wait a maximum of 60 seconds for existing tasks to finish
            if (!executor.awaitTermination(60, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("⚠️ Pool didn’t terminate in time – forcing shutdown");
                executor.shutdownNow(); // cancel currently executing tasks
            } else {
                System.out.println("🛑 All tasks completed – executor shut down cleanly.");
            }
        } catch (InterruptedException ie) {
            // Preserve interrupt status & force shutdown
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

- **Parallelism**: การเรียก `submit` แต่ละครั้งจะส่งการแปลงให้ worker thread ทำงาน ดังนั้นไฟล์สี่ไฟล์สามารถประมวลผลพร้อมกันบนเครื่อง quad‑core  
- **Isolation**: เมธอด `convertAndSave` มีตรรกะทั้งหมดที่จำเป็นสำหรับ **save HTML document as PDF**, ทำให้การสลับไลบรารีภายหลังทำได้ง่าย  
- **Graceful termination**: การเรียก `shutdown()` ก่อนบอก pool ว่า “ไม่มีงานใหม่แล้ว, โปรดทำงานที่เหลือให้เสร็จ”. ลูป `awaitTermination` ให้โอกาส thread สรุปงาน, และหากยังคงค้างอยู่เราจึงใช้ `shutdownNow()`. รูปแบบนี้เป็นวิธีที่แนะนำสำหรับ **shutdown ExecutorService gracefully**

---

## Save HTML Document as PDF – Core Conversion Logic

หัวใจของกระบวนการ **convert HTML to PDF** ใด ๆ คือไลบรารีการแปลง ตัวอย่างนี้ใช้ `HTMLDocument` จำลอง, ต่อไปนี้คือตัวอย่างสั้น ๆ ว่าจะทำอย่างไรกับ **OpenHTMLtoPDF**:

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

public class HTMLDocument {
    private final String htmlPath;

    public HTMLDocument(String htmlPath) {
        this.htmlPath = htmlPath;
    }

    public void save(String pdfPath) throws IOException {
        try (OutputStream os = new FileOutputStream(pdfPath);
             InputStream is = new FileInputStream(htmlPath)) {

            PdfRendererBuilder builder = new PdfRendererBuilder();
            builder.withHtmlContent(new String(is.readAllBytes()), null);
            builder.toStream(os);
            builder.run();
        }
    }
}
```

**กำลังเกิดอะไรขึ้น?**  
1. อ่านไฟล์ HTML เข้าเป็นสตริง  
2. `PdfRendererBuilder` วิเคราะห์ markup, ประยุกต์ CSS, และสตรีมผลลัพธ์ไปยังไฟล์ PDF  
3. `IOException` ใด ๆ จะลอยขึ้นไปยัง `convertAndSave`, ที่ซึ่งเราจะบันทึกข้อความสำเร็จหรือความล้มเหลว

คุณสามารถแทนที่สแนปนี้ด้วย `HtmlConverter.convertToPdf` ของ iText หรือ `ITextRenderer` ของ Flying Saucer ได้เลย โค้ดส่วน thread‑pool จะคงเดิม ซึ่งเป็นเหตุผลที่เราตั้งหัวข้อ **save HTML document as PDF** เป็นความกังวลแยกส่วน

---

## Shutdown ExecutorService Gracefully – Best Practices

ข้อผิดพลาดทั่วไปคือการเรียก `shutdownNow()` ทันทีหลังจาก submit งาน ซึ่งจะขัดจังหวะ thread อย่างฉับพลัน ทำให้ไฟล์ PDF ครึ่งหนึ่งอาจค้างอยู่บนดิสก์ รูปแบบที่เราใช้ — `shutdown()` → `awaitTermination()` → (optional) `shutdownNow()` — รับประกันว่า:

- **No new tasks** จะถูกรับหลังจากคุณคิวงานทั้งหมดแล้ว  
- **Running tasks** จะได้รับโอกาสทำงานให้เสร็จอย่างสะอาด  
- **Blocked threads** จะถูกขัดจังหวะเฉพาะเมื่อเกิน timeout ที่สมเหตุสมผล (ที่นี่ 60 วินาที)

หากคุณคาดว่าจะได้ PDF ขนาดใหญ่หรือใช้ engine เรนเดอร์ช้า, ให้เพิ่ม timeout หรือใช้ `executor.invokeAll(tasks, timeout, unit)` เพื่อควบคุมที่แน่นขึ้น

---

## Full Working Example (All Pieces Together)

ด้านล่างเป็นโปรแกรมทั้งหมดที่คุณสามารถคัดลอก‑วางลงในไฟล์ `HtmlToPdfBatch.java` ไฟล์เดียว เพียงเพิ่ม dependency ของ OpenHTMLtoPDF (หรือไลบรารีที่คุณเลือก) ลงใน `pom.xml` หรือ Gradle build แล้วคุณก็พร้อมใช้งาน



## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ ทุกแหล่งข้อมูลมีโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [วิธีแปลง HTML เป็น PDF ด้วย Java – ใช้ Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [แปลง HTML เป็น PDF ด้วย Java – การตั้งค่าสภาพแวดล้อมใน Aspose.HTML](/html/english/java/configuring-environment/)
- [แปลง HTML เป็น PDF ใน Java – คู่มือขั้นตอนพร้อมการตั้งค่าขนาดหน้า](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}