# Abschlussbericht – Fachkrafthaus AI Recruiting Assistant
**Stand:** 23.10.2026 · **Status:** Technisch getesteter Prototyp, nicht produktiv freigegeben

## Ausgangslage und Ziel
Die manuelle Voranalyse neuer Stellenanfragen bindet Zeit: Muss- und Wunschkriterien trennen, alternative Berufsbezeichnungen prüfen, Suchbegriffe für Active Sourcing formulieren und offene Kundenfragen erkennen. Das Projekt erprobt, ob diese Vorbereitung mit einer KI-gestützten n8n-Automatisierung reproduzierbar strukturiert werden kann.

## Lösung und Architektur
Der n8n-Workflow besteht aus acht Knoten: Webhook → Eingabevalidierung → Pflichtfeld-IF → GPT-4.1-Analyse → formale JSON-Prüfung → Gültigkeits-IF → Erfolgs- oder Fehlerantwort. Der Systemprompt verlangt strukturierte Aussagen, Warnungen und Rückfragen und untersagt autonome Einstellungsentscheidungen. Die Ausgabe ist ausdrücklich ein **KI-Entwurf mit menschlicher Qualitätskontrolle**.

## Evaluation und Messwerte
Es liegen 20 dokumentierte reale OpenAI-Ausführungen mit synthetischen Stellenanfragen vor (n8n Exec 44–63). Die Eingaben wurden im n8n-Lauf injiziert, **nicht** über einen externen HTTP-Webhook gesendet.
- 19/20: reguläre Antwort (95 % technische Erfolgsantwortquote)
- 1/20: kontrollierter KI_FEHLER / 502 (Test E-19)
- Zeit innerhalb von n8n: 1,77–4,28 Sekunden, Mittel ca. 2,62 Sekunden
- 14 weitere Prüf-Node-Regressionstests mit simulierten KI-Antworten, Exec 29–42
- **Keine unabhängige fachliche Erfolgsquote verfügbar.** Die in TESTPROTOKOLL.md notierten fachlichen Auffälligkeiten stammen aus Vorbewertungen, nicht aus einer unabhängigen Expertenbeurteilung.

## Wichtigste Fehler und Grenzen
1. **E-19:** Zu vage Anforderung: Das Modell gibt zu Recht kaum belastbare Suchbegriffe aus; eine harte Regel für mindestens drei Begriffe verwirft dennoch sinnvolle Rückfragen und liefert 502. Verbesserungsansatz: eigener Status RUECKFRAGE_NOETIG.
2. **RG-03:** Eingabewerte mit falschem Typ werden bislang zu Strings umgewandelt statt vor dem KI-Aufruf mit 400 abgelehnt.
3. Teilweise unpräzise Widerspruchsbehandlung, zu generische Suchbegriffe und partieller Einfluss manipulativer Eingabetexte.
4. Externer Webhook-POST auf die Test-URL bisher 404, weil der Listener nicht aktiv war; daher **kein erfolgreicher externer HTTP-End-to-End-Nachweis**.
5. Ein echter OpenAI-Ausfall wurde im Gesamtfluss nicht nachgewiesen.

Diese Einschränkungen werden als Projektbefunde ausgewiesen, nicht verschwiegen.

## Wirtschaftlichkeitsbetrachtung
**Gemessen:** Technische Workflow-Laufzeiten von durchschnittlich ca. 2,62 Sekunden. **Nicht gemessen:** Tatsächliche Arbeitszeit eines Recruiters mit und ohne Assistenzsystem sowie die Qualität nach menschlicher Nachbearbeitung.

**Annahmenszenario, kein Messergebnis:** Bei 40 Stellenanalysen pro Monat und hypothetisch 8 Minuten Netto-Zeitersparnis je Anfrage wären das 320 Minuten = 5,33 Stunden pro Monat. Bei angenommenen internen Vollkosten von 35 €/Stunde entspräche das einem rechnerischen Bruttonutzen von rund 187 €/Monat vor Lizenz-, API-, Prüf- und Wartungskosten. Diese Werte sind zu validieren; ein tatsächlicher ROI ist nicht belegt.

## Datenschutz, Verantwortung und Governance
Im Test wurden ausschließlich **synthetische Stellenanfragen** verwendet, keine Kandidatenprofile. Der Workflow versendet keine Nachrichten und fällt keine Personalentscheidungen. Vor einem Realeinsatz sind zu prüfen: Rechtsgrundlagen und Transparenz, Auftragsverarbeitung, technische und organisatorische Maßnahmen, Lösch- und Zugriffskonzept, Datenminimierung, n8n-/KI-Anbieterbedingungen, menschliche Qualitätsprüfung und risikobasierte KI-Governance. Eine abschließende rechtliche Konformitätsbescheinigung liegt nicht vor.

## Reflexion
Die zentrale Erkenntnis lautet: **Technisch valides JSON ist kein Beweis für fachlich richtige Recruiting-Empfehlungen.** Die Kombination aus generativer KI, regelbasierter Validierung, Fehlertests und menschlicher Freigabe ist deshalb der sinnvollere Ansatz.

## Artefakte und Nachweise
- `README.md`: Projektüberblick
- `TESTPROTOKOLL.md`: Test-IDs und Ergebnisse
- JSON-Workflow-Datei: exportierter technischer Stand
- Screenshot: grafische Workflowdarstellung

## Offen für formale Abgabe
Unabhängige fachliche Bewertung der 20 Szenarien, echter HTTP-Test, Peer-Review durch eine andere Person sowie persönliche Prüfung/Einreichung in Codio sind **nicht belegt** und dürfen nicht als abgeschlossen bezeichnet werden.
