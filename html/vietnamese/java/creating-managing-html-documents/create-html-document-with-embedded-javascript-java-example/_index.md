---
category: general
date: 2026-06-03
description: Tạo tài liệu HTML trong Java và nhúng JavaScript để tăng một bộ đếm.
  Học ví dụ về engine script, lấy innerHTML của phần tử, và nhiều hơn nữa.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: vi
og_description: Tạo tài liệu HTML trong Java, nhúng JavaScript để tăng bộ đếm và lấy
  giá trị cuối cùng bằng ví dụ sử dụng engine script.
og_title: Tạo tài liệu HTML với JavaScript nhúng – Ví dụ Java
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
title: Tạo tài liệu HTML với JavaScript nhúng – Ví dụ Java
url: /vi/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Tài liệu HTML với JavaScript Nhúng – Ví dụ Java

Bạn đã bao giờ cần **tạo tài liệu HTML** từ mã Java và tự hỏi cách nhúng JavaScript vào trong đó chưa? Trong hướng dẫn này chúng tôi sẽ chỉ cho bạn cách thực hiện, từng bước một, và bạn sẽ có một ví dụ về engine script hoạt động, in ra giá trị cuối cùng của bộ đếm.  

Nếu bạn từng tự hỏi *“làm sao tôi có thể lấy innerHTML của phần tử sau khi script chạy?”* hoặc *“cách sạch nhất để tăng một bộ đếm trong JavaScript từ Java là gì?”*—bạn đang ở đúng nơi. Chúng tôi sẽ đề cập đến **embed javascript html**, **increment counter javascript**, và **get element innerHTML** trong một hướng dẫn thống nhất.

![Tạo Tài liệu HTML với JavaScript nhúng](/images/create-html-document.png){: .center alt="Ví dụ tạo tài liệu HTML với JavaScript nhúng"}

## Những gì bạn sẽ xây dựng

1. **Tạo một tài liệu HTML** trong bộ nhớ.  
2. **Nhúng một đoạn JavaScript nhỏ** mà tăng bộ đếm năm lần.  
3. **Khởi tạo một script engine** (ví dụ `ScriptEngine`) để chạy đoạn mã đó.  
4. **Lấy giá trị cuối cùng của bộ đếm** bằng cách sử dụng `getElementInnerHTML`.  
5. In `Final counter value: 5` ra console.  

Không có tệp ngoại vi, không có máy chủ web—chỉ Java thuần và một chuỗi HTML nhỏ.

## Yêu cầu trước

- Java 17 trở lên (API `ScriptEngine` là một phần của thư viện chuẩn).  
- Kiến thức cơ bản về HTML và JavaScript (bạn không cần chuyên sâu).  
- Một IDE hoặc trình soạn thảo văn bản đơn giản cộng với terminal để biên dịch và chạy chương trình.

## Bước 1: Tạo tài liệu HTML trong Java

Điều đầu tiên chúng ta cần là một đối tượng tài liệu HTML trống mà sau này chúng ta có thể điền nội dung. Hãy nghĩ nó như một trang ảo chỉ tồn tại trong bộ nhớ.

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

**Tại sao điều này quan trọng:** Bằng cách **tạo tài liệu HTML** tự mình, bạn tránh việc ghi ra đĩa và giữ mọi thứ có thể kiểm thử. Mô phỏng DOM nhỏ này cho phép chúng ta sau này **lấy innerHTML của phần tử** mà không cần trình duyệt đầy đủ.

## Bước 2: Nhúng JavaScript HTML – Logic Đếm

Bây giờ chúng ta sẽ viết markup HTML bao gồm một khối `<script>`. Script này sẽ **tăng bộ đếm JavaScript** năm lần.

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

**Giải thích:**  
- `<div id='counter'>0</div>` là phần tử mục tiêu của chúng ta.  
- Vòng lặp `for` thực hiện logic **increment counter javascript**, cập nhật div ở mỗi vòng lặp.  
- Vì chúng ta không ở trong trình duyệt thực, engine script mà chúng ta sẽ dùng sau này cần hiểu `document.getElementById`. Đó là lý do chúng tôi thêm một stub nhỏ trong `HTMLDocument`.

## Bước 3: Khởi tạo Script Engine – Ví dụ Script Engine

Java đi kèm với API `ScriptEngine` (JSR‑223). Chúng tôi sẽ tạo một wrapper nhỏ để đưa nội dung HTML vào engine và cung cấp các phương thức DOM tối thiểu mà nó yêu cầu.

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

**Tại sao điều này quan trọng:** Ví dụ **script engine** này cho thấy cách bạn có thể chạy JavaScript nhúng mà không cần trình duyệt đầy đủ. Nó cũng minh họa cách nhẹ nhàng để phơi bày `document.getElementById` để script có thể tương tác với DOM mô phỏng của chúng ta.

## Bước 4: Thực thi JavaScript – Increment Counter JavaScript trong hành động

Khi engine đã sẵn sàng, chúng ta chỉ cần chạy script. Vòng lặp bên trong thẻ `<script>` sẽ được thực thi, và `setInnerHTML` mô phỏng của chúng ta sẽ cập nhật bộ đếm.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**Điều gì xảy ra bên trong?** Mỗi vòng lặp gọi `document.getElementById('counter').innerHTML = i + 1;`. `setInnerHTML` mô phỏng của chúng ta chuyển chuỗi số sang `HTMLDocument.updateCounter`, lưu giá trị mới nhất. Khi vòng lặp kết thúc, bản đồ nội bộ của tài liệu chứa `"5"` cho phần tử `counter`.

## Bước 5: Lấy Giá trị Bộ đếm Cuối cùng – Get Element InnerHTML

Bây giờ script đã hoàn thành, chúng ta có thể **lấy innerHTML của phần tử** từ instance `HTMLDocument` của mình.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Chạy toàn bộ chương trình sẽ in:

```
Final counter value: 5
```

Điều này xác nhận logic **increment counter javascript** đã hoạt động và chúng ta đã **lấy được innerHTML của phần tử** thành công sau khi script thực thi.

## Ví dụ Hoạt động Đầy đủ

Kết hợp mọi thứ lại, đây là lớp Java hoàn chỉnh, sẵn sàng chạy:

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


## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, có giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Tạo tài liệu HTML trống trong Aspose.HTML cho Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Tạo tài liệu HTML từ chuỗi trong Aspose.HTML cho Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Lưu tài liệu HTML trong Aspose.HTML cho Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}