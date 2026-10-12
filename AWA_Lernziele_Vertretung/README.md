# Lernziele „Vertretung im Zollverfahren" (Rise-360-Code-Block)

Vertonter Lernziel-Block. Auf dem Bildschirm stehen **nur die vier
gelieferten Zeilen**. Zeile 3 trägt die Vorlage „Dokumentation", damit sie auch
ohne Ton ableitbar bleibt; Zeile 4 steht ohne Vorlage. Eine Sprecherin liest die Lernziele,
und während sie spricht, tritt die passende Zeile nach vorn und die Begriffe
leuchten einzeln auf, genau in dem Moment, in dem sie gesprochen werden.

Eigenständige `index.html` (430 KB, Ton eingebettet) zum Hochladen als Code-Block
in Rise 360. Auslieferung: `AWA_Lernziele_Vertretung_Rise.zip` (index.html + OFL.txt).

## Was zu sehen ist
Links läuft eine **Route** mit vier Stationen, auf der ein neutrales Paket
unterwegs ist. Es hält an einer Station, solange deren Lernziel gelesen wird,
und fährt erst gegen Ende des Abschnitts weiter – so, wie ein Bote ausliefert.
Hinter ihm bleibt der zurückgelegte Weg als petrolfarbene Linie stehen.

- Die **aktive Zeile** wächst, ihre Ziffer wird groß, ein warmer Lichtstreifen
  läuft einmal darüber, der Grund hellt sich leicht auf, die Sperrung der
  Buchstaben läuft zusammen.
- Jedes **Schlüsselwort** bekommt im Augenblick des Sprechens eine feine
  Goldlinie und hebt sich kurz an.
- Gelesene Zeilen bleiben stehen, ihre Begriffe behalten eine stille graue Linie.
  **Gold liegt immer nur auf der Zeile, die gerade gesprochen wird.**
- Am Ende stehen alle vier Zeilen gleich ruhig nebeneinander: das fertige Bild.

Kein Bildmaterial, keine erfundenen Beispiele, keine Figuren – das Paket ist ein
reines Strichsymbol.

## Die Tonspur gibt den Takt vor
Die Aufnahme ist 38,9 s lang. Die Einsätze sind **an den gemessenen Sprechpausen**
der Datei ausgerichtet, nicht geschätzt.

| Sekunde | gesprochen | was passiert |
|---|---|---|
| 0,30 | „Nach diesem Kurs unterscheidest du …" | Zeile 1 tritt vor |
| 1,85 | „direkte" | *direkte* leuchtet auf |
| 2,75 | „und indirekte Vertretung" | *indirekte Vertretung* |
| 4,42 | „ordnest die Rollen …" | *Rollen zuordnen* |
| 11,24 | „Du prüfst Auftragsdaten …" | Zeile 2 tritt vor |
| 13,50 / 14,76 / 16,05 | die drei Funde | *Widersprüche* · *Informationslücken* · *Zuordnungsprobleme* |
| 18,50 | „Du beurteilst, ob …" | Zeile 3 tritt vor |
| 19,20 | „Vollmachten, Genehmigungen und Nachweise" | *Dokumentation* |
| 23,11 / 24,10 / 24,85 / 25,80 | die vier Fragen | *geeignet* · *gültig* · *zugeordnet* · *verfügbar* |
| 28,45 | „Und wenn Angaben fehlen …" | Zeile 4 tritt vor |
| 34,07 / 35,72 / 36,58 / 37,54 | der Vermerk | *Prüfgrundlage* · *Entscheidung* · *Status* · *Übergabe* |
| 38,80 | | alle vier Zeilen stehen gleich ruhig |

Alles steht in zwei Arrays oben in der index.html:

```js
L  = die vier Zeilen, Zeichen für Zeichen wie geliefert
CUE= {t:2.75, m:[0,2]}   // Sekunde, [Zeile, Schlüsselwort]
```

Wird die Aufnahme neu gesprochen, müssen nur die `t`-Werte angepasst werden.
Die Pausen findet man mit
`ffmpeg -i datei.mp3 -af silencedetect=noise=-32dB:d=0.14 -f null -`.

## Ohne Ton funktioniert es auch
- Die vier Zeilen stehen von Anfang an lesbar da, nur ruhiger.
- Ein Klick auf eine Zeile springt zu diesem Lernziel.
- Lässt der Browser den Ton nicht zu, läuft es auf einer eigenen Uhr weiter.
- Der gesprochene Text steht vollständig unter „Transkript".
- `prefers-reduced-motion`: die Einsätze schalten hart statt zu überblenden.

Autoplay gibt es nicht: Browser blockieren Ton ohne Klick, und in Rise wäre eine
von allein losredende Stimme ohnehin unangenehm.

## Ton
Base64-MP3 direkt in der Datei – keine externen Dateien, nichts kann beim Upload
verloren gehen. Umgerechnet auf **56 kbit/s mono, 32 kHz** (aus 192 kbit/s): für
eine Sprechstimme hörbar unverändert, spart zwei Drittel.

```
ffmpeg -i Lernziele_VO.mp3 -ac 1 -ar 32000 -b:a 56k -codec:a libmp3lame vo.mp3
```

## Prüfung
Mit Playwright bei 1000, 700 und 375 px sowie mit `prefers-reduced-motion`
durchgespielt: keine Konsolenfehler, kein horizontales Scrollen, alle 15
Schlüsselwörter leuchten bis zum Ende, am Schluss stehen alle vier Zeilen als
„gelesen". Blockhöhe rund 390 px (Desktop), 500 px (375 px breit).
