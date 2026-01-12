---
category: general
date: 2026-01-01
description: เรียนรู้วิธีใช้ fixed thread pool ใน Java เพื่อลบแท็ก script จากไฟล์ HTML
  ตัวอย่าง executorservice นี้ใน Java แสดงการโหลดเอกสาร HTML อย่างมีประสิทธิภาพ.
draft: false
keywords:
- fixed thread pool java
- remove script tags
- remove javascript html
- executorservice example java
- load html document
language: th
og_description: เชี่ยวชาญการใช้ Fixed Thread Pool ใน Java เพื่อลบแท็ก script จากไฟล์
  HTML. ตัวอย่าง ExecutorService ที่สมบูรณ์ใน Java พร้อมขั้นตอนการโหลดเอกสาร HTML.
og_title: กลุ่มเธรดคงที่ใน Java – คู่มือทำความสะอาด HTML แบบขนาน
tags:
- Java concurrency
- HTML processing
- Aspose.HTML
title: พูลเธรดคงที่ของ Java – การทำความสะอาด HTML แบบขนานด้วย ExecutorService
url: /th/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fixed thread pool java – Parallel HTML Cleaning with ExecutorService

เคยต้องการ **fixed thread pool java** เพื่อเร่งการประมวลผล HTML จำนวนมากหรือไม่? คุณไม่ได้เป็นคนเดียว เมื่อคุณมีไฟล์ HTML หลายสิบหรือแม้แต่หลายร้อยไฟล์ที่เต็มไปด้วยองค์ประกอบ `<script>` การทำงานแบบต่อเนื่องอาจรู้สึกเหมือนรอให้สีแห้ง  

ในบทแนะนำนี้เราจะสาธิตวิธีสร้าง **fixed thread pool java** โหลดเอกสาร HTML แต่ละไฟล์ ลบ JavaScript (`<script>` tags) ทั้งหมดออก และบันทึกไฟล์ที่ทำความสะอาดแล้ว—ทั้งหมดทำงานพร้อมกันด้วย **executorservice example java** เมื่อเสร็จคุณจะได้โปรแกรมพร้อมรันที่ลบ `<script>` อย่างมีประสิทธิภาพ และเข้าใจว่าทำไม fixed thread pool จึงมักเป็นตัวเลือกที่เหมาะสมสำหรับงานที่ใช้ CPU อย่างหนัก

## What You’ll Achieve

- ตั้งค่า `ExecutorService` ด้วยจำนวนเธรดคงที่  
- โหลดไฟล์ HTML ด้วย `HTMLDocument` ของ Aspose.HTML  
- ใช้ CSS selector เพื่ **remove script tags** (หรือองค์ประกอบที่ไม่ต้องการอื่น ๆ)  
- บันทึกผลลัพธ์ที่ทำความสะอาดด้วยรูปแบบการตั้งชื่อที่ชัดเจน  
- จัดการการปิดและการหยุดทำงานอย่างสุภาพของ thread pool  

ไม่มีเครื่องมือสร้างโค้ดภายนอก ไม่มีเวทมนตร์ลับ—แค่ Java 8+ และ Aspose.HTML

---

## Prerequisites

ก่อนที่เราจะเริ่ม โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

