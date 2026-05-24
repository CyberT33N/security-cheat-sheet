
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
