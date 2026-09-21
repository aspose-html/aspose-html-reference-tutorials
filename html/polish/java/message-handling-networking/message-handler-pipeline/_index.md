---
date: 2026-02-23
description: Dowiedz się, jak konwertować pliki zip na PDF przy użyciu Aspose.HTML
  dla Javy. Ten przewodnik krok po kroku pokazuje, jak skonfigurować usługę sieciową,
  dodać własny handler i rejestrować czas trwania żądania.
linktitle: Creating Message Handler Pipelines in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Jak przekonwertować ZIP na PDF przy użyciu Aspose.HTML dla Javy
url: /pl/java/message-handling-networking/message-handler-pipeline/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przekonwertować ZIP na PDF przy użyciu Aspose.HTML for Java

## Wprowadzenie
W tym obszernej tutorialu dowiesz się **jak konwertować archiwa zip** na dokumenty PDF przy użyciu Aspose.HTML for Java. Przejdziemy przez budowanie potoku obsługi komunikatów, konfigurowanie usługi sieciowej, dodawanie własnego handlera oraz logowanie czasu trwania żądania — wszystko przy zachowaniu przejrzystego i uruchamialnego kodu. Niezależnie od tego, czy automatyzujesz generowanie raportów, czy potrzebujesz niezawodnego sposobu na spakowanie treści HTML jako PDF, ten przewodnik ma wszystko, czego potrzebujesz.

## Szybkie odpowiedzi
- **Co robi potok?** Przetwarza plik ZIP, wyodrębnia HTML i renderuje go do PDF.  
- **Który handler loguje czas trwania?** `StartRequestDurationLoggingMessageHandler` i `StopRequestDurationLoggingMessageHandler`.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w testach; licencja komercyjna jest wymagana w produkcji.  
- **Czy mogę zmienić ścieżkę wyjściową?** Tak — zmodyfikuj zmienną `savePath` w Kroku 1.  
- **Jakiej wersji Javy wymaga?** JDK 8 lub wyższej.

## Co to jest potok obsługi komunikatów?
Potok obsługi komunikatów to konfigurowalny łańcuch komponentów przetwarzających, które przechwytują żądania sieciowe wykonywane przez Aspose.HTML. Wstawiając własne handlery, możesz kontrolować sposób pobierania, przekształcania i logowania zasobów — idealne w scenariuszach takich jak konwersja archiwum ZIP do PDF.

## Dlaczego używać potoku do konwersji ZIP na PDF?
- **Precyzyjna kontrola** – Dodawaj, zmieniaj kolejność lub usuwaj handlery, aby dopasować je do swojego przepływu pracy.  
- **Wgląd w wydajność** – Loguj czas trwania żądania, aby zidentyfikować wąskie gardła.  
- **Rozszerzalność** – Podłącz własną logikę (np. uwierzytelnianie, buforowanie).  
- **Niezawodność** – Biblioteka automatycznie obsługuje przypadki brzegowe, takie jak nieprawidłowy HTML.

