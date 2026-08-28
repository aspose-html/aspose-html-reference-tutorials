---
category: general
date: 2026-05-31
description: Python을 사용하여 id로 요소를 가져오고, HTML 배경색을 변경하며, HTML 텍스트를 읽고, HTML 속성을 설정하는
  방법을 배웁니다. 단계별 튜토리얼.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: ko
og_description: Python을 사용해 ID로 요소를 가져오고, HTML 텍스트를 읽으며, HTML 속성을 설정하고 배경 색을 변경하는
  방법을 한 번에 따라하기 쉬운 가이드.
og_title: Python에서 ID로 요소 가져오기 – 전체 HTML 조작 튜토리얼
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
title: Python에서 ID로 요소 가져오기 – 완전한 HTML 조작 가이드
url: /ko/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 id로 요소 가져오기 – 완전한 HTML 조작 가이드

빠른 Python 스크립트를 작성하면서 HTML 페이지에서 **get element by id**가 필요했던 적이 있나요? 당신만 그런 것이 아닙니다—대부분의 개발자는 사이트를 크롤링하거나 로컬 보고서를 수정하기 시작할 때 바로 그 장애물에 부딪힙니다. 좋은 소식은? 몇 줄의 코드만으로 요소의 텍스트를 읽고, 배경 색을 변경하고, 새로운 속성을 설정할 수 있으며, 모두 편집기를 떠나지 않고 할 수 있다는 것입니다.

이 튜토리얼에서는 실제 예제를 단계별로 살펴보겠습니다: 로컬 `sample.html`을 로드하고, ID가 `main‑content`인 요소를 가져와 내부 텍스트를 출력한 뒤, 배경 색을 연한 회색으로 바꾸는 과정입니다. 마지막까지 하면 **how to read HTML text**, **how to set HTML attribute**, 그리고 **manipulate HTML with Python**이 자동화 도구 상자에서 얼마나 유용한 기술인지 알게 될 것입니다.

## 필요 사항

- **Python 3.9+** (any recent version works)
- The **`lxml`** library (or **BeautifulSoup** if you prefer) – we’ll use `lxml.html` because it gives a clean `get_element_by_id`‑style API.
- A tiny HTML file named `sample.html` sitting in a folder called `YOUR_DIRECTORY`. Feel free to copy the snippet below into that file:

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

That’s it—no fancy frameworks, just plain Python and a static HTML file.

## 단계 1: 필요한 라이브러리 설치

If you haven’t installed `lxml` yet, fire up a terminal and run:

```bash
pip install lxml
```

*Pro tip:* Using a virtual environment keeps your global Python tidy, especially when you start juggling multiple projects.

## 단계 2: HTML 문서 로드

Now we’ll read the file into an `lxml.html` document object. Think of this as turning the raw text into a navigable tree.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

Running this prints “Document loaded successfully.” If the file can’t be found, Python will raise a `FileNotFoundError`—good to catch early before you chase a phantom element.

## 단계 3: id로 요소 가져오기

Here’s the heart of the matter. `lxml` gives us a convenient `get_element_by_id` method that mirrors the DOM API you’d use in JavaScript.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

When the element exists, you’ll see “Element found!” printed to the console. This is the **get element by id** step that powers most of our later manipulations.

## 단계 4: HTML 텍스트 읽는 방법

Once you have the element, extracting its visible text is a breeze. The `text_content()` method returns everything inside, stripped of tags.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Expected output:

```
Inner text: Hello, world! This is the original text.
```

You might wonder, *what if the element contains nested tags?* `text_content()` still works—it concatenates all descendant text nodes, giving you a clean string you can log, store, or feed into another algorithm.

## 단계 5: HTML 속성 설정 방법

Changing or adding attributes is just as straightforward. The `set` method lets you assign any attribute name you like.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Output:

```
New attribute value: true
```

That line demonstrates **how to set HTML attribute** on the fly. You can replace `"data-modified"` with `"class"`, `"title"` or any other attribute the element supports.

## 단계 6: HTML 배경 색 변경

Now for the visual tweak. To change the background colour, we inject a `style` attribute that overrides the default.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

After running the script, the `div` in `sample.html` will look like this when you open it in a browser:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

That’s the **change background colour html** technique you can reuse for any element—just swap the colour code.

## 단계 7: Python으로 HTML 조작 – 전체 예제

Below is the full, runnable script that combines every step. Save it as `modify_html.py` and execute it from the same directory as your `YOUR_DIRECTORY` folder.

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

### 스크립트가 수행하는 작업, 한 줄씩

1. **Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.  
2. **Loads** `sample.html` and aborts with a clear error if the file is missing.  
3. **Retrieves** the element using **get element by id**.  
4. **Prints** the element’s text—showing **how to read HTML text**.  
5. **Adds** a custom attribute, illustrating **how to set HTML attribute**.  
6. **Changes** the background colour, fulfilling the **change background colour html** requirement.  
7. **Writes** the updated markup to `sample_modified.html`, so you can open it in a browser and see the changes.

Running the script yields console output similar to:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

Open `sample_modified.html` and you’ll notice the gray background behind the text—proof that **manipulate HTML with python** really works.

## 흔히 발생하는 실수와 회피 방법

- **Missing ID** – If the target element doesn’t exist, `get_element_by_id` returns `None`. Always check for `None` before accessing properties; otherwise you’ll hit an `AttributeError`.  
- **Encoding issues** – When reading non‑ASCII pages, pass `encoding='utf-8'` to `html.parse` or ensure your file is saved in UTF‑8.  
- **Overwriting existing styles** – Setting the `style` attribute replaces any previous inline styles. If you need to preserve existing rules, read the current `style` value first, append your new rule, then write it back.  
- **File permissions** – Writing back to the same folder may fail on read‑only systems. Choose a writable output path, as we did with `sample_modified.html`.

## 예제 확장

Now that you’ve mastered the basics, consider these next steps:

- **Loop over multiple IDs** – Use a list of IDs and iterate with a `for` loop to batch‑process sections of a page.  
- **Replace text content** – Call `elem.text = "New text"` to alter the visible string.  
- **Add child elements** – Use `

## 다음에 배울 내용은?

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}