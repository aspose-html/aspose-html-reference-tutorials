---
category: general
date: 2026-10-21
description: Tìm hiểu cách phân tích HTML bằng Python, tải tài liệu HTML, sử dụng
  bộ chọn CSS và nhanh chóng trích xuất các liên kết từ HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: vi
lastmod: 2026-10-21
og_description: Cách phân tích HTML trong Python bằng các bộ chọn CSS. Tải tài liệu
  HTML, chọn các liên kết và trích xuất siêu liên kết từ HTML với mã sạch sẽ.
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: Cách phân tích HTML trong Python – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: Cách phân tích HTML trong Python bằng bộ chọn CSS
url: /vi/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách phân tích HTML trong Python bằng bộ chọn CSS

Nếu bạn cần **cách phân tích html** trong một script Python, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Bạn sẽ học cách tải một tài liệu HTML, cách sử dụng cú pháp selector để tìm phần tử, và cách trích xuất các liên kết từ html mà không phải viết parser tùy chỉnh.

Phân tích HTML là một nhiệm vụ phổ biến cho các scraper web, pipeline phân tích dữ liệu, hoặc kiểm thử tự động. Khi kết thúc tutorial này, bạn sẽ có một hàm tái sử dụng được để tải tài liệu HTML, chọn tất cả các thẻ `<a>` bằng bộ chọn CSS, và trả về một danh sách URL sạch sẽ.

## Những gì bạn cần

- Python 3.8+ (mã chạy trên bất kỳ phiên bản gần đây nào)  
- Thư viện **lxml** (`pip install lxml`) – cung cấp khả năng phân tích HTML nhanh và hỗ trợ bộ chọn CSS  
- Một file HTML bạn muốn phân tích (ví dụ, `sample.html`)  

Không cần công cụ bổ sung nào; mọi thứ chạy với thư viện chuẩn và một gói bên thứ ba duy nhất.

## Bước 1: Cách phân tích HTML – tải tài liệu

Bước đầu tiên trong bất kỳ quy trình làm việc với HTML nào là đọc file vào bộ nhớ. Sử dụng **lxml.html** sẽ cho bạn một đối tượng cây hỗ trợ bộ chọn CSS.

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**Tại sao điều này quan trọng:**  
`load_html` trừu tượng hoá phần boilerplate đọc file và đảm bảo tài liệu được phân tích bằng một parser HTML chịu lỗi. Đây là cách an toàn nhất để **load html document python** mà không lo về markup sai cấu trúc.

## Bước 2: Cách sử dụng selector – tìm tất cả các phần tử liên kết

Sau khi tài liệu đã được tải, bạn có thể dùng một bộ chọn CSS để xác định mọi thẻ `<a>`. Bộ chọn `"a"` khớp với tất cả các phần tử anchor, nhưng bạn có thể tinh chỉnh (ví dụ, `"a.external"` hoặc `"nav a"`).

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**Tại sao điều này quan trọng:**  
Cách **how to use selector** cho phép bạn diễn đạt các truy vấn phức tạp trong một chuỗi duy nhất, dễ đọc, tránh việc duyệt cây thủ công. Nó hoạt động với bất kỳ mẫu CSS nào được `lxml.cssselect` hỗ trợ.

## Bước 3: Trích xuất hyperlink từ HTML và xử lý chúng

Bây giờ bạn đã có danh sách các phần tử `<a>`, bạn có thể lấy thuộc tính `href` từ mỗi phần tử. Trợ giúp dưới đây cũng chuẩn hoá URL tương đối dựa trên một base URL (nếu bạn cung cấp).

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**Kết quả mong đợi** (giả sử `sample.html` chứa ba liên kết):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**Tại sao điều này quan trọng:**  
`extract_hyperlinks` là lõi của **extract hyperlinks from html**. Nó xử lý một cách nhẹ nhàng các trường hợp thiếu thuộc tính `href`, giải quyết các liên kết tương đối, và trả về một danh sách Python thuần mà bạn có thể đưa vào các bước xử lý tiếp theo (ví dụ, requests, pandas, hoặc cơ sở dữ liệu).

## Ví dụ toàn diện từ đầu đến cuối

Kết hợp ba hàm lại với nhau sẽ cho bạn một script duy nhất tải file, chọn tất cả các anchor, và in ra mỗi hyperlink.

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

Chạy `python parse_links.py` sẽ in ra mọi hyperlink, đã được giải quyết đầy đủ, trên console. Script này minh họa **how to parse html**, **how to use selector**, và **extract hyperlinks from html** trong một luồng công việc tái sử dụng.

## Các biến thể phổ biến và xử lý trường hợp biên

| Tình huống | Cần thay đổi | Lý do |
|-----------|--------------|-------|
| **Chỉ cần URL tuyệt đối** | Bỏ qua đối số `base_url` trong `extract_hyperlinks` | Giữ nguyên các URL tương đối |
| **Bạn cần cả văn bản liên kết** | Trả về một tuple `(href, link.text_content())` từ `extract_hyperlinks` | Cho phép lưu cả URL và nội dung anchor |
| **File HTML lớn** | Sử dụng `lxml.etree.iterparse` với bộ lọc selector CSS | Giảm sử dụng bộ nhớ bằng cách streaming |
| **Selector khác** | Thay `"a"` bằng `"nav a[href]"` hoặc `"div.content a.external"` | Nhắm tới một tập con các liên kết, hữu ích cho **how to use selector** trong các trang phức tạp |

**Mẹo:** Luôn xác thực các URL đã trích xuất trước khi thực hiện các yêu cầu mạng. Kiểm tra nhanh bằng `urlparse` có thể lọc bỏ các chuỗi sai định dạng và bảo vệ scraper của bạn khỏi lỗi.

## Kết luận

Bây giờ bạn đã biết **how to parse html** trong Python, cách **load html document python**, cách **how to use selector** để nhắm mục tiêu các phần tử, và cách **extract hyperlinks from html** một cách hiệu quả. Ví dụ hoàn chỉnh ở trên đã sẵn sàng để sao chép‑dán vào dự án của bạn, và bạn có thể điều chỉnh mỗi hàm để phù hợp với các trường hợp sử dụng nâng cao hơn như phân trang, nội dung được tạo bởi JavaScript, hoặc thu thập đa trang.

Các bước tiếp theo bạn có thể khám phá bao gồm:

- Sử dụng **requests‑html** hoặc **Playwright** để lấy các trang cần thực thi JavaScript.  
- Lưu các URL đã trích xuất vào CSV hoặc cơ sở dữ liệu SQLite để phân tích sau.  
- Thêm xử lý lỗi cho timeout mạng và mã trạng thái HTTP.

Chúc bạn phân tích thành công, và đừng ngại thử nghiệm các selector khác nhau để khai thác tối đa sức mạnh của truy vấn HTML dựa trên CSS trong Python!


## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to configure HTML resource handling in Python and load an HTML document](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [How to Parse HTML in Python – Complete Guide](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [How to Load HTML in Python – Step‑by‑Step Guide](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}