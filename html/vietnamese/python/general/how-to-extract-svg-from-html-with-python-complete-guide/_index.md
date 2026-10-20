---
category: general
date: 2026-05-31
description: Học cách trích xuất SVG từ HTML bằng Python. Hướng dẫn từng bước này
  cho thấy cách đọc tài liệu HTML, lưu các tệp SVG và lưu SVG nội tuyến một cách hiệu
  quả.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: vi
og_description: Cách trích xuất SVG từ HTML bằng Python. Theo dõi hướng dẫn này để
  đọc tài liệu HTML, lưu các tệp SVG và xử lý SVG nội tuyến một cách dễ dàng.
og_title: Cách trích xuất SVG từ HTML bằng Python – Hướng dẫn toàn diện
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: Cách trích xuất SVG từ HTML bằng Python – Hướng dẫn toàn diện
url: /vi/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách trích xuất SVG từ HTML bằng Python – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi **cách trích xuất SVG** từ một trang HTML lộn xộn mà không làm rối tóc chưa? Bạn không phải là người duy nhất. Dù bạn đang xây dựng một web‑scraper, một pipeline thiết kế, hay chỉ cần xuất hàng loạt các biểu tượng, việc biết **cách trích xuất SVG** là một mẹo hữu ích giúp tiết kiệm thời gian và giảm căng thẳng.

Trong tutorial này, chúng tôi sẽ chỉ cho bạn **cách trích xuất SVG** bằng thư viện Aspose.HTML cho Python. Chúng ta sẽ đọc tài liệu HTML, lấy cả markup `<svg>` nội tuyến **và** các tham chiếu SVG bên ngoài, sau đó **lưu các tệp SVG** vào đĩa — tất cả trong một script gọn gàng, có thể tái sử dụng. Khi kết thúc, bạn sẽ có một giải pháp sẵn sàng chạy mà bạn có thể tùy chỉnh cho dự án của mình.

> **Mẹo chuyên nghiệp:** Nếu bạn chỉ muốn “ngửi” nhanh nội dung của trang, `BeautifulSoup` cũng hoạt động, nhưng Aspose.HTML cung cấp một DOM đầy đủ, giúp việc trích xuất cả SVG nội tuyến và SVG liên kết trở nên dễ dàng.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Python 3.8+ (code sử dụng f‑strings, vì vậy 3.6+ là mức tối thiểu tuyệt đối)
* `pip install aspose-html` – thư viện thương mại hỗ trợ việc phân tích HTML của chúng ta
* Một thư mục chứa tệp `input.html` có các SVG bạn muốn lấy ra
* Quyền ghi vào thư mục đầu ra (chúng tôi sẽ gọi nó là `YOUR_DIRECTORY`)

Đó là tất cả — không cần binary phụ trợ, không cần trình duyệt headless. Đơn giản, phải không?

## Bước 1: Đọc tài liệu HTML với Aspose.HTML

Điều đầu tiên bạn phải làm là **đọc tài liệu HTML** để có thể duyệt cây DOM của nó. Aspose.HTML cung cấp một đối tượng `HTMLDocument` hoạt động giống như `document` của trình duyệt.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Lý do quan trọng:* Bằng cách tải HTML vào một DOM chuẩn, bạn tránh được các bẫy của việc phân tích bằng regex, và bạn có sẵn các phương thức như `get_elements_by_tag_name` và `query_selector_all`.

## Bước 2: Thu thập tất cả các phần tử `<svg>` nội tuyến

SVG nội tuyến là những khối `<svg>…</svg>` nằm ngay trong HTML. Để **lưu SVG nội tuyến** chúng ta chỉ cần lấy HTML bên ngoài của chúng.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Chú ý chúng tôi đang nối thẳng markup thô vào `svg_contents`. Sau này chúng tôi sẽ quyết định mỗi mục là markup hay là đường dẫn tệp.

## Bước 3: Tìm các tham chiếu SVG bên ngoài (thẻ img và object)

Nhiều trang liên kết tới các tệp SVG bên ngoài qua `<img src="icon.svg">` hoặc `<object data="logo.svg">`. Để **trích xuất SVG từ HTML** chúng ta cần nắm bắt các URL này nữa.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Cảnh báo trường hợp đặc biệt:* Nếu URL SVG là tương đối, bạn sẽ muốn nối nó với đường dẫn cơ sở của tệp HTML. Để ngắn gọn, chúng tôi giả sử HTML nằm cùng thư mục với các tệp SVG.

