---
category: general
date: 2026-08-25
description: 간단한 파이썬 스크립트를 사용하여 HTML 문서를 만들고, 요소의 CSS를 선택하고, HTML 텍스트를 수정하며, HTML
  파일을 저장하는 방법을 배우세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: ko
lastmod: 2026-08-25
og_description: 몇 줄의 파이썬으로 HTML 문서를 생성하고, 요소의 CSS를 선택하며, HTML 텍스트를 수정하고 HTML 파일을 저장합니다.
  이 완전한 튜토리얼을 따라하세요.
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: Python으로 HTML 문서를 만들고 내용 편집하기 – 단계별 가이드
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
title: Python으로 HTML 문서를 만들고 내용 편집하기
url: /ko/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 HTML 문서를 생성하고 내용 편집하기

처음부터 **create html document**를 생성하고 요소를 프로그래밍 방식으로 변경해야 한다면, 이 가이드가 정확히 방법을 보여줍니다. 파일을 생성하고, CSS 선택자를 사용해 단락을 선택하고, 텍스트를 업데이트한 뒤, 결과를 디스크에 다시 쓰는 짧은 실행 가능한 스크립트를 확인할 수 있습니다.

Python에서 HTML을 다루는 것은 보고서, 이메일 템플릿, 정적 사이트 콘텐츠를 생성할 때 일반적입니다. 이 튜토리얼이 끝날 때쯤이면 **select element css**, **modify html text**, **save html file**을 IDE를 떠나지 않고도 수행할 수 있게 됩니다.

## 사전 요구 사항

* Python 3.9 이상 설치되어 있어야 합니다.
* `beautifulsoup4`와 `lxml` 패키지 (`pip install beautifulsoup4 lxml` 명령으로 설치).
* 출력 파일을 저장하려는 디렉터리에 대한 쓰기 권한.

추가 도구는 필요하지 않으며, 표준 라이브러리로 파일 I/O를 처리합니다.

## 단계 1: 필요한 라이브러리 설치

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4`는 HTML을 파싱하고 조작하기 위한 편리한 API를 제공하고, `lxml`은 CSS 선택자를 이해하는 빠른 파서를 제공합니다.

## 단계 2: 초기 HTML 문서 생성

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

`BeautifulSoup` 생성자는 메모리 내에 **create html document** 객체를 구축합니다. `"lxml"` 파서를 사용하면 전체 CSS 선택자 지원이 보장됩니다.

## 단계 3: CSS 선택자를 사용해 단락 요소 선택

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

`select_one` 메서드는 **select element css** 로직을 구현하여 첫 번째 일치하는 태그를 반환합니다. 선택자가 아무것도 일치하지 않으면 `para`는 `None`이 되므로, 실제 코드에서는 방어적 검사가 권장됩니다.

## 단계 4: 단락 텍스트 내용 수정

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

`para.string`에 할당하면 **modify html text** 작업이 수행됩니다. BeautifulSoup는 기본 DOM 트리를 업데이트하므로, 문서를 직렬화할 때 변경 사항이 반영됩니다.

## 단계 5: 업데이트된 HTML을 파일에 저장

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

`open` 호출과 `write`를 함께 사용하면 **save html file** 기능이 구현됩니다. `prettify()`를 사용하면 들여쓰기가 잘 된 출력이 생성되어 디버깅에 유용합니다.

### 빠른 복사를 위한 전체 스크립트

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

`python edit_html.py`를 실행하면 `updated.html`이 생성되고, 내용은 다음과 같습니다:

```html
<p>
 New
</p>
```

## 일반적인 변형 및 엣지 케이스

### 여러 요소 선택

여러 태그와 일치하는 **select element css** 선택자가 필요하다면(예: `"div.note"`), 리스트를 반환하는 `doc.select("div.note")`를 사용하세요. 리스트를 순회하면서 각 요소에 변경을 적용합니다.

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### 기존 속성 보존

텍스트를 교체할 때 BeautifulSoup는 태그의 모든 속성을 유지합니다. 예시:

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### 누락된 요소를 우아하게 처리하기

실제 스크립트에서는 종종 잘못된 HTML을 마주칩니다. Step 4에서 보여준 것처럼 선택을 조건문이나 try‑except 블록으로 감싸서 크래시를 방지하세요.

### 특정 디렉터리에 쓰기

`output_path`를 절대 경로나 상대 경로로 교체하세요:

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

디렉터리가 존재하는지 확인하세요; 그렇지 않으면 Python이 `FileNotFoundError`를 발생시킵니다.

## 전문가 팁

* **Performance** – 대용량 HTML 파일의 경우 `lxml.etree`를 직접 사용하는 것이 좋습니다; BeautifulSoup는 편리하지만 약간 느린 얇은 추상화 레이어를 추가합니다.
* **Encoding** – 비ASCII 문자를 보존하려면 항상 `encoding="utf-8"`으로 파일을 열어야 합니다.
* **Testing** – 수정 후에는 단위 테스트에서 `assert "New" in open(output_path).read()`와 같이 출력이 올바른지 확인할 수 있습니다.

## 결론

이제 **create html document** 방법, **select element css** 쿼리로 노드를 찾는 방법, **modify html text** 방법, 그리고 최종적으로 Python으로 **save html file** 하는 방법을 알게 되었습니다. 이 패턴은 대량 업데이트, 속성 변경, 템플릿 생성 등 더 복잡한 변환에도 확장됩니다.

다음으로 XPath 표현식을 사용한 **how to edit html**, Jinja2로 전체 HTML 페이지 생성, 여러 파일의 배치 처리 자동화와 같은 관련 주제를 탐색해 보세요. 각각은 여기서 보여준 핵심 단계들을 기반으로 하며 프로그래밍 방식 HTML 조작을 위한 도구 모음을 확장합니다.

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 작동 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [Create HTML Document with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}