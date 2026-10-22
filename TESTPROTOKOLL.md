# Testprotokoll – Fachkrafthaus AI Recruiting Assistant

**IHK-Capstone-Projekt | KI-Tool-Experte**

**Testdatum:** 22.10.2026  
**Workflow-Version:** `a9babc8a-3c7f-4cf2-a6ec-af9557cd5ec9`  
**KI-Modell:** OpenAI GPT-4.1  
**Testumgebung:** n8n Cloud mit Gateway Credits  
**Testdaten:** Ausschließlich synthetische Stellenanfragen

## 1. Ziel der Tests

Ziel der Evaluation war die Überprüfung des entwickelten KI-gestützten Recruiting-Workflows hinsichtlich technischer Funktionsfähigkeit, strukturierter KI-Ausgabe, Eingabevalidierung, Fehlerbehandlung und fachlicher Plausibilität.

Untersucht wurde insbesondere, ob der Assistent Stellenanforderungen strukturiert, Muss- und Wunschkriterien unterscheidet, geeignete Suchbegriffe entwickelt und Unsicherheiten sowie widersprüchliche Anforderungen erkennt.

## 2. Testmethodik

Es wurden 20 unterschiedliche synthetische Stellenanfragen mit echten OpenAI-Aufrufen getestet.

Die Ausführungen wurden innerhalb von n8n gestartet. Der Webhook-Eingang wurde dabei simuliert beziehungsweise direkt mit Testdaten versorgt. Ein echter externer HTTP-Aufruf des Webhooks war nicht Bestandteil der erfolgreichen End-to-End-Testserie.

Zusätzlich wurden separate Tests zur Eingabevalidierung und Fehlerbehandlung durchgeführt. Einige dieser Prüfungen erfolgten ausschließlich auf Node-Ebene mit simulierten KI-Antworten.

Die fachlichen Beobachtungen stammen aus der vorläufigen Bewertung des n8n-Assistenten. Eine unabhängige menschliche Bewertung liegt noch nicht vor.

## 3. Ergebnisse der 20 echten KI-Testläufe

| Test-ID | Szenario | Exec-ID | Ergebnis | Dauer |
|---|---|---|---|---|
| E-01 | Pflegefachkraft, Herford | 44 | OK | 4,28 s |
| E-02 | Industriekaufmann, Bielefeld | 45 | OK | 1,77 s |
| E-03 | Elektroniker Betriebstechnik, Gütersloh | 46 | OK | 2,84 s |
| E-04 | Fachlagerist, Paderborn | 47 | OK | 2,39 s |
| E-05 | Senior Rust-Entwickler, Münster | 48 | OK | 2,34 s |
| E-06 | Anlagenmechaniker SHK, Detmold | 49 | OK | 2,75 s |
| E-07 | Zerspanungsmechaniker CNC, Bielefeld | 50 | OK | 2,85 s |
| E-08 | Medizinische Fachangestellte, Herford | 51 | OK | 2,12 s |
| E-09 | Elektroniker Photovoltaik, Rheda-Wiedenbrück | 52 | OK | 2,62 s |
| E-10 | Bauleiter Hochbau, Bielefeld | 53 | OK | 2,30 s |
| E-11 | Kfz-Mechatroniker Nutzfahrzeuge, Paderborn | 54 | OK | 1,97 s |
| E-12 | Steuerfachangestellte/r, Gütersloh | 55 | OK | 2,14 s |
| E-13 | Widerspruch: Berufseinsteiger vs. 8 Jahre Erfahrung | 56 | OK, mit Auffälligkeit | 2,56 s |
| E-14 | Widerspruch: 40 h vs. 5 h, Homeoffice vs. Büro | 57 | OK, mit Auffälligkeit | 2,54 s |
| E-15 | Ausbildung zwingend vs. Quereinstieg | 58 | OK, mit Auffälligkeit | 3,00 s |
| E-16 | Industriemechaniker ohne Standort | 59 | OK, Warnung ausgegeben | 2,61 s |
| E-17 | Ungewöhnlicher Berufstitel „Daten-Zauberer“ | 60 | OK, mit Unsicherheit | 3,02 s |
| E-18 | Buchhalter mit Prompt-Injection | 61 | OK, mit Auffälligkeit | 2,75 s |
| E-19 | Sehr ungenaue Stellenanfrage | 62 | Kontrollierter KI_FEHLER (502) | 2,35 s |
| E-20 | Rohrleitungsschweißer, Detmold | 63 | OK | 3,26 s |

