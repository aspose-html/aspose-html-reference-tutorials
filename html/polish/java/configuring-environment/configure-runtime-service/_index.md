---
date: 2025-12-10
description: Dowiedz się, jak ustawić limit czasu w Aspose.HTML dla Javy, skonfigurować
  usługę Runtime Service do konwersji HTML na PNG, zapobiegać nieskończonym pętlom
  i zwiększyć wydajność.
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Jak ustawić limit czasu w usłudze Aspose.HTML dla środowiska uruchomieniowego
  Java
url: /pl/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić limit czasu w usłudze Runtime Aspose.HTML dla Java

## Wprowadzenie
Jeśli szukasz **jak ustawić limit czasu** dla skryptów podczas pracy z Aspose.HTML dla Java, trafiłeś we właściwe miejsce. Kontrola wykonywania skryptów nie tylko zapobiega nieskończonym pętlom, ale także pomaga **szybciej konwertować html na png** i utrzymać responsywność aplikacji. W tym samouczku przeprowadzimy Cię krok po kroku przez konfigurację usługi Runtime, ograniczenie wykonywania skryptów i ostateczne wygenerowanie obrazu PNG z HTML bez zawieszania programu.

## Szybkie odpowiedzi
- **Co robi usługa Runtime?** Pozwala kontrolować czas wykonywania skryptów i zarządzać zasobami podczas przetwarzania HTML.  
- **Jak ustawić limit czasu dla JavaScript?** Użyj `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.  
- **Czy mogę zapobiec nieskończonym pętlom?** Tak – limit czasu przerywa pętle, które przekraczają określony limit.  
- **Czy ma to wpływ na konwersję HTML‑do‑PNG?** Nie, konwersja przebiega po zakończeniu skryptu lub jego przerwaniu przez limit czasu.  
- **Jakiej wersji Aspose.HTML potrzebuję?** Najnowszej dostępnej na stronie pobierania Aspose.

## Wymagania wstępne
Zanim przejdziemy do szczegółów, upewnij się, że masz następujące elementy:

1. **Java Development Kit (JDK)** – zainstaluj go ze [strony Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Biblioteka Aspose.HTML dla** – pobierz najnowszą wersję ze [strony wydań Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse lub NetBeans będą odpowiednie.  
4. **Podstawowa znajomość Java i HTML** – niezbędna do zrozumienia fragmentów kodu.

## Importowanie pakietów
Najpierw zaimportuj klasy, które będą potrzebne. Import `java.io.IOException` jest wymagany do obsługi plików.

```java
import java.io.IOException;
```

## Krok 1: Utworzenie pliku HTML z kodem JavaScript
Zaczniemy od wygenerowania prostego pliku HTML zawierającego pętlę JavaScript. Pętla ta działałaby w nieskończoność, gdyby nie wymuszony limit czasu, co czyni ją idealnym przykładem dla usługi Runtime.

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

- Skrypt `while(true) {}` reprezentuje potencjalną nieskończoną pętlę.  
- `FileWriter` zapisuje zawartość HTML do **runtime-service.html**.

## Krok 2: Utworzenie obiektu konfiguracji
Następnie utwórz instancję `Configuration`. Ten obiekt jest podstawą wszystkich usług Aspose.HTML, w tym usługi Runtime.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Krok 3: Konfiguracja usługi Runtime
Tutaj faktycznie **ustawiamy limit czasu**. Pobierając `IRuntimeService` z konfiguracji, możemy zdefiniować limit wykonywania JavaScript.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` ogranicza wykonywanie skryptu do **5 sekund**, skutecznie **zapobiegając nieskończonym pętlom**.  
- To także **ogranicza wykonywanie skryptu** dla wszelkiego ciężkiego kodu po stronie klienta.

## Krok 4: Załadowanie dokumentu HTML z konfiguracją
Teraz wczytaj plik HTML używając konfiguracji, która zawiera naszą regułę limitu czasu.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Dokument respektuje wcześniej zdefiniowany limit, więc niekończąca się pętla zostanie zatrzymana po 5 sekundach.

## Krok 5: Konwersja HTML do PNG
Po bezpiecznym załadowaniu dokumentu możemy **konwertować html na png**. Konwersja odbywa się dopiero po zakończeniu skryptu lub jego przerwaniu przez limit czasu.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions` instruuje Aspose.HTML, aby wyjściowym formatem był obraz PNG.  
- Powstały plik, **runtime-service_out.png**, przedstawia wyrenderowany HTML bez zawieszania aplikacji.

## Krok 6: Zwolnienie zasobów
Na koniec zwolnij obiekty, aby uwolnić pamięć i uniknąć wycieków.

```java
} finally {
    if (document != null) {
        document.dispose();
    }
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- Prawidłowe zwalnianie jest kluczowe w aplikacjach działających długo.

## Zakończenie
Właśnie nauczyłeś się **ustawiać limit czasu** dla wykonywania JavaScript w Aspose.HTML dla Java, **zapobiegać nieskończonym pętlom** oraz **bezpiecznie konwertować html na png**. Konfigurując usługę Runtime zyskujesz precyzyjną kontrolę nad zachowaniem skryptów, co przekłada się na szybsze uruchamianie i bardziej niezawodne konwersje. Eksperymentuj z różnymi wartościami limitu, aby dopasować je do swoich obciążeń, a zauważysz wyraźny wzrost wydajności.

## Najczęściej zadawane pytania

**P: Jaki jest cel usługi Runtime w Aspose.HTML dla Java?**  
O: Pozwala kontrolować czas wykonywania skryptów, pomagając **zapobiegać nieskończonym pętlom** i utrzymać responsywność konwersji.

**P: Jak mogę pobrać Aspose.HTML dla Java?**  
O: Pobierz najnowszą wersję ze [strony wydań](https://releases.aspose.com/html/java/).

**P: Czy konieczne jest zwolnienie obiektów `document` i `configuration`?**  
O: Tak, zwolnienie zwalnia zasoby natywne i zapobiega wyciekom pamięci.

**P: Czy mogę ustawić limit czasu JavaScript na inną wartość niż 5 sekund?**  
O: Oczywiście – zmień argument w `TimeSpan.fromSeconds()` na dowolny limit pasujący do Twojego scenariusza.

**P Gdzie mogę znaleźć pomoc w razie problemów?**  
O: Odwiedź [forum Aspose.HTML](https://forum.aspose.com/c/html/29), gdzie społeczność i personel udzielają wsparcia.

---

**Ostatnia aktualizacja:** 2025-12-10  
**Testowano z:** Aspose.HTML dla Java 24.11 (najnowsza)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}