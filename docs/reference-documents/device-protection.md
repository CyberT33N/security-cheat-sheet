# Referenzdokument: Sicherheits-, Produkt- und Firewall-Vergleiche aus dem Gesamtkontext
[INTENT: KONTEXT]

---

## 1. Aufgabenübersicht
[INTENT: KONTEXT]

Dieses Referenzdokument fasst den gesamten bisherigen Kontext vollständig zusammen und strukturiert ihn so, dass ein LLM-Agent die besprochenen Themen ohne weitere Suche autonom verarbeiten kann.

Abgedeckt werden alle im Kontext behandelten Hauptthemen:

- **Gesamtarchitektur für sichere Entwickler-Hosts** einschließlich der Grundsatzentscheidung, dass für maximale Sicherheit kein Einzelprodukt, sondern eine **mehrschichtige Software-Architektur** gewinnt.
- **Bitdefender-interne Vergleiche**, insbesondere:
  - `Bitdefender Ultimate Security`
  - `GravityZone Small Business Security`
  - `GravityZone Business Security`
  - `GravityZone Business Security Premium`
  - ergänzend `GravityZone Business Security Enterprise`
- **Direktvergleich Bitdefender vs. Malwarebytes**, einschließlich der Unterscheidung zwischen Consumer-/Small-Business- und ThreatDown-/EDR-nahen Varianten.
- **Linux-Unterstützung in GravityZone** einschließlich der Frage, welche Security-Features auf Linux wirklich vorhanden sind und wo es Unterschiede oder Einschränkungen gibt.
- **Vollständige Administratorfunktionen in GravityZone** für Client-Rechner:
  - was ein Administrator sehen kann
  - was er kontrollieren / sperren kann
  - was er aktiv ausführen kann
  - wann er tieferen Systemzugriff erhält
- **Socket-Produkte und -Pakete**:
  - `Free`
  - `Team`
  - `Business`
  - `Enterprise`
  - plus die sicherheitsrelevanten Unterschiede der Pläne
- **Begriffs- und Funktionsklärungen**:
  - `Reachability Analysis`
  - `SBOM`
  - `AI model scan`
  - `HyperDetect`
- **Aikido-Produktzerlegung**:
  - `Aikido Protect`
  - `Zen`
  - `Device Protection`
  - `Safe Chain`
  - inkl. Klarstellung, dass `Zen` nicht dieselbe Schicht wie eine Package-/Registry-Firewall ist
- **Direktvergleiche im Supply-Chain-/Firewall-Bereich**:
  - `Socket Firewall` vs. `Aikido`
  - `Socket Firewall` vs. `Aikido Safe Chain`
  - `Socket Firewall` vs. `Sonatype Repository Firewall`
- **Kontextprodukte und Zusatzkontrollen**, die im Verlauf als ergänzende oder alternative Schichten behandelt wurden:
  - `Microsoft Defender Suite`
  - `CrowdStrike Falcon`
  - `Phylum Package Firewalls`
  - `Docker Buildx Policies`
  - `Harbor`
  - `Chainguard`
  - native `VS Code`-/Browser-Extension-Governance
  - explorative Punktlösungen wie `VSXSentry Guard`, `IDE Shepherd`, `Ward`

Das Dokument trennt strikt zwischen verschiedenen **Entscheidungsscop es**. Dadurch werden scheinbare Widersprüche vermieden. Beispielsweise kann ein Produkt in einem Scope `Platz 1` sein und in einem anderen Scope verlieren, wenn sich die Bewertungsachsen ändern.

---

## 2. Informationsregister (INHALT-Einheiten)
[INTENT: REFERENZ]

| ID | Typ | Beschreibung | Veränderung | Status |
|----|-----|-------------|-------------|--------|
| REQ-001 | ANFORDERUNG | Dokumentiere die Bewertungsmethodik, die Scope-Trennung und die Sicherheitsfilter, die in den einzelnen Vergleichen angewandt wurden. | Nein | ✅ |
| REQ-002 | ANFORDERUNG | Dokumentiere das finale Gesamtbild und die `Platz 1`-Entscheidungen je Vergleichsscope, inklusive Prozentwerten und Begründungen. | Nein | ✅ |
| REQ-003 | ANFORDERUNG | Dokumentiere alle Bitdefender-, GravityZone- und Malwarebytes-Vergleiche, inklusive Linux-Support und Paketdeltas. | Nein | ✅ |
| REQ-004 | ANFORDERUNG | Dokumentiere die vollständigen Administratorfunktionen in GravityZone für Client-Rechner: sehen, kontrollieren, sperren, aktiv eingreifen, remote zugreifen. | Nein | ✅ |
| REQ-005 | ANFORDERUNG | Dokumentiere die Socket-Pläne, die sicherheitsrelevanten Unterschiede der Pläne sowie die Begriffe `Reachability Analysis`, `SBOM` und `AI model scan`. | Nein | ✅ |
| REQ-006 | ANFORDERUNG | Dokumentiere die Aikido-Produktstruktur und die Vergleichsergebnisse im Verhältnis zu Socket, unter Ausschluss von Device Protection in Linux/Windows-unfertigen Scopes. | Nein | ✅ |
| REQ-007 | ANFORDERUNG | Dokumentiere den Direktvergleich `Socket Firewall` vs. `Sonatype Repository Firewall` ausschließlich nach Sicherheitsmerkmalen. | Nein | ✅ |
| REQ-008 | ANFORDERUNG | Dokumentiere alle ergänzenden und sekundären Produkte/Kontrollschichten, die im Kontext behandelt wurden, und ordne sie richtig ein. | Nein | ✅ |
| CONV-001 | CONSTRAINT | In mehreren Teilvergleichen wurden auf Wunsch Verwaltungs-, Rechte-, Mandanten- und Orga-Aspekte ausgefiltert; bewertet wurde dann nur die reine Sicherheitsschicht. | Nein | ✅ |
| CONV-002 | CONSTRAINT | Zielbild bleibt softwarebasiert; Hardware-Firewalls und Hardware-Zwangslösungen sind außerhalb des Zielraums. | Nein | ✅ |
| INFO-001 | INFORMATION | Der Bericht basiert auf den im Kontext tatsächlich recherchierten Dokumenten, Produktseiten und Vergleichen; Vendor-Dokumente wurden bei Widersprüchen gegeneinander abgeglichen. | Nein | ✅ |

