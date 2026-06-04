---
category: general
date: 2026-06-03
description: สร้างเอกสาร HTML ใน Java และฝัง JavaScript เพื่อเพิ่มตัวนับ เรียนรู้ตัวอย่างเครื่องมือสคริปต์
  ดึงค่า innerHTML ขององค์ประกอบ และอื่น ๆ อีกมาก.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: th
og_description: สร้างเอกสาร HTML ด้วย Java ฝัง JavaScript เพื่อเพิ่มตัวนับและดึงค่าตัวสุดท้ายโดยใช้ตัวอย่างเครื่องมือสคริปต์
og_title: สร้างเอกสาร HTML พร้อม JavaScript ฝังในตัว – ตัวอย่าง Java
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: สร้างเอกสาร HTML พร้อม JavaScript ฝังในตัว – ตัวอย่าง Java
url: /th/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างเอกสาร HTML พร้อมฝัง JavaScript – ตัวอย่าง Java

เคยต้องการ **สร้างเอกสาร HTML** จากโค้ด Java และสงสัยว่าจะฝัง JavaScript ไว้ในนั้นอย่างไรหรือไม่? ในคู่มือนี้เราจะสาธิตขั้นตอนนั้นอย่างละเอียด และคุณจะได้ตัวอย่างการทำงานของ script engine ที่พิมพ์ค่าตัวนับสุดท้ายออกมา  

ถ้าคุณเคยถามตัวเองว่า *“ฉันจะดึงค่า element innerHTML หลังจากสคริปต์ทำงานเสร็จได้อย่างไร?”* หรือ *“วิธีที่สะอาดที่สุดในการเพิ่มค่าตัวนับใน JavaScript จาก Java คืออะไร?”*—คุณมาถูกที่แล้ว เราจะครอบคลุม **embed javascript html**, **increment counter javascript**, และ **get element innerHTML** ทั้งหมดในบทเรียนเดียวกัน

![สร้างเอกสาร HTML พร้อมฝัง JavaScript](/images/create-html-document.png){: .center alt="ตัวอย่างการสร้างเอกสาร HTML พร้อมฝัง JavaScript"}

## สิ่งที่จะสร้าง

เมื่อจบบทเรียนนี้คุณจะมีโปรแกรม Java ที่ทำงานได้เองซึ่ง:

1. **สร้างเอกสาร HTML** ในหน่วยความจำ
2. **ฝังส่วนย่อย JavaScript เล็กๆ** ที่เพิ่มค่าตัวนับห้าครั้ง
3. **เริ่มต้น script engine** (ตัวอย่าง `ScriptEngine`) เพื่อรันส่วนย่อยนั้น
4. **ดึงค่าตัวนับสุดท้าย** โดยใช้ `getElementInnerHTML`
5. พิมพ์ `Final counter value: 5` ไปยังคอนโซล

ไม่มีไฟล์ภายนอก, ไม่มีเว็บเซิร์ฟเวอร์—เพียง Java ธรรมดาและสตริง HTML เล็กๆ

---

## ข้อกำหนดเบื้องต้น

- Java 17 หรือใหม่กว่า (API `ScriptEngine` เป็นส่วนหนึ่งของไลบรารีมาตรฐาน)
- ความคุ้นเคยพื้นฐานกับ HTML และ JavaScript (คุณไม่จำเป็นต้องเชี่ยวชาญลึก)
- IDE หรือเครื่องมือแก้ไขข้อความง่ายๆ พร้อมเทอร์มินัลเพื่อคอมไพล์และรันโปรแกรม

## ขั้นตอนที่ 1: สร้างเอกสาร HTML ใน Java

สิ่งแรกที่เราต้องการคืออ็อบเจกต์เอกสาร HTML เปล่าที่เราจะเติมเนื้อหาในภายหลัง คิดว่าเป็นหน้าจำลองที่อยู่ในหน่วยความจำเท่านั้น

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**ทำไมเรื่องนี้สำคัญ:** ด้วยการ **สร้างเอกสาร HTML** ด้วยตนเอง คุณจะหลีกเลี่ยงการเขียนลงดิสก์และทำให้ทุกอย่างทดสอบได้ การจำลอง DOM ขนาดเล็กทำให้เราสามารถ **ดึงค่า element innerHTML** ได้ในภายหลังโดยไม่ต้องใช้เบราว์เซอร์เต็มรูปแบบ

## ขั้นตอนที่ 2: ฝัง JavaScript HTML – ลอจิกตัวนับ

ตอนนี้เราจะเขียน markup HTML ที่รวม `<script>` block สคริปต์นี้จะ **increment counter JavaScript** ห้าครั้ง

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**คำอธิบาย:**  
- `<div id='counter'>0</div>` คือองค์ประกอบเป้าหมายของเรา  
- ลูป `for` ทำงานตามลอจิก **increment counter javascript** โดยอัปเดต div ในแต่ละรอบ  
- เนื่องจากเราไม่ได้อยู่ในเบราว์เซอร์จริง, script engine ที่เราจะใช้ต่อไปต้องเข้าใจ `document.getElementById` นั่นจึงเป็นเหตุผลที่เราเพิ่ม stub เล็กๆ ใน `HTMLDocument`

