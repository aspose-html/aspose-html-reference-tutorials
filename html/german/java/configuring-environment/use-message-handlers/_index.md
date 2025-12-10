---
date: 2025-12-10
description: Erfahren Sie, wie Sie Aspose verwenden, um defekte Links in Java zu behandeln,
  HTML in PNG zu konvertieren und ein HTML‑Dokument in Java mit Aspose.HTML für Java
  zu laden.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Wie man Aspose.HTML‑Message‑Handler in Java verwendet
url: /de/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Aspose.HTML Message Handlers in Java verwendet

## Einführung
In diesem Tutorial wird **how to use aspose** für die Behandlung fehlender Ressourcen in HTML Schritt für Schritt demonstriert. Wir erstellen ein einfaches HTML‑Dokument, das ein fehlendes Bild referenziert, fügen einen benutzerdefinierten Message Handler hinzu und zeigen Ihnen, wie Sie **load html document java** verwenden können, während Sie defekte Links elegant handhaben. Am Ende sehen Sie außerdem, wie Sie **convert html to png** mit Aspose.HTML nutzen können, was Ihnen ein vollständiges Bild der HTML‑zu‑Bild‑Konvertierung in Java liefert.

## Schnelle Antworten
- **Was ist der Hauptzweck eines Message Handlers?** Um Netzwerkoperationen abzufangen und auf Statuscodes wie fehlende Ressourcen zu reagieren.  
- **Kann Aspose.HTML HTML in PNG konvertieren?** Ja, mit `Converter.convertHTML` können Sie die HTML‑zu‑Bild‑Konvertierung durchführen.  
- **Benötige ich eine Lizenz für dieses Beispiel?** Eine temporäre Lizenz entfernt Bewertungseinschränkungen; eine permanente Lizenz ist für die Produktion erforderlich.  
- **Welche Java‑Version wird unterstützt?** Jede JDK 8+ (das Tutorial verwendet JDK 11).  
- **Ist es möglich, mehrere defekte Links zu behandeln?** Absolut – Sie können mehrere Handler verketten, um verschiedene Szenarien zu verwalten.

