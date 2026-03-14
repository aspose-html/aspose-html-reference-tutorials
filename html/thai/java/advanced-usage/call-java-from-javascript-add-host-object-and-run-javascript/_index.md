---
category: general
date: 2026-03-14
description: เรียนรู้วิธีเรียกใช้ Java จาก JavaScript ด้วย Aspose.HTML คู่มือนี้จะแสดงวิธีเพิ่มอ็อบเจ็กต์โฮสต์,
  รัน JavaScript ใน Java, และบันทึกจาก JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: th
og_description: เรียก Java จาก JavaScript ด้วย Aspose.HTML เพิ่มอ็อบเจ็กต์โฮสต์ รัน
  JavaScript ใน Java และบันทึกจาก JavaScript ในบทเรียนเดียว
og_title: เรียกใช้ Java จาก JavaScript – คู่มือฉบับสมบูรณ์กับอ็อบเจ็กต์โฮสต์
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: เรียก Java จาก JavaScript – เพิ่ม Host Object และรัน JavaScript ใน Java
url: /th/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เรียก Java จาก JavaScript – เพิ่ม Host Object และรัน JavaScript ใน Java

เคยต้องการ **เรียก Java จาก JavaScript** ภายในแอปพลิเคชัน Java หรือไม่? บางทีคุณอาจกำลังสร้างเครื่องมือรายงาน HTML แบบไดนามิก หรือเพียงต้องการเปิดให้สคริปต์ที่คุณควบคุมเข้าถึง Java logger. ในบทแนะนำนี้คุณจะได้เห็นวิธีเพิ่ม host object, รัน JavaScript ใน Java, และแม้กระทั่ง **บันทึกจาก JavaScript** กลับไปยัง JVM—ทั้งหมดด้วย Aspose.HTML.

เราจะเดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งสร้างเอกสาร HTML ว่างเปล่า, แทรกคลาส Java `Logger` เป็น host object, รันสคริปต์เล็ก ๆ, และพิมพ์ผลลัพธ์ไปยังคอนโซล. ไม่ต้องใช้เว็บเบราว์เซอร์ภายนอก, ไม่ต้องมี “เวทมนตร์”—เพียงโค้ด Java ธรรมดาที่คุณสามารถคัดลอก‑วางและรันได้ทันที

## ข้อกำหนดเบื้องต้น

- Java 17 (หรือ JDK ล่าสุดใดก็ได้) ที่ติดตั้งและกำหนดค่าแล้ว
- ไลบรารี Aspose.HTML สำหรับ Java (เวอร์ชัน 23.10 หรือใหม่กว่า) คุณสามารถดาวน์โหลดได้จาก Maven Central หรือเว็บไซต์ Aspose
- IDE หรือโปรแกรมแก้ไขข้อความง่าย ๆ; ตัวอย่างทำงานได้จากบรรทัดคำสั่งเช่นกัน

> **เคล็ดลับ:** หากคุณใช้ Maven ให้เพิ่ม dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

หรือสำหรับ Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

ตอนนี้เมื่อเราได้จัดการพื้นฐานแล้ว, มาเริ่มลงลึกในวิธีแก้ปัญหาแบบขั้นตอนต่อขั้นตอนกัน

## ขั้นตอนที่ 1: สร้างโครงการ Java ขั้นต่ำ

แรกเริ่ม, สร้างคลาส Java ใหม่ชื่อ `JsHostObjectDemo`. คลาสนี้จะบรรจุเมธอด `main` ของเราและการกำหนด host object. การเก็บทุกอย่างไว้ในไฟล์เดียวทำให้บทแนะนำเป็นอิสระและง่ายต่อการคัดลอก

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### ทำไมต้องใช้ `HTMLDocument`?

คลาส `HTMLDocument` ของ Aspose.HTML จะสร้างสภาพแวดล้อมการสคริปต์ที่สอดคล้องกับ HTML‑5 อย่างเต็มรูปแบบ. แม้ว่าเราจะไม่โหลด markup ใด ๆ, วัตถุ `window` ของเอกสารให้เราเข้าถึงเครื่องยนต์ JavaScript, ซึ่งเป็นที่ที่เกิด **การรัน JavaScript ใน Java** อย่างมหัศจรรย์

