---
category: general
date: 2026-04-03
description: เรียนรู้วิธีใช้ sandbox ใน Aspose.HTML Java เพื่อกำหนด user agent, กำหนดขนาด,
  และรับขนาด viewport ทันที พร้อมโค้ดเต็ม คำอธิบาย และเคล็ดลับครบถ้วน
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: th
og_description: เรียนรู้วิธีใช้ sandbox ใน Aspose.HTML Java เพื่อกำหนด user agent,
  กำหนดขนาด, และรับขนาด viewport อย่างทันที คู่มือครบถ้วนพร้อมโค้ดและแนวปฏิบัติที่ดีที่สุด
og_title: วิธีใช้ Sandbox – ตั้งค่า User Agent และรับขนาด Viewport
tags:
- AsposeHTML
- Java
- Sandbox
title: วิธีใช้ Sandbox – ตั้งค่า User Agent และรับขนาด Viewport
url: /th/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ Sandbox – ตั้งค่า User Agent & รับขนาด Viewport

เคยสงสัย **วิธีใช้ sandbox** เมื่อต้องเรนเดอร์ HTML ด้วย Aspose.HTML for Java หรือไม่? บางครั้งคุณอาจเจออุปสรรคเมื่อต้องจำลองขนาดหน้าจอเฉพาะหรือจำเป็นต้องปลอมแปลงสตริง user‑agent เพื่อให้หน้าเว็บทำงานเหมือนถูกเยี่ยมชมจากเบราว์เซอร์มือถือ  

ข่าวดีคือ API ของ sandbox ทำให้คุณทำได้เช่นนั้น และคุณยังสามารถดึงขนาด viewport ที่คำนวณได้หลังจากหน้าโหลดเสร็จ ในบทแนะนำนี้เราจะอธิบายการสร้าง sandbox, ตั้งขนาด, ตั้งค่า user agent แบบกำหนดเอง, โหลดหน้าเว็บระยะไกล, และสุดท้ายอ่านขนาด viewport สรุปแล้วคุณจะรู้ **วิธีตั้งขนาด**, **วิธีรับ viewport**, และเหตุผลที่ขั้นตอนเหล่านี้สำคัญสำหรับการเรนเดอร์แบบ headless ที่เชื่อถือได้

> **ชนะอย่างรวดเร็ว:** คุณจะได้คลาส Java ที่สามารถรันได้และพิมพ์ผลลัพธ์เช่น `Viewport: 1280×800` ภายในไม่กี่วินาที

---

## สิ่งที่คุณต้องเตรียม

- **Aspose.HTML for Java** เวอร์ชัน 24.6 หรือใหม่กว่า (API ที่เราใช้ถูกแนะนำตั้งแต่ 24.5)  
- ชุดพัฒนา Java 17+ (JDK ใดก็ได้ที่เป็นรุ่นล่าสุด)  
- IDE หรือเพียงแค่โปรแกรมแก้ไขข้อความ—ไม่ต้องใช้ปลั๊กอินพิเศษ  
- การเชื่อมต่ออินเทอร์เน็ตหากต้องการโหลด URL ภายนอก เช่น `https://example.com`

เท่านี้แค่นั้น ไม่จำเป็นต้องใช้ Maven/Gradle หากคุณต้องการก็สามารถวางไฟล์ JAR ลงใน classpath ด้วยตนเองได้  

---

## วิธีใช้ Sandbox – ภาพรวม

sandbox แยกเอ็นจิ้นการเรนเดอร์ออกจากระบบปฏิบัติการโฮสต์ ทำให้คุณกำหนดหน้าจอเสมือน (ความกว้าง, ความสูง, DPI) และสตริง **user agent** แบบกำหนดเอง คิดว่าเป็นหน้าต่างเบราว์เซอร์ขนาดเล็กที่ทำงานอยู่ในหน่วยความจำเท่านั้น เมื่อคุณเรียก `HTMLDocument` เพื่อขอ view เริ่มต้น เอ็นจิ้นจะรายงาน **viewport size** ที่คำนวณจากการตั้งค่า sandbox  

ขั้นตอนโดยสรุป:

1. **สร้าง** `DocumentSandbox` แล้วกำหนดความกว้าง, ความสูง, DPI, และ user‑agent  
2. **โหลด** `HTMLDocument` ภายใน sandbox นั้น  
3. **สอบถาม** view เริ่มต้นของเอกสารเพื่อรับขนาด viewport  

มาดูรายละเอียดแต่ละขั้นตอนกัน

---

## ขั้นตอนที่ 1: สร้าง Sandbox และตั้งขนาด

แรกเริ่มเราจะสร้าง sandbox แล้วบอกให้มันรู้ว่าหน้าจอเสมือนควรมีขนาดเท่าไหร่ นี่คือการตอบคำถาม **วิธีตั้งขนาด** สำหรับการเรนเดอร์แบบ headless  

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **เคล็ดลับ:** หากคุณกำลังทดสอบเลย์เอาต์แบบ responsive ลองตั้งความกว้างแคบเช่น `360` เพื่อจำลองโทรศัพท์ หรือกว้างเช่น `1920` เพื่อจำลองเดสก์ท็อป sandbox จะเคารพค่า DPI ที่คุณตั้งไว้ ดังนั้นหน้าจอความหนาแน่นสูง (เช่น 144 DPI) จะส่งผลต่อ media‑queries ที่ใช้ `device-pixel-ratio`

