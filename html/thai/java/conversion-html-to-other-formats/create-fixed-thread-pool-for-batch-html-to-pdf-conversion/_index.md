---
category: general
date: 2026-02-22
description: สร้างกลุ่มเธรดคงที่เพื่อทำการแปลง HTML เป็น PDF เป็นชุดอย่างมีประสิทธิภาพใน
  Java. เรียนรู้ตัวอย่างการใช้กลุ่มเธรดใน Java ที่บันทึก HTML เป็น PDF อย่างรวดเร็ว.
draft: false
keywords:
- create fixed thread pool
- convert html to pdf
- batch html to pdf
- thread pool java example
- save html as pdf
language: th
og_description: สร้าง Fixed Thread Pool เพื่อทำการแปลง HTML เป็น PDF แบบชุด งานนี้จะแนะนำคุณผ่านตัวอย่าง
  Thread Pool ใน Java ที่ช่วยบันทึก HTML เป็น PDF อย่างมีประสิทธิภาพ
og_title: สร้าง Fixed Thread Pool สำหรับการแปลง HTML เป็น PDF แบบกลุ่ม
tags:
- Java
- Concurrency
- PDF Generation
title: สร้าง Fixed Thread Pool สำหรับการแปลง HTML เป็น PDF แบบชุด
url: /th/java/conversion-html-to-other-formats/create-fixed-thread-pool-for-batch-html-to-pdf-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Fixed Thread Pool สำหรับการแปลง HTML เป็น PDF แบบเป็นชุด

เคยสงสัยไหมว่า **create fixed thread pool** ที่เปลี่ยนกองไฟล์ HTML เป็น PDF โดยไม่ทำให้ CPU ของคุณอัดแน่น? คุณไม่ได้เป็นคนเดียว เมื่อคุณมีหลายสิบหรือแม้แต่หลายร้อยหน้าให้ประมวลผล การรันทีละหน้าเป็นเรื่องน่าเบื่อ แต่การเปิดใช้งาน thread pool ที่ไม่มีขีดจำกัดอาจทำให้หน่วยความจำหมดอย่างรวดเร็ว  

ในบทแนะนำนี้ เราจะแก้ปัญหานั้นโดยแสดง **thread pool Java example** ที่ **batch HTML to PDF**, บันทึกผลลัพธ์แต่ละไฟล์ และปิดการทำงานอย่างเรียบร้อย เมื่อจบคุณจะสามารถ **convert HTML to PDF** แบบขนานได้ และคุณจะเข้าใจว่าทำไม fixed thread pool จึงเป็นจุดที่เหมาะสมสำหรับงานแบบ batch ส่วนใหญ่

## สิ่งที่คุณจะได้เรียนรู้

- โปรแกรม Java ที่สมบูรณ์และสามารถรันได้ซึ่งสร้าง fixed thread pool
- คำอธิบายทีละขั้นตอนของแต่ละบรรทัด เพื่อให้คุณรู้ **why** เราทำสิ่งที่ทำ
- คำแนะนำในการเลือกไลบรารี PDF (เพื่อให้คุณสามารถ **save HTML as PDF** ได้โดยไม่ต้องค้นหาโค้ดสแนปช็อต)
- เคล็ดลับในการจัดการข้อผิดพลาด ปรับขนาด pool และขยายโซลูชันสำหรับ batch ขนาดใหญ่ขึ้น

**Prerequisites** – ติดตั้ง Java 8+ แล้ว, มี IDE เบื้องต้น (IntelliJ, Eclipse หรือ VS Code) และไลบรารีการแปลง PDF อยู่ใน classpath ของคุณ (เราจะใช้ *OpenHTMLtoPDF* ในตัวอย่าง) ไม่จำเป็นต้องใช้เฟรมเวิร์กอื่น

---

## สร้าง Fixed Thread Pool – ทำไมถึงสำคัญ

เมื่อคุณ **create fixed thread pool** คุณบอก JVM ว่าจะอนุญาตให้มี worker threads กี่ตัวทำงานพร้อมกันเท่านั้น การทำเช่นนี้ป้องกันการเกิด storm ของการสร้าง thread, ทำให้การใช้หน่วยความจำคาดเดาได้, และทำให้ OS สามารถจัดตารางงานได้อย่างมีประสิทธิภาพ  

ลองนึกภาพเหมือนแถวชำระเงินในซูเปอร์มาร์เก็ต: คุณเปิดจำนวนแถวที่กำหนดไว้ล่วงหน้า, ให้ลูกค้าเข้าคิว, และปิดแถวเมื่อไม่มีคิวเหลือ `FixedThreadPool` ทำงานในลักษณะเดียวกัน—งานจะรอคิวของตน, แต่จะไม่มีการสร้าง thread เพิ่มเติมแบบทันที  

```java
// Step 1: Build a fixed‑size thread pool with 4 workers
ExecutorService threadPool = Executors.newFixedThreadPool(4);
```

