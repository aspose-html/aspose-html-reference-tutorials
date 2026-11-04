---
category: general
date: 2026-05-28
description: Cách phân tích HTML trong Python nhanh chóng—tải tệp HTML, sử dụng bộ
  chọn CSS và trích xuất các thuộc tính href bằng ví dụ XPath chứa.
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: vi
og_description: 'Cách phân tích HTML bằng Python: học cách tải tệp HTML, sử dụng bộ
  chọn CSS và lấy thuộc tính href với ví dụ XPath chứa.'
og_title: Cách phân tích HTML trong Python – Từng bước
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: Cách phân tích HTML trong Python – Hướng dẫn toàn diện
url: /vi/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Phân Tích HTML trong Python – Hướng Dẫn Toàn Diện

Bạn có bao giờ tự hỏi **cách phân tích HTML** trong một script Python mà không cần tải một trình duyệt nặng? Bạn không phải là người duy nhất. Hầu hết chúng ta chỉ cần **tải tệp HTML**, thu thập một vài tiêu đề, và có thể lấy một hoặc hai liên kết tải xuống. Trong hướng dẫn này, tôi sẽ chỉ cho bạn cách làm đó—sử dụng một thư viện nhỏ, một CSS selector, và một ví dụ XPath contains để **lấy giá trị thuộc tính href**.

Chúng ta sẽ đi qua toàn bộ quá trình, từ việc đọc một tài liệu HTML cục bộ đến việc in ra dữ liệu bạn quan tâm. Không có phần thừa, chỉ có một ví dụ thực tế, có thể chạy ngay mà bạn có thể đưa vào dự án của mình ngay hôm nay.

## Những Điều Bạn Sẽ Học

- Cách **tải một tệp HTML** bằng một parser nhẹ.
- Cách **sử dụng cú pháp CSS selector** để lấy các phần tử như tiêu đề bài viết.
- Cách tạo một **ví dụ XPath contains** để lọc các liên kết.
- Cách an toàn **lấy giá trị thuộc tính href** từ các node khớp.
- Mẹo xử lý markup bị hỏng và mở rộng script.

Bạn chỉ cần Python 3.8+ và các gói `lxml` và `cssselect`—cả hai đều có thể cài đặt bằng một lệnh `pip` duy nhất.

---

## Bước 1: Tải Tệp HTML

Trước hết, bạn cần nội dung HTML trong bộ nhớ. Module `lxml.html` cung cấp một helper tiện lợi `fromstring`, nhưng khi bạn có một tệp trên đĩa, hàm `parse` còn gọn hơn.

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **Tại sao điều này quan trọng:** Việc tải tệp một lần giúp giảm sử dụng bộ nhớ và cung cấp cho bạn một đối tượng `root` duy nhất hỗ trợ cả CSS selector và truy vấn XPath. Nếu tệp bị thiếu hoặc không đọc được, `html.parse` sẽ ném ra một `OSError` rõ ràng, bạn có thể bắt lại sau.

### Mẹo chuyên nghiệp
Nếu bạn đang làm việc với một chuỗi thay vì tệp, hãy thay `html.parse` bằng `html.fromstring(your_html_string)`.

---

## Bước 2: Sử Dụng CSS Selector Để Lấy Tiêu Đề

CSS selector ngắn gọn và quen thuộc với bất kỳ ai đã viết stylesheet. Hãy lấy mọi thẻ `<h2>` bên trong `<article>`—hoàn hảo cho tiêu đề tin tức.

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**Kết quả mong đợi** (giả sử HTML mẫu chứa hai bài viết):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **Tại sao lại dùng CSS?** Nó dễ đọc, nhanh, và hoạt động ngay với `lxml`. Phương thức `cssselect` chuyển selector thành một biểu thức XPath ngầm, cho bạn lợi thế của cả hai.

---

## Bước 3: Ví dụ XPath Contains – Tìm Các Liên Kết “download”

