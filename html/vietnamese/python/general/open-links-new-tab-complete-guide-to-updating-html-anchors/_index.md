---
category: general
date: 2026-07-05
description: Mở liên kết trong tab mới bằng Python – học cách thêm `target="_blank"`,
  thay đổi mục tiêu liên kết, sử dụng bộ chọn chứa thuộc tính, và lưu HTML đã chỉnh
  sửa một cách dễ dàng.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: vi
og_description: Mở liên kết trong tab mới nhanh chóng. Hướng dẫn này chỉ cách thêm
  target="_blank", thay đổi mục tiêu liên kết và lưu HTML đã chỉnh sửa bằng Python.
og_title: Mở Liên Kết Trong Tab Mới – Hướng Dẫn Cập Nhật HTML Từng Bước
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: Mở Liên Kết Trong Tab Mới – Hướng Dẫn Toàn Diện Về Cập Nhật Thẻ Anchor HTML
url: /vi/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mở Liên Kết Trong Tab Mới – Hướng Dẫn Toàn Diện Để Cập Nhật Anchor HTML

Bạn đã bao giờ cần **open links new tab** trên một trang HTML tĩnh nhưng không chắc bắt đầu từ đâu chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp phải vấn đề này khi dọn dẹp các trang cũ hoặc thêm các cải tiến về khả năng truy cập. Trong hướng dẫn này, chúng tôi sẽ trình bày một giải pháp thực tế giúp **adds target blank**, **changes link target**, và an toàn **saves modified html**—tất cả chỉ với vài dòng Python.

Chúng tôi cũng sẽ hướng dẫn cách sử dụng **attribute contains selector** để bạn chỉ thao tác với những anchor thực sự cần thiết (ví dụ, mọi liên kết trỏ tới *example.com*). Khi kết thúc, bạn sẽ có một script có thể tái sử dụng và chèn vào bất kỳ dự án nào, dù lớn hay nhỏ.

## Những Điều Bạn Sẽ Học

- Tải một tệp HTML vào một đối tượng tài liệu có thể thao tác.  
- Chọn các phần tử `<a>` có thuộc tính `href` chứa một chuỗi con cụ thể.  
- **Add target blank** và đặt thuộc tính `rel="noopener"` để cải thiện bảo mật.  
- **Save modified html** trở lại đĩa mà không mất định dạng.  

Không có phụ thuộc bên ngoài nào ngoài thư viện chuẩn và **beautifulsoup4** (cài đặt rất nhẹ). Nếu bạn đã sử dụng một trình phân tích khác, các khái niệm vẫn áp dụng trực tiếp.

---

## Yêu Cầu Trước

- Python 3.8+ đã được cài đặt trên máy của bạn.  
- Hiểu biết cơ bản về HTML và Python.  
- `beautifulsoup4` package (`pip install beautifulsoup4`).  

Chỉ vậy—không cần bất kỳ framework nặng nào.

---

## Bước 1: Tải Tài Liệu HTML

Đầu tiên, chúng ta cần đọc tệp nguồn và truyền nó cho BeautifulSoup. Hãy nghĩ đây như mở một canvas trống nơi bạn có thể vẽ các thuộc tính mới.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Tại sao điều này quan trọng:** Sử dụng `Path` giữ cho mã không phụ thuộc vào hệ điều hành, và `html.parser` là bộ phân tích tích hợp, vì vậy bạn không cần trình phân tích bổ sung cho các tác vụ đơn giản.

---

## Bước 2: Sử Dụng Attribute Contains Selector Để Tìm Các Liên Kết Phù Hợp

Chúng ta chỉ muốn thao tác với các anchor trỏ tới *example.com*. Bộ chọn CSS `a[href*='example.com']` thực hiện đúng điều đó—`*=` có nghĩa là “chứa”. Phương thức `select` của BeautifulSoup hiểu cú pháp này.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Mẹo chuyên nghiệp:** Nếu bạn cần so khớp không phân biệt chữ hoa/thường, hãy chuyển sang một vòng lặp nhỏ kiểm tra `if 'example.com' in a.get('href', '').lower()`.

Bây giờ `anchor_elements` chứa mọi liên kết chúng ta quan tâm, sẵn sàng cho bước chuyển đổi tiếp theo.

---

## Bước 3: Thay Đổi Đích Liên Kết – Thêm Target Blank và Bảo Mật Liên Kết

