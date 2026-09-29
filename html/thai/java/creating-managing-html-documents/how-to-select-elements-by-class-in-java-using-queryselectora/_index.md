---
category: general
date: 2026-09-29
description: เรียนรู้วิธีเลือกองค์ประกอบตามคลาส, อ่าน HTML จากไฟล์, และค้นหาลิงก์ภายนอกใน
  Java. คู่มือขั้นตอนต่อขั้นตอนนี้ครอบคลุมการวนซ้ำ NodeList อย่างมีประสิทธิภาพ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: th
lastmod: 2026-09-29
og_description: เลือกองค์ประกอบตามคลาสใน Java, อ่าน HTML จากไฟล์, และค้นหาลิงก์ภายนอกโดยใช้
  querySelectorAll. ทำตามตัวอย่างเต็มเพื่อวนรอบ NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: เลือกองค์ประกอบตามคลาสใน Java – คู่มือฉบับสมบูรณ์ด้วย querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: วิธีเลือกองค์ประกอบตามคลาสใน Java ด้วย querySelectorAll
url: /th/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเลือกองค์ประกอบโดยคลาสใน Java ด้วย querySelectorAll

หากคุณต้องการ **เลือกองค์ประกอบโดยคลาส** ขณะประมวลผลไฟล์ HTML ด้วย Java คำแนะนำนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าจะทำอย่างไร คุณจะได้เรียนรู้การอ่าน HTML จากไฟล์, ใช้ `querySelectorAll` เพื่อค้นหาลิงก์ภายนอก, และวนซ้ำ `NodeList` ที่ได้อย่างปลอดภัย

การทำงานกับ HTML ใน Java มักรู้สึกหนักหน่วง แต่ไลบรารีสมัยใหม่ให้ API ที่กระชับและอิง CSS‑selector ตัวอย่างด้านล่างใช้ **jsoup** (เวอร์ชัน 1.17.2) เนื่องจากรองรับตัวเลือกสไตล์ `querySelectorAll` และคืนค่าเป็นคอลเลกชัน `Elements` ที่ทำงานเหมือน `NodeList` คุณสามารถปรับใช้ตรรกะเดียวกันกับการทำงานของ DOM อื่น ๆ หากต้องการ

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน ให้ตรวจสอบว่าคุณมี:

* JDK 17 หรือใหม่กว่า ติดตั้งอยู่
* Maven หรือ Gradle สำหรับจัดการ dependency
* ความคุ้นเคยพื้นฐานกับ Java streams และโมเดล DOM

เพิ่ม jsoup เข้าในโปรเจกต์ของคุณ:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## ขั้นตอนที่ 1: อ่าน HTML จากไฟล์

งานแรกคือการโหลดเอกสาร HTML จากดิสก์ `Jsoup.parse(Path, Charset)` จะอ่านไฟล์และสร้างต้นไม้ DOM ที่คุณสามารถ query ได้

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*ทำไมเรื่องนี้ถึงสำคัญ*: การโหลดไฟล์เพียงครั้งเดียวช่วยหลีกเลี่ยงการทำ I/O ซ้ำเมื่อคุณวนซ้ำองค์ประกอบในภายหลัง วัตถุ `Document` ถือ DOM ทั้งหมด ทำให้สามารถทำการคิวรีเซเลกเตอร์ได้อย่างรวดเร็ว

## ขั้นตอนที่ 2: ใช้ `querySelectorAll` เพื่อเลือกองค์ประกอบโดยคลาส

เมื่อเอกสารอยู่ในหน่วยความจำแล้ว คุณสามารถ **เลือกองค์ประกอบโดยคลาส** ด้วย CSS selector ตัวเลือก `"a.external"` จะจับแท็ก `<a>` ที่มีคลาส `external` — สิ่งที่คุณต้องการเพื่อ **ค้นหาลิงก์ภายนอก**

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*ทำไมเรื่องนี้ถึงสำคัญ*: การใช้ตัวเลือกคลาสให้ความหมายชัดเจนและมีประสิทธิภาพ ไลบรารีจะแปลงตัวเลือกเป็นการเดินทางที่ปรับแต่งแล้ว ดังนั้นคุณไม่จำเป็นต้องเขียนลูปด้วยตนเองสำหรับทุกโหนด

## ขั้นตอนที่ 3: วนซ้ำ NodeList (Elements) ใน Java