## ขั้นตอนที่ 2: เพิ่ม Host Object – “javaLogger”

บรรทัด

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

ทำหน้าที่หลักสำหรับความต้องการ **เพิ่ม host object**. โดยการลงทะเบียนอินสแตนซ์ `Logger` ภายใต้ชื่อ `"javaLogger"`, สคริปต์ใด ๆ ที่ประเมินในเอกสารนี้สามารถเรียก `javaLogger.log(...)`. นี่คือแกนหลักของแนวคิด **javascript host object**: สะพานที่ทำให้ JavaScript เข้าถึง JVM

### ข้อผิดพลาดทั่วไป

- **การชนชื่อ** – หากคุณมีตัวแปรระดับ global ชื่อ `javaLogger` อยู่แล้วในสคริปต์, host object จะถูกเขียนทับ. เลือกชื่อที่ไม่ซ้ำกัน.
- **ความปลอดภัยของเธรด** – host object ถูกแชร์ระหว่างการรันสคริปต์บนเอกสารเดียวกัน. หากคุณวางแผนรันสคริปต์พร้อมกัน, ทำให้คลาส host มีความปลอดภัยต่อเธรด (เช่น ใช้ `synchronized` หรือ primitive ของ `java.util.concurrent`)

## ขั้นตอนที่ 3: เขียนและรัน JavaScript

สคริปต์ที่เราป้อนเข้า `eval` มีขนาดเล็กโดยเจตนา:

```javascript
javaLogger.log('Hello from JavaScript!');
```

เมื่อ `document.getWindow().eval(script)` ทำงาน, เอนจินจะค้นหา `javaLogger` ในสโคประดับ global, พบอ็อบเจ็กต์ Java ที่เราเพิ่ม, และเรียกเมธอด `log` ของมันด้วยสตริงที่ให้มา.

### ผลลัพธ์ที่คาดหวัง

การรันเมธอด `main` จะพิมพ์บรรทัดต่อไปนี้ไปยังคอนโซล:

```
[JS] Hello from JavaScript!
```

บรรทัดเล็ก ๆ นั้นพิสูจน์ว่าเราสามารถ **เรียก java จาก javascript** ได้สำเร็จ, และ **การบันทึกจาก javascript** ปรากฏตรงที่ข้อความ `System.out` ของ Java ปกติจะอยู่.

## ขั้นตอนที่ 4: ขยาย Host – มากกว่าการบันทึก

หากคุณต้องการเปิดเผยฟังก์ชันเพิ่มเติม (เช่น การเข้าถึงไฟล์, คำสั่งฐานข้อมูล), เพียงเพิ่มเมธอดในคลาส `Logger`—หรือสร้างคลาส host ใหม่. นี่คือตัวอย่างสั้น ๆ ที่ยังคืนค่า:

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

ตอนนี้คอนโซลจะแสดง:

```
[JS] 3+4=7
```

สิ่งนี้แสดงถึงความยืดหยุ่นของรูปแบบ **javascript host object**: คุณสามารถเปิดเผย API ของ Java ใดก็ได้ที่ต้องการ, ตราบใดที่ชนิดข้อมูลสามารถแปลงระหว่าง Java และ JavaScript (primitive, string, array ฯลฯ).

## ขั้นตอนที่ 5: ทำความสะอาดทรัพยากร

เมื่อคุณเสร็จสิ้นการใช้สภาพแวดล้อมสคริปต์, ทำการ dispose `HTMLDocument` เพื่อปล่อยทรัพยากรเนทีฟ:

```java
document.dispose(); // Important for long‑running applications
```

