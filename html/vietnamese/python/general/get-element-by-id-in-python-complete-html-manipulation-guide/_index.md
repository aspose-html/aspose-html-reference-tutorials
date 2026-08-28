---
category: general
date: 2026-05-31
description: Học cách lấy phần tử theo id, thay đổi màu nền HTML, đọc văn bản HTML
  và đặt thuộc tính HTML bằng Python. Hướng dẫn từng bước.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: vi
og_description: Lấy phần tử theo id, đọc văn bản HTML, đặt thuộc tính HTML và thay
  đổi màu nền HTML bằng Python trong một hướng dẫn duy nhất, dễ theo dõi.
og_title: Lấy phần tử theo id trong Python – Hướng dẫn đầy đủ về thao tác HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: Lấy phần tử theo id trong Python – Hướng dẫn đầy đủ về thao tác HTML
url: /vi/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lấy phần tử theo id trong Python – Hướng dẫn Toàn diện về Manipulation HTML

Bạn đã bao giờ cần **lấy phần tử theo id** từ một trang HTML khi viết một script Python nhanh chóng chưa? Bạn không phải là người duy nhất—hầu hết các nhà phát triển đều gặp phải rào cản này khi bắt đầu crawl site hoặc chỉnh sửa báo cáo cục bộ. Tin tốt là gì? Chỉ với vài dòng code, bạn có thể đọc nội dung văn bản của phần tử, thay đổi màu nền, và thậm chí đặt các thuộc tính mới, tất cả mà không rời khỏi trình soạn thảo.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ thực tế: tải một file `sample.html` cục bộ, lấy phần tử có ID là `main‑content`, in ra nội dung văn bản bên trong, và cuối cùng đổi màu nền thành màu xám nhạt. Khi kết thúc, bạn sẽ biết **cách đọc văn bản HTML**, **cách đặt thuộc tính HTML**, và tại sao **manipulate HTML with Python** là một kỹ năng hữu ích trong bất kỳ bộ công cụ tự động hoá nào.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- **Python 3.9+** (bất kỳ phiên bản mới nào cũng được)
- Thư viện **`lxml`** (hoặc **BeautifulSoup** nếu bạn thích) – chúng ta sẽ dùng `lxml.html` vì nó cung cấp API kiểu `get_element_by_id` sạch sẽ.
- Một file HTML nhỏ tên `sample.html` nằm trong thư mục có tên `YOUR_DIRECTORY`. Bạn có thể sao chép đoạn mã dưới đây vào file đó:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

Chỉ vậy—không cần framework phức tạp, chỉ Python thuần và một file HTML tĩnh.

## Bước 1: Cài đặt Thư viện Yêu cầu

Nếu bạn chưa cài `lxml`, mở terminal và chạy:

```bash
pip install lxml
```

*Pro tip:* Sử dụng môi trường ảo (virtual environment) giúp giữ Python toàn cục của bạn sạch sẽ, đặc biệt khi bạn bắt đầu làm việc với nhiều dự án.

## Bước 2: Tải Tài liệu HTML

Bây giờ chúng ta sẽ đọc file vào một đối tượng tài liệu `lxml.html`. Hãy nghĩ đây như việc biến văn bản thô thành một cây có thể duyệt được.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

Chạy đoạn này sẽ in “Document loaded successfully.” Nếu file không tìm thấy, Python sẽ ném ra `FileNotFoundError`—điều này nên được bắt sớm trước khi bạn truy tìm một phần tử ảo.

## Bước 3: Lấy phần tử theo id

Đây là phần cốt lõi. `lxml` cung cấp phương thức tiện lợi `get_element_by_id` tương tự API DOM mà bạn dùng trong JavaScript.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

Khi phần tử tồn tại, bạn sẽ thấy “Element found!” được in ra console. Đây là bước **get element by id** mà chúng ta sẽ dùng cho các thao tác tiếp theo.

## Bước 4: Cách đọc văn bản HTML

Sau khi đã có phần tử, việc trích xuất văn bản hiển thị là cực kỳ dễ dàng. Phương thức `text_content()` trả về mọi thứ bên trong, đã loại bỏ các thẻ.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Kết quả mong đợi:

```
Inner text: Hello, world! This is the original text.
```

