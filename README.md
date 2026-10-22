# Fachkrafthaus AI Recruiting Assistant

**IHK-Capstone-Projekt | KI-Tool-Experte | Oktober 2026**

## 1. Projektbeschreibung

Der Fachkrafthaus AI Recruiting Assistant ist ein KI-gestützter Recruiting-Prototyp, der Stellenanfragen automatisiert analysiert und Recruiter bei der Vorbereitung von Suchstrategien unterstützt.

Das Projekt wurde im Rahmen der Weiterbildung zum KI-Tool-Experten entwickelt und basiert auf der Workflow-Automatisierungsplattform **n8n** und dem OpenAI-Modell **GPT-4.1**.

**Ziel:** Wiederkehrende Analyseaufgaben im Recruiting vereinfachen, Ergebnisse standardisieren und die Vorbereitung auf Kundengespräche unterstützen.

## 2. Problemstellung

Die Analyse neuer Stellenanfragen erfordert mehrere manuelle Arbeitsschritte:

- Anforderungen einer Vakanz verstehen und strukturieren
- Muss- und Wunschkriterien unterscheiden
- Geeignete Berufsbezeichnungen und verwandte Berufe identifizieren
- Suchbegriffe für Active Sourcing und Direct Search entwickeln
- Recruiting-Schwierigkeiten einschätzen
- Rückfragen für Kundengespräche vorbereiten

Der AI Recruiting Assistant unterstützt diese Aufgaben durch eine strukturierte KI-Analyse.

## 3. Technischer Aufbau

**Verwendete Technologien:**

- n8n – Workflow-Automatisierung
- OpenAI GPT-4.1 – KI-basierte Stellenanalyse
- JavaScript – Validierung und Fehlerbehandlung
- JSON – Strukturiertes Ein- und Ausgabeformat
- GitHub – Versionsverwaltung und Projektdokumentation

**Workflow mit acht Nodes:**

1. Webhook – Stellenanfrage entgegennehmen
2. Eingabe validieren – Pflichtfelder prüfen
3. IF – Vollständigkeit kontrollieren
4. OpenAI Analyse – Stellenanfrage analysieren
5. KI-Ausgabe formal prüfen – Struktur und Datentypen validieren
6. IF – KI-Ergebnis kontrollieren
7. Antwort OK – Erfolgreiche Analyse ausgeben
8. Antwort Fehler – Kontrollierte Fehlermeldung zurückgeben

## 4. Funktionen

Der Assistent erstellt aus einer synthetischen Stellenanfrage:

- Muss- und Wunschkriterien
- Einschätzung der Besetzungsschwierigkeit
- Verwandte Berufsbezeichnungen
- Suchbegriffe für Active Sourcing
- Recruiting-Strategie
- Offene Rückfragen und Warnhinweise

Die Ausgaben werden als strukturierte JSON-Daten zurückgegeben.

## 5. Tests und Ergebnisse

Der Workflow wurde mit 20 unterschiedlichen synthetischen Stellenanfragen getestet.

| Kennzahl | Ergebnis |
|---|---|
| Echte OpenAI-Testausführungen | 20 |
| Reguläre Erfolgsantworten | 19 |
| Kontrollierte Fehlerantworten | 1 |
| Technische Erfolgsantwortquote | 95 % |
| Durchschnittliche Ausführungsdauer | ca. 2,62 Sekunden |
| Schnellste Ausführung | 1,77 Sekunden |
| Langsamste Ausführung | 4,28 Sekunden |

Die Tests wurden innerhalb der n8n-Ausführungsumgebung durchgeführt. Der Webhook wurde dabei nicht über einen externen HTTP-Aufruf ausgelöst.

Die technische Erfolgsantwortquote ist **keine fachliche Qualitätsquote**. Eine unabhängige fachliche Bewertung der Ergebnisse steht noch aus.

## 6. Erkenntnisse und Einschränkungen

Die Tests zeigten, dass der Workflow strukturierte Recruiting-Analysen erzeugen und verschiedene Fehler kontrolliert behandeln kann.

Es wurden aber auch Grenzen festgestellt:

- Bei unvollständigen Stellenanfragen kann die starre Vorgabe von mindestens drei Suchbegriffen eine sinnvolle Rückfrageantwort blockieren.
- Widersprüchliche Anforderungen werden nicht in jedem Fall vollständig korrekt verarbeitet.
- Ungewöhnliche Berufsbezeichnungen führen teilweise zu unsicheren Suchbegriffen.
- Nicht alle ungültigen Eingabedatentypen werden vor dem KI-Aufruf abgefangen.
- Der externe HTTP-Webhook und ein tatsächlicher OpenAI-Ausfall im vollständigen Workflow wurden noch nicht erfolgreich getestet.

Diese Punkte sind Teil der technischen Evaluation und zeigen Verbesserungspotenzial für eine spätere Weiterentwicklung.

## 7. Datenschutz und KI-Governance

Das Projekt berücksichtigt grundlegende Anforderungen an einen verantwortungsvollen KI-Einsatz:

- Ausschließliche Verwendung synthetischer Testdaten
- Keine Verarbeitung realer Bewerberdaten im Testbetrieb
- Keine automatisierten Einstellungsentscheidungen
- Keine automatische Kontaktaufnahme mit Kandidaten
- Kennzeichnung der KI-Ergebnisse als überprüfungsbedürftige Entwürfe
- Menschliche Kontrolle vor der operativen Verwendung

Der Prototyp ist kein produktives Bewerbermanagementsystem.

## 8. Wirtschaftlicher Nutzen

Das Projekt soll wiederkehrende Vorbereitungsarbeiten im Recruiting reduzieren.

Der mögliche Nutzen besteht in einer schnelleren Erststrukturierung von Stellenanfragen, einheitlicheren Analysen und einer besseren Vorbereitung auf Kundengespräche.

Die tatsächliche Zeitersparnis und der wirtschaftliche Nutzen wurden noch nicht durch eine vergleichende Zeitmessung im realen Recruiting-Prozess bestätigt.

## 9. Projektstatus

**Stand: 22. Oktober 2026**

Der technische Prototyp wurde implementiert und mehrfach mit echten KI-Aufrufen getestet.

Der Workflow ist derzeit nicht produktiv veröffentlicht.

Weitere Schritte für einen produktiven Einsatz wären insbesondere die Behebung der bekannten Einschränkungen, eine vollständige fachliche Qualitätssicherung, ein abgesicherter Webhook-Zugang und die Prüfung der Datenschutzanforderungen.

## 10. Fazit

Der Fachkrafthaus AI Recruiting Assistant zeigt, wie generative KI und Workflow-Automatisierung im Recruiting kombiniert werden können.

Das Projekt verdeutlicht sowohl den praktischen Nutzen einer KI-gestützten Stellenanalyse als auch die Bedeutung von Validierung, Fehlerbehandlung, transparenter Evaluation und menschlicher Qualitätskontrolle.

**Die zentrale Erkenntnis:** Eine technisch erfolgreiche KI-Ausgabe ist nicht automatisch eine fachlich korrekte Recruiting-Analyse.

---

*Projekt: Fachkrafthaus AI Recruiting Assistant – IHK-Capstone 2026*
