---
category: general
date: 2026-10-28
description: เรียนรู้วิธีเปิดลิงก์ในแท็บใหม่โดยการแยกวิเคราะห์ HTML ด้วย Java ค้นหาลิงก์ภายนอกและเพิ่ม
  target="_blank
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: th
lastmod: 2026-10-28
og_description: 'เปิดลิงก์ในแท็บใหม่โดยใช้ Java: แยกวิเคราะห์ HTML, ค้นหาลิงก์ภายนอก,
  เพิ่ม target blank, และบันทึก HTML ที่แก้ไขแล้ว.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: เปิดลิงก์ในแท็บใหม่ด้วย Java – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: วิธีเปิดลิงก์ในแท็บใหม่ด้วย Java
url: /th/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดลิงก์ในแท็บใหม่ด้วย Java

หากคุณต้องการ **เปิดลิงก์ในแท็บใหม่** จากไฟล์ HTML แบบสแตติก คู่มือนี้จะแสดงให้คุณเห็นขั้นตอนอย่างละเอียด คุณจะได้เรียนรู้การ **parse HTML in Java**, **find external links**, **add target blank**, และ **save modified HTML** โดยไม่ต้องออกจาก IDE ของคุณ.  

การเปิดลิงก์ภายนอกในแท็บเบราว์เซอร์ใหม่ช่วยปรับปรุงประสบการณ์ผู้ใช้และทำให้ผู้เยี่ยมชมอยู่บนหน้าเดิม โซลูชันด้านล่างทำงานกับเอกสาร HTML ใดก็ได้ ต้องการเพียงไลบรารี jsoup ที่เป็นที่นิยมและทำงานบน Java 8 หรือใหม่กว่า.

## ความต้องการเบื้องต้น

* ติดตั้ง JDK 8 + แล้ว  
* มีเครื่องมือสร้าง (Maven หรือ Gradle) เพื่อดึง dependency ของ **jsoup**  
* มีไฟล์ HTML ที่มีแท็ก `<a>` พร้อมคลาส `external`

คุณไม่จำเป็นต้องมีเว็บเซิร์ฟเวอร์หรือเฟรมเวิร์กเพิ่มเติม—jsoup จัดการทุกอย่างในเครื่อง

## ขั้นตอนที่ 1: ตั้งค่า jsoup ในโปรเจกต์ของคุณ

เพิ่ม jsoup เป็น dependency หากคุณใช้ Maven ให้ใส่ส่วนนี้ใน `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

สำหรับ Gradle ให้เพิ่มบรรทัดต่อไปนี้ใน `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

พารามิเตอร์เหล่านี้จะดึงเวอร์ชันเสถียรล่าสุด (ณ เดือนตุลาคม 2026) หลังจากซิงค์แล้ว คุณสามารถนำเข้าคลาส `org.jsoup` ในไฟล์ซอร์ส Java ของคุณได้

## ขั้นตอนที่ 2: แยกวิเคราะห์เอกสาร HTML

การแยกวิเคราะห์ไฟล์เป็นขั้นตอนแรกสู่การ **open links new tab** เมธอด `Jsoup.parse` จะอ่านไฟล์เข้าสู่โครงสร้างแบบ DOM ที่สามารถแก้ไขได้

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*ทำไมสิ่งนี้ถึงสำคัญ*: `Document` ให้คุณใช้ตัวเลือกแบบ CSS ทำให้ค้นหาองค์ประกอบที่ต้องการได้อย่างง่ายดาย

## ขั้นตอนที่ 3: ค้นหาลิงก์ภายนอก

