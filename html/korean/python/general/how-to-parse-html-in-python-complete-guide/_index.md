---
category: general
date: 2026-05-28
description: Python에서 HTML을 빠르게 파싱하는 방법—HTML 파일을 로드하고, CSS 선택자를 사용하며, XPath contains
  예제로 href 속성을 추출하기.
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: ko
og_description: 'Python에서 HTML 파싱하기: HTML 파일을 로드하고, CSS 선택자를 사용하며, XPath contains
  예제로 href 속성을 가져오는 방법.'
og_title: Python에서 HTML을 파싱하는 방법 – 단계별
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
title: Python에서 HTML 파싱하는 방법 – 완전 가이드
url: /ko/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 파이썬에서 HTML 파싱하기 – 완전 가이드

파이썬 스크립트에서 무거운 브라우저를 사용하지 않고 **HTML을 파싱하는 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 대부분은 **HTML 파일을 로드**하고, 몇 개의 헤드라인을 스크랩하고, 필요하면 다운로드 링크를 하나 두 개 정도 가져오면 됩니다. 이 튜토리얼에서는 바로 그 방법을 보여드리겠습니다—작은 라이브러리와 CSS 선택자, 그리고 XPath contains 예제를 사용해 **href 속성** 값을 얻는 방법을 다룹니다.

우리는 로컬 HTML 문서를 읽는 것부터 원하는 데이터를 출력하는 전체 과정을 단계별로 안내합니다. 불필요한 내용 없이 실용적이고 바로 실행 가능한 예제를 제공하니 오늘 바로 여러분의 프로젝트에 적용할 수 있습니다.

## 배울 내용

- 경량 파서로 **HTML 파일을 로드**하는 방법.
- 기사 헤드라인과 같은 요소를 가져오기 위해 **CSS 선택자** 구문을 사용하는 방법.
- 링크를 필터링하는 **XPath contains 예제**를 만드는 방법.
- 매치된 노드에서 **href 속성** 값을 안전하게 **얻는** 방법.
- 잘못된 마크업을 처리하고 스크립트를 확장하기 위한 팁.

Python 3.8 이상과 `lxml`, `cssselect` 패키지만 있으면 됩니다—두 패키지는 `pip` 한 줄 명령으로 설치할 수 있습니다.

---

## 단계 1: HTML 파일 로드

무엇보다 먼저, HTML 내용을 메모리로 읽어와야 합니다. `lxml.html` 모듈은 편리한 `fromstring` 헬퍼를 제공하지만, 디스크에 파일이 있을 경우 `parse` 함수가 더 간단합니다.

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **왜 중요한가:** 파일을 한 번만 로드하면 메모리 사용량이 낮아지고 CSS 선택자와 XPath 쿼리를 모두 지원하는 단일 `root` 객체를 얻을 수 있습니다. 파일이 없거나 읽을 수 없을 경우 `html.parse`는 명확한 `OSError`를 발생시키며, 이를 나중에 잡을 수 있습니다.

### 전문가 팁
파일 대신 문자열을 다루는 경우 `html.parse`를 `html.fromstring(your_html_string)`으로 교체하면 됩니다.

---

## 단계 2: CSS 선택자를 사용해 헤드라인 가져오기

CSS 선택자는 간결하고 스타일시트를 작성해 본 사람이라면 익숙합니다. `<article>` 안에 있는 모든 `<h2>` 요소를 가져와 보겠습니다—뉴스 헤드라인에 딱 맞습니다.

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**예상 출력** (샘플 HTML에 두 개의 기사가 있다고 가정하면):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **왜 CSS인가?** 가독성이 좋고 빠르며 `lxml`에서 바로 사용할 수 있습니다. `cssselect` 메서드는 선택자를 내부적으로 XPath 표현식으로 변환해 두 장점 모두를 제공합니다.

---

## 단계 3: XPath Contains 예제 – “download” 링크 찾기

