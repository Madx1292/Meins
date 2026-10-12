# Lernziele „Vertretung im Zollverfahren" (Rise-360-Code-Block)

Vertonter Lernziel-Block: eine Sprecherin liest die vier Lernziele, auf der Bühne
läuft dazu ein Vorgang durch vier Stationen, und die vier Zeilen darunter färben
sich genau in dem Moment ein, in dem ihr Begriff fällt.

Eigenständige `index.html` (455 KB, Ton eingebettet) zum Hochladen als Code-Block
in Rise 360. Auslieferung: `AWA_Lernziele_Vertretung_Rise.zip` (index.html + OFL.txt).

## Die Tonspur gibt den Takt vor
Die Aufnahme ist 38,9 s lang. Die Einsätze sind **an den gemessenen Sprechpausen**
der Datei ausgerichtet, nicht geschätzt: drei Pausen von je rund einer Sekunde
trennen die vier Sätze, die kurzen Atempausen innerhalb der Sätze markieren die
Aufzählungen.

| Sekunde | gesprochen | Bühne | Schlagwort leuchtet |
|---|---|---|---|
| 0,3 | „Nach diesem Kurs …" | Rollen-Reihe erscheint, Schalter auf *direkt* | |
| 1,85 | „direkte …" | | direkte Vertretung |
| 2,75 | „… und indirekte Vertretung" | Schalter kippt, **Zollschuldner-Marke springt** zum Zollvertreter | indirekte Vertretung |
| 4,42 | „ordnest die Rollen von Anmelder," | die drei Rollen bekommen ihre Linie | |
| 6,73 | „… dem konkreten Fall zu" | Rahmen „konkreter Fall" legt sich um die Reihe | |
| 11,24 | „Du prüfst Auftragsdaten und Unterlagen" | zwei Belege nebeneinander | |
| 13,50 | „Widersprüche," | Mengenzeile leuchtet, Marke `≠` | Widersprüche |
| 14,76 | „Informationslücken" | leere Zeile, Marke `!` | Informationslücken |
| 16,05 | „und Zuordnungsprobleme" | fast gleicher Name, Marke `?` | Zuordnungsprobleme |
| 18,5 / 19,9 / 21,2 | „Vollmachten, Genehmigungen und Nachweise" | drei Belege legen sich hin | |
| 22,94 | „Du beurteilst, ob …" | das Prüfraster erscheint | |
| 23,11 / 24,10 / 24,85 / 25,80 | „geeignet, gültig, … zugeordnet … verfügbar" | Spalte für Spalte wird abgehakt, **eine bleibt offen** | geeignet / gültig / zugeordnet / verfügbar |
| 28,45 | „Und wenn Angaben fehlen" | der offene Punkt wird zum Auslöser | |
| 30,07 | „oder sich ändern" | die Menge ändert sich 420 → 380 | |
| 31,35 | „bestimmst du den zulässigen nächsten Schritt" | Weggabelung mit drei Wegen | |
| 33,00 | | ein Weg wird gewählt | |
| 34,07 / 35,72 / 36,58 / 37,54 | „Prüfgrundlage, Entscheidung, Status und Übergabe" | der Vermerk schreibt sich Feld für Feld | Prüfgrundlage / Entscheidung / Status / Übergabe |
| 38,30 | | Goldlinie, Vorgang übergeben | |

Alles steht im Array `CUE` in der index.html. Eine Zeile = ein Einsatz:

```js
{t:2.75, sw:1, ch:[0,1]}   // t Sekunde, sw Schalterstellung, ch [Lernziel, Schlagwort]
```

- `sc` wechselt die Szene, `st` setzt den Schritt innerhalb der Szene
- `g` macht ein Lernziel aktiv, `ch` lässt ein Schlagwort aufleuchten

Wird die Aufnahme neu gesprochen, müssen nur die `t`-Werte angepasst werden.
Die Pausen findet man mit
`ffmpeg -i datei.mp3 -af silencedetect=noise=-32dB:d=0.14 -f null -`.

## Ohne Ton funktioniert es auch
- Die vier Zeilen stehen von Anfang an lesbar da, nur ruhiger.
- Ein Klick auf eine Zeile oder auf eine Marke der Tonspur springt zu diesem
  Lernziel; die Bühne spielt die Station dazu.
- Lässt der Browser den Ton nicht zu, läuft die Geschichte auf einer eigenen Uhr
  weiter – die Bilder kommen trotzdem.
- Der gesprochene Text steht vollständig unter „Gesprochenen Text anzeigen".
- `prefers-reduced-motion`: die Einsätze schalten hart statt zu überblenden.

Autoplay gibt es nicht: Browser blockieren Ton ohne Klick, und in Rise wäre eine
von allein losredende Stimme ohnehin unangenehm. Der Vorspann startet erst, wenn
jemand „Lernziele anhören" drückt.

## Ton
Die Aufnahme liegt als Base64-MP3 direkt in der Datei – keine externen Dateien,
nichts kann beim Upload verloren gehen. Umgerechnet auf **56 kbit/s mono, 32 kHz**
(aus 192 kbit/s): für eine Sprechstimme hörbar unverändert, spart aber zwei Drittel.

```
ffmpeg -i Lernziele_VO.mp3 -ac 1 -ar 32000 -b:a 56k -codec:a libmp3lame vo.mp3
```

## Inhalt ändern
- `GOAL` – die vier Zeilen (Titel + Schlagworte)
- `CUE` – die Einsätze
- Die Szenen stehen als HTML in der Bühne (`.awa-sc` mit `data-s="1"` … `"4"`).
  `data-at="n"` lässt ein Element ab Schritt n auftreten, `data-k="n"` schaltet ab
  Schritt n eine Zustandsklasse (`data-ks`), `data-off="n"` nimmt sie wieder weg.
  So ist die Markierung einer Zeile ein Scheinwerfer und kein Stapel.

Die Szenen sind in HTML und CSS gebaut, nicht als SVG-Zeichnung: dadurch fließen
sie auf schmalen Blöcken sauber um (die Rollen-Reihe stapelt sich, das Prüfraster
bricht auf zwei Spalten).

## Erfundene Beispieldaten – bitte gegenlesen
Für die Bühne braucht es konkrete Zahlen. Frei erfunden und **vor dem Einsatz zu
prüfen** sind:

- Vorgang 24-0187, Nordhafen GmbH / Nordhafen Logistik, Spedition Mehlhorn
- 420 statt 380 Kartons, Fristen 12.03. / 14.03.
- die drei Wege „Rückfrage an den Auftraggeber", „Nachweis nachfordern",
  „Vorgang anhalten" und die Auszeichnung des mittleren als *zulässiger nächster
  Schritt* – das ist eine Fachaussage, die zum Lektionstext passen muss
- die Überschriften von Zeile 2 und 3 („Daten prüfen", „Unterlagen beurteilen");
  Zeile 1 und 4 stehen wörtlich so, wie sie geliefert wurden

## Prüfung
Mit Playwright bei 1000, 700 und 375 px sowie mit `prefers-reduced-motion`
durchgespielt: keine Konsolenfehler, kein horizontales Scrollen, alle 13
Schlagworte leuchten bis zum Ende, Szenenwechsel und Höhenwechsel sauber.
Die Bühne atmet mit der aktiven Szene (Desktop 196–220 px), die Blockhöhe
liegt bei rund 530 px im Ruhezustand.