---

## 3. Informationseinheiten
[INTENT: SPEZIFIKATION]

### 3.1 REQ-001: Bewertungsmethodik, Scope-Trennung und Sicherheitsfilter
[INTENT: SPEZIFIKATION]

**Typ:** ANFORDERUNG

**Beschreibung:**  
Die Vergleiche im Gesamtkontext wurden nicht über einen einzigen, globalen Score geführt, sondern über mehrere **Entscheidungsscopes**. Das ist notwendig, weil unterschiedliche Fragen unterschiedliche Bewertungsachsen erzwingen.

Die wichtigsten Scopes waren:

1. **Gesamtarchitektur für Entwickler-Hosts**  
   Fokus: maximale Sicherheit über OS-Malware, Ausführungskontrolle, Supply-Chain, IDE-/Browser-Extensions, Container, Recovery.
2. **Reiner Bitdefender-/Endpoint-Schutzkern**  
   Fokus: Malware, Echtzeitschutz, Exploit-/Fileless-/Ransomware-Abwehr.
3. **Bitdefender vs. Malwarebytes**  
   Fokus: Endpoint-Sicherheitskern ohne Preis-/Seat-/Verwaltungseffekte.
4. **Bitdefender-intern: `Ultimate` vs. `GravityZone`-Pakete**  
   Fokus: Consumer-Bundle vs. Business-Endpoint-Sicherheitskern.
5. **Supply-Chain-/Firewall-Schicht**  
   Fokus: Installationspunkt, Proxy-/Repository-Grenze, Malware-/Payload-/Package-/Container-/Model-Schutz.
6. **GravityZone-Adminrechte**  
   Fokus: Sichtbarkeit, Kontrolle, Sperrung, Task-Ausführung, Remote-Zugriff.

**Bewertungslogik:**  
Es wurden mehrfach bewusst **nicht sicherheitsrelevante Achsen** entfernt, wenn dies explizit verlangt wurde. Besonders häufig ausgefiltert wurden:
- zentrale Verwaltung
- Benutzer-/Rechte-/Rollensteuerung
- Preis / Seats / Scan-Quoten
- Compliance-/Support-/Mandanten-Aspekte
- allgemeine Produktivitäts- oder Orga-Funktionen

**Ist-Zustand:**  
Im Verlauf wurden mehrere Vergleiche zunächst breiter geführt und später auf Wunsch enger auf reine Sicherheitsaspekte reduziert.

**Soll-Zustand:**  
Alle Ergebnisse müssen im Bericht so dargestellt werden, dass klar erkennbar bleibt:
- **welcher Scope** gemeint war
- **welche Achsen** gewertet wurden
- **welche Achsen explizit entfernt** wurden

**✅ Positivbeispiel(e):**
- `Reachability Analysis` als **sicherheitsrelevante Präzisionsschicht**, aber **nicht** als zusätzlicher aktiver Blockier-Motor einordnen.
- `VPN` und `Password Manager` bei `Ultimate Security` **nicht** als stärkere Endpoint-Schutzschicht gegen Malware/Exploit werten.

**❌ Negativbeispiel(e):**
- `Ultimate Security` nur deshalb zum Sieger erklären, weil es mehr Consumer-Extras enthält.  
  Falsch, weil dadurch der **Schutzkern** mit **Bündel-Extras** vermischt würde.
- `Socket Team` als eindeutig stärkere Schutzschicht bewerten, obwohl es im Kern primär **Präzision / Priorisierung** und nicht eine neue Block-Engine hinzufügt.  
  Falsch, weil hier Reporting-/Präzisionsgewinn mit **aktivem Zusatzschutz** verwechselt würde.

---

### 3.2 REQ-002: Finale Gesamtplatzierungen und `Platz 1`-Entscheidungen
[INTENT: SPEZIFIKATION]

**Typ:** ANFORDERUNG

**Beschreibung:**  
Es gibt **keinen einzigen globalen Sieger** über alle diskutierten Fragen. Die `Platz 1`-Entscheidung hängt vom Scope ab.

#### 3.2.1 Gesamtarchitektur für sichere Entwickler-Hosts
**Platz 1:**  
`Bitdefender GravityZone Business Security Enterprise + Socket Firewall + native IDE-/Browser-Allowlisting + Docker/Harbor-Policies`

**Score:** `47 %`

**Warum Platz 1?**  
Weil diese Architektur als einzige im Kontext die vier notwendigen Ebenen gemeinsam abdeckt:
- primäre Endpoint-/EDR-Schicht
- install-time Package-/Supply-Chain-Gate
- harte IDE-/Browser-Allowlisting-Schicht
- Container-/Image-Policy

**Weitere Platzierungen im selben Scope:**
- Platz 2: `Microsoft Defender Suite` als stärkster One-Vendor-Ansatz — `31 %`
- Platz 3: `Aikido-zentrierte macOS-Hochrisiko-Enklave + primärer EDR` — `22 %`

