---
category: general
date: 2026-11-27
description: Python을 사용하여 SVG 문서를 만들고 SVG 파일을 저장합니다. 벡터를 SVG로 내보내는 방법을 배우고 SVG 이미지를
  빠르게 생성합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: ko
lastmod: 2026-11-27
og_description: Python으로 SVG 문서를 만들고 SVG 파일을 저장하세요. 이 가이드는 벡터를 SVG로 내보내고 몇 분 안에 SVG
  이미지를 만드는 방법을 보여줍니다.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Python을 사용해 SVG 문서를 만들고 SVG 파일 저장
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Python을 사용하여 SVG 문서를 만들고 SVG 파일을 저장하기
url: /ko/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python으로 SVG 문서 만들기 및 SVG 파일 저장하기

If you need to **create SVG document** from scratch, this guide walks you through the entire process. You’ll see how to **save SVG file** on disk, export the vector as SVG, and end up with a ready‑to‑use SVG image in just a few lines of code.

처음부터 **create SVG document**가 필요하다면, 이 가이드는 전체 과정을 단계별로 안내합니다. 디스크에 **save SVG file**하는 방법, 벡터를 SVG로 내보내는 방법을 확인하고, 몇 줄의 코드만으로 바로 사용할 수 있는 SVG 이미지를 얻을 수 있습니다.

Generating scalable graphics programmatically is useful for reports, UI icons, or any situation where you want resolution‑independent images. By the end of this tutorial you’ll be able to answer “**how to create SVG**?” for simple shapes and extend the pattern to complex vector artwork.

프로그램matically scalable graphics를 생성하는 것은 보고서, UI 아이콘, 혹은 해상도에 독립적인 이미지를 원하는 모든 상황에 유용합니다. 이 튜토리얼을 마치면 간단한 도형에 대해 “**how to create SVG**?”라는 질문에 답할 수 있게 되고, 이 패턴을 복잡한 벡터 아트워크로 확장할 수 있습니다.

## 필요한 사항

- Python 3.8 이상  
- `svgwrite` 패키지 (`pip`으로 설치 가능)  
- 출력 파일을 저장할 수 있는 쓰기 가능한 디렉터리  

No external graphics editors are required; everything runs from the command line.

외부 그래픽 편집기가 필요하지 않으며, 모든 작업은 명령줄에서 실행됩니다.

## 단계 1: `svgwrite` 라이브러리 설치

`svgwrite`는 SVG 마크업을 만들기 위한 깔끔하고 Pythonic한 API를 제공합니다. 한 번만 다음과 같이 설치합니다:

```bash
pip install svgwrite
```

> **Pro tip:** 가상 환경(`python -m venv .venv`)을 사용하여 의존성을 격리하세요.

## 단계 2: SVG 문서 만들기

Now we actually **create SVG document** objects. The `Drawing` class represents the root `<svg>` element and handles namespaces automatically.

이제 실제로 **create SVG document** 객체를 만듭니다. `Drawing` 클래스는 루트 `<svg>` 요소를 나타내며 네임스페이스를 자동으로 처리합니다.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

The `Drawing` instance is the entry point for all subsequent SVG operations. By specifying `size` we set the canvas dimensions, which influences how browsers render the image.

`Drawing` 인스턴스는 이후 모든 SVG 작업의 진입점입니다. `size`를 지정함으로써 캔버스 크기를 설정하고, 이는 브라우저가 이미지를 렌더링하는 방식에 영향을 줍니다.

## 단계 3: 빨간 원 요소 추가

Adding shapes is straightforward. The `circle` method creates a `<circle>` element; we then attach it to the root.

도형을 추가하는 것은 간단합니다. `circle` 메서드는 `<circle>` 요소를 생성하고, 이를 루트에 연결합니다.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Why we choose a circle: circles are vector primitives that demonstrate scalability without any loss of quality, making the output ideal for testing **export vector as SVG** workflows.

우리가 원을 선택한 이유: 원은 품질 손실 없이 확장성을 보여주는 벡터 기본 도형이며, **export vector as SVG** 워크플로를 테스트하기에 이상적인 출력물입니다.

## 단계 4: SVG 파일 저장

Finally, write the markup to disk. This step fulfills the **save SVG file** requirement and produces a file you can open in any browser or vector editor.

