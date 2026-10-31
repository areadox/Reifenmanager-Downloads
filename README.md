# Reifenmanager

Verwaltung von Kundenreifensätzen im Reifenhotel: Lagerplätze, Reifendaten, Sommer- und Winterreifen,
Einlagerungsbescheid zum Drucken – als Windows-Programm mit Weboberfläche, die im ganzen Firmennetzwerk erreichbar ist.

## Download

Die aktuelle Version findest du unter **[Releases](../../releases/latest)** (rechts auf dieser Seite).
Dort liegen zwei Dateien:

| Datei | Verwendung |
|---|---|
| `Reifenmanager-Setup-<Version>.exe` | **Empfohlen.** Installer mit Startmenü-Eintrag, Deinstallation über die Windows-Einstellungen und Update-Funktion im Programm |
| `Reifenmanager-portable.exe` | Einzelne Datei ohne Installation (z. B. für einen USB-Stick) |

> **Hinweis zu Windows SmartScreen:** Die Programme sind nicht digital signiert. Beim ersten Start meldet Windows evtl.
> „Der Computer wurde durch Windows geschützt". Klicke auf **Weitere Informationen → Trotzdem ausführen**.

## Erste Schritte

1. Setup ausführen und dem Assistenten folgen (ohne Administratorrechte für den eigenen Benutzer, oder „für alle Benutzer").
2. Das Programmfenster zeigt **„Server läuft"** und die **Adressen im Netzwerk**, z. B. `http://192.168.1.20:8080`.
   Diese Adresse gibst du auf jedem Rechner, Tablet oder Handy im Netzwerk in den Browser ein.
3. Ein **Passwort** setzt du im Programmfenster (Benutzername: `reifen`). Ohne Passwort kann jeder im Netzwerk die Daten sehen.
   Der Zugriff ist unverschlüsselt (HTTP) – bitte nur im internen Netz verwenden.
4. Beim ersten Start fragt die Windows-Firewall, ob der Zugriff im **privaten Netzwerk** erlaubt sein soll – bitte erlauben,
   sonst erreichen andere Geräte die Seite nicht.
5. Unter **Lagerorte** legst du fest, welche Plätze es gibt (z. B. Platz 1–50 = „Halle A, Regal 1").
6. Mit **+ Einlagern** erfasst du den ersten Kunden.

## Funktionen

- Kunde, Telefon, Kennzeichen, Fahrzeug
- bis zu **zwei Reifensätze je Platz** (z. B. 4 Winter + 4 Sommer) mit Hersteller, Modell, Dimension, Index,
  Felge, Anzahl und **Profiltiefe je Reifen**
- **Status je Satz:** im Lager oder am Fahrzeug – im Lagerplan auf einen Blick sichtbar (❄ Winter, ☀ Sommer)
- Lagerplan, Liste und Suche (Kunde, Kennzeichen, Dimension, Lagerort …), CSV-Export für Excel
- **Einlagerungsbescheid** zum Drucken mit eigener Firmen-Kopfzeile
- **Änderungsverlauf** (was wann geändert wurde) und **tägliche automatische Sicherung**
- Update-Hinweis im Programm mit Installation per Klick

## Community-Version und Firmenlizenz

- **Community-Version:** kostenlos, bis zu **100 Lagerplätze**.
- **Firmenlizenz:** für mehr Plätze. Du erhältst einen Lizenzschlüssel und trägst ihn im Programmfenster unter
  **„Lizenz eintragen"** (oder in der Weboberfläche unter **Lizenz**) ein. Danach gilt die lizenzierte Platzanzahl.
- Läuft eine befristete Lizenz ab, bleiben alle Daten erhalten; neue Einlagerungen sind dann nur noch im Rahmen der Community-Grenze möglich.

## Updates

Das Programm sucht beim Start nach einer neuen Version und meldet sie im Fenster und in der Weboberfläche.
Mit **„Jetzt aktualisieren"** wird der Installer geladen und die neue Version installiert; deine Daten bleiben erhalten.
(Bei der portablen Version öffnet der Knopf diese Download-Seite.)

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

**Was bedeutet „am Fahrzeug"?**
Der Kunde fährt gerade mit diesem Satz. Der Platz bleibt für ihn reserviert; der andere Satz kann im Lager liegen.

## Lizenz und Haftung

Alle Rechte vorbehalten. Die Community-Version darf kostenlos genutzt werden; weitergehende Nutzung benötigt einen Lizenzschlüssel.
Die Software wird ohne Gewährleistung „wie besehen" bereitgestellt. Sichere deine Daten regelmäßig zusätzlich außerhalb des Rechners.
