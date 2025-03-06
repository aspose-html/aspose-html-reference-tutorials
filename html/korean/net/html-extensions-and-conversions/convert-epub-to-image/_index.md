---
title: Aspose.HTML을 사용하여 .NET에서 EPUB를 이미지로 변환
linktitle: .NET에서 EPUB를 이미지로 변환
second_title: Aspose.HTML .NET HTML 조작 API
description: Aspose.HTML for .NET을 사용하여 EPUB를 이미지로 변환하는 방법을 알아보세요. 코드 예제와 사용자 정의 가능한 옵션이 있는 단계별 튜토리얼.
weight: 11
url: /ko/net/html-extensions-and-conversions/convert-epub-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML을 사용하여 .NET에서 EPUB를 이미지로 변환


오늘날의 디지털 시대에 다양한 문서 형식을 조작하고 변환하는 능력은 귀중한 기술입니다. Aspose.HTML for .NET은 개발자가 HTML 및 EPUB 문서를 손쉽게 작업할 수 있는 강력한 도구입니다. 이 튜토리얼에서는 Aspose.HTML for .NET의 세계를 탐구하고 EPUB 문서를 다양한 이미지 형식으로 변환하는 과정을 안내합니다. 각 예를 여러 단계로 나누어 각 단계를 설명합니다.

## 필수 조건

.NET용 Aspose.HTML의 세계로 들어가기 전에 다음과 같은 필수 구성 요소가 있는지 확인해야 합니다.

1. Visual Studio: 시스템에 Visual Studio가 설치되어 있는지 확인하세요. 웹사이트에서 다운로드할 수 있습니다.

