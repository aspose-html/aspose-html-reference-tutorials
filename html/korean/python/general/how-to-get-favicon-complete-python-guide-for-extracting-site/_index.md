---
category: general
date: 2026-06-26
description: URL에서 HTML을 로드하고 link 태그의 href를 추출하여 파비콘을 가져오는 방법을 배웁니다. 웹사이트 아이콘을 빠르게
  얻기 위한 단계별 Python 코드.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: ko
og_description: '파비콘을 빠르게 가져오는 방법: URL에서 HTML을 로드하고, link rel=''icon''을 찾아서, Python을
  사용해 link 태그에서 href를 추출합니다.'
og_title: 파비콘 가져오는 방법 – 파이썬 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: 파비콘 가져오기 방법 – 사이트 아이콘 추출을 위한 완전한 파이썬 가이드
url: /ko/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 파비콘 가져오기 – 사이트 아이콘 추출을 위한 완전한 파이썬 가이드

수동으로 페이지 소스를 살펴보지 않고도 모든 웹사이트에서 **파비콘을 얻는 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다—개발자, SEO 전문가, 그리고 디자이너까지도 종종 사이트를 대표하는 작은 아이콘이 필요합니다. 이 튜토리얼에서는 URL에서 HTML을 로드하고, `<link rel="icon">` 태그를 찾아 아이콘 URL을 추출하는 깔끔한 파이썬 중심 방법을 보여드립니다. 끝까지 보면 어떤 도메인에서도 정확히 **파비콘을 얻는 방법**을 알게 되고, 프로젝트에 바로 사용할 수 있는 재사용 가능한 스크립트를 갖게 됩니다.

우리는 HTML을 가져오는 것부터 상대 URL 및 다양한 아이콘 형식과 같은 엣지 케이스를 처리하는 것까지 모두 다룰 것입니다. 외부 서비스는 필요 없으며—표준 `requests` 라이브러리와 가벼운 HTML 파서만 있으면 됩니다. 시작할 준비가 되셨나요? 바로 들어가 보겠습니다.

## 사전 요구 사항

- Python 3.8+ 설치 (코드는 3.10에서도 작동합니다)  
- `requests`와 리스트 컴프리헨션에 대한 기본적인 이해  
- 대상 웹사이트에 대한 인터넷 접속  

이미 갖추고 있다면, 좋습니다—첫 번째 단계로 바로 넘어가세요. 그렇지 않다면, 필요한 유일한 의존성을 설치하세요:

```bash
pip install requests beautifulsoup4
```

> **Pro tip:** `beautifulsoup4`는 “load html from url”을 손쉽게 해주는 검증된 파서입니다.

## 1단계: 파이썬으로 URL에서 HTML 로드하기  

파비콘을 얻는 방법을 배우기 위해 가장 먼저 해야 할 일은 페이지 소스를 가져오는 것입니다. 이것이 “load html from url” 과정의 일부입니다.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

`requests`를 사용하는 이유는 무엇일까요? 이 라이브러리는 리다이렉트, HTTPS 검증, 타임아웃을 자동으로 처리해 주므로 나중에 **웹사이트 아이콘을 가져올 때** 예상치 못한 문제가 적어집니다.

## 2단계: 문서를 파싱하고 아이콘 링크 찾기  

이제 HTML을 확보했으니, `rel` 속성이 아이콘을 나타내는 모든 `<link>` 요소를 찾아야 합니다. 이것이 **파비콘을 얻는 방법**의 핵심입니다.

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

`icon`과 `shortcut icon` 모두를 확인하는데, 오래된 사이트는 여전히 후자를 사용하기 때문입니다. 이 작은 차이가 “how to extract favicons”를 검색할 때 사람들을 흔히 혼란스럽게 합니다.

## 3단계: 링크 요소에서 href 추출하기  

관련 태그를 손에 넣었으니, 다음 논리적 단계인 **링크에서 href 추출**은 간단합니다.

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

`urljoin`을 사용하면 사이트가 `/favicon.ico`와 같은 상대 경로를 제공하더라도 올바른 절대 URL을 얻을 수 있어, 신뢰할 수 있는 **파비콘을 얻는 방법** 스크립트에 필수적입니다.

