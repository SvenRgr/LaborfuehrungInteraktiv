## Projektkonzept: Interaktiver digitaler Labor-Guide (Web-App)

### 1. Ausgangssituation & Zielsetzung

An Hochschulen und Instituten stehen moderne Labore oft vor der Herausforderung, dass Dozierende bei Führungen, Tagen der offenen Tür oder für eigenständiges studentisches Arbeiten nicht durchgehend persönlich anwesend sein können.

Ziel der Studienarbeit ist die Konzeption und Realisierung einer browserbasierten Anwendung (Web-App), die Besucher, Studierende und Interessierte eigenständig, interaktiv und multimedial durch Universitätslabore führt. Sie ersetzt bzw. ergänzt die klassische Führung durch flexible Informationsvermittlung und aktive Einbindung der vor Ort vorhandenen Hardware.

---

### 2. Funktionale Kernmodule

Das System ist modular aufgebaut und staffelt sich in zwei wesentliche Interaktionsebenen sowie eine Verwaltungsebene:

#### A. Basis-Modus (Informations- & Guide-Ebene)

* **QR-Code-Trigger:** An Labortüren, Arbeitsstationen oder Exponaten angebrachte QR-Codes dienen als Einstiegspunkt. Nach dem Scan öffnet sich ohne Installationshürde die entsprechende Seite in der Web-App.
* **Multimediale Inhalte:**
* **Audioguide:** Wie im Museum erhalten Nutzer beim Betreten oder Auswählen einer Station standortbezogene Audio-Erklärungen.
* **Video & Bildmaterial:** Einblick in Prozesse, Experimente oder Demonstrationen.
* **Text & Grafiken:** Hintergrundwissen, Datenblätter und Sicherheitshinweise.



#### B. Aufgaben- & Projektmodus (Hands-on-Stationen)

* **Geführte Praxis-Aufgaben:** Besucher/Studierende können in der App konkrete Bastel- und Montageaufgaben auswählen (z. B. *„Löten eines LED-Tannenbaums“*).
* **Material- & Schritt-für-Schritt-Anleitung:** Die App verweist auf reale Lagerorte im Raum (z. B. beschriftete Schachteln/Schubladen für Bauteile) und führt sequenziell durch Vorbereitung, Messung und Aufbau.

#### C. Fortgeschrittener Interaktionsmodus (Hardware- & Spatial-Computing)

* **Direkte Maschinen- & Gerätesteuerung:**
* Ansteuerung programmierbarer Geräte über Schnittstellen/APIs (z. B. Fahrbefehle an Saugroboter oder Mini-Fahrzeuge direkt aus der Web-App).
* Anbindung von Sensoren und Messgeräten (z. B. Smart-Armbänder zur Live-Erfassung von Vitaldaten wie Blutdruck/Puls, Strom-/Spannungsmessgeräte).
* Interaktion mit Trainings- und Ergometer-Fahrrädern (Auslesen von Wattwerten, Kadenz, Geschwindigkeit).


* **AR- / VR-Integration:**
* Einbindung von Virtual Reality (z. B. VR-Brillen im Raum für immersive Rundgänge/Simulationen).
* Augmented Reality (AR) im Browser (z. B. über WebXR): Einblenden virtueller Messwerte, 3D-Modelle oder Schrittmarkierungen über der Kameraansicht des Smartphones.



#### D. Administrations- & CMS-Bereich (Dozenten-Portal)

* **Dynamische Raum- & Stationsverwaltung:** Dozierende können ohne Programmieraufwand neue Räume, Tische oder Stationen im Backend anlegen.
* **Content Management:** Upload und Zuordnung von Texten, Audio-Dateien, Videos und Schritt-für-Schritt-Anleitungen.
* **Automatisierte Code-Generierung:** Das System generiert auf Knopfdruck druckbare QR-Codes für jede neu angelegte Station oder Aufgabe.
* **Erweiterbarkeit für Code/Skripte:** Für tiefergehende Labore können Entwickler spezifische Steuerungs-Skripte oder API-Endpunkte für Sondergeräte hinterlegen.

---

### 3. Reale Einsatzbeispiele & Laborausstattung

| Laborbereich / Hardware | Interaktionsform in der App | Funktion / Mehrwert |
| --- | --- | --- |
| **Roboter & IoT-Geräte** (z. B. Staubsaugerroboter mit offener API) | Direkte Steuerung / API-Trigger | Besucher starten Fahrmuster oder testen Sensor-Reaktionen direkt vom Smartphone. |
| **Elektronik- & Lötbereich** (Platinen, Messgeräte) | Aufgabenbasierte Anleitung | Bauteillisten-Auswahl, Fachzuordnung im Raum, geführte Lötanleitung mit Messkontrollen. |
| **Messstation Vitaldaten** (Messarmbänder) | Live-Datenvisualisierung | Anzeige und Auswertung von Puls/Blutdruck direkt auf der Weboberfläche. |
| **Fahrrad-Station** (Watt- & Leistungsmessung) | Sensordaten-Streaming | Visualisierung der Tretleistung und physiologischer Parameter in Echtzeit. |
| **VR/AR-Ecke** (Headsets, WebXR) | Räumliche Projektion / Immersion | Virtuelle Einblendung nicht sichtbarer Prozesse oder interaktiver 3D-Objekte im Raum. |

---

Möchtest du als Nächstes die technische Architektur (Frontend, Backend, Datenbank und Schnittstellen) skizzieren oder direkt eine Gliederung für deine schriftliche Ausarbeitung erstellen?