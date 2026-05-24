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
- **https://github.com/CyberT33N/security-cheat-sheet/blob/main/docs/av/bitdefender-vs-malewarebytes.md**

---

### 3.4 REQ-004: Vollständige Administratorfunktionen in GravityZone
https://github.com/CyberT33N/security-cheat-sheet/blob/main/docs/av/bitdefender/gravity-zone/admin-features.md

---

### 3.6 REQ-006: Aikido-Produktstruktur und Vergleiche zu Socket
https://github.com/CyberT33N/security-cheat-sheet/blob/main/docs/supply-chain-attacks/registry-firewalls/aikido-device-protect-vs-socketdev.md

---

### 3.7 REQ-007: Direktvergleich `Socket Firewall` vs. `Sonatype Repository Firewall`
https://github.com/CyberT33N/security-cheat-sheet/tree/main/docs/supply-chain-attacks/registry-firewalls

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
