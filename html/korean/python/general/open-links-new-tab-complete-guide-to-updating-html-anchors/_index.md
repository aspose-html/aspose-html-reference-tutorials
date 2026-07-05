---
category: general
date: 2026-07-05
description: Python을 사용해 링크를 새 탭에서 열기 – target="_blank" 추가 방법, 링크 타깃 변경, 속성 포함 선택자
  사용, 그리고 수정된 HTML을 손쉽게 저장하는 방법을 배워보세요.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: ko
og_description: 링크를 새 탭에서 빠르게 열기. 이 튜토리얼에서는 target='_blank'을 추가하고, 링크 타깃을 변경하며, 수정된
  HTML을 Python으로 저장하는 방법을 보여줍니다.
og_title: 링크를 새 탭에서 열기 – 단계별 HTML 업데이트 가이드
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
title: 링크를 새 탭에서 열기 – HTML 앵커 업데이트 완전 가이드
url: /ko/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 링크를 새 탭에서 열기 – HTML 앵커 업데이트 완전 가이드

정적 HTML 페이지에서 **open links new tab**이 필요했지만 어디서 시작해야 할지 몰랐던 적이 있나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 레거시 사이트를 정리하거나 접근성 개선을 할 때 이 문제에 부딪힙니다. 이 튜토리얼에서는 몇 줄의 Python으로 **adds target blank**, **changes link target**, 그리고 안전하게 **saves modified html**을 수행하는 실용적인 솔루션을 단계별로 안내합니다.

또한 **attribute contains selector**를 사용하는 방법을 다루어, 실제로 필요한 앵커(예: *example.com*을 가리키는 모든 링크)만을 수정하도록 할 수 있습니다. 끝까지 읽으면 크기와 관계없이 어떤 프로젝트에도 바로 넣어 사용할 수 있는 재사용 가능한 스크립트를 얻게 됩니다.

## 배울 내용

- 조작 가능한 문서 객체로 HTML 파일을 로드합니다.  
- `href` 속성에 특정 문자열이 포함된 `<a>` 요소를 선택합니다.  
- **Add target blank**하고 `rel="noopener"` 속성을 설정하여 보안을 강화합니다.  
- **Save modified html**을 디스크에 저장하면서 포맷을 유지합니다.  

표준 라이브러리와 **beautifulsoup4**(작은 설치) 외에 외부 의존성이 없습니다. 다른 파서를 이미 사용 중이라면 개념은 그대로 적용됩니다.

---

## 전제 조건

- Python 3.8+이 설치되어 있어야 합니다.  
- HTML 및 Python에 대한 기본적인 이해가 필요합니다.  
- `beautifulsoup4` 패키지(`pip install beautifulsoup4`).  

그것뿐—무거운 프레임워크는 필요하지 않습니다.

---

## Step 1: Load the HTML Document

먼저 해야 할 일은 소스 파일을 읽어 BeautifulSoup에 전달하는 것입니다. 이는 새로운 속성을 추가할 수 있는 빈 캔버스를 여는 것과 같습니다.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Why this matters:** `Path`를 사용하면 코드가 OS‑agnostic가 되고, `html.parser`는 내장 파서이므로 간단한 작업에 추가 파서가 필요하지 않습니다.

---

## Step 2: Use an Attribute Contains Selector to Find the Right Links

우리는 *example.com*을 가리키는 앵커만 수정하고 싶습니다. CSS 선택자 `a[href*='example.com']`가 바로 그 역할을 합니다—`*=`는 “포함”을 의미합니다. BeautifulSoup의 `select` 메서드는 이 구문을 이해합니다.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Pro tip:** 대소문자를 구분하지 않는 매치를 원한다면 `if 'example.com' in a.get('href', '').lower()`와 같은 작은 루프로 전환하세요.

이제 `anchor_elements`에 우리가 관심 있는 모든 링크가 들어 있어 다음 변환을 수행할 준비가 되었습니다.

---

## Step 3: Change Link Target – Add Target Blank and Secure the Link

