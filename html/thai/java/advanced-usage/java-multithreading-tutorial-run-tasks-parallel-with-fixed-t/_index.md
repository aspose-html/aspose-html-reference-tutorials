---
category: general
date: 2026-04-05
description: บทเรียนการทำงานหลายเธรดใน Java แสดงวิธีรันงานแบบขนานโดยใช้ Fixed Thread
  Pool ของ Java และปิด ExecutorService อย่างปลอดภัย
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: th
og_description: บทแนะนำการทำงานหลายเธรดใน Java ที่พาคุณผ่านการรันงานแบบขนาน การสร้าง
  Fixed Thread Pool ใน Java การพิมพ์ชื่อเธรด และการปิด ExecutorService อย่างเรียบร้อย
og_title: บทเรียนการทำงานหลายเธรดใน Java – การดำเนินการแบบขนานด้วยพูลเธรดคงที่
tags:
- Java
- Concurrency
- ExecutorService
title: 'บทเรียนการทำงานหลายเธรดใน Java: รันงานพร้อมกันด้วย Fixed Thread Pool'
url: /th/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – การทำงานแบบขนานอย่างง่าย

เคยสงสัยไหมว่าจะแบบ **run tasks parallel** ใน Java อย่างไรโดยไม่ต้องจมอยู่กับการจัดการเธรดระดับต่ำ? ใน **java multithreading tutorial** นี้ เราจะพาคุณผ่านขั้นตอนนั้นโดยใช้ **fixed thread pool java**, พิมพ์ชื่อของแต่ละเธรด, และทำการ **shutdown executorservice** อย่างสะอาดเมื่อทำงานเสร็จ  

หากคุณเคยเขียนลูปที่บล็อกอยู่กับ network I/O หรือคุณต้องการดึงข้อมูลหลายหน้าเว็บพร้อมกัน, รูปแบบที่เราจะอธิบายด้านล่างจะช่วยคุณประหยัดเวลาและความยุ่งยาก  

เราจะครอบคลุมทุกอย่างที่คุณต้องการ—ไม่มีเอกสารภายนอก, เพียงโค้ด Java แท้ที่คุณสามารถคัดลอก‑วาง, รัน, และดูผลลัพธ์ได้ทันที. เมื่อจบคุณจะเข้าใจว่าทำไม fixed thread pool จึงมักเป็นจุดที่เหมาะสมสำหรับการทำงานขนานแบบจำกัด, วิธีการหยุดทำงานอย่างปลอดภัย, และวิธีทำให้บันทึกของคุณอ่านง่ายขึ้นโดยการพิมพ์ชื่อเธรด  

> **Prerequisites**: Java 8+ (แพคเกจ `java.util.concurrent` มีความเสถียรมาหลายปี), IDE หรือคำสั่ง `javac`/`java` แบบง่าย, และความเข้าใจพื้นฐานของ OOP. ไม่จำเป็นต้องใช้ไลบรารีเพิ่มเติมนอกจาก Aspose HTML for Java jar ที่คุณมีอยู่แล้ว.

---