## Bước 4: Ghi mỗi SVG vào một tệp riêng

Bây giờ chúng ta có một danh sách hỗn hợp gồm các chuỗi markup và các đường dẫn tệp, chúng ta sẽ lặp qua và **lưu các tệp SVG**. Script sẽ tự động phân biệt giữa markup nội tuyến và tham chiếu tới một tệp đã tồn tại.

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**Bạn sẽ thấy:** Sau khi script kết thúc, `YOUR_DIRECTORY` sẽ chứa các tệp có tên `svg_0.svg`, `svg_1.svg`, … mỗi tệp chứa hoặc markup nội tuyến gốc hoặc một bản sao của SVG bên ngoài.

### Kết quả mong đợi

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Nếu một tệp được tham chiếu không tồn tại, script sẽ in cảnh báo nhưng vẫn tiếp tục — vì vậy một liên kết hỏng sẽ không làm dừng toàn bộ quá trình trích xuất.

## Xử lý các vấn đề thường gặp

| Vấn đề | Nguyên nhân | Giải pháp nhanh |
|--------|-------------|-----------------|
| **URL tương đối bị lỗi** | Thuộc tính `src` có thể là `"../assets/icon.svg"` | Dùng `os.path.join(os.path.dirname(html_path), src)` để giải quyết. |
| **Tên tệp trùng lặp** | Hai SVG có cùng tên sẽ bị ghi đè | Thêm hash của nội dung vào tên tệp (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **SVG nội tuyến lớn gây tăng bộ nhớ** | Lưu toàn bộ markup trong danh sách trước khi ghi | Ghi từng phần tử trực tiếp vào tệp thay vì lưu vào bộ đệm. |
| **Ảnh không phải SVG lọt qua** | Một số thẻ `<img>` kết thúc bằng `.svg?version=1` | Loại bỏ chuỗi truy vấn trước khi kiểm tra phần mở rộng (`src.split('?')[0]`). |

## Toàn bộ script bạn có thể sao chép‑dán

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy. Lưu lại dưới tên `extract_svg.py`, điều chỉnh `YOUR_DIRECTORY`, và chạy `python extract_svg.py`.

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## Tóm tắt – Cách trích xuất SVG trong một cái nhìn tổng quan

* **Đọc tài liệu HTML** bằng `HTMLDocument`.
* **Thu thập các `<svg>` nội tuyến** qua `get_elements_by_tag_name`.
* **Xác định các SVG bên ngoài** bằng bộ chọn CSS kết thúc bằng `.svg`.
* **Lưu mỗi phần** — ghi markup trực tiếp vào tệp hoặc sao chép tệp được tham chiếu.
* **Xử lý các trường hợp đặc biệt** như đường dẫn tương đối, trùng lặp và tệp thiếu.

Đó là toàn bộ câu trả lời cho **cách trích xuất SVG** từ một trang HTML, gói gọn trong một script dễ chỉnh sửa.

## Tiếp theo là gì?

Bây giờ bạn đã có thể **trích xuất SVG** một cách đáng tin cậy, hãy cân nhắc các ý tưởng tiếp theo:

* **Xử lý hàng loạt:** Lặp qua một thư mục các tệp HTML để xây dựng thư viện biểu tượng.
* **Tối ưu hoá:** Chạy mỗi SVG đã lưu qua SVGO (một công cụ tối ưu Node.js) để giảm kích thước tệp.
* **Chuyển đổi:** Dùng `cairosvg` hoặc `svglib` để chuyển SVG sang PNG cho các trình duyệt cũ.
* **Trích xuất metadata:** Phân tích các thẻ `<title>` hoặc `<desc>` trong mỗi SVG để tạo nhãn có thể tìm kiếm.

Mỗi chủ đề trên đều liên quan tới các từ khóa phụ của chúng tôi — **read HTML document**, **save svg files**, **save inline svg**, **extract svg from html** — vì vậy bạn sẽ có rất nhiều tài liệu để khám phá.

---

*Chúc bạn hacking vui vẻ! Nếu gặp khó khăn, hãy để lại bình luận bên dưới hoặc nhắn tin cho tôi trên GitHub. Thế giới SVG rộng lớn, nhưng với công cụ phù hợp, việc trích xuất chúng trở nên dễ dàng như ăn bánh.*


## Bạn nên học gì tiếp theo?

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Rendre un document SVG au format PNG dans .NET avec Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}