Mở một liên kết trong tab mới đơn giản chỉ bằng cách đặt `target="_blank"`. Tuy nhiên, các trình duyệt hiện đại khuyến nghị cũng thêm `rel="noopener"` (hoặc `noreferrer`) để ngăn trang mới mở truy cập vào cửa sổ gốc qua `window.opener`. Thay đổi bảo mật nhỏ này có thể ngăn chặn các cuộc tấn công phishing.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Tại sao chúng ta dùng gán từ điển trực tiếp:** Nó tự động tạo thuộc tính nếu thiếu, và ghi đè nếu đã tồn tại—hoàn hảo cho thao tác **change link target**.

---

## Bước 4: Lưu HTML Đã Sửa Đổi Lại Vào Đĩa

Bước cuối cùng là ghi markup đã cập nhật vào một tệp mới. Giữ nguyên bản gốc không bị thay đổi cho phép bạn khôi phục nếu có sự cố.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **`prettify()` làm gì:** Nó định dạng HTML với thụt lề đẹp mắt, giúp tệp đã lưu dễ đọc và so sánh sau này hơn. Nếu bạn muốn giữ nguyên khoảng trắng gốc, thay thế `prettify()` bằng `str(soup)`.

---

## Đoạn Mã Đầy Đủ – Giải Pháp Một Nhấn

Dưới đây là đoạn script hoàn chỉnh, sẵn sàng chạy. Lưu lại với tên `update_links.py` và thực thi `python update_links.py` từ terminal của bạn.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### Kết Quả Dự Kiến

Giả sử `links.html` ban đầu chứa:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Sau khi chạy script, `links-updated.html` sẽ trông như sau:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Chỉ liên kết tới *example.com* mới nhận được các thuộc tính **add target blank**, chứng minh rằng **attribute contains selector** của chúng ta đã hoạt động đúng như mong đợi.

---

## Câu Hỏi Thường Gặp & Trường Hợp Cạnh

### Nếu một liên kết đã có thuộc tính `rel` thì sao?

Vòng lặp của chúng tôi sẽ ghi đè bằng `"noopener"`. Nếu bạn cần giữ lại các giá trị hiện có (ví dụ, `"nofollow"`), hãy nối chúng lại thay vì:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Làm thế nào để xử lý nhiều miền?

Chỉ cần mở rộng danh sách selector:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### `prettify()` có thay đổi cấu trúc HTML gốc không?

Nó chỉ thay đổi thụt lề mà không thay đổi thứ tự thẻ hay giá trị thuộc tính. Nếu bạn phải giữ nguyên khoảng trắng gốc, hãy thay thế `prettify()` bằng `str(soup)` như đã đề cập trước đó.

---

## Mẹo Chuyên Nghiệp Cho Script Sẵn Sàng Sản Xuất

- **Backup before overwriting:** Thêm bước sao chép (`shutil.copy`) để giữ tệp gốc an toàn.  
- **Logging instead of print:** Sử dụng mô-đun `logging` cho các dự án có khả năng mở rộng.  
- **Batch processing:** Lặp qua một thư mục bằng `Path.rglob("*.html")` để cập nhật nhiều tệp trong một lần chạy.  

Những điều chỉnh này biến một script **open links new tab** đơn giản thành một công cụ mạnh mẽ cho bất kỳ quy trình bảo trì web nào.

---

## Kết Luận

Bây giờ bạn đã có một phương pháp vững chắc, có thể tái sử dụng để **open links new tab** trên bất kỳ bộ sưu tập HTML tĩnh nào. Bằng cách tận dụng **attribute contains selector**, bạn có thể **change link target** một cách chính xác ở nơi cần, **add target blank**, và **save modified html** mà không mất định dạng.

Hãy thử trên một trang thử nghiệm, sau đó mở rộng ra toàn bộ site của bạn. Cần điều chỉnh selector cho PDF, hoặc các miền khác? Chỉ cần thay đổi chuỗi CSS—các phần còn lại vẫn giữ nguyên.

Bạn cứ thoải mái để lại bình luận nếu gặp bất kỳ vấn đề nào, hoặc chia sẻ cách bạn mở rộng script cho dự án của mình. Chúc lập trình vui vẻ, và hy vọng mọi anchor của bạn luôn mở đúng nơi bạn muốn!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng dựa trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Chỉnh Sửa HTML Bằng Aspose.HTML cho Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Cách Thêm CSS – CSS Nội Tuyến vào Tài Liệu HTML trong Aspose.HTML cho Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}