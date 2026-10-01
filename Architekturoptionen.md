# Architekturoptionen & Technologie-Evaluation

Dieses Dokument analysiert und vergleicht alternative Architekturoptionen für das Projekt **Interaktiver digitaler Labor-Guide**. Es dient als Entscheidungsgrundlage und technologische Nutzenanalyse (Trade-Off-Analyse) für die Ausarbeitung der Studienarbeit.

---

## 1. Übersicht der evaluierten Architekturmuster

### Referenz-Architektur: FastAPI Backend + React PWA (Single-Page Application)
* **Konzept:** Klare Trennung zwischen einem performanten, asynchronen Python-Backend (FastAPI) und einem reaktiven TypeScript/React-Frontend, das als Progressive Web App (PWA) sowohl auf mobilen Endgeräten als auch auf Desktop-Monitoren lauffähig ist.
* **Besonderheiten:** Hardware-Anbindung, Safety-Gates und Datenhaltung liegen gekapselt im Backend; das Frontend konzentriert sich auf Nutzerführung, Sensor-Visualisierung und Gamification.

---

### Alternative 1: Fullstack-Framework (z. B. Next.js / Remix / SvelteKit)
*Alles in einem TypeScript-Ökosystem (SSR, API-Routes, Frontend).*

* **Wie es funktioniert:** Eine einzige Codebasis. React läuft sowohl auf dem Server (Server-Side Rendering / Node.js API-Routen) als auch als PWA auf dem Client.
* **Vorteile:**
  * **End-to-End Type Safety:** Typendefinitionen (z. B. für Stationen, Quizfragen, Profile) können direkt zwischen Client und Server geteilt werden (z. B. via tRPC oder Server Actions).
  * **Einheitliche Sprache:** Vollständige Umsetzung in TypeScript ohne Sprachwechsel zwischen Frontend und Backend.
  * **Schnelles initiales Laden:** SSR rendert HTML direkt auf dem Server vor.
* **Nachteile / Herausforderungen im Laborkontext:**
  * **Hardware- & IoT-Anbindung in Node.js oft unzureichend:** Das Python-Ökosystem für Hardware (Sensoren, BLE, serielle Schnittstellen, OpenCV, KI-Bibliotheken) ist industrieller Standard und bietet weitaus breitere Bibliotheksunterstützung als Node.js.
  * Persistente WebSockets und langlaufende Hardware-Verbindungen sind in serverlosen Architekturen (wie Next.js oft betrieben wird) unnötig komplex zu verwalten.
* **Fazit:** Großartig für datengetriebene Webanwendungen, jedoch schwächer bei maschinen- und hardwarenaher Sensoranbindung.

---

### Alternative 2: Klassischer Monolith mit Server-Side-Rendering + HTMX (z. B. Django / Flask)
*Klassische Web-Architektur mit moderner HTML-over-the-Wire Interaktivität.*

* **Wie es funktioniert:** Python (Django oder Flask) rendert die HTML-Seiten serverseitig. HTMX tauscht per AJAX/WebSockets gezielt Fragmente des DOMs aus, ohne dass ein komplexes clientseitiges JavaScript-Framework benötigt wird.
* **Vorteile:**
  * **Geringe Einstiegshürde & minimaler JS-Code:** Keine aufwendige Node.js/NPM-Build-Toolchain erforderlich.
  * **Integrierte Admin-Oberfläche:** Bei Django ist ein vollwertiges Redaktionssystem für Dozierende (Stationen anlegen, Medien hochladen) standardmäßig enthalten (*Django Admin*).
  * Sehr gut für rein inhaltsbasierte CRUD-Seiten (Texte, Anleitungen, einfache Formulare).
* **Nachteile / Herausforderungen im Laborkontext:**
  * **Eingeschränkte Offline-Fähigkeit:** PWAs mit Service Workern, Offline-Caching und lokalem App-State lassen sich schwerer mit rein serverseitigem Rendering vereinbaren.
  * **Schwächen bei hochdynamischen Echtzeit-UIs:** Bei hochfrequentem Sensordaten-Streaming (z. B. Watt- und Trittfrequenz-Werte des Ergometers mehrfach pro Sekunde) oder clientseitigem Rendering (Canvas, Charts, WebXR/AR) stößt HTMX an seine Grenzen.
