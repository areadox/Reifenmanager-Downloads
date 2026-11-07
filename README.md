# Reifenmanager

Verwaltung von Kundenreifensätzen im Reifenhotel: Lagerplätze, Reifendaten, Sommer- und Winterreifen, Reifenwechsel,
Terminplaner und Einlagerungsbescheid zum Drucken – als Programm für Windows und Linux mit Weboberfläche, die im ganzen
Firmennetzwerk erreichbar ist.

## Download

Die aktuelle Version findest du unter **[Releases](../../releases/latest)** (rechts auf dieser Seite).
Der Reifenmanager ist noch in Entwicklung, daher tragen die Versionen eine **0.x**-Nummer (z. B. 0.3.14).
Wer noch die frühere Python-Version (2.x) oder eine Testversion 3.0.x installiert hat: einfach das aktuelle Setup
installieren – die Daten werden übernommen; ab dann kommen Updates wieder automatisch.
Dort liegen drei Dateien:

| Datei | Verwendung |
|---|---|
| `Reifenmanager-Setup-<Version>.exe` | **Windows, empfohlen.** Installer mit Startmenü-Eintrag, Deinstallation über die Windows-Einstellungen und Update-Funktion im Programm |
| `Reifenmanager-portable.exe` | Windows: einzelne Datei ohne Installation (z. B. für einen USB-Stick) |
| `Reifenmanager-linux-x86_64-<Version>.tar.gz` | **Linux** (64 Bit): Programmfenster und Server ohne Fenster, siehe [Linux](#linux) |

> **Hinweis zu Windows SmartScreen:** Die Programme sind nicht digital signiert. Beim ersten Start meldet Windows evtl.
> „Der Computer wurde durch Windows geschützt". Klicke auf **Weitere Informationen → Trotzdem ausführen**.
> Meldet Microsoft Defender einen Fund wie *Trojan:Win32/Bearfoos.A!ml*, siehe [Häufige Fragen](#häufige-fragen).

## Linux

Das Paket `Reifenmanager-linux-x86_64-<Version>.tar.gz` entpacken (`tar xzf Reifenmanager-linux-x86_64-*.tar.gz`). Es enthält:

| Datei | Verwendung |
|---|---|
| `reifenmanager` | Programmfenster wie unter Windows – starten mit `./reifenmanager`. Benötigt eine grafische Oberfläche und ein aktuelles System (z. B. Ubuntu 22.04, Debian 12, Linux Mint 21 oder neuer) |
| `reifenmanager-server` | ohne Fenster, für Server, NAS oder Mini-PC; läuft auf jedem 64-Bit-Linux: `./reifenmanager-server --port 8080 --passwort GEHEIM` (weitere Optionen mit `--help`) |
| `reifenmanager.service` | Vorlage für einen systemd-Dienst, der den Server beim Hochfahren startet (Anleitung in der Datei) |
| `LIESMICH.txt` | Kurzanleitung |

Die Daten liegen unter `~/.local/share/reifenmanager` (beim Server mit `--daten` wählbar) und sind mit der Windows-Version
austauschbar – `reifenlager.db` und `lizenz.txt` einfach kopieren. Damit andere Geräte zugreifen können, den Port in der
Firewall freigeben (z. B. `sudo ufw allow 8080/tcp`). Autostart und automatische Installation von Updates gibt es nur unter
Windows; unter Linux öffnet „Jetzt aktualisieren" die Download-Seite (neues Paket entpacken, Dateien ersetzen – die Daten bleiben).

## Erste Schritte

1. Setup ausführen und dem Assistenten folgen (ohne Administratorrechte für den eigenen Benutzer, oder „für alle Benutzer").
2. Das Programmfenster zeigt **„Server läuft"** und die **Adressen im Netzwerk**, z. B. `http://192.168.1.20:8080`.
   Diese Adresse gibst du auf jedem Rechner, Tablet oder Handy im Netzwerk in den Browser ein.
3. Im Programmfenster legst du ein Passwort für den **Hauptzugang** fest (voreingestellter Name `reifen`) und richtest
   danach im Browser unter **Admin → Benutzer & Rechte** für jeden Mitarbeiter einen eigenen Zugang ein.
   Ohne Passwort und ohne Benutzer kann jeder im Netzwerk die Daten sehen und ändern.
   Der Zugriff ist unverschlüsselt (HTTP) – bitte nur im internen Netz verwenden.
4. Beim ersten Start fragt die Windows-Firewall, ob der Zugriff im **privaten Netzwerk** erlaubt sein soll – bitte erlauben,
   sonst erreichen andere Geräte die Seite nicht.
5. Unter **Admin** trägst du die Kopfzeile deiner Firma ein und legst unter **Lagerorte** fest, welche Plätze es gibt
   (z. B. Platz 1–50 = „Halle A, Regal 1").
6. Mit **+ Einlagern** erfasst du den ersten Kunden.

## Funktionen

- Kunde, Telefon, Kennzeichen, Fahrzeug
- bis zu **zwei Reifensätze je Platz** (z. B. 4 Winter + 4 Sommer) mit Hersteller, Modell, Felge, **Profiltiefe je Reifen**
  und **Reifengröße/Index je Achse** – bei Mischbereifung (vorne andere Größe als hinten) einfach die Hinterachse ausfüllen
- **Anzahl je Satz:** 1, 2, 3, 4 oder **2×2** (2 vorne + 2 hinten)
- **Status je Satz:** im Lager oder am Fahrzeug – im Lagerplan auf einen Blick sichtbar (❄ Winter, ☀ Sommer).
  Es kann immer nur **ein Satz am Fahrzeug** sein.
- **Reifenwechsel:** Kunde, Kennzeichen oder Platz suchen, Satz wählen – der bisher montierte Satz wird automatisch
  als eingelagert geführt. Dabei fragt das Programm die **Profiltiefe des Satzes ab, der ins Lager kommt**,
  damit die Werte in der Datenbank immer aktuell sind. Außerdem siehst du die **Satzdaten** (Hersteller, Modell, Größe,
  Index, Felge, Anzahl) beider Sätze und kannst sie gleich **berichtigen**. Je Reifen gibt es einen Haken **„erneuern“** –
  so markierte Reifen erscheinen auf der **Meldeliste**, auch wenn die Profiltiefe noch reicht (abwählbar unter
  „Bearbeiten“, z. B. nachdem der Reifen ersetzt wurde).
  Ist bisher **nur ein Satz** gespeichert, fragt der Reifenwechsel nach dem **Satz, der vom Fahrzeug kommt**: welcher
  Satz Winter- und welcher Sommerreifen ist, dazu Hersteller, Größe, Profiltiefe usw. – er wird dann gleich als zweiter
  Satz eingelagert. Wird kein Satz eingelagert (Kunde nimmt die Reifen mit), einfach „Kein Satz kommt ins Lager“ wählen.
- **Terminplaner:** Termine je Tag mit Wochenübersicht, für eingelagerte Kunden (Platznummer) oder Laufkunden.
  Der passende Satz wird automatisch gewählt (der im Lager liegt bzw. nach Jahreszeit) oder frei ausgewählt.
  Je Termin gibt es Haken für **Winterreifen wuchten/waschen** und **Sommerreifen wuchten/waschen**.
- **Tagesliste und Holliste zum Drucken** (A4, gleicher Aufbau): Lagerplatz, Kennzeichen, Name, Reifengröße,
  Waschen und Wuchten mit Kästchen zum Abhaken. Die **Tagesliste** ist nach Uhrzeit sortiert und enthält alle Termine;
  die **Holliste** ist nach Lagerplatz sortiert und enthält nur Kunden mit eingelagerten Reifen – zum Holen in einem Gang.
- Lagerplan, Liste und Suche (Kunde, Kennzeichen, Dimension, Lagerort …), CSV-Export für Excel
- **CSV-Import** im Programmfenster: Datei hineinziehen, Spalten werden automatisch erkannt – CSV-Export zurückspielen
  oder Kunden aus dem DMS bzw. einer Excel-Tabelle übernehmen
- **Einlagerungsbescheid** zum Drucken mit eigener Firmen-Kopfzeile
- **+ Einlagern** mit Suche nach bestehenden Sätzen (Platznummer, Kennzeichen oder Kunde) – mit Knöpfen zum Öffnen,
  Bearbeiten, Reifenwechsel und Termin; tippt man eine belegte Platznummer ein, zeigt das Formular sofort, wer dort liegt
- **Meldeliste mit Saison-Ablauf:** alle Reifensätze, bei denen ein Reifen die Mindestprofiltiefe erreicht oder
  unterschreitet (getrennt einstellbar für Sommer, Winter, Ganzjahr; Standard 3 / 4 / 4 mm) oder zum Erneuern markiert ist.
  Vor der neuen Saison arbeitest du sie Schritt für Schritt ab – jede Stufe hat ihre eigene Liste:
  1. **Anrufen** (druckbare **Anrufliste** mit Telefon und Platz für Notizen): Ergebnis eintragen – *will neue Reifen*,
     *fährt noch diese Saison* (verschwindet bis zur nächsten Saison und kommt dann von selbst wieder), *nicht erreicht*
     (mit „wieder anrufen am“) oder *will nicht*
  2. **Bestellen:** Hersteller, Modell, Größe/Index, Anzahl, Lieferant, Bestellnummer, Preis – die **Bestellliste** fasst
     gleiche Reifen zusammen (z. B. „205/55 R16 91H – 3 Sätze, 12 Stück“), dann „Bestellt“
  3. **Lieferung offen:** „Geliefert“ anklicken, sobald die Reifen da sind
  4. **Vormontieren** (druckbare Liste mit Lagerplatz): nach dem Vormontieren werden die Satzdaten automatisch auf die
     neuen Reifen umgestellt
  5. **Termin vereinbaren:** Termin direkt aus der Liste anlegen
  6. **Erledigt:** passiert automatisch beim Reifenwechsel
  Filter nach Saison (z. B. im Herbst nur Winterreifen) und „nur im Lager“; die Platzseite zeigt, wo ein Satz gerade steht
- **Startseite „Heute“:** Termine heute, wie viele Kunden anzurufen sind, was zu bestellen, zu liefern, vorzumontieren
  ist, und überlagerte Sätze – jeweils mit einem Klick zur Liste
- **Archiv:** „Platz freigeben“ löscht den Kunden nicht mehr, sondern legt ihn mit seinen Reifensätzen ins **Archiv**
  (Menü Listen → Archiv). Kommt er wieder, findet ihn die Suche auf „+ Einlagern“ – mit „Zurückholen“ liegt er wieder
  auf einem freien Platz
- **Überlagerung:** Sätze, die länger als eine Frist (Standard 12 Monate) oder seit einem frei wählbaren Datum im Lager
  liegen, ohne gewechselt worden zu sein – mit Dauer, druckbar
- **Benutzer & Rechte:** eigener Zugang für jeden Mitarbeiter mit Vorlagen **Administrator**, **Mitarbeiter**
  (einlagern, Reifenwechsel, Termine, Listen) und **Nur lesen** – oder einzelne Rechte frei anhaken
  (Einlagern, Platz freigeben, Reifenwechsel, Termine, Listen, Verlauf, CSV-Export, Admin). Anmeldung über eine Anmeldeseite,
  auf Wunsch „angemeldet bleiben“ (30 Tage); jeder kann sein Passwort unter **Mein Konto** ändern
- **Übersichtliche Menüleiste:** Lagerplan, Liste, Reifenwechsel, Termine, Aufklappmenüs **Listen** und **Admin**,
  **+ Einlagern**, Suche und Benutzermenü – jeder sieht nur, was er darf; auf dem Handy hinter dem Knopf ☰
- **Admin:** Kopfzeile, Mindestprofiltiefen, Frist für die Überlagerung sowie Lagerorte, Lizenz, Verlauf und CSV-Export
- **Änderungsverlauf** (was wann **von wem** geändert wurde, filterbar nach Benutzer) und **tägliche automatische Sicherung**
- Update-Hinweis im Programm mit Installation per Klick

## Community-Version und Firmenlizenz

- **Community-Version:** kostenlos, bis zu **100 Lagerplätze**.
- **Firmenlizenz:** für mehr Plätze. Du erhältst einen Lizenzschlüssel und trägst ihn im Programmfenster unter
  **„Lizenz eintragen"** (oder in der Weboberfläche unter **Lizenz**) ein. Danach gilt die lizenzierte Platzanzahl.
- Läuft eine befristete Lizenz ab, bleiben alle Daten erhalten. Das Programm läuft dann als Community-Version: Plätze oberhalb von 100 sind **gesperrt**
  (nicht mehr sichtbar oder bearbeitbar); ihre Daten stehen weiter im **CSV-Export**. Mit einer neuen Lizenz sind sie sofort wieder nutzbar.
  Rechtzeitig vor Ablauf erinnert das Programm an die Verlängerung.

## Updates

Das Programm sucht beim Start nach einer neuen Version und meldet sie im Fenster und in der Weboberfläche.
Mit **„Jetzt aktualisieren"** wird der Installer geladen und die neue Version installiert; deine Daten bleiben erhalten.
(Bei der portablen Version und unter Linux öffnet der Knopf diese Download-Seite.)

## Häufige Fragen

**Die Seite ist von einem anderen Gerät nicht erreichbar.**
Prüfe, dass das Programm auf dem Server-PC läuft („Server läuft"), und dass du die angezeigte IP-Adresse mit Port benutzt
(nicht `localhost`). Außerdem muss die Windows-Firewall den Zugriff im privaten Netzwerk erlauben.

**Der Port 8080 ist belegt.**
Im Programmfenster einen anderen Port eintragen und neu starten.

**Wo liegen meine Daten?**
In `%LOCALAPPDATA%\Reifenmanager` (Datenbank, Einstellungen, Log). Dort legt das Programm täglich eine Sicherung im Ordner
`sicherungen` ab. Liegt neben der `.exe` eine Datei `portable.txt`, werden die Daten stattdessen im Ordner der `.exe` gespeichert.

**Wie spiele ich eine Sicherung zurück?**
Programm beenden, die gewünschte Datei aus `sicherungen` als `reifenlager.db` in den Datenordner kopieren, Programm starten.

**Ich habe neue Rechner / will umziehen.**
Datenordner (mindestens `reifenlager.db`) auf den neuen Rechner kopieren, Programm installieren und starten.
Die Lizenz (`lizenz.txt`) liegt im selben Ordner.

**Wie importiere ich Daten aus einer CSV-Datei?**
Im Programmfenster unter **CSV-Import** die Datei mit **„Durchsuchen …"** wählen oder einfach ins Fenster ziehen
(alternativ `Reifenmanager.exe --import datei.csv`). Das Programm liest sie sofort ein:

- Zeichensatz (UTF-8 oder Windows/ANSI) und Trennzeichen (Semikolon, Komma, Tabulator) werden erkannt; die erste Zeile
  muss die Spaltenüberschriften enthalten.
- Die Spalten werden **automatisch zugeordnet** (z. B. *Lagerplatz* → Platz, *Name* → Kunde, *Reifengröße* → Dimension,
  *Reifengröße hinten* / *Index hinten* → Hinterachse, Anzahl auch als „2x2",
  *Marke* → Hersteller). Unter **„Zuordnung der Spalten"** lässt sich das ändern; fehlt Platz oder Kunde, klappt sie von selbst auf.
- Eine **Vorschau** zeigt die ersten Zeilen, darunter steht, wie viele Plätze neu angelegt werden und welche Zeilen Fehler
  haben – das wird bei jeder Änderung neu berechnet, es wird noch nichts geändert.
- Mit **„… Plätze importieren"** werden die Daten in einem Schritt übernommen (bei einem Fehler wird nichts geändert);
  vorher legt das Programm automatisch eine Sicherung im Ordner `sicherungen` an. Danach steht das Ergebnis im Fenster; **„OK"**
  schließt die Meldung, und die Karte sieht wieder aus wie vor dem Import.
- Belegte Plätze werden übersprungen, außer du setzt den Haken **„Belegte Plätze überschreiben"**.

Eine Zeile je Reifensatz; zwei Zeilen mit gleichem Platz ergeben einen Kunden mit Sommer- und Winterreifen. Am einfachsten:
das Format des **CSV-Exports** verwenden.

**Woher weiß das Programm, wie lange ein Satz im Lager liegt?**
Jeder Satz merkt sich das Datum, an dem er ins Lager kam (beim Einlagern, beim Reifenwechsel oder wenn er wieder
eingelagert wird); es steht auf der Platzseite unter „Im Lager seit". Bei Daten aus älteren Versionen wird es beim ersten
Start aus dem Verlauf ermittelt, sonst gilt das Einlagerungsdatum des Kunden.

**Was bedeutet „am Fahrzeug"?**
Der Kunde fährt gerade mit diesem Satz. Der Platz bleibt für ihn reserviert; der andere Satz kann im Lager liegen.
Es kann nur ein Satz am Fahrzeug sein – beim Reifenwechsel stellt das Programm den Status automatisch richtig.

**Wie richte ich Benutzer ein und was dürfen sie?**
Unter **Admin → Benutzer & Rechte** Name und Passwort eingeben, eine Vorlage wählen (oder Rechte einzeln anhaken) und
**„Benutzer anlegen“**. Ansehen und Drucken (Lagerplan, Liste, Platzseiten, Termine, Tagesliste) darf jeder angemeldete
Benutzer; alles andere regeln die Rechte – Knöpfe ohne Recht werden gar nicht erst angezeigt. Benutzer lassen sich
sperren, ändern oder löschen; der letzte Administrator kann sich nicht selbst aussperren.

**Abmelden** geht über das Benutzermenü oben rechts – auf jedem Gerät, auch am PC, auf dem das Programm läuft.

**Ich habe mein Passwort vergessen.**
Ein Administrator setzt es unter **Benutzer & Rechte** neu. Hat niemand mehr Zugang, im Programmfenster auf dem
Server-PC ein Passwort für den **Hauptzugang** setzen – damit meldest du dich immer als Administrator an.

**Ein Kunde holt seine Reifen ab und kommt nicht mehr – was tun?**
Auf der Platzseite **„Platz freigeben (Archiv)“**. Der Platz ist dann frei, Kunde und Reifensätze liegen im **Archiv**
und lassen sich jederzeit zurückholen. Endgültig löschen kann nur ein Administrator.

**Wie läuft die Vorbereitung auf die neue Saison?**
**Listen → Meldeliste / Saison**, Saison wählen (z. B. Winter) und die Reiter von links nach rechts abarbeiten:
Anrufliste drucken und telefonieren, Bestellungen eintragen und mit der **Bestellliste** gesammelt bestellen, Lieferungen
abhaken, vormontieren, Termine vereinbaren. Die Startseite zeigt unter **„Heute“**, was in jeder Stufe offen ist.

**Wie mache ich einen Reifenwechsel?**
Menüpunkt **Reifenwechsel** (oder der Knopf auf der Platzseite bzw. im Terminplaner): Kunde suchen, auf
z. B. „❄ Winter ans Fahrzeug, ☀ Sommer einlagern" klicken, die gemessene Profiltiefe des eingelagerten Satzes eintragen,
bei Bedarf Satzdaten berichtigen und Reifen zum **Erneuern** anhaken, dann **„Reifenwechsel speichern"**. Danach kannst du direkt den Einlagerungsbescheid drucken.
Offene Termine des Kunden bis heute werden dabei automatisch als erledigt markiert.

**Wie plane ich Termine und drucke die Tagesliste?**
Menüpunkt **Termine**: Tag wählen, unter „Neuer Termin" Datum, Uhrzeit und Lagerplatz eintragen (oder auf der Platzseite
**„Termin planen"**) und bei Bedarf die Haken für Waschen und Wuchten setzen. Mit **„Tagesliste drucken"** öffnet sich
die Tagesliste (nach Uhrzeit) im selben Browsertab; oben kannst du zur **Holliste** (nach Lagerplatz) umschalten.
**„Drucken"** öffnet den Druckdialog, **„Zurück"** führt wieder zur Terminübersicht.

**Microsoft Defender meldet „Trojan:Win32/Bearfoos.A!ml" (oder ähnlich).**
Das Kürzel **„!ml"** bedeutet, dass Defender die Datei nur per *maschinellem Lernen* als verdächtig einschätzt – es ist
keine Erkennung eines bekannten Schädlings. Neue, nicht digital signierte Programme werden so häufig fälschlich gemeldet.
Lade das Programm nur von dieser Seite herunter. Wenn du der Datei vertraust:
**Windows-Sicherheit → Viren- & Bedrohungsschutz → Schutzverlauf**, den Eintrag öffnen und **„Zulassen"** bzw.
**„Wiederherstellen"** wählen. Bitte melde uns den Fund mit Versionsnummer, damit wir ihn bei Microsoft klären können.

## Lizenz und Haftung

Alle Rechte vorbehalten. Die Community-Version darf kostenlos genutzt werden; weitergehende Nutzung benötigt einen Lizenzschlüssel.
Die Software wird ohne Gewährleistung „wie besehen" bereitgestellt. Sichere deine Daten regelmäßig zusätzlich außerhalb des Rechners.

Der Reifenmanager enthält Open-Source-Bibliotheken anderer Entwickler (freizügige Lizenzen wie MIT, Apache-2.0, BSD).
Ihre Lizenzhinweise findest du im Programmfenster unter **Lizenz → „Lizenzen Dritter"**, in der Weboberfläche über den Link
**„Lizenzen Dritter"** unten auf jeder Seite, im Startmenü (Setup) und als `LIZENZEN-DRITTER.html` im Linux-Paket.
