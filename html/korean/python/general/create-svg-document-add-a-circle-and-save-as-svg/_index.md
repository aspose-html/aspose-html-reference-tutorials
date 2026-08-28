---
category: general
date: 2026-07-31
description: SVG 문서를 만드는 방법, 원을 추가하는 방법, 그리고 SVG 파일을 빠르게 저장하는 방법을 배워보세요. 몇 줄의 파이썬
  코드로 그래픽을 SVG로 내보낼 수 있습니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: ko
lastmod: 2026-07-31
og_description: SVG 문서를 만들고 원을 추가한 뒤, 몇 초 만에 SVG 파일을 저장하세요. 이 가이드는 명확하고 실행 가능한 코드를
  사용해 그래픽을 SVG로 내보내는 방법을 보여줍니다.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: SVG 문서 만들기 – 원을 추가하고 SVG로 저장
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: SVG 문서 만들기 – 원 추가하고 SVG로 저장
url: /ko/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG 문서 만들기 – 원 추가 및 SVG로 저장

코드에서 **create SVG document** 를 만들어야 하는데 어디서 시작해야 할지 몰라 고민한 적 있나요? 혼자가 아닙니다. 많은 개발자들이 벡터 그래픽을 처음 다룰 때 이 장벽에 부딪히곤 합니다. 이 튜토리얼에서는 **add circle to SVG** 를 수행하고 **save SVG file** 하여 **export graphic as SVG** 를 웹이나 디자인 툴에서 사용할 수 있도록 하는 작고 독립적인 예제를 단계별로 살펴보겠습니다.

우리는 가볍게 진행합니다: 몇 줄의 Python 코드, 인기 있는 SVG 헬퍼 라이브러리, 그리고 간단한 설명만 있으면 됩니다. 끝까지 따라오면 폴더에 바로 사용할 수 있는 `circle.svg` 파일이 생성되고, 각 단계가 왜 중요한지 이해하게 될 것입니다—흐릿한 “문서 참고” 같은 지름길은 없습니다.

## What You’ll Need

- Python 3.8+ (최근 버전이면 모두 가능)
- `svgwrite` 패키지 – `pip install svgwrite` 로 설치
- 텍스트 편집기 또는 IDE (VS Code, PyCharm, 혹은 메모장도 OK)
- 파일을 저장하려는 디렉터리에 대한 쓰기 권한

그게 전부입니다. 무거운 의존성도 없고 외부 서비스도 필요 없습니다.

## Step 1: Set Up the SVG Document

SVG 문서를 만드는 것은 `svgwrite` 의 `Drawing` 객체를 인스턴스화하는 것만큼 간단합니다. 이 객체를 모든 도형이 살아가는 빈 캔버스로 생각하면 됩니다.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Why this matters:** `Drawing` 클래스는 XML 보일러플레이트—네임스페이스, 헤더, 루트 `<svg>` 요소—를 모두 처리해 줍니다. 파일명을 미리 지정하면 나중에 **save svg file** 단계가 매우 간단해집니다.

### Pro tip
많은 파일을 루프 안에서 생성할 계획이라면 각 `Drawing` 에 고유한 이름을 부여하거나 `io.BytesIO` 를 사용해 메모리 상에 모두 보관한 뒤 필요할 때 쓰기 작업을 수행하세요.

## Step 2: Add a Circle to the SVG

이제 문서가 준비됐으니 **add circle to SVG** 해봅시다. `add()` 메서드는 어떤 도형 객체든 받아들입니다; `Circle` 은 중앙에 간단한 빨간 점을 찍기에 안성맞춤입니다.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Why we use `center` and `radius` variables:** 숫자를 하드코딩하면 코드 가독성과 유지보수가 어려워집니다. 값을 변수에 담아 이름을 붙이면 의도가 명확해집니다—이 원은 200 × 200 캔버스의 정확히 가운데에 위치하고, 눈에 띄기에 충분히 큽니다.

### Edge case – Transparent background
투명 배경이 필요하다면(기본 SVG 배경) 루트에 `fill` 을 지정하지 않으면 됩니다. 흰색 배경을 원한다면 다음 코드를 추가하세요:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

원 추가 전에 이 코드를 넣어야 사각형이 원 아래에 위치합니다.

## Step 3: Save the SVG File

도형이 준비되었으니 마지막으로 **save SVG file** 을 수행합니다. `save()` 메서드는 XML을 디스크에 기록하고, 이미 `Drawing` 에 파일명을 지정했기 때문에 한 번의 호출만으로 작업이 끝납니다.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **What happens under the hood?** `svgwrite` 는 요소 트리를 문자열로 직렬화하고 XML 선언을 추가한 뒤 UTF‑8 인코딩으로 파일에 씁니다. 대상 디렉터리가 존재하지 않으면 Python 이 `FileNotFoundError` 를 발생시키니, 경로가 올바른지 확인하거나 `os.makedirs()` 로 미리 만들어 주세요.

### Bonus: Export graphic as SVG programmatically

SVG 내용을 문자열로 바로 얻고 싶다면(예: HTML 이메일에 삽입) `save()` 대신 `dwg.tostring()` 을 호출하면 됩니다:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Full Working Example

전체 흐름을 한 번에 보여주는 완전한 실행 스크립트는 다음과 같습니다:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Expected output:** 스크립트를 실행하면 동일한 폴더에 `circle.svg` 파일이 생성됩니다. 브라우저나 벡터 편집기로 열면 흰색 사각형 중앙에 빨간 원이 표시됩니다—우리가 코딩한 그대로입니다.

## Common Questions & Gotchas

- **다른 도형을 그리고 싶다면?** `dwg.circle` 을 `dwg.rect`, `dwg.ellipse` 혹은 사용자 정의 `<path>` 문자열로 바꾸면 됩니다. API 가 모든 도형에 대해 일관됩니다.
- **SVG 를 HTML에 직접 삽입할 수 있나요?** 물론 가능합니다. 방금 만든 파일은 `<img src="circle.svg" alt="Red circle">` 로 참조하거나 `<svg>` 태그 안에 인라인할 수 있습니다.
- **왜 직접 XML을 작성하지 않나요?** 직접 작성할 수도 있지만 `svgwrite` 와 같은 라이브러리는 네임스페이스 문제를 처리하고, 특히 그라디언트나 애니메이션을 추가할 때 코드를 훨씬 유지보수하기 쉽게 만들어 줍니다.

## Conclusion

이제 **create SVG document**, **add circle to SVG**, **save SVG file** 을 몇 줄의 Python 코드만으로 수행하고 **export graphic as SVG** 할 수 있게 되었습니다. 이 패턴은 확장성이 뛰어나서 원을 다른 벡터 도형으로 교체하거나, 데이터를 순회해 차트를 만들거나, 디자인 시스템을 위한 에셋을 일괄 처리하는 데 활용할 수 있습니다.

다음 단계는? 텍스트 라벨을 추가해 보거나, 그라디언트를 실험해 보거나, 한 스크립트로 아이콘 갤러리를 전체 생성해 보세요. 더 고급 기능이 궁금하다면 `svgwrite` 문서에서 그룹(`<g>`), 변환, 애니메이션 지원 부분을 확인해 보세요.

Happy coding, and may your vectors always stay crisp!

## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하여 밀접하게 연관된 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공하므로, 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Java용 Aspose.HTML에서 SVG 문서 저장](/html/english/java/saving-html-documents/save-svg-document/)
- [Java용 Aspose.HTML에서 SVG 문서 만들기 및 관리](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Aspose.HTML for Java로 SVG를 이미지로 변환](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}