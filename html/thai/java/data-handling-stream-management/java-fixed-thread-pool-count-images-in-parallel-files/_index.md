---
category: general
date: 2026-02-10
description: เรียนรู้วิธีใช้ java fixed thread pool เพื่อคำนวณจำนวนรูปภาพในไฟล์ HTML,
  รันงานพร้อมกันด้วย java, และปิด executor service อย่างถูกต้อง.
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: th
og_description: เชี่ยวชาญการใช้ Fixed Thread Pool ของ Java เพื่อการนับภาพ, ประมวลผลไฟล์แบบขนาน,
  และปิด Executor Service อย่างปลอดภัย.
og_title: 'java fixed thread pool: นับจำนวนรูปภาพในไฟล์แบบขนาน'
tags:
- Java
- Concurrency
- Aspose.HTML
title: 'java fixed thread pool: นับจำนวนรูปภาพในไฟล์แบบขนาน'
url: /th/java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – คู่มือการนับรูปภาพแบบขนาน

เคยสงสัยไหมว่าคุณจะใช้ **java fixed thread pool** เพื่อจัดการกับไฟล์ HTML หลายสิบไฟล์และนับรูปภาพได้อย่างรวดเร็วได้อย่างไร? บางทีคุณอาจมองไดเรกทอรีของหน้าเว็บแล้วคิดว่า “ฉันต้องการรู้ว่าแต่ละไฟล์มีแท็ก `<img>` กี่ตัว” แล้วจึงตระหนักว่าการวนลูปแบบ single‑threaded จะใช้เวลานานมาก.

ข่าวดีคือคุณไม่จำเป็นต้องเขียนตัวจัดการเธรดแบบกำหนดเองหรือสู้กับอ็อบเจ็กต์ `Thread` ระดับต่ำ ในคู่มือนี้เราจะสาธิตอย่างชัดเจน **how to count images** ด้วย *java fixed thread pool* , run tasks concurrently java, และปิด **shutdown executor service** อย่างเรียบร้อยเมื่อทำงานเสร็จ.

เราจะครอบคลุมทุกอย่างตั้งแต่การตั้งค่า pool, การเตรียมรายการไฟล์, การส่งงานแบบขนาน, การจัดการกรณีขอบ, จนถึงการตรวจสอบผลลัพธ์. เมื่อเสร็จคุณจะมีโปรแกรมพร้อมรันที่แสดง **java parallel file processing** อย่างสะอาดและดูแลได้ง่าย.

## ข้อกำหนดเบื้องต้น

- Java 17 หรือใหม่กว่า (โค้ดใช้คีย์เวิร์ด `var` เพื่อความกระชับ, แต่คุณสามารถลดเวอร์ชันลงได้หากต้องการ).
- Aspose.HTML for Java บน classpath ของคุณ – คุณสามารถดาวน์โหลดได้จาก Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- ไฟล์ HTML จำนวนไม่กี่ไฟล์ที่คุณต้องการวิเคราะห์ (คู่มือสมมติว่าไฟล์อยู่ใน `YOUR_DIRECTORY/`).
- IDE หรือเครื่องมือสร้างที่คุณถนัด – IntelliJ IDEA, VS Code, หรือ `javac` ธรรมดาก็ใช้ได้ดี.

เท่านี้เอง ไม่ต้องเซิร์ฟเวอร์เพิ่มเติม ไม่ต้อง Docker เพียงแค่ Java ธรรมดาและไลบรารีของบุคคลที่สามขนาดเล็ก.

## ขั้นตอนที่ 1: สร้าง java fixed thread pool

*java fixed thread pool* ให้ชุดเธรดทำงานที่มีขอบเขตซึ่งจะนำกลับมาใช้ใหม่สำหรับแต่ละงานที่ส่งเข้าไป. สิ่งนี้ช่วยป้องกันค่าใช้จ่ายจากการสร้างเธรดใหม่ตลอดเวลาและจำกัดระดับความขนาน, ซึ่งสำคัญเมื่อคุณอ่านไฟล์จากดิสก์.

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**ทำไมถึง 4?** หากคุณมีแล็ปท็อป quad‑core, เธรดสี่ตัวจะทำให้แต่ละคอร์ทำงานเต็มโดยไม่เกิน. บนเซิร์ฟเวอร์ที่มีคอร์มากกว่านี้คุณสามารถเพิ่มจำนวนได้, แต่จำไว้ว่าแต่ละเธรดจะเปิดไฟล์แฮนด์เดิล, ดังนั้นจำนวนมากเกินไปอาจทำให้เกินขีดจำกัดของ OS.

## ขั้นตอนที่ 2: รายการไฟล์ HTML ที่คุณต้องการวิเคราะห์