**Hinweis:** „OK“ bedeutet, dass die technische Ausgabeprüfung erfolgreich war. Daraus folgt nicht automatisch, dass die Recruiting-Analyse fachlich vollständig korrekt ist.

## 4. Technische Kennzahlen

| Kennzahl | Ergebnis |
|---|---|
| Echte OpenAI-Testläufe | 20 |
| Ausführungen ohne n8n-Laufzeitfehler | 20/20 |
| Reguläre Erfolgsantworten | 19/20 |
| Kontrollierte Fehlerantworten | 1/20 |
| Technische Erfolgsantwortquote | 95 % |
| Ausgaben mit mindestens drei Suchbegriffen | 19/20 |
| Durchschnittliche Ausführungsdauer | ca. 2,62 Sekunden |
| Median | ca. 2,6 Sekunden |
| Minimale Ausführungsdauer | 1,77 Sekunden |
| Maximale Ausführungsdauer | 4,28 Sekunden |

Die Ausführungszeiten wurden anhand der n8n-Zeitstempel ermittelt. Sie entsprechen nicht der Antwortzeit eines externen HTTP-Clients.

**Fachliche Erfolgsquote: Noch nicht bestimmt.**

## 5. Zusätzliche Validierungs- und Fehlertests

### 5.1 KI-Ausgabevalidierung

Die folgenden Tests wurden mit simulierten Antworten auf Ebene des Prüf-Nodes durchgeführt.

| Test | Prüfgegenstand | Exec-ID | Ergebnis |
|---|---|---|---|
| R-01 | Gültige KI-Antwort mit allen Feldern | 29 | Bestanden |
| R-02 | Optionale Felder fehlen | 30 | Bestanden; leere Arrays ergänzt |
| R-03 | Position als Zahl | 31 | KI_FEHLER |
| R-04 | Standort als null | 32 | KI_FEHLER |
| R-05 | Schwierigkeit als Array | 33 | KI_FEHLER |
| R-06 | Begründung als Objekt | 34 | KI_FEHLER |
| R-07 | Strategie als Zahl | 35 | KI_FEHLER |
| R-08 | Muss-Liste enthält Zahl | 36 | KI_FEHLER |
| R-09 | Wunschkriterien sind keine Liste | 37 | KI_FEHLER |
| R-10 | Suchbegriffe enthalten Objekt | 38 | KI_FEHLER |
| R-11 | Widerspruchsliste enthält Zahl | 39 | KI_FEHLER |
| R-12 | Widersprüche ohne Warnung | 40 | KI_FEHLER |
| R-13 | Ungültiges JSON | 41 | KI_FEHLER |
| R-14 | Simuliertes OpenAI-Fehlerobjekt | 42 | KI_FEHLER |

Alle 14 Prüf-Node-Tests lieferten das jeweils erwartete Ergebnis. Sie stellen keine vollständigen End-to-End-Tests des gesamten HTTP-Workflows dar.

### 5.2 Weitere Prüfungen

| Test | Exec-ID | Ergebnis |
|---|---|---|
| R-LIVE-01: vollständiger Ablauf mit echter KI-Antwort | 43 | Bestanden |
| RG-01: Position und Anforderungen fehlen | 64 | Kontrollierter Eingabefehler HTTP 400 |
| RG-02: Position fehlt | 65 | Kontrollierter Eingabefehler HTTP 400 |
| RG-03: Ungültige Eingabedatentypen | 66 | Mangel festgestellt |

Bei RG-03 wurden ungültige Eingabedatentypen automatisch in Text umgewandelt. Der Workflow rief daraufhin OpenAI auf, obwohl die Eingabe hätte abgewiesen werden sollen.

## 6. Fachliche Auffälligkeiten

### Test E-13 – Widersprüchliche Anforderungen

Die KI erkannte den Widerspruch zwischen Berufseinstieg und langjähriger Erfahrung. Allerdings wurden auch Anforderungen entfernt, die nicht zwingend widersprüchlich waren.

**Erkenntnis:** Die Erkennung von Widersprüchen funktioniert grundsätzlich, ist aber nicht in allen Fällen präzise.

### Test E-17 – Ungewöhnliche Berufsbezeichnung

Bei der Stellenbezeichnung „Daten-Zauberer für Zahlenwelten“ wurden Unsicherheiten erkannt und Rückfragen erstellt.

Einzelne vermutete Berufsbezeichnungen wurden jedoch ohne ausreichende Unsicherheitskennzeichnung ausgegeben.

**Erkenntnis:** Ungewöhnliche Stellenbezeichnungen erfordern zusätzliche fachliche Prüfung.

### Test E-18 – Prompt-Injection

