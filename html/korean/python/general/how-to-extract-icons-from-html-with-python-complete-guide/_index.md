---
category: general
date: 2026-07-02
description: Python을 사용하여 HTML 파일에서 아이콘을 추출하는 방법. Python으로 HTML 파일을 읽고, HTML 문서를 파싱하며,
  href 속성을 추출해 파비콘 URL을 얻는 방법을 배웁니다.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: ko
og_description: Python을 사용하여 HTML 페이지에서 아이콘을 추출하는 방법. 이 튜토리얼에서는 Python으로 HTML 파일을
  읽고, 문서를 파싱하며, 파비콘 URL을 추출하는 방법을 보여줍니다.
og_title: HTML에서 아이콘 추출하기 – 파이썬 가이드
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
title: Python으로 HTML에서 아이콘 추출하는 방법 – 완전 가이드
url: /ko/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python으로 HTML에서 아이콘 추출하기 – 완전 가이드

브라우저를 열지 않고 웹 페이지에서 **아이콘을 추출하는 방법**을 궁금해 본 적 있나요? 사이트 카탈로그를 만들거나, SEO 감사 도구를 개발하거나, 탭에 표시되는 작은 파비콘이 궁금할 수도 있겠죠. 좋은 소식은 Python 몇 줄만으로도 가능합니다—Selenium도, 헤드리스 Chrome도 필요 없고, 순수 텍스트 HTML 파일만 있으면 됩니다.

이 튜토리얼에서는 HTML 파일을 Python으로 읽고, HTML 문서를 파싱한 뒤, `<link rel="icon">` 태그에서 **href 속성을 추출**하여 파비콘 URL을 얻는 과정을 단계별로 살펴봅니다. 최종적으로 어떤 정적 HTML에도 사용할 수 있는 재사용 가능한 스니펫을 만들 수 있으며, 상대 경로나 여러 아이콘 선언과 같은 예외 상황도 처리하는 방법을 확인하게 됩니다.

## 배울 내용

- Python으로 로컬 HTML 파일 로드하기 (read html file python)  
- 가벼운 파서를 사용해 **HTML 문서 파싱** 안전하게 수행하기  
- 아이콘을 선언하는 `<link>` 요소 찾기  
- **href 속성** 값을 추출하고 절대 URL로 변환하기  
- 발견한 모든 **파비콘 URL** 수집 및 출력하기  

외부 서비스 없이—표준 라이브러리와 인기 있는 **BeautifulSoup** 패키지만으로 가능합니다.

---

