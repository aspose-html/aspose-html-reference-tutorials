---
category: general
date: 2026-10-15
description: Python에서 Markdown 저장을 위한 리소스 처리 옵션을 만드는 방법과 최대 처리 깊이를 설정하는 방법을 배워보세요.
  단계별 가이드를 따라하세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: ko
lastmod: 2026-10-15
og_description: Python에서 리소스 처리 옵션을 생성하여 중첩된 리소스 처리를 제어합니다. 이 튜토리얼에서는 신뢰할 수 있는 Markdown
  내보내기를 위해 최대 처리 깊이를 설정하는 방법을 보여줍니다.
og_image_alt: Screenshot showing Python code to create resource handling options and
  set max handling depth
og_title: 리소스 처리 옵션 만들기 – Python 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Learn how to create resource handling options and how to set max handling
    depth for Markdown saving in Python. Follow a step‑by‑step guide.
  headline: How to create resource handling options with Python
  type: TechArticle
tags:
- resource handling
- Markdown
- Python
- options
title: Python을 사용하여 리소스 처리 옵션을 만드는 방법
url: /ko/python/general/how-to-create-resource-handling-options-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python으로 리소스 처리 옵션 만들기

Markdown 내보내기를 위해 **리소스 처리 옵션을 생성**해야 하는 경우, 이 가이드는 완전한 솔루션을 제공합니다. **max handling depth를 설정하는 방법**을 정확히 확인하여 중첩된 리소스가 원하는 수준 이후에 처리를 중단하도록 할 수 있습니다.

리소스 처리는 이미지, 임베디드 파일 또는 기타 연결된 자산을 포함하는 복잡한 문서에서 Markdown을 생성할 때 필수적입니다. 제어되지 않은 재귀는 성능 문제나 메모리 부족 오류를 초래할 수 있습니다. 처리 깊이를 구성함으로써 프로세스를 예측 가능하고 효율적으로 유지할 수 있습니다.

이 튜토리얼에서는 다음을 수행합니다:

* `ResourceHandlingOptions` 객체를 초기화합니다.
* 최대 처리 깊이를 구성합니다.
* 옵션을 `MarkdownSaveOptions` 인스턴스에 연결합니다.
* 프로젝트에 복사해 사용할 수 있는 전체 예제를 실행합니다.

표준 SDK 외에 외부 라이브러리는 필요하지 않으며, 코드는 2026년 10월 현재 최신 버전의 Python 패키지와 함께 작동합니다.

## 전제 조건

시작하기 전에 다음이 설치되어 있는지 확인하십시오:

* Python 3.9 이상.
* `ResourceHandlingOptions`와 `MarkdownSaveOptions`를 제공하는 SDK(예: `groupdocs-viewer` 또는 유사 패키지). 다음 명령으로 설치합니다:

```bash
pip install groupdocs-viewer
```

* Python 클래스와 객체 속성에 대한 기본적인 이해.

## 단계 1: 리소스 처리 옵션 만들기

첫 번째 단계는 **리소스 처리 옵션을 생성**하는 것입니다. 이 객체는 모든 리소스 관련 설정을 담는 컨테이너 역할을 합니다.

```python
from groupdocs.viewer import ResourceHandlingOptions, MarkdownSaveOptions

# Step 1: Instantiate the options object
resource_options = ResourceHandlingOptions()
```

`ResourceHandlingOptions`는 기본적으로 제한을 적용하지 않으며, 이는 뷰어가 발견하는 모든 연결된 리소스를 따라간다는 의미입니다. 객체를 초기화하면 정밀한 제어를 적용할 수 있는 깨끗한 상태가 됩니다.

## 단계 2: max handling depth 설정 방법

이제 **max handling depth를 설정하는 방법**을 배웁니다. `max_handling_depth` 속성은 내보내기가 중단되기 전까지 처리할 중첩 레벨 수를 정의합니다.

```python
# Step 2: Limit the handling depth to five levels
resource_options.max_handling_depth = 5
```

깊이를 제한하는 이유는 무엇일까요? Markdown 문서가 다른 Markdown 파일을 참조하고, 그 파일이 또 다른 파일을 참조하는 식으로 무한히 이어질 수 있습니다. 깊이 제한이 없으면 내보내기가 무한히 재귀하여 메모리와 CPU를 소모할 수 있습니다. `max_handling_depth`를 `5`로 설정하면 엔진이 다섯 단계의 중첩 리소스 이후에 중단하도록 하며, 이는 대부분의 프로젝트에 안전한 기본값입니다.

