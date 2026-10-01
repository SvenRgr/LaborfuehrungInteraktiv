Innovative Interaktionskonzepte aus internationalen Museen und Science Centern bieten erprobte Vorlagen, um das Hochschullabor-Konzept von einem rein passiven Informationsguide zu einem immersiven, handlungsorientierten System weiterzuentwickeln.

---

## 1. Recherche: Reale Museumskonzepte und Referenzen

| Museum / Institution | Etabliertes Konzept | Kernmechanik |
| --- | --- | --- |
| **Cooper Hewitt, Smithsonian Design Museum** *(New York)* | **Phygital Token & Sammel-Logik** (*"The Pen"*) | Besucher berühren physische Tags an Exponaten. Diese werden in einem persönlichen Web-Profil gespeichert und können interaktiv auf Tischen manipuliert oder nach dem Besuch zu Hause vertieft werden. |
| **Exploratorium** *(San Francisco)* | **Inquiry-based Hands-on** (*"Predict – Observe – Explain"*) | Besucher werden nicht schrittweise instruiert, sondern stellen Hypothesen auf, verändern Stellgrößen an echten Apparaten und überprüfen Annahmen über Live-Visualisierungen. |
| **Deutsches Museum** *(München)* | **Web-AR-Röntgenblick & Explosionsansichten** | Über Browser-AR wird das unsichtbare Innenleben verschlossener Maschinen oder Schnittmodelle deckungsgleich über das reale Exponat projiziert. |
| **NEMO Science Museum** *(Amsterdam)* | **Geführte Forschungs-Parcours & Rollenwahl** | Besucher wählen ein narratives Profil (z. B. "Qualitätsprüfer", "Entwickler") und lösen abgestimmte Challenges an verschiedenen Stationen, deren Ergebnisse am Ende zusammengeführt werden. |
| **Ars Electronica Center** *(Linz)* | **Digital Twin & Live-Telemetrie** | Sensordaten physischer Systeme werden in Echtzeit in dynamische Dashboards und Raumprojektionen eingespeist, um Systemzustände sichtbar zu machen. |
| **MIT Museum / FabLab-Netzwerk** *(Cambridge, MA)* | **Digital Badging & Safety-Gates** | Nach dem Lösen eines interaktiven Sicherheits- und Funktionsquiz schaltet das System die Stromzufuhr oder Steuer-API einer Werkzeugmaschine digital frei. |

---

## 2. Evaluation: Übertragbarkeit auf das Hochschullabor

### A. Phygital Token & digitales Laborbuch (Cooper Hewitt / NEMO)

* **Transfer:** Statt QR-Codes nur als Informationsabruf zu nutzen, erhält jeder Besucher beim Start der Web-App eine eindeutige Session-ID (digitales Laborprotokoll). An jeder Station (Löten, Fahrrad, Roboter) werden Messwerte, absolvierte Schritte oder Fotos der eigenen Schaltung in diesem Profil gespeichert.
* **Mehrwert:** Besucher nehmen am Ende ein fertiges "digitales Versuchsprotokoll" mit nach Hause; Studierende können es direkt als Praktikumsnachweis exportieren.
* **Machbarkeit:** **Hoch**. Reine Frontend-/Backend-Logik (State-Management im LocalStorage oder einer Session-Datenbank), keine zusätzliche Hardware nötig.

### B. "Predict – Observe – Explain" statt starrer Anleitung (Exploratorium)

* **Transfer:** Bei der Fahrrad- und Vitaldatenstation nicht nur Messwerte anzeigen, sondern vor der Messung schätzen lassen: *"Welche Herzfrequenz erreichst du bei 150 Watt?"* Erst nach der Schätzung startet der Messlauf, gefolgt von einer automatischen Delta-Analyse.
* **Mehrwert:** Verwandelt reines "Ausprobieren" in didaktisches Begreifen.
* **Machbarkeit:** **Sehr hoch**. Erfordert lediglich eine Umgestaltung der UI-Flows in der Web-App.

### C. Safety-Gates & API-Freischaltung (MIT Badging)

* **Transfer:** Die Ansteuerung der Maschinen (z. B. Saugroboter fahren lassen, Lötstation anwerfen) ist standardmäßig gesperrt. Erst wenn der Nutzer ein kurzes 3-Fragen-Sicherheits- oder Funktionsquiz in der Web-App besteht, sendet das Backend das Freischaltsignal an die Geräte-API.
* **Mehrwert:** Löst das größte Problem von Hochschullaboren: **Sicherheit und Geräteschutz bei unbeaufsichtigtem Betrieb**.
* **Machbarkeit:** **Mittel**. Setzt eine Relais- oder REST/MQTT-Steuerung der Hardware voraus.

### D. WebXR / Browser-AR (Deutsches Museum)

* **Transfer:** Die Kamera erfasst ein Messgerät oder eine Platine und markiert Bauteilbezeichnungen, Messpunkte oder Gefahrenzonen direkt im Kamerabild.
* **Mehrwert:** Hoher Show-Effekt am Tag der offenen Tür; didaktisch wertvoll bei komplexen Schaltungen.
* **Machbarkeit:** **Mittel bis Schwer**. WebXR hat stark schwankende Kompatibilität über verschiedene Mobilgeräte und erfordert zuverlässiges Image-Tracking bei wechselnden Lichtverhältnissen.

---

## 3. Konkrete Handlungsempfehlungen zur Erweiterung

1. **Labor-Status-Dashboard als "Zentrale":**
Ein zentraler Monitor im Raum zeigt live den Status aller Stationen (z. B. "Station 2 belegt: Roboter fährt Parcours", "Gesamte getretene Watt-Leistung heute: 4,2 kWh"). Die Web-Apps der Nutzer kommunizieren via WebSockets mit diesem Dashboard.
2. **Modus-Trennung im CMS:**
Das Dozenten-Portal sollte denselben Raum in zwei Betriebsmodi schalten können:
* *Showroom-Modus (Tag der offenen Tür):* Kurze, spielerische 3-Minuten-Aufgaben, Highscores, Fokus auf Steuerung (Roboter) und Visualisierung (Fahrrad/Puls).
* *Praktikums-Modus (Reguläre Lehre):* Vollständiges Protokollwesen, Pflichtschritte, Messwert-Validierung, Export als PDF/Markdown.


3. **Hardware-Abstraktionsschicht (HAL):**
Um Wartungsaufwand zu minimieren, sollten Geräte über ein einheitliches IoT-Protokoll (z. B. MQTT via WebSockets) angebunden werden, statt für jedes Gerät individuelle proprietäre Web-APIs zu pflegen.