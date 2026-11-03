---
category: general
date: 2026-02-21
description: วิธีใช้ ExecutorService เพื่อแปลง HTML เป็น PNG อย่างรวดเร็ว เรียนรู้การแปลงไฟล์
  HTML เป็นชุดด้วยงานขนานใน Java
draft: false
keywords:
- how to use executorservice
- convert html to png
- how to run parallel tasks
- how to convert html to png
- batch convert html files
language: th
og_description: วิธีใช้ ExecutorService เพื่อแปลงไฟล์ HTML เป็น PNG เป็นชุด ขั้นตอนโดยละเอียดพร้อมตัวอย่าง
  Java ครบถ้วน
og_title: วิธีใช้ ExecutorService สำหรับการแปลง HTML เป็น PNG แบบขนาน
tags:
- Java
- concurrency
- Aspose.HTML
- image‑conversion
title: วิธีใช้ ExecutorService สำหรับการแปลง HTML เป็น PNG แบบขนานเป็นชุด
url: /th/java/conversion-html-to-various-image-formats/how-to-use-executorservice-for-parallel-html-to-png-batch-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ ExecutorService สำหรับการแปลง HTML‑to‑PNG แบบแบตช์แบบขนาน

เคยสงสัย **วิธีใช้ ExecutorService** เมื่อคุณมีโฟลเดอร์เต็มไปด้วยหน้า HTML ที่ต้องแปลงเป็นภาพ PNG หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อตัว pipeline การรายงานเว็บของพวกเขาติดอยู่ในลูปการแปลงแบบสิงเกิล‑เธรด  

ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ Java และ Aspose.HTML `Converter` ที่ทรงพลัง คุณสามารถสร้างพูลของเธรดทำงาน, ส่งไฟล์ HTML แต่ละไฟล์ให้กับคอนเวอร์เตอร์, และดูภาพที่สร้างขึ้นแบบขนาน ในบทแนะนำนี้เราจะพูดถึงพื้นฐานของ **convert html to png**, แสดงวิธี **run parallel tasks**, และให้สคริปต์ **batch convert html files** ที่พร้อมรัน

## ข้อกำหนดเบื้องต้น

- Java 17 หรือใหม่กว่า (โค้ดใช้ API `java.nio.file` สมัยใหม่)  
- ไลบรารี Aspose.HTML for Java อยู่ใน classpath ของคุณ สามารถดึงจาก Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

- โฟลเดอร์ที่มีไฟล์ `.html` ต้นฉบับและโฟลเดอร์เปล่าสำหรับผลลัพธ์  
- RAM ปริมาณพอสมควร—การแปลงแต่ละครั้งทำงานในเธรดของตนเอง ดังนั้นขนาดพูลควรตรงกับจำนวนคอร์ CPU ที่คุณมี

> **เคล็ดลับ:** หากคุณใช้เครื่องที่มี hyper‑threading, `Runtime.getRuntime().availableProcessors()` มักจะคืนค่าจำนวนคอร์ที่เหมาะสมที่สุด

## ขั้นตอนที่ 1 – กำหนดเส้นทางอินพุตและเอาต์พุต

ก่อนอื่นเราต้องบอก Java ว่าไฟล์ HTML อยู่ที่ไหนและ PNG ควรบันทึกไว้ที่ไหน การใช้วัตถุ `Path` ทำให้โค้ดเป็นแบบ platform‑independent

```java
import java.nio.file.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Input folder containing .html files
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        // Output folder for the generated .png files
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");

        // Ensure the output folder exists
        Files.createDirectories(outputDir);
```

> **ทำไมถึงสำคัญ:** การสร้างโฟลเดอร์เอาต์พุตล่วงหน้าช่วยป้องกัน `FileNotFoundException` เมื่อเธรดทำงานตัวแรกพยายามเขียนไฟล์

## ขั้นตอนที่ 2 – สร้าง Fixed‑Size Thread Pool