| Requirement | Why it matters |
|-------------|----------------|
| **Java 8 or newer** | จำเป็นสำหรับ lambda expressions และ API ของ `ExecutorService` |
| **Aspose.HTML for Java** (download from <https://products.aspose.com/html/java/>) | ให้คลาส `HTMLDocument` ที่ใช้โหลดและจัดการ HTML |
| **A folder with sample HTML files** | ตัวอย่างจะประมวลผลไฟล์เช่น `input1.html`, `input2.html` เป็นต้น |
| **An IDE or command‑line build tool** (IntelliJ, Eclipse, Maven, Gradle) | เพื่อคอมไพล์และรันโค้ด |

หากคุณยังไม่ได้เพิ่ม Aspose.HTML ไปยังโปรเจกต์ของคุณ ให้วางไฟล์ JAR ลงในโฟลเดอร์ `libs` แล้วเพิ่มลงใน classpath หรือประกาศ dependency ของ Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

---

## Step 1: Create a Fixed Thread Pool java

**fixed thread pool java** ให้จำนวนเธรดทำงานที่คงที่ซึ่งคงอยู่ตลอดงานทั้งหมด ช่วยหลีกเลี่ยงค่าใช้จ่ายจากการสร้างและทำลายเธรดบ่อย ๆ ซึ่งเป็นประโยชน์อย่างยิ่งเมื่อแต่ละงานสั้น ๆ เช่น การโหลดและทำความสะอาดไฟล์ HTML หนึ่งไฟล์

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

public class ParallelProcessingDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
        // ...
    }
}
```

> **Pro tip:** เลือกขนาดของ pool ตามจำนวนคอร์ของ CPU (`Runtime.getRuntime().availableProcessors()`) แล้วเพิ่มบัฟเฟอร์เล็กน้อยหากงานมีส่วนเกี่ยวข้องกับ I/O

---

## Step 2: List the HTML Files You Want to Process

คุณอาจสแกนโฟลเดอร์แบบไดนามิกได้ แต่เพื่อความชัดเจนเราจะกำหนดอาร์เรย์แบบฮาร์ดโค้ด แทนที่ `"YOUR_DIRECTORY"` ด้วยพาธจริงบนเครื่องของคุณ

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/input1.html",
    "YOUR_DIRECTORY/input2.html",
    "YOUR_DIRECTORY/input3.html",
    "YOUR_DIRECTORY/input4.html"
};
```

หากต้องการวิธีแบบไดนามิก `Files.list(Paths.get("YOUR_DIRECTORY"))` สามารถเติมอาร์เรย์ให้โดยอัตโนมัติ

---

## Step 3: Submit a Cleaning Task for Each File

แต่ละไฟล์จะได้รับ **executorservice example java** task ของตนเอง ภายใน lambda เราจะทำ:

1. เปิดไฟล์ด้วย `HTMLDocument`  
2. **Remove script tags** ด้วย CSS selector (`"script"`)  
3. บันทึกไฟล์ที่ทำความสะอาดด้วยส่วนต่อท้าย `_clean.html`

```java
for (String htmlFile : htmlFiles) {
    executor.submit(() -> {
        // Load the document (each thread works with its own instance)
        try (HTMLDocument doc = new HTMLDocument(htmlFile)) {
            // Remove all <script> elements from the document
            doc.querySelectorAll("script")
               .forEach(node -> node.getParentNode().removeChild(node));

            // Save the cleaned document with a new name
            doc.save(htmlFile.replace(".html", "_clean.html"));
        } catch (Exception e) {
            System.err.println("Failed to process " + htmlFile + ": " + e.getMessage());
        }
    });
}
```

> **Why this works:** `querySelectorAll("script")` คืนคอลเลกชันของทุกองค์ประกอบ `<script>` ที่มีอยู่แบบ live แล้วลูป `forEach` จะตัดโหนดแต่ละอันออกจากพาเรนต์ ทำให้ **remove javascript html** จากแหล่งที่มา

---

## Step 4: Shut Down the Pool and Await Completion

การหยุดทำงานอย่างสุภาพเป็นสิ่งสำคัญ; คุณไม่ต้องการให้เธรดค้างคาอยู่หลังจากงานเสร็จ

```java
// Step 4: Shut down the pool and wait for all tasks to finish
executor.shutdown();
if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
    System.err.println("Some tasks did not finish within the timeout.");
    executor.shutdownNow(); // Force shutdown if needed
}
System.out.println("All HTML files have been cleaned.");
```

หากคุณมีไฟล์จำนวนมากหรือเอกสารขนาดใหญ่ ให้เพิ่มค่า timeout ให้มากขึ้น

---

## Full Working Example

