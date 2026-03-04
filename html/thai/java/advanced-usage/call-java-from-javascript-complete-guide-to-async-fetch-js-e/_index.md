---
category: general
date: 2026-03-04
description: เรียก Java จาก JavaScript ด้วย Aspose.HTML, รัน JavaScript แบบอะซิงโครนัส,
  และดึง JSON ใน Java ด้วยตัวอย่างง่าย ๆ. เรียนรู้การทำงานของเอนจิน JavaScript อย่างมีประสิทธิภาพ.
draft: false
keywords:
- call java from javascript
- run async javascript
- fetch json in java
- asynchronous fetch api
- execute javascript engine
language: th
og_description: เรียกใช้ Java จาก JavaScript ด้วย Aspose.HTML, รัน JavaScript แบบอะซิงโครนัส,
  และดึง JSON ใน Java. มีโค้ดเต็ม, คำอธิบาย, และเคล็ดลับรวมอยู่ด้วย.
og_title: เรียก Java จาก JavaScript – บทเรียนการดึงข้อมูลแบบอะซิงโครนัสแบบขั้นตอนต่อขั้นตอน
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: เรียกใช้ Java จาก JavaScript – คู่มือฉบับสมบูรณ์สำหรับการดึงข้อมูลแบบอะซิงค์และการทำงานของเครื่องยนต์
  JS
url: /th/java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เรียก Java จาก JavaScript – บทเรียนเต็มพร้อม Async Fetch API

เคยสงสัยไหมว่า **call Java from JavaScript** โดยไม่ต้องออกจากแอปพลิเคชัน Java ของคุณ? บางทีคุณอาจกำลังสร้างตัวเรนเดอร์ HTML ฝั่งเซิร์ฟเวอร์, หรือคุณต้องการเปิดเผยตรรกะ Java บางส่วนให้สคริปต์ที่ทำงานภายในเอกสารเข้าถึงได้. ข่าวดีคือ Aspose.HTML ทำให้เรื่องนี้ง่ายเหมือนเค้ก. ในคู่มือนี้เราจะไม่เพียงแสดงวิธี *run async JavaScript* ภายในเอกสารที่สนับสนุน Java, แต่ยังสอนวิธี **fetch JSON in Java** ด้วย **asynchronous fetch API** สมัยใหม่และสุดท้ายการเรียก **execute JavaScript engine** อย่างปลอดภัย.

สรุปแล้ว คุณจะได้ตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งดึง payload JSON จาก endpoint สาธารณะ, ส่งต่อให้กับอ็อบเจ็กต์โฮสต์ Java, และพิมพ์ผลลัพธ์บนคอนโซล. ไม่ต้องใช้เว็บเซิร์ฟเวอร์ภายนอก, ไม่ต้องใช้ไลบรารีเพิ่มเติม—เพียงแค่ Java แท้และ Aspose.HTML.

## สิ่งที่คุณจะได้เรียนรู้

- วิธีสร้างเอกสาร HTML ว่างด้วย Aspose.HTML.
- วิธีรับและ **execute JavaScript engine** จาก Java.
- วิธีลงทะเบียนอ็อบเจ็กต์โฮสต์ Java ที่ JavaScript สามารถเรียกใช้ได้.
- วิธีเขียนฟังก์ชัน **asynchronous JavaScript** ที่ใช้ **asynchronous fetch API**.
- วิธีจัดการข้อมูลที่ดึงมาใน Java ด้วย callback ที่เรียบง่าย.
- ผลลัพธ์ที่คาดหวังและเคล็ดลับการแก้ไขปัญหา.

### ข้อกำหนดเบื้องต้น

- Java 17 หรือใหม่กว่า (โค้ดนี้ยังคอมไพล์ได้กับ JDK 11 ด้วย).
- Aspose.HTML for Java 23.7 (หรือเวอร์ชันล่าสุดในขณะเขียน).
- ความคุ้นเคยพื้นฐานกับ Java และ promises ของ JavaScript.
- การเข้าถึงอินเทอร์เน็ตสำหรับการร้องขอ `jsonplaceholder` ตัวอย่าง.

หากสิ่งใดดูแปลกใหม่ อย่าตื่นตระหนก—แต่ละขั้นตอนอธิบายเป็นภาษาอังกฤษแบบง่าย ๆ และคุณจะเห็นเหตุผลที่เราทำเช่นนั้นอย่างชัดเจน.

---

## ขั้นตอนที่ 1 – สร้างเอกสาร HTML ว่างและดึง JavaScript Engine ของมัน

