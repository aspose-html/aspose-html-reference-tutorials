---
date: 2025-12-10
description: Aspose를 사용하여 깨진 링크를 처리하고, HTML을 PNG로 변환하며, Aspose.HTML for Java를 사용해
  Java에서 HTML 문서를 로드하는 방법을 배워보세요.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Java에서 Aspose.HTML 메시지 핸들러 사용 방법
url: /ko/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML 메시지 핸들러를 Java에서 사용하는 방법

## 소개
이 튜토리얼에서는 HTML에서 인스턴스화된 리소스를 처리하기 **how to use aspose**를 오류로 시연합니다. 사용자화된 이미지를 참조하는 간단한 HTML 문서를 생성하고, 사용자 정의 메시지 핸들러를 연결한 뒤, **html 문서 로드** java를 활용해 향상된 링크를 좀 더 처리하는 방법을 보여줍니다. 마지막으로 Aspose.HTML을 사용하면 **html을 png로 변환**하여 수행하는 작업을 통해 Java에서 HTML-to-image 변환 전체를 시뮬레이션할 수 있습니다.

## 빠른 답변
- **메시지 처리기의 주요 목적은 무엇입니까?** 네트워크 작업을 고려하고 있는 배터리와 동일한 상태 코드를 처리하기 가능합니다.
- **Aspose.HTML이 HTML을 PNG로 변환할 수 있나요?** 네, `Converter.convertHTML`을 사용하면 HTML을 이미지로 변환할 수 있습니다.
- **이 예를 사용하려면 라이선스가 필요합니까?** 임시 전력으로 평가를 제한할 수 있지만, 실제 운영 환경에서는 권위가 필요합니다.
- **어떤 Java 버전이 지원됩니까?** JDK8이면 모두 지원됩니다(본 튜토리얼은 JDK11 사용).
- **깨진 여러 링크를 처리하는 것이 가능합니까?** 물론입니다 – 다양한 핸들러를 체인으로 연결해 다양한 시나리오를 관리할 수 있습니다.