จำนวน `4` เป็นจุดเริ่มต้นที่ดีสำหรับแล็ปท็อปที่มีคอร์ CPU สี่คอร์; คุณสามารถปรับได้ตามจำนวนคอร์ของ CPU และลักษณะการทำ I/O ของระบบ  

## Batch HTML to PDF: การแปลงแต่ละหน้า

เมื่อ pool มีอยู่แล้ว เราต้องส่งงานที่ **convert HTML to PDF** ให้กับมัน งานแต่ละงานจะ:

1. โหลดเอกสาร HTML จากดิสก์
2. ส่งต่อให้ไลบรารี PDF
3. เขียนไฟล์ PDF ที่ได้กลับไปยังไดเรกทอรีเดียวกัน  

เนื่องจากงานนี้หนักด้าน I/O (การอ่านไฟล์, การเขียน PDF) pool ขนาดเล็กมักทำงานได้ดีกว่า pool ขนาดใหญ่ที่นั่งรอคอยดิสก์โดยไม่มีการทำงาน  

```java
// Step 2: Submit a conversion job for every HTML file you have
for (int i = 0; i < 4; i++) {
    final int pageIndex = i;               // capture loop variable for the lambda
    threadPool.submit(() -> {
        // Load the HTML file
        Path htmlPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".html");
        String html = Files.readString(htmlPath, StandardCharsets.UTF_8);

        // Convert and save as PDF
        Path pdfPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".pdf");
        convertHtmlToPdf(html, pdfPath);
    });
}
```

> **Pro tip:** หากคุณมีมากกว่าสี่หน้า เพียงเพิ่มขอบเขตของลูปหรืออ่านรายการไฟล์แบบไดนามิก—`Files.list(Paths.get("YOUR_DIRECTORY")).filter(p -> p.toString().endsWith(".html"))` ทำให้ง่ายดาย  

## อธิบาย Thread Pool Java Example

มาดู **thread pool Java example** ทีละบรรทัด เพื่อให้คุณไม่เพียงแค่คัดลอกโค้ด แต่เข้าใจการทำงานจริง  

| Line | สิ่งที่ทำ | ทำไมจึงสำคัญ |
|------|-----------|--------------------|
| `ExecutorService threadPool = Executors.newFixedThreadPool(4);` | สร้าง pool ที่มีจำนวน thread อย่างแม่นยำที่สี่ตัว | รับประกันจำนวนการแปลงพร้อมกันที่จำกัด, ป้องกันข้อผิดพลาด out‑of‑memory |
| `for (int i = 0; i < 4; i++) { … }` | วนลูปผ่านหน้าที่คุณต้องการประมวลผล | ลูปนี้สร้างงาน; คุณสามารถเปลี่ยนขอบเขตคงที่เป็นรายการแบบไดนามิกได้ |
| `final int pageIndex = i;` | เก็บค่าดัชนีของลูปเพื่อใช้ภายใน lambda | หากไม่มี `final` (หรือ effectively final) lambda จะเห็นค่าที่เปลี่ยนแปลง ทำให้ชื่อไฟล์ผิดพลาด |
| `threadPool.submit(() -> { … });` | ส่ง `Runnable` ไปยัง pool เพื่อทำงานแบบอะซิงโครนัส | pool จะจัดตาราง runnable บน worker thread ที่ว่าง, ปล่อยให้ main thread สามารถคิวงานต่อได้ |
| `Files.readString(htmlPath, …);` | อ่านไฟล์ HTML เป็น `String` | จำเป็นเนื่องจากไลบรารี PDF ส่วนใหญ่รับ HTML เป็นสตริงหรือสตรีม |
| `convertHtmlToPdf(html, pdfPath);` | เรียกเมธอดช่วยเหลือที่ทำการแปลงจริง | ทำให้ lambda สะอาดและแยกโค้ดที่ขึ้นกับไลบรารีออก |

ด้านล่างเป็นเมธอดช่วยเต็มรูปแบบที่ใช้ **OpenHTMLtoPDF**, ไลบรารีขนาดเล็กที่ **save HTML as PDF** ด้วยการเรียกเพียงครั้งเดียว  

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