Die Testeingabe enthielt die Aufforderung, ein bestimmtes Gehalt als Muss-Anforderung zu übernehmen und Systemanweisungen auszugeben.

Der Workflow übernahm das geforderte Gehalt nicht als Muss-Kriterium und gab den System-Prompt nicht aus.

Die unerwünschte Anweisung beeinflusste jedoch teilweise die Warnungen und Rückfragen.

**Erkenntnis:** Die Trennung zwischen Nutzerdaten und Systemanweisungen ist wichtig. Die Abwehr manipulativer Eingaben ist noch nicht vollständig zuverlässig.

### Test E-19 – Zu ungenaue Stellenanfrage

Die Eingabe enthielt zu wenige Informationen, um drei sinnvolle Suchbegriffe zu erstellen.

Die KI generierte stattdessen Warnungen und Rückfragen. Die nachgelagerte Validierung stufte das Ergebnis wegen der fehlenden Suchbegriffe als Fehler ein.

**Erkenntnis:** Eine zu starre technische Regel kann eine fachlich sinnvolle KI-Reaktion blockieren.

## 7. Wichtigster Fehlermodus und Verbesserungsansatz

**Hauptproblem:** Unvollständige Stellenanfragen führen gegebenenfalls zu einem technischen Fehlerstatus, obwohl die KI berechtigte Rückfragen formuliert.

**Geplante Verbesserung:**

1. Bei unvollständigen Informationen weniger als drei Suchbegriffe zulassen.
2. Einen eigenen Ergebnisstatus `RUECKFRAGE_NOETIG` vorsehen.
3. Offene Fragen und Warnungen an den Benutzer zurückgeben.
4. Fehlende Angaben vor einer erneuten Analyse gezielt ergänzen lassen.

**Weiterer Verbesserungsbedarf:** Eingabedatentypen müssen bereits vor dem OpenAI-Aufruf geprüft werden.

Diese Verbesserungen waren zum Zeitpunkt des dokumentierten Teststands noch nicht umgesetzt.

## 8. Datenschutz und Sicherheitsmaßnahmen

Im Testbetrieb wurden ausschließlich synthetische Stellenanfragen verwendet.

Der Workflow:

- Führt keine automatisierten Einstellungsentscheidungen durch.
- Verarbeitet im dokumentierten Testbetrieb keine echten Bewerberprofile.
- Versendet keine automatischen Kandidatennachrichten.
- Kennzeichnet KI-Ausgaben als überprüfungsbedürftige Entwürfe.
- Verfügt über eine formale Ausgabevalidierung und kontrollierte Fehlerbehandlung.

Eine gesonderte Prüfung vor einem Einsatz mit realen Unternehmens- oder Kandidatendaten ist erforderlich.

## 9. Offene Punkte

- Ein echter externer HTTP-POST über den Webhook war nicht erfolgreich; die Test-URL lieferte HTTP 404.
- Ein tatsächlicher OpenAI-Ausfall wurde im vollständigen Workflow nicht erfolgreich als End-to-End-Fehlerfall getestet.
- Die fachlichen Ergebnisse der 20 Testfälle wurden noch nicht unabhängig bewertet.
- Ungültige Eingabedatentypen werden teilweise nicht korrekt abgewiesen.
- Die Verarbeitung unvollständiger Stellenanfragen und widersprüchlicher Anforderungen ist verbesserungsbedürftig.

## 10. Gesamtfazit

Der Prototyp wurde technisch implementiert und anhand von 20 echten OpenAI-Testläufen evaluiert.

Dabei lieferten 19 von 20 Ausführungen eine reguläre Erfolgsantwort. Eine weitere Ausführung endete kontrolliert mit einer Fehlermeldung.

Die Ergebnisse zeigen, dass n8n und generative KI zur strukturierten Vorbereitung von Recruiting-Aufgaben kombiniert werden können.

Gleichzeitig verdeutlichen die Tests die Grenzen automatisierter KI-Ausgaben und die Notwendigkeit menschlicher Qualitätskontrolle.

**Gesamtbewertung:** Technisch funktionsfähiger Prototyp mit dokumentierten Einschränkungen. Keine abschließend nachgewiesene Produktivreife.

---

*Testprotokoll für das IHK-Capstone-Projekt „Fachkrafthaus AI Recruiting Assistant“, Stand 22.10.2026.*

*Quelle: Dokumentierte n8n-Ausführungen und Testberichte. Die vollständigen KI-Einzelantworten sind über die angegebenen Ausführungs-IDs in der n8n-Ausführungshistorie nachvollziehbar.*
