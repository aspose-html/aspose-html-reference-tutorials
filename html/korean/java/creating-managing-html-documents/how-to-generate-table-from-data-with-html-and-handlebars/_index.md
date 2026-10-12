---
category: general
date: 2026-10-12
description: Handlebars를 사용하여 데이터를 기반으로 테이블을 생성하고 JSON으로 테이블을 채우는 방법을 배웁니다. 동적 HTML
  테이블에서 행을 반복하는 단계별 가이드.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: ko
lastmod: 2026-10-12
og_description: 데이터에서 테이블을 생성하고 Handlebars를 사용해 JSON으로 테이블을 채우세요. 반복되는 테이블 행을 활용해
  동적 HTML 테이블을 만드는 이 튜토리얼을 따라보세요.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Handlebars로 데이터에서 테이블 생성 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-12'
  description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  headline: How to generate table from data with HTML and Handlebars
  type: TechArticle
- description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  name: How to generate table from data with HTML and Handlebars
  steps:
  - name: 1. Empty data sets
    text: 'If the JSON array is empty, Handlebars will still render the header row
      but no data rows. To display a friendly message, wrap the table in a conditional
      block:'
  - name: 2. Nested loops (e.g., multiple addresses per person)
    text: 'When a person can have several addresses, you can nest another `{{#foreach}}`
      inside the row:'
  - name: 3. Using a real API
    text: 'Replace the static `<script id="people-data">` with a fetch call:'
  - name: 4. Accessibility considerations
    text: '* Add `scope="col"` to `<th>` elements. * Use `<caption>` to describe the
      table purpose. * Ensure sufficient color contrast if you apply custom CSS.'
  type: HowTo
tags:
- HTML
- Handlebars
- JSON
- templating
title: HTML과 Handlebars를 사용하여 데이터로부터 테이블 생성하는 방법
url: /ko/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML과 Handlebars로 데이터에서 테이블 생성하기

웹 페이지에서 **데이터에서 테이블을 생성**해야 할 경우, 이 튜토리얼이 정확히 어떻게 하는지 보여줍니다. 간단한 Handlebars 루프를 사용하면 **JSON에서 테이블을 채우고**, **테이블 행을 반복**하며, 소스가 변경될 때마다 자동으로 업데이트되는 **동적 HTML 테이블**을 만들 수 있습니다.

몇 분 안에 완전한 실행 예제를 확인하고, 각 부분이 왜 중요한지 이해하며, 조건부 열이나 중첩 객체와 같은 더 복잡한 시나리오에 패턴을 적용하는 방법을 배울 수 있습니다.

## 만들게 될 것

다음과 같은 HTML 테이블을 만들 것입니다.

* 사람 목록을 포함하는 JSON 페이로드를 읽습니다.
* 각 사람마다 테이블 행을 **반복**합니다 (`repeat table rows`).
* 각 사람의 이름, 성, 주소를 적절한 셀에 삽입합니다.
* 서버‑사이드 렌더링 없이 브라우저에서 전체 과정이 이루어집니다.

**전제 조건**

* HTML 및 JavaScript 기본 지식.
* 최신 브라우저(Chrome, Edge, Firefox, Safari 중 하나).
* Handlebars.js – CDN에서 로드하므로 빌드 도구가 필요 없습니다.

---

## Step 1: JSON 데이터 소스 준비하기

첫 번째 단계는 API에서 받을 JSON을 흉내 내는 JavaScript 객체를 정의하는 것입니다. Handlebars는 일반 객체와 함께 작동하므로, 데모 목적이라면 데이터를 `<script>` 태그에 직접 삽입할 수 있습니다.

```html
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>
```

**왜 중요한가** – 데이터를 별도 `<script>` 요소에 두면 나중에 실제 AJAX 호출로 쉽게 교체할 수 있습니다. 구조(`Persons.Person`)는 Handlebars `{{#foreach Persons.Person}}` 블록에서 사용되는 경로와 일치하므로 **JSON에서 테이블을 채우는** 데 필수적입니다.

---

## Step 2: 행을 반복하는 Handlebars 템플릿 작성하기

다음으로, 테이블 마크업을 포함하는 `<script type="text/x-handlebars-template">` 블록을 만듭니다. Handlebars는 자리표시자를 실제 값으로 교체하고 각 사람마다 `<tr>`을 반복합니다.