สิ่งแรกที่เราต้องการคือเอกสารเปล่าที่ให้สภาพแวดล้อม JavaScript แบบ sandboxed. คลาส `Document` ของ Aspose.HTML ทำเช่นนั้นได้อย่างแม่นยำ.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Create an empty HTML document
        Document document = new Document();

        // Obtain the JavaScript engine associated with the document's window
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();
```

**ทำไมเรื่องนี้ถึงสำคัญ:** อ็อบเจ็กต์ `Document` จำลองหน้าต่างเบราว์เซอร์, และ `JavaScriptEngine` ของมันทำให้เรารันสคริปต์ได้เหมือนเบราว์เซอร์จริง. นี่คือพื้นฐานสำหรับ **call java from javascript**—engine ทำหน้าที่เป็นสะพาน.

---

## ขั้นตอนที่ 2 – ลงทะเบียนอ็อบเจ็กต์โฮสต์เพื่อให้ JavaScript สามารถเรียกกลับไปยัง Java

Aspose.HTML อนุญาตให้คุณเปิดเผยอ็อบเจ็กต์ Java ใด ๆ ให้กับสคริปต์. เราจะสร้างคลาสนิรนามที่มีเมธอด `onResult` เพียงหนึ่งเดียวซึ่งพิมพ์ JSON ที่ได้รับออกมา.

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**คำอธิบาย:**  
- `addHostObject` ผูกชื่อ `javaCallback` กับอ็อบเจ็กต์ Java นิรนาม.  
- ภายใน JavaScript เราจะเรียก `javaCallback.onResult(...)`.  
- นี่คือหัวใจของ **call java from javascript**—สคริปต์เข้าถึง Java, และ Java ตอบสนอง.

> **เคล็ดลับ:** ให้เมธอดของอ็อบเจ็กต์โฮสต์เป็น `public` และเรียบง่าย; อ็อบเจ็กต์ที่ซับซ้อนอาจทำให้เกิดปัญหาในการทำ serialization.

---

## ขั้นตอนที่ 3 – เขียนฟังก์ชัน JavaScript แบบอะซิงโครนัสโดยใช้ Asynchronous Fetch API

ต่อไปคือส่วนที่สนุก: สคริปต์เล็ก ๆ ที่ดึง JSON จาก endpoint ระยะไกล. เราจะใช้ `async/await`, ซึ่งเป็นวิธีสมัยใหม่ในการ **run async JavaScript**.

```java
        // Asynchronous script that fetches JSON and passes it to the Java host object
        String asyncScript =
            "async function fetchData() {" +
            "  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "  const json = await response.json();" +
            "  javaCallback.onResult(JSON.stringify(json));" +
            "}" +
            "fetchData();";
```

**ทำไมเราเลือก `fetch` แทน XHR เก่า:**  
- `fetch` คืนค่า `Promise` ทำให้โค้ดสะอาดขึ้น.  
- ทำงานร่วมกับ `await` อย่างเนทีฟ, ทำให้ลำดับการทำงานอ่านจากบนลงล่าง—เหมาะสำหรับการสาธิต **asynchronous fetch api**.  
- API นี้พร้อมสำหรับอนาคต; เบราว์เซอร์และเอนจินส่วนใหญ่ (รวมถึงของ Aspose) รองรับโดยไม่ต้องตั้งค่าเพิ่มเติม.

---

## ขั้นตอนที่ 4 – รันสคริปต์ภายใน JavaScript Engine ของ Document

สุดท้าย เราให้สคริปต์กับ engine. engine จะสร้าง event loop เล็ก ๆ, แก้ไข `fetch` promise, และเรียกกลับไปยัง Java เมื่อเสร็จ.

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

เมื่อคุณรันคลาส `AsyncJsTutorial`, คุณควรเห็นผลลัพธ์ประมาณนี้:

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

ผลลัพธ์นั้นยืนยันสามสิ่ง:  

1. **asynchronous fetch API** ดึงข้อมูลสำเร็จ.  
2. JSON ถูก serialize และส่งต่อให้ Java.  
3. การเรียก **execute javascript engine** ของเราสำเร็จโดยไม่มี deadlock.

---

## ขั้นตอนที่ 5 – การจัดการข้อผิดพลาดและกรณีขอบ (การปรับปรุงเพิ่มเติม)

โค้ดในโลกจริงมักไม่ทำงานสมบูรณ์ทุกครั้ง. ด้านล่างเป็นข้อผิดพลาดทั่วไปบางประการและวิธีป้องกัน.

### 5.1 ความล้มเหลวของเครือข่าย

หากเซิร์ฟเวอร์ระยะไกลหยุดทำงาน, `fetch` จะโยนข้อยกเว้น. ให้ห่อการเรียกในบล็อก `try/catch`:

```java
String asyncScript =
    "async function fetchData() {" +
    "  try {" +
    "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
    "    if (!response.ok) throw new Error('Network response was not ok');" +
    "    const json = await response.json();" +
    "    javaCallback.onResult(JSON.stringify(json));" +
    "  } catch (e) {" +
    "    javaCallback.onResult('Error: ' + e.message);" +
    "  }" +
    "}" +
    "fetchData();";
