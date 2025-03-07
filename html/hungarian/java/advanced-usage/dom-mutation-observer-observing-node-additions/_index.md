---
title: DOM Mutation Observer Aspose.HTML for Java-val
linktitle: DOM Mutation Observer – Csomópont-kiegészítések megfigyelése
second_title: Java HTML feldolgozás Aspose.HTML-lel
description: Ebből a lépésről lépésre szóló útmutatóból megtudhatja, hogyan használja az Aspose.HTML for Java-t DOM-mutáció-megfigyelő megvalósításához. Hatékonyan figyeli és reagál a DOM-változásokra.
weight: 11
url: /hu/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# DOM Mutation Observer Aspose.HTML for Java-val


Ön Java-fejlesztő, aki egy HTML-dokumentum Document Object Model (DOM) változásait szeretné megfigyelni és reagálni? Az Aspose.HTML for Java hatékony megoldást kínál erre a feladatra. Ebben a lépésenkénti útmutatóban megvizsgáljuk, hogyan használhatjuk az Aspose.HTML for Java-t HTML-dokumentumok létrehozására és a csomópontok hozzáadásának megfigyelésére a Mutation Observer segítségével. Ez az oktatóanyag végigvezeti a folyamaton, minden példát több lépésre bontva. A végére könnyedén implementálhatja a DOM mutációfigyelőket Java projektjeibe.

## Előfeltételek

Mielőtt belevágnánk az Aspose.HTML for Java használatába, győződjünk meg arról, hogy megvannak a szükséges előfeltételek:

1. Java fejlesztői környezet: Győződjön meg arról, hogy a Java Development Kit (JDK) telepítve van a rendszerén.