การละเลยการทำ disposal อาจทำให้เกิด memory leak, โดยเฉพาะหากคุณสร้างเอกสารหลาย ๆ ฉบับในลูป.

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นไฟล์ซอร์สเต็มรูปแบบที่คุณสามารถคอมไพล์และรันได้ทันที. บันทึกเป็น `JsHostObjectDemo.java`, ตรวจสอบให้แน่ใจว่า JAR ของ Aspose.HTML อยู่ใน classpath, แล้วรัน `java JsHostObjectDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

การรันโปรแกรมนี้จะได้ผลลัพธ์:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

นี่คือขั้นตอนทั้งหมดของ **call java from javascript** ในไม่กี่บรรทัด.

## คำถามที่พบบ่อย

### ทำงานบน Android หรือไม่?

Aspose.HTML เป็นไลบรารี pure‑Java, ดังนั้นมันทำงานบน JVM ใดก็ได้, รวมถึง Dalvik/ART ของ Android. เพียงบรรจุ JAR แล้วคุณจะมีความสามารถของ host‑object เหมือนเดิม.

### ถ้าต้องการส่งอ็อบเจ็กต์ที่ซับซ้อนล่ะ?

คุณสามารถเปิดเผย POJO (plain old Java objects) ที่มีฟิลด์, getter, และ setter. เอนจินจะแมปพวกมันเป็นอ็อบเจ็กต์ JavaScript โดยอัตโนมัติ. สำหรับคอลเลกชัน, ใช้ `java.util.List` หรืออาร์เรย์—ทั้งสองสามารถแปลงได้.

### การจัดการข้อผิดพลาดทำงานอย่างไร?

หากสคริปต์โยนข้อผิดพลาด JavaScript, `eval` จะส่งต่อ `ScriptException`. ห่อการเรียกในบล็อก try‑catch เพื่อบันทึกหรือกู้คืน:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### สามารถรันหลายสคริปต์ต่อเนื่องกันได้หรือไม่?

ได้เลย. อินสแตนซ์ `HTMLDocument` เดียวกันจะรักษา global scope, ดังนั้นคุณสามารถเรียก `eval` ซ้ำได้. เพียงระวังการชนชื่อของตัวแปรระหว่างสคริปต์.

## แนวทางปฏิบัติที่ดีที่สุด & เคล็ดลับ

- **ตั้งชื่อ host object อย่างชัดเจน**—`javaLogger`, `javaUtils` ฯลฯ—เพื่อหลีกเลี่ยงความสับสน.
- **ทำให้เมธอดของ host มีขนาดเล็กและไม่มี side‑effect** เมื่อเป็นไปได้; จะทำให้การดีบักง่ายขึ้น.
- **Dispose เอกสาร** ทันทีที่เสร็จ; จะปล่อยหน่วยความจำเนทีฟที่ Aspose.HTML จัดสรร.
- **ตรวจสอบความถูกต้องของอินพุต** จาก JavaScript, โดยเฉพาะหากสคริปต์มาจากแหล่งที่ไม่เชื่อถือ. ปฏิบัติเช่นเดียวกับข้อมูลภายนอกใด ๆ.

## สรุป

ตอนนี้คุณมีตัวอย่างครบวงจรว่าต้อง **เรียก java จาก javascript** อย่างไรโดย **เพิ่ม host object**, **รัน JavaScript ใน Java**, และ **บันทึกจาก JavaScript** ด้วย Aspose.HTML. รูปแบบนี้มีพลัง: บริการ Java ใด ๆ ก็สามารถเปิดเผยให้สคริปต์ใช้ได้, ทำให้แอปพลิเคชัน Java ของคุณกลายเป็นแพลตฟอร์มสคริปต์แบบเบา.

ต่อไป, คุณอาจสำรวจ:

- การแทรกหน้า HTML เต็มรูปแบบและจัดการ DOM จาก JavaScript.
- การใช้ host object เพื่อสตรีมข้อมูลกลับไปยังฝั่ง Java (เช่น การทำ JSON serialization).
- การรวมกับเอนจินสคริปต์อื่น ๆ เช่น Nashorn หรือ GraalVM เพื่อรองรับภาษาที่หลากหลายขึ้น.

ลองทำดู, ปรับแต่งคลาส `Logger` หรือ `Utils`, และดูว่าคุณสามารถผลักดันแนวคิด **javascript host object** ไปไกลแค่ไหนในโครงการของคุณ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}