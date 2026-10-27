---
category: general
date: 2026-05-28
description: วิธีใช้ Executor ใน Java กับ Fixed Thread Pool, ดึงข้อความจาก HTML และเร่งความเร็วการประมวลผล
  – ตัวอย่างเต็มของ Thread Pool ใน Java
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: th
og_description: วิธีใช้ executor ใน Java กับ fixed thread pool. เรียนรู้ตัวอย่าง java
  thread pool อย่างครบถ้วนที่ดึงข้อความจากไฟล์ HTML อย่างมีประสิทธิภาพ.
og_title: วิธีใช้ Executor ใน Java – คู่มือการใช้ Fixed Thread Pool
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: วิธีใช้ Executor ใน Java – คู่มือพูลเธรดคงที่
url: /th/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ Executor ใน Java – คู่มือ Fixed Thread Pool

เคยสงสัย **วิธีใช้ executor** เพื่อรันงานหลาย ๆ งานพร้อมกันโดยไม่ทำให้หน่วยความจำพุ่งไหม? คุณไม่ได้เป็นคนเดียว ในหลายแอปพลิเคชันจริง ๆ คุณอาจต้องสแกนโฟลเดอร์ของไฟล์ HTML ดึงข้อความในส่วน body ออกมาและทำให้เร็วที่สุด — นี่คือสถานการณ์ที่บทเรียนนี้แก้ไข

เราจะพาคุณผ่านการทำงานของ **fixed thread pool java** ที่สกัดข้อความจาก HTML, พิมพ์จำนวนอักขระของแต่ละไฟล์, และปิดการทำงานอย่างเรียบร้อย เมื่อจบคุณจะได้ **java thread pool example** ที่สามารถนำไปใช้ในโปรเจกต์ใดก็ได้ พร้อมเคล็ดลับการปรับขนาด pool และการจัดการกรณีขอบ

> **สิ่งที่คุณต้องมี**  
> * Java 17 (หรือ JDK รุ่นใหม่ใดก็ได้)  
> * ไลบรารีการแยกวิเคราะห์ HTML เล็ก ๆ – เราจะใช้ *jsoup* เพราะทดสอบแล้วและไม่มีการตั้งค่า  
> * ไฟล์ *.html* ตัวอย่างหลายไฟล์ในโฟลเดอร์ที่คุณเลือก

---

## วิธีใช้ Executor กับ Fixed Thread Pool

หัวใจของโปรแกรม Java ที่ทำงานพร้อมกันหลาย ๆ อย่างคือ `ExecutorService` การสร้าง **fixed thread pool** จะบอก JVM ให้คงอยู่เพียง N worker threads เท่านั้น ซึ่งช่วยลดค่าใช้จ่ายของการสร้างเธรดและจำกัดการใช้ทรัพยากร

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*ทำไมเรื่องนี้ถึงสำคัญ:*  
ถ้าคุณสร้าง `Thread` ใหม่สำหรับไฟล์ HTML แต่ละไฟล์ ระบบปฏิบัติการจะต้องจัดตารางหลายสิบเธรดบนแล็ปท็อปที่มีทรัพยากรจำกัด ทำให้เกิดการสลับคอนเท็กซ์บ่อย ๆ Fixed pool จะใช้เธรดสี่ตัวเดียวซ้ำ ๆ ทำให้การใช้ CPU คาดเดาได้

---

## กำหนดไฟล์ HTML ที่จะประมวลผล – Fixed Thread Pool Java

ต่อไปเราจะระบุไฟล์ที่ต้องการส่งเข้า pool ในแอปจริงคุณอาจเดินสำรวจโครงสร้างโฟลเดอร์; ที่นี่เราจะทำให้เรียบง่าย

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*เคล็ดลับ:* `List.of` คืนค่าเป็นรายการที่ไม่เปลี่ยนแปลง ซึ่งปลอดภัยต่อการแชร์ระหว่างเธรดโดยไม่ต้องซิงโครไนซ์เพิ่มเติม

---

## ส่งงานแยกต่างหากสำหรับแต่ละไฟล์ HTML

ตอนนี้เราจะส่งพาธแต่ละไฟล์ให้ executor Lambda ที่ส่งไปจะทำงาน **แบบขนาน** บนหนึ่งในสี่ worker threads

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**เหตุผลที่เราห่อโลจิกไว้ในเมธอด** (`extractBodyText`) จะชัดเจนในส่วนต่อไป — ทำให้ lambda สะอาดและให้เรานำโค้ดการสกัดข้อความไปใช้ซ้ำได้ที่อื่น

---

## สกัดข้อความจาก HTML – โลจิกหลัก