`Elements` implements `Iterable<Element>` ซึ่งหมายความว่าคุณสามารถใช้ลูป `for‑each` มาตรฐานเพื่อ **วนซ้ำ NodeList ใน Java** วัตถุ ตัวอย่างด้านล่างพิมพ์ค่าแอตทริบิวต์ `href` ของแต่ละลิงก์

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*ทำไมเรื่องนี้ถึงสำคัญ*: การวนซ้ำโดยตรงทำให้โค้ดอ่านง่ายและหลีกเลี่ยงค่าโอเวอร์เฮดของการแปลงคอลเลกชันเป็น stream เมื่อคุณต้องการเพียงแค่แสดงผลอย่างง่าย

## ตัวอย่างทำงานเต็มรูปแบบ

รวมสามขั้นตอนเข้าด้วยกันจะได้โปรแกรมที่ทำงานได้อย่างอิสระและสามารถรันจากบรรทัดคำสั่ง

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

สมมติว่า `input.html` มีเนื้อหา:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

เมื่อรันโปรแกรมจะพิมพ์ผล:

```
External link: https://example.com
External link: https://openai.com
```

## เคล็ดลับระดับมืออาชีพและข้อผิดพลาดทั่วไป

* **Encoding matters** – อ่านไฟล์เสมอด้วย UTF‑8 (หรือ charset ที่ตรงกับแหล่งข้อมูล) การเข้ารหัสที่ไม่ถูกต้องอาจทำให้ตัวอักษรในค่าแอตทริบิวต์เสียหาย
* **Multiple classes** – หากองค์ประกอบมีหลายคลาส (เช่น `class="btn external"` ) ตัวเลือก `"a.external"` ยังจับได้อยู่ เพราะตัวเลือกคลาสของ CSS ตรวจสอบการมีอยู่ของโทเคน ไม่ใช่สตริงเต็ม
* **Performance tip** – หากคุณต้องการแค่แอตทริบิวต์ `href` สามารถเรียกโดยตรงด้วย `doc.select("a.external[href]").eachAttr("href")` วิธีนี้หลีกเลี่ยงการสร้างอ็อบเจ็กต์ `Element` เต็มรูปแบบสำหรับแต่ละผลลัพธ์
* **Null safety** – `link.attr("href")` จะคืนสตริงว่างหากแอตทริบิวต์ไม่มีค่า ดังนั้นไม่จำเป็นต้องตรวจสอบ null ก่อนพิมพ์

## คำถามที่พบบ่อย

**Q: Does this work with HTML fragments that lack a `<html>` root?**  
A: ใช่ `Jsoup.parse` จะถืออินพุตเป็น fragment และเพิ่ม root ที่ขาดหายโดยอัตโนมัติ ทำให้ตัวเลือกทำงานบน body ของ fragment ได้

**Q: Can I use `querySelectorAll` without jsoup?**  
A: API DOM มาตรฐานของ Java (`org.w3c.dom`) ไม่ได้รวม `querySelectorAll` ไลบรารีอย่าง **HTMLUnit** หรือ **jodd-lagarto** มีเมธอดที่คล้ายกัน รูปแบบที่แสดงในที่นี้ – โหลด, เลือกด้วย CSS, วนซ้ำ – ยังคงเหมือนเดิม

**Q: What if I need to modify the links instead of just printing them?**  
A: หลังจากได้ `Element` แต่ละอันแล้ว คุณสามารถเรียก `link.attr("href", "newUrl")` แล้วเขียนเอกสารกลับไปยังดิสก์ด้วย `Files.writeString`

## สรุป

คุณได้เรียนรู้วิธี **เลือกองค์ประกอบโดยคลาส**, **อ่าน HTML จากไฟล์**, **ค้นหาลิงก์ภายนอก**, และ **วนซ้ำ NodeList ใน Java** ด้วยตัวเลือกสไตล์ `querySelectorAll` ตัวอย่างเต็มรูปแบบแสดงกระบวนการทำงานที่สะอาดและพร้อมใช้งานในโปรดักชัน ซึ่งคุณสามารถนำไปฝังใน pipeline การสเกรปหรือการแปลงข้อมูลขนาดใหญ่ได้

ต่อไปลองสำรวจหัวข้อที่เกี่ยวข้อง เช่น **การ parse เนื้อหาแบบไดนามิกด้วย HTMLUnit**, **การเขียน HTML ที่แก้ไขแล้วกลับไปยังดิสก์**, หรือ **การใช้ Java streams เพื่อรวบรวม URL ของลิงก์เป็นรายการ** ทุกหัวข้อนี้ต่อยอดจากเทคนิคการเลือกโดยคลาสที่แสดงในที่นี้ ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณ

- [วิธี query HTML ใน Java – เลือกองค์ประกอบ, กรองตามแอตทริบิวต์, และดึงข้อความ](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [วนซ้ำ NodeList Java – อ่าน HTML & ดึง src ของรูปภาพ](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [โหลดเอกสาร HTML จากไฟล์ใน Aspose.HTML สำหรับ Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}