## 전제 조건
단계별 가이드를 진행하기 전에 아래 항목을 모두 준비하세요:
1. Java Development Kit (JDK): 시스템에 JDK가 설치되어 있는지 확인합니다. [오라클 홈페이지](https://www.oracle.com/java/technologies/javase-downloads.html)에서 다운로드할 수 있습니다.
2. Aspose.HTML for Java: Aspose.HTML for Java가 설치되어 있어야 합니다. [Aspose 릴리스 페이지](https://releases.aspose.com/html/java/)에서 다운로드하세요.
3. IDE: IntelliJ IDEA, Eclipse, NetBeans 등 Java IDE를 선호합니다.
4. Java의 기본 지식: Java 프로그래밍에 대한 기본 지식이 필요합니다.
5. 임시 라이선스: Aspose.HTML 체험판을 사용 중이라면 개발 중 제한을 막기 위해 [임시 라이선스](https://purchase.aspose.com/temporary-license/)를 인증받으세요.

## 패키지 가져오기
프로젝트에 필요한 패키지를 먼저 import 해야 합니다. 아래는 필수 import 목록입니다:
```java
import java.io.IOException;
```
이 import 문들을 통해 네트워크 작업, HTML 문서 생성, HTML‑to‑PNG 변환 등에 필요한 클래스와 메서드에 접근할 수 있습니다.

## 1단계: HTML 코드 준비
먼저 이미지 파일을 참조하는 간단한 HTML 스니펫을 준비합니다. 오류 처리 메커니즘을 트리거하기 위해 존재하지 않는 이미지를 의도적으로 참조합니다.
```java
String code = "<img src='missing.jpg'>";
```
위 코드는 `missing.jpg` 를 가리키는 `<img>` 태그를 생성합니다. 이미지가 없기 때문에 네트워크 서비스는 200이 아닌 상태 코드를 반환하고, 이를 사용자 정의 핸들러가 잡게 됩니다.

## 2단계: HTML 코드를 파일에 저장
다음으로 HTML 스니펫을 파일로 저장해 Aspose.HTML이 문서로 로드할 수 있도록 합니다.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
`FileWriter` 를 사용해 HTML을 **document.html** 로 저장합니다. 이 파일이 이후 **load html document java** 단계의 소스가 됩니다.

## 3단계: 사용자 지정 메시지 처리기 생성
이제 이미지가 없을 때 동작할 사용자 정의 메시지 핸들러를 구현합니다. 핸들러는 HTTP 상태 코드를 확인하고 친절한 메시지를 출력합니다.
```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```
`invoke` 메서드에서 `context.getResponse().getStatusCode()` 를 검사합니다. 상태 코드가 **200** 이 아니면 파일이 누락되었다는 경고를 출력합니다. 마지막 `invoke(context);` 호출은 체인상의 다음 핸들러로 제어를 넘깁니다.

## 4단계: 네트워크 서비스 구성
Aspose.HTML이 우리 핸들러를 인식하도록 `Configuration` 클래스를 통해 네트워크 서비스에 등록합니다.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
여기서는 `Configuration` 인스턴스를 생성하고, `INetworkService` 를 가져온 뒤, 사용자 정의 핸들러를 컬렉션에 추가합니다. 이렇게 하면 이미지 로드와 같은 모든 네트워크 요청 시 핸들러가 실행됩니다.

## 5단계: HTML 문서 불러오기
구성 설정이 완료되었으니 앞서 만든 HTML 파일을 로드합니다. 이 단계는 **load html document java** 를 시연하면서 누락된 이미지가 핸들러를 트리거하도록 합니다.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```
`HTMLDocument` 생성자는 파일 경로와 커스텀 `configuration` 을 모두 받습니다. 문서가 `<img>` 태그를 파싱할 때 네트워크 서비스가 `missing.jpg` 를 요청하고 404 응답을 받으면, 핸들러가 경고를 출력합니다.

## 6단계: HTML을 PNG로 변환
Aspose.HTML의 전반적인 기능을 보여주기 위해 로드한 문서를 PNG 이미지로 변환합니다. 이는 전형적인 **convert html to png** 시나리오입니다.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` 은 `HTMLDocument`, 선택적 `ImageSaveOptions` (DPI, 품질 등 설정 가능), 출력 파일명을 인수로 받아 렌더링된 HTML을 래스터 이미지로 저장합니다.

## 7단계: 자원 정리
Java 애플리케이션에서는 리소스 관리를 철저히 해야 합니다. `Configuration` 과 `HTMLDocument` 를 모두 해제해 메모리 누수를 방지합니다.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
정리 코드를 `finally` 블록에 넣으면 예외가 발생하더라도 반드시 실행됩니다.

## 메시지 핸들러를 사용하는 이유는 무엇입니까?
메시지 핸들러를 사용하면 **깨진 링크를 처리합니다. java** 와 같은 네트워크 작업을 세밀하게 제어할 수 있습니다. 슬리버가 조용히 실패하는 대신에 로그아웃하거나 재시도, 교체, 대체 콘텐츠 제공 등을 구현해 HTML 처리를 위한 키보드 및 고급으로 만들 수 있습니다.

## 일반적인 문제 및 해결 방법
- **처리기 재귀** – `invoke(context);`를 한 번만 호출하도록 무한 루프를 방지합니다.
- **라이센스가 없습니다** – 존재하지 않으면 변환 결과에 워터마크가 삽입될 수 있습니다.
- **파일 경로 오류** – 절대 사용하지 않거나 작업복을 설정하여 **document.html** 로드 오류를 방지합니다.

## 자주 묻는 질문

**Q: 여러 메시지 핸들러를 연결할 수 있나요?**
A: 예, `network.getMessageHandlers()` 컬렉션에 여러 핸들러를 추가할 수 있습니다. 추가된 순서대로 실행됩니다.

**질문: 이 핸들러는 CSS나 스크립트 리소스에도 적용되나요?**
답변: 네, HTML 엔진에서 발생하는 모든 네트워크 요청(이미지, CSS, JS, 폰트)은 이 핸들러를 거칩니다.

**질문: HTTP 요청을 보내기 전에 어떻게 변경할 수 있나요?**
답변: `invoke(context)`를 호출하기 전에 `context.getRequest()`를 수정하는 핸들러를 구현하면 됩니다.

**질문: 특정 URL에 대한 경고를 숨기는 방법이 있나요?**
답변: 핸들러 내부에서 `context.getRequest().getRequestUri()`를 검사하고, 조건부로 로그를 건너뛰도록 설정하면 됩니다.

**질문: 이러한 API를 사용하려면 어떤 버전의 Aspose.HTML이 필요한가요?**
답변: 이 코드는 Aspose.HTML for Java 22.10 이상 버전에서 작동합니다.

## 결론
이제 **How ​​to use Aspose** 메시지 핸들러를 Java에서 사용하는 전체 과정을 이해하셨습니다. HTML 파일 생성, **깨진 링크 처리 java**를 사용자 정의 핸들러 연결, 문서 로드, 그리고 **html을 png로 변환** 지원하기까지 모두 진행했습니다. 이 패턴을 통해 리소스를 제공하고 관리하고 맞춤화하여 Aspose.HTML의 네트워킹 기능을 어떤 Java 기능에서도 확장할 수 있습니다.

---

**최종 업데이트:** 2025-12-10
**테스트 대상:** Java 24.11용 Aspose.HTML
**저자:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}