ตอนนี้ให้ค้นหาแท็ก `<a>` ทุกตัวที่มีคลาส `external` ซึ่งสอดคล้องกับความต้องการ **find external links**

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` คือคอลเลกชันของโหนดที่ตรงกัน หากตัวเลือกคืนค่าเป็นชุดว่าง HTML ของคุณอาจไม่มีคลาสนี้หรือใช้ชื่อคลาสอื่น—ให้ปรับตัวเลือกให้เหมาะสม

## ขั้นตอนที่ 4: เพิ่ม `target="_blank"` ให้กับลิงก์แต่ละอัน

สำหรับแต่ละโหนดที่ได้จาก **find external links** ให้ตั้งค่าแอตทริบิวต์ `target` เป็น `_blank` สิ่งนี้ทำให้ขั้นตอน **add target blank** เสร็จสมบูรณ์และทำให้เบราว์เซอร์เปิดลิงก์ในแท็บใหม่

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

เมธอด `attr` จะเขียนทับค่า `target` ที่มีอยู่เดิม ทำให้พฤติกรรมของลิงก์ภายนอกทั้งหมดสอดคล้องกัน

## ขั้นตอนที่ 5: บันทึก HTML ที่แก้ไขแล้ว

หลังจากอัปเดต DOM แล้ว ให้เขียนการเปลี่ยนแปลงกลับไปยังไฟล์ ซึ่งเป็นการสรุปส่วน **save modified html** ของบทเรียน

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` จะทำการซีเรียลไลซ์เอกสารทั้งหมดโดยคงรูปแบบการเยื้องและการจัดรูปแบบตามที่ jsoup แยกวิเคราะห์ไว้เดิม

## ตัวอย่างทำงานเต็มรูปแบบ

การรวมทุกขั้นตอนเข้าด้วยกันจะได้โปรแกรมที่ทำงานอิสระซึ่งคุณสามารถคัดลอก วาง และรันได้

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### ผลลัพธ์ที่คาดหวัง

สมมติว่า `sample.html` มีเนื้อหา:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

หลังจากรันโปรแกรม `updated.html` จะมีเนื้อหา:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

เฉพาะลิงก์ภายนอกเท่านั้นที่ได้รับแอตทริบิวต์ `target="_blank"` ซึ่งหมายความว่าเบราว์เซอร์จะเปิดลิงก์นั้นในแท็บใหม่

## เคล็ดลับระดับมืออาชีพและข้อผิดพลาดทั่วไป

* **เคล็ดลับระดับมืออาชีพ:** หากคุณต้องการพิจารณาลิงก์ที่ขึ้นต้นด้วย `http://` หรือ `https://` เป็นลิงก์ภายนอกแม้ไม่มีคลาส CSS ให้ขยายตัวเลือกเป็น: `doc.select("a[href^=http]")`.
* **กรณีขอบ:** บางหน้าอาจกำหนด `target="_self"` ไว้แล้ว; การเรียก `attr` จะเขียนทับค่า ทำให้พฤติกรรมสอดคล้องกัน
* **ประสิทธิภาพ:** สำหรับไฟล์ HTML ขนาดใหญ่มาก ควรพิจารณาใช้การแยกวิเคราะห์แบบสตรีม (`Jsoup.parse(File, String, String, Parser.htmlParser())`) เพื่อลดการใช้หน่วยความจำ
* **การทดสอบ:** ตรวจสอบผลลัพธ์โดยเปิด `updated.html` ในเบราว์เซอร์และตรวจสอบลิงก์ด้วยเครื่องมือพัฒนา—มองหาแอตทริบิวต์ `target`

## สรุป

ตอนนี้คุณมีโซลูชันที่สมบูรณ์และสามารถรันได้เพื่อ **open links in a new tab** ด้วย Java บทเรียนนี้ครอบคลุมวิธี **parse html in java**, **find external links**, **add target blank**, และ **save modified html** ทั้งหมดโดยใช้ไลบรารี jsoup ที่เบา  

จากนี้คุณสามารถ:

* ขยายตัวเลือกเพื่อจัดการรูปแบบลิงก์อื่น ๆ (เช่น `rel="external"`)  
* ผสานตรรกะนี้กับขั้นตอนการสร้างที่ประมวลผลไฟล์ HTML ทั้งหมดในโปรเจกต์  
* รวมโค้ดนี้เข้ากับ pipeline การจัดการเนื้อหาขนาดใหญ่  

คุณสามารถทดลองใช้ตัวเลือกหรือรูปแบบผลลัพธ์ที่ต่างกันได้ตามต้องการ และแบ่งปันผลลัพธ์ของคุณกับชุมชน!

## สิ่งต่อไปที่คุณควรเรียนรู้

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}