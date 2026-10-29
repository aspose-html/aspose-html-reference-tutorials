---
category: general
date: 2026-06-19
description: วิธีเริ่ม thread ใน Java ด้วย Runnable ที่สามารถใช้ซ้ำได้, เริ่มหลาย
  thread, พิมพ์ชื่อ thread, และแยกวิเคราะห์ HTML ด้วย Java. ตัวอย่างขั้นตอนต่อขั้นตอน.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: th
og_description: วิธีเริ่ม thread ใน Java ด้วย Runnable, รันหลาย thread, พิมพ์ชื่อ
  thread, และแยกวิเคราะห์ HTML ด้วย Java ในตัวอย่างเดียวที่สามารถรันได้
og_title: วิธีเริ่มต้นเธรดใน Java – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: วิธีเริ่มต้นเธรดใน Java – คู่มือครบถ้วน
url: /th/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเริ่ม thread ใน Java – คู่มือฉบับสมบูรณ์

เคยสงสัย **วิธีเริ่ม thread** ใน Java โดยไม่ต้องเจอกับโค้ดซ้ำซ้อนหรือเปล่า? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังสร้างเว็บครอเลอร์, ตัวอัปเดต UI, หรือแค่ต้องการย้ายการคำนวณหนักออกไป การเชี่ยวชาญการสร้าง thread เป็นทักษะที่จำเป็นสำหรับนักพัฒนา Java ทุกคน

ในบทเรียนนี้เราจะเดินผ่านสถานการณ์จริง: **แยกวิเคราะห์ HTML ด้วย Java**, พิมพ์ชื่อ thread ปัจจุบัน, และ **เริ่มหลาย thread** ที่ใช้ตรรกะเดียวกัน เมื่อจบคุณจะรู้ **วิธีใช้ Runnable**, สร้าง worker หลายตัว, และเห็นผลลัพธ์ที่คาดหวัง—ทั้งหมดในตัวอย่างที่สามารถคัดลอก‑วางได้ทันที

## สิ่งที่คุณจะได้เรียน

- ขั้นตอนที่แม่นยำ **วิธีเริ่ม thread** ด้วยคลาส `Thread` และ `Runnable`
- วิธี **เริ่มหลาย thread** ที่ทำงานเดียวกันโดยไม่ต้องคัดลอกโค้ด
- วิธีที่ง่ายที่สุดในการ **พิมพ์ชื่อ thread** ควบคู่กับผลลัพธ์การประมวลผลของคุณ
- วิธีที่สะอาดในการ **แยกวิเคราะห์ HTML ด้วย Java** โดยใช้ตัวช่วย `HTMLDocument` ที่มีน้ำหนักเบา (หรือพาร์เซอร์ใดก็ได้ที่คุณต้องการ)
- ทำไม **วิธีใช้ runnable** ถึงสำคัญสำหรับโค้ดที่นำกลับมาใช้ใหม่และทดสอบได้

ไม่ต้องใช้ไลบรารีภายนอกสำหรับตัวอย่างหลัก แต่เราจะบอกจุดที่คุณอาจเปลี่ยนเป็น Jsoup หรือพาร์เซอร์อื่นหากต้องการพลังมากขึ้น

---

## ขั้นตอนที่ 1: กำหนดงานที่นำกลับมาใช้ได้ – **วิธีใช้ runnable**

สิ่งแรกที่คุณต้องรู้ **วิธีใช้ runnable** คือการห่อหุ้มงานที่แต่ละ thread จะทำ `Runnable` เป็นเพียงอินเทอร์เฟซฟังก์ชันที่มีเมธอด `run()` เพียงเมธอดเดียว ทำให้เหมาะกับ lambda expression

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**ทำไมเรื่องนี้ถึงสำคัญ:** การเก็บตรรกะไว้ใน `Runnable` ทำให้คุณสามารถส่งต่อให้กับออบเจ็กต์ `Thread` ใดก็ได้, thread pool, หรือแม้แต่ executor service ในภายหลัง ทำให้โค้ดของคุณ DRY และทดสอบได้ง่าย

---

## ขั้นตอนที่ 2: **วิธีเริ่ม thread** – สร้าง worker ตัวแรก

เมื่อเรามี `Runnable` แล้ว การเปิด thread ก็ง่ายเหมือนเรียกคอนสตรัคเตอร์ของ `Thread` คำถาม **วิธีเริ่ม thread** จะได้รับคำตอบในบรรทัดเดียว

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

สังเกตอาร์กิวเมนต์ที่สอง `"Worker-1"` ชื่อนี้จะปรากฏเมื่อเราต่อม **พิมพ์ชื่อ thread** ทำให้การดีบักง่ายขึ้นมาก

---

## ขั้นตอนที่ 3: **เริ่มหลาย thread** – ใช้ `Runnable` เดียวกันซ้ำ

ต้องการประมวลผลไฟล์ HTML หลายไฟล์พร้อมกัน? เพียงสร้าง `Thread` อีกตัวโดยใช้ `Runnable` เดียวกัน นี่แสดงให้เห็น **เริ่มหลาย thread** โดยไม่ต้องคัดลอกโค้ดงาน

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

ทั้ง `Worker-1` และ `Worker-2` จะทำงานในบล็อกที่กำหนดใน `extractTextLength` พร้อมกัน เนื่องจากงานไม่มีสถานะ (อ่านไฟล์เท่านั้น) จึงไม่มีปัญหา race condition

---

## ขั้นตอนที่ 4: **พิมพ์ชื่อ thread** ขณะแยกวิเคราะห์ HTML

ภายใน `Runnable` เราได้เรียก `Thread.currentThread().getName()` แล้ว นั่นคือวิธีมาตรฐานในการ **พิมพ์ชื่อ thread** ผลลัพธ์จะออกมาประมาณนี้ (สมมติว่า body ของ HTML มี 1 234 ตัวอักษร)

```
Worker-1: 1234
Worker-2: 1234
```

หากคุณรันโปรแกรมกับไฟล์ขนาดใหญ่กว่า แต่ละบรรทัดจะยังคงแสดงความยาวเดียวกันเพราะทั้งสอง thread อ่านไฟล์เดียวกัน เปลี่ยนพาธหรือส่งชื่อไฟล์เป็นพารามิเตอร์เพื่อดูผลลัพธ์ที่แตกต่างกัน

---

## ขั้นตอนที่ 5: ตัวอย่างเต็มที่สามารถรันได้ – ตั้งแต่ import จนถึงการทำงาน

ด้านล่างเป็นโปรแกรม **self‑contained** เต็มรูปแบบที่คุณสามารถวางลงในไฟล์ชื่อ `HtmlThreadDemo.java` มันรวม stub `HTMLDocument` เล็ก ๆ เพื่อให้โค้ดคอมไพล์ได้แม้คุณไม่มีพาร์เซอร์จริง ๆ แทนที่ stub ด้วย Jsoup หรือไลบรารีใดก็ได้ที่คุณต้องการสำหรับการใช้งานจริง

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### ผลลัพธ์ที่คาดหวัง

สมมติว่า `page.html` มี 2 567 ตัวอักษรอยู่ในแท็ก `<body>` คุณจะเห็นประมาณนี้:

```
Worker-1: 2567
Worker-2: 2567
```

หากไฟล์ไม่สามารถอ่านได้ stack trace จะถูกพิมพ์ออกมา—ขอบคุณบล็อก `catch`

---

## ข้อผิดพลาดทั่วไป & เคล็ดลับระดับมืออาชีพ

| ปัญหา | ทำไมเกิดขึ้น | วิธีแก้ |
|-------|--------------|----------|
| **File not found** | พาธ `"YOUR_DIRECTORY/page.html"` เป็นพาธสัมพันธ์กับตำแหน่งที่คุณเรียก JVM | ใช้พาธแบบ absolute หรือ `Paths.get("").toAbsolutePath()` เพื่อดีบัก |
| **Race conditions** | หาก `Runnable` แก้ไขสถานะที่แชร์กัน thread จะชนกัน | ทำให้งานเป็น stateless หรือ synchronize การเข้าถึงออบเจ็กต์ที่แชร์ |
| **Too many threads** | การสร้าง `Thread` จำนวนหลายสิบอาจทำให้ทรัพยากร OS หมด | เปลี่ยนเป็น `ExecutorService` พร้อม pool ที่จำกัดหลังจากคุณเชี่ยวชาญพื้นฐาน |
| **Incorrect HTML parsing** | Stub `HTMLDocument` มีความเรียบง่าย; หน้าเว็บซับซ้อนอาจพัง | แทนที่ด้วย Jsoup: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## การขยายตัวอย่าง

ตอนนี้คุณรู้ **วิธีเริ่ม thread** แล้ว คุณอาจต้องการ:

- **แยกวิเคราะห์ไฟล์ต่าง ๆ** โดยส่งชื่อไฟล์เข้า `Runnable` (ใช้คอนสตรัคเตอร์หรือ lambda ที่จับตัวแปร)
- **รวบรวมผลลัพธ์** ด้วย `ConcurrentLinkedQueue<Integer>` แทนการพิมพ์เท่านั้น
- **ใช้ thread pool** (`Executors.newFixedThreadPool(4)`) เพื่อความสามารถในการขยายตัวที่ดีกว่า
- **สลับพาร์เซอร์** เป็น Jsoup, HtmlUnit หรือไลบรารีใดก็ได้ที่เหมาะกับโครงการของคุณ

ขั้นตอนทั้งหมดยังคงอิงกับแนวคิดหลักที่เราอธิบายไว้: กำหนดงานที่นำกลับมาใช้ได้, ส่งให้กับหนึ่งหรือหลาย thread, และสังเกตว่า thread ใดกำลังทำงานโดย **พิมพ์ชื่อ thread**

---

## สรุป

เราได้ครอบคลุม **วิธีเริ่ม thread** ใน Java, แสดง **วิธีใช้ runnable** เพื่อทำงานที่นำกลับมาใช้ได้, สาธิต **วิธีเริ่มหลาย thread**, และอธิบายวิธี **แยกวิเคราะห์ HTML ด้วย Java** พร้อม **พิมพ์ชื่อ thread** สำหรับแต่ละ worker โค้ดเต็มที่อยู่ด้านบนพร้อมรันได้ทันที และแนวคิดเหล่านี้สามารถขยายไปสู่แอปพลิเคชันระดับ production ที่ซับซ้อนได้

ลองเปลี่ยนพาธไฟล์, เพิ่มจำนวน worker, หรือเชื่อมต่อพาร์เซอร์ HTML จริง ผลลัพธ์พื้นฐานยังคงเหมือนเดิม และคุณมีพื้นฐานที่มั่นคงสำหรับโครงการ Java แบบหลาย thread ใด ๆ

มีคำถามเกี่ยวกับ thread safety, executor services, หรือไลบรารีการแยกวิเคราะห์ HTML? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ต่อ‑ขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}