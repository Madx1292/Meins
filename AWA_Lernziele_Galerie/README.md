# Lernziele-Galerie (Rise-360-Code-Block)

Interaktiver Rundgang durch die vier Lernziele des Kurses „US-Exportkontrolle“.
Eigenständige `index.html` zum Hochladen als Code-Block in Rise 360.

## Auslieferung
`AWA_Lernziele_01c_Kurs_Galerie_Rise.zip` (im Wurzelverzeichnis) enthält
`index.html` + `OFL.txt` und wird in Rise 360 als Code-Block hochgeladen.

## Vorspann: Trailer, Titel, dann der Gang
Der Block beginnt wie ein Filmvorspann:

1. **Schnittfolge** – sechs schnelle Schnitte aus der Welt des Kurses, jeder
   mit einem Wort unten links: OFAC · BIS · EXPORT ENFORCEMENT ·
   COMMERCE CONTROL LIST · SANCTIONS LISTS · 15 CFR 730–774. Die Standzeiten
   werden kürzer (620 → 400 ms), das zieht an.
2. **Titelkarte** – **US-Exportkontrolle** fährt aus der Unschärfe heran,
   ein Lichtstreifen läuft darüber, darunter eine Gold-Petrol-Linie und
   „In diesem Kurs lernst du …".
3. **Knopf „Lernziele entdecken"** – der Vorspann bleibt stehen, bis man
   ihn drückt. Erst dann blendet er ab und der Gang beginnt.

Während der Schnitte gibt es rechts unten **„Überspringen"**; Scrollen,
Tippen oder eine Taste brechen ebenfalls ab. Der Vorspann startet erst,
wenn der Block im Bild ist (IntersectionObserver), nicht schon beim Laden
der Rise-Seite. Bei `prefers-reduced-motion` entfällt die Schnittfolge und
die Titelkarte steht sofort da.

**Noch einmal ansehen:** der runde Knopf mit dem Abspielsymbol oben rechts
startet den Vorspann neu und setzt den Rundgang auf den Anfang zurück.

Die Schnitte stehen im Array `TR`:

```js
{k:'ofac', c:[0,0,1,1], d:620, t:'OFAC', fx:.22}
```

- `k` Schlüssel aus `IMG`, `c` Ausschnitt, `d` Standzeit in Millisekunden
- `t` das Wort unten links
- `fx` waagerechter Bildausschnitt beim formatfüllenden Schnitt (0 = links,
  .5 = Mitte, 1 = rechts) – wichtig auf schmalen Blöcken
- `f:1` zeigt den Ausschnitt ganz, gerahmt auf hellem Grund, statt
  formatfüllend. Für hochformatige Ausschnitte wie das Heft oder die Sidebar.

## Der Gang selbst bleibt leer
Im Gang hängen **keine** Bilder – er gehört allein den Lernzielen
(`var DEKOR='aus';`). Die Wandbilder sind weiterhin eingebaut und über
`'leise'` oder `'voll'` zuschaltbar; platziert werden sie im Array `EX`.

## Bilder austauschen
Die Bilddaten stehen als Base64-WebP im Objekt `IMG` (`ear`, `ofac`, `post`)
direkt in der index.html – keine externen Dateien, nichts kann beim Upload
verloren gehen. Sie liegen in **voller Auflösung** (1873 bzw. 1872 px breit,
Qualität 88), damit die Schnitte auf großen Bildschirmen scharf bleiben.

Ein neues Bild: als WebP in Base64 umwandeln, in `IMG` eintragen, dann in
`TR` und/oder `EX` verwenden. Quellbilder sollten mindestens 1400 px breit
sein; alles darunter wird im formatfüllenden Schnitt sichtbar weich.

### Rechtlicher Hinweis
Die Bilder sind Screenshots von bis.gov und ofac.treasury.gov. Inhalte von
US-Bundesbehörden sind in der Regel gemeinfrei; die **Dienstsiegel** darauf
sind es nicht in gleicher Weise. Für einen internen Schulungskurs über genau
diese Behörden ist die illustrative Verwendung üblich – bitte trotzdem
einmal mit eurer Rechtsabteilung abklopfen.

## Sprache und Satzzeichen
- Bildunterschrift je Station: Rahmenzeile „DU LERNST …", darunter der
  Lernzieltext mit **Punkt** am Ende.
- Dialog „Alle Lernziele": Einleitung „In diesem Kurs lernst du …", die
  Lernziele 1–3 mit **Semikolon**, das vierte mit **Punkt** – wie in der
  Kursvorlage.
- Die vier Lernzieltexte stehen wortgleich zur Vorlage im Array `G` und
  werden nirgends gekürzt.

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
