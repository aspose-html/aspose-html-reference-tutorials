---
category: general
date: 2026-04-09
description: เรียกใช้หลายเธรดใน Java อย่างมีประสิทธิภาพโดยใช้ try‑with‑resources ใน
  Java. เรียนรู้วิธีโหลดเอกสาร HTML ใน Java อย่างปลอดภัยและหลีกเลี่ยงปัญหาการทำงานพร้อมกันใน
  Java.
draft: false
keywords:
- run multiple threads java
- use try with resources java
- load html document java
- avoid concurrency issues java
language: th
og_description: เรียกใช้หลายเธรดใน Java ด้วย try‑with‑resources Java. บทเรียนนี้แสดงวิธีโหลดเอกสาร
  HTML ใน Java อย่างปลอดภัยพร้อมหลีกเลี่ยงปัญหาการทำงานพร้อมกันใน Java.
og_title: เรียกใช้หลายเธรดใน Java – คู่มือ Try With Resources
tags:
- java
- multithreading
- html-parsing
title: รันหลายเธรดใน Java – ใช้ try‑with‑resources ใน Java
url: /th/java/creating-managing-html-documents/run-multiple-threads-java-use-try-with-resources-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# run multiple threads java – use try with resources java

เคยสงสัยไหมว่า **run multiple threads java** จะทำอย่างไรโดยไม่ทำให้กันและกันชนกัน? คุณไม่ได้เป็นคนเดียว—นักพัฒนาส่วนใหญ่เจออุปสรรคเดียวกันเมื่อต้องแชร์อ็อบเจกต์ที่เปลี่ยนแปลงได้ระหว่างเธรด ข่าวดีคือ? มีวิธีที่สะอาดและทันสมัยในการทำเช่นนั้น และเริ่มต้นด้วยคำสั่ง `try‑with‑resources`.

ในคู่มือนี้เราจะเดินผ่านตัวอย่างที่พร้อมคัดลอก‑วาง **loads an HTML document java**, สร้างหลายเธรด, และรับประกันว่าแต่ละเธรดทำงานกับอินสแตนซ์เอกสารของตนเอง เมื่อเสร็จคุณจะเห็นวิธี **avoid concurrency issues java** เพื่อให้แอปของคุณคงที่แม้โหลดสูง.

> **สิ่งที่คุณจะได้:** โปรแกรม Java ที่รันได้, คำอธิบายทีละขั้นตอน, เคล็ดลับสำหรับโครงการจริง, และการทดสอบอย่างรวดเร็วที่คุณสามารถรันได้ทันที

---

![ภาพประกอบการรันหลายเธรด java](run-multiple-threads-java.png "แผนภาพแสดงหลายเธรดแต่ละเธรดถืออินสแตนซ์ HTMLDocument แยกกัน")

## Prerequisites

- Java 17 หรือใหม่กว่า (ไวยากรณ์ `try‑with‑resources` ทำงานเช่นเดียวกันตั้งแต่ Java 7, แต่เราจะใช้ฟีเจอร์ภาษาใหม่เพื่อความกระชับ)  
- คลาสช่วยเหลือการแยกวิเคราะห์ HTML เล็ก ๆ ชื่อ `HTMLDocument`. หากคุณไม่มี คุณสามารถสร้างสแตกได้ตามที่แสดงต่อไป  
- ความรู้พื้นฐานเกี่ยวกับเธรด (`java.lang.Thread`) และอินเทอร์เฟซ `Runnable`

หากส่วนใดฟังดูแปลกใจ อย่ากังวล—แต่ละแนวคิดจะถูกอธิบายใหม่ในขั้นตอนต่อไป

---

## Step 1: Load HTML document java with a shared reference

สิ่งแรกที่เราต้องการคือ *อ้างอิงที่แชร์* ที่ชี้ไปยังไฟล์ที่ต้องการแยกวิเคราะห์ คิดว่าเป็นแบบแปลน: URL เหมือนกันสำหรับทุกเธรด แต่เอกสารจริงจะถูกสร้างต่อเธรดในภายหลัง