private static void convertHtmlToPdf(String html, Path outputPdf) throws IOException {
    try (OutputStream os = Files.newOutputStream(outputPdf)) {
        PdfRendererBuilder builder = new PdfRendererBuilder();
        builder.withHtmlContent(html, null);     // base URI is null because we use absolute paths
        builder.toStream(os);
        builder.run();                           // blocks until PDF is written
    } catch (Exception e) {
        // Wrap any checked exception as an unchecked one so the lambda can compile
        throw new RuntimeException("Failed to convert HTML to PDF for " + outputPdf, e);
    }
}
```

> **Why OpenHTMLtoPDF?** เป็น Java แท้, ไม่มีการพึ่งพา native, และสนับสนุน CSS ทำให้ PDF ที่ได้ดูคล้ายหน้าเว็บต้นฉบับ หากคุณชอบ iText หรือ Flying Saucer เพียงเปลี่ยนการทำงานภายใน `convertHtmlToPdf`  

## Save HTML as PDF – การเลือกไลบรารี

คุณอาจถามว่า “ควรใช้ไลบรารีใดในการ **convert HTML to PDF**?” นี่คือการเปรียบเทียบอย่างรวดเร็ว:

| Library | Maven Coordinates | Pros | Cons |
|---------|-------------------|------|------|
| OpenHTMLtoPDF | `com.openhtmltopdf:openhtmltopdf-pdfbox:1.0.10` | Pure Java, รองรับ CSS ดี, น้ำหนักเบา | ฟีเจอร์ PDF ขั้นสูงจำกัด (เช่น การเข้ารหัส) |
| iText 7 + html2pdf | `com.itextpdf:html2pdf:3.0.6` | ฟีเจอร์ครบครัน, มีการสนับสนุนเชิงพาณิชย์ | ต้องมีลิขสิทธิ์แบบชำระเงินสำหรับหลายกรณีการใช้งาน |
| Flying Saucer | `org.xhtmlrenderer:flying-saucer-pdf:9.1.22` | มั่นคง, ทำงานกับ Java เวอร์ชันเก่าได้ | ช้าในเอกสารขนาดใหญ่, รองรับ CSS น้อยกว่า |

เลือกไลบรารีที่ตรงกับความต้องการของโครงการของคุณ สำหรับงาน **batch HTML to PDF** OpenHTMLtoPDF มักเป็นตัวเลือกที่เหมาะสม: เร็ว, เรียบง่าย, และฟรี  

## การปิดอย่างสุภาพและการจัดการข้อผิดพลาด

การปล่อยให้ executor ทำงานต่อไปอาจทำให้ JVM ไม่สามารถออกได้, และข้อยกเว้นที่ไม่ได้จับใน thread อาจยากต่อการสังเกต รูปแบบต่อไปนี้ทำให้การปิดทำงานเป็นระเบียบ:

```java
// Step 5: Initiate an orderly shutdown after all tasks are queued
threadPool.shutdown();                     // No new tasks accepted
try {
    // Wait up to 60 seconds for existing tasks to finish
    if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
        threadPool.shutdownNow();          // Force shutdown if tasks linger
    }
} catch (InterruptedException ex) {
    threadPool.shutdownNow();              // Preserve interrupt status
    Thread.currentThread().interrupt();
}
```

- `shutdown()` บอก pool ให้ทำงานที่กำลังทำให้เสร็จแต่ปฏิเสธงานใหม่
- `awaitTermination` จะบล็อกจนกว่าทุกอย่างจะเสร็จหรือเวลาหมด
- `shutdownNow()` พยายามยกเลิกงานที่กำลังทำ—มีประโยชน์สำหรับการหยุดโดยบังคับ  

หากการแปลงใดล้มเหลว `RuntimeException` ที่เราทำการโยนจะลอยขึ้นไปยัง executor ซึ่งโดยค่าเริ่มต้นจะบันทึกลงคอนโซล ในการใช้งานจริงคุณอาจแนบ `ThreadPoolExecutor` ที่กำหนดเองพร้อมเมธอด `afterExecute` ที่ถูก override เพื่อบันทึกลงไฟล์หรือระบบมอนิเตอร์  

## ตัวอย่างการทำงานเต็มรูปแบบ

เมื่อนำทั้งหมดมารวมกัน นี่คือคลาส Java ที่เป็นอิสระซึ่งคุณสามารถคัดลอก‑วางลงใน `src/main/java/com/example/BatchPdfConverter.java` ตรวจสอบให้แน่ใจว่า dependency ของ OpenHTMLtoPDF อยู่ใน classpath ของคุณ  

```java
package com.example;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;
import java.util.concurrent.*;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;

/**
 * Demonstrates how to create a fixed thread pool to batch HTML to PDF conversion.
 * Adjust POOL_SIZE and DIRECTORY constants to fit your environment.
 */
public class BatchPdfConverter {

    private static final int POOL_SIZE = 4;                     // Number of parallel workers
    private static final Path DIRECTORY = Paths.get("YOUR_DIRECTORY"); // Change to your folder

    public static void main(String[] args) {
        ExecutorService threadPool = Executors.newFixedThreadPool(POOL_SIZE);

        // Discover all *.html files in the target directory
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(DIRECTORY, "*.html")) {
            for (Path htmlPath : stream) {
                threadPool.submit(() -> processFile(htmlPath));
            }
        } catch (IOException e) {
            System.err.println("Failed to list HTML files: " + e.getMessage());
        }

        // Graceful shutdown
        thread

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}