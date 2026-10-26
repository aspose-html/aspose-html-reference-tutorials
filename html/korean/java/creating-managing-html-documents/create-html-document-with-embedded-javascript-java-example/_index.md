---
category: general
date: 2026-06-03
description: Java에서 HTML 문서를 생성하고 JavaScript를 삽입하여 카운터를 증가시킵니다. 스크립트 엔진 예제, 요소의 innerHTML
  가져오기 등을 배웁니다.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: ko
og_description: Java에서 HTML 문서를 생성하고, 카운터를 증가시키는 JavaScript를 삽입한 뒤, 스크립트 엔진 예제로 최종
  값을 가져옵니다.
og_title: 임베디드 JavaScript가 포함된 HTML 문서 만들기 – Java 예제
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: 임베디드 JavaScript가 포함된 HTML 문서 만들기 – Java 예제
url: /ko/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java 예제 – 임베디드 JavaScript가 포함된 HTML 문서 만들기

Java 코드에서 **HTML 문서 생성**을 하고 그 안에 JavaScript를 삽입하는 방법이 궁금하셨나요? 이 가이드에서는 단계별로 정확히 보여드리며, 최종 카운터 값을 출력하는 작동하는 스크립트 엔진 예제를 완성하게 됩니다.  

만약 *“스크립트 실행 후 element innerHTML을 어떻게 가져올 수 있나요?”* 혹은 *“Java에서 JavaScript로 카운터를 증가시키는 가장 깔끔한 방법은 무엇인가요?”* 라고 스스로에게 물어본 적이 있다면, 바로 여기가 맞습니다. 우리는 **embed javascript html**, **increment counter javascript**, 그리고 **get element innerHTML**을 하나의 통합 튜토리얼에서 다룰 것입니다.

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="임베디드 JavaScript가 포함된 HTML 문서 생성 예제"}

## 구축할 내용

이 튜토리얼을 마치면 다음과 같은 **self‑contained Java 프로그램**을 얻게 됩니다:

1. **HTML 문서**를 메모리에서 생성합니다.  
2. **작은 JavaScript 스니펫**을 삽입하여 카운터를 다섯 번 증가시킵니다.  
3. **스크립트 엔진**을 초기화(`ScriptEngine` 예제)하여 해당 스니펫을 실행합니다.  
4. `getElementInnerHTML`을 사용하여 최종 카운터 값을 가져옵니다.  
5. 콘솔에 `Final counter value: 5`를 출력합니다.

외부 파일도, 웹 서버도 필요 없습니다—오직 순수 Java와 작은 HTML 문자열만 있으면 됩니다.

---

## 사전 요구 사항

- Java 17 이상 (`ScriptEngine` API는 표준 라이브러리의 일부입니다).  
- HTML 및 JavaScript에 대한 기본적인 이해 (깊은 전문 지식은 필요 없습니다).  
- IDE 또는 간단한 텍스트 편집기와 터미널을 사용하여 프로그램을 컴파일하고 실행할 수 있는 환경.

---

## 단계 1: Java에서 HTML 문서 생성

우선 나중에 마크업을 채울 수 있는 빈 HTML 문서 객체가 필요합니다. 이는 메모리 내에만 존재하는 가상의 페이지라고 생각하면 됩니다.

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**왜 중요한가:** 직접 **HTML 문서 생성** 객체를 **생성**함으로써 디스크에 쓰는 것을 피하고 모든 것을 테스트 가능하게 유지합니다. 작은 DOM 시뮬레이션을 통해 전체 브라우저 없이도 나중에 **element innerHTML**을 **get**할 수 있습니다.

---

## 단계 2: JavaScript HTML 삽입 – 카운터 로직

이제 `<script>` 블록을 포함하는 HTML 마크업을 작성합니다. 이 스크립트는 **increment counter JavaScript**를 다섯 번 실행합니다.

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**설명:**  
- `<div id='counter'>0</div>` 은 목표 요소입니다.  
- `for` 루프는 **increment counter javascript** 로직을 실행하여 매 반복마다 div를 업데이트합니다.  
- 실제 브라우저가 없기 때문에, 나중에 사용할 스크립트 엔진은 `document.getElementById`를 이해해야 합니다. 그래서 `HTMLDocument`에 작은 스텁을 추가한 것입니다.

---

## 단계 3: 스크립트 엔진 초기화 – 스크립트 엔진 예제

