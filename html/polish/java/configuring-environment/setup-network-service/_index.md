---
date: 2025-12-05
description: Dowiedz się, jak tworzyć pliki HTML, zarządzać zasobami sieciowymi i
  konwertować HTML na PNG przy użyciu Aspose.HTML dla Javy z niestandardową obsługą
  błędów.
language: pl
linktitle: Set Up Network Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Utwórz plik HTML i skonfiguruj usługę sieciową (Aspose.HTML Java)
url: /java/configuring-environment/setup-network-service/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz plik HTML i skonfiguruj usługę sieciową (Aspose.HTML Java)

## Introduction
Jeśli potrzebujesz **utworzyć plik html**, który pobiera obrazy z sieci, a następnie przekształcić tę stronę w obraz, jesteś we właściwym miejscu. W tym samouczku przejdziemy przez każdy krok wymagany do skonfigurowania Aspose.HTML dla Javy, **zarządzania zasobami sieciowymi**, obsługi brakujących zasobów przy użyciu własnego obsługiwacza błędów, **konwersji html do png**, oraz w końcu **czyszczenia zasobów**, aby Twoja aplikacja pozostawała zdrowa. Niezależnie od tego, czy budujesz silnik raportowania, automatyczny generator miniatur, czy po prostu eksperymentujesz z konwersją HTML‑do‑obrazu, przedstawiony tutaj wzorzec zaoszczędzi Ci czas i nerwy.

## Quick Answers
- **Jaki jest pierwszy krok?** Utwórz plik HTML, który odwołuje się do obrazów hostowanych w sieci.  
- **Która klasa konfiguruje sieć?** `com.aspose.html.Configuration`.  
- **Jak przechwycić błędy ładowania?** Dodaj własny `MessageHandler` do `INetworkService`.  
- **Jaki format wyjściowy generuje ten przykład?** Obraz PNG (`output.png`).  
- **Czy muszę zwolnić obiekty?** Tak – wywołaj `dispose()` zarówno na dokumencie, jak i konfiguracji.