```java
// Step 1: Load the source HTML document (shared reference for its URL)
HTMLDocument sharedDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

### ทำไมต้องเป็นอ้างอิงที่แชร์?

หากคุณให้ทุกเธรดใช้อินสแตนซ์ `HTMLDocument` เดียวกัน พวกมันจะอ่านและเขียนไปยังบัฟเฟอร์ภายในเดียวกัน นั่นคือสูตรคลาสสิกของ race condition—ปัญหา **concurrency issues java** ที่เราต้องการหลีกเลี่ยง โดยการแชร์เฉพาะ *URL* เท่านั้น แต่ละเธรดจึงสามารถเปิดสตรีมของตนเองได้อย่างปลอดภัย

> **Pro tip:** เก็บ URL ไว้ในตัวแปร `final` หากคุณไม่มีใจจะเปลี่ยนค่า ตัวคอมไพเลอร์จะถือว่าเป็นค่าคงที่ ลดความเสี่ยงจากการเปลี่ยนแปลงโดยบังเอิญ

---

## Step 2: Create a thread‑safe task using try with resources java

ต่อไปเราจะกำหนดสิ่งที่แต่ละเธรดทำจริง ๆ เทคนิคคือการห่อการสร้าง `HTMLDocument` ของแต่ละเธรดไว้ในบล็อก `try‑with‑resources` ซึ่งรับประกันว่าเอกสารจะถูกปิดโดยอัตโนมัติ แม้จะเกิดข้อยกเว้นก็ตาม

```java
// Step 2: Define a task that creates its own document instance per thread
Runnable task = () -> {
    // Each thread works with its own copy to avoid concurrency issues
    try (HTMLDocument threadDoc = new HTMLDocument(sharedDoc.getUrl())) {
        // Perform thread‑specific operations on threadDoc here
        System.out.println("Thread " + Thread.currentThread().getName()
                + " loaded: " + threadDoc.getTitle());
    } catch (Exception e) {
        System.err.println("Error in thread " + Thread.currentThread().getName()
                + ": " + e.getMessage());
    }
};
```

### `try‑with‑resources` ช่วยอย่างไร

คลาส `HTMLDocument` implements `java.lang.AutoCloseable`. เมื่อบล็อก `try` สิ้นสุด JVM จะเรียก `threadDoc.close()` โดยอัตโนมัติ วิธีนี้ปลอดภัยกว่าการใช้ `finally` ด้วยตนเองและขจัดความเสี่ยงจากการลืมปล่อยทรัพยากรเนทีฟ—สิ่งที่อาจทำให้เกิด memory leak ในแอปหลายเธรดที่ทำงานต่อเนื่อง

---

## Step 3: Launch threads and avoid concurrency issues java

เมื่อเตรียมงานแล้ว เราสามารถสปินเธรดได้ตามต้องการ สำหรับการสาธิต เราจะเริ่มสองเธรด, แต่คุณก็สามารถเปิด thread pool ที่มีหลายสิบ worker ได้ตามสบาย

```java
// Step 3: Launch multiple threads that execute the same task
Thread t1 = new Thread(task, "Worker‑1");
Thread t2 = new Thread(task, "Worker‑2");

// Start the threads
t1.start();
t2.start();

// Optional: wait for them to finish (join) if you need deterministic ordering
t1.join();
t2.join();
```

### ทำไมไม่ใช้ `ExecutorService`?

ในโค้ดผลิตจริงคุณอาจ **จะ** ใช้ `ExecutorService` เพื่อจัดการ pool ของ worker ตัวอย่าง `Thread` ธรรมดานี้ทำให้บทเรียนมุ่งเน้นที่แนวคิดหลัก—การสร้างเอกสารแยกกันต่อเธรดพร้อมใช้ `try‑with‑resources` หากต้องการ คุณสามารถแทนที่การเรียก `Thread` ด้วย `FixedThreadPool` ได้ตามสถาปัตยกรรมของโครงการ

---

## Full, runnable example

รวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมที่ทำงานได้เองซึ่งคุณสามารถวางลงในไฟล์ชื่อ `MultiThreadHtmlDemo.java` พร้อมสแตกขั้นต่ำสำหรับ `HTMLDocument` เพื่อให้คุณคอมไพล์และรันได้ทันที

```java
// MultiThreadHtmlDemo.java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

// --- Minimal stub for demonstration purposes ---
class HTMLDocument implements AutoCloseable {
    private final String url;
    private String content;

    public HTMLDocument(String url) throws IOException {
        this.url = url;
        // Simulate loading the file (replace with real parser in production)
        this.content = Files.readString(Path.of(url));
    }

    public String getUrl() {
        return url;
    }

    public String getTitle() {
        // Very naive title extraction – just for demo
        int start = content.indexOf("<title>");
        int end = content.indexOf("</title>");
        if (start != -1 && end != -1 && end > start) {
            return content.substring(start + 7, end).trim();
        }
        return "Untitled";
    }

    @Override
    public void close() {
        // In a real library you’d release native buffers here
        content = null;
        System.out.println("Closed document for URL: " + url);
    }
}