새 탭에서 링크를 여는 것은 `target="_blank"`을 설정하는 것만큼 간단합니다. 하지만 최신 브라우저는 `rel="noopener"`(또는 `noreferrer`)를 추가하도록 권장합니다. 이는 새로 열린 페이지가 `window.opener`를 통해 원래 창에 접근하는 것을 방지하여 피싱 공격을 차단하는 작은 보안 트윅입니다.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Why we use direct dictionary assignment:** 속성이 없으면 자동으로 생성하고, 이미 존재하면 덮어쓰기 때문에 **change link target** 작업에 최적입니다.

---

## Step 4: Save Modified HTML Back to Disk

마지막 단계는 업데이트된 마크업을 새 파일에 쓰는 것입니다. 원본을 그대로 두면 문제가 생겼을 때 쉽게 되돌릴 수 있습니다.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **What `prettify()` does:** HTML을 깔끔한 들여쓰기로 포맷팅해 저장된 파일을 읽기 쉽고 차이점을 비교하기 편하게 만듭니다. 원본 공백을 유지하고 싶다면 `prettify()`를 `str(soup)`로 교체하면 됩니다.

---

## Full Script – One‑Click Solution

아래는 완전하고 바로 실행 가능한 스크립트입니다. `update_links.py`라는 이름으로 저장하고 터미널에서 `python update_links.py`를 실행하세요.

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

### Expected Result

예를 들어 `links.html`에 다음과 같은 내용이 있었다고 가정해 봅시다:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

스크립트를 실행한 후 `links-updated.html`은 다음과 같이 표시됩니다:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

*example.com*에 대한 링크에만 **add target blank** 속성이 추가되어, 우리의 **attribute contains selector**가 정확히 의도대로 작동했음을 보여줍니다.

---

## Common Questions & Edge Cases

### What if a link already has a `rel` attribute?

우리 루프는 기존 값을 `"noopener"`로 덮어씁니다. 기존 값(예: `"nofollow"`)을 보존해야 한다면 다음과 같이 연결하면 됩니다:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### How to handle multiple domains?

선택자 목록을 확장하기만 하면 됩니다:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### Does `prettify()` change the original HTML structure?

`prettify()`는 들여쓰기만 재조정하고 태그 순서나 속성 값은 변경하지 않습니다. 정확한 원본 공백을 유지해야 한다면 앞서 언급한 대로 `prettify()`를 `str(soup)`로 교체하면 됩니다.

---

## Pro Tips for Production‑Ready Scripts

- **Backup before overwriting:** 원본 파일을 안전하게 보관하려면 복사 단계(`shutil.copy`)를 추가하세요.  
- **Logging instead of print:** 규모가 커지는 프로젝트에서는 `logging` 모듈을 사용하세요.  
- **Batch processing:** `Path.rglob("*.html")`로 디렉터리를 순회하면 한 번에 여러 파일을 업데이트할 수 있습니다.  

이러한 개선점은 간단한 **open links new tab** 스크립트를 모든 웹 유지보수 워크플로우에 사용할 수 있는 견고한 유틸리티로 바꿔 줍니다.

---

## Conclusion

이제 정적 HTML 컬렉션 전반에 걸쳐 **open links new tab**을 적용할 수 있는 견고하고 재사용 가능한 방법을 갖추었습니다. **attribute contains selector**를 활용하면 **change link target**을 정확히 원하는 위치에만 적용하고, **add target blank**와 **save modified html**을 포맷 손실 없이 수행할 수 있습니다.

테스트 페이지에서 한 번 실행해 본 뒤 전체 사이트에 적용해 보세요. PDF나 다른 도메인에 대한 선택자를 조정해야 할 경우 CSS 문자열만 바꾸면 나머지는 그대로 유지됩니다.

스크립트를 사용하면서 궁금한 점이 있거나 확장한 사례가 있다면 댓글로 알려 주세요. 즐거운 코딩 되시고, 모든 앵커가 원하는 대로 정확히 열리길 바랍니다!

## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 보여준 기술을 기반으로 하여 밀접하게 연관된 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.HTML for Java를 사용하여 HTML 편집하기](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Aspose.HTML for Java에서 HTML 문서에 CSS 추가하기 – 인라인 CSS](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}