หัวใจของ **วิธีใช้ ExecutorService** อยู่ที่การสร้างพูลที่สอดคล้องกับฮาร์ดแวร์ของคุณ พูล *fixed* จะรับประกันว่าเราจะไม่สร้างเธรดมากเกินกว่าที่สามารถรันได้จริง

```java
        // Create a thread pool sized to the number of available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());
```

> **คำอธิบาย:** `ExecutorService` จัดการการทำงานของเธรดระดับต่ำให้คุณโดยอัตโนมัติ การใช้ `newFixedThreadPool` ทำให้ JVM สามารถนำเธรดกลับมาใช้ใหม่ได้ ซึ่งลดภาระการสร้างและทำลายเธรดบ่อยครั้ง

## ขั้นตอนที่ 3 – ส่งงานแปลงหนึ่งงานต่อไฟล์ HTML

ต่อไปเราจะเดินผ่านโฟลเดอร์อินพุต, เลือกไฟล์ `*.html` ทุกไฟล์, และส่งให้พูลแต่ละงานเป็น lambda เล็ก ๆ ที่เรียก `Converter.convert`

```java
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        // Build the output filename by swapping .html for .png
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();

                        // Perform the actual conversion
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }
```

### สิ่งที่เกิดขึ้นเบื้องหลังคืออะไร?

1. **DirectoryStream** อ่านชื่อไฟล์แบบ lazy ทำให้การใช้หน่วยความจำต่ำแม้จะมีไฟล์หลายพันไฟล์  
2. Lambda จับตัวแปร `htmlFile` และ `outputDir`—ไม่ต้องสร้างคลาส `Runnable` แยกต่างหาก  
3. `Converter.convert` เป็นการเรียกแบบบล็อกที่อ่าน HTML, เรนเดอร์, แล้วเขียน PNG เนื่องจากแต่ละการเรียกทำงานในเธรดของตนเอง ไฟล์หลายไฟล์จึงถูกประมวลผลพร้อมกัน—พฤติกรรมที่คุณคาดหวังเมื่อ **run parallel tasks**

## ขั้นตอนที่ 4 – ปิดพูลอย่างสุภาพ

หลังจากงานทั้งหมดถูกคิวแล้ว เราบอกพูลให้หยุดรับงานใหม่และรอให้ทุกอย่างเสร็จ หากมีบางอย่างค้าง, timeout จะยกเลิกหลังจากหนึ่งชั่วโมง ซึ่งถือว่าอุ่นใจสำหรับงานแบตช์ส่วนใหญ่

```java
        // No more tasks will be submitted
        pool.shutdown();

        // Wait up to 1 hour for all conversions to complete
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }

        System.out.println("All conversions completed.");
    }
}
```

> **กรณีขอบ:** หากคุณมีไฟล์ HTML ขนาดใหญ่มาก, คุณอาจต้องเพิ่ม timeout หรือเฝ้าติดตามการใช้หน่วยความจำ การเพิ่ม `pool.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy())` จะทำให้เธรดเรียกใช้งานทำงานส่วนที่เหลือ, ป้องกัน `RejectedExecutionException`

## ตัวอย่างเต็มพร้อมรัน

ด้านล่างเป็นโปรแกรมทั้งหมดที่สามารถคัดลอก‑วางลงในไฟล์ `ParallelBatchConversion.java` เพียงไฟล์เดียว

