# Lernziele-Galerie (Rise-360-Code-Block)

Interaktiver Rundgang durch die vier Lernziele des Kurses „US-Exportkontrolle“.
Eigenständige `index.html` zum Hochladen als Code-Block in Rise 360.

## Auslieferung
`AWA_Lernziele_01c_Kurs_Galerie_Rise.zip` (im Wurzelverzeichnis) enthält
`index.html` + `OFL.txt` und wird in Rise 360 als Code-Block hochgeladen.

## Dramaturgie: erst der Gang, dann die Lernziele
Der Rundgang hat zwei Teile.

**Auftakt** – man fährt wie in einer Kamerafahrt durch den Gang. Links und
rechts hängen Exponate aus der Welt des Kurses, jedes mit einem Wandschild:
Vereinigte Staaten, BIS, OFAC, EAR. Zwischen den späteren Lernzielen hängen
weitere: Commerce Control List, Country Groups, Reexport. Keine Haltepunkte
mit Inhalt, nur Atmosphäre und Kontext.

**Lernziele** – danach beginnen die vier Stationen (siehe unten).

### Exponate austauschen
Alle Exponate stehen im Skript in einem Array `EX`:

```js
{p:1, s:1, t:'BIS', u:'Genehmigungen für Dual-Use-Güter', c:agency(...)}
```

- `p:0…3` = Platz im Auftakt, `m:0…2` = Platz zwischen Lernziel 1/2, 2/3, 3/4
- `s:-1` linke Wand, `s:1` rechte Wand
- `t` / `u` = Wandschild (Titel, Unterzeile)
- `c` = die eingebaute Grafik

**Echtes Bild statt Grafik:** `c` weglassen und stattdessen
`img:'img/bis.png'` setzen, die Datei neben die `index.html` legen und mit
ins ZIP packen. Das Bild füllt den Rahmen (`object-fit: cover`), gutes
Seitenverhältnis ist etwa 4:3.

### Was hier bewusst NICHT drin ist
Die mitgelieferten Exponate sind **Platzhalter**, keine Nachbildungen:
- **Keine Behördensiegel.** BIS und OFAC stehen als Schrifttafeln mit dem
  ausgeschriebenen Namen da. Die echten Siegel nachzuzeichnen wäre das
  Nachbauen eines Hoheitszeichens – wenn ihr die Logos verwenden dürft,
  legt die Dateien als `img:` dazu.
- **Keine Screenshots der CCL oder der Country Groups.** Gezeigt wird nur
  die öffentliche *Struktur*: die zehn CCL-Kategorien 0–9 mit den
  Produktgruppen A–E und die Bezeichnungen der Country Groups
  (A:1, B, D:1, E:1 …) ohne Länderzuordnung. Erfundene ECCN oder erfundene
  Länderlisten hätten in einem Compliance-Kurs nichts zu suchen.
- Die **US-Flagge** ist gezeichnet (gemeinfreies Design), in gedämpften
  Tönen, damit sie neben Petrol und Gold nicht schreit.

Fachlich gegenlesen: die Kategorientexte der CCL und die Kurzbeschreibungen
der Country Groups.

## Dramaturgie der Stationen: erst Gemälde, dann Lernziel
Jede Station hat zwei Haltepunkte:

1. **Geschlossen** – das Bild hängt ruhig im Gang. Zu sehen sind nur die große,
   schimmernde Nummer, ein blasser Umriss des Motivs, das Prägesiegel und
   „Näher treten“.
2. **Offen** – beim Weiterscrollen (oder Tippen/Klicken auf das Bild) tritt die
   Kamera heran und das Bild öffnet sich: die Nummer verblasst, das Motiv
   zeichnet sich fertig und nimmt Farbe an, Titel, Schlagworte und der
   Lernzieltext erscheinen.

Dadurch gibt es zehn Haltepunkte (Start, 4 × zu/offen, Überblick); die
Punkteleiste rechts zeigt weiterhin nur die sechs Stationen (`RAIL`).
Der Knopf unten rechts beschriftet sich mit: „Rundgang starten“ →
„Lernziel zeigen“ → „Weiter“ → „Zum Überblick“.

## US-Bezug: Gravur statt Flagge
Der Bezug zum US-Regelwerk liegt in der Papier- und Urkundenwelt, nicht in
nationaler Symbolik:
- eine feine **Guilloche-Rosette** (Wertpapierstich) ganz hinten im Gang – man
  geht auf das Regelwerk zu,
- ein **Prägesiegel mit Stern** auf jedem Bild,
- im Motiv von Lernziel 1 die beschrifteten Rechtsräume **US** und **EU**.

## Rot bei Red Flags
Rot (`#d7382c`) steht hier für den Fachbegriff „Red Flag“, nicht als
Bewertungsfarbe. Erledigt/dokumentiert bleibt petrol, Hinweise bleiben gold –
die Kursregel gilt unverändert.

## Aufbau
- **Halle**: ein statisches SVG mit exakter Fluchtpunkt-Geometrie
  (Decke, Boden, zwei Wände, Sockelleiste, Bilderschiene, Lichtvoute).
  Da die Kamera sich nur vorwärts bewegt, bleibt diese Projektion unverändert –
  sie wird einmal pro Größenänderung gezeichnet.
- **Welt**: alle beweglichen Teile (Wandrippen, Deckenlichter, Bodenbalken,
  Staub, Lernziel-Tafeln, Wand- und Bodenlicht) sind achsenparallele Elemente,
  die pro Bild mit `translate3d(...) scale(...)` gesetzt werden. Die Perspektive
  wird dabei selbst gerechnet (`s = f / z`).
  Kein CSS-3D, keine gedrehten Ebenen, kein globales `scale` auf der Bühne –
  deshalb steht das Bild im Ruhezustand absolut still und Text bleibt scharf.
- **Bedienung**: Mausrad, Ziehen/Wischen, Pfeiltasten, Pos1/Ende, Punkteleiste,
  Klick/Tipp auf ein Bild, Weiter/Zurück. Am Anfang und Ende gibt der Block
  das Scrollen an die Seite ab.
- **Barrierefreiheit**: Die Szene ist `aria-hidden`; der Lernziel-Text steht in
  der Bildunterschrift (`aria-live`) und vollständig im Dialog „Alle Lernziele“.
  `prefers-reduced-motion` wird respektiert.

## Inhalt ändern
Alles Inhaltliche steht im Skript in einem Block:

- `G` – die vier Lernziele (Name, Icon, Akzentfarben, Chips, Text, hervorgehobene Stelle)
- `ILL` – je ein SVG-Motiv pro Lernziel (gleiche Reihenfolge wie `G`)
- `CFG` – Raummaße je Breite (L / M / S)

Werden Lernziele hinzugefügt oder entfernt, müssen `G` und `ILL` gleich lang
bleiben; die Zahl der Haltepunkte, die Punkteleiste und der Überblick ergeben
sich daraus automatisch. Die Beschriftung „/ 04“ im Fortschritt und die
Rahmenzeile der Bildunterschrift stehen im HTML.

## Prüfung
Mit Playwright bei 1000, 700 und 375 px geprüft: keine Konsolenfehler, kein
horizontales Scrollen, im Ruhezustand genau ein Transform-Wert über 36 Bilder
(kein Wackeln), Rad / Ziehen / Tastatur / Punkteleiste / Mini-Karten getestet.
