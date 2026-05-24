
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
