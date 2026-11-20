---
date: 2026-04-23
description: Dowiedz się, jak uzyskać zewnętrzny kod HTML i poczekać na załadowanie
  dokumentu przy użyciu Aspose.HTML dla Javy w tym przewodniku krok po kroku.
keywords:
- get outer html
- wait for document load
- java html processing
- navigate html document
- aspose html example
linktitle: Obsługa zdarzeń ładowania dokumentu w Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Pobierz zewnętrzny HTML i obsłuż zdarzenia ładowania w Aspose.HTML dla Javy
url: /pl/java/creating-managing-html-documents/handle-document-load-events/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pobierz zewnętrzny HTML i obsłuż zdarzenia ładowania w Aspose.HTML dla Javy

## Wprowadzenie
Kiedy potrzebujesz **get outer html** z zdalnej strony i chcesz zareagować natychmiast po zakończeniu ładowania dokumentu, obsługa zdarzeń ładowania dokumentu staje się niezbędna. W Javie Aspose.HTML zapewnia czyste API zarówno do nawigacji do URL, jak i nasłuchiwania zdarzenia `OnLoad`, umożliwiając bezpieczny dostęp do HTML, gdy jest gotowy. Ten samouczek przeprowadzi Cię przez cały proces — od konfiguracji środowiska po wypisanie zewnętrznego HTML załadowanej strony — abyś mógł zintegrować go z dowolną aplikacją Java skoncentrowaną na sieci.

## Szybkie odpowiedzi
- **Co oznacza „get outer html”?** Zwraca pełny znacznik HTML elementu głównego dokumentu.  
- **Która biblioteka obsługuje zdarzenia ładowania?** Aspose.HTML for Java udostępnia zdarzenie `OnLoad`.  
- **Czy potrzebna jest licencja do testów?** Dostępna jest bezpłatna wersja próbna; licencja komercyjna jest wymagana w produkcji.  
- **Jak mogę poczekać, aż dokument się załaduje?** Użyj obsługi `OnLoad` lub prostego opóźnienia (sleep) w celach demonstracyjnych.  
- **Czy to podejście jest bezpieczne w kontekście asynchroniczności?** Tak, zdarzenie wyzwalane jest po zakończeniu ładowania dokumentu, zapewniając gotowość HTML.

## Co to jest „get outer html”?
`document.getDocumentElement().getOuterHTML()` zwraca pełny ciąg HTML elementu głównego dokumentu, włącznie z otwierającymi i zamykającymi tagami. Jest to przydatne, gdy potrzebny jest surowy znacznik do dalszego przetwarzania, przechowywania lub konwersji.

## Dlaczego warto używać Aspose.HTML dla Javy?
- **Solidne parsowanie HTML** bez potrzeby używania silnika przeglądarki.  
- **Model zdarzeniowy** pozwala reagować dokładnie wtedy, gdy dokument jest gotowy.  
- **Wieloplatformowe** wsparcie dla Windows, Linux i macOS.  
- **Bogate API** do nawigacji, manipulacji i konwersji do PDF, obrazu itp.

## Wymagania wstępne
Zanim przejdziemy do kodu, upewnij się, że masz następujące:

1. **Java Development Kit (JDK)** – Zainstaluj ze [strony Oracle](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html).  
2. **Aspose.HTML for Java** – Pobierz najnowszy plik JAR ze [strony wydań Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse lub dowolny edytor, którego preferujesz.  
4. **Podstawowa znajomość Javy** – Zrozumienie klas, metod i obsługi zdarzeń.  
5. **Połączenie internetowe** – Przykład ładuje stronę HTML z sieci.

Gdy wszystko będzie gotowe, możesz rozpocząć kodowanie!

## Przewodnik krok po kroku

### Krok 1: Zainicjuj dokument HTML
Najpierw utwórz instancję `HTMLDocument`. Ustawiamy również `AtomicBoolean`, aby śledzić stan ładowania.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument();
java.util.concurrent.atomic.AtomicBoolean isLoading = new java.util.concurrent.atomic.AtomicBoolean(false);
```

### Krok 2: Subskrybuj zdarzenie **OnLoad**
Dołącz obsługę, która zmieni flagę `isLoading` po zakończeniu ładowania dokumentu. To miejsce, w którym będziemy wiedzieć, że można bezpiecznie wywołać **get outer html**.

```java
document.OnLoad.add(new DOMEventHandler() {
    @Override
    public void invoke(Object o, Event event) {
        isLoading.set(true);
    }
});
```

### Krok 3: Nawiguj do dokumentu (załaduj HTML z URL)
Powiedz `HTMLDocument`, którą stronę pobrać. W tym przykładzie ładujemy publiczną stronę dokumentacji Aspose.

```java
document.navigate("https://docs.aspose.com/html/net/creating-a-document/document.html");
```

### Krok 4: Poczekaj na załadowanie dokumentu
Ładowanie zdalnej strony jest asynchroniczne. Dla demonstracji wstrzymujemy wątek na kilka sekund; w produkcji należy polegać na fladze `OnLoad` lub bardziej zaawansowanej technice synchronizacji.

```java
Thread.sleep(5000);
```

### Krok 5: Uzyskaj dostęp do załadowanego dokumentu i **Get Outer HTML**
Teraz, gdy `isLoading` jest prawdziwe, pobierz pełny znacznik elementu głównego dokumentu.

```java
System.out.println("outerHTML = " + document.getDocumentElement().getOuterHTML());
```

Powinieneś zobaczyć kompletny HTML załadowanej strony wydrukowany w konsoli.

## Częste problemy i rozwiązania
| Problem | Powód | Rozwiązanie |
|-------|--------|-----|
| **`isLoading` nigdy nie staje się true** | Obsługa `OnLoad` nie została podłączona przed `navigate()` | Dołącz obsługę **przed** wywołaniem `navigate()`. |
| **`NullPointerException` przy `getDocumentElement()`** | Dokument nie został w pełni załadowany w momencie dostępu | Użyj odpowiedniego mechanizmu oczekiwania (np. pętla na `isLoading.get()` lub `CountDownLatch`). |
| **SSLHandshakeException** przy ładowaniu adresów HTTPS | Brak zaufanych certyfikatów | Dodaj odpowiedni certyfikat do keystore Javy lub użyj `-Djsse.enableSNIExtension=false`. |
| **Wolne ładowanie powodujące timeout** | Duża strona lub opóźnienia sieciowe | Zwiększ czas opóźnienia lub zaimplementuj nasłuchiwacz z obsługą timeoutu. |

## Najczęściej zadawane pytania

**P: Czym jest Aspose.HTML dla Javy?**  
O: Aspose.HTML dla Javy to biblioteka umożliwiająca programistom tworzenie, manipulację i konwersję dokumentów HTML w aplikacjach Java.

**P: Jak pobrać Aspose.HTML dla Javy?**  
O: Możesz go pobrać ze [strony wydań Aspose](https://releases.aspose.com/html/java/).

**P: Czy mogę używać Aspose.HTML za darmo?**  
O: Tak, możesz wypróbować Aspose.HTML za darmo, pobierając wersję próbną ze [strony Aspose](https://releases.aspose.com/).

**P: Czy dostępne jest wsparcie dla Aspose.HTML?**  
O: Tak, możesz znaleźć wsparcie i zadawać pytania na [forum Aspose](https://forum.aspose.com/c/html/29).

**P: Jak uzyskać tymczasową licencję dla Aspose.HTML?**  
O: Możesz poprosić o tymczasową licencję, odwiedzając [stronę tymczasowej licencji Aspose](https://purchase.aspose.com/temporary-license/).

---

**Ostatnia aktualizacja:** 2026-04-23  
**Testowano z:** Aspose.HTML for Java 24.11  
**Autor:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}