때때로 CSS보다 더 세밀한 제어가 필요합니다. XPath의 `contains()` 함수는 속성 안의 부분 문자열을 매치하고 싶을 때, 예를 들어 다운로드를 가리키는 모든 링크를 찾을 때 유용합니다.

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**샘플 출력**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **왜 XPath contains인가?** 추가적인 파이썬 루프 없이 속성 값에 직접 필터링할 수 있습니다. 이는 튜토리얼에서 자주 보는 고전적인 **xpath contains example**이지만, 여기서는 실제 사용 사례와 결합되었습니다.

---

## 단계 4: 전체를 재사용 가능한 함수로 묶기

경로와 출력문을 하드코딩하는 것은 빠른 테스트에는 괜찮지만, 실제 코드에서는 함수가 필요합니다. 아래는 헤드라인과 다운로드 링크를 모두 반환하는 간결한 헬퍼 함수입니다.

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

이제 함수를 호출하고 결과를 예쁘게 출력할 수 있습니다:

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

스크립트를 실행하면 이전과 동일한 출력이 나오지만, 이제 재사용을 위해 깔끔하게 패키징되었습니다.

---

## 단계 5: 엣지 케이스 및 흔한 함정 처리

1. **`href` 속성 누락** – XPath는 `href`가 없어도 `<a>` 노드를 반환합니다. `None`에 대비하세요:

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **상대 URL vs. 절대 URL** – 링크가 상대 경로라면 기본 URL에 대해 해석해 주는 것이 좋습니다:

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **잘못된 HTML** – `lxml`은 관대하지만, 매우 깨진 마크업은 `html.parse`가 `XMLSyntaxError`를 발생시킬 수 있습니다. 파싱 호출을 `try/except` 블록으로 감싸 로그를 남기고 문제 파일을 건너뛰세요.

4. **대용량 파일 성능** – 수 메가바이트 규모의 페이지는 전체 DOM을 메모리에 로드하는 대신 `iterparse`로 스트리밍하는 것을 고려하세요.

---

## 시각적 개요 (선택 사항)

![HTML 파싱 흐름도: 파일 로드 → CSS 선택자 → XPath contains → href 속성 가져오기](how-to-parse-html-flow.png "HTML 파싱 흐름도")

*Alt 텍스트에는 SEO를 만족시키기 위해 주요 키워드가 포함됩니다.*

---

## 결론

우리는 파이썬에서 **HTML을 파싱하는 방법**을 처음부터 끝까지 다루었습니다: HTML 파일을 로드하고, CSS 선택자를 사용해 기사 헤드라인을 추출하며, 다운로드 링크를 찾기 위해 XPath contains 예제를 만들고, 마지막으로 **href 속성** 값을 안전하게 **얻는** 방법을 살펴보았습니다. 재사용 가능한 `parse_news_html` 함수는 어떤 스크래핑 작업에도 적용할 수 있는 깔끔하고 유지보수하기 쉬운 접근 방식을 보여줍니다.

다음 도전에 준비가 되었나요? 스크립트를 확장해 보세요:

- `//table//tr` XPath 쿼리로 테이블 파싱하기.
- 다른 **xpath contains example**을 사용해 이미지 `src` 속성 추출하기.
- 실시간 웹 페이지를 위해 `aiohttp`로 비동기 가져오기로 전환하기.

즐거운 파싱 되세요. 이 기본을 마스터하면 나머지 HTML 스크래핑은 식은 죽 먹기입니다. 문제가 생기면 아래에 댓글을 남겨 주세요—함께 해결해 봅시다!

## 관련 튜토리얼

- [Aspose.HTML for Java에서 파일로부터 HTML 문서 로드하기](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Aspose.HTML for Java에서 HTML 문서 트리 편집하기](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Aspose.HTML for Java에서 CSS 추가 – HTML 문서에 인라인 CSS 삽입하기](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}