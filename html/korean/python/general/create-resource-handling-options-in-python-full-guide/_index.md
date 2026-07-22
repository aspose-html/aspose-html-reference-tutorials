---
category: general
date: 2026-07-21
description: Python에서 리소스 처리 옵션을 만들고 HTML 파싱을 위한 최대 처리 깊이 설정 방법을 배워보세요. 신뢰할 수 있는 리소스
  관리를 위해 단계별 튜토리얼을 따라가세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: ko
lastmod: 2026-07-21
og_description: Python에서 리소스 처리 옵션을 만들고, 안전한 HTML 문서 로드를 위한 최대 처리 깊이 설정 방법을 즉시 확인하세요.
  몇 분 안에 이 기술을 마스터하세요.
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: Python에서 리소스 처리 옵션 만들기 – 완전한 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: Python에서 리소스 처리 옵션 만들기 – 전체 가이드
url: /ko/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python에서 리소스 처리 옵션 만들기 – 전체 가이드

거대한 HTML 페이지에 대해 메모리를 초과하지 않으면서 **리소스 처리 옵션을 만들** 수 있는 방법이 궁금하셨나요? 당신만 그런 것이 아닙니다. 거대한 문서를 파서에 넣으면 프레임, iframe, 연결된 CSS와 같은 중첩된 리소스가 금방 제어 불가능해질 수 있습니다.  

좋은 소식은? 파서에게 일정 수준 이상의 중첩 레벨에 도달하면 멈추라고 지시할 수 있습니다. 이 튜토리얼에서는 **max handling depth를 설정하는 방법**을 보여드리고 애플리케이션이 응답성을 유지하도록 합니다. 준비되셨나요? 바로 시작합니다.

## 배울 내용

- 성능 및 보안을 위해 중첩 깊이를 제한하는 것이 왜 중요한지.  
- `ResourceHandlingOptions` 클래스를 사용해 **리소스 처리 옵션을 만들**기 위한 정확한 코드.  
- 파서가 세 단계 이후에 멈추도록 `max_handling_depth`를 구성하는 방법.  
- 순환 참조나 누락된 리소스와 같은 엣지 케이스를 처리하는 팁.  

라이브러리에 대한 사전 경험은 필요하지 않습니다—Python 3이 설치되어 있고 파일 I/O에 대한 기본 이해만 있으면 됩니다.

## 사전 요구 사항

- Python 3.8+ (라이브러리는 최신 버전 모두에서 동작합니다).  
- `HTMLDocument`와 `ResourceHandlingOptions`를 제공하는 `htmlparser` 패키지.  
- 참조할 수 있는 폴더에 위치한 샘플 HTML 파일(`big_page.html`).  

아직 패키지를 설치하지 않았다면 다음을 실행하세요:

```bash
pip install htmlparser
```

이제 기본 준비가 끝났으니 본격적인 내용으로 들어갑니다.

## 리소스 처리 옵션 만들기 – Step 1

먼저 `ResourceHandlingOptions` 인스턴스를 만들어야 합니다. 이는 파서가 따라야 할 제한 및 정책을 설정할 수 있는 도구 상자와 같습니다.

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**왜 중요한가:**  
파서가 `<iframe>` 안에 또 다른 `<iframe>`을 만나면 보통 무한히 체인을 따라갑니다. 깊이를 `3`으로 제한하면 RAM을 고갈시키거나 스택 오버플로우를 일으킬 수 있는 무제한 재귀를 방지할 수 있습니다.  

> **프로 팁:** 신뢰할 수 없는 콘텐츠(예: 사용자가 업로드한 HTML)를 파싱할 경우, 잠재적 공격을 완화하기 위해 깊이를 `1` 또는 `2`로 낮추는 것을 고려하세요.

## HTML 문서 로드 – Step 2

옵션 객체가 준비되었으면 `HTMLDocument`에 전달합니다. 생성자는 방금 설정한 `max_handling_depth`를 존중합니다.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**내부에서 무슨 일이 일어나나요?**  
`HTMLDocument`는 파일을 읽고 DOM 트리를 만든 뒤 모든 외부 리소스(스타일시트, 스크립트, 이미지)를 순회합니다. 중첩된 리소스를 만나면 `resource_options.max_handling_depth`를 확인합니다. 제한에 도달하면 파서는 경고를 로그에 남기고 추가 중첩을 건너뜁니다.  