* **Fazit:** Sehr schnell prototypisierbar, aber für moderne, app-ähnliche Interaktivität und Telemetrie-Visualisierung zu starr.

---

### Alternative 3: Headless-CMS & Low-Code IoT-Plattform (z. B. Strapi + Node-RED + PWA)
*Trennung in fertiges Content-Management und visuelle IoT-Steuerung.*

* **Wie es funktioniert:**
  * **Strapi / PocketBase / Directus:** Fertige Headless-Lösung für Dozierenden-Verwaltung, Medien und Aufgaben per REST/GraphQL-API.
  * **Node-RED:** Visueller IoT-Broker zur Orchestrierung der Maschinen (Saugroboter, Ergometer, Sensoren) per Drag-and-Drop.
  * **Frontend:** Ein leichtes Web-Frontend (z. B. React/Vue) bindet beide Systeme an.
* **Vorteile:**
  * **Minimale Backend-Eigenentwicklung:** Content-Management und Hardware-Routing existieren weitgehend modular und vorkonfiguriert.
  * Niedrige Hürde für spätere Dozierende, die neue Sensoren ohne Programmierung in Node-RED verknüpfen können.
* **Nachteile / Herausforderungen im Laborkontext:**
  * **Geringe softwaretechnische Eigenleistung:** Der Schwerpunkt der Studienarbeit verschiebt sich von der Konzeption einer sauberen Software-Architektur hin zur Systemkonfiguration.
  * **Betriebsaufwand & Fragmentierung:** Mehrere unabhängige Dienste (CMS, Node-RED, MQTT-Broker) müssen parallel gehostet, authentifiziert und gewartet werden.
* **Fazit:** Pragmatisch in Produktionsumgebungen, für eine wissenschaftliche Studienarbeit mit Programmierfokus jedoch oft zu stark assemblierend.

---

### Alternative 4: Cross-Platform Native Mobile App (z. B. Flutter oder React Native)
*Kompilierte Applikation für mobile Betriebssysteme.*

* **Wie es funktioniert:** Eine gemeinsame Codebasis wird in native Android- und iOS-Apps kompiliert.
* **Vorteile:**
  * **Voller nativer Hardware-Zugriff:** Bluetooth Low Energy (BLE) für Pulsuhren und Fahrräder kann direkt vom Smartphone der Besucher aus angesprochen werden (Web-Bluetooth im Browser wird von iOS/Safari standardmäßig blockiert).
  * Höhere Rechenleistung und tiefere Integration für rechenintensive Augmented Reality (ARKit / ARCore).
* **Nachteile / Herausforderungen im Laborkontext:**
  * **Gravierende Einstiegshürde (K.o.-Kriterium):** Besucher und Laufkundschaft an Tagen der offenen Tür sind selten bereit, vor einer 15-minütigen Laborführung erst eine App aus dem App Store zu laden, Berechtigungen zu erteilen oder Zertifikate zu installieren.
  * **Desktop-Tauglichkeit:** Die Anforderung eines simultanen Desktop-Modus (z. B. für das zentrale Labor-Dashboard oder Dozenten-CMS) ist mit rein mobilen Frameworks deutlich aufwendiger umzusetzen als im Web.
* **Fazit:** Technisch überlegen bei direktem Bluetooth-Pairing, verfehlt jedoch die Zielgruppe durch unverhältnismäßig hohe Zugangsbarrieren.

---

## 2. Vergleichende Bewertungsmatrix

