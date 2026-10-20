---
category: general
date: 2026-08-06
description: Python으로 HTML을 PDF로 변환하기 (전체 예제 포함). HTML에서 PDF를 생성하고, HTML을 PDF로 저장하며,
  일반적인 예외 상황을 처리하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: ko
lastmod: 2026-08-06
og_description: Python에서 HTML을 PDF로 변환하고 문서 생성을 자동화하세요. 이 가이드를 따라 HTML에서 PDF를 생성하고,
  HTML을 PDF로 저장하며, 출력물을 맞춤 설정하세요.
og_image_alt: Example of convert html to pdf script in Python
og_title: Python에서 HTML을 PDF로 변환하기 – 종합 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: Python에서 HTML을 PDF로 변환하기 – 단계별 가이드
url: /ko/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 HTML을 PDF로 변환하기 – 단계별 가이드

빠르게 **HTML을 PDF로 변환**해야 한다면, 이 튜토리얼은 Python에서 완전한 솔루션을 보여줍니다. HTML에서 PDF를 생성하고, HTML을 PDF로 저장하며, 코드를 떠나지 않고 변환 과정을 제어하는 방법을 확인할 수 있습니다.

이 가이드는 신뢰할 수 있는 라이브러리 설치, HTML 문서 로드, 변환 수행, 결과 검증까지 순서대로 안내합니다. 끝까지 따라 하면 정적 페이지든 동적으로 생성된 마크업이든 관계없이 모든 Python 프로젝트에서 HTML 파일을 PDF로 만들 수 있습니다.

## 배울 내용

* HTML‑to‑PDF 변환에 필요한 `pdfkit`와 `wkhtmltopdf` 의존성을 설치합니다.  
* 디스크 또는 문자열에서 HTML 문서를 로드합니다.  
* 페이지 크기, 여백, 인코딩 옵션을 커스터마이징하여 HTML에서 PDF를 생성합니다.  
* 단일 함수 호출로 HTML을 PDF로 저장합니다.  
* 누락된 자산, 유니코드 문자, 대용량 파일 등 일반적인 엣지 케이스를 처리합니다.  

**전제 조건** – Python 3.8+ 및 파일 I/O에 대한 기본 지식. 외부 서비스는 필요하지 않습니다.

## Convert HTML to PDF – overall workflow

변환 프로세스는 세 가지 논리적 단계로 구성됩니다:

1. **Preparation** – 변환기를 설치하고 `wkhtmltopdf` 바이너리가 접근 가능하도록 합니다.  
2. **Input handling** – HTML 파일을 읽거나 프로그램matically 마크업을 생성합니다.  
3. **Output generation** – 변환기를 호출하고 PDF 파일을 작성한 뒤 결과를 확인합니다.

각 단계는 아래 전용 섹션에서 자세히 다룹니다.

## Step 1: Install required libraries

`pdfkit`은 널리 사용되는 `wkhtmltopdf` 엔진을 감싸는 얇은 Python 래퍼를 제공합니다. `pip`으로 두 패키지를 설치하고 바이너리 경로를 확인합니다.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