## 4단계 (선택): 아이콘 URL 검증 및 필터링  

때때로 페이지에 많은 아이콘(Apple 터치 아이콘, 다양한 크기의 PNG 등)이 나열됩니다. 클래식 `.ico` 파일만 필요하다면 그에 맞게 필터링하면 됩니다. 이 단계는 특정 유형의 **파비콘을 추출하는 방법**을 보여줍니다.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

필터를 자유롭게 조정하세요: `".ico"`를 `".png"`로 바꾸거나 고해상도 아이콘이 필요하면 `rel="apple-touch-icon"`을 확인하면 됩니다.

## 5단계: 아이콘 파일 다운로드 (실제 이미지를 원한다면)

URL을 추출하는 것만으로도 절반은 성공한 셈입니다; 다운로드하면 표시하거나 저장할 수 있는 파일을 얻을 수 있습니다. 간단한 헬퍼를 소개합니다:

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

이 코드를 앞 단계들 뒤에 실행하면 발견된 모든 파비콘의 로컬 복사본을 얻을 수 있어 캐시나 오프라인 분석에 최적입니다.

## 6단계: 전체 예제 – 완전한 작동 예시

아래는 어떤 사이트에서든 **파비콘을 얻는 방법**을 보여주는 완전하고 바로 실행 가능한 스크립트입니다. 복사‑붙여넣기하고 `target_url`을 바꾼 뒤 출력을 확인하세요.

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**예상 출력 (간략히 표시):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

사이트가 PNG나 Apple 터치 아이콘만 제공하는 경우, 스크립트는 대신 해당 URL들을 나열하여 모든 상황에서 정확히 **파비콘을 얻는 방법**을 보여줍니다.

## 일반적인 질문 및 엣지 케이스

### 사이트가 `<link>` 대신 `<meta>` 태그를 사용하는 경우는?

일부 오래된 페이지는 `<meta name="msapplication‑TileImage">`에 아이콘 URL을 삽입합니다. `find_icon_links`를 확장하여 이러한 메타 태그도 검색하고 동일하게 처리하도록 할 수 있습니다.

### `//` 로 시작하는 상대 URL을 어떻게 처리하나요?

`urljoin`은 기본 URL의 스킴을 기준으로 프로토콜‑상대 URL(`//example.com/favicon.ico`)을 자동으로 해결하므로 별도의 로직이 필요 없습니다.

### 여러 크기(예: 32×32, 180×180)를 자동으로 가져올 수 있나요?

네—`filter_ico_urls` 단계를 생략하면 됩니다. 스크립트는 발견한 모든 아이콘 URL을 반환하며, PNG 등 다양한 해상도의 파일도 포함됩니다. 이후 파일명 패턴을 기준으로 정렬하거나 선택할 수 있습니다.

### 봇을 차단하는 사이트에서도 작동하나요?

사이트가 403을 반환하거나 커스텀 User‑Agent가 필요하면 `requests.get` 호출을 다음과 같이 조정하세요:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

이 작은 변경만으로도 엄격한 도메인에서 **파비콘을 얻는 방법** 문제를 해결할 수 있습니다.

## 시각적 개요

![웹사이트에서 파비콘을 가져오는 흐름을 보여주는 다이어그램 – HTML 로드, 링크 태그 파싱, href 추출, 선택적 다운로드](how-to-get-favicon-diagram.png "파비콘 가져오기 흐름 다이어그램")

*이미지의 alt 텍스트에 주요 키워드가 포함되어 있어 이미지 SEO에 도움이 됩니다.*

## 결론

우리는 **파비콘을 얻는 방법**을 단계별로 살펴보았습니다: URL에서 HTML을 로드하고,

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하여 밀접하게 연관된 주제를 다룹니다. 각 리소스는 완전한 작동 코드 예제와 단계별 설명을 포함하고 있어 추가 API 기능을 마스터하고 자체 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [C#에서 HTML 저장 방법 – 커스텀 리소스 핸들러를 이용한 완전 가이드](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Aspose.HTML for Java를 사용한 HTML 편집 방법](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Java에서 HTML을 PDF로 변환 – Aspose.HTML for Java 사용](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}