![Screenshot showing Python script extracting icons – how to extract icons](https://example.com/images/extract-icons-python.png "how to extract icons")

*Image alt text: "how to extract icons using a Python script"*

## 사전 요구 사항

- Python 3.8+ 설치  
- `beautifulsoup4` 라이브러리 (`pip install beautifulsoup4`)  
- 스캔하려는 로컬 HTML 파일 (예: `sample.html`)  

위 항목이 모두 준비되었다면 바로 시작해봅시다.

## 1단계: HTML 파일 읽기 – 문서 로드

우선 파일을 열어 내용을 파서에 전달해야 합니다. `with open(..., "r", encoding="utf‑8")`를 사용하면 파일이 자동으로 닫히고, UTF‑8 인코딩은 대부분의 최신 페이지를 올바르게 처리합니다.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**왜 중요한가:** 올바른 인코딩으로 파일을 열지 않으면 파서를 방해할 수 있는 `�` 문자들이 나타날 수 있습니다. 표준 라이브러리의 `Path`를 사용하면 코드가 플랫폼에 구애받지 않게 됩니다.

## 2단계: HTML 문서 파싱 – 모든 아이콘 링크 찾기

이제 원시 HTML을 **BeautifulSoup**에 전달하면 탐색 가능한 트리가 만들어집니다. `rel` 속성에 `icon`이라는 단어가 포함된 모든 `<link>` 태그를 찾아야 합니다. `rel`은 공백으로 구분된 리스트(`rel="shortcut icon"`)일 수 있으므로 유연한 검사가 필요합니다.

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

**왜 이 단계가 핵심인가:** `soup.find_all("link", rel="icon")`만 사용하면 `rel="shortcut icon"`이나 `rel="apple-touch-icon"`과 같은 변형을 놓치게 됩니다. 우리의 헬퍼 함수 `is_icon_link`가 이러한 경우를 모두 포괄해 추출을 견고하게 만듭니다.

## 3단계: href 속성 추출 – URL 가져오기

관련 태그를 모았다면 이제 각 태그에서 `href` 속성을 추출합니다. 일부 페이지는 `href`를 생략하기도 하므로(`None` 가능) 이를 방어적으로 처리합니다. 또한 파비콘은 상대 URL로 지정되는 경우가 많아, 페이지의 기본 URL을 알고 있다면 이를 기준으로 절대 경로로 변환합니다. 로컬 파일인 경우 경로를 그대로 유지합니다.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**공백을 제거하는 이유:** HTML 작성자가 실수로 URL 앞뒤에 공백을 넣는 경우가 있는데, 이는 이후 요청을 깨뜨릴 수 있습니다. 트리밍을 통해 깨끗한 문자열을 확보합니다.

## 4단계: 파비콘 URL 추출 – 결과 출력

마지막으로 발견된 URL 목록을 출력(또는 반환)합니다. 실제 스크립트에서는 CSV 파일에 기록하거나 아이콘을 다운로드하거나 다른 서비스에 전달할 수 있습니다. 아래는 콘솔에 결과를 보여주는 간단한 루프 예시입니다.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### 예외 상황 처리

- **다중 rel 값:** `is_icon_link` 검사는 이미 `rel="shortcut icon"` 및 `rel="apple-touch-icon"`을 포착합니다.  
- **상대 경로:** 나중에 절대 URL이 필요하면 `urllib.parse.urljoin(base_url, href)`를 사용하세요.  
- **href 누락:** `if href:` 조건문으로 잘못된 태그를 건너뛰어 `NoneType` 오류를 방지합니다.  
- **중복 항목:** `icon_urls = list(dict.fromkeys(icon_urls))`와 같이 중복을 제거할 수 있습니다.

---

## 전체 스크립트 – 원스톱 솔루션

이제 모든 코드를 하나로 모아 완전 실행 가능한 프로그램을 보여드립니다. 파일명을 `extract_icons.py`로 저장하고 `html_path`를 원하는 파일 경로로 지정하면 됩니다.

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

**예상 출력** (예: `sample.html`에 아이콘 두 개가 포함된 경우):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

`python extract_icons.py` 명령으로 실행하면 콘솔에 URL이 출력됩니다.

---

## 자주 묻는 질문

**Q: HTML에 `<meta>` 태그로 아이콘이 정의돼 있으면 어떻게 하나요?**  
A: 일부 사이트는 `<meta itemprop="image">`를 사용해 아이콘을 삽입합니다. `is_icon_link`에 `meta`와 `itemprop="image"`를 검사하도록 확장하고 `content` 속성을 추출하면 됩니다.

**Q: 아이콘을 자동으로 다운로드할 수 있나요?**  
A: 가능합니다—각 URL을 `requests.get(url, stream=True)`에 전달하고 파일로 저장하면 됩니다. 상대 URL는 `urljoin`으로 처리하는 것을 잊지 마세요.

**Q: 원격 페이지에서도 동작하나요?**  
A: 물론입니다. 파일 읽기 단계 대신 `requests.get(page_url).text`로 HTML 문자열을 받아 BeautifulSoup에 전달하면 됩니다. 다만 robots.txt와 요청 속도 제한을 준수하세요.

---

## 마무리

Python을 사용해 정적 HTML 어디에서든 **아이콘을 추출하는 방법**을 살펴보았습니다. 파일 읽기, 문서 파싱, 올바른 태그 찾기, `href` 속성 추출이라는 핵심 흐름은 다양한 웹 스크래핑 작업에서도 재사용 가능한 패턴입니다.

다음 단계로는:

- 상대 URL을 페이지의 기본 URL에 맞게 해석하기  
- 각 아이콘을 다운로드해 로컬에 저장하기  
- 추가 아이콘 형식 지원 (`rel="mask-icon"` for Safari)  

실험해 보시고, 궁금한 점이 있으면 아래 댓글에 남겨 주세요. 즐거운 파싱 되세요!

## 다음에 배울 내용

다음 튜토리얼들은 이번 가이드에서 다룬 기술을 확장하고, 추가 API 기능을 마스터하며, 다양한 구현 방법을 탐구할 수 있도록 도와줍니다.

- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}