---

## ขั้นตอนที่ 2: ตั้ง User Agent สำหรับ Sandbox

ทำไมต้องใช้ **user agent** แบบกำหนดเอง? บางเว็บไซต์จะแสดง markup หรือสคริปต์ที่แตกต่างกันตามเบราว์เซอร์ที่รายงานไว้ โดยการเรียก `setUserAgent` คุณสามารถทำให้หน้าเว็บคิดว่ากำลังถูกเยี่ยมชมจาก Chrome, Firefox หรืออุปกรณ์มือถือ  

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

ตอนนี้หน้าเว็บจะคิดว่ากำลังเรนเดอร์บน iPhone หากคุณต้องการ **ตั้ง user agent** กลับเป็นค่าเริ่มต้น เพียงใช้สตริง “AsposeHTML/24.6 …” เดิมอีกครั้ง

---

## ขั้นตอนที่ 3: โหลด HTML Document ภายใน Sandbox

เมื่อ sandbox พร้อมแล้ว เราสามารถโหลด URL ใดก็ได้หรือไฟล์ HTML ภายในเครื่อง ตัวสร้าง `HTMLDocument` รับ sandbox เป็นอาร์กิวเมนต์ที่สอง ทำให้สองอย่างเชื่อมต่อกัน  

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

บล็อก `try‑with‑resources` จะทำให้เอกสารถูกทำลายอย่างถูกต้อง ปล่อยทรัพยากรเนทีฟที่ Aspose.HTML จัดสรรไว้เบื้องหลัง

---

## ขั้นตอนที่ 4: รับขนาด Viewport จาก Document

นี่คือช่วงเวลาที่คุณรอคอย: ดึง **viewport size** ที่เอ็นจิ้นการเรนเดอร์คำนวณไว้ นี่คือการตอบ **วิธีรับ viewport** หลังจากหน้าเว็บถูกจัดวางแล้ว  

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

เมื่อคุณรันโปรแกรม ควรเห็นผลลัพธ์ประมาณนี้:

```
Viewport: 1280×800
```

หากคุณเปลี่ยนขนาด sandbox ในขั้นตอนที่ 1 ตัวเลขที่พิมพ์ออกมาจะสะท้อนค่าที่ใหม่—เหมาะสำหรับการทดสอบอัตโนมัติที่ตรวจสอบ breakpoint ของ responsive design

---

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นคลาสที่พร้อมรันทั้งหมด คัดลอกและวางลงในไฟล์ชื่อ `SandboxExample.java` เพิ่ม JAR ของ Aspose.HTML ลงใน classpath แล้วสั่ง `java SandboxExample`

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตามการตั้งค่า sandbox ด้านบน):

```
Viewport: 1280×800
```

หากคุณตั้งค่าความกว้าง/ความสูงที่ต่างออกไปใน sandbox ผลลัพธ์ก็จะเปลี่ยนตาม—เป็นสิ่งที่คุณต้องการเมื่อทดสอบการออกแบบแบบ responsive

---

## กรณีขอบและคำถามที่พบบ่อย

### ถ้าหน้าเว็บใช้ `window.innerWidth` แทนการใช้ CSS media queries จะเป็นอย่างไร?

ขนาดหน้าจอเสมือนของ sandbox มีผลต่อทั้งการจัดวาง CSS และค่า `window.innerWidth/innerHeight` ของ JavaScript ดังนั้น **วิธีรับ viewport** ผ่าน JavaScript จะให้ค่าที่ตรงกับที่คุณเห็นในคอนโซล Java

### ฉันสามารถรันหลาย sandbox พร้อมกันได้หรือไม่?

ได้ ทุกอินสแตนซ์ของ `DocumentSandbox` ทำงานแยกจากกัน คุณจึงสามารถสร้าง thread pool ให้แต่ละเธรดมี sandbox ของตนเองพร้อมขนาดต่างกันและเรนเดอร์หลายหน้าได้พร้อมกัน เพียงแค่ตรวจสอบให้แน่ใจว่า JAR ของคุณรองรับการทำงานแบบหลายเธรด (ซึ่งรองรับอยู่แล้ว)

### การตั้งค่า DPI มีผลต่อการสเกลภาพหรือไม่?

มีผลอย่างแน่นอน DPI ที่สูงทำให้หนึ่ง CSS pixel แปลงเป็นหลาย device pixel ซึ่งทำให้ภาพความละเอียดสูงดูคมชัดยิ่งขึ้น หากคุณกำลังทดสอบ assets แบบ retina ให้ลอง `sandbox.setDeviceDpi(144)`

### จะจัดการกับใบรับรอง HTTPS ที่เป็น self‑signed อย่างไร

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}