รวมทั้งหมดเข้าด้วยกัน นี่คือโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงใน `ParallelProcessingDemo.java` แล้วรันได้

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelProcessingDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ List the HTML files to be processed
        String[] htmlFiles = {
            "YOUR_DIRECTORY/input1.html",
            "YOUR_DIRECTORY/input2.html",
            "YOUR_DIRECTORY/input3.html",
            "YOUR_DIRECTORY/input4.html"
        };

        // 3️⃣ Submit a cleaning task for each file
        for (String htmlFile : htmlFiles) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(htmlFile)) {
                    // 🌟 Remove all <script> elements (remove script tags)
                    doc.querySelectorAll("script")
                       .forEach(node -> node.getParentNode().removeChild(node));

                    // Save cleaned version
                    doc.save(htmlFile.replace(".html", "_clean.html"));
                } catch (Exception e) {
                    System.err.println("Error processing " + htmlFile + ": " + e.getMessage());
                }
            });
        }

        // 4️⃣ Shut down the pool and wait for completion
        executor.shutdown();
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            System.err.println("Timeout reached before all tasks finished.");
            executor.shutdownNow();
        } else {
            System.out.println("All files cleaned successfully!");
        }
    }
}
```

### Expected Output

เมื่อรันโปรแกรม คุณจะเห็นข้อความในคอนโซลเช่น:

```
All files cleaned successfully!
```

และในโฟลเดอร์ของคุณจะพบไฟล์:

- `input1_clean.html`
- `input2_clean.html`
- `input3_clean.html`
- `input4_clean.html`

แต่ละไฟล์ `_clean.html` จะเหมือนต้นฉบับ ยกเว้นส่วน `<script>` ทั้งหมดที่ถูกลบออก

---

## Frequently Asked Questions (FAQ)

**Q: Can I change the thread pool size at runtime?**  
A: Yes. Use `Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() + 1)` for a dynamic size based on the host machine.

**Q: What if my HTML files contain inline event handlers (`onclick`, `onload`)?**  
A: The current selector only removes `<script>` tags. To strip inline handlers, you’d need to traverse all elements and clear attributes that start with `on`. That’s a good extension for a later tutorial.

**Q: Is Aspose.HTML the only library that supports `querySelectorAll`?**  
A: No. Libraries like jsoup also offer CSS selectors, but Aspose.HTML gives you a full DOM API that mirrors browser behavior, which is handy for complex cleaning tasks.

**Q: How do I handle very large HTML files that might not fit into memory?**  
A: For massive files, consider streaming parsers (e.g., Saxon for XML) or processing the file in chunks. The fixed thread pool pattern still applies; you’d just replace `HTMLDocument` with a streaming solution.

---

## Next Steps & Related Topics

- **Remove JavaScript HTML with jsoup** – ทางเลือกที่เบากว่า หากคุณไม่ต้องการ DOM เต็มรูปแบบ  
- **Dynamic thread pool sizing** – สำรวจ `ThreadPoolExecutor` เพื่อควบคุมอย่างละเอียด  
- **Batch processing with `CompletableFuture`** – ผสาน futures เพื่อสร้าง pipeline ที่ซับซ้อนขึ้น  
- **HTML sanitization beyond scripts** – ลบสไตล์, iframe, หรือแอตทริบิวต์ที่ไม่ปลอดภัย  

ทั้งหมดนี้ต่อเนื่องจากพื้นฐาน **executorservice example java** ที่เราได้วางไว้ในบทนี้

---

## Conclusion

คุณมีตัวอย่างพร้อมใช้งานระดับ production ที่ใช้ **fixed thread pool java** เพื่ **remove script tags** จากชุดไฟล์ HTML จำนวนมากแล้ว ด้วยการใช้ `ExecutorService` แต่ละไฟล์จะถูกประมวลผลแบบขนาน ลดเวลารันโดยรวมอย่างมาก วิธีนี้เป็นโมดูลาร์ ปรับขยายง่าย และทำงานร่วมกับไลบรารี HTML ใด ๆ ที่รองรับการ `load html document`

ลองใช้งาน ปรับขนาด pool หรือเพิ่มกฎการทำความสะอาดเพิ่มเติม—การผจญภัยต่อไปของคุณกับการประมวลผล HTML อยู่แค่ไม่กี่บรรทัดโค้ดเท่านั้น

---

![ภาพประกอบ Fixed thread pool java](https://example.com/fixed-thread-pool-java.png "Fixed thread pool java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}