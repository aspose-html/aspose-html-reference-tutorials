---
category: general
date: 2026-07-02
description: Cách trích xuất biểu tượng từ tệp HTML bằng Python. Học cách đọc tệp
  HTML bằng Python, phân tích tài liệu HTML và trích xuất thuộc tính href để lấy URL
  của favicon.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: vi
og_description: Cách trích xuất biểu tượng từ trang HTML bằng Python. Hướng dẫn này
  cho bạn biết cách đọc tệp HTML bằng Python, phân tích tài liệu và lấy URL của favicon.
og_title: Cách Trích xuất biểu tượng từ HTML – Hướng dẫn Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: Cách trích xuất biểu tượng từ HTML bằng Python – Hướng dẫn toàn diện
url: /vi/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Trích Xuất Icon từ HTML bằng Python – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi **cách trích xuất icon** từ một trang web mà không cần mở trình duyệt chưa? Có thể bạn đang xây dựng một danh mục site, một công cụ kiểm tra SEO, hoặc chỉ đơn giản tò mò về những favicon nhỏ xuất hiện trên các tab. Tin tốt là bạn có thể thực hiện điều này chỉ trong vài dòng Python—không cần Selenium, không cần Chrome headless, chỉ một tệp HTML dạng văn bản thuần.

Trong hướng dẫn này, chúng ta sẽ đi qua việc đọc một tệp HTML bằng Python, phân tích tài liệu HTML, và cuối cùng **trích xuất thuộc tính href** từ các thẻ `<link rel="icon">` để lấy các URL favicon. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng cho bất kỳ HTML tĩnh nào, và bạn cũng sẽ thấy cách xử lý các trường hợp đặc biệt như đường dẫn tương đối hoặc nhiều khai báo icon.

## Những Điều Bạn Sẽ Học

- Tải một tệp HTML cục bộ bằng Python (read html file python)  
- Sử dụng một trình phân tích nhẹ để **phân tích tài liệu html** một cách an toàn  
- Xác định các phần tử `<link>` khai báo một icon  
- **Trích xuất giá trị thuộc tính href** và chuyển chúng thành URL tuyệt đối  
- Thu thập và in ra tất cả các **URL favicon** đã phát hiện  

Không cần dịch vụ bên ngoài—chỉ cần thư viện chuẩn và gói **BeautifulSoup** phổ biến.

---