Đôi khi bạn cần kiểm soát chi tiết hơn so với CSS. Hàm `contains()` của XPath tỏa sáng khi bạn muốn khớp một chuỗi con trong một thuộc tính, như tất cả các liên kết trỏ tới một file tải xuống.

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**Kết quả mẫu**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **Tại sao lại dùng XPath contains?** Nó cho phép bạn lọc trực tiếp trên giá trị thuộc tính mà không cần vòng lặp Python thêm. Đây là **ví dụ xpath contains** cổ điển mà bạn thường thấy trong các hướng dẫn, nhưng ở đây nó được kết hợp với một trường hợp thực tế.

---

## Bước 4: Gói Gọn Tất Cả Vào Một Hàm Có Thể Tái Sử Dụng

Việc hard‑code đường dẫn và in ra là ổn cho một thử nghiệm nhanh, nhưng mã sản xuất thích các hàm. Dưới đây là một helper gọn gàng trả về cả tiêu đề và liên kết tải xuống.

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

Bạn có thể gọi hàm và in đẹp kết quả:

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

Chạy script sẽ cho ra cùng kết quả như trước, nhưng bây giờ nó được đóng gói gọn gàng để tái sử dụng.

---

## Bước 5: Xử Lý Các Trường Hợp Cạnh và Những Cạm Bẫy Thông Thường

1. **Thiếu thuộc tính `href`** – XPath vẫn sẽ trả về node `<a>` ngay cả khi `href` không có. Hãy bảo vệ khỏi `None`:

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **URL tương đối vs. tuyệt đối** – Nếu các liên kết của bạn là tương đối, bạn có thể muốn giải quyết chúng dựa trên URL gốc:

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **HTML bị hỏng** – `lxml` khá khoan dung, nhưng markup quá hỏng có thể khiến `html.parse` ném ra `XMLSyntaxError`. Hãy bao quanh lời gọi parse trong khối `try/except` để ghi log và bỏ qua các tệp có vấn đề.

4. **Hiệu suất với tệp lớn** – Đối với các trang đa megabyte, hãy cân nhắc streaming với `iterparse` thay vì tải toàn bộ DOM vào bộ nhớ.

---

## Tổng Quan Trực Quan (tùy chọn)

![Sơ đồ luồng cách phân tích HTML cho thấy tải tệp → CSS selector → XPath contains → lấy thuộc tính href](how-to-parse-html-flow.png "Sơ đồ luồng cách phân tích HTML")

*Văn bản thay thế bao gồm từ khóa chính để đáp ứng SEO.*

---

## Kết Luận

Chúng ta đã bao quát **cách phân tích HTML** trong Python từ đầu đến cuối: tải một tệp HTML, sử dụng CSS selector để lấy tiêu đề bài viết, tạo một ví dụ XPath contains để tìm các liên kết tải xuống, và cuối cùng **lấy giá trị thuộc tính href** một cách an toàn. Hàm `parse_news_html` có thể tái sử dụng cho thấy một cách tiếp cận sạch sẽ, dễ bảo trì mà bạn có thể áp dụng cho bất kỳ nhiệm vụ scraping nào.

Sẵn sàng cho thử thách tiếp theo? Hãy thử mở rộng script để:

- Phân tích bảng với truy vấn XPath `//table//tr`.
- Trích xuất thuộc tính `src` của hình ảnh bằng một **ví dụ xpath contains** khác.
- Chuyển sang lấy dữ liệu bất đồng bộ với `aiohttp` cho các trang web trực tiếp.

Chúc bạn parsing vui vẻ, và nhớ—khi bạn đã nắm vững những kiến thức cơ bản này, phần còn lại của việc scraping HTML sẽ trở nên dễ dàng. Nếu gặp bất kỳ vấn đề nào, hãy để lại bình luận bên dưới—cùng nhau giải quyết!

## Các Hướng Dẫn Liên Quan

- [Tải Tài Liệu HTML từ Tệp trong Aspose.HTML cho Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Cách Chỉnh Sửa Cây Tài Liệu HTML trong Aspose.HTML cho Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Cách Thêm CSS – CSS Nội Tuyến vào Tài Liệu HTML trong Aspose.HTML cho Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}