```java
import com.aspose.html.converters.Converter;
import java.nio.file.*;
import java.util.concurrent.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Step 1: Define source and destination folders
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");
        Files.createDirectories(outputDir);

        // Step 2: Create a thread pool sized to the available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());

        // Step 3: Submit a conversion task for each HTML file found
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }

        // Step 4: Shut down the pool and wait for all conversions to finish
        pool.shutdown();
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }
        System.out.println("All conversions completed.");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะพิมพ์บรรทัดหนึ่งสำหรับการแปลงที่สำเร็จแต่ละครั้ง:

```
Converted: report1.html
Converted: dashboard.html
Converted: summary.html
All conversions completed.
```

หากไฟล์ใดล้มเหลว, คุณจะเห็นบรรทัดแสดงข้อผิดพลาดพร้อมข้อความ exception ทำให้การดีบักง่ายขึ้น

## วิธีขยายรูปแบบนี้

- **รูปแบบภาพอื่น:** เปลี่ยนนามสกุลจาก `.png` เป็น `.jpg` หรือ `.bmp` แล้วปรับตัวเลือกการแปลงของ Aspose ให้สอดคล้อง  
- **จำนวนเธรดแบบไดนามิก:** สำหรับงานที่ผูกกับ I/O คุณอาจเพิ่มขนาดพูล (`availableProcessors() * 2`)  
- **การติดตามความคืบหน้า:** แทนที่ `System.out.println` ด้วยไลบรารี progress bar ที่ thread‑safe เช่น `jline` หรือบันทึกลงไฟล์  
- **การจัดการข้อผิดพลาด:** เก็บเส้นทางที่ล้มเหลวไว้ใน `List<Path>` แล้วลองใหม่หลังจากลูปหลักเสร็จสิ้น

## คำถามที่พบบ่อย

**ถาม: โค้ดนี้ทำงานบน Windows และ Linux ได้หรือไม่?**  
ตอบ: ใช่. `java.nio.file` แยกการทำงานของระบบไฟล์พื้นฐานออก, ดังนั้นโค้ดเดียวกันทำงานได้โดยไม่ต้องเปลี่ยนแปลงบน OS ใด ๆ ที่รองรับ Java

**ถาม: ถ้ามีไฟล์ HTML มากกว่า 10 000 ไฟล์จะทำอย่างไร?**  
ตอบ: ตัว iterator ของ `DirectoryStream` อ่านรายการแบบ lazy ทำให้หน่วยความจำคงที่ เพียงแค่ตรวจสอบให้ดิสก์มีพื้นที่ว่างเพียงพอสำหรับผลลัพธ์ PNG

**ถาม: สามารถจำกัดหน่วยความจำที่แต่ละการแปลงใช้ได้หรือไม่?**  
ตอบ: Aspose.HTML ให้คุณกำหนดค่า engine การเรนเดอร์ผ่าน `HtmlLoadOptions` และ `ImageSaveOptions` คุณสามารถตั้งขนาด bitmap สูงสุดหรือเปิดการเรนเดอร์คุณภาพต่ำเพื่อควบคุมการใช้ RAM

## สรุป

เราได้อธิบาย **วิธีใช้ ExecutorService** เพื่อ **batch convert html files** เป็นภาพ PNG, แสดงเหตุผลที่พูลขนาดคงที่เป็นจุดที่เหมาะสมสำหรับการเรนเดอร์ที่ใช้ CPU, และให้โปรแกรม Java เต็มรูปแบบที่คัดลอก‑วางได้ ด้วยการทำตามขั้นตอนนี้ คุณจะเปลี่ยนลูปสิงเกิล‑เธรดที่ช้าให้เป็น pipeline ที่เร็วและขยายได้, สามารถจัดการไฟล์หลายพันไฟล์ด้วยคำสั่งเดียว

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองเปลี่ยน `Converter.convert` เป็นการส่งออก PDF ของ Aspose เพื่อ **convert html to pdf**, หรือผสานตรรกะนี้เข้าไปใน microservice Spring Boot ที่รับคำขออัปโหลด‑และ‑แปลง. แนวคิดหลัก—การใช้ `ExecutorService` เพื่อ **run parallel tasks**—ยังคงเหมือนเดิมและจะเป็นประโยชน์ในหลายสถานการณ์การประมวลผลแบบแบตช์

ขอให้เขียนโค้ดอย่างสนุกสนาน, และขอให้เธรดของคุณทำงานต่อเนื่องไม่มีที่สิ้นสุด!

![how to use executorservice diagram](placeholder.png "Diagram illustrating the thread pool workflow for parallel HTML‑to‑PNG conversion")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}