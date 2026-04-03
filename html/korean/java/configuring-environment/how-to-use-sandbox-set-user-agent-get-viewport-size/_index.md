---
category: general
date: 2026-04-03
description: Aspose.HTML Java에서 샌드박스를 사용해 사용자 에이전트를 설정하고, 크기를 지정하며, 뷰포트 크기를 즉시 가져오는
  방법을 배워보세요. 전체 코드, 설명 및 팁이 포함되어 있습니다.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: ko
og_description: Aspose.HTML Java에서 샌드박스를 사용해 사용자 에이전트를 설정하고, 크기를 지정하며, 뷰포트 크기를 즉시
  가져오는 방법을 배워보세요. 코드와 모범 사례가 포함된 완전한 가이드.
og_title: 샌드박스 사용 방법 – 사용자 에이전트 설정 및 뷰포트 크기 가져오기
tags:
- AsposeHTML
- Java
- Sandbox
title: 샌드박스 사용 방법 – 사용자 에이전트 설정 및 뷰포트 크기 가져오기
url: /ko/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 샌드박스 사용 방법 – 사용자 에이전트 설정 및 뷰포트 크기 가져오기

Aspose.HTML for Java로 HTML을 렌더링할 때 **샌드박스를 어떻게 사용하는지** 궁금하셨나요? 특정 화면 크기를 시뮬레이션하려다 막히거나, 페이지가 모바일 브라우저에서 방문된 것처럼 동작하도록 사용자‑에이전트 문자열을 위조해야 할 수도 있습니다.  

좋은 소식은 샌드박스 API를 사용하면 바로 그 작업을 할 수 있으며, 페이지가 로드된 후 계산된 뷰포트 크기도 가져올 수 있다는 점입니다. 이 튜토리얼에서는 샌드박스를 생성하고, 크기를 설정하고, 사용자 지정 사용자 에이전트를 지정하고, 원격 페이지를 로드한 뒤 최종적으로 뷰포트 차원을 읽는 과정을 단계별로 살펴봅니다. 끝까지 읽으면 **크기 설정 방법**, **뷰포트 가져오기 방법**, 그리고 이러한 단계가 신뢰할 수 있는 헤드리스 렌더링에 왜 중요한지 알게 됩니다.

> **빠른 성과:** 몇 초 안에 `Viewport: 1280×800` 와 같은 출력을 하는 실행 가능한 Java 클래스를 얻을 수 있습니다.

---

## 필요 사항

- **Aspose.HTML for Java** 버전 24.6 이상 (우리가 사용하는 API는 24.5에서 도입되었습니다).  
- Java 17+ 개발 키트 (최근 JDK이면 모두 사용 가능).  
- IDE 또는 간단한 텍스트 편집기—특별한 플러그인 필요 없음.  
- `https://example.com` 와 같은 외부 URL을 로드하려면 인터넷 연결이 필요합니다.

이것만 있으면 됩니다. Maven/Gradle 같은 빌드 도구가 필수는 아니며, 원한다면 JAR 파일을 직접 클래스패스에 넣어 사용할 수 있습니다.

---

## 샌드박스 사용 방법 – 개요

샌드박스는 렌더링 엔진을 호스트 OS와 격리시켜 가상 화면(너비, 높이, DPI)과 사용자 지정 **user agent** 문자열을 정의할 수 있게 합니다. 메모리 안에만 존재하는 작은 브라우저 창이라고 생각하면 됩니다. 이후 `HTMLDocument`의 기본 뷰를 요청하면 엔진은 샌드박스 설정을 기반으로 계산한 **viewport size** 를 반환합니다.

다음은 고수준 흐름도입니다:

1. `DocumentSandbox`을 **생성**하고 너비, 높이, DPI, 그리고 user‑agent를 설정합니다.  
2. 해당 샌드박스 안에서 `HTMLDocument`를 **로드**합니다.  
3. 문서의 기본 뷰를 **조회**하여 뷰포트 크기를 얻습니다.  

각 단계를 자세히 살펴보겠습니다.

---

## 단계 1: 샌드박스 생성 및 크기 설정