## Wymagania wstępne
- **Java Development Kit (JDK) 8+** – Upewnij się, że `java -version` zwraca wersję 8 lub nowszą.  
- **Biblioteka Aspose.HTML for Java** – Pobierz ze strony [Aspose downloads](https://releases.aspose.com/html/java/).  
- **IDE** – IntelliJ IDEA, Eclipse lub NetBeans ułatwią programowanie.  
- **Podstawowa znajomość Javy i HTML** – Przydatna, ale nieobowiązkowa.

## Importowanie pakietów
Na początek zaimportuj klasy, których będziemy potrzebować. Te importy dają dostęp do funkcji konfiguracyjnych, sieciowych i renderowania PDF.

```java
import com.aspose.html.Configuration;
import com.aspose.html.HTMLDocument;
import com.aspose.html.net.MessageHandlerCollection;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.services.INetworkService;
```

## Przewodnik krok po kroku

### Krok 1: Przygotuj ścieżki do plików
```java
// Prepare path to a source zip file
String documentPath = "input/test.zip";
// Prepare path for converted file saving
String savePath = "output/zip-to-pdf-duration.pdf";
```
Ustaw `documentPath` na plik ZIP zawierający Twoje pliki HTML oraz `savePath` na miejsce, w którym ma zostać zapisany końcowy PDF.

### Krok 2: Utwórz instancję Configuration
```java
// Create an instance of the Configuration class
Configuration configuration = new Configuration();
```
Obiekt `Configuration` jest podstawą do dostosowywania potoku przetwarzania.

### Krok 3: Zainicjalizuj usługę sieciową
```java
INetworkService service = configuration.getService(INetworkService.class);
MessageHandlerCollection handlers = service.getMessageHandlers();
```
Tutaj **konfigurujemy usługę sieciową** i uzyskujemy `MessageHandlerCollection`, które jest zestawem narzędzi do dodawania własnych handlerów.

### Krok 4: Dodaj handler wiadomości pliku ZIP
```java
// Custom Schema: ZIP. Add ZipFileSchemaMessageHandler to the end of the pipeline
handlers.addItem(new ZIPFileSchemaMessageHandler(documentPath));
```
Poprzez **dodanie własnego handlera** (`ZIPFileSchemaMessageHandler`) informujemy Aspose.HTML, jak traktować plik ZIP jako wirtualny system plików.

### Krok 5: Wstaw handler logujący początkowy czas trwania żądania
```java
// Duration Logging. Add the StartRequestDurationLoggingMessageHandler at the first place in the pipeline
handlers.insertItem(0, new StartRequestDurationLoggingMessageHandler());
```
Ten handler **loguje czas trwania żądania** na samym początku potoku, dostarczając znacznik czasu, kiedy rozpoczyna się przetwarzanie.

### Krok 6: Dodaj handler logujący końcowy czas trwania żądania
```java
// Add the StopRequestDurationLoggingMessageHandler to the end of the pipeline
handlers.addItem(new StopRequestDurationLoggingMessageHandler());
```
Umieszczenie go na końcu pozwala uchwycić całkowity czas potrzebny na konwersję ZIP do PDF.

### Krok 7: Zainicjalizuj dokument HTML
```java
// Initialize an HTML document with specified configuration
HTMLDocument document = new HTMLDocument("zip-file:///test.html", configuration);
```
Wskazujemy `HTMLDocument` na plik HTML startowy wewnątrz ZIP (`zip-file:///test.html`). Konfiguracja, którą zbudowaliśmy wcześniej, jest stosowana automatycznie.

### Krok 8: Utwórz urządzenie PDF
```java
// Create the PDF Device
PdfDevice device = new PdfDevice(savePath);
```
**Urządzenie PDF** (`PdfDevice`) jest tym, co **tworzy PDF z zawartości ZIP**. Otrzymuje wyrenderowane strony i zapisuje je do `savePath`.

### Krok 9: Renderuj ZIP do PDF
```java
// Render ZIP to PDF
document.renderTo(device);
```
Wywołanie `renderTo` uruchamia cały potok: ZIP jest rozpakowywany, HTML renderowany, czas jest logowany, a końcowy PDF zapisywany.

## Typowe problemy i rozwiązania
| Problem | Przyczyna | Rozwiązanie |
|---------|-----------|-------------|
| `FileNotFoundException` | Nieprawidłowy `documentPath` lub `savePath` | Sprawdź, czy ścieżki są absolutne lub względne względem katalogu roboczego. |
| Brak treści w PDF | Nieprawidłowa nazwa pliku HTML w konstruktorze `HTMLDocument` | Upewnij się, że nazwa pliku dokładnie odpowiada plikowi HTML wewnątrz ZIP (`test.html`). |
| Czas nie jest logowany | Handlery nie zostały wstawione w odpowiedniej kolejności | Wstaw `StartRequestDurationLoggingMessageHandler` na indeks 0 oraz `StopRequestDurationLoggingMessageHandler` po wszystkich pozostałych handlerach. |
| Nieobsługiwane funkcje HTML | Używanie CSS/JS nieobsługiwanego przez Aspose.HTML | Uprość znacznik lub wstępnie przetwórz HTML przed renderowaniem. |

## Najczęściej zadawane pytania

**P: Czym jest Aspose.HTML for Java?**  
O: Aspose.HTML for Java to biblioteka umożliwiająca manipulację dokumentami HTML oraz konwersję do formatów takich jak PDF, obraz oraz EPUB.

**P: Jak pobrać Aspose.HTML for Java?**  
O: Możesz pobrać ją ze strony [Aspose downloads](https://releases.aspose.com/html/java/).

**P: Czy mogę używać Aspose.HTML za darmo?**  
O: Tak, dostępna jest wersja próbna. Zarejestruj się [tutaj](https://releases.aspose.com/).

**P: Gdzie mogę znaleźć wsparcie dla Aspose.HTML?**  
O: Odwiedź [Aspose Support Forum](https://forum.aspose.com/c/html/29), aby uzyskać pomoc od społeczności i inżynierów Aspose.

**P: Czym są handlery wiadomości w Aspose.HTML?**  
O: Handlery wiadomości to komponenty, które przechwytują i przetwarzają żądania sieciowe w potoku — przydatne do logowania, uwierzytelniania lub pobierania własnych treści.

**P: Jak mogę dodać własny własny handler?**  
O: Zaimplementuj `IMessageHandler` i dodaj go do `MessageHandlerCollection` za pomocą `handlers.addItem(new MyCustomHandler())`.

**P: Czy można konwertować wiele plików ZIP jednocześnie?**  
O: Tak — iteruj listę ścieżek ZIP, ponownie używając tej samej konfiguracji i potoku dla każdej iteracji.

## Podsumowanie
Teraz wiesz **jak konwertować archiwa zip** na pliki PDF przy użyciu Aspose.HTML for Java, wraz z konfigurowalną usługą sieciową, własnym handlerem ZIP oraz precyzyjnym logowaniem czasu trwania żądania. Ten potok daje pełną kontrolę nad procesem konwersji, co czyni go idealnym rozwiązaniem dla automatycznego raportowania, archiwizacji dokumentów lub każdego scenariusza, w którym treść HTML musi być spakowana jako PDF.

---

**Ostatnia aktualizacja:** 2026-02-23  
**Testowano z:** Aspose.HTML for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}