마지막으로 마크업을 디스크에 기록합니다. 이 단계는 **save SVG file** 요구사항을 충족시키며, 브라우저나 벡터 편집기에서 열 수 있는 파일을 생성합니다.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

When you run the script, you’ll see a console message confirming the location of the generated file.

스크립트를 실행하면 생성된 파일 위치를 확인하는 콘솔 메시지가 표시됩니다.

### 예상 출력

The resulting `circle.svg` contains:

결과물인 `circle.svg`는 다음과 같습니다:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Opening the file in a browser displays a crisp red circle, and because it’s vector‑based you can zoom indefinitely without pixelation.

브라우저에서 파일을 열면 선명한 빨간 원이 표시되며, 벡터 기반이기 때문에 픽셀화 없이 무한히 확대할 수 있습니다.

## 단계 5: 일반적인 변형 및 엣지 케이스

### 더 복잡한 벡터 내보내기

If you need to **export vector as SVG** for multi‑shape illustrations, simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`, `path`, etc.). For example:

멀티 도형 일러스트레이션을 위해 **export vector as SVG**가 필요하다면, 다른 기본 도형(`rect`, `line`, `path` 등)과 함께 `dwg.add()` 패턴을 반복하면 됩니다. 예시:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### 유니코드 및 텍스트 처리

SVG supports text elements with full Unicode support. Use `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` to embed multilingual labels.

SVG는 전체 유니코드 지원 텍스트 요소를 지원합니다. `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")`를 사용하여 다국어 라벨을 삽입하세요.

### 다른 위치에 저장

When **save SVG image** to a user‑specified folder, validate the path to avoid permission errors:

사용자가 지정한 폴더에 **save SVG image**할 때는 권한 오류를 방지하기 위해 경로를 검증하세요:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### 출력 최소화

For production pipelines, you might want a smaller file size. Pass `pretty=False` to `dwg.tostring()` and write the result manually:

프로덕션 파이프라인에서는 파일 크기를 줄이고 싶을 수 있습니다. `dwg.tostring()`에 `pretty=False`를 전달하고 결과를 직접 기록하세요:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## 대체 라이브러리로 SVG 만들기 (선택 사항)

While `svgwrite` is lightweight and pure‑Python, other ecosystems exist:

`svgwrite`는 가볍고 순수 Python이지만, 다른 생태계도 존재합니다:

- **cairosvg** – PNG, PDF, HTML을 SVG로 변환합니다.  
- **lxml** – XML API를 사용해 SVG 마크업을 수동으로 구축할 수 있습니다.  

Choosing a library depends on your project’s complexity and existing dependencies.

라이브러리 선택은 프로젝트의 복잡도와 기존 의존성에 따라 달라집니다.

## 결론

You now know how to **create SVG document**, add vector shapes, and **save SVG file** using Python. The complete solution demonstrates the steps to **export vector as SVG**, generate a **SVG image**, and answer the common query **how to create SVG** programmatically.

이제 Python을 사용해 **create SVG document**하고, 벡터 도형을 추가하며, **save SVG file**하는 방법을 알게 되었습니다. 전체 솔루션은 **export vector as SVG** 단계, **SVG image** 생성, 그리고 일반적인 질문인 **how to create SVG**에 대한 프로그래밍 방식 답변을 보여줍니다.

From here you can:

- 루프를 사용해 스크립트를 확장하여 차트나 아이콘을 자동으로 생성합니다.  
- SVG 출력을 웹 애플리케이션이나 이메일 템플릿에 통합합니다.  
- `svgwrite`로 `<animate>` 요소를 추가하여 애니메이션을 탐색합니다.

Experiment with different shapes, colors, and gradients to fully harness the power of scalable vector graphics in your Python projects. Happy coding!

다양한 도형, 색상, 그라디언트를 실험하여 Python 프로젝트에서 확장 가능한 벡터 그래픽의 힘을 완전히 활용해 보세요. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 완전한 코드 예제와 단계별 설명을 포함하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [SVG 문서 만들기 – 원 추가 및 SVG로 저장](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Python에서 SVG 문서 만들기 – SVG를 PNG로 변환 가이드](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Python에서 SVG 파일 로드 – 내보내기, 삽입 및 변환 완전 가이드](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}