Bạn có thể tự hỏi, *nếu phần tử chứa các thẻ lồng nhau thì sao?* `text_content()` vẫn hoạt động—nó sẽ nối tất cả các node văn bản con lại, cho bạn một chuỗi sạch sẽ để ghi log, lưu trữ, hoặc đưa vào thuật toán khác.

## Bước 5: Cách đặt thuộc tính HTML

Thay đổi hoặc thêm thuộc tính cũng không phức tạp. Phương thức `set` cho phép bạn gán bất kỳ tên thuộc tính nào bạn muốn.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Kết quả:

```
New attribute value: true
```

Dòng này minh họa **how to set HTML attribute** ngay trong quá trình chạy. Bạn có thể thay `"data-modified"` bằng `"class"`, `"title"` hoặc bất kỳ thuộc tính nào mà phần tử hỗ trợ.

## Bước 6: Thay đổi màu nền HTML

Bây giờ là phần tinh chỉnh trực quan. Để thay đổi màu nền, chúng ta chèn một thuộc tính `style` ghi đè giá trị mặc định.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

Sau khi chạy script, thẻ `div` trong `sample.html` sẽ trông như sau khi mở trong trình duyệt:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

Đây là kỹ thuật **change background colour html** mà bạn có thể tái sử dụng cho bất kỳ phần tử nào—chỉ cần thay đổi mã màu.

## Bước 7: Manipulate HTML with Python – Kết hợp Tất cả

Dưới đây là script đầy đủ, có thể chạy ngay. Lưu lại dưới tên `modify_html.py` và thực thi trong cùng thư mục với thư mục `YOUR_DIRECTORY` của bạn.

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### Giải thích script, từng dòng một

1. **Imports** `lxml.html` để phân tích và `pathlib` cho các đường dẫn độc lập với hệ điều hành.  
2. **Loads** `sample.html` và dừng lại với lỗi rõ ràng nếu file bị thiếu.  
3. **Retrieves** phần tử bằng **get element by id**.  
4. **Prints** văn bản của phần tử—đây là **how to read HTML text**.  
5. **Adds** một thuộc tính tùy chỉnh, minh họa **how to set HTML attribute**.  
6. **Changes** màu nền, đáp ứng yêu cầu **change background colour html**.  
7. **Writes** markup đã cập nhật vào `sample_modified.html`, để bạn mở trong trình duyệt và thấy các thay đổi.

Chạy script sẽ xuất ra console tương tự:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

Mở `sample_modified.html` và bạn sẽ thấy nền xám phía sau văn bản—chứng minh rằng **manipulate HTML with python** thực sự hoạt động.

## Những Sai Lầm Thường Gặp & Cách Tránh

- **Missing ID** – Nếu phần tử mục tiêu không tồn tại, `get_element_by_id` sẽ trả về `None`. Luôn kiểm tra `None` trước khi truy cập thuộc tính; nếu không sẽ gặp `AttributeError`.  
- **Encoding issues** – Khi đọc các trang không phải ASCII, truyền `encoding='utf-8'` vào `html.parse` hoặc đảm bảo file của bạn được lưu dưới UTF‑8.  
- **Overwriting existing styles** – Đặt thuộc tính `style` sẽ thay thế bất kỳ style nội tuyến nào đã có. Nếu bạn cần giữ lại các quy tắc hiện có, hãy đọc giá trị `style` hiện tại, nối thêm quy tắc mới, rồi ghi lại.  
- **File permissions** – Ghi lại vào cùng thư mục có thể thất bại trên hệ thống chỉ đọc. Chọn một đường dẫn đầu ra có quyền ghi, như chúng ta đã làm với `sample_modified.html`.

## Mở Rộng Ví Dụ

Khi đã nắm vững các kiến thức cơ bản, bạn có thể thử các bước tiếp theo:

- **Loop over multiple IDs** – Dùng một danh sách các ID và lặp qua chúng bằng vòng `for` để xử lý hàng loạt các phần của trang.  
- **Replace text content** – Gọi `elem.text = "New text"` để thay đổi chuỗi hiển thị.  
- **Add child elements** – Use `

## Bạn Nên Học Gì Tiếp Theo?

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}