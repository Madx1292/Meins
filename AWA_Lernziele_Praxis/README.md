# Lernziele „Exportkontrolle in der Unternehmenspraxis" (Rise-360-Code-Block)

Immersiver Galerie-Rundgang durch die **fünf** Lernziele des Kurses. Gleiche
Architektur wie der Block zur US-Exportkontrolle, inhaltlich neu aufgesetzt.

Eigenständige `index.html` (1,1 MB, Bilder eingebettet) zum Hochladen als
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

## Vorspann: bitte entscheiden
Die Schnittfolge stammt aus dem US-Kurs. Sechs Schnitte, 4,2 s:

| Bild | Wort |
|------|------|
| Containerhafen | WARE VERLÄSST DAS HAUS |
| bis.gov | US-AUSFUHRVORSCHRIFTEN |
| Güterlisten-Position | US-GÜTERLISTE |
| Denied Persons List | US-SANKTIONSLISTE |
| Pressemitteilung Robert Bosch | AUCH IN DEUTSCHLAND |
| BIS-Heft | VERSTÖSSE HABEN FOLGEN |

**Drei der sechs Bilder sind US-Behördenseiten.** Für einen Kurs zur
betrieblichen Praxis ist das ein Übergang, keine Lösung: Wer den Vorspann sieht,
hält den Kurs in der ersten Sekunde für einen US-Kurs, und die vier Leitfragen
haben in diesem Material gar kein Bild. Deshalb tragen die Beschriftungen
ausdrücklich „US-".

Besser wäre ein Vorspann aus dem Papier, mit dem wirklich gearbeitet wird:
Verordnung (EU) 2021/821, Ausfuhrliste, BAFA, eine Arbeitsanweisung mit
Zuständigkeiten und Eskalationsweg, eine Auftragsbestätigung mit Angabe zur
Endverwendung, eine Red-Flag-Liste. Eigene Unterlagen vorher anonymisieren,
Bildrechte wie bisher abklopfen.

Die Schnitte stehen im Array `TR`, eine Zeile je Schnitt. Zeilen löschen
verkürzt den Vorspann; `IMG` enthält weiterhin alle acht Bilder des US-Kurses,
also auch `ofac` und `amat`.

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