ส่วนต่อไปของ **java parallel file processing** คือการสร้างอาเรย์ (หรือ `List`) ของเส้นทางไฟล์อย่างง่าย. ในโครงการจริงคุณอาจเดินสำรวจไดเรกทอรีแบบเรียกซ้ำ, กรองตามส่วนขยาย, หรืออ่านเส้นทางจากฐานข้อมูล. นี่คือวิธีที่ตรงไปตรงมาที่สุด:

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

หากคุณต้องการจัดการชุดข้อมูลแบบไดนามิก, ให้แทนที่อาเรย์คงที่ด้วยอย่างเช่น:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

โค้ดส่วนนั้นแสดง **java parallel file processing** สำหรับไฟล์จำนวนใดก็ได้โดยไม่ต้องแก้ไขโค้ดส่วนอื่น.

## ขั้นตอนที่ 3: ส่งงานไปยัง **run tasks concurrently java**

ต่อมาคือหัวใจของบทเรียน – เราจะ **run tasks concurrently java** โดยส่งลัมบ์ดาให้แต่ละไฟล์. งานแต่ละงานจะโหลดเอกสาร HTML ด้วย Aspose.HTML, ค้นหาองค์ประกอบ `<img>` ทั้งหมด, และพิมพ์จำนวน.

```java
import com.aspose.html.HTMLDocument;

public static void main(String[] args) throws InterruptedException {
    for (String filePath : htmlFiles) {
        executor.submit(() -> {
            // Load the document – Aspose.HTML does the heavy lifting
            HTMLDocument document = new HTMLDocument(filePath);
            // querySelectorAll returns a NodeList; its length is the image count
            int imageCount = document.querySelectorAll("img").length;
            System.out.println(filePath + " contains " + imageCount + " images.");
        });
    }

    // Step 4 is next – gracefully shut down the pool
    shutdownAndAwaitTermination();
}
```

**ทำไมต้องใช้ลัมบ์ดา?** มันทำให้โค้ดกระชับและหลีกเลี่ยงการสร้างคลาส `Runnable` แยกต่างหาก. ลัมบ์ดาจะจับ `filePath` โดยอัตโนมัติ, ดังนั้นแต่ละงานจะทำงานกับไฟล์ของตนเอง.

### วิธี **count images** อย่างมีประสิทธิภาพ

Aspose.HTML จะพาร์สไฟล์หนึ่งครั้ง, สร้าง DOM, แล้ว `querySelectorAll("img")` ทำงานใน O(n) โดยที่ *n* คือจำนวนโหนด. สำหรับหน้า HTML ส่วนใหญ่นี่ถือว่าไม่มีนัยสำคัญ. หากคุณต้องการวิธีที่เร็วกว่าและทำแบบสตรีมเท่านั้น (เช่นไฟล์ขนาดกิกะไบต์), คุณอาจเปลี่ยนไปใช้ SAX parser, แต่จะทำให้เสียความเรียบง่ายที่เราต้องการ.

## ขั้นตอนที่ 4: ปิด **shutdown executor service** อย่างถูกต้อง

อย่าลืมปิด pool, มิฉะนั้น JVM ของคุณจะทำงานต่อไปตลอด. รูปแบบด้านล่างเป็นวิธีที่แนะนำเพื่อ **shutdown executor service** ขณะรอให้ทุกงานเสร็จสิ้น:

```java
private static void shutdownAndAwaitTermination() {
    executor.shutdown(); // Disable new tasks from being submitted
    try {
        // Wait a while for existing tasks to terminate
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            executor.shutdownNow(); // Cancel currently executing tasks
            // Wait a second for tasks to respond to being cancelled
            if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                System.err.println("Pool did not terminate");
        }
    } catch (InterruptedException ie) {
        // (Re-)Cancel if current thread also interrupted
        executor.shutdownNow();
        // Preserve interrupt status
        Thread.currentThread().interrupt();
    }
}
```

**ถ้างานหนึ่งค้าง?** การเรียก `shutdownNow()` จะพยายามขัดจังหวะเธรดที่กำลังทำงาน. หากตรรกะการนับรูปภาพของคุณเคารพการขัดจังหวะ (ซึ่ง Aspose.HTML ไม่บล็อก I/O), pool จะหยุดทำงานอย่างสะอาด. รูปแบบนี้เป็นมาตรฐานทองสำหรับการใช้ **java fixed thread pool** ใด ๆ.

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์

รันโปรแกรมจาก IDE ของคุณหรือผ่านบรรทัดคำสั่ง:

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

ผลลัพธ์ทั่วไปจะเป็นเช่นนี้:

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