#### 3.2.2 Reiner Bitdefender-/Endpoint-Schutzkern
**Platz 1 innerhalb der Bitdefender-Pakete:**  
`GravityZone Business Security Premium`

**Security-Tiefe:** `94 / 100`  
**Empfehlungsgewichtung innerhalb des GravityZone-Paketvergleichs:** `48 %`

Weitere Platzierungen:
- `GravityZone Business Security` — `84 / 100` / `31 %`
- `GravityZone Small Business Security` — `76 / 100` / `21 %`
- `Ultimate Security` wurde nicht als vollwertiger GravityZone-Business-Ersatz bewertet, sondern als Consumer-Bundle in einem separaten Vergleich.

#### 3.2.3 `Ultimate Security` vs. `GravityZone Small Business Security`
**Platz 1:** `GravityZone Small Business Security`  
**Score:** `55 %` vs. `45 %`

**Warum Platz 1?**  
Weil bei reiner Sicherheitskern-Betrachtung `GravityZone Small` härter auf ML-/Behavior-/Fileless-/Ransomware-/Exploit-Schutz fokussiert ist, während `Ultimate Security` mehr Consumer-Zusatzdienste bündelt.

#### 3.2.4 `Bitdefender` vs. `Malwarebytes`
**Hauptvergleich Endpoint-Sicherheitskern:**  
- `Bitdefender`: `63 %`
- `Malwarebytes`: `37 %`

**Näherer Consumer/Small-Business-Vergleich:**  
- `Bitdefender`: `60 %`
- `Malwarebytes Premium / Teams`: `40 %`

**Näherer Business/ThreatDown-Vergleich:**  
- `Bitdefender`: `56 %`
- `Malwarebytes ThreatDown / EDR-nah`: `44 %`

**Warum Bitdefender Platz 1?**  
Weil Bitdefender im Kontext als breitere und tiefer geschichtete Endpoint-Sicherheitsplattform mit stärkeren unabhängigen Gesamtsignalen eingeordnet wurde.

#### 3.2.5 `Socket Firewall` vs. `Aikido`
**Wenn Aikido als `Zen` (Runtime-Firewall) missverstanden wird:**  
- `Socket Firewall`: `88 %`
- `Aikido Zen`: `12 %`

**Warum?**  
Weil `Zen` die falsche Schutzschicht für Package-/NPM-/Supply-Chain-Installationen ist.

**Fairer Vergleich `Socket Firewall` vs. `Aikido Safe Chain`:**
- `Socket Firewall`: `57 %`
- `Aikido Safe Chain`: `43 %`

**Warum Socket Platz 1?**  
Weil `Socket Firewall` klarer als dedizierte Package-/Installations-Firewall positioniert ist.

#### 3.2.6 `Socket Firewall` vs. `Sonatype Repository Firewall`
**Reiner Firewall-/Ingress-Sicherheitsvergleich:**  
- `Sonatype Repository Firewall`: `58 %`
- `Socket Firewall`: `42 %`

**Warum Sonatype Platz 1?**  
Weil Sonatype auf der reinen Repository-/Proxy-/Quarantäne-Schicht stärker ist:
- Malware-/Malicious-Code-Defense
- Release Integrity
- Quarantäne
- Docker-/Container-Quarantäne
- AI/ML-Modell-Evaluierung am Downloadpunkt

**✅ Positivbeispiel(e):**
- `Platz 1` immer scopespezifisch dokumentieren.
- Den Stack-Sieger für Gesamtarchitektur nicht mit dem Sieger für reine Firewall-Sicherheit verwechseln.

**❌ Negativbeispiel(e):**
- `Sonatype` zum globalen Sieger über alles erklären.  
  Falsch, weil Sonatype nur in der **reinen Repository-Firewall-Schicht** `Platz 1` war.
- `Socket` zum globalen Sieger über alles erklären.  
  Falsch, weil `Socket` nicht die stärkste reine Repository-/Proxy-Quarantäneschicht war.

---

### 3.3 REQ-003: Bitdefender-, GravityZone- und Malwarebytes-Vergleiche
[INTENT: SPEZIFIKATION]

**Typ:** ANFORDERUNG

**Beschreibung:**  
Diese Einheit bündelt alle internen Bitdefender-Vergleiche, den Vergleich zu Malwarebytes sowie die Linux-Support-Frage.

#### 3.3.1 Produktdossier: `Bitdefender Ultimate Security`
**Explizit betrachtete Features im Kontext:**
- `Bitdefender Shield`
- `Advanced Threat Defense`
- `Exploit detection`
- `Online Threat Prevention`
- `Email Protection`
- `Ransomware Remediation`
- `Scam Protection Pro` / `Scam Copilot`
- `Unlimited VPN`
- `Password Manager`
- `Digital Identity Protection`

**Einordnung:**  
`Ultimate Security` ist ein **Consumer-/Household-Bundle**:
- stark für Privatnutzer
- stark bei Anti-Malware plus Privacy-/Identity-Zusatzdiensten
- aber nicht der stärkste Bitdefender-Ansatz für den **reinen Endpoint-Schutzkern**

**Wichtiger Preis-/Bundle-Kontext:**  
Im Kontext wurde festgehalten, dass `Ultimate Security` typischerweise als **5-Geräte-Bundle** vermarktet wird. Das erklärt einen Teil des Vergleichs mit `GravityZone Small`, das stärker endpoint-/seat-basiert wirkt.