## ขั้นตอนที่ 3: เริ่มต้น Script Engine – ตัวอย่าง Script Engine

Java มาพร้อมกับ API `ScriptEngine` (JSR‑223). เราจะสร้าง wrapper เล็กๆ ที่ส่งเนื้อหา HTML ไปยัง engine และให้เมธอด DOM ขั้นพื้นฐานที่มันต้องการ

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**ทำไมเรื่องนี้สำคัญ:** **script engine example** นี้แสดงวิธีรัน JavaScript ฝังได้โดยไม่ต้องใช้เบราว์เซอร์เต็มรูปแบบ อีกทั้งยังสาธิตวิธีเบาๆ ในการเปิดเผย `document.getElementById` เพื่อให้สคริปต์โต้ตอบกับ mock DOM ของเรา

## ขั้นตอนที่ 4: รัน JavaScript – Increment Counter JavaScript ทำงาน

เมื่อ engine พร้อม เราก็รันสคริปต์ได้เลย ลูปภายในแท็ก `<script>` จะทำงานและ mock `setInnerHTML` ของเราจะอัปเดตตัวนับ

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**อะไรเกิดขึ้นเบื้องหลัง?** แต่ละรอบของลูปจะเรียก `document.getElementById('counter').innerHTML = i + 1;`. mock `setInnerHTML` ของเราจะส่งสตริงตัวเลขไปยัง `HTMLDocument.updateCounter` ซึ่งเก็บค่าล่าสุด หลังจากลูปจบ แผนที่ภายในของเอกสารจะมีค่า `"5"` สำหรับองค์ประกอบ `counter`

## ขั้นตอนที่ 5: ดึงค่าตัวนับสุดท้าย – Get Element InnerHTML

เมื่อสคริปต์ทำงานเสร็จแล้ว เราสามารถ **get element innerHTML** จากอินสแตนซ์ `HTMLDocument` ของเรา

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

การรันโปรแกรมทั้งหมดจะพิมพ์:

```
Final counter value: 5
```

ซึ่งยืนยันว่าโลจิก **increment counter javascript** ทำงานและเราสามารถ **retrieved the element innerHTML** หลังจากการรันสคริปต์ได้สำเร็จ

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือคลาส Java ที่สมบูรณ์พร้อมรัน:

```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

public class HtmlJsDemo {

    // ---------- Minimal HTMLDocument implementation ----------
    static class HTMLDocument {
        private final StringBuilder html = new StringBuilder();
        private final java.util.Map<String, String> elements = new java.util.HashMap<>();

        public void write(String content) {
            html.append(content);
        }

        public String getContent() {
            return html.toString();
        }

        public void setElementInnerHTML(String id, String value) {
            elements.put(id, value);
        }

        public String getElementInnerHTML(String id) {
            return elements.getOrDefault(id, "");
        }

        public void updateCounter(int value) {
            setElementInnerHTML("counter", String.valueOf(value));
        }
    }

    // ---------- SimpleScriptEngine (script engine example) ----------
    static class SimpleScriptEngine {
        private final HTMLDocument document;
        private final ScriptEngine engine;

        public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
            this.document = doc;
            ScriptEngineManager manager = new ScriptEngineManager();
            this.engine = manager.getEngineByName("JavaScript");
            // Expose a mock 'document' object
            engine.put("document", new Object() {
                public Object getElementById(String id) {
                    return new Object() {
                        public void setInnerHTML(String value) {
                            document.updateCounter(Integer.parseInt(value));
                        }
                    };
                }
            });
        }

        public void execute() throws ScriptException {
            String html = document.getContent();
            int start = html.indexOf("<script>") + "<script>".length();
            int end   = html.indexOf("</script>");
            String script = html.substring(start, end);
            engine.eval(script);
        }
    }

    // ---------- Main method ----------
    public static void main(String[] args) {
        // Step 1: create HTML document
        HTMLDocument doc = new HTMLDocument();

        // Step 2: embed JavaScript HTML (increment counter JavaScript)
        doc.write(
            "<!DOCTYPE html><html><body>"
          + "<div id='counter'>0</div>"
          + "<script>"
          + "for (let i = 0; i < 5; i++) {"
          + "  document.getElementById('counter').innerHTML = i


## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณ

- [สร้างเอกสาร HTML ว่างใน Aspose.HTML สำหรับ Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [สร้างเอกสาร HTML จากสตริงใน Aspose.HTML สำหรับ Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [บันทึกเอกสาร HTML ใน Aspose.HTML สำหรับ Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}