휴대용 바이너리를 선호한다면, [wkhtmltopdf GitHub page](https://github.com/wkhtmltopdf/wkhtmltopdf/releases)에서 해당 릴리스를 다운로드하여 `PATH`에 포함된 디렉터리에 배치하십시오. 스크립트가 이후에 경로를 자동으로 확인합니다.

## Step 2: Load the HTML document

정적 파일을 읽거나 원격 콘텐츠를 가져오거나 HTML을 즉석에서 구성할 수 있습니다. 아래 예시는 사용자가 정의한 디렉터리에 위치한 `sample.html`이라는 로컬 파일을 로드합니다.

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

파일을 유니코드 문자열로 읽으면 “é”, “ß”와 같은 문자나 아시아 문자들이 변환 중에 보존됩니다. 이 단계는 국제 텍스트가 포함된 **HTML에서 PDF를 생성**할 때 필수적입니다.

## Step 3: Generate PDF from HTML

`pdfkit.from_string`은 HTML 마크업이 포함된 문자열을 PDF 파일로 변환합니다. 페이지 크기, 여백, 헤더/푸터 동작 등을 제어하기 위해 옵션 딕셔너리를 전달할 수 있습니다.

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

위 호출은 `sample.pdf`에 **HTML 파일에서 PDF를 생성**합니다. 소스 HTML이 로컬 CSS나 이미지를 참조한다면 `enable‑local‑file‑access` 플래그가 `wkhtmltopdf`가 해당 리소스를 해결하도록 합니다.

### Why this approach works

* `pdfkit`은 무거운 작업을 `wkhtmltopdf`에 위임하는데, 이는 WebKit 엔진으로 HTML을 렌더링해 원본 레이아웃과 높은 충실도를 보장합니다.  
* 옵션 딕셔너리를 제공하면 HTML 자체를 수정하지 않고도 출력물을 세밀하게 조정할 수 있습니다.  
* `from_string`을 사용하면 워크플로가 메모리 내에서 이루어져, HTML이 즉석에서 생성될 때 유용합니다.

## Step 4: Save HTML as PDF and verify output

변환 후 PDF가 존재하고 읽을 수 있는지 확인하고 싶을 수 있습니다. 아래 스니펫은 파일 크기를 검사하고 기본 시스템 뷰어(플랫폼별)로 PDF를 엽니다.

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

스크립트를 실행하면 성공 메시지가 출력되고 PDF 뷰어가 실행되어 레이아웃이 원본 HTML과 일치하는지 즉시 확인할 수 있습니다. 이 단계가 **HTML을 PDF로 저장** 사이클을 완성합니다.

## Step 5: Advanced options – create PDF from HTML file with custom settings

때때로 디스크에 물리적인 HTML 파일이 존재하고 직접 내용을 로드하는 대신 `pdfkit.from_file`을 선호할 수 있습니다. 이 방법은 HTML에 복잡한 상대 경로가 이미 포함되어 있을 때 유용합니다.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

`options` 딕셔너리를 확장하여 표지 페이지, 목차, JavaScript 실행 플래그 등을 삽입할 수도 있습니다. 예를 들어 표지 페이지를 추가하려면:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

이러한 조정은 보다 정교한 퍼블리싱 파이프라인을 위해 **HTML을 PDF로 변환하는 방법**을 보여줍니다.

## Common pitfalls and how to avoid them

| Issue | Cause | Remedy |
|-------|-------|--------|
| 이미지 또는 CSS가 표시되지 않음 | `wkhtmltopdf`가 기본적으로 로컬 파일 접근을 차단 | 옵션 딕셔너리에 `"enable-local-file-access": None` 추가 |
| 유니코드 문자가 깨짐 | `encoding` 옵션 누락 또는 잘못된 문자셋으로 파일을 읽음 | 항상 `"encoding": "UTF-8"`을 설정하고 HTML 파일을 UTF‑8로 읽기 |
| PDF가 빈 페이지만 표시 | `wkhtmltopdf` 바이너리 경로가 잘못됨 | 경로를 명시적으로 제공: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| 대용량 HTML 파일이 타임아웃 발생 | 기본 타임아웃이 너무 짧음 | `"javascript-delay": "2000"`을 설정하거나 `"timeout": "60"`으로 타임아웃 증가 |

이러한 문제들을 해결하면 다양한 환경에서 **HTML에서 PDF를 생성**하는 프로세스가 안정적으로 동작합니다.

## Full script – end‑to‑end example

다음 코드를 `html_to_pdf.py` 파일로 저장하고 `python html_to_pdf.py` 명령으로 실행하십시오. `YOUR_DIRECTORY`를 프로젝트 폴더 경로로 변경하세요.

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 단계별 설명과 완전한 코드 예제를 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}