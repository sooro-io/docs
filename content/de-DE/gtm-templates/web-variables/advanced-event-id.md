---
navigation:
  order: 1
  title: Advanced Event ID
---

# Advanced Event ID

Diese GTM-Variablen-Vorlage ermöglicht es dir, eine eindeutige Event ID zu generieren.

Die Variable ist besonders hilfreich, wenn du einen hybriden Ansatz in deinem Tracking verwendest. Das bedeutet, dass du client- und serverseitiges Tracking gleichzeitig einsetzt. In diesem Szenario können Ereignisse doppelt getrackt werden, was du vermeiden möchtest.

Die Lösung dafür ist die sogenannte Event-Deduplizierung. Um Ereignisse zu deduplizieren, ist ein Identifikator erforderlich, meist eine Event ID. Folglich benötigst du für jedes einzelne Ereignis, das du trackst, eine eindeutige Event ID. Leider ist eine solche ID oft nicht verfügbar.

Unsere Vorlage hilft dir, dieses Problem zu lösen, indem sie Event IDs für dich erstellt.

## Wie es funktioniert

Eine Event ID kann mithilfe verschiedener verfügbarer Datenpunkte erstellt werden. Die gute Nachricht ist, dass der GTM selbst einige sehr nützliche Informationen für diese Aufgabe bereitstellt. Wenn du jedoch nur diese verwendest, könnte leicht eine ID-Kollision auftreten. Also den Fall, dass zwei identische IDs generiert werden. Um dies zu vermeiden, kommt ein weiteres Element ins Spiel, um die Einzigartigkeit der Event IDs zu gewährleisten.

In unserer Vorlage verwenden wir die folgenden Datenpunkte, um die Event IDs zu erstellen:

- Eindeutigkeitselement (eine Client-ID oder etwas ähnliches)
- GTM Start
- GTM unique Event ID (die ist aber nicht so einzigartig, wie sie klingt)

Wenn ein Element nicht verfügbar ist, gibt es immer einen Fallback. Dies stellt sicher, dass du eigentlich immer eine eindeutige Ereignis-ID erstellen kannst.

## Konfiguration

Die Konfiguration der Variablen sollte schnell gehen, da es nur wenige Optionen gibt. Aber sie sind leistungsstark genug, dass du in deinem gesamten GTM-Container nur eine einzige Event-ID-Variable erstellen brauchst.

### Uniqness Element (Eindeutigkeitselement)

Dieses Element stellt sicher, dass die erstellten Event IDs einzigartig sind. Idealerweise hast du in deinem Tracking eine Client ID, die du dafür verwenden kannst.

Wenn nicht, kannst du auch die Option wählen, eine ID basierend auf einer Zufallszahl und einem Zeitstempel zu generieren. Wir empfehlen, dass das Eindeutigkeitselement für einen einzelnen Client möglichst statisch ist. Daher bietet dir die Vorlage zwei Optionen für das Caching. Du kannst das Caching auch vollständig deaktivieren, wenn du datenschutzrechtliche Bedenken hast.

#### Caching Behavior (Caching Verhalten)

<blockqoute type="tip" isSingleParagraph>
Wenn du eine der beiden Caching-Option wählst, findest du den generierten Wert unter dem Schlüssel `gtmClientId` (entweder im window-Objekt oder im localStorage). Da der generierte Wert so etwas wie eine Client-ID ist, könnte er dir an anderer Stelle hilfreich sein.
</blockqoute>

- **temporary (temporär)**  
  Das Eindeutigkeitselement wird vorübergehend im window-Objekt des Browsers zwischengespeichert. Es wird gelöscht, sobald du den Tab oder den Browser schließt.

- **persistent**  
  Das Eindeutigkeitselement wird im localStorage des Browsers zwischengespeichert. Der Wert bleibt daher über mehrere Sitzungen und sogar über Tabs in deinem Browser hinweg gleich.

<blockqoute type="warning" isSingleParagraph>
Wenn du die Option **persistent** verwendest, werden Informationen dauerhaft auf den Geräten von Endnutzern gespeichert. Es kann daher erforderlich sein, die Informationen in deinem Zustimmungsbanner und/oder deiner Datenschutzrichtlinie anzupassen, um die gesetzlichen Anforderungen zu erfüllen.
</blockqoute>

### Override Rules (Überschreibungsregeln)

Es gibt immer Situationen, in denen eine eindeutige ID, die aus deinen Systemen stammt, von Vorteil ist. Beispielsweise könnte ein Nutzer eine bestimmte Seite neu laden, sodass das Tracking erneut ausgelöst wird. Bei wichtigen Ereignissen (z.B. Kauf) würde dies zu einer Verzerrung in der Berichterstellung oder der Optimierung von Marketing-Kampagnen führen. Um dieses Problem zu umgehen, bieten wir dir die Möglichkeit, die Event ID zu überschreiben.

**use GA4 transaction ID (GA4-Transaktions-ID verwenden)**

Wenn dein Tracking auf GA4-Ereignissen basiert, kannst du die im purchase-Event angegebene Transaktions-ID verwenden.

**Special IDs (Spezielle IDs)**

Du kannst hier so viele Einträge vornehmen, wie du möchtest, wenn du deine eigene Event ID verwenden möchtest. Gib dazu den Ereignisnamen und deine vorhandene ID ein.

## Gut zu wissen

Im Code des Vorlage gibt es verschiedene Fallbacks, sodass immer eine Event ID generiert wird. Daher ist ein undefinierter Wert in einer deiner Eingaben kein Problem.
