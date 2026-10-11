# Lernziele-Galerie (Rise-360-Code-Block)

Interaktiver Rundgang durch die vier Lernziele des Kurses „US-Exportkontrolle“.
Eigenständige `index.html` zum Hochladen als Code-Block in Rise 360.

## Auslieferung
`AWA_Lernziele_01c_Kurs_Galerie_Rise.zip` (im Wurzelverzeichnis) enthält
`index.html` + `OFL.txt` und wird in Rise 360 als Code-Block hochgeladen.

## Vorspann: Trailer, Titel, dann der Gang
Der Block beginnt wie ein Filmvorspann:

1. **Schnittfolge** – acht Schnitte mit einem Bogen vom Welthandel bis zur
   Warnung, jeder mit einem Wort unten links:

   | # | Bild | Standzeit | Wort |
   |---|------|-----------|------|
   | 1 | Containerhafen | 1500 ms | GLOBALER HANDEL |
   | 2 | ofac.treasury.gov | 560 ms | OFAC |
   | 3 | bis.gov, EAR-Inhaltsverzeichnis | 520 ms | BIS |
   | 4 | ECCN 3B001, License Requirements | 470 ms | COMMERCE CONTROL LIST |
   | 5 | Denied Persons List | 430 ms | DENIED PERSONS LIST |
   | 6 | BIS-Pressemitteilung Applied Materials | 400 ms | ENFORCEMENT |
   | 7 | BIS-Pressemitteilung Robert Bosch | 380 ms | KONSEQUENZEN |
   | 8 | BIS-Heft „Don’t Let This Happen To You!“ | 640 ms | DON’T LET THIS HAPPEN TO YOU |

   Der erste Schnitt steht lange und atmet, danach werden die Standzeiten
   kürzer – das zieht an. Der letzte Schnitt steht wieder länger und
   bereitet die Titelkarte vor.
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

### Die Kräne arbeiten
Im ersten Schnitt hängen an zwei Kränen Container – und die bewegen sich:
der mittlere wird gehoben, der rechte gefiert. Dafür sind die beiden
Spreader aus dem Bild **freigestellt** worden; im Hintergrundbild (`port`)
sind sie wegretuschiert, die Hubseile enden sauber an der Stelle, an der
der Spreader in Ruhelage hängt. Die zwei Freisteller liegen als
`IMG.cmid` / `IMG.crgt` daneben und werden als eigene Ebene im Bild
platziert – in Prozent, also bei jeder Blockbreite passgenau:

```css
.awa-cz.a{left:52.47%;top:59.49%;width:5.34%;height:4.15%}
```

Beide bewegen sich nur **nach oben aus der Ruhelage heraus** bzw. in sie
hinein. So bleibt das Seil immer richtig lang: der Spreader verdeckt den
Teil des Seils, den er beim Heben aufwickeln würde. Gezeichnet werden muss
nichts nach. Bei `prefers-reduced-motion` wird die Ebene gar nicht erst
eingehängt.

Die Schnitte stehen im Array `TR`:

```js
{k:'port', c:[0,0,1,1], d:1500, t:'GLOBALER HANDEL', fy:.66, hz:1, slow:1}
```

- `k` Schlüssel aus `IMG`, `c` Ausschnitt, `d` Standzeit in Millisekunden
- `t` das Wort unten links
- `fx` / `fy` waagerechter bzw. senkrechter Bildausschnitt beim
  formatfüllenden Schnitt (0 = links/oben, .5 = Mitte, 1 = rechts/unten) –
  wichtig auf schmalen Blöcken
- `f:1` zeigt den Ausschnitt ganz, gerahmt auf hellem Grund, statt
  formatfüllend. Für hochformatige Ausschnitte wie das Heft oder die Sidebar.
- `hz:1` hängt die beiden Kran-Container ein (nur beim Hafenbild sinnvoll)
- `slow:1` nimmt die Kamerafahrt zurück: statt eines Zooms eine ruhige
  Fahrt mit leichtem Schwenk