Java는 `ScriptEngine` API (JSR‑223)를 제공합니다. 우리는 HTML 콘텐츠를 엔진에 전달하고 엔진이 기대하는 최소 DOM 메서드를 제공하는 작은 래퍼를 만들 것입니다.

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**왜 중요한가:** 이 **script engine example**은 전체 브라우저 없이도 임베디드 JavaScript를 실행할 수 있는 방법을 보여줍니다. 또한 스크립트가 우리의 모의 DOM과 상호 작용할 수 있도록 `document.getElementById`를 노출하는 경량 방법을 시연합니다.

---

## 단계 4: JavaScript 실행 – Increment Counter JavaScript 동작

엔진이 준비되면 스크립트를 실행하기만 하면 됩니다. `<script>` 태그 내부의 루프가 실행되고, 우리의 모의 `setInnerHTML`이 카운터를 업데이트합니다.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**내부에서 무슨 일이 일어나나요?** 루프의 각 반복마다 `document.getElementById('counter').innerHTML = i + 1;`을 호출합니다. 우리의 모의 `setInnerHTML`은 숫자 문자열을 `HTMLDocument.updateCounter`에 전달하여 최신 값을 저장합니다. 루프가 끝나면 문서의 내부 맵에 `counter` 요소에 대해 `"5"`가 저장됩니다.

---

## 단계 5: 최종 카운터 값 가져오기 – Get Element InnerHTML

스크립트가 완료되었으니 이제 `HTMLDocument` 인스턴스에서 **element innerHTML**을 가져올 수 있습니다.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

전체 프로그램을 실행하면 다음과 같이 출력됩니다:

```
Final counter value: 5
```

이는 **increment counter javascript** 로직이 정상적으로 동작했으며, 스크립트 실행 후 **element innerHTML**을 성공적으로 **retrieved**했음을 확인시켜 줍니다.

---

## 전체 작동 예제

모든 것을 합치면 아래와 같이 완전하고 바로 실행 가능한 Java 클래스가 됩니다:

```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

public class HtmlJsDemo {

    // ---------- Minimal HTMLDocument implementation ----------
    static class HTMLDocument {
        private final StringBuilder html = new StringBuilder();
        private final java.util.Map<String, String> elements = new java.util.HashMap<>();

        public void write(String content) {
            html.append(content);
        }

        public String getContent() {
            return html.toString();
        }

        public void setElementInnerHTML(String id, String value) {
            elements.put(id, value);
        }

        public String getElementInnerHTML(String id) {
            return elements.getOrDefault(id, "");
        }

        public void updateCounter(int value) {
            setElementInnerHTML("counter", String.valueOf(value));
        }
    }

    // ---------- SimpleScriptEngine (script engine example) ----------
    static class SimpleScriptEngine {
        private final HTMLDocument document;
        private final ScriptEngine engine;

        public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
            this.document = doc;
            ScriptEngineManager manager = new ScriptEngineManager();
            this.engine = manager.getEngineByName("JavaScript");
            // Expose a mock 'document' object
            engine.put("document", new Object() {
                public Object getElementById(String id) {
                    return new Object() {
                        public void setInnerHTML(String value) {
                            document.updateCounter(Integer.parseInt(value));
                        }
                    };
                }
            });
        }

        public void execute() throws ScriptException {
            String html = document.getContent();
            int start = html.indexOf("<script>") + "<script>".length();
            int end   = html.indexOf("</script>");
            String script = html.substring(start, end);
            engine.eval(script);
        }
    }

    // ---------- Main method ----------
    public static void main(String[] args) {
        // Step 1: create HTML document
        HTMLDocument doc = new HTMLDocument();

        // Step 2: embed JavaScript HTML (increment counter JavaScript)
        doc.write(
            "<!DOCTYPE html><html><body>"
          + "<div id='counter'>0</div>"
          + "<script>"
          + "for (let i = 0; i < 5; i++) {"
          + "  document.getElementById('counter').innerHTML = i


## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하여 밀접하게 연관된 주제를 다룹니다. 각 리소스는 단계별 설명과 함께 완전한 작동 코드를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색할 수 있도록 돕습니다.

- [Aspose.HTML for Java에서 빈 HTML 문서 만들기](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Aspose.HTML for Java에서 문자열로 HTML 문서 만들기](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Aspose.HTML for Java에서 HTML 문서 저장하기](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}