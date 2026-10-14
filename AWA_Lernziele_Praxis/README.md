# Lernziele „Exportkontrolle in der Unternehmenspraxis" (Rise-360-Code-Block)

Immersiver Galerie-Rundgang durch die **fünf** Lernziele des Kurses. Gleiche
Architektur wie der Block zur US-Exportkontrolle, inhaltlich neu aufgesetzt.

Eigenständige `index.html` (535 KB, Bilder eingebettet) zum Hochladen als
Code-Block in Rise 360. Auslieferung: `AWA_Lernziele_Praxis_Rise.zip`
(index.html + OFL.txt).

## Die fünf Tafeln

| # | Karte | Schlagworte | golden unterstrichen | Motiv |
|---|-------|-------------|----------------------|-------|
| 01 | Zweck und Folgen | Schutzziele · Verstöße · Konsequenzen | mögliche Folgen von Verstößen | Balkenwaage mit goldenem Drehpunkt, links ein Schild, rechts eine Akte |
| 02 | Berührungspunkte | Arbeitsprozess · Schnittstellen · Rollen · Zuordnung | betriebliche Verantwortlichkeiten | der eigene Arbeitsweg mit vier Stationen; eine leuchtet golden |
| 03 | Vier Leitfragen | Ware · Zielland · Empfänger · Verwendungszweck | Leitfragen WAS, WOHIN, WER und WOFÜR | ein Vorgang, in vier Felder aufgefächert, Scanbalken darüber |
| 04 | Internes Programm | Zuständigkeiten · Prüfwege · Eskalation · Dokumentation | Prüf-, Eskalations- und Dokumentationswege | Bürohaus: Eskalation nach oben, Prüfen links, Dokumentation rechts |
| 05 | Red-Flag-Reaktion | Innehalten · Interne Meldung · Freigabe | angemessen zu reagieren | der Vorgang hält an der roten Fahne, wird gemeldet, läuft nach goldener Freigabe weiter |

Die **Lernzieltexte stehen Zeichen für Zeichen wie in der Kursvorlage**, nur ohne
Schlusspunkt – den setzt der Code. Maschinell geprüft. Die golden unterstrichene
Stelle wird per `String.replace` gesucht; sie muss deshalb wörtlich im Text stehen.

Kartennamen, Schlagworte und Motive sind neu entworfen und ergänzen die Vorlage,
ohne ihr etwas hinzuzudichten.

## Was gegenüber dem US-Block geändert wurde

**Inhalt**
- `G` und `ILL` auf fünf Einträge, alle Texte und Motive neu
- Titelkarte: „Exportkontrolle in der Unternehmenspraxis"
- Untertitel und Einleitung der Liste: „Nach Abschluss des Kurses kannst du …"
- Rahmenzeile der Bildunterschrift: „DU KANNST …" statt „DU LERNST …"
- Fortschritt „/ 05", Vorlesetext „Rundgang durch die fünf Lernziele"

**Technik** – der Vorgängerblock war an sieben Stellen fest auf vier Lernziele
verdrahtet. Alle rechnen jetzt mit `NG = G.length`:
Wandlichter, Bodenlichter, Tafelbau, Haltepunkte, Darstellung, Punkteleiste,
das `seen`-Feld und die Nummer der Endstation. Der Überblick nutzt
`repeat(auto-fit, minmax(148px, 1fr))` statt fester vier Spalten.
**Dadurch trägt der Block jetzt beliebig viele Lernziele**: `G` und `ILL` müssen
nur gleich lang bleiben, alles andere ergibt sich.

**Barrierefreiheit** – zwei Mängel behoben, die auch im US-Block stecken:
- Der Vorspann war komplett `aria-hidden`, enthielt aber zwei bedienbare
  Schaltflächen („Lernziele entdecken", „Überspringen"). Jetzt sind nur noch die
  Bildebenen ausgeblendet.
- Der Fokusring war Gold auf Weiß (rund 1,7:1 Kontrast, zu wenig). Jetzt Petrol
  mit weichem Hof.

## Vorspann: Pressespiegel
Der Vorspann ist kein Vollbild-Schnitt mehr, sondern ein **Pressespiegel**:
Ausschnitte fallen nacheinander leicht gedreht auf eine helle Fläche, schieben
sich übereinander und ragen über den Rand hinaus – wie Zeitungsausschnitte auf
einem Tisch. Jeder Ausschnitt hat eine weiße Papierkante und einen weichen
Schatten. Am Ende bleibt der Stapel schwach sichtbar hinter der Titelkarte stehen.

Die Ausschnitte stehen im Array `TR`, eine Zeile je Ausschnitt:

```js
{k:'zweck', c:[0,0,1,1], d:760, t:'WARUM EXPORTKONTROLLE', w:.58, x:-.18, y:-.19, r:-3.6}
```

- `k` Schlüssel aus `IMG`, `c` Bildausschnitt `[x, y, Breite, Höhe]` als Anteil
- `d` Standzeit in Millisekunden, `t` das Wort unten links
- `w` Breite als Anteil der Bühnenbreite
- `x` / `y` Versatz aus der Mitte, als Anteil von Bühnenbreite bzw. -höhe
- `r` Drehung in Grad