นี่คือ helper ที่ใช้ **สกัดข้อความจาก html** ด้วย Jsoup เปิดไฟล์, แยก DOM, แล้วคืนค่า plain body text

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*ทำไมต้อง Jsoup?* มันเบา, จัดการ markup ที่ผิดรูปได้อย่างอ่อนโยน, และไม่ต้องใช้ engine ของเบราว์เซอร์ เมธอดจะโยน `IOException` ให้ผู้เรียกตัดสินใจว่าจะบันทึกหรือกู้คืนอย่างไร — เหมาะกับสถานการณ์ thread‑pool ที่คุณไม่ต้องการให้ไฟล์ที่เสียหายไฟล์เดียวทำให้ executor ทั้งหมดหยุดทำงาน

---

## ปิด Executor อย่างเรียบร้อย – สร้าง Fixed Thread Pool

หลังจากส่งงานทั้งหมดแล้ว เราต้องบอก pool ให้หยุดรับงานใหม่และทำงานที่คิวอยู่ให้เสร็จ

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*คำอธิบาย:* `shutdown()` ป้องกันการส่งงานใหม่, ส่วน `awaitTermination` จะบล็อกจนกว่างานแยกวิเคราะห์ทั้งหมดจะจบ (หรือเวลาสิ้นสุด). ถ้ามีบางอย่างค้าง, `shutdownNow()` จะพยายามยกเลิกงานที่กำลังทำอยู่ รูปแบบนี้เป็นวิธีที่แนะนำเพื่อ **create fixed thread pool** อย่างปลอดภัย

---

## ตัวอย่างเต็มที่สามารถรันได้

รวมทุกอย่างเข้าด้วยกัน นี่คือไฟล์เดียวที่คุณสามารถคอมไพล์และรันได้ มี import ที่จำเป็น, เมธอด `main`, และ helper ที่อธิบายข้างต้น

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่าแต่ละไฟล์มีข้อความใน body ประมาณ 1 200 ตัวอักษร):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

หากไฟล์ใดหายหรือรูปแบบไม่ถูกต้อง คุณจะเห็น stack trace พิมพ์ไปที่ `stderr` แต่งานอื่น ๆ จะดำเนินต่อไปโดยไม่มีผลกระทบ — พฤติกรรมที่ **java thread pool example** ควรมี

---

## คำถามทั่วไป & กรณีขอบ

| Question | Answer |
|----------|--------|
| *What if I have more than four files?* | The pool will queue the extra tasks and run them as soon as a thread becomes free. No extra code needed. |
| *Should I use `newCachedThreadPool` instead?* | `newCachedThreadPool` creates threads on demand and can grow unbounded, which is risky for I/O‑heavy jobs. A **fixed thread pool** gives you predictable memory and CPU usage. |
| *How do I change the pool size based on CPU cores?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` is a common pattern. |
| *What if parsing fails for one file?* | The `catch (IOException e)` inside the lambda isolates the failure, logs it, and lets the rest of the pool keep working. |
| *Can I return the extracted text to the caller?* | Yes—use `Future<String>` instead of `submit(Runnable)`. The code would look like `Future<String> f = executor.submit(() -> extractBodyText(path));` and later `String result = f.get();`. |

---

## สรุป

เราได้อธิบาย **วิธีใช้ executor** เพื่อสร้าง **fixed thread pool java** ที่ประมวลผลคอลเลกชันไฟล์ HTML พร้อมกัน, สกัดข้อความในส่วน body, และรายงานจำนวนอักขระ ตัวอย่าง **java thread pool example** ครบถ้วนนี้แสดงการจัดการทรัพยากรอย่างเหมาะสม, การจัดการข้อผิดพลาด, และเมธอดสกัดข้อความที่สามารถนำกลับมาใช้ใหม่ได้

ขั้นตอนต่อไป? ลองเปลี่ยนการทำงานของ `extractBodyText` ให้เป็น scraper ที่ซับซ้อนขึ้น, ทดลองเพิ่มขนาด pool, หรือส่งผลลัพธ์ไปยังฐานข้อมูล คุณยังสามารถสำรวจ `CompletionService` เพื่อดึงผลลัพธ์เมื่อพร้อม ซึ่งมีประโยชน์เมื่อขนาดไฟล์แตกต่างกันมาก

ปรับเปลี่ยนเส้นทางโฟลเดอร์, เพิ่มไฟล์, หรือรวมโค้ดส่วนนี้เข้าในเฟรมเวิร์กการครอว์ลที่ใหญ่ขึ้นก็ได้ รูปแบบหลัก — สร้าง pool, ส่งงานอิสระ, และปิดอย่างเรียบร้อย — ยังคงเหมือนเดิมไม่ว่าภาระงานจะซับซ้อนแค่ไหน

ขอให้เขียนโค้ดสนุกและเธรดของคุณทำงานต่อเนื่อง (จนกว่าคุณจะปิดมัน, แน่นอน)!

## บทเรียนที่เกี่ยวข้อง

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Use Aspose.HTML for Java - Mastering HTML5 Canvas Rendering](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}