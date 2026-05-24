---
category: general
date: 2026-02-11
description: Tạo tài liệu HTML trong Java bằng Aspose.HTML. Tìm hiểu cách lấy JSON
  JavaScript, thêm phần tử script, tạo HTML từ JSON và chuyển JSON thành pre.
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: vi
og_description: Tạo tài liệu HTML trong Java bằng Aspose.HTML. Lấy JSON JavaScript,
  thêm phần tử script, tạo HTML từ JSON và chuyển JSON thành thẻ pre — tất cả trong
  một hướng dẫn.
og_title: Tạo tài liệu HTML trong Java – Hướng dẫn đầy đủ
tags:
- Aspose.HTML
- Java
- Web Automation
title: Tạo tài liệu HTML bằng Java – Lấy JSON và tạo nội dung
url: /vi/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

inside.

Let's produce final content.

Start with shortcodes unchanged.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Tài Liệu HTML – Hướng Dẫn Java Đầy Đủ

Bạn đã bao giờ cần **tạo tài liệu HTML** một cách nhanh chóng nhưng không chắc làm sao để kéo dữ liệu từ xa vào đó? Bạn không phải là người duy nhất. Trong nhiều dự án, bạn sẽ muốn lấy JSON bằng JavaScript, chèn kết quả vào một trang, và sau đó lưu markup cuối cùng thành một tệp tĩnh. Hướng dẫn này sẽ chỉ cho bạn cách thực hiện điều đó bằng Aspose.HTML cho Java.

Chúng ta sẽ đi qua từng bước: từ khởi tạo một tài liệu rỗng, tới **fetch JSON JavaScript**, tới **add script element**, và cuối cùng là **generate HTML from JSON** và **convert JSON to pre**. Khi hoàn thành, bạn sẽ có một tệp `fetchResult.html` sẵn sàng, chứa dữ liệu đã lấy được được hiển thị dưới dạng JSON được format đẹp.

## Yêu Cầu Trước

- Java 17 hoặc mới hơn (mã cũng biên dịch được với JDK 11+)
- Thư viện Aspose.HTML cho Java (có sẵn qua Maven Central)
- Kiến thức cơ bản về HTML và JavaScript bất đồng bộ
- Một IDE hoặc dòng lệnh `javac`/`java`

Không cần bất kỳ framework nào khác—mọi thứ chạy cục bộ.

## Bước 1: Thiết Lập Dự Án và Nhập Aspose.HTML

Đầu tiên, thêm phụ thuộc Aspose.HTML vào file `pom.xml` của bạn (hoặc tải JAR thủ công).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **Mẹo:** Giữ cho số phiên bản luôn cập nhật; các bản phát hành mới sửa lỗi và cải thiện engine script.

## Bước 2: **Create HTML Document** – Canvas Trống

Chúng ta bắt đầu bằng việc tạo một `HTMLDocument` rỗng. Hãy nghĩ nó như một trang trắng mà sau này chúng ta sẽ chèn script vào.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

Tại sao cần một đối tượng tài liệu? `ScriptEngine` của Aspose.HTML hoạt động trên một DOM, không phải một chuỗi thô. Khi xây dựng một tài liệu đúng chuẩn, chúng ta cung cấp cho engine một môi trường thực để thực thi **fetch JSON JavaScript** của mình.

## Bước 3: Viết Đoạn JavaScript – **Fetch JSON JavaScript** và **Convert JSON to pre**

Trái tim của tutorial nằm trong chuỗi đa dòng này. Nó thực hiện một `fetch` bất đồng bộ, phân tích JSON, rồi ghi một phần tử `<pre>` với dữ liệu được format đẹp.

```java
        // Step 3: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;
```

Chú ý comment *Convert JSON to <pre>* – đó chính là những gì lệnh `JSON.stringify(..., null, 2)` thực hiện. Nó thêm thụt lề, làm cho đầu ra dễ đọc cho con người.

## Bước 4: **Add Script Element** vào Tài Liệu

Bây giờ chúng ta tạo một thẻ `<script>`, đặt mã của mình vào trong, và gắn nó vào thân trang. Đây là phần **add script element**.

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

Tại sao lại gắn vào `<body>`? Trong một trình duyệt thực, script sẽ chạy ngay khi được phân tích. Bằng cách thêm nó vào DOM, chúng ta mô phỏng hành vi chính xác đó, đảm bảo việc fetch bất đồng bộ chạy khi chúng ta gọi engine.

## Bước 5: Chạy Script Engine – Để Async Fetch Hoàn Thành