## Voraussetzungen
Bevor wir in die Schritt‑für‑Schritt‑Anleitung eintauchen, stellen Sie sicher, dass Sie alles Notwendige haben:
1. Java Development Kit (JDK): Stellen Sie sicher, dass das JDK auf Ihrem System installiert ist. Sie können es von der [Oracle-Website](https://www.oracle.com/java/technologies/javase-downloads.html) herunterladen.
2. Aspose.HTML für Java: Sie müssen Aspose.HTML für Java installiert haben. Sie können es von der [Aspose‑Release‑Seite](https://releases.aspose.com/html/java/) herunterladen.
3. IDE: Verwenden Sie Ihre bevorzugte integrierte Entwicklungsumgebung (IDE) für Java, wie IntelliJ IDEA, Eclipse oder NetBeans.
4. Grundkenntnisse in Java: Vertrautheit mit der Java‑Programmierung ist erforderlich, um diesem Tutorial effektiv zu folgen.
5. Temporäre Lizenz: Wenn Sie die Testversion von Aspose.HTML verwenden, sollten Sie eine [temporäre Lizenz](https://purchase.aspose.com/temporary-license/) erwerben, um Einschränkungen während der Entwicklung zu vermeiden.

## Pakete importieren
Bevor wir beginnen, stellen Sie sicher, dass die erforderlichen Pakete in Ihr Java‑Projekt importiert sind. Nachfolgend finden Sie die notwendigen Importe:
```java
import java.io.IOException;
```
Diese Importe geben Ihnen Zugriff auf die Klassen und Methoden, die für die Behandlung von Netzwerkoperationen, das Erstellen von HTML‑Dokumenten und die Durchführung der HTML‑zu‑PNG‑Konvertierung erforderlich sind.

## Schritt 1: HTML‑Code vorbereiten
Das Erste, was wir benötigen, ist ein einfacher HTML‑Snippet, das eine Bilddatei referenziert. Wir werden bewusst ein Bild referenzieren, das nicht existiert, um den Fehlerbehandlungsmechanismus auszulösen.
```java
String code = "<img src='missing.jpg'>";
```
Dieser Code erzeugt ein `<img>`‑Tag, das auf `missing.jpg` verweist. Da das Bild fehlt, gibt der Netzwerkdienst einen Nicht‑200‑Statuscode zurück, den unser benutzerdefinierter Handler abfängt.

## Schritt 2: HTML‑Code in eine Datei schreiben
Als Nächstes müssen wir das HTML‑Snippet speichern, damit Aspose.HTML es als Dokument laden kann.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
Mit einem `FileWriter` speichern wir das HTML in **document.html**. Diese Datei wird später die Quelle für den **load html document java**‑Schritt.

## Schritt 3: Benutzerdefinierten Message Handler erstellen
Jetzt erstellen wir einen benutzerdefinierten Message Handler, der reagiert, wenn das Bild nicht gefunden werden kann. Der Handler prüft den HTTP‑Statuscode und gibt eine freundliche Meldung aus.
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
Die Methode `invoke` untersucht `context.getResponse().getStatusCode()`. Wenn sie nicht **200** ist, geben wir eine klare Warnung aus, dass die Datei fehlt. Der abschließende Aufruf `invoke(context);` übergibt die Kontrolle an den nächsten Handler in der Kette.

## Schritt 4: Netzwerkdienst konfigurieren
Damit Aspose.HTML unseren Handler kennt, registrieren wir ihn beim Netzwerkdienst über die Klasse `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Hier erstellen wir eine `Configuration`‑Instanz, rufen den `INetworkService` ab und fügen unseren benutzerdefinierten Handler zu seiner Sammlung hinzu. Dadurch wird der Handler bei jeder Netzwerk‑Anfrage, z. B. beim Laden von Bildern, ausgeführt.

## Schritt 5: HTML‑Dokument laden
Mit der fertigen Konfiguration können wir nun die zuvor erstellte HTML‑Datei laden. Dieser Schritt demonstriert **load html document java**, während das fehlende Bild unseren Handler auslöst.
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
Der Konstruktor `HTMLDocument` erhält sowohl den Dateipfad als auch die benutzerdefinierte `configuration`. Wenn das Dokument das `<img>`‑Tag analysiert, versucht der Netzwerkdienst, `missing.jpg` abzurufen, erhält einen 404‑Fehler, und unser Handler gibt die Warnung aus.

## Schritt 6: HTML in PNG konvertieren
Um die umfassenderen Fähigkeiten von Aspose.HTML zu veranschaulichen, konvertieren wir das geladene Dokument in ein PNG‑Bild. Dies ist ein klassisches **convert html to png**‑Szenario.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` nimmt das `HTMLDocument`, optionale `ImageSaveOptions` (mit denen Sie DPI, Qualität usw. festlegen können) und den Ausgabedateinamen. Das Ergebnis ist ein Rasterbild des gerenderten HTML.

## Schritt 7: Ressourcen bereinigen
Eine ordnungsgemäße Ressourcenverwaltung ist in jeder Java‑Anwendung unerlässlich. Wir entsorgen sowohl die `Configuration` als auch das `HTMLDocument`, um Speicherlecks zu vermeiden.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Das Einwickeln der Bereinigung in einen `finally`‑Block garantiert die Ausführung, selbst wenn vorher eine Ausnahme auftritt.

## Warum Message Handler verwenden?
Message Handler geben Ihnen eine feinkörnige Kontrolle über Netzwerkoperationen wie **handle broken links java**. Anstatt die Bibliothek still scheitern zu lassen, können Sie protokollieren, erneut versuchen, Ressourcen ersetzen oder Fallback‑Inhalte bereitstellen – wodurch Ihre HTML‑Verarbeitung robust und produktionsreif wird.

## Häufige Probleme und Lösungen
- **Handler‑Rekursion** – Stellen Sie sicher, dass Sie `invoke(context);` nur einmal aufrufen, um Endlosschleifen zu vermeiden.  
- **Fehlende Lizenz** – Ohne eine gültige Lizenz kann die Konvertierung ein Bild mit Wasserzeichen erzeugen.  
- **Dateipfad‑Fehler** – Verwenden Sie absolute Pfade oder setzen Sie das Arbeitsverzeichnis korrekt, wenn Sie `document.html` laden.

## Häufig gestellte Fragen

**Q: Kann ich mehrere Message Handler verketten?**  
A: Ja, Sie können mehrere Handler zur `network.getMessageHandlers()`‑Sammlung hinzufügen; sie werden in der Reihenfolge ihrer Hinzufügung ausgeführt.

**Q: Funktioniert der Handler auch für CSS‑ oder Skript‑Ressourcen?**  
A: Absolut – jede Netzwerk‑Anfrage, die von der HTML‑Engine gestellt wird (Bilder, CSS, JS, Schriftarten), durchläuft den Handler.

**Q: Wie ändere ich die HTTP‑Anfrage, bevor sie gesendet wird?**  
A: Implementieren Sie einen Handler, der `context.getRequest()` modifiziert, bevor `invoke(context)` aufgerufen wird.

**Q: Gibt es eine Möglichkeit, die Warnung für bestimmte URLs zu unterdrücken?**  
A: Untersuchen Sie im Handler `context.getRequest().getRequestUri()` und überspringen Sie das Log bedingt.

**Q: Welche Version von Aspose.HTML wird für diese APIs benötigt?**  
A: Der Code funktioniert mit Aspose.HTML für Java 22.10 und später.

## Fazit
Und das war's – ein umfassender Leitfaden zu **how to use aspose** Message Handlern in Java. Wir haben das Erstellen einer HTML‑Datei, das Anschließen eines benutzerdefinierten Handlers an **handle broken links java**, das Laden des Dokuments und die Durchführung von **convert html to png** behandelt. Mit diesem Muster können Sie fehlende Ressourcen sicher verwalten, benutzerdefinierte Richtlinien durchsetzen und die Netzwerk‑Fähigkeiten von Aspose.HTML in jeder Java‑Anwendung erweitern.

---

**Zuletzt aktualisiert:** 2025-12-10  
**Getestet mit:** Aspose.HTML for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}