Ausschnitte dürfen über den Rand hinausragen – angeschnitten ist gewollt. Auf
schmalen Blöcken greifen sie automatisch weiter (Faktor 1,62 bei S, 1,18 bei M)
und rücken enger zusammen, sonst schwimmen sie verloren in der Fläche.

### Die Ausschnitte
Fünf Seiten, alle amtlich, alle deutsch, selbst erfasst am 14.10.2026:

| Ausschnitt | Quelle | Wort |
|---|---|---|
| `zweck`  | BAFA – Allgemeine Einführung in die Exportkontrolle | WARUM EXPORTKONTROLLE |
| `vo`     | EUR-Lex – Verordnung (EU) 2021/821 (EU-Dual-Use-VO) | EU-DUAL-USE-VERORDNUNG |
| `recht`  | BAFA – Rechtsgrundlagen (AWG, AWV, Dual-Use-VO) | AWG UND AWV |
| `gueter` | BAFA – Güterlisten (Anhänge EU-Dual-Use-VO, Ausfuhrliste) | GÜTERLISTEN |
| `hilfen` | BAFA – Arbeitshilfen (Merkblätter, HADDEX) | MERKBLÄTTER UND HADDEX |

Der Bogen führt vom Warum über die EU-Verordnung und das deutsche Recht zu den
Listen und endet beim Arbeitsmaterial – also dort, wo die Lerner im Alltag
landen.

**Die Ausschnitte zeigen bewusst nur Text.** Beide BAFA-Seiten tragen
lizenzierte Stockfotos (Fotolia); die Ausschnitte sind so gesetzt, dass davon
nichts im Bild ist. Wird neu zugeschnitten, bitte darauf achten.

**Lizenz:** EUR-Lex ist zur Weiterverwendung freigegeben (Beschluss
2011/833/EU), Quellenangabe genügt. Für bafa.de gelten die Nutzungsbedingungen
im Impressum – für interne Schulung üblicherweise unproblematisch, einmal
hinschauen schadet nicht.

### Was noch fehlt
Ein Ausschnitt zu **Verstößen und ihren Folgen** – Lernziel 1 nennt sie
ausdrücklich. Gesucht wurde bei Zoll, Generalbundesanwalt und Europol:

- zoll.de führt in der Presse die Rubriken Rauschgift, Schwarzarbeit,
  Produktpiraterie, Bargeld und Jahresbilanzen – **keine zur Außenwirtschaft**
- der Generalbundesanwalt veröffentlicht derzeit zu Terrorismus, Spionage und
  Völkerstrafrecht, nicht zur Ausfuhrkontrolle
- die Pressemitteilungssuche des Zolls weist automatisierte Zugriffe ab

Ein Verlagsartikel wäre die naheliegende Lücke-Füllung, ist aber ein
geschütztes Werk. Sauberer: eine amtliche Mitteilung heraussuchen, sobald eine
passende vorliegt, und als sechsten Ausschnitt in `TR` ergänzen.

## Inhalt ändern
- `G` – die fünf Lernziele (Name, Icon, Akzentfarben, Schlagworte, Text,
  hervorgehobene Stelle)
- `ILL` – je ein SVG-Motiv, gleiche Reihenfolge wie `G`
- `TR` – die Schnitte des Vorspanns
- `CFG` – Raummaße je Breite (L / M / S)

Die Motive nutzen nur diese Bausteine: `.s1` kräftige Kontur, `.s2` Hilfslinie,
`.s3` mittlere Kontur, `.gd` Goldfläche, `.gs` Goldkontur, `.lb` Beschriftung,
dazu die Bewegungen `.dash .draw .drop .ping .scan .mer .blink .wave .sweep`.
Ein goldenes Element je Motiv, Rot nur auf Tafel 05.

## Prüfung
Mit Playwright bei 1000, 700 und 375 px sowie mit `prefers-reduced-motion`
durchgespielt: keine Konsolenfehler, kein horizontales Scrollen, im Ruhezustand
genau ein Transform-Wert über 40 Bilder (kein Wackeln). Alle fünf Stationen
öffnen sich, Fortschritt läuft 01 → 05, Punkteleiste hat sieben Punkte,
Überblick zeigt fünf Mini-Karten, Dialog „Alle Lernziele" listet alle fünf
Lernzieltexte wortgleich.

Zusätzlich inhaltlich gegengelesen: Treue zur Vorlage, Rechtschreibung und
Zeichensetzung, Hausstil, und gezielt die Stellen, die noch von vier Lernzielen
ausgingen.

### Bekannte Einschränkung
Die Motiv-Klassen (`.s1`, `.s2`, `.gd` …) tragen kein `awa-`-Präfix. Sie sind
unter `#awa-lernziele` verschachtelt und können nicht nach außen wirken –
theoretisch könnte aber fremdes CSS aus Rise mit gleichnamigen Klassen
hineinwirken. Bisher in keinem Kurs aufgetreten.