```

ตอนนี้ฝั่ง Java จะได้รับข้อความข้อผิดพลาดแทนการค้าง.

### 5.2 เวลาหมด (Timeouts)

Engine ของ Aspose ไม่ได้เปิดเผย timeout เนทีฟสำหรับ `fetch`, แต่คุณสามารถทำเองใน JavaScript:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 การเรียกหลายครั้ง

หากต้องการดึงหลายทรัพยากร, เพียงวนลูปหรือ map ผ่านอาร์เรย์ของ URL. อ็อบเจ็กต์โฮสต์สามารถขยายให้รับตัวระบุ, เพื่อให้คุณเชื่อมโยงการตอบกลับได้.

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็น **ไฟล์ซอร์สเต็ม** ที่คุณสามารถคัดลอก‑วางลงใน IDE ของคุณ. ไม่มีการพึ่งพาที่ซ่อนอยู่, เพียงแค่ Aspose.HTML JAR บน classpath.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty HTML document and obtain its JavaScript engine
        Document document = new Document();
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();

        // Step 2: Register a host object that JavaScript can call back into Java
        jsEngine.addHostObject("javaCallback", new Object() {
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });

        // Step 3: Write an async function that uses the asynchronous fetch API
        String asyncScript =
            "async function fetchData() {" +
            "  try {" +
            "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "    if (!response.ok) throw new Error('Network error');" +
            "    const json = await response.json();" +
            "    javaCallback.onResult(JSON.stringify(json));" +
            "  } catch (e) {" +
            "    javaCallback.onResult('Error: ' + e.message);" +
            "  }" +
            "}" +
            "fetchData();";

        // Step 4: Execute the script inside the document's JavaScript engine
        jsEngine.execute(asyncScript);
    }
}
```

**ผลลัพธ์ที่คาดหวังบนคอนโซล**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

หากคุณเห็นบรรทัดข้อผิดพลาดที่เริ่มด้วย `Error:` แสดงว่ามีบางอย่างผิดพลาด—อาจเป็นการขัดข้องของเครือข่าย.

---

## ภาพรวมเชิงภาพ

![แผนภาพแสดงวิธีที่ Java เรียก JavaScript และรับผลลัพธ์จาก async fetch – call java from javascript](/images/java-js-async.png)

*ภาพแสดงกระบวนการ: Java → JavaScriptEngine → async fetch → JavaCallback.*

---

## คำถามที่พบบ่อย

**ฉันสามารถใช้วิธีนี้กับเอนจิน JavaScript อื่นได้หรือไม่?**  
ได้, เอนจินใด ๆ ที่เปิดเผยกลไก host object (เช่น Nashorn, GraalVM) สามารถทำงานได้, แต่ Aspose.HTML ให้สภาพแวดล้อมแบบเบราว์เซอร์ที่ครบถ้วนพร้อม `fetch` ในตัว.

**ถ้าฉันต้องการส่งคืนอ็อบเจ็กต์ Java ที่ซับซ้อนแทนสตริงจะทำอย่างไร?**  
คุณสามารถ serialize อ็อบเจ็กต์เป็น JSON ฝั่ง Java แล้วให้ JavaScript แปลง, หรือคุณสามารถเปิดเผยหลายเมธอดบนอ็อบเจ็กต์โฮสต์เพื่อรับฟิลด์แยกต่างหาก.

**การทำงานของ `fetch` เป็นไปตามมาตรฐานหรือไม่?**  
Aspose.HTML ปฏิบัติตาม WHATWG Fetch Standard, ดังนั้นคุณจะได้การจัดการการเปลี่ยนเส้นทาง, CORS, และการสตรีมอย่างถูกต้อง.

**การทำงานนี้บล็อกเธรด Java ขณะรอเครือข่ายหรือไม่?**  
ไม่. การเรียก `execute` จะคืนค่าทันที, และเอนจินภายในจะประมวลผล promise อย่างอะซิงโครนัส. อย่างไรก็ตาม เธรดหลักจะคงอยู่จนกว่าสคริปต์จะเสร็จหรือคุณปิดเอนจินอย่างชัดเจน.

---

## สรุป

เราพึ่งได้อธิบายสถานการณ์เชิงปฏิบัติที่ทำให้คุณ **call Java from JavaScript**, **run async JavaScript**, และ **fetch JSON in Java** ด้วย **asynchronous fetch API**. ด้วยการสร้างอ็อบเจ็กต์โฮสต์, เขียนฟังก์ชัน `async` ที่เรียบร้อย, และรันมันด้วย **JavaScript engine** ของ Aspose.HTML, คุณจะได้สะพานที่สะอาดและไม่บล็อกระหว่างสองรันไทม์.

ลองใช้งาน, ปรับ URL, หรือเพิ่ม callback เพิ่มเติม—จินตนาการของคุณคือขีดจำกัด. ขั้นต่อไปคุณอาจสำรวจ:

- **Executing JavaScript engine** กับสคริปต์หลายตัวพร้อมกัน.  
- ใช้ **run async javascript** เพื่อประมวลผลชุดข้อมูลขนาดใหญ่แบบขนาน.  
- ผสานรูปแบบนี้เข้ากับเว็บ‑เซอร์วิสที่เรนเดอร์ HTML แบบไดนามิกแบบเรียลไทม์.

อย่าลังเลที่จะทดลอง, และหากเจออุปสรรคที่ไม่คาดคิด อย่ากลัวที่จะฝากคอมเมนต์. ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}