## Prerequisites
- **Java Development Kit (JDK)** 1.8 lub nowszy.  
- **Biblioteka Aspose.HTML for Java** – pobierz najnowszą wersję ze [strony oficjalnych wydań](https://releases.aspose.com/html/java/).  
- **IDE** według własnego wyboru (IntelliJ IDEA, Eclipse, NetBeans, itp.).  
- Podstawowa znajomość składni Javy oraz konfiguracji projektu Maven/Gradle.

## Import Packages
Na początek musisz zaimportować wymagane pakiety do swojego projektu Java. Pakiety te umożliwią korzystanie z różnych funkcjonalności Aspose.HTML for Java.

```java
import java.io.IOException;
```

Te importy są podstawą omawianej funkcjonalności, więc upewnij się, że znajdują się na początku swojego pliku Java.

## Step 1: Create an HTML File with Network‑Dependent Images
### Krok 1: Utwórz plik HTML z obrazami zależnymi od sieci
Aby **utworzyć plik html**, który odwołuje się do zewnętrznych zasobów, napisz mały fragment kodu, który wstawia kilka znaczników `<img>` wskazujących na publicznie dostępne obrazy.

```java
String code = "<img src=\"https://docs.aspose.com/svg/net/drawing-basics/filters-and-gradients/park.jpg\" >\r\n" +
        "<img src=\"https://docs.aspose.com/html/net/missing1.jpg\" >\r\n" +
        "<img src=\"https://docs.aspose.com/html/net/missing2.jpg\" >\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

Ten plik HTML jest punktem wejścia dla usługi sieciowej; obrazy będą pobierane przez HTTP podczas ładowania dokumentu.

## Step 2: Initialize the Configuration Object
### Krok 2: Zainicjalizuj obiekt Configuration
Teraz utwórzmy **konfigurację**, która będzie zawierała ustawienia naszej usługi sieciowej.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

Obiekt `Configuration` to miejsce, w którym określisz, jak Aspose.HTML ma obsługiwać ruch sieciowy, logowanie i obsługę błędów.

## Step 3: Add a Custom Error Message Handler
### Krok 3: Dodaj własny obsługiwacz komunikatów o błędach
Własny `MessageHandler` zapewnia wgląd w problemy, takie jak brakujące obrazy lub przekroczenia czasu.

```java
com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
com.aspose.html.net.MessageHandler logHandler = new LogMessageHandler();
network.getMessageHandlers().addItem(logHandler);
```

Poprzez podłączenie `LogMessageHandler` każdy ostrzeżenie lub błąd związany z siecią jest przechwytywany, co ułatwia debugowanie.

## Step 4: Load the HTML Document with the Configuration
### Krok 4: Załaduj dokument HTML z konfiguracją
Gdy usługa sieciowa jest gotowa, załaduj wcześniej utworzony plik HTML.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

Podczas ładowania dokumentu Aspose.HTML użyje własnej konfiguracji sieciowej i wywoła nasz obsługiwacz komunikatów w przypadku jakichkolwiek problemów.

## Step 5: Convert HTML to PNG
### Krok 5: Konwertuj HTML do PNG
Teraz **przekonwertujemy html na png**, zamieniając załadowaną stronę (wraz z pomyślnie pobranymi obrazami) na obraz rastrowy.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

Wynikiem jest pojedynczy plik PNG (`output.png`), który możesz osadzić w innym miejscu lub udostępnić użytkownikom.

## Step 6: Clean Up Resources
### Krok 6: Posprzątaj zasoby
Właściwe zarządzanie zasobami jest kluczowe. Po konwersji zwolnij obiekty, aby **posprzątać zasoby** i uniknąć wycieków pamięci.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

Pomyśl o tym jak o myciu naczyń po posiłku — pozostawienie zasobów może później powodować problemy z wydajnością.

## Common Issues and Solutions
| Problem | Dlaczego się dzieje | Jak naprawić |
|---------|---------------------|--------------|
| Obrazy nie ładują się | Przekroczenie limitu czasu sieci lub nieprawidłowy URL | Sprawdź URL‑e, zwiększ limit czasu w ustawieniach `NetworkService` lub dodaj logikę awaryjną w `LogMessageHandler`. |
| PNG jest pusty | Dokument nie został w pełni załadowany przed konwersją | Upewnij się, że `HTMLDocument` jest tworzony z konfiguracją zawierającą własny obsługiwacz; opcjonalnie wywołaj `document.waitForLoad()`, jeśli używasz asynchronicznego ładowania. |
| Błąd braku pamięci | Bardzo duży HTML lub wiele obrazów wysokiej rozdzielczości | Użyj `ImageSaveOptions.setMaxWidth/MaxHeight`, aby ograniczyć rozmiar wyjścia, lub niezwłocznie zwalniaj obiekty pośrednie. |

## Frequently Asked Questions

**P: Jaki jest główny cel konfiguracji usługi sieciowej w Aspose.HTML dla Javy?**  
**O:** Pozwala **zarządzać zasobami sieciowymi**, takimi jak zdalne obrazy, skrypty czy arkusze stylów, oraz daje kontrolę nad obsługą błędów i logowaniem.

**P: Czy mogę użyć tej konfiguracji do generowania innych formatów obrazów (np. JPEG, BMP)?**  
**O:** Tak — wystarczy zmienić właściwość formatu w `ImageSaveOptions` na żądany typ wyjściowy.

**P: Czym różni się własny `MessageHandler` od domyślnego loggera?**  
**O:** Własny obsługiwacz pozwala kierować komunikaty do własnego frameworka logowania, filtrować określone ostrzeżenia lub wyzwalać alerty, podczas gdy domyślny logger zapisuje je jedynie w konsoli.

**P: Czy konieczne jest wywołanie `dispose()` zarówno na dokumencie, jak i konfiguracji?**  
**O:** Zdecydowanie tak. Zwolnienie zwalnia zasoby natywne i **czyści zasoby**, które biblioteka przechowuje wewnętrznie.

**P: Gdzie mogę znaleźć więcej przykładów konwersji HTML do obrazów w Javie?**  
**O:** Sprawdź dokumentację Aspose.HTML for Java oraz oficjalną stronę z przykładami na GitHubie, gdzie znajdziesz dodatkowe scenariusze, takie jak konwersja do PDF, renderowanie SVG i przetwarzanie wsadowe.

---

**Ostatnia aktualizacja:** 2025-12-05  
**Testowano z:** Aspose.HTML for Java 24.12 (latest)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}