```html
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Header row describing the columns -->
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <!-- Data row – this block is repeated for each Person -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**핵심 부분 설명**

* `{{#foreach Persons.Person}}` 은 `Persons.Person` 배열의 각 항목에 대해 **테이블 행을 반복**하도록 Handlebars에 지시합니다.
* `{{FirstName}} {{LastName}}` 와 `{{Address.*}}` 표현식은 현재 배열 요소에서 값을 가져옵니다.
* 전체 테이블을 `data_merge` 속성으로 감싸는 것은 선택 사항이며, 다운스트림 처리나 CSS 선택자에 유용할 수 있습니다.

---

## Step 3: Handlebars 로드 및 템플릿 컴파일하기

CDN에서 Handlebars를 가져오고, JSON을 파싱한 뒤 템플릿을 컴파일하고, 최종 HTML을 페이지에 삽입합니다.

```html
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  // Parse the JSON stored in the <script id="people-data">
  const rawData = document.getElementById('people-data').textContent;
  const context = JSON.parse(rawData);

  // Grab the template markup and compile it
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);

  // Generate the final HTML by applying the context
  const html = template(context);

  // Insert the generated table into the DOM
  document.getElementById('output').innerHTML = html;
</script>
```

**런타임에 컴파일하는 이유** – 템플릿을 한 번만 컴파일하고 재사용하면 데이터가 자주 바뀔 때 페이지가 빠르게 동작합니다. 이 패턴은 페이지를 새로 고치지 않고도 **JSON에서 테이블을 채우는** 작업을 여러 번 수행할 수 있게 해줍니다.

---

## Step 4: 생성된 테이블을 위한 컨테이너 예약하기

동적 테이블이 표시될 자리인 `<div>` 를 추가합니다. 이렇게 하면 정적 레이아웃과 생성된 콘텐츠를 명확히 구분할 수 있어 마크업이 깔끔해집니다.

```html
<div id="output"></div>
```

Step 3의 스크립트가 실행되면 `<div id="output">` 안에 완전한 `<table>` 요소가 들어가며, 스타일링이나 추가 조작을 바로 할 수 있습니다.

---

## Step 5: 출력 확인 및 테이블 스타일링 (선택)

브라우저에서 페이지를 열면 아래와 같은 테이블이 표시됩니다.

![데이터에서 생성된 테이블 스크린샷](image.png "데이터에서 생성된 테이블 스크린샷")

```html
<table border="1" data_merge="true">
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <tr>
    <td>Alice Anderson</td>
    <td>Maple 123, Springfield</td>
  </tr>
  <tr>
    <td>Bob Baker</td>
    <td>Oak 456, Rivertown</td>
  </tr>
</table>
```

**선택적 스타일링** – 더 깔끔한 모습을 원한다면 몇 가지 CSS 규칙을 추가하세요:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## 엣지 케이스 및 일반적인 변형 처리

### 1. 빈 데이터 세트

JSON 배열이 비어 있으면 Handlebars는 헤더 행만 렌더링하고 데이터 행은 출력하지 않습니다. 친절한 메시지를 표시하려면 테이블을 조건부 블록으로 감싸세요:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. 중첩 루프 (예: 사람당 여러 주소)

한 사람이 여러 주소를 가질 수 있는 경우, 행 안에 또 다른 `{{#foreach}}` 를 중첩할 수 있습니다:

```handlebars
{{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>
      {{#foreach Address}}
        {{Street}} {{Number}}, {{City}}<br>
      {{/foreach}}
    </td>
  </tr>
{{/foreach}}
```

### 3. 실제 API 사용하기

정적 `<script id="people-data">` 를 fetch 호출로 교체합니다:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

이렇게 하면 **동적 테이블 행** 기술을 그대로 유지하면서 실시간 데이터를 가져올 수 있습니다.

### 4. 접근성 고려 사항

* `<th>` 요소에 `scope="col"` 추가.
* `<caption>` 으로 테이블 목적 설명.
* 사용자 정의 CSS를 적용할 경우 충분한 색 대비 확보.

---

## 전체 실행 예제

다음 블록을 `index.html` 파일에 복사하고 브라우저에서 열어보세요. 페이지는 **데이터에서 테이블을 생성**, **JSON에서 테이블을 채우고**, 행을 자동으로 반복합니다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dynamic table from JSON</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; border: 1px solid #ddd; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<!-- Step 1: JSON data source -->
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>

<!-- Step 2: Handlebars template -->
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th scope="col">Person</th>
    <th scope="col">Address</th>
  </tr>
  {{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
  {{/foreach}}
</table>
</script>

<!-- Step 4: Container for the generated table -->
<div id="output"></div>

<!-- Step 3: Load Handlebars, compile, and render -->
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  const raw = document.getElementById('people-data').textContent;
  const context = JSON.parse(raw);
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);
  document.getElementById('output').innerHTML = template(context);
</script>

</body>
</html>
```

**예상 결과**

헤더 외에 두 개의 데이터 행(“Alice Anderson”와 “Bob Baker”)이 표시됩니다. 페이지는 오프라인에서도 동작하므로 **데이터에서 테이블을 생성**하는 데 서버 구성 요소가 필요 없음을 증명합니다.

---

## 결론

이제 Handlebars 템플릿을 사용해 **데이터에서 테이블을 생성**, **JSON에서 테이블을 채우기**, 그리고 **행을 반복**해 **동적 HTML 테이블**을 만드는 방법을 알게 되었습니다. 이 패턴은 더 큰 데이터 세트, 중첩 구조, 실시간 API 호출까지 확장 가능하므로 클라이언트‑사이드 보고서나 관리 UI에 견고한 기반을 제공합니다.

**다음 단계**

* 날짜나 숫자 포맷팅을 위한 Handlebars 헬퍼 탐색.
* CSS Grid 또는 Flexbox와 결합해 반응형 테이블 레이아웃 구현.
* 매우 큰 데이터 세트를 다루기 위한 페이지네이션 또는 정렬 라이브러리 통합.

다양한 JSON 형태를 실험하고, 조건부 열을 추가하거나 Handlebars를 다른 템플릿 엔진으로 교체해 보세요—새로운 스킬을 통해 유연하고 데이터‑구동 인터페이스를 빠르고 안정적으로 구축할 수 있습니다.

## 다음에 배워야 할 내용

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하며, 단계별 설명과 완전한 코드 예제를 포함하고 있어 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}