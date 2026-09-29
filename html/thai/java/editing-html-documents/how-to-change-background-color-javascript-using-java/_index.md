---
category: general
date: 2026-09-29
description: เปลี่ยนสีพื้นหลังด้วย JavaScript ในไฟล์ HTML โดยใช้ Java. เรียนรู้วิธีโหลด
  HTML ใน Java, รัน JavaScript ใน HTML, และแก้ไข HTML ด้วย Java เพื่อเปลี่ยนพื้นหลังของหน้าใหม่.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: th
lastmod: 2026-09-29
og_description: เปลี่ยนสีพื้นหลังด้วย JavaScript ในหน้า HTML โดยใช้ Java บทเรียนนี้จะแสดงวิธีโหลด
  HTML ใน Java, รัน JavaScript ใน HTML, และตั้งค่าสีพื้นหลังของหน้าโดยโปรแกรม
og_image_alt: Screenshot of Java code that changes the page background color
og_title: เปลี่ยนสีพื้นหลังด้วย JavaScript และ Java – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: วิธีเปลี่ยนสีพื้นหลังด้วย JavaScript โดยใช้ Java
url: /th/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปลี่ยนสีพื้นหลังด้วย JavaScript โดยใช้ Java

หากคุณต้องการ **change background color javascript** ในไฟล์ HTML ที่มีอยู่ คุณสามารถทำได้ทั้งหมดจาก Java โดยไม่ต้องเปิดเบราว์เซอร์ tutorial นี้จะแสดงวิธี **load html in java**, รันส่วนย่อย JavaScript เล็ก ๆ แล้ว **modify html with java** เพื่อให้พื้นหลังของหน้าได้รับการอัปเดต  

โซลูชันนี้ทำงานร่วมกับไลบรารี **HTMLUnit** แบบโอเพ่นซอร์ส ซึ่งให้เบราว์เซอร์แบบ headless ที่สามารถประเมิน JavaScript ได้เหมือนกับเบราว์เซอร์จริง ๆ ในตอนท้ายของคู่มือนี้ คุณจะมีเมธอดที่สามารถนำกลับมาใช้ใหม่ได้ซึ่ง **sets page background** เป็นสีใดก็ได้ที่คุณเลือก

## ข้อกำหนดเบื้องต้น

| สิ่งที่ต้องการ | เหตุผล |
|---------------|--------|
| Java 8 หรือใหม่กว่า | HTMLUnit ต้องการอย่างน้อย Java 8. |
| เครื่องมือสร้าง Maven หรือ Gradle | เพื่อดึง dependencies ของ HTMLUnit อัตโนมัติ. |
| ไฟล์ HTML ที่คุณต้องการแก้ไข (เช่น `input.html`) | เอกสารต้นฉบับที่จะถูกโหลดและแก้ไข. |

เพิ่ม HTMLUnit ไปยังโปรเจกต์ของคุณ:

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **Pro tip:** ใช้เวอร์ชันเสถียรล่าสุดของ HTMLUnit เพื่อให้ได้เอ็นจิ้น JavaScript ที่แม่นยำที่สุด.

## Change background color javascript – โหลด HTML ใน Java

ขั้นตอนแรกคือการโหลดเอกสาร HTML ไปยังอ็อบเจ็กต์ `HTMLPage` ซึ่งจะให้ API คล้าย DOM และบริบทการรัน JavaScript.

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*Why this matters*: `WebClient` สร้างสภาพแวดล้อมแบบ sandbox ที่ JavaScript สามารถทำงานได้ ดังนั้นคุณสามารถ **run js in html** ได้เหมือนกับเบราว์เซอร์ของผู้ใช้.

## Run js in html เพื่อกำหนดพื้นหลังของหน้า

เมื่อหน้าโหลดแล้ว คุณสามารถประเมินค่า JavaScript ใดก็ได้ ส่วนย่อยด้านล่างจะเปลี่ยนสไตล์ `backgroundColor` ขององค์ประกอบ `<body>`.

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*คำอธิบาย*:
- `document.body.style.backgroundColor` เป็นคุณสมบัติ DOM มาตรฐานสำหรับพื้นหลังของหน้า.
- โดยการเรียก `eval` เรา **run js in html** โดยไม่ต้องมีหน้าต่างเบราว์เซอร์จริง.
- เมธอดนี้สามารถนำกลับมาใช้ใหม่ได้สำหรับสีใดก็ได้ ตอบสนองความต้องการ **set page background**.

## Modify html with java และบันทึกผลลัพธ์

หลังจากสคริปต์ทำงาน DOM จะสะท้อนสไตล์ใหม่ คุณสามารถเขียน HTML ที่อัปเดตกลับไปยังดิสก์ได้แล้ว.

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

การรวมทุกอย่างเข้าด้วยกันจะให้โปรแกรมเดียวที่สามารถรันได้:

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะพิมพ์:

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

การเปิด `js_modified.html` ในเบราว์เซอร์ใดก็จะเห็นหน้าที่มีพื้นหลังสีฟ้าอ่อน ยืนยันว่าการดำเนินการ **change background color javascript** สำเร็จ.

## ความแปรผันทั่วไปและกรณีขอบ

| สถานการณ์ | วิธีจัดการ |
|-----------|------------|
| **รูปแบบสีที่แตกต่าง** | ส่งค่าที่เข้ากันได้กับ CSS ใดก็ได้ (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`). |
| **Missing `<body>` tag** | สคริปต์จะล้มเหลวโดยไม่มีการแจ้งเตือน; คุณสามารถตรวจสอบให้แน่ใจว่า `<body>` มีอยู่ก่อนด้วย `page.getFirstByXPath("//body")`. |
| **Large HTML files** | ปิดการทำงานของ CSS (`setCssEnabled(false)`) และเปิดเฉพาะฟีเจอร์ JavaScript ที่จำเป็นเพื่อประหยัดหน่วยความจำ. |
| **Running multiple scripts** | เรียก `changeBackground` หลายครั้งหรือสร้างเมธอดยูทิลิตี้ที่รับรายการคำสั่ง JavaScript. |

## สรุป

ตอนนี้คุณรู้วิธี **change background color javascript** โดยการโหลดไฟล์ HTML ใน Java, **run js in html**, และ **modify html with java** เพื่อ **set page background** เป็นสีใดก็ได้ที่คุณเลือก ตัวอย่างเต็มที่แสดงด้านบนทำงานกับไลบรารี HTMLUnit ล่าสุดและสามารถนำไปผสานกับ pipeline การทำอัตโนมัติขนาดใหญ่ เช่น การประมวลผลเป็นชุดของรายงาน HTML หรือการเตรียมเทมเพลตอีเมล.

**Next steps**  
- สำรวจการจัดการ DOM อื่น ๆ (เช่น การแทรกองค์ประกอบ, การลบสคริปต์).  
- ผสานวิธีนี้กับเครื่องมือแปลง PDF เพื่อสร้าง PDF ของหน้าที่มีสไตล์.  
- ลองใช้เอนจิน headless ตัวอื่นเช่น Selenium WebDriver หากคุณต้องการความแม่นยำของเบราว์เซอร์เต็มรูปแบบ.

ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลรวมตัวอย่างโค้ดที่ทำงานได้สมบูรณ์พร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบอื่นในโปรเจกต์ของคุณ.

- [รับสไตล์ที่คำนวณแล้วใน Java – ดึงสีพื้นหลังจาก HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [วิธีโหลด HTML, ตั้งค่า DPI ของอุปกรณ์ & อ่านสีพื้นหลัง](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [สร้าง HTML จาก JavaScript ใน Java – คู่มือขั้นตอนเต็ม](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}