### 예외 상황: 무제한 깊이

프로덕션에서는 드물지만 의도적으로 무제한 재귀를 원한다면 값을 `None`으로 설정하십시오:

```python
resource_options.max_handling_depth = None  # No limit
```

무제한 깊이는 매우 큰 문서 트리에서 성능 저하를 일으킬 수 있음을 유념하십시오.

## 단계 3: 옵션을 MarkdownSaveOptions에 연결하기

리소스 처리를 구성한 후에는 옵션을 `MarkdownSaveOptions` 인스턴스에 연결해야 합니다. 이렇게 하면 저장 시 내보내기가 해당 설정을 사용하게 됩니다.

```python
# Step 3: Create MarkdownSaveOptions and attach the resource handling config
markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

`MarkdownSaveOptions`는 모든 내보내기 관련 설정을 집계합니다. `resource_options`를 `resource_handling_options` 속성에 할당하면 변환 중에 깊이 제한이 적용됩니다.

## 단계 4: 전체 변환 실행 (옵션 데모)

다음 스니펫은 샘플 문서를 Markdown으로 완전 변환하는 예시를 보여줍니다. 환경에 맞게 파일 경로를 조정하십시오.

```python
from groupdocs.viewer import Viewer

# Path to the source document (e.g., a DOCX with embedded images)
source_path = "sample.docx"
# Path where the Markdown output will be saved
output_path = "output.md"

# Initialize the viewer with the source file
viewer = Viewer(source_path)

# Perform the conversion using the configured options
viewer.save(output_path, markdown_options)

print(f"Conversion complete. Markdown saved to {output_path}")
```

**예상 출력**

```
Conversion complete. Markdown saved to output.md
```

스크립트를 실행한 후 `output.md`를 열어보면 이미지 및 기타 리소스가 최대 다섯 단계까지 참조되는 것을 확인할 수 있습니다; 더 깊은 링크는 제외되어 무한 재귀를 방지합니다.

## 전문가 팁: 런타임에서 처리 깊이 확인하기

깊이 제한이 적용되었는지 확인하려면 생성된 Markdown에서 누락된 리소스 참조를 검사하거나 SDK에서 자세한 로깅을 활성화하십시오:

```python
viewer.set_logging(True)  # Enable detailed logs
```

로그에는 다음과 같은 메시지가 표시됩니다:

```
[INFO] Resource handling stopped at depth 5 for file 'nested_image.png'
```

## 일반적인 질문

**문서에 다섯 단계보다 적은 중첩 리소스만 있는 경우는 어떻게 되나요?**  
깊이 제한이 실제 깊이보다 높기 때문에 내보내기는 사용 가능한 모든 리소스를 처리합니다. 리소스가 잘리지는 않습니다.

**파일 유형별로 다른 제한을 설정할 수 있나요?**  
예. 각 내보내기 형식마다 별도의 `ResourceHandlingOptions` 객체를 생성하고 해당 `SaveOptions` 인스턴스에 할당하면 됩니다.

**깊이 제한이 이미지에만 적용되나요?**  
아니요. 제한은 *모든* 리소스에 적용됩니다. 여기에는 임베디드 파일, 하이퍼링크, 중첩된 Markdown 포함 등이 포함됩니다.

## 결론

이제 Python에서 신뢰할 수 있는 Markdown 내보내기를 위해 **리소스 처리 옵션을 생성**하고 **max handling depth를 설정**하는 방법을 알게 되었습니다. 재귀를 제한함으로써 과도한 메모리 사용을 방지하면서도 필요한 콘텐츠 계층 구조를 유지할 수 있습니다.

다음 단계로 살펴볼 내용:

* `extract_images` 또는 `preserve_links`와 같은 다른 `ResourceHandlingOptions` 속성을 조정합니다.
* 추출된 파일에 대한 사용자 지정 명명 규칙과 리소스 처리를 결합합니다.
* 다양한 깊이 값을 실험하여 특정 문서 집합에 최적의 값을 찾습니다.

코드 스니펫을 자신의 워크플로에 맞게 자유롭게 적용하고 커뮤니티와 결과를 공유하세요. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하여 밀접하게 관련된 주제를 다룹니다. 각 리소스에는 단계별 설명과 함께 완전한 작동 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Zip HTML in C# – Custom Resource Handler Tutorial](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-custom-resource-handler-tutorial/)
- [How to create custom schema handler with Aspose.HTML for Java](/html/english/java/custom-schema-message-handling/custom-schema-message-handler/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}