즉, 처음 세 레이어에 대해서는 완전한 DOM을 얻고 나머지는 안전하게 무시됩니다.

## 설정 확인 – Step 3

설정이 실제로 적용됐는지 확인하는 것이 좋습니다. `resource_options` 객체는 현재 상태를 노출하므로 출력하거나 테스트에서 단언할 수 있습니다.

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

단언이 통과하면 파서가 실행 전체에 걸쳐 제한을 준수한다는 확신을 가질 수 있습니다.

## 엣지 케이스 처리

### 순환 참조

일부 레거시 사이트는 원본 페이지를 가리키는 iframe을 삽입해 루프를 만들기도 합니다. `max_handling_depth`가 설정되어 있으면 세 번째 반복 이후에 루프가 자동으로 차단됩니다. 그러나 로그에 경고가 남을 수 있습니다. 시끄러운 로그를 없애려면 로거 레벨을 조정하세요:

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### 누락된 리소스

중첩된 리소스가 로드에 실패하면(404 또는 네트워크 타임아웃) 파서는 기본적으로 예외를 발생시킵니다. `try/except` 블록으로 로드 호출을 감싸면 애플리케이션이 계속 실행됩니다:

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### 깊이 동적 조정

파이프라인의 서로 다른 부분에 대해 다른 깊이가 필요할 때가 있습니다. `resource_options`는 가변 객체이므로 실행 중에 `max_handling_depth`를 변경할 수 있습니다:

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

단, 다른 스레드에서 동일한 옵션 인스턴스를 재사용하기 전에 값을 재설정하는 것을 잊지 마세요.

## 전체 작동 예제

아래는 바로 복사‑붙여넣기하고 파일 경로만 조정하면 즉시 실행할 수 있는 완전한 스크립트입니다.

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**예상 출력(파일이 존재하고 올바르게 형식화된 경우):**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

파일을 읽을 수 없으면 충돌 대신 오류 메시지가 표시됩니다.

![Python에서 리소스 처리 옵션 만들기](/images/resource-options.png){alt="Python에서 리소스 처리 옵션 만들기"}

## 요약 – 이 접근 방식이 뛰어난 이유

- **안전 우선:** 중첩 깊이 제한으로 무제한 재귀와 메모리 폭주를 방지합니다.  
- **유연성:** 런타임에 `max_handling_depth`를 변경해 다양한 시나리오에 대응할 수 있습니다.  
- **단순성:** 몇 줄의 코드만으로 **리소스 처리 옵션을 만들**고 즉시 적용할 수 있습니다.  

요약하면, 이제 파서가 외부 리소스를 얼마나 깊이 따라갈지 제어할 수 있는 견고한 패턴을 갖추게 되었습니다.

## 다음 단계

- `ResourceHandlingOptions` 클래스를 더 탐색해 보세요—캐싱, 타임아웃 처리, MIME‑type 필터링을 위한 플래그가 있습니다.  
- 깊이 제한을 커스텀 `UserAgent` 문자열과 결합해 공격적인 서버에 차단당하는 것을 방지하세요.  
- 비동기 I/O를 사용한다면 `asyncio`와 함께 동작하면서 동일한 옵션을 지원하는 `aiohtmlparser` 변형을 살펴보세요.  

자유롭게 실험해 보세요: 깊이를 `0`으로 설정하면 파서가 모든 외부 참조를 무시합니다. 원시 HTML 마크업만 필요할 때 유용한 바로가기입니다.

궁금한 점이나 여전히 문제를 일으키는 페이지가 있나요? 아래에 댓글을 남겨 주세요. 설정을 미세 조정하는 데 기꺼이 도와드리겠습니다. 즐거운 파싱 되세요!

## 다음에 배울 내용

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함해 추가 API 기능을 마스터하고 프로젝트에 적용할 수 있도록 돕습니다.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Create sandbox for HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}