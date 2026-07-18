---
category: general
date: 2026-07-18
description: Chuyển đổi HTML sang EPUB trong Python một cách nhanh chóng. Tìm hiểu
  cách tải tệp HTML trong Python và cũng chuyển đổi HTML sang MHTML bằng các thư viện
  đơn giản.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: vi
lastmod: 2026-07-18
og_description: Chuyển đổi HTML sang EPUB trong Python với ví dụ rõ ràng, có thể chạy
  được. Cũng học cách tải tệp HTML trong Python và chuyển đổi HTML sang MHTML trong
  vài phút.
og_image_alt: Diagram showing convert html to epub workflow
og_title: Chuyển đổi HTML sang EPUB bằng Python – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: Chuyển đổi HTML sang EPUB trong Python – Hướng dẫn chi tiết từng bước
url: /vi/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển đổi HTML sang EPUB trong Python – Hướng dẫn chi tiết từng bước

Bạn đã bao giờ tự hỏi làm sao **chuyển đổi HTML sang EPUB** mà không phải rối rắm? Bạn không phải là người duy nhất—các nhà phát triển luôn cần biến các trang web thành sách điện tử để đọc offline, và việc này trong Python lại khá dễ dàng. Trong hướng dẫn này, chúng ta sẽ cùng nhau tải một tệp HTML trong Python, chuyển đổi HTML sang EPUB, và thậm chí chuyển cùng một nguồn thành MHTML để lưu trữ thân thiện với email.

Khi hoàn thành, bạn sẽ có một script sẵn sàng chạy, nhận vào một tệp `sample.html` và tạo ra cả `sample.epub` và `sample.mhtml`. Không có bí ẩn, chỉ có mã rõ ràng và giải thích chi tiết.

---

![Conversion pipeline diagram](https://example.com/images/convert-html-epub.png "Diagram showing convert html to epub workflow")

## Những gì bạn sẽ xây dựng

- **Tải một tệp HTML trong Python** bằng các module tích hợp `pathlib` và `io`.  
- **Chuyển đổi HTML sang EPUB** bằng thư viện `ebooklib`, thư viện này sẽ lo phần định dạng container EPUB cho bạn.  
- **Chuyển đổi HTML sang MHTML** (còn gọi là MHT) bằng gói `email`, tạo một tệp lưu trữ web dạng một file mà trình duyệt có thể mở trực tiếp.  

Chúng ta cũng sẽ đề cập tới:

- Các phụ thuộc cần thiết và cách cài đặt chúng.  
- Xử lý lỗi để script của bạn không bị sập đột ngột.  
- Cách tùy chỉnh siêu dữ liệu như tiêu đề và tác giả cho tệp EPUB.  

Sẵn sàng chưa? Hãy bắt đầu.

---

## Yêu cầu trước

Trước khi viết code, hãy chắc chắn bạn đã có:

1. **Python 3.9+** – cú pháp ở đây hoạt động trên bất kỳ phiên bản Python mới nào.  
2. **pip** – để cài đặt các package của bên thứ ba.  
3. Một tệp HTML đơn giản, ví dụ `sample.html`, đặt trong một thư mục bạn quản lý.  

Nếu bạn đã có những thứ trên, tuyệt vời—tiếp tục tới phần tiếp theo.  

> **Mẹo chuyên nghiệp:** Giữ HTML của bạn được viết đúng chuẩn (có phần `<head>` và `<body>` đầy đủ). Mặc dù `ebooklib` sẽ cố gắng sửa các lỗi nhỏ, một nguồn sạch sẽ sẽ giảm thiểu rắc rối sau này.

---

## Bước 1 – Cài đặt các thư viện cần thiết

Chúng ta cần hai package bên ngoài:

- **ebooklib** – để tạo EPUB.  
- **beautifulsoup4** – không bắt buộc, nhưng rất hữu ích để làm sạch HTML trước khi chuyển đổi.

Chạy lệnh sau trong terminal của bạn:

```bash
pip install ebooklib beautifulsoup4
```

> **Tại sao lại chọn các thư viện này?** `ebooklib` xây dựng cấu trúc EPUB dựa trên ZIP cho bạn, tự động tạo thư mục `META‑INF`, tệp `content.opf`, và `toc.ncx`. `beautifulsoup4` giúp chúng ta dọn dẹp HTML, đảm bảo sách điện tử cuối cùng hiển thị đúng trên mọi thiết bị đọc.

---

## Bước 2 – Tải tệp HTML trong Python

Việc tải một tệp HTML rất đơn giản, nhưng chúng ta sẽ gói nó trong một hàm trợ giúp nhỏ trả về một đối tượng **BeautifulSoup** để xử lý sau.

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**Giải thích:**  
- `Path` cung cấp cách xử lý tệp độc lập với hệ điều hành.  
- Dùng `read_text` tránh việc phải viết mã `open`/`close` thủ công.  
- Trả về một đối tượng `BeautifulSoup` cho phép chúng ta loại bỏ script, sửa các thẻ bị hỏng, hoặc chèn stylesheet trước khi **chuyển đổi HTML sang EPUB**.

---

## Bước 3 – Chuyển đổi HTML sang EPUB

Bây giờ chúng ta đã có thể **tải HTML trong Python**, hãy biến nó thành một EPUB sạch sẽ. Hàm dưới đây nhận vào một đối tượng `BeautifulSoup`, đường dẫn đích, và các siêu dữ liệu tùy chọn.

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**Tại sao cách này hoạt động:**  
- `ebooklib.epub.EpubBook` trừu tượng hoá container ZIP và các tệp manifest bắt buộc.  
- Chúng ta tạo một UUID làm định danh để tránh trùng lặp khi tạo nhiều sách.  
- `spine` chỉ định thứ tự các chương; một cuốn sách một chương là đủ cho hầu hết các nguồn HTML đơn giản.  

**Chạy chuyển đổi:**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

Khi thực thi script, bạn sẽ thấy một dấu kiểm màu xanh lá xác nhận vị trí tệp EPUB đã được tạo.

---

## Bước 4 – Chuyển đổi HTML sang MHTML

MHTML (hoặc MHT) gói HTML và tất cả tài nguyên (hình ảnh, CSS) vào một tệp MIME duy nhất. Gói `email` của Python có thể xây dựng định dạng này mà không cần phụ thuộc bên ngoài.

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**Các điểm quan trọng:**  

- Kiểu MIME `multipart/related` thông báo cho trình duyệt rằng phần HTML và các tài nguyên của nó thuộc cùng một nhóm.  
- Chúng ta lặp qua các thẻ `<img>` để nhúng hình ảnh; nếu không cần hình ảnh, có thể bỏ qua khối này.  
- `Content-Location` sử dụng URI `file://` để trình duyệt có thể giải quyết tài nguyên nội bộ.  

**Gọi hàm:**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

Bây giờ bạn có cả `sample.epub` và `sample.mhtml` nằm cạnh nhau.

---

## Script đầy đủ – Tất cả các bước trong một file

Dưới đây là script hoàn chỉnh, sẵn sàng chạy, kết hợp mọi thứ lại. Lưu lại với tên `convert_html.py` và thay `YOUR_DIRECTORY` bằng đường dẫn chứa `sample.html` của bạn.

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
convert_html.py

A tiny utility that demonstrates:
- How to load an HTML file in Python
- How to convert HTML to EPUB (convert html to epub)
- How to convert HTML to MHTML (convert html to mhtml)

Author: Your Name
Date: 2026‑07‑18
"""

from pathlib import Path
import uuid
import mimetypes


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Convert EPUB to PDF with Java – Using Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [How to Convert EPUB to Images with Aspose.HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}