Aspose.HTML cung cấp một `ScriptEngine` có thể thực thi JavaScript dựa trên DOM. Chúng ta gọi `run()` và chờ chuỗi promise hoàn tất.

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

Engine sẽ chặn cho đến khi tất cả các tác vụ đang chờ (fetch của chúng ta) được giải quyết, bảo đảm HTML đã được tạo ra chứa dữ liệu.

## Bước 6: **Generate HTML from JSON** – Lưu Kết Quả

Cuối cùng chúng ta ghi tài liệu ra đĩa. Tệp bây giờ chứa khối `<pre>` với payload JSON.

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

Chạy chương trình sẽ tạo ra `fetchResult.html`. Mở nó trong bất kỳ trình duyệt nào và bạn sẽ thấy một thứ gì đó như:

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

Đó là kết quả **generate HTML from JSON** mà bạn đang tìm.

## Ví Dụ Hoàn Chỉnh

Dưới đây là file nguồn đầy đủ, sẵn sàng chạy. Sao chép, dán, chỉnh đường dẫn xuất, và chạy `java JsFetchExample`.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();

        // Step 2: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;

        // Step 3: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);

        // Step 4: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();

        // Step 5: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

## Kết Quả Mong Đợi & Kiểm Tra

1. **Console:** Bạn sẽ thấy `HTML with fetched data saved.`  
2. **File (`fetchResult.html`):** Mở nó sẽ hiển thị JSON bên trong một khối `<pre>`, được thụt lề đẹp mắt.  
3. **Xác Thực:** Nếu xem nguồn trang, bạn sẽ chỉ thấy một phần tử `<pre>`—không còn thẻ script nào vì engine đã thực thi chúng.

## Câu Hỏi Thường Gặp & Các Trường Hợp Cạnh

| Question | Answer |
|----------|--------|
| *What if the API returns an error?* | Wrap the `fetch` call in a `try…catch` block and write an error message to the body instead of the JSON. |
| *Can I fetch multiple resources?* | Yes—just chain additional `await fetch(...)` calls or use `Promise.all`. The final `innerHTML` can concatenate several `<pre>` blocks. |
| *Do I need to set CORS headers?* | Since the script runs inside Aspose.HTML’s sandbox, it respects the same‑origin policy. The public JSONPlaceholder endpoint already allows cross‑origin requests. |
| *How to change the output directory at runtime?* | Pass the path as a command‑line argument (`args[0]`) and replace the hard‑coded string in `htmlDoc.save`. |
| *Is there a way to embed CSS for styling?* | Absolutely. Create a `<style>` element, set its `textContent` to your CSS, and append it to `<head>` before running the engine. |

## Mẹo Dành Cho Sản Xuất

- **Cache the JSON** nếu endpoint chậm; bạn có thể ghi chuỗi đã lấy vào tệp và tái sử dụng.  
- **Sanitize the data** trước khi chèn, đặc biệt nếu nguồn không đáng tin cậy. Sử dụng `JSON.stringify` một cách an toàn hoặc escape các thực thể HTML.  
- **Configure the ScriptEngine timeout** (`scriptEngine.setTimeout(5000)`) để tránh treo khi dịch vụ không phản hồi.

## Tóm Tắt Hình Ảnh

![create html document example showing the generated HTML with JSON inside a pre tag](fetchResult.png "Screenshot of the generated HTML document")

*Alt text:* *ví dụ tạo tài liệu html – tệp HTML đã tạo hiển thị JSON đã fetch bên trong một phần tử pre.*

## Kết Luận

Bây giờ bạn đã biết cách **create HTML document** một cách lập trình trong Java, **fetch JSON JavaScript**, **add script element**, **generate HTML from JSON**, và **convert JSON to pre** để có đầu ra dễ đọc. Toàn bộ quy trình chạy offline, chỉ cần Aspose.HTML, và tạo ra một tệp tĩnh sạch sẽ mà bạn có thể phục vụ ở bất kỳ đâu.

Tiếp theo, hãy thử mở rộng script để lặp qua một mảng các đối tượng, thêm CSS styling, hoặc viết nhiều trang bằng cùng một kỹ thuật. Bạn cũng có thể thay đổi URL `fetch` bằng API của riêng mình để biến dữ liệu động thành các ảnh chụp tĩnh—hoàn hảo cho việc render trước thân thiện SEO.

Chúc lập trình vui vẻ, và đừng ngại chia sẻ các thí nghiệm của bạn trong phần bình luận!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}