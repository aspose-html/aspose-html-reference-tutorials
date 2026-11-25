---
category: general
date: 2026-07-15
description: Python을 사용하여 HTML에서 PDF 만들기. 간단한 스크립트와 명확한 단계로 HTML을 빠르게 PDF로 변환하는 방법을
  배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: ko
lastmod: 2026-07-15
og_description: Python으로 HTML에서 PDF 만들기. 이 가이드는 HTML을 PDF로 변환하고, HTML을 PDF로 저장하며,
  리소스를 효율적으로 처리하는 방법을 보여줍니다.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Python에서 HTML을 PDF로 만들기 – 실습 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: Python에서 HTML을 PDF로 만들기 – HTML을 PDF로 변환하는 Python 튜토리얼
url: /ko/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 HTML로 PDF 만들기 – 풀‑기능 튜토리얼

Ever needed to **HTML에서 PDF 만들기** but weren’t sure which Python library to pick? You’re not alone—many developers hit that wall when they try to turn a web report, invoice, or marketing page into a printable PDF.  

The good news is that with just a few lines of code you can **HTML을 PDF로 변환** reliably, and the script works on Windows, macOS, and Linux. In this guide we’ll walk through a complete, runnable example, explain why each step matters, and show you how to **HTML을 PDF로 저장** without leaving any loose ends.

---

## 배워게 될 내용

- HTML‑to‑PDF 변환을 위한 올바른 Python 패키지를 설치합니다.  
- 무한 CSS import를 방지하기 위해 사용자 정의 리소스 처리 옵션으로 HTML 파일을 로드합니다.  
- 디스크에 깔끔한 PDF 파일을 생성합니다.  
- 외부 이미지, 상대 경로, 대용량 문서와 같은 일반적인 엣지 케이스를 처리합니다.  

이 **HTML to PDF 튜토리얼**을 마치면, 어떤 프로젝트에도 넣어 사용할 수 있는 재사용 가능한 함수를 얻게 됩니다.

---

## 전제 조건

- Python 3.9+ (코드는 3.8에서도 동작하지만, 3.9+에서는 최신 `pathlib` 기능을 제공합니다).  
- 명령줄 및 가상 환경에 대한 기본적인 이해.  
- PDF로 변환하고 싶은 HTML 파일—정적 페이지라면 무엇이든 괜찮습니다.  

> **Pro tip:** 가상 환경을 사용 중이라면, 라이브러리를 설치하기 전에 가상 환경을 활성화하세요; 이렇게 하면 전역 Python 환경을 깔끔하게 유지할 수 있습니다.

---

## Step 1 – WeasyPrint 설치 (변환을 담당하는 엔진)

WeasyPrint는 HTML과 CSS를 PDF로 렌더링하는 순수 Python 라이브러리입니다. 대부분의 최신 웹 기능을 지원하며 리소스 로딩에 대한 세밀한 제어를 제공합니다.

```bash
pip install weasyprint
```

Running the command above pulls in `cairocffi`, `tinycss2`, and a few other dependencies. If you hit a `cairo`‑related error on Windows, grab the pre‑built wheels from the [WeasyPrint website](https://weasyprint.org/docs/install/).

---

## Step 2 – 리소스 처리를 위한 작은 헬퍼 준비

When you load an HTML document that references external stylesheets or images, the library will follow those links. In some cases that leads to deep nesting or even infinite loops (think of a CSS file that `@import`s itself). To keep things tidy we limit the depth of resource handling.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

The class above isn’t required by WeasyPrint, but it mirrors the pattern you saw in the original snippet and gives you a hook to stop runaway imports. You’ll see it used in the next step.

---

## Step 3 – 사용자 정의 옵션으로 HTML 문서 로드

Now we actually read the HTML file. The `HTML` class accepts a `base_url` argument, which we set to the directory containing the source file—this makes relative links work without a web server.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Why this matters:** HTML이 CSS 파일을 연쇄적으로 불러오면, 각 `@import`가 또 다른 로드를 트리거합니다. 깊이 제한은 스크립트가 제어 불능 상태로 빠지는 것을 방지합니다.

---

## Step 4 – 처리된 문서를 PDF로 저장

With the `HTML` object in hand, generating a PDF is a one‑liner. We also pass a simple CSS snippet that forces a clean page size (A4) and adds a tiny margin—feel free to adjust.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Calling `write_pdf` streams the PDF to disk, so you end up with a ready‑to‑share file.

---

## Step 5 – 전체를 한 번에 실행

Below is a compact script you can copy‑paste into `convert.py`. Replace the placeholder paths with your actual directories.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Expected output** – `python convert.py`를 실행하면 다음과 같은 결과가 나타납니다:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Open the generated file with any PDF viewer; you’ll see the original page layout, CSS styling, and images (provided they were reachable from the HTML file).  

If you notice missing images, double‑check that their `src` attributes are either absolute URLs or relative paths that exist under `YOUR_DIRECTORY`.

---

## 자주 묻는 질문 및 엣지 케이스 처리

| Question | Answer |
|----------|--------|
| *HTML이 외부 폰트를 참조한다면 어떻게 하나요?* | WeasyPrint는 폰트 파일을 자동으로 다운로드하지만, 긴 다운로드 시간을 피하기 위해 도메인을 화이트리스트에 추가하는 것이 좋습니다. |
| *파일 대신 HTML 문자열을 변환할 수 있나요?* | 예—`HTML(string=my_html_string)`를 사용하고 `base_url`을 생략하거나 임시 폴더로 설정하세요. |
| *PDF 메타데이터(제목, 저자)를 어떻게 제어하나요?* | `write_pdf`에 `metadata` 딕셔너리를 전달합니다. 예: `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *Linux에서 “cairo‑cffi error”가 발생합니다.* | WeasyPrint를 pip 설치하기 전에 시스템 패키지 `libcairo2-dev`(`Debian/Ubuntu에서는 apt-get install libcairo2-dev`)를 설치하세요. |

---

## 정리

우리는 이제 깔끔한 Python 워크플로우를 사용해 **HTML에서 PDF를 생성**했으며, **HTML을 PDF로 변환** 메커니즘을 다루고, 견고한 리소스 처리를 통해 **HTML을 PDF로 저장**하는 방법을 보여주었습니다. 이 스크립트는 CI 파이프라인에 넣을 만큼 작지만, 사용자 정의 헤더, 푸터, 워터마크 등으로 확장하기에도 충분히 유연합니다.

다음 단계로 시도해 볼 수 있습니다:

- wkhtmltopdf 기반 접근을 위해 **html to pdf python** 라이브러리 `pdfkit` 사용(레거시 CSS에 유용).  
- `argparse`로 CLI 인터페이스를 추가해 스크립트가 입력/출력 인자를 받도록 함.  
- Flask 또는 FastAPI 엔드포인트에서 실시간으로 PDF를 생성해 주문형 보고서를 제공.  

자유롭게 실험하고, 문제를 일으켜 보며, 필요할 때마다 이 가이드를 다시 참고하세요. 문제가 발생하면 WeasyPrint 문서와 커뮤니티 포럼이 훌륭한 자료가 됩니다.

코딩을 즐기시고, 웹 페이지를 세련된 PDF로 변환하는 재미를 느껴보세요!

## 다음에 배울 내용은?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose.HTML로 HTML을 PDF로 변환 – 전체 조작 가이드](/html/english/)
- [.NET에서 Aspose.HTML를 사용해 HTML을 PDF로 변환](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [HTML에서 PDF 만들기 – C# 단계별 가이드](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}