![Ảnh chụp màn hình cho thấy script Python trích xuất icon – cách trích xuất icon](https://example.com/images/extract-icons-python.png "cách trích xuất icon")

*Văn bản alt hình ảnh: "cách trích xuất icon bằng script Python"*

## Yêu Cầu Trước

- Python 3.8+ đã được cài đặt  
- `beautifulsoup4` thư viện (`pip install beautifulsoup4`)  
- Một tệp HTML cục bộ mà bạn muốn quét (ví dụ: `sample.html`)  

Nếu bạn đã có những thứ này, hãy bắt đầu.

## Bước 1: Đọc Tệp HTML bằng Python – Tải Tài Liệu

Đầu tiên, chúng ta cần mở tệp và đưa nội dung của nó cho trình phân tích. Sử dụng `with open(..., "r", encoding="utf‑8")` đảm bảo tệp được đóng tự động, và mã hóa UTF‑8 xử lý hầu hết các trang hiện đại.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Tại sao điều này quan trọng:** Mở tệp với mã hóa đúng ngăn ngừa các ký tự `�` bí ẩn có thể làm trình phân tích gặp lỗi sau này. Sử dụng `Path` từ thư viện chuẩn cũng giúp mã chạy đa nền tảng.

## Bước 2: Phân Tích Tài Liệu HTML – Tìm Tất Cả Các Liên Kết Icon

Bây giờ chúng ta truyền HTML thô cho **BeautifulSoup**, công cụ này xây dựng một cây có thể duyệt được. Chúng ta sẽ tìm mọi thẻ `<link>` mà thuộc tính `rel` chứa từ `icon`. Lưu ý rằng `rel` có thể là danh sách phân tách bằng dấu cách (`rel="shortcut icon"`), vì vậy chúng ta cần một kiểm tra linh hoạt.

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**Tại sao bước này quan trọng:** Một câu lệnh `soup.find_all("link", rel="icon")` đơn giản sẽ bỏ qua các biến thể như `rel="shortcut icon"` hoặc `rel="apple-touch-icon"`. Hàm trợ giúp `is_icon_link` của chúng ta bao phủ những trường hợp đó, làm cho việc trích xuất trở nên vững chắc.

## Bước 3: Trích Xuất Thuộc Tính href – Lấy Các URL

Với các thẻ liên quan đã được thu thập, chúng ta bây giờ lấy thuộc tính `href` từ mỗi thẻ. Một số trang có thể không có `href` (hiếm, nhưng có thể), vì vậy chúng ta kiểm tra tránh `None`. Thêm nữa, favicon thường được chỉ định bằng URL tương đối, vì vậy chúng ta sẽ giải quyết chúng dựa trên URL cơ sở của trang nếu bạn biết. Đối với tệp cục bộ, chúng ta sẽ giữ nguyên đường dẫn.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Tại sao chúng ta loại bỏ khoảng trắng:** Các tác giả HTML đôi khi vô tình thêm khoảng trắng quanh URL, điều này sẽ làm hỏng yêu cầu tiếp theo. Việc cắt bỏ đảm bảo chúng ta có được chuỗi sạch.

## Bước 4: Trích Xuất URL Favicon – Xuất Kết Quả

Cuối cùng, chúng ta in (hoặc trả về) danh sách các URL đã phát hiện. Trong một script thực tế, bạn có thể ghi chúng vào CSV, tải xuống các icon, hoặc đưa chúng vào một dịch vụ khác. Dưới đây là một vòng lặp đơn giản hiển thị kết quả trên console.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Xử Lý Các Trường Hợp Đặc Biệt

- **Nhiều giá trị rel:** Kiểm tra `is_icon_link` của chúng ta đã bắt được `rel="shortcut icon"` và `rel="apple-touch-icon"`.  
- **Đường dẫn tương đối:** Nếu sau này bạn cần URL tuyệt đối, hãy dùng `urllib.parse.urljoin(base_url, href)`.  
- **Thiếu href:** Điều kiện `if href:` sẽ bỏ qua các thẻ sai định dạng, tránh lỗi `NoneType`.  
- **Các mục trùng lặp:** Bạn có thể dùng `icon_urls = list(dict.fromkeys(icon_urls))` để loại bỏ trùng lặp.

---

## Script Đầy Đủ – Giải Pháp Một Cửa

Kết hợp tất cả lại, đây là chương trình hoàn chỉnh, sẵn sàng chạy. Lưu nó dưới tên `extract_icons.py` và chỉ định `html_path` tới bất kỳ tệp nào bạn muốn.

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**Kết quả mong đợi** (giả sử `sample.html` chứa hai icon):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Chạy nó bằng `python extract_icons.py` và bạn sẽ thấy các URL được in ra console.

---

## Câu Hỏi Thường Gặp

**Q: Nếu HTML sử dụng thẻ `<meta>` cho icon thì sao?**  
A: Một số trang nhúng icon qua `<meta itemprop="image">`. Mở rộng `is_icon_link` để cũng kiểm tra `meta` với `itemprop="image"` và lấy thuộc tính `content` của nó.

**Q: Tôi có thể tự động tải các icon không?**  
A: Có—chỉ cần đưa mỗi URL vào `requests.get(url, stream=True)` và ghi nội dung ra file. Nhớ xử lý các URL tương đối bằng `urljoin`.

**Q: Điều này có hoạt động trên các trang từ xa không?**  
A: Hoàn toàn có. Thay bước đọc tệp bằng `requests.get(page_url).text` và truyền chuỗi HTML cho BeautifulSoup. Chỉ cần chú ý tới robots.txt và giới hạn tần suất yêu cầu.

## Tổng Kết

Chúng ta đã trình bày **cách trích xuất icon** từ bất kỳ HTML tĩnh nào bằng Python, từ việc đọc tệp đến việc in ra mỗi URL favicon. Các ý tưởng cốt lõi—đọc tệp, phân tích tài liệu, xác định các thẻ đúng, và lấy thuộc tính `href`—là các mẫu có thể tái sử dụng mà bạn sẽ gặp trong nhiều nhiệm vụ web‑scraping.

Bước tiếp theo? Hãy thử mở rộng script để:

- Giải quyết các URL tương đối dựa trên URL cơ sở của trang  
- Tải xuống mỗi icon và lưu cục bộ  
- Hỗ trợ các định dạng icon bổ sung (`rel="mask-icon"` cho Safari)  

Hãy thoải mái thử nghiệm, và nếu bạn gặp bất kỳ vấn đề nào, hãy để lại bình luận bên dưới. Chúc bạn parsing vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao quát các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Truy Vấn HTML trong Java – Hướng Dẫn Toàn Diện](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Cách Chỉnh Sửa Cây Tài Liệu HTML trong Aspose.HTML cho Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Lưu Tài Liệu HTML vào Tệp trong Aspose.HTML cho Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}