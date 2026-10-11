# Lernziele-Galerie (Rise-360-Code-Block)

Interaktiver Rundgang durch die vier Lernziele des Kurses „US-Exportkontrolle“.
Eigenständige `index.html` zum Hochladen als Code-Block in Rise 360.

## Auslieferung
`AWA_Lernziele_01c_Kurs_Galerie_Rise.zip` (im Wurzelverzeichnis) enthält
`index.html` + `OFL.txt` und wird in Rise 360 als Code-Block hochgeladen.

## Der Schalter für die Wanddekoration
Ganz oben im Skript steht eine Zeile:

```js
var DEKOR='leise';
```

- **`'leise'`** (Standard) – die echten Seiten liegen als sehr blasse,
  fast einfarbige Projektion auf den Wänden. Kein Rahmen, kein Wandschild,
  nicht zum Lesen gedacht. Man nimmt wahr: amtliche Dokumente, amerikanische
  Behörden – aber die Lernziele bleiben die einzige scharfe Ebene im Raum.
- **`'aus'`** – gar keine Bilder. Der Gang ist leer, der Auftakt dauert nur
  einen Schritt, das erste Lernziel kommt sofort.
- **`'voll'`** – die Seiten in Originalfarben, mit Rahmen und Wandschild.
  Schön anzusehen, zieht aber Aufmerksamkeit von den Lernzielen ab.

Warum das ein Schalter und keine feste Entscheidung ist: Die Screenshots
gehören semantisch nicht zu einem bestimmten Lernziel. Sie gehören zum
**Thema**. In diesem Block können sie nur Atmosphäre sein – ihren
eigentlichen Platz haben sie in den Lektionen, wo sie etwas erklären.

### Wandbilder austauschen
Die Bilddaten stehen als Base64-WebP im Objekt `IMG` (`ear`, `ofac`, `post`)
direkt in der index.html – keine externen Dateien, nichts kann beim Upload
verloren gehen. Platziert werden sie im Array `EX`:

```js
{p:1, s:1, k:'ear', c:[0,0,1,1], ar:.490, hf:.72,
 t:'Export Administration Regulations', u:'bis.gov · Table of Contents'}
```

- `p:0…1` Platz im Auftakt, `m:0…2` Platz zwischen Lernziel 1/2, 2/3, 3/4
- `s:-1` linke Wand, `s:1` rechte Wand
- `k` Schlüssel aus `IMG` – oder `i:'img/datei.png'` für eine Datei daneben
- `c:[x, y, Breite, Höhe]` Ausschnitt als Anteil des Bildes (`[0,0,1,1]` = ganz)
- `ar` Höhe/Breite **des Ausschnitts**, `hf` Höhe als Anteil der Raumhöhe
- `t` / `u` Wandschild (nur bei `DEKOR='voll'` sichtbar)

Ein neues Bild: als WebP (etwa 1300 px breit, Qualität 80) in Base64
umwandeln, in `IMG` eintragen, Eintrag in `EX` ergänzen. `ar` muss zum
Ausschnitt passen, sonst wird das Bild gestaucht.

### Rechtlicher Hinweis
Die Wandbilder sind Screenshots von bis.gov und ofac.treasury.gov. Inhalte
von US-Bundesbehörden sind in der Regel gemeinfrei; die **Dienstsiegel**
darauf sind es nicht in gleicher Weise. Für einen internen Schulungskurs
über genau diese Behörden ist die illustrative Verwendung üblich – bitte
trotzdem einmal mit eurer Rechtsabteilung abklopfen.

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