| Bewertungskriterium | **FastAPI + React PWA (Referenz)** | **Next.js (Fullstack TS)** | **Django + HTMX** | **Strapi + Node-RED** | **Flutter / Native App** |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Barrierefreiheit (QR-Code-Einstieg)** | **Sehr hoch (PWA)** | Sehr hoch (PWA) | Sehr hoch (Web) | Sehr hoch (PWA) | **Sehr gering (Store-Zwang)** |
| **Hardware- & IoT-Integration** | **Hervorragend (Python/MQTT)** | Befriedigend (Node.js) | Gut (Python) | Hervorragend (Node-RED) | Gut (Client-BLE) / Mittel (Server) |
| **Echtzeit-Telemetrie & Charts** | **Sehr gut (WebSockets)** | Gut | Eingeschränkt | Sehr gut | Hervorragend |
| **Desktop- & Mobil-Konsistenz** | **Sehr gut (Responsive)** | Sehr gut (Responsive) | Gut | Sehr gut (Responsive) | Befriedigend |
| **Wissenschaftliche Eigenleistung** | **Optimal** | Optimal | Gut | Gering (Konfigurationslastig) | Optimal |
| **Wartbarkeit / Komplexität** | **Ausgewogen (2 Services)** | Ausgewogen (1 Stack) | Sehr hoch (Monolith) | Komplex (Multi-Service) | Mittel |

---

## 3. Begründung der Architekturentscheidung

Die Kombination aus **FastAPI** und **React PWA** stellt für den interaktiven Labor-Guide die optimale Balance dar:

1. **Minimale Hürde für den Nutzer:** Der Zugang über einen simplen QR-Code-Scan im Standard-Smartphone-Browser ohne Installationsschritte ist essenziell für die Akzeptanz bei spontanen Führungen.
2. **Kapselung der Hardware:** Durch die Verlagerung von Sensor- und Geräteschnittstellen in das FastAPI-Backend (z. B. via MQTT / Hardware Abstraction Layer) werden browserseitige Restriktionen (wie die fehlende Web-BLE-Unterstützung auf iOS) umgangen.
3. **Didaktische & visuelle Flexibilität:** React erlaubt modular aufgebaute, flüssige Benutzeroberflächen für Quizzes, Schätzfragen und Live-Diagramme bei gleichzeitiger Wiederverwendbarkeit von Komponenten für das Dozenten-Portal und das zentrale Labor-Dashboard.

---

## 4. Relevanz von Asynchronität: Die hybride Stärke von FastAPI

Ein zentrales architektonisches Argument für FastAPI in dieser Studienarbeit ist dessen Fähigkeit, **synchrone und asynchrone Paradigmen nahtlos in einer Codebasis zu vereinen**. Ein rein synchrones Backend (wie Standard-Flask) würde bei diesem Anforderungsprofil an harte Grenzen stoßen.

### Wann reicht synchron (`def`)?
Klassische CRUD-Operationen sind kurzlebig (Bearbeitungszeit oft < 50 ms). FastAPI führt synchrone Handler automatisch in einem separaten Threadpool aus, ohne den Server zu blockieren:
* **Stationsabruf per QR-Code:** Laden von Texten, Beschreibungen, Audio- und Videolinks.
* **Quiz & Laborbuch:** Absenden von Antworten, Speichern von Multiple-Choice-Ergebnissen im Nutzerprofil.
* **Dozenten-CMS:** Anlegen neuer Stationen, Hochladen von Medien, Generieren von druckbaren QR-Codes.

### Wann ist asynchron (`async def`) zwingend nötig?
Hier würden synchrone Server Worker-Threads blockieren und bei mehreren gleichzeitigen Besuchern zum Stillstand führen:
* **WebSockets für Live-Telemetrie:** Dauerhafte Verbindungen für das Streaming hochfrequenter Daten (z. B. Watt- und Trittfrequenz-Werte des Ergometers, Puls-Messwerte) an Nutzer-Smartphones und den zentralen Labor-Monitor.
* **Hardware-I/O & Safety-Gates:** Zeitintensive Maschinen-Kommunikation (z. B. Warten auf Rückmeldungen von Saugrobotern, Ansteuerung von Relais oder MQTT-Antworten). Durch `await` blockiert das Backend während der Wartezeit keine anderen Nutzeranfragen.

> **Ergebnis für die Umsetzung:** FastAPI erlaubt es, die überwiegende Mehrheit der Standard-Endpunkte einfach und synchron zu halten, während gezielt nur dort auf `async`/WebSockets zurückgegriffen wird, wo Hardware-Events und Live-Streams es zwingend erfordern.