2.  Aspose.HTML for Java: Le kell töltenie és telepítenie kell az Aspose.HTML for Java programot. A letöltési linket megtalálod[itt](https://releases.aspose.com/html/java/).

3. IDE (Integrated Development Environment): Java kód írásához és futtatásához használja a preferált Java IDE-t, mint például az IntelliJ IDEA vagy az Eclipse.

## Csomagok importálása

Az Aspose.HTML for Java használatának megkezdéséhez importálnia kell a szükséges csomagokat a Java-kódba. A következőképpen teheti meg:

```java
// Importálja a szükséges csomagokat
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// Hozzon létre egy üres HTML dokumentumot
HTMLDocument document = new HTMLDocument();
```

Most, hogy importálta a szükséges csomagokat, folytassa a DOM Mutation Observer Java nyelven történő megvalósításának lépésről lépésre szóló útmutatójával.

## 1. lépés: Hozzon létre egy Mutation Observer példányt

Először is létre kell hoznia egy Mutation Observer példányt. Ez a megfigyelő figyeli a DOM változásait, és mutációk esetén visszahívási funkciót hajt végre.

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

Ebben a lépésben létrehozunk egy megfigyelőt egy visszahívási funkcióval, amely üzenetet nyomtat, amikor csomópontokat adnak a DOM-hoz.

## 2. lépés: Az Observer konfigurálása

Most állítsuk be a megfigyelőt a kívánt opciókkal. Meg akarjuk figyelni a gyermeklista és részfa változásait, valamint a karakteradatok változásait.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Adja meg a célcsomópontot a megfigyeléshez a megadott konfigurációval
observer.observe(document.getBody(), config);
```

 Itt beállítjuk a`config` objektumot a gyermeklista-, részfa- és karakteradatok változásainak megfigyelésére. Ezután átadjuk a célcsomópontot (ebben az esetben a dokumentumé`<body>`) és a konfigurációt a megfigyelő számára.

## 3. lépés: Módosítsa a DOM-ot

Most néhány változtatást végzünk a DOM-on, hogy elindítsuk a megfigyelőt. Létrehozunk egy bekezdéselemet, és hozzáfűzzük a dokumentum törzséhez.

```java
// Hozzon létre egy bekezdéselemet, és fűzze hozzá a dokumentumtörzshez
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Hozzon létre egy szöveget, és fűzze a bekezdéshez
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

Ebben a lépésben létrehozunk egy HTML bekezdéselemet, és hozzáadjuk a dokumentum törzséhez. Ezután létrehozunk egy szöveges csomópontot a „Hello World” tartalommal, és hozzáfűzzük a bekezdéshez.

## 4. lépés: Várjon a megfigyelésekre (aszinkron módon)

Mivel a mutációk aszinkron módon figyelhetők meg, várnunk kell egy pillanatot, hogy a megfigyelő rögzítse a változásokat. Használjuk`synchronized` és`wait` erre a célra, az alábbiak szerint.

```java
// Mivel a mutációk aszinkron módban működnek, várjon néhány másodpercet
synchronized (this) {
    wait(5000);
}
```

Itt 5 másodpercet várunk, hogy a megfigyelőnek legyen esélye az esetleges mutációk rögzítésére.

## 5. lépés: Hagyja abba a megfigyelést

Végül, amikor befejezte a megfigyelést, elengedhetetlen, hogy a megfigyelőt lekapcsolja az erőforrások felszabadítása érdekében.

```java
// Hagyd abba a megfigyelést
observer.disconnect();
```

Ezzel a lépéssel befejezte a megfigyelést, és megtisztíthatja az erőforrásokat.

## Következtetés

Ebben az oktatóanyagban végigvezettük az Aspose.HTML for Java használatát egy DOM-mutációs megfigyelő megvalósításához. Megtanulta, hogyan lehet megfigyelőt létrehozni, konfigurálni, módosítani a DOM-ot, várni a megfigyelésekre, és abbahagyni a megfigyelést. Most már rendelkezik azzal a képességgel, hogy DOM-mutáció-megfigyelőket alkalmazzon Java-projektjeiben, hogy hatékonyan figyelje a HTML-dokumentumok DOM-jának változásait és reagáljon azokra.

Ha bármilyen kérdése van, vagy problémába ütközik, ne habozzon kérni segítséget a[Aspose.HTML fórum](https://forum.aspose.com/) . Ezenkívül hozzáférhet a[dokumentáció](https://reference.aspose.com/html/java/) részletes információkért az Aspose.HTML for Java-ról.

## GYIK

### 1. kérdés: Mi az a DOM-mutációs megfigyelő?

1. válasz: A DOM-mutációfigyelő egy JavaScript-funkció, amely lehetővé teszi a HTML-dokumentumok dokumentumobjektum-modelljében (DOM) bekövetkezett változások figyelését. Lehetővé teszi a DOM-csomópontok hozzáadásának, törlésének vagy módosításának valós idejű reagálását.

### 2. kérdés: Használhatom az Aspose.HTML for Java-t kereskedelmi projektjeimben?

 2. válasz: Igen, az Aspose.HTML for Java használható kereskedelmi projektekben. Megtalálhatja az engedélyezési és vásárlási információkat[itt](https://purchase.aspose.com/buy).

### 3. kérdés: Elérhető ingyenes próbaverzió az Aspose.HTML for Java számára?

 3. válasz: Igen, megkaphatja az Aspose.HTML ingyenes próbaverzióját Javahoz[itt](https://releases.aspose.com/). Ez lehetővé teszi, hogy a vásárlás előtt felfedezze a funkcióit és képességeit.

### 4. kérdés: Milyen előnyökkel jár a karakteradatok változásainak a Mutation Observer segítségével történő megfigyelése?

4. válasz: A karakteradatok változásainak megfigyelése olyan forgatókönyvekben hasznos, ahol a HTML-elemek szövegtartalmának változásait szeretné figyelni és reagálni azokra. Használhatja például a webes űrlapokon lévő felhasználói bevitel nyomon követésére és reagálására.

### 5. kérdés: Hogyan távolíthatom el az erőforrásokat az Aspose.HTML for Java használatakor?

 5. válasz: Fontos, hogy felszabadítsa az erőforrásokat, ha végzett. Példánkban használtuk`document.dispose()` a HTML-dokumentumhoz társított erőforrások megtisztításához. Ügyeljen arra, hogy a létrehozott objektumokat és erőforrásokat semmisítse meg, hogy elkerülje a memóriaszivárgást.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