หากคุณเห็นจำนวนที่พิมพ์ออกมาในลำดับใดก็ได้, นั่นเป็นปกติ – เธรดเสร็จในเวลาที่ต่างกัน. สิ่งสำคัญคือทุกไฟล์ถูกนับและโปรแกรมออกอย่างสะอาดหลังจากขั้นตอน shutdown.

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelImageCounter {
    // 1️⃣ Fixed thread pool – change size based on your hardware
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);

    public static void main(String[] args) throws InterruptedException {
        // 2️⃣ List of HTML files – replace with your own directory
        String[] htmlFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // 3️⃣ Submit a counting task for each file
        for (String filePath : htmlFiles) {
            executor.submit(() -> {
                HTMLDocument document = new HTMLDocument(filePath);
                int imageCount = document.querySelectorAll("img").length;
                System.out.println(filePath + " contains " + imageCount + " images.");
            });
        }

        // 4️⃣ Gracefully shut down the pool
        shutdownAndAwaitTermination();
    }

    // 5️⃣ Helper method to cleanly stop the executor
    private static void shutdownAndAwaitTermination() {
        executor.shutdown(); // Disable new tasks
        try {
            if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
                executor.shutdownNow(); // Cancel currently executing tasks
                if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                    System.err.println("Pool did not terminate");
            }
        } catch (InterruptedException ie) {
            executor.shutdownNow();
            Thread.currentThread().interrupt();
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันสคริปต์จะพิมพ์เส้นทางไฟล์แต่ละไฟล์ตามด้วยจำนวนแท็ก `<img>` ที่มี, แล้ว JVM จะออก. ไม่มีเธรดค้าง, ไม่มีการรั่วของหน่วยความจำ.

## ข้อผิดพลาดทั่วไป & เคล็ดลับมืออาชีพ

- **Pitfall:** การใช้ `newCachedThreadPool()` แทน *fixed* pool. มันสร้างเธรดไม่จำกัดจำนวน, ซึ่งอาจทำให้ไฟล์ดีสคริปเตอร์หมดเมื่อประมวลผลจำนวนมาก. ควรใช้ `newFixedThreadPool`.
- **Pro tip:** หากไฟล์ HTML ของคุณมีขนาดใหญ่, พิจารณาเพิ่ม heap (`-Xmx2g`) หรือเปลี่ยนไปใช้ streaming parser. สำหรับหน้าเว็บการตลาดส่วนใหญ่ heap ค่าเริ่มต้นก็พอ.
- **Pitfall:** ลืมเรียก `shutdown()` – แอปของคุณจะค้างหลังจากพิมพ์ผลลัพธ์. วิธี `shutdownAndAwaitTermination` ด้านบนจัดการอย่างมั่นคง.
- **Pro tip:** บันทึกเวลาเริ่มและสิ้นสุดของแต่ละงานหากต้องการเมตริกประสิทธิภาพ. ใช้ `System.nanoTime()` ก่อนและหลังการสร้าง `HTMLDocument` เพื่อบอกระยะเวลาการพาร์ส.
- **Pitfall:** กำหนดจำนวนเธรดแบบคงที่. ใช้ `Runtime.getRuntime().availableProcessors()` เพื่อเลือกค่าเริ่มต้นที่เหมาะสม:

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## หัวข้อที่เกี่ยวข้องที่คุณอาจสนใจต่อไป

- **run tasks concurrently java** ด้วย `CompletableFuture` เพื่อสร้าง pipeline ที่แสดงออกได้มากขึ้น.
- การบันทึกจำนวนรูปภาพลงฐานข้อมูลเพื่อใช้ในแดชบอร์ดวิเคราะห์.
- การใช้ **java parallel file processing** ร่วมกับ API `java.nio.file.Files.walk` พร้อมสตรีม.
- การสร้าง `ThreadFactory` แบบกำหนดเองเพื่อให้เธรดมีชื่อที่มีความหมาย (ช่วยการดีบัก).

## สรุป

เราเพิ่งผ่านตัวอย่างครบวงจรที่แสดงให้เห็นว่า **java fixed thread pool** สามารถนำไปใช้เพื่อ **how to count images** ในหลายไฟล์ HTML, พร้อมแสดงวิธีที่ถูกต้องในการ **shutdown executor service**. รูปแบบนี้ขยายได้ดี—เปลี่ยนอาเรย์ไฟล์เป็นรายการไดนามิก, เพิ่มขนาด pool, แล้วคุณจะได้โซลูชันที่มั่นคงสำหรับงาน **java parallel file processing** ใด ๆ.

ลองใช้งาน, ปรับจำนวนเธรด, และอาจเพิ่มการส่งออกผลลัพธ์เป็น CSV. ไม่มีขีดจำกัดเมื่อคุณผสานพื้นฐานการทำงานพร้อมกันที่แข็งแกร่งกับไลบรารีที่สะดวกเช่น Aspose.HTML. Happy coding!

![java fixed thread pool diagram](image.png){alt="แผนภาพ java fixed thread pool"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}