2.  .NET용 Aspose.HTML: Aspose 웹사이트에서 라이브러리를 얻을 수 있습니다.[여기](https://releases.aspose.com/html/net/).

3. 데이터 디렉토리: EPUB 파일을 저장하고 출력 이미지를 저장할 디렉토리를 준비하세요.

4. C#에 대한 기본 지식: 이 튜토리얼에서 제공하는 코드 예제를 이해하고 구현하려면 C# 프로그래밍에 대한 지식이 필수적입니다.

## 필요한 네임스페이스 가져오기

Aspose.HTML for .NET 작업을 시작하기 전에 필요한 네임스페이스를 C# 코드로 가져와야 합니다. 이러한 네임스페이스는 Aspose.HTML for .NET 기능에 대한 액세스를 제공합니다.

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

이제 필수 구성 요소와 네임스페이스가 준비되었으므로 단계별 예제로 넘어가겠습니다.

## EPUB를 JPEG로 변환

```csharp
    string dataDir = "Your Data Directory";
    // 기존 EPUB 파일을 열어서 읽습니다.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // ConvertEPUB 메서드를 호출하여 EPUB 파일을 이미지로 변환합니다.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### 단계

1. dataDir 변수에 EPUB 파일의 경로를 제공합니다.
2. FileStream을 사용하여 EPUB 파일을 읽기 위해 엽니다.
3. EPUB 스트림, 출력 형식(JPEG)을 지정하는 ImageSaveOptions, 출력 파일 이름("output.jpg")을 전달하여 ConvertEPUB 메서드를 호출합니다.
5. EPUB 파일은 JPEG 이미지로 변환됩니다.

이 예에서 우리는 EPUB 파일을 열고, 그 내용을 읽고, JPEG 이미지 형식으로 변환합니다. 출력 이미지는 "output.jpg"로 저장됩니다.

## EPUB를 PNG로 변환

유사한 코드 구조를 사용하여 EPUB 파일을 PNG, BMP, GIF, TIFF와 같은 다양한 이미지 형식으로 쉽게 변환할 수 있습니다. PNG로 변환하는 예는 다음과 같습니다.

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### 단계
1. FileStream을 사용하여 EPUB 파일을 읽기 위해 엽니다.
2. 원하는 출력 형식(이 경우 PNG)으로 ImageSaveOptions 객체를 초기화합니다.
3. EPUB 스트림, 이미지 저장 옵션 및 출력 파일 이름을 전달하여 ConvertEPUB 메서드를 호출합니다.
4. EPUB 파일이 지정된 이미지 형식으로 변환됩니다.

## 이미지 저장 옵션 지정

페이지 크기 및 배경색과 같은 옵션을 지정하여 이미지 출력을 사용자 정의할 수 있습니다. 다음은 예입니다.

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### 단계

1.  EPUB 파일에 대한 경로를 제공하세요.`dataDir` 변하기 쉬운.
2.  EPUB 파일을 읽기 위해 열기`FileStream`.
3.  생성하다`ImageSaveOptions` 객체를 선택하고 원하는 출력 형식(JPEG)을 지정합니다.
4. 필요한 경우 페이지 크기와 배경색을 사용자 지정합니다.
5.  전화하다`ConvertEPUB`EPUB 스트림, 이미지 저장 옵션 및 출력 파일 이름을 전달하는 방법입니다.
6. 지정된 옵션을 사용하여 EPUB 파일이 이미지로 변환됩니다.

## 사용자 정의 스트림 공급자 지정

출력 스트림을 조작해야 하는 경우 사용자 지정 스트림 공급자를 사용할 수 있습니다. 다음은 예입니다.

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
MemoryStreamProvider 클래스 소스 코드.

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // 문서 렌더링 중에 생성된 MemoryStream 개체 목록
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // 이 메서드는 예를 들어 XPS, PDF 또는 TIFF 형식의 경우와 같이 단 하나의 출력 스트림만 필요할 때 호출됩니다.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // 이 메서드는 여러 출력 스트림을 만들어야 할 때 호출됩니다. 예를 들어 HTML을 렌더링하는 동안 이미지 파일(JPG, PNG 등)을 나열합니다.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // 여기서 데이터로 채워진 스트림을 해제하고 예를 들어 하드 드라이브에 플러시할 수 있습니다.
            }
            public void Dispose()
            {
                // 리소스 해제
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```

### 단계
1.  EPUB 파일에 대한 경로를 제공하세요.`dataDir` 변하기 쉬운.
2.  EPUB 파일을 읽기 위해 열기`FileStream`.
3.  생성하다`MemoryStreamProvider` 사용자 정의 출력 스트림을 처리합니다.
4.  전화하다`ConvertEPUB` EPUB 스트림, 이미지 저장 옵션(JPEG), 사용자 지정 스트림 공급자를 전달하는 방법입니다.
5. 사용자 지정 공급자의 메모리 스트림을 반복하여 개별 파일에 저장합니다.
6. 이 예제에서는 필요에 따라 여러 개의 출력 스트림을 조작하고 저장할 수 있습니다.

## 결론

Aspose.HTML for .NET은 EPUB 및 HTML 문서 작업을 간소화하는 다재다능한 라이브러리입니다. EPUB 문서를 다양한 이미지 포맷과 사용자 정의 가능한 옵션으로 변환할 수 있는 기능을 통해 개발자에게 광범위한 애플리케이션을 제공합니다.

---

## 자주 묻는 질문

### 1. .NET용 Aspose.HTML을 어디서 다운로드할 수 있나요?

 .NET용 Aspose.HTML은 릴리스 페이지에서 다운로드할 수 있습니다.[여기](https://releases.aspose.com/html/net/).

### 2. Aspose.HTML for .NET에 대한 임시 라이선스를 어떻게 받을 수 있나요?

 임시 면허를 받으려면 임시 면허 페이지를 방문하세요.[여기](https://purchase.aspose.com/temporary-license/).

### 3. .NET용 Aspose.HTML에 대한 추가 지원은 어디에서 찾을 수 있나요?

 질문이나 문제가 있는 경우 지원 포럼에서 Aspose 커뮤니티에 도움을 요청할 수 있습니다.[여기](https://forum.aspose.com/).

### 4. EPUB 문서를 PDF나 XPS와 같은 다른 포맷으로 변환할 수 있나요?

네, Aspose.HTML for .NET을 사용하면 EPUB 문서를 PDF, XPS 등 다양한 포맷으로 변환할 수 있습니다.

### 5. Aspose.HTML for .NET은 소규모 및 대규모 프로젝트에 모두 적합합니까?

물론입니다! Aspose.HTML for .NET은 확장 가능하도록 설계되어 모든 규모의 프로젝트에 적합한 선택입니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