**Quellen:**  
[Bitdefender Ultimate Security](https://www.bitdefender.com/en-us/consumer/ultimate-security?icid=main-menu%7Cv4%7Cultimate_security), [Ultimate Security User Guide](https://www.bitdefender.com/content/dam/bitdefender/consumers/case-studies/ultimate-security/EN.pdf)

#### 3.3.2 Produktdossier: `GravityZone Small Business Security`
**Explizit betrachtete Features im Kontext:**
- `Advanced Threat`
- `Ransomware Mitigation`
- `Fileless Attack Protection`
- Machine Learning
- Behavioral Analysis
- Continuous Monitoring
- Process termination
- Quarantine
- Rollback of malicious changes
- Anti-phishing and Fraud Prevention
- Advanced Anti-Exploit

**Optional/ergänzend betrachtete Add-ons / Kontextmodule:**
- `Web Access and Device Control`
- `Network Attack Defense and Risk Management`

**Einordnung:**  
`GravityZone Small` ist ein echter Business-/Endpoint-Schutz mit deutlich stärkerem Security-Core als `Ultimate Security`, wenn Consumer-Extras aus der Wertung entfernt werden.

**Quellen:**  
[GravityZone Small Business Security](https://www.bitdefender.com/en-gb/business/products/gravityzone-small-business-security), [Bitdefender Business Compare](https://www.bitdefender.com/en-us/business/compare)

#### 3.3.3 Produktdossier: `GravityZone Business Security`
**Explizit betrachtete Features im Kontext:**
- alles Wesentliche aus `Small`
- `Network Attack Defense`
- `Endpoint Risk Management` / `Endpoint Risk Analytics`
- Multi-layered next-gen endpoint protection
- Machine Learning Anti-Malware
- Ransomware mitigation with tamperproof backups
- Web-based security
- Prevention / detection / remediation / visibility
- optional `Email Security`
- optional `Patch Management`
- optional `Full Disk Encryption`

**Zusätzliche Features gegenüber `Small` laut offizieller Compare-Seite:**
- `Network Attack Defense`
- `Web Access Control`
- `Device Control`
- `Endpoint Risk Analytics`

**Sicherheitsrelevant nach Filterung:**  
- `Network Attack Defense`
- `Endpoint Risk Management / Analytics`

**Quellen:**  
[GravityZone Business Security](https://www.bitdefender.com/en-no/business/products/gravityzone-business-security), [Bitdefender Business Compare](https://www.bitdefender.com/en-us/business/compare)

#### 3.3.4 Produktdossier: `GravityZone Business Security Premium`
**Explizit betrachtete Features im Kontext:**
- alles aus `Business Security`
- `HyperDetect`
- `Sandbox Analyzer`
- `Fileless Attack Defense`
- `Attack Forensics / Incident Analysis / Visualization`
- `Process Inspection`
- `Registry Monitoring`
- `Code Inspection`
- `Machine Learning Anti-Malware`
- `Advanced Anti-Exploit`
- `Microsoft Exchange`-Abdeckung
- `antispam`
- `antimalware for mail servers`

**Zusätzliche Features gegenüber `Business Security` laut offizieller Compare-Seite:**
- `Tunable Machine Learning (HyperDetect)`
- `Sandbox Analyzer`
- `Fileless Attack Defense`
- `Microsoft Exchange coverage, top-rated antispam and antimalware for mail servers`

**Einordnung:**  
Im Bitdefender-internen Vergleich ist `Business Security Premium` die stärkste Sicherheitsstufe der betrachteten drei Business-Pakete.

**Quellen:**  
[GravityZone Business Security Premium](https://www.bitdefender.com/en-us/business/products/gravityzone-premium-security), [Bitdefender Business Compare](https://www.bitdefender.com/en-us/business/compare)

#### 3.3.5 Kontextprodukt: `GravityZone Business Security Enterprise`
**Explizit betrachtete Features im Kontext:**
- EDR
- Cross-endpoint correlation
- Business Security Premium + EDR/XEDR
- optional XDR-Sensoren
- Live Search
- Incident visibility / human-readable attack context
- `Remote Connection`
- `Remote Shell` (zusätzliche Lizenz-/Modulfrage)

**Einordnung:**  
Wurde im Gesamtkontext als Teil des stärksten Full-Developer-Host-Stacks verwendet, aber nicht als Small-/Mid-Tier-Paket verglichen.

**Quellen:**  
[GravityZone Business Security Enterprise](https://www.bitdefender.com/en-us/business/products/gravityzone-enterprise-security), [Investigating Incidents](https://www.bitdefender.com/business/support/en/77209-151142-investigating-incidents.html), [Live Search](https://techzone.bitdefender.com/en/security-layers/detection/live-search.html)

#### 3.3.6 Direktvergleich: `Ultimate Security` vs. `GravityZone Small`
**Ergebnis:**  
- `GravityZone Small`: `55 %`
- `Ultimate Security`: `45 %`

**Warum `GravityZone Small` gewinnt:**  
- stärkerer Fokus auf ML-/Behavior-/Fileless-/Exploit-/Ransomware-Schutz
- weniger Consumer-Bündel-Charakter
- härtere Endpoint-Sicherheitslogik

**Warum `Ultimate Security` trotzdem stark bleibt:**  
- sehr guter Basisschutz
- zusätzliche Mail-/Scam-/Identity-/VPN-/Password-Features
- für Privatnutzer oft das rundere Paket

#### 3.3.7 Direktvergleich: `Bitdefender` vs. `Malwarebytes`
**Malwarebytes Premium / Teams / ThreatDown:**
- Real-time threat quarantine
- Web protection
- Exploit protection
- Ransomware protection
- Ransomware rollback (ThreatDown / EDR-nah)
- Endpoint isolation
- Suspicious Activity Monitoring
- Active Response Shell
- DNS filtering (add-on / planabhängig)
- Firewall Control / Brute Force Protection in bestimmten Produktlinien

**Bitdefender gewinnt im Kontext insgesamt, weil:**
- breitere mehrschichtige Präventionsarchitektur
- stärkere Exploit-/Fileless-/Memory-/Script-Abwehr
- stärkere unabhängige Gesamtsignale
- härtere Business-/Endpoint-Ausrichtung

**Malwarebytes bleibt stark bei:**
- Behavioral Detection
- Ransomware Recovery / Rollback
- einfacherer / leichterer Endpoint-Ansatz

**Quellen:**  
[Malwarebytes Premium](https://www.malwarebytes.com/premium), [Malwarebytes Windows](https://www.malwarebytes.com/windows), [ThreatDown EDR](https://www.threatdown.com/products/endpoint-detection-and-response/), [ThreatDown Endpoint Protection](https://www.threatdown.com/wp-content/uploads/2024/05/TD_EP_Datasheet.pdf), [AV-Comparatives Summary Report 2025](https://av-comparatives.org/tests/summary-report-2025/)

#### 3.3.8 Linux-Support in GravityZone
**Bedeutung von „für Linux verfügbar“:**  
Es gibt einen echten Linux-Agenten: `Bitdefender Endpoint Security Tools for Linux (BEST for Linux)`.

**Wichtige Linux-Features, die im Kontext als vorhanden verifiziert wurden:**
- Antimalware / On-access / On-demand
- Advanced Threat Control
- Fileless Attack Protection
- HyperDetect
- Advanced Anti-Exploit
- Ransomware Mitigation
- Network Attack Defense
- Risk Management
- EDR
- Sandbox Analyzer
- Integrity Monitoring
- Container Protection
- Patch Management

**Wichtige Linux-Einschränkungen:**
- `Content Control` auf Linux nur als `Application Blacklisting`
- `Sandbox Analyzer` auf Linux: **manuelle** Sample Submission, keine gleichwertige automatische Submission wie auf Windows
- Kernel-/Distro-Abhängigkeiten
- nicht jede Funktion ist 1:1 identisch mit Windows/macOS

**Quellen:**  
[Features by endpoint type](https://www.bitdefender.com/business/support/en/77211-376324-features-by-asset-type.html), [BEST for Linux Quick Start](https://www.bitdefender.com/business/support/en/77211-157515-bitdefender-endpoint-security-tools-for-linux-quick-start-guide.html), [HyperDetect](https://www.bitdefender.com/business/support/en/77212-342938-hyperdetect.html), [Sandbox Analyzer](https://www.bitdefender.com/business/support/en/77209-376317-sandbox-analyzer.html), [Content Control](https://www.bitdefender.com/business/support/en/77211-342965-content-control.html), [Risk Management](https://www.bitdefender.com/business/support/en/77209-342985-risk-management.html), [Network Attack Defense](https://www.bitdefender.com/business/support/en/77211-376343-network-attack-defense.html)

**✅ Positivbeispiel(e):**
- `GravityZone Business Security Premium` wählen, wenn der stärkste Bitdefender-Sicherheitskern gewünscht ist.
- `GravityZone Small` vor `Ultimate Security` wählen, wenn Consumer-Extras explizit nicht mitgezählt werden sollen.

**❌ Negativbeispiel(e):**
- `Ultimate Security` als stärkeres Security-Core-Produkt werten, weil VPN und Password Manager enthalten sind.  
  Falsch, weil diese Extras nicht den Endpoint-Schutzkern stärken.
- Linux-Support so interpretieren, als seien automatisch alle Windows-Funktionen in identischer Form vorhanden.  
  Falsch, weil Bitdefender Linux-spezifische Einschränkungen dokumentiert.

---

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

---

### 3.6 REQ-006: Aikido-Produktstruktur und Vergleiche zu Socket
[INTENT: SPEZIFIKATION]

**Typ:** ANFORDERUNG

**Beschreibung:**  
Diese Einheit klärt die Aikido-Produktlogik und dokumentiert die fairen Vergleichsergebnisse.

#### 3.6.1 Produktzerlegung `Aikido`
##### `Aikido Protect`
Plattform-/Landing-Bereich für Runtime-/Protect-Themen. Im Kontext sichtbar:
- `Runtime Protection`
- `Device Protection`
- `Bot Protection`

##### `Zen`
Runtime-/In-App-Firewall:
- läuft **in der App**
- schützt APIs / Runtime / Requests
- blockiert Bots, Angriffe, bekannte Threat Actors
- kann Outbound-Domains beobachten
- ist **nicht** dieselbe Schicht wie eine Package-/Registry-Firewall

Quellen: [Aikido Protect](https://www.aikido.dev/platform/protect), [Zen](https://www.aikido.dev/protect/zen)

##### `Device Protection`
Agent-basierter Workstation-Schutz für Entwicklergeräte:
- blockiert Packages / Extensions / AI-Tools vor Installation
- org-weite Device-Sicht und Policies
- im Kontext wichtig: öffentliches Signal `Windows/Linux support in Q2 2026`, aber Doku-/Hilfetexte zeigten noch Mac-zentrierten Status

Quellen: [Device Protection page](https://www.aikido.dev/protect/device-protection), [Aikido Device Protection docs](https://help.aikido.dev/aikido-device-protection/endpoint-protection.md)

##### `Safe Chain`
Separates Open-Source-CLI / Wrapper-Werkzeug:
- blockiert Malware bei Package-Installationen
- für Einzelentwickler oder CI/CD
- prüft nested dependencies
- erkennt obfuscated code, exfiltration, install scripts, crypto miners
- blockiert halluzinierte/fake packages
- blockiert sehr neue Versionen und fällt auf ältere sichere Version zurück

Quellen: [Safe Chain Docs](https://help.aikido.dev/code-scanning/aikido-malware-scanning), [Introducing Safe Chain](https://www.aikido.dev/blog/introducing-safe-chain), [Securing AI-Generated Code](https://help.aikido.dev/ai-and-dev-tools/securing-ai-generated-code)

#### 3.6.2 Wichtige Klarstellung
**`Safe Chain` ist nicht dasselbe wie `Device Protection`.**  
**`Zen` ist nicht dasselbe wie `Safe Chain`.**

- `Zen` = Runtime-Firewall in der App
- `Safe Chain` = install-time Package-Schutz
- `Device Protection` = org-weiter Workstation-Agent

#### 3.6.3 Direktvergleich `Socket Firewall` vs. `Aikido Zen`
**Ergebnis:** `88 %` vs. `12 %`

**Warum?**  
Weil `Zen` für NPM-/Package-/Supply-Chain-Install-Schutz die falsche Schicht ist.

#### 3.6.4 Direktvergleich `Socket Firewall` vs. `Aikido` ohne `Device Protection`
**Ergebnis:** `65 %` vs. `35 %`

**Warum?**  
Weil ohne `Device Protection` auf Aikido-Seite primär:
- `Safe Chain`
- Repo-/Container-Detection
- `Zen` als andere Schicht  
übrigbleiben.

#### 3.6.5 Direktvergleich `Socket Firewall` vs. `Aikido Safe Chain`
**Ergebnis:** `57 %` vs. `43 %`

**Warum `Socket` knapp gewinnt:**
- klarere Firewall-/Proxy-Positionierung
- stärker als dedizierte Package-Firewall ausgerichtet
- breitere Wahrnehmung als Installationsgrenzen-Schutz

**Warum `Aikido Safe Chain` stark bleibt:**
- nested dependency checks
- Hallucinated-package-Blockierung
- Altersregel für neue Versionen
- Fallback auf ältere sichere Version

**✅ Positivbeispiel(e):**
- `Socket Firewall` mit `Aikido Safe Chain` vergleichen, wenn es um Package-Install-Schutz geht.
- `Zen` als Runtime-Firewall separat behandeln.

**❌ Negativbeispiel(e):**
- `Socket Firewall` direkt gegen `Zen` vergleichen und daraus ein Paket-/Supply-Chain-Urteil ableiten.  
  Falsch, weil die Schutzschichten unterschiedlich sind.
- `Safe Chain` und `Device Protection` als dasselbe Produkt behandeln.  
  Falsch, weil Aikido diese Wege selbst trennt.

---

### 3.7 REQ-007: Direktvergleich `Socket Firewall` vs. `Sonatype Repository Firewall`
[INTENT: SPEZIFIKATION]

**Typ:** ANFORDERUNG

**Beschreibung:**  
Dieser Vergleich wurde mehrfach verfeinert und schließlich **nur nach Sicherheitsaspekten** geführt.

#### 3.7.1 Sicherheitsmerkmale `Socket Firewall`
- blockiert malicious packages at install time
- custom security policy
- AI analysis of hidden dependency behavior
- Integration in developer-/CI-Workflows
- Modell- und Dependency-nahe Zusatzsicherheitsflächen im Socket-Umfeld

**Quellen:**  
[Socket Firewall](https://socket.dev/features/firewall), [Socket Pricing](https://socket.dev/pricing)

#### 3.7.2 Sicherheitsmerkmale `Sonatype Repository Firewall`
- automatische Bewertung jeder neuen Komponente am Download-/Proxy-Punkt
- automatische Quarantäne riskanter Komponenten
- Malware Defense Evaluate API für OSS-Komponenten und AI/ML-Modelle
- `Release Integrity`: `normal` / `suspicious` / `malicious`
- AI/ML-Modell-Evaluierung (z. B. Hugging Face)
- Docker-/Container-Quarantäne
- Policy-Compliant Component Selection für npm/PyPI

**Quellen:**  
[Sonatype Repository Firewall Docs](https://help.sonatype.com/en/repository-firewall.html), [Firewall Quarantine](https://help.sonatype.com/en/firewall-quarantine.html), [Malware Defense Evaluate API](https://help.sonatype.com/en/malware-defense-evaluate-api.html), [Release Integrity](https://help.sonatype.com/en/release-integrity.html), [Firewall for Docker](https://help.sonatype.com/en/firewall-for-docker.html), [Policy Compliant Component Selection](https://help.sonatype.com/en/policy-compliant-component-selection.html), [Sonatype Product Page](https://www.sonatype.com/products/sonatype-repository-firewall)

#### 3.7.3 Endergebnis nach reinem Firewall-/Sicherheits-Scope
- `Sonatype Repository Firewall`: `58 %`
- `Socket Firewall`: `42 %`

**Warum Sonatype gewinnt:**
- stärkere Repository-/Proxy-/Quarantäne-Schicht
- ausgeprägtere malicious-code-/release-integrity-Logik
- Container-/AI/ML-Modell-Schutz direkt am Repository-/Downloadpunkt
- stärkeres Fail-Closed-Verhalten für den Artefakt-Eingang

#### 3.7.4 Wichtige Ergänzung
`Socket` bleibt außerhalb der reinen Firewall enger und moderner aufgestellt bei:
- developer-zentriertem Installationsschutz
- Reachability
- SBOM
- GitHub Actions
- AI-/Model-Workflows

Aber diese Vorteile machen `Socket` nicht automatisch zur stärkeren **reinen Repository-Firewall-Schicht**.

**✅ Positivbeispiel(e):**
- `Sonatype` wählen, wenn die strengste Repository-/Proxy-Quarantäne am Artefakt-Eingang gefragt ist.
- `Socket` wählen, wenn die Firewall in einen breiteren developer-zentrierten Package-/Scan-Workflow eingebettet werden soll.

**❌ Negativbeispiel(e):**
- Sonatype und Socket als identisch betrachten, nur weil beide „Firewall“ heißen.  
  Falsch, weil Einbauort und Sicherheitsmodell unterschiedlich sind.
- Reachability / SBOM als Beweis dafür verwenden, dass Socket die stärkere reine Firewall ist.  
  Falsch, weil das ergänzende Supply-Chain-Analyse, aber nicht dieselbe Firewall-Schicht ist.

---

### 3.8 REQ-008: Ergänzende und sekundäre Produkte / Kontrollschichten
[INTENT: SPEZIFIKATION]

**Typ:** ANFORDERUNG

**Beschreibung:**  
Diese Einheit bündelt alle im Kontext behandelten ergänzenden oder sekundären Produkte, die nicht den zentralen Hauptvergleich getragen haben, aber Teil des Entscheidungskontexts waren.

#### 3.8.1 `Microsoft Defender Suite`
**Einordnung:**  
Stärkster One-Vendor-Ansatz im Kontext, aber keine vollwertige install-time Package-Firewall über alle Entwickler-Ökosysteme.

**Im Kontext relevante Stärken:**
- `Defender for Endpoint`
- `Defender Vulnerability Management`
- Web protection / network protection
- browser extension assessment
- `VS Code`-Enterprise-Policies
- Web content filtering

**Kontext-Score im One-Vendor-Scope:** `31 %` hinter dem mehrschichtigen Sieger-Stack.

**Quellen:**  
[Defender Vulnerability Management](https://learn.microsoft.com/en-us/defender-vulnerability-management/defender-vulnerability-management), [Network Protection for macOS](https://learn.microsoft.com/en-us/defender-endpoint/network-protection-macos), [VS Code for enterprise](https://code.visualstudio.com/docs/enterprise/overview)

#### 3.8.2 `CrowdStrike Falcon`
**Einordnung:**  
Sehr starke EDR-/Cross-domain-Detection, aber im Kontext nicht die stärkste Antwort auf developer-spezifische Supply-Chain-Risiken.

**Kontextsignal:**  
Starke vendor-gestützte MITRE-/SE-Labs-Signale, aber nicht Sieger im diskutierten Entwickler-Host-Gesamtbild.

**Quelle:**  
[CrowdStrike MITRE 2025](https://www.crowdstrike.com/en-us/blog/crowdstrike-achieves-100-percent-2025-mitre-attack-enterprise-evaluation/)

#### 3.8.3 `Phylum Package Firewalls`
**Einordnung:**  
Registry-/Package-Firewall-Alternative mit starker Policy-/Block-Logik über Package-Manager / registries.

**Kontextrolle:**  
Sekundäre Alternative zu Socket / Sonatype / Aikido-Safe-Chain-Pfad.

**Quelle:**  
[Phylum Package Firewalls](https://docs.phylum.io/package_firewall/about)

#### 3.8.4 `Docker Buildx Policies` und `Harbor`
**Einordnung:**  
Nicht Ersatz für Endpoint- oder Package-Firewall, sondern ergänzende Schicht für Container-/Image-Supply-Chain.

**Kontextstärken:**
- `Docker Buildx Policies`: Build-Inputs, Digests, Provenance, Signaturen
- `Harbor`: Quarantäne / Pull-Block / Deployment Security für Images

**Quellen:**  
[Docker Build Policies](https://docs.docker.com/build/policies/), [Harbor Deployment Security](https://goharbor.io/docs/main/administration/vulnerability-scanning/deployment-security/)

#### 3.8.5 `Chainguard`
**Einordnung:**  
Signatur-/Policy-Gates und vertrauenswürdige Container-Basis als zusätzliche Container-Härtung.

**Quelle:**  
[Chainguard Policy Gates](https://edu.chainguard.dev/chainguard/administration/policy-gates/)

#### 3.8.6 Native IDE-/Browser-Allowlisting
Im Kontext als notwendige Begleitkontrolle genannt:
- `VS Code Allowed Extensions`
- `Chrome ExtensionSettings`
- `Edge ExtensionSettings`
- `Firefox ExtensionSettings`

**Rolle:**  
Unverzichtbare Zusatzschicht gegen bösartige IDE-/Browser-Erweiterungen.

**Quellen:**  
[VS Code for enterprise](https://code.visualstudio.com/docs/enterprise/overview), [Chrome ExtensionSettings](https://support.google.com/chrome/a/answer/9867568), [Edge ExtensionSettings](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensionsettings), [Firefox ExtensionSettings](https://firefox-admin-docs.mozilla.org/reference/policies/extensionsettings/)

#### 3.8.7 Explorative Punktlösungen
Diese Produkte wurden im Kontext als punktuelle, interessante Speziallösungen erwähnt:

- `VSXSentry Guard`  
  Feed-basierte Block-/Remove-Lösung für VS Code-Extensions  
  Quelle: [VSXSentry Guard](https://marketplace.visualstudio.com/items?itemName=mthcht.vsxsentry-guard)

- `IDE Shepherd`  
  VS Code/Cursor-Extension mit Runtime-Interception gegen bösartige Extensions / Tasks  
  Quelle: [IDE Shepherd](https://marketplace.visualstudio.com/items?itemName=Datadog.ide-shepherd-extension)

- `Ward`  
  lokale Schutzidee für Package-Installationen, auch im AI-Coding-Kontext  
  Quelle: [Ward](https://github.com/Vanguard-Defense-Solutions/ward)

**✅ Positivbeispiel(e):**
- `VS Code`-/Browser-Allowlisting als eigene Kontrollschicht neben AV/EDR und Package-Firewall einführen.
- `Docker Buildx`/`Harbor` separat als Image-/Container-Grenzschutz behandeln.

**❌ Negativbeispiel(e):**
- erwarten, dass ein AV/EDR allein Package-Firewall, Extension-Governance und Container-Provenance vollständig ersetzt.  
  Falsch, weil diese Kontrollen eigene Schichten bilden.
- `CrowdStrike` oder `Microsoft Defender` automatisch als vollständige Antwort auf NPM-/Package-Install-Supply-Chain interpretieren.  
  Falsch, weil dort die install-time Package-Grenze im Kontext nicht als gleich stark nachgewiesen wurde.

---

## 4. Konventionen & Constraints
[INTENT: CONSTRAINT]

- Vergleiche müssen scopespezifisch interpretiert werden.
- Wo ausdrücklich verlangt wurde, wurden Verwaltungs-, Benutzer-, Rollen-, Mandanten-, Reporting- oder Lizenzaspekte aus Sicherheitsvergleichen ausgefiltert.
- `Reachability Analysis` ist sicherheitsrelevante Präzision, aber keine zweite aktive Schutz-Engine.
- `SBOM` ist primär Transparenz, nicht aktive Schutzmaßnahme.
- `Zen` ist Runtime-Firewall, nicht Package-/Registry-Firewall.
- `Safe Chain` ist separater Package-/Install-Schutz und nicht identisch mit `Device Protection`.
- `Linux support` in GravityZone bedeutet realen Schutz mit Linux-Agent, aber nicht automatisch 1:1-Funktionsgleichheit zu Windows.
- Zielbild bleibt softwarebasiert; Hardware-Firewalls waren außerhalb des Zielraums.

---

## 5. Dateipfad-Index
[INTENT: REFERENZ]

Es wurden **keine Projektquell-Dateien** des Workspace als Gegenstand der Sicherheitsvergleiche analysiert. Relevante lokale Referenzdateien aus dem Kontext:

| # | Dateipfad | Relevanz | Zugehörige Einheit-IDs |
|---|-----------|----------|----------------------|
| 1 | `C:\Users\denni\.cursor\projects\c-Projects-cheat-sheets-ai-prompting-prompts-cheat-sheet\uploads\device-protection-0.md` | Lokale Referenzkopie der Aikido-Device-Protection-Seite | REQ-006 |
| 2 | `C:\Users\denni\.cursor\projects\c-Projects-cheat-sheets-ai-prompting-prompts-cheat-sheet\uploads\protect-0.md` | Lokale Referenzkopie der Aikido-Protect-Seite | REQ-006 |

Alle übrigen Quellen sind Web- und Produktdokumentationen und wurden in den jeweiligen Sektionen direkt verlinkt.

---

## 6. Ausführungskontext für LLM-Agents
[INTENT: KONTEXT]

Dieses Dokument ist so zu verwenden:

1. **Zuerst Scope identifizieren.**  
   Vor jeder Entscheidung klären:
   - Geht es um **Gesamtarchitektur**?
   - um **reine Endpoint-Sicherheit**?
   - um **Bitdefender-internen Paketvergleich**?
   - um **reine Firewall-/Repository-Schicht**?
   - um **Adminrechte / BYOD-Risiko**?

2. **Dann die passende `Platz 1`-Entscheidung anwenden.**  
   Die wichtigsten Sieger im Dokument sind:
   - **Gesamtarchitektur Entwickler-Host:** `Bitdefender GravityZone Business Security Enterprise + Socket Firewall + native IDE-/Browser-Allowlisting + Docker/Harbor-Policies`
   - **Bitdefender-intern stärkster Security-Core:** `GravityZone Business Security Premium`
   - **Small vs Ultimate:** `GravityZone Small`
   - **Bitdefender vs Malwarebytes:** `Bitdefender`
   - **Socket vs Aikido Safe Chain:** `Socket`
   - **Socket vs Sonatype reine Firewall-Schicht:** `Sonatype Repository Firewall`

3. **Filterregeln beachten.**  
   Falls erneut reine Sicherheitsvergleiche verlangt werden:
   - Management
   - Rechte
   - Seats
   - Scans pro Monat
   - Support
   - Compliance-Workflows  
   **nicht** als Sicherheitsmehrwert zählen.

4. **Aikido korrekt einordnen.**
   - `Zen` = Runtime
   - `Safe Chain` = install-time Package-Schutz
   - `Device Protection` = Workstation-Agent

5. **GravityZone-Adminrechte konservativ lesen.**  
   Standard-GravityZone ist nicht automatisch voller Explorer-Zugriff, aber mit EDR/XDR/Remote Shell kann der Zugriff in tiefen Systemzugriff übergehen.

6. **Linux-Fähigkeiten nicht unter- oder überschätzen.**  
   Linux ist in GravityZone kein Fake-Support, aber Features sind teilweise anders umgesetzt oder eingeschränkt.

Alle notwendigen Informationen sind in den Sektionen 1-5 vollständig enthalten.