Die Kamerafahrt ist eine **Heranfahrt** (`scale(1) → scale(1.045)`). Sie
beginnt also beim vollen Bildausschnitt – der erste Moment jedes Schnitts,
auf den das Auge springt, ist vollständig zu sehen – und zieht dann an.

## Der Gang selbst bleibt leer
Im Gang hängen **keine** Bilder – er gehört allein den Lernzielen
(`var DEKOR='aus';`). Die Wandbilder sind weiterhin eingebaut und über
`'leise'` oder `'voll'` zuschaltbar; platziert werden sie im Array `EX`.

## Bilder austauschen
Die Bilddaten stehen als Base64-WebP im Objekt `IMG` direkt in der
index.html – keine externen Dateien, nichts kann beim Upload verloren gehen.

| Schlüssel | Motiv | Größe |
|-----------|-------|--------|
| `port`  | Containerhafen (retuschiert, ohne die beiden Spreader) | 1254 × 1254 |
| `ofac`  | ofac.treasury.gov | 1700 × 877 |
| `ear`   | bis.gov, EAR Table of Contents | 1700 × 833 |
| `eccn`  | ECCN 3B001, License Requirements | 1360 × 913 |
| `dpl`   | Denied Persons List | 1460 × 868 |
| `amat`  | BIS-Pressemitteilung Applied Materials | 1480 × 840 |
| `bosch` | BIS-Pressemitteilung Robert Bosch | 1480 × 874 |
| `post`  | BIS-Heft „Don’t Let This Happen To You!“ | 270 × 703 |
| `cmid`  | Freisteller: Spreader am mittleren Kran | 67 × 52 |
| `crgt`  | Freisteller: Spreader am rechten Kran | 69 × 57 |

Zusammen rund 970 KB Base64; die fertige index.html wiegt etwa 1,1 MB.
Bei der Denied Persons List ist oben und links ein weißer Rand angesetzt,
damit die Überschrift während der Heranfahrt nicht an den Rand stößt.

Ein neues Bild: als WebP in Base64 umwandeln, in `IMG` eintragen, dann in
`TR` und/oder `EX` verwenden. Quellbilder sollten mindestens 1400 px breit
sein; alles darunter wird im formatfüllenden Schnitt sichtbar weich.

### Rechtlicher Hinweis
Die Screenshots stammen von bis.gov und ofac.treasury.gov. Inhalte von
US-Bundesbehörden sind in der Regel gemeinfrei; die **Dienstsiegel** darauf
sind es nicht in gleicher Weise. Für einen internen Schulungskurs über genau
diese Behörden ist die illustrative Verwendung üblich – bitte trotzdem
einmal mit eurer Rechtsabteilung abklopfen. Das Gleiche gilt für die
**Hafen-Illustration**, die nicht von einer Behörde stammt: hier bitte die
Lizenz der Bildquelle prüfen.

Die beiden Pressemitteilungen nennen **Firmennamen und Bußgeldsummen**
(Applied Materials, Robert Bosch GmbH). Das ist eine redaktionelle
Entscheidung – inhaltlich stark, aber bitte bewusst getroffen. Datum und
Wortlaut bitte an der Quelle gegenprüfen.

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
Mit Playwright bei 1000, 700 und 375 px sowie mit `prefers-reduced-motion`
geprüft: keine Konsolenfehler, kein horizontales Scrollen, im Ruhezustand
genau ein Transform-Wert über 40 Bilder (kein Wackeln), Rad / Ziehen /
Tastatur / Punkteleiste / Mini-Karten getestet.

Für den Vorspann zusätzlich: jeder der acht Schnitte im ersten Moment
abfotografiert (nichts Wichtiges liegt am Rand), die beiden Kran-Container
über eine Sekunde vermessen (sie laufen gegenläufig und ruckeln nicht),
und „noch einmal ansehen" geprüft – der Vorspann startet neu, der Rundgang
springt auf Anfang.