먼저 샌드박스를 시작하고 가상 화면의 크기를 지정합니다. 여기서 **headless 렌더링을 위한 크기 설정 방법**을 답하게 됩니다.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **전문가 팁:** 반응형 레이아웃을 테스트한다면, 전화기를 에뮬레이트하기 위해 `360` 같은 좁은 너비를, 데스크톱을 위해 `1920` 같은 넓은 너비를 시도해 보세요. 샌드박스는 설정한 DPI를 그대로 반영하므로, 고밀도 화면(예: 144 DPI)은 `device-pixel-ratio`를 사용하는 미디어 쿼리에 영향을 줍니다.

---

## 단계 2: 샌드박스 사용자 에이전트 설정

왜 사용자 지정 **user agent**를 사용해야 할까요? 일부 사이트는 보고된 브라우저에 따라 다른 마크업이나 스크립트를 제공합니다. `setUserAgent`를 호출하면 페이지가 Chrome, Firefox, 혹은 모바일 기기에서 방문된 것처럼 속일 수 있습니다.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

이제 페이지는 iPhone에서 렌더링되는 것으로 인식합니다. 기본값으로 **user agent**를 다시 설정하려면 앞에서 사용한 “AsposeHTML/24.6 …” 문자열을 재사용하면 됩니다.

---

## 단계 3: 샌드박스 내부에 HTML 문서 로드

샌드박스가 준비되면任意의 URL이나 로컬 HTML 파일을 로드할 수 있습니다. `HTMLDocument` 생성자는 두 번째 인자로 샌드박스를 받아 두 객체를 연결합니다.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

`try‑with‑resources` 블록은 문서가 적절히 해제되도록 보장하여 Aspose.HTML이 내부에서 할당한 네이티브 리소스를 해제합니다.

---

## 단계 4: 문서에서 뷰포트 크기 가져오기

이제 기다리던 순간입니다: 렌더링 엔진이 계산한 **viewport size**를 가져오는 단계입니다. 이는 페이지 레이아웃이 완료된 후 **뷰포트 가져오기 방법**에 대한 답이 됩니다.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

프로그램을 실행하면 다음과 같은 출력이 나타납니다:

```
Viewport: 1280×800
```

Step 1에서 샌드박스 차원을 변경했다면, 출력된 숫자는 새로운 값들을 반영합니다—반응형 브레이크포인트를 검증하는 자동화 테스트에 최적입니다.

---

## 전체 동작 예제

아래는 모든 요소를 결합한 완전한 실행 가능한 클래스입니다. `SandboxExample.java`라는 파일에 복사·붙여넣기하고, Aspose.HTML JAR를 클래스패스에 추가한 뒤 `java SandboxExample`을 실행하십시오.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**예상 출력** (위의 샌드박스 설정을 가정할 경우):

```
Viewport: 1280×800
```

샌드박스에서 다른 너비/높이를 설정하면 출력이 그에 맞게 변경됩니다—반응형 디자인을 테스트할 때 정확히 필요한 기능입니다.

---

## 엣지 케이스 및 일반 질문

### 페이지가 CSS 미디어 쿼리 대신 `window.innerWidth`를 사용할 경우는?

샌드박스의 가상 화면 크기는 CSS 레이아웃과 JavaScript의 `window.innerWidth/innerHeight` 모두에 영향을 미칩니다. 따라서 JavaScript를 통해 **뷰포트 가져오기**를 하면 Java 콘솔에서 보는 숫자와 동일한 값을 반환합니다.

### 여러 샌드박스를 병렬로 실행할 수 있나요?

네. 각 `DocumentSandbox` 인스턴스는 독립적이므로 스레드 풀을 생성하고 각 스레드에 서로 다른 차원의 샌드박스를 할당해 수십 개의 페이지를 동시에 렌더링할 수 있습니다. JAR가 스레드‑안전하도록 유지하면 됩니다(이미 스레드‑안전합니다).

### DPI 설정이 이미지 스케일링에 영향을 미치나요?

물론입니다. DPI가 높을수록 하나의 CSS 픽셀이 더 많은 디바이스 픽셀에 매핑되어 고해상도 이미지가 더 선명하게 보입니다. 레티나 스타일 자산을 테스트한다면 `sandbox.setDeviceDpi(144)`를 시도해 보세요.

### How do I handle HTTPS certificates that are self

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}