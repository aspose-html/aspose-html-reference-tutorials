---
title: Java용 Aspose.HTML을 사용하는 DOM 돌연변이 관찰자
linktitle: DOM 돌연변이 관찰자 - 노드 추가 관찰
second_title: Aspose.HTML을 사용한 Java HTML 처리
description: 이 단계별 가이드에서 Java용 Aspose.HTML을 사용하여 DOM Mutation Observer를 구현하는 방법을 알아보세요. DOM 변경 사항을 효과적으로 모니터링하고 대응합니다.
type: docs
weight: 11
url: /ko/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

HTML 문서의 DOM(문서 개체 모델) 변경 사항을 관찰하고 이에 대응하려는 Java 개발자이신가요? Java용 Aspose.HTML은 이 작업을 위한 강력한 솔루션을 제공합니다. 이 단계별 가이드에서는 Java용 Aspose.HTML을 사용하여 HTML 문서를 생성하고 Mutation Observer로 노드 추가를 관찰하는 방법을 살펴보겠습니다. 이 튜토리얼에서는 각 예를 여러 단계로 나누어 프로세스를 안내합니다. 결국에는 Java 프로젝트에서 DOM Mutation Observer를 쉽게 구현할 수 있습니다.

## 전제 조건

Java용 Aspose.HTML을 사용하기 전에 필요한 전제 조건이 갖추어져 있는지 확인하십시오.

1. Java 개발 환경: 시스템에 JDK(Java Development Kit)가 설치되어 있는지 확인하십시오.

2.  Java용 Aspose.HTML: Java용 Aspose.HTML을 다운로드하여 설치해야 합니다. 다운로드 링크를 찾을 수 있습니다[여기](https://releases.aspose.com/html/java/).

3. IDE(통합 개발 환경): IntelliJ IDEA 또는 Eclipse와 같은 선호하는 Java IDE를 사용하여 Java 코드를 작성하고 실행합니다.

## 패키지 가져오기

Java용 Aspose.HTML을 시작하려면 필수 패키지를 Java 코드로 가져와야 합니다. 방법은 다음과 같습니다.

```java
// 필요한 패키지 가져오기
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// 빈 HTML 문서 만들기
HTMLDocument document = new HTMLDocument();
```

이제 필요한 패키지를 가져왔으므로 Java에서 DOM Mutation Observer를 구현하는 단계별 가이드로 넘어가겠습니다.

## 1단계: 돌연변이 관찰자 인스턴스 생성

먼저 Mutation Observer 인스턴스를 생성해야 합니다. 이 관찰자는 DOM의 변경 사항을 관찰하고 돌연변이가 발생하면 콜백 함수를 실행합니다.

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

이 단계에서는 노드가 DOM에 추가될 때 메시지를 인쇄하는 콜백 함수를 사용하여 관찰자를 만듭니다.

## 2단계: 관찰자 구성

이제 원하는 옵션으로 관찰자를 구성해 보겠습니다. 우리는 하위 목록 변경, 하위 트리 변경, 문자 데이터 변경을 관찰하려고 합니다.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// 지정된 구성으로 관찰할 대상 노드를 전달합니다.
observer.observe(document.getBody(), config);
```

 여기서는`config` 하위 목록, 하위 트리 및 문자 데이터 변경 사항을 관찰할 수 있는 개체입니다. 그런 다음 대상 노드(이 경우 문서의`<body>`) 및 관찰자에 대한 구성입니다.

## 3단계: DOM 수정

이제 관찰자를 트리거하기 위해 DOM을 일부 변경하겠습니다. 단락 요소를 만들어 문서 본문에 추가하겠습니다.

```java
// 단락 요소를 만들어 문서 본문에 추가합니다.
Element p = document.createElement("p");
document.getBody().appendChild(p);

// 텍스트를 만들고 단락에 추가합니다.
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

이 단계에서는 HTML 단락 요소를 생성하여 문서 본문에 추가합니다. 그런 다음 "Hello World" 콘텐츠가 포함된 텍스트 노드를 만들고 이를 단락에 추가합니다.

## 4단계: 관찰 대기(비동기식)

돌연변이는 비동기적으로 관찰되므로 관찰자가 변경 사항을 포착할 수 있도록 잠시 기다려야 합니다. 우리는 사용할 것이다`synchronized` 그리고`wait` 이를 위해 아래와 같이 .

```java
// 돌연변이는 비동기 모드에서 작동하므로 몇 초 동안 기다리십시오.
synchronized (this) {
    wait(5000);
}
```

여기서는 관찰자가 돌연변이를 포착할 수 있도록 5초 동안 기다립니다.

## 5단계: 관찰 중단

마지막으로 관찰이 끝나면 관찰자의 연결을 끊고 리소스를 해제하는 것이 중요합니다.

```java
// 관찰 중지
observer.disconnect();
```

이 단계를 통해 관찰을 완료하고 리소스를 정리할 수 있습니다.

## 결론

이 튜토리얼에서는 Java용 Aspose.HTML을 사용하여 DOM Mutation Observer를 구현하는 과정을 살펴보았습니다. 관찰자를 만들고, 구성하고, DOM을 변경하고, 관찰을 기다리고, 관찰을 중지하는 방법을 배웠습니다. 이제 Java 프로젝트에 DOM Mutation Observer를 적용하여 HTML 문서의 DOM 변경 사항을 효과적으로 모니터링하고 대응할 수 있는 기술을 갖추게 되었습니다.

질문이 있거나 문제가 발생하면 주저하지 말고[Aspose.HTML 포럼](https://forum.aspose.com/) . 또한 다음 항목에 액세스할 수 있습니다.[선적 서류 비치](https://reference.aspose.com/html/java/) Java용 Aspose.HTML에 대한 자세한 내용은 여기를 참조하세요.

## FAQ

### Q1: DOM Mutation Observer란 무엇입니까?

A1: DOM Mutation Observer는 HTML 문서의 DOM(문서 개체 모델) 변경 사항을 감시할 수 있는 JavaScript 기능입니다. DOM 노드의 추가, 삭제 또는 수정에 실시간으로 반응하는 방법을 제공합니다.

### Q2: 상업용 프로젝트에서 Java용 Aspose.HTML을 사용할 수 있나요?

 A2: 예, 상용 프로젝트에서 Java용 Aspose.HTML을 사용할 수 있습니다. 라이센스 및 구매정보를 확인하실 수 있습니다.[여기](https://purchase.aspose.com/buy).

### Q3: Aspose.HTML for Java에 대한 무료 평가판이 있습니까?

 A3: 예, Java용 Aspose.HTML 무료 평가판을 받을 수 있습니다.[여기](https://releases.aspose.com/). 이를 통해 구매하기 전에 해당 기능을 탐색할 수 있습니다.

### Q4: 돌연변이 관찰자로 캐릭터 데이터 변화를 관찰하면 어떤 이점이 있나요?

대답 4: 문자 데이터 변경 사항을 관찰하는 것은 HTML 요소의 텍스트 콘텐츠 변경 사항을 모니터링하고 이에 반응하려는 시나리오에 유용합니다. 예를 들어 웹 양식의 사용자 입력을 추적하고 이에 응답하는 데 사용할 수 있습니다.

### Q5: Java용 Aspose.HTML을 사용할 때 리소스를 어떻게 폐기합니까?

 A5: 완료되면 리소스를 해제하는 것이 중요합니다. 이 예에서는`document.dispose()` HTML 문서와 관련된 리소스를 정리합니다. 메모리 누수를 방지하려면 생성한 개체와 리소스를 모두 삭제하세요.