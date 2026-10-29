---
category: general
date: 2026-08-25
description: Học cách tạo tài liệu HTML, chọn phần tử CSS, chỉnh sửa văn bản HTML
  và lưu tệp HTML bằng một script Python đơn giản.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: vi
lastmod: 2026-08-25
og_description: Tạo tài liệu HTML, chọn phần tử CSS, chỉnh sửa văn bản HTML và lưu
  tệp HTML chỉ trong vài dòng Python. Thực hiện theo hướng dẫn đầy đủ này.
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: Tạo tài liệu HTML và chỉnh sửa nội dung của nó bằng Python – hướng dẫn từng
  bước
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: Cách tạo tài liệu HTML và chỉnh sửa nội dung của nó trong Python
url: /vi/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách tạo html document và chỉnh sửa nội dung của nó trong Python

Nếu bạn cần **create html document** từ đầu và thay đổi các phần tử của nó một cách lập trình, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ thấy một đoạn script ngắn, có thể chạy được, tạo một tệp, chọn một đoạn văn bằng CSS selector, cập nhật văn bản và ghi kết quả trở lại đĩa.

Làm việc với HTML trong Python thường gặp khi tạo báo cáo, mẫu email, hoặc nội dung trang tĩnh. Khi kết thúc tutorial này, bạn sẽ có thể **select element css**, **modify html text**, và **save html file** mà không rời khỏi môi trường IDE của mình.

## Yêu cầu trước

* Cài đặt Python 3.9 hoặc mới hơn.
* Các gói `beautifulsoup4` và `lxml` (cài đặt bằng `pip install beautifulsoup4 lxml`).
* Quyền ghi vào thư mục nơi bạn dự định lưu tệp đầu ra.

Không cần công cụ bổ sung nào; thư viện chuẩn đã xử lý I/O tệp.

## Bước 1: Cài đặt các thư viện cần thiết

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` cung cấp một API tiện lợi để phân tích và thao tác HTML, trong khi `lxml` cung cấp một parser nhanh có khả năng hiểu CSS selectors.

## Bước 2: Tạo tài liệu HTML ban đầu

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

Constructor `BeautifulSoup` tạo một đối tượng **create html document** trong bộ nhớ. Sử dụng parser `"lxml"` đảm bảo hỗ trợ đầy đủ CSS selector.

## Bước 3: Chọn phần tử đoạn văn bằng CSS selector

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

Phương thức `select_one` thực hiện logic **select element css**, trả về thẻ đầu tiên khớp. Nếu selector không khớp với bất kỳ phần tử nào, `para` sẽ là `None`, vì vậy nên kiểm tra phòng ngừa trong mã sản xuất.

## Bước 4: Thay đổi nội dung văn bản của đoạn văn

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

Gán giá trị cho `para.string` thực hiện một thao tác **modify html text**. BeautifulSoup cập nhật cây DOM bên dưới, vì vậy thay đổi sẽ được phản ánh khi tài liệu được tuần tự hoá.

## Bước 5: Lưu HTML đã cập nhật vào tệp

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

Lệnh `open` kết hợp với `write` thực hiện chức năng **save html file**. Sử dụng `prettify()` tạo ra đầu ra được thụt lề đẹp mắt, hữu ích khi gỡ lỗi.

### Đoạn script đầy đủ để sao chép nhanh

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

Chạy `python edit_html.py` sẽ tạo `updated.html` chứa:

```html
<p>
 New
</p>
```

## Các biến thể phổ biến và trường hợp đặc biệt

### Chọn nhiều phần tử

Nếu bạn cần các **select element css** selector khớp với nhiều thẻ (ví dụ, `"div.note"`), hãy dùng `doc.select("div.note")` để trả về một danh sách. Lặp qua danh sách để áp dụng thay đổi cho mỗi phần tử.

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### Giữ nguyên các thuộc tính hiện có

Khi bạn thay thế văn bản, BeautifulSoup giữ lại mọi thuộc tính trên thẻ. Ví dụ:

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### Xử lý các phần tử thiếu một cách nhẹ nhàng

Trong các script sản xuất, bạn thường gặp HTML không hợp lệ. Bao quanh việc chọn trong một câu điều kiện hoặc khối try‑except, như trong Bước 4, để tránh lỗi.

### Ghi vào thư mục cụ thể

Thay `output_path` bằng đường dẫn tuyệt đối hoặc tương đối:

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

Đảm bảo thư mục tồn tại; nếu không, Python sẽ ném `FileNotFoundError`.

## Mẹo chuyên nghiệp

* **Performance** – Đối với các tệp HTML lớn, nên dùng trực tiếp `lxml.etree`; BeautifulSoup thêm một lớp trừu tượng mỏng, tiện lợi nhưng hơi chậm hơn.
* **Encoding** – Luôn mở tệp với `encoding="utf-8"` để bảo toàn các ký tự không phải ASCII.
* **Testing** – Sau khi chỉnh sửa, bạn có thể xác minh đầu ra bằng `assert "New" in open(output_path).read()` trong một unit test.

## Kết luận

Bây giờ bạn đã biết cách **create html document**, sử dụng truy vấn **select element css** để tìm một node, **modify html text**, và cuối cùng **save html file** bằng Python. Mô hình này có thể mở rộng cho các chuyển đổi phức tạp hơn như cập nhật hàng loạt, thay đổi thuộc tính, hoặc tạo mẫu.

Tiếp theo, khám phá các chủ đề liên quan như **how to edit html** bằng biểu thức XPath, tạo các trang HTML đầy đủ với Jinja2, hoặc tự động xử lý hàng loạt nhiều tệp. Mỗi chủ đề đều dựa trên các bước cốt lõi được trình bày ở đây và mở rộng bộ công cụ của bạn cho việc thao tác HTML một cách lập trình.

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Create HTML Document with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}