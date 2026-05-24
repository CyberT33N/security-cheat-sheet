
### 3.4 REQ-004: Vollständige Administratorfunktionen in GravityZone
[INTENT: SPEZIFIKATION]

**Typ:** ANFORDERUNG

**Beschreibung:**  
Diese Einheit dokumentiert die vollständigen im Kontext bestätigten Admin-Möglichkeiten auf verwalteten Client-Rechnern.

#### 3.4.1 Was ein Administrator **sehen** kann
**Standard-Inventar / Endpoint-Details:**
- Name
- `FQDN`
- IP-Adresse
- Betriebssystem / OS-Version
- Endpoint-Typ
- `Last seen`
- Online-/Offline-Status
- Policy-Zuordnung
- Modulstatus
- Label / Tag

**Optional / policyabhängig:**
- eingeloggte Benutzer
- Login-Zeitpunkt
- Login-Methode lokal / remote

**Mit weiteren Modulen / Inventaren:**
- installierte und entdeckte Anwendungen
- Prozesse
- Version, Publisher, Pfad / Location
- Patch-Status
- Quarantäne-Objekte
- Policy-Compliance / Audit-/Protection-Reports
- Incident-Kontext / EDR-/XDR-Daten

**Quellen:**  
[Viewing endpoint details](https://www.bitdefender.com/business/support/en/77212-155147-viewing-endpoint-details.html), [Application inventory](https://www.bitdefender.com/business/support/en/77212-155236-application-inventory.html), [Report types](https://www.bitdefender.com/business/support/en/77212-88549-report-types.html)

#### 3.4.2 Was ein Administrator **kontrollieren / sperren** kann
**Policies / Schutzmodule:**
- Policies zuweisen
- Module aktivieren / deaktivieren
- Exclusions setzen
- Agenten reconfigurieren

**Web / Internet / Netzwerk:**
- Webseiten / Kategorien / URLs blockieren (`Web Access Control`)
- App-spezifische Netzwerkregeln setzen (`Firewall`)
- Netzattacken reporten oder blockieren (`Network Attack Defense`)
- Endpoint isolieren (`Isolate endpoint`)

**Apps / Prozesse / Geräte:**
- unbekannte oder unerwünschte Anwendungen blockieren (`Application Control`, `Application Blacklisting`)
- Geräteklassen erlauben / blockieren / auf `Read-Only` setzen (`Device Control`)

**Verschlüsselung / Recovery:**
- Vollverschlüsselung erzwingen / aufheben
- lokale Benutzeraktionen zur Verschlüsselung unterbinden, wenn zentral verwaltet
- Recovery Keys auslesen

**Patch- und Risikosteuerung:**
- Patches inventarisieren und installieren
- Risk Scans planen / ausführen
- Risk Management konfigurieren

**Quellen:**  
[Security management](https://www.bitdefender.com/business/support/en/77209-77398-security-management.html), [Content Control](https://www.bitdefender.com/business/support/en/77209-342965-content-control.html), [Rules](https://www.bitdefender.com/business/support/en/77209-342962-rules.html), [Device Control](https://www.bitdefender.com/business/support/en/77209-376305-device-control.html), [Managing permission rules and exclusions](https://www.bitdefender.com/business/support/en/77212-342971-device-control-configuration.html), [Full Disk Encryption](https://www.bitdefender.com/business/support/en/77212-376312-full-disk-encryption.html), [Using Recovery Manager for encrypted volumes](https://www.bitdefender.com/business/support/en/77212-155203-using-recovery-manager-for-encrypted-volumes.html)

#### 3.4.3 Was ein Administrator **aktiv ausführen** kann
**Endpoint-Tasks / Aktionen:**
- Malware scan
- IOC scan
- Risk scan
- Install agent
- Uninstall agent
- Update agent
- Upgrade agent
- Reconfigure agent
- Repair agent
- Restart machine
- Run network discovery
- Run applications discovery
- Patch Scan / Install / Uninstall
- Isolate endpoint / Remove from isolation
- Resume endpoint protection
- Submit to Sandbox Analyzer
- Quarantine restore / delete / empty

**Quellen:**  
[Using actions](https://www.bitdefender.com/business/support/en/77209-155163-running-tasks-on-endpoints.html), [Viewing and managing tasks](https://www.bitdefender.com/business/support/en/77212-155162-viewing-and-managing-tasks.html), [Patch tasks](https://www.bitdefender.com/business/support/en/77212-155238-patch-tasks.html), [Managing the quarantine](https://www.bitdefender.com/business/support/en/77212-343013-quarantine.html)

#### 3.4.4 Dateisystem- und Dateisicht
**Wichtige Trennung:**

**Nicht automatisch als Explorer/Finder:**
- Standard-GravityZone zeigt nicht einfach blind den gesamten Dateibaum wie ein Remote-Desktop-Dateimanager.

**Aber dateibezogene Sicht und Eingriffe sind vorhanden über:**
- Quarantäne-Ansicht
- Application Inventory mit Dateipfaden
- Patch-/Risk-/Event-Daten
- `Live Search` (Osquery-basierte Abfragen zu Dateien, Hashes, Modifikationen)
- `Remote Connection`
- `Remote Shell` (wenn verfügbar)

#### 3.4.5 `Remote Connection`, `Live Search`, `Remote Shell`
**`Live Search`:**
- Echtzeit-Forensik per Osquery
- Abfragen zu Prozessen, Verbindungen, Hashes, Dateimodifikationen, Kernelmodulen, Systemkonfiguration
- funktioniert auf Windows, Linux, macOS

**`Remote Connection`:**
- vordefiniertes Command-Set aus Incident-Details
- kein vollwertiger System-Shell-Zugang
- dient Untersuchung und Response

**`Remote Shell`:**
- nur mit passender Lizenz / Add-on / Policy
- startet echte Remote-Shell-Session
- Ausführung von Systemkommandos
- laut Doku mit `root privileges`
- Upload/Download-Funktionen
- forensische und mitigative Aktionen

**Schlussfolgerung:**  
Mit `Remote Shell` kann der Administrator faktisch auf das Dateisystem zugreifen und darüber Dateien ansehen, manipulieren und bewegen.

**Quellen:**  
[runLiveSearchQuery](https://www.bitdefender.com/business/support/en/77209-1223938-runlivesearchquery.html), [Live Search](https://techzone.bitdefender.com/en/security-layers/detection/live-search.html), [Investigating Incidents](https://www.bitdefender.com/business/support/en/77209-151142-investigating-incidents.html), [Starting a Remote Shell session](https://www.bitdefender.com/business/support/en/77209-201640-starting-a-remote-shell-session.html)

#### 3.4.6 Konsequenz für private Rechner / BYOD
Wenn ein privater Rechner als verwalteter GravityZone-Endpoint in derselben Firmeninstanz hängt, dann gilt technisch:
- der Endpoint unterliegt Admin-Policies
- der Nutzer kann sich lokal nicht eigenständig aus der zentralen Steuerung herausnehmen
- eine Ausnahme ist nur möglich, wenn der Admin sie bewusst gewährt
- lokale Sonderrechte (`Power User`) sind ebenfalls admin-gesteuert

**Quellen:**  
[Using the Power User module](https://www.bitdefender.com/business/support/en/77209-87461-using-the-power-user-module.html), [Security management](https://www.bitdefender.com/business/support/en/77209-77398-security-management.html)

**✅ Positivbeispiel(e):**
- Für strikte Trennung Arbeits-/Privatgerät eigenes Firmen-Device oder separate Arbeits-VM verwenden.
- `Remote Shell` klar als höher privilegierten Zugriff dokumentieren, nicht als Standardfunktion jeder kleinen Lizenz.

**❌ Negativbeispiel(e):**
- Annehmen, ein Admin könne in Standard-GravityZone immer automatisch den kompletten Dateibaum browsen.  
  Falsch, weil das im Standard-UI so nicht dokumentiert ist.
- Annehmen, ein privater Nutzer könne sich lokal selbst aus einer Firmen-Policy ausklinken.  
  Falsch, weil Policy- und Modulsteuerung zentral vom Admin kommt.

---

### 3.5 REQ-005: Socket-Pläne, Reachability, SBOM und AI model scan
[INTENT: SPEZIFIKATION]

**Typ:** ANFORDERUNG

**Beschreibung:**  
Diese Einheit dokumentiert die sicherheitsrelevanten Unterschiede der Socket-Pläne und erklärt die drei im Kontext besonders wichtigen Begriffe.

#### 3.5.1 Sicherheitsrelevante Socket-Plan-Features
##### `Free`
Sicherheitskern:
- erkennt `70+ risk types`
- blockiert bösartige Dependencies automatisch
- AI analysis für verborgenes / verdächtiges Dependency-Verhalten

##### `Team`
Zusätzlich sicherheitsrelevant:
- `precomputed reachability analysis`
- `priority scoring`
- Slack-Alerts für neue Malware / CVEs (operativ, nicht Kernschutz)

##### `Business`
Zusätzlich sicherheitsrelevant:
- `SBOM import/export`
- `Scan GitHub Actions`
- `Scan AI models`

##### `Enterprise`
Zusätzlich sicherheitsrelevant:
- `Full Application Function-level Reachability`

**Wichtige Kontextschlussfolgerung:**  
Wenn **Scan-Anzahl**, **Seats**, **AI models** und **GitHub Actions** aus dem Scope entfernt werden, dann bleibt:
- `Free` enthält bereits die **eigentliche Kernschutzschicht** für normale Package-Malware-Blockierung
- `Team` bringt vor allem **Präzision**
- `Business` bringt zusätzliche Schutzflächen
- `Enterprise` bringt maximale Reachability-Tiefe

**Quellen:**  
[Socket Pricing](https://socket.dev/pricing), [Reachability Analysis](https://docs.socket.dev/docs/reachability-analysis)

#### 3.5.2 `Reachability Analysis`
`Reachability Analysis` beantwortet nicht nur:  
„Ist irgendwo ein CVE in einer Dependency?“

Sondern:  
„Kann dieser verwundbare Code in meiner Anwendung überhaupt erreicht und ausgenutzt werden?“

Socket unterscheidet drei Stufen:
- `Tier 3 – Dependency Reachability`
- `Tier 2 – Precomputed Reachability`
- `Tier 1 – Full Application Reachability`

**Sicherheitsnutzen:**
- weniger irrelevante CVE-Treffer
- Fokus auf wirklich exploitable Pfade
- präzisere Priorisierung

**Einordnung:**  
Sicherheitsrelevant **ja**, aber **keine zusätzliche aktive Block-Engine**.

**Quellen:**  
[Reachability Analysis](https://docs.socket.dev/docs/reachability-analysis), [Socket Reachability](https://socket.dev/features/reachability), [Full Application Reachability](https://docs.socket.dev/docs/full-application-reachability)

#### 3.5.3 `SBOM`
`SBOM` = `Software Bill of Materials`

Bedeutung:
- Stückliste der enthaltenen Softwarebestandteile
- direkte und transitive Dependencies
- Versionen / Herkunft / Metadaten

**Sicherheitsnutzen:**
- Transparenz
- bessere CVE-/Lizenz-/Policy-Analyse
- Vergleichbarkeit zwischen Builds
- bessere Incident- und Audit-Fähigkeit

**Einordnung:**  
Primär **Sichtbarkeit / Transparenz**, nicht selbst aktive Schutzmaßnahme.

**Quellen:**  
[Socket Pricing](https://socket.dev/pricing), [Create full scan / SBOM artifacts](https://docs.socket.dev/reference/createorgfullscan)

#### 3.5.4 `AI model scan`
Socket scannt laut Doku die Inhalte von AI-Modell-Dateien und modellnahen Artefakten, u. a.:
- `Pickle`
- `PyTorch`
- `Keras`
- `TensorFlow`
- `GGUF`
- `Llamafile`
- `LiteRT / TFLite`
- `Hugging Face`

**Worauf geprüft wird:**
- Malware / Backdoors
- schädliche Payloads
- Deserialisierungsrisiken
- Runtime-Risiken
- angrenzende Package-/Code-Risiken

**Wie es funktioniert:**
- lokal / manuell per CLI-Workflow möglich
- CI/CD möglich
- GitHub Actions möglich
- spezialisierte PURL-/AIBOM-Workflows vor allem in Enterprise-orientierten Modell-Scans

**Wichtiger Kontextschluss:**  
Es ist **kein passiver lokaler Echtzeit-AV**, sondern ein **Supply-Chain-Scan-Workflow** für Modellartefakte.

**Quellen:**  
[Socket Ecosystem Support](https://docs.socket.dev/docs/language-support), [Socket Hugging Face Model Scan](https://socket.dev/blog/announcing-experimental-malware-scanning-for-hugging-face), [socket scan](https://docs.socket.dev/docs/socket-scan), [Socket for GitHub Actions](https://docs.socket.dev/docs/socket-for-github-actions)

#### 3.5.5 Socket Firewall-Produktmerkmale (im Kontext betrachtet)
Explizit aus Pricing / Feature-Kontext:
- block malicious packages at install time
- 4 supported ecosystems
- custom security policy
- self-hosted or client/server deployment
- centralized visibility
- custom registries

**Quellen:**  
[Socket Pricing](https://socket.dev/pricing), [Socket Firewall](https://socket.dev/features/firewall)

**✅ Positivbeispiel(e):**
- `Free` als ausreichende Baseline wählen, wenn nur normale Package-Malware-Blockierung gefordert ist und AI/GitHub-Actions/extra Präzision nicht im Scope liegen.
- `Reachability` als präzisierenden Sicherheitsmehrwert und nicht als zweite Firewall einordnen.

**❌ Negativbeispiel(e):**
- `Team` als klar stärkere Schutzschicht werten, obwohl hauptsächlich Reachability/Priorisierung hinzukommt.  
  Falsch, weil der Kernblockier-Schutz schon in `Free` steckt.
- `SBOM` als aktive Schutzmaßnahme statt als Transparenz-/Analysegrundlage darstellen.  
  Falsch, weil SBOM nicht selbst blockiert.