![java multithreading tutorial diagram showing a thread pool feeding tasks](https://example.com/images/java-multithreading-tutorial.png "java multithreading tutorial diagram")

## java multithreading tutorial – ตั้งค่า Fixed Thread Pool

**fixed thread pool** จำกัดจำนวนเธรดที่ทำงานพร้อมกัน, ป้องกันแอปพลิเคชันของคุณจากการสร้างเธรดของ OS มากเกินไปและทำให้ทรัพยากรหมด. ที่นี่เราจะสร้าง pool ที่มี worker สี่คน:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Why four?* มันตรงกับจำนวน URL ที่เราจะดึง, แต่คุณสามารถปรับจำนวนนี้ตามจำนวนคอร์ CPU, ความเข้มข้นของ I/O, หรือขีดจำกัดหน่วยความจำ. ฟactory `Executors` ปกป้องคุณจากคอนสตรัคเตอร์ระดับต่ำของ `Thread` และให้คุณอ้างอิง `ExecutorService` ที่สะอาดซึ่งคุณจะใช้ **shutdown executorservice** ต่อไป.

## เตรียม URLs และกำหนด Parallel Tasks

ต่อไปเราจะรายการหน้าเว็บที่ต้องการประมวลผล. ใน scraper จริงคุณอาจอ่านรายการเหล่านี้จากไฟล์หรือฐานข้อมูล, แต่การใช้ array แบบคงที่ทำให้ตัวอย่างนี้เป็นอิสระ:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

ตอนนี้มาถึงส่วน **run tasks parallel**. สำหรับแต่ละ URL เราจะส่ง lambda ที่โหลดเอกสารและพิมพ์หัวเรื่องของมัน. สังเกตการใช้ `Thread.currentThread().getName()` – นี่คือเทคนิค **print thread name** ของเราซึ่งทำให้การดีบักง่ายขึ้นมาก:

```java
        // Step 3: Submit a task for each URL that loads the document and prints its title
        for (String url : pageUrls) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(url)) {
                    String title = doc.getTitle();
                    // Print the thread name alongside the title
                    System.out.println(Thread.currentThread().getName() + " – " + title);
                } catch (Exception e) {
                    System.err.println(Thread.currentThread().getName() + " failed: " + e.getMessage());
                }
            });
        }
```

> **Pro tip**: การห่อ `HTMLDocument` ด้วยบล็อก try‑with‑resources รับประกันว่าสตรีมพื้นฐานจะถูกปิด, แม้หน้าเว็บจะโหลดไม่สำเร็จ.

## ปิดการทำงานของ ExecutorService อย่างสุภาพ

การปล่อยให้ thread pool ยังคงทำงานหลังจากงานเสร็จแล้วอาจทำให้ JVM ค้าง. วิธีที่ถูกต้องคือ **shutdown executorservice**, แล้วรอการสิ้นสุด:

```java
        // Step 4: Shut down the pool and wait for all tasks to finish
        executor.shutdown();                         // No new tasks will be accepted
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            // Force shutdown if tasks exceed the timeout
            executor.shutdownNow();
        }
    }
}
```

*Why the timeout?* มันปกป้องคุณจากงานที่ไม่คืนค่า (เช่น การเรียกเครือข่ายที่ค้าง). หาก pool ไม่เสร็จภายในหนึ่งนาที เราจะเรียก `shutdownNow()` เพื่อขัดจังหวะเธรดที่ค้างอยู่.

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะพิมพ์อะไรคล้าย ๆ นี้:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

ลำดับที่แน่นอนอาจแตกต่างกัน—เพราะงานทำงานแบบขนานจริง ๆ. สิ่งที่คงที่คือคำนำหน้า **print thread name**, ซึ่งบอกคุณอย่างชัดเจนว่า worker ใดจัดการ URL แต่ละอัน.

---

## ความแตกต่างทั่วไปและกรณีขอบ

| สถานการณ์ | สิ่งที่ต้องเปลี่ยน | เหตุผล |
|-----------|----------------|--------|
| **URLs มากกว่าจำนวนเธรด** | คงขนาด pool เดิม; งานที่เหลือจะถูกจัดคิวโดยอัตโนมัติ. | Fixed pool จะจัดการ back‑pressure ให้คุณเอง. |
| **งานที่ใช้ CPU มาก** | ตั้งค่าขนาด pool เป็น `Runtime.getRuntime().availableProcessors()` แทนการกำหนดค่า 4 แบบคงที่. | เพิ่มการใช้ CPU ให้เต็มที่โดยไม่ทำให้เกิดการ oversubscribe. |
| **ต้องการยกเลิกงานเฉพาะ** | เก็บอ้างอิง `Future<?>` จาก `executor.submit()` แล้วเรียก `future.cancel(true)`. | ให้การควบคุมระดับละเอียดต่อแต่ละงาน. |
| **ประมวลผลไฟล์ขนาดใหญ่** | เพิ่มขนาด pool อย่างพอประมาณ *หรือ* เปลี่ยนไปใช้ `newCachedThreadPool()` หากคาดว่าจะมีการระเบิดงาน. | Cached pool จะสร้างเธรดตามความต้องการ แต่ต้องระวังการเติบโตที่ไม่มีขีดจำกัด. |

---

## สรุป

คุณมี **java multithreading tutorial** ที่แข็งแกร่งแล้ว ซึ่งแสดงวิธี **run tasks parallel** ด้วย **fixed thread pool java**, **print thread name** เพื่อการบันทึกที่ชัดเจน, และ **shutdown executorservice** อย่างเรียบร้อย. โค้ดที่สมบูรณ์และรันได้อยู่ในคลาสเดียว, ดังนั้นคุณสามารถนำไปใส่ในโปรเจกต์ใดก็ได้และเริ่มขยายงาน I/O‑bound ของคุณได้ทันที.

ต่อไปคุณจะทำอะไร? ลองเปลี่ยน `HTMLDocument` เป็น HTTP client ของคุณเอง, ทดลองขนาด pool ต่าง ๆ, หรือรวม `CompletionService` เพื่อรวบรวมผลลัพธ์เมื่อเสร็จ. คุณอาจสำรวจ `java.util.concurrent.Flow` สำหรับ reactive streams หากต้องการการจัดการ back‑pressure ที่ซับซ้อนกว่าคิวแบบง่าย.

ขอให้สนุกกับการเขียนโค้ด, และจำไว้ว่า: ด้วยกลยุทธ์ thread‑pool ที่เหมาะสม, การทำงานพร้อมกันจะกลายเป็น *piece of cake* ไม่ใช่แหล่งของบั๊ก. หากมีคำถาม, อย่าลังเลที่จะคอมเมนต์—ผมพร้อมพูดคุยเกี่ยวกับ Java concurrency เสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}