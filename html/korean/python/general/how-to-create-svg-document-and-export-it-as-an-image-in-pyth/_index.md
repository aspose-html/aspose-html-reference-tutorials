---
category: general
date: 2026-10-02
description: Python에서 SVG 문서를 만드는 방법, SVG를 파일에 저장하는 방법, 그리고 짧고 완전한 스크립트로 SVG 이미지를
  내보내는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: ko
lastmod: 2026-10-02
og_description: Python으로 SVG 문서를 만들고 이 실용적인 튜토리얼을 통해 SVG 이미지를 내보내세요. 스크립트를 따라 SVG를
  파일에 저장하고 벡터 그래픽을 즉시 재사용하세요.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Python으로 SVG 문서 만들기 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Python에서 SVG 문서를 만들고 이미지를 내보내는 방법
url: /ko/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 SVG 문서를 생성하고 이미지로 내보내는 방법

프로그램matically **SVG 문서를 생성**해야 할 때, 이 튜토리얼에서는 Python으로 정확히 어떻게 하는지 보여줍니다. 간단한 원을 만들고, SVG를 파일에 저장하며, 어디서든 삽입할 수 있는 내보내기 가능한 SVG 이미지를 만드는 전체 스크립트를 확인해 보세요.

코드로 확장 가능한 벡터 그래픽을 생성하면 GUI 편집기에서 수작업으로 도형을 그리는 노력을 없앨 수 있습니다. 이 가이드를 마치면 데이터 시각화 파이프라인, 자동 보고서 생성기, 혹은 선명하고 해상도에 독립적인 그래픽이 필요한 모든 프로젝트에 SVG 생성을 통합할 수 있습니다.

## 전제 조건

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- Python 3.8 이상이 설치되어 있음
- `svgwrite` 라이브러리 (`pip install svgwrite` 로 설치)
- SVG가 저장될 디렉터리에 대한 쓰기 권한

이 요구 사항은 예제를 가볍게 유지하고 대부분의 환경과 호환되도록 합니다.

## 1단계: SVG 라이브러리 설치 및 임포트

첫 번째 단계는 SVG 생성을 위한 편리한 API를 제공하는 서드파티 라이브러리를 추가하는 것입니다.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite`는 SVG 파일의 XML 구조를 추상화하여, 원시 마크업 대신 기하학에 집중할 수 있게 해줍니다.

## 2단계: SVG 문서 객체 생성

이제 `svgwrite.Drawing`을 인스턴스화하여 **SVG 문서를 생성**할 수 있습니다. 이 객체는 루트 `<svg>` 요소를 나타내며 이후 모든 도형을 보관합니다.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

`size` 인자는 렌더링될 픽셀 크기를 정의하고, `viewBox`는 나중에 정의할 기하학과 일치하는 좌표계를 설정합니다.

## 3단계: 원 요소 추가

원은 중심(`cx`, `cy`)과 반지름(`r`)으로 정의됩니다. `circle` 헬퍼를 사용해 이러한 속성을 지정합니다.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

원은 100 × 100 캔버스의 중앙에 위치하며, 각 측면에 10픽셀 여백을 남깁니다. `fill`과 `stroke`를 조정해 디자인 언어에 맞게 색상을 지정하세요.

## 4단계: SVG를 파일에 저장

그래픽을 조립했으면 `save` 메서드를 사용해 **SVG를 파일에 저장**할 수 있습니다. 이렇게 하면 브라우저와 벡터 편집기가 이해할 수 있는 잘 형성된 XML이 작성됩니다.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

이제 `circle.svg` 파일이 현재 작업 디렉터리에 생성되었습니다. 웹 브라우저, Inkscape, 혹은 SVG 형식을 지원하는 어떤 도구에서도 열어볼 수 있습니다.

## 5단계: 내보낸 SVG 이미지 확인

브라우저에서 저장된 파일을 열어 출력 결과를 확인하세요. 지정한 색상의 중앙 원이 보일 것입니다. 원시 XML은 다음과 같습니다:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

SVG는 벡터 기반이므로 품질 손실 없이 이미지를 확대·축소할 수 있어, 반응형 웹 디자인이나 고해상도 인쇄에 이상적입니다.

## 팁: SVG를 PNG 또는 JPEG로 내보내기

래스터 버전이 필요하다면 **CairoSVG**와 같은 변환 도구와 SVG 파일을 결합하세요:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

이 단계는 **SVG 이미지를** 비트맵 형식으로 **내보내는** 방법을 보여주며, 하위 시스템이 SVG를 직접 렌더링할 수 없을 때 유용합니다.

## 일반적인 변형 및 예외 상황

| 변형 | 처리 방법 |
|-----------|---------------|
| 여러 도형 | 새로운 요소(사각형, 선, 경로)마다 `dwg.add()`를 호출 |
| 동적 차원 | `Drawing`을 만들기 전에 데이터에서 `size`와 `viewBox`를 계산 |
| 텍스트 레이블 | `dwg.text("Label", insert=("10", "20"))`를 사용하고 `font_size`와 `fill`로 스타일 지정 |
| 문서 재사용 | `Drawing` 객체를 메모리에 유지하고 필요할 때마다 `save()` 호출 |
| 대용량 파일 | `dwg.tostring()`으로 출력 스트리밍 후 파일 객체에 직접 기록해 메모리 급증 방지 |

이러한 시나리오를 다루면 **SVG 생성 방법** 스크립트가 간단한 아이콘부터 복잡한 다이어그램까지 확장 가능합니다.

## 전체 스크립트 요약

아래는 모든 단계와 선택적 변환을 포함한 완전하고 실행 가능한 예제입니다:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

이 스크립트를 실행하면 `circle.svg`가 생성되고, `cairosvg`가 설치된 경우 `circle.png`도 생성됩니다. 두 파일 모두 웹 페이지, 보고서, 혹은 추가 처리에 바로 사용할 수 있습니다.

## 결론

이제 Python에서 **SVG 문서를 생성**하고, **SVG를 파일에 저장**하며, **SVG 이미지를 내보내**는 방법을 알게 되었습니다. 예제는 핵심 API 호출을 다루고 각 단계가 왜 중요한지 설명하며, 더 복잡한 그래픽을 위한 확장 방법도 제시합니다.

다음으로는 **SVG Python 튜토리얼**의 추가 주제—경로 그리기, 그라디언트 적용, 요소 애니메이션—을 탐색해 보세요. 이러한 기술을 통합하면 Python 애플리케이션에서 동적이고 데이터 기반의 벡터 그래픽을 직접 생성할 수 있습니다. 즐거운 코딩 되세요!


## 다음에 배울 내용은 무엇인가요?


다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하여 밀접하게 관련된 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공하므로, 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}