// --- Main class that runs multiple threads java ---
public class MultiThreadHtmlDemo {
    public static void main(String[] args) throws InterruptedException, IOException {
        // Step 1: Load the source HTML document (shared reference for its URL)
        HTMLDocument sharedDoc = new HTMLDocument("sample.html");

        // Step 2: Define a task that creates its own document instance per thread
        Runnable task = () -> {
            try (HTMLDocument threadDoc = new HTMLDocument(sharedDoc.getUrl())) {
                System.out.println("Thread " + Thread.currentThread().getName()
                        + " loaded title: " + threadDoc.getTitle());
            } catch (Exception e) {
                System.err.println("Error in thread " + Thread.currentThread().getName()
                        + ": " + e.getMessage());
            }
        };

        // Step 3: Launch multiple threads that execute the same task
        Thread t1 = new Thread(task, "Worker‑1");
        Thread t2 = new Thread(task, "Worker‑2");

        t1.start();
        t2.start();

        // Wait for both threads to finish
        t1.join();
        t2.join();

        System.out.println("All threads completed.");
    }
}
```

#### ผลลัพธ์ที่คาดหวัง (สมมติว่า `sample.html` มี `<title>Hello World</title>`)

```
Thread Worker-1 loaded title: Hello World
Closed document for URL: sample.html
Thread Worker-2 loaded title: Hello World
Closed document for URL: sample.html
All threads completed.
```

สังเกตว่าแต่ละเธรดพิมพ์ *title ที่โหลด* ของตนเองแล้วเมธอด `close()` ทำงานโดยอัตโนมัติ—ตรงกับสิ่งที่ `try‑with‑resources` สัญญาไว้

---

## Common questions & edge‑case handling

**ไฟล์ไม่พบจะทำอย่างไร?**  
คอนสตรัคเตอร์จะโยน `IOException`. ในตัวอย่างเราจับข้อยกเว้นภายใน `Runnable` และบันทึกข้อผิดพลาด ดังนั้นไฟล์หายจะไม่ทำให้แอปทั้งหมดพัง

**ฉันสามารถใช้ `HTMLDocument` ตัวเดียวกันข้ามเธรดได้หรือไม่?**  
ได้เฉพาะเมื่อคลาสนั้นระบุว่า thread‑safe อย่างชัดเจน ตัวพาร์เซอร์ส่วนใหญ่มีสถานะที่เปลี่ยนแปลงได้ (เช่น DOM tree) การแชร์อินสแตนซ์เดียวมักทำให้เกิด **concurrency issues java**. รูปแบบที่แสดงที่นี่—หนึ่งอินสแตนซ์ต่อเธรด—เป็นค่าเริ่มต้นที่ปลอดภัยที่สุด

**ต้องซิงโครไนซ์อะไรบ้างหรือไม่?**  
ไม่ต้อง เพราะแต่ละเธรดทำงานกับ `HTMLDocument` ของตนเอง ไม่มีสถานะที่เปลี่ยนแปลงได้ที่แชร์กัน เพียงส่วนที่แชร์คือสตริง URL ซึ่งเป็น immutable อยู่แล้ว

**จะเป็นอย่างไรถ้าใช้ `ExecutorService`?**  

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
for (int i = 0; i < 4; i++) {
    executor.submit(task);
}
executor.shutdown();
executor.awaitTermination(1, TimeUnit.MINUTES);
```

ตรรกะหลักยังคงเหมือนเดิม; pool จะจัดการวงจรชีวิตของเธรดให้คุณ

---

## Pro tips for production‑grade multithreading

1. **จำกัดจำนวนเธรด** – การสร้างเธรด `Thread` จำนวนหลายสิบอาจทำให้ OS ลำบาก ใช้ thread pool ที่มีขอบเขตแทน  
2. **ใช้การกำหนดค่าที่ไม่เปลี่ยนแปลง** – ทำให้ URL, เส้นทางไฟล์, และการตั้งค่าพาร์เซอร์เป็น immutable เพื่อไม่ให้ worker เปลี่ยนแปลงโดยบังเอิญ  
3. **ตรวจสอบการใช้ทรัพยากร** – แม้จะใช้ `try‑with‑resources` ก็ตาม การเปิดไฟล์หลายไฟล์พร้อมกันอาจทำให้หมด file descriptor จัดการจำนวนงานพร้อมกันให้เหมาะสมหากถึงขีดจำกัด  
4. **Shutdown อย่างสุภาพ** – ปิด executor หรือ join เธรดเสมอ เพื่อให้ JVM สามารถออกจากการทำงานได้อย่างสะอาด

---

## Conclusion

ตอนนี้คุณมีรูปแบบที่พร้อมคัดลอก‑วางสำหรับ **run multiple threads java** พร้อม **using try with resources java**, **loading html document java**, และ **avoiding concurrency issues java** อย่างปลอดภัย ประเด็นสำคัญคือ: ให้แต่ละเธรดมีอินสแตนซ์เอกสารของตนเอง, ให้ `try‑with‑resources` จัดการทำความสะอาด, และทำให้ข้อมูลที่แชร์เป็น immutable

ต่อไปคุณอาจสำรวจ:

- ขยายรูปแบบด้วย `ExecutorService` และ work queue  
- เปลี่ยนไปใช้พาร์เซอร์ HTML จริงอย่าง *jsoup* (ซึ่งก็ implement `Closeable`)  
- เพิ่มการจัดการข้อผิดพลาดที่ซับซ้อนหรือ logic การ retry สำหรับ I/O ที่ไม่เสถียร

ลองใช้ ปรับจำนวน worker แล้วดูผลลัพธ์ในคอนโซลยังคงเป็นระเบียบ—no

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}