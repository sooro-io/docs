---
navigation:
  order: 2
  title: Erste Schritte
---

# Erste Schritte

Dieser Leitfaden führt dich durch die Einrichtung und Bereitstellung deines ersten GTM-Tagging-Servers. Er zeigt dir zudem, wie du mit dem serverseitigen Tagging beginnen kannst.

## Voraussetzungen

1. GTM-Konto mit einem Webcontainer
2. GTM-Benutzer mit Administrator-Rolle
3. GA4-Konto mit einem Web-Datenstream
4. Sooro-Konto

## Schritt 1: Erstellen Sie einen Servercontainer

Lass uns mit der Erstellung des Google Tag Manager Server Containers beginnen. Öffnen dazu https://tagmanager.google.com und starte den Erstellungsprozess über die drei Punkte oben rechts beim gewünschten Konto. Wählen Sie im Kontextmenü die Aktion **Container erstellen**.

![starte die Erstellung eines neuen Containers in GTM](/assets/images/gtm-tagging-server-hosting/get-started/open-container-creation-dialog.webp)

Lege den Namen und Typ des Containers in dem sich öffnenden Fenster (Slide-Over) an. Grundlegend kann zwar jeder beliebige Name verwendet werden, wir empfehlen jedoch, im Namen auch die Art des Containers anzugeben. Dies erleichtert später die Unterscheidung, um schnell festzustellen, in welchem Container man sich gerade befindet.

Wähle als Zielplattform **Server**. Anschließend kannst du den Container erstellen, indem du oben rechts auf **Erstellen** klickst.

![erstelle einen Servercontainer durch die Auswahl der Zielplatform Server](/assets/images/gtm-tagging-server-hosting/get-started/create-gtm-server-container.webp)

Du wirst automatisch zum neu erstellten Servercontainer weitergeleitet. Es gilt jetzt die Wahl zu Treffen, wie deine Tagging-Server bereitgestellt werden. Wähle hier **Tagging-Server manuell bereitstellen** und **kopiere** die sogenannte _Containerkonfiguration_.

Bei der Containerkonfiguration handelt es sich um in Base64 kodierte Informationen, die neben der Container ID auch einen Autorisierungsschlüssel enthält. Deine Tagging-Server benötigen diese Informationen, damit sie deine Konfiguration aus dem Servercontainer abrufen können.

![wählen „Tagging-Server manuell bereitstellen“ und kopiere die Containerkonfiguration](/assets/images/gtm-tagging-server-hosting/get-started/provision-of-tagging-servers.webp)

## Schritt 2: Erstelle dein Tagging-Server

Öffne [https://www.sooro.io/app/organizations](https://www.sooro.io/app/organizations) und wähle die Organisation aus, für die du den Tagging-Server erstellen möchtest. Auf der folgenden Seite kannst du mit der Erstellung beginnen, indem du in der Mitte des Bildschirms auf die Schaltfläche **Set up your first GTM Tagging Server** klicks. Falls du bereits einen GTM Tagging Server hast, verwenden den rechts oben den Button **New GTM Tagging Server**.

Gebe als erstes den **Namen** des GTM Tagging Servers an. Um die Zuordnung zu erleichtern, empfehlen wir dir, den selben Namen zu verwenden den du im GTM verwendest. Die gewählte **Server Location** sollte in der Nähe deiner Kunden liegen, damit Anfragen schneller bearbeitet werden. Fügen unter **Container Configuration** den Wert ein, den du am Ende des ersten Schritts kopiert hast. Falls dieser nicht mehr verfügbar ist, kannst du die Containerkonfiguration jederzeit in deinem GTM Server Container finden. Gehe dafür auf **Verwaltung** > **Containereinstellungen** > **Tagging-Server einrichten** > **Tagging-Server manuell bereitstellen**.

![erstelle einen GTM Tagging Server](/assets/images/gtm-tagging-server-hosting/get-started/create-gtm-tagging-server.webp)

Sobald du den Tagging Server erstellt hast, wirst du zur Bestätigungsseite weitergeleitet. Die hier angezeigte URL stellt die Servercontainer-URL dar, die im GTM Server Container gespeichert werden muss. Dies ist notwendig, um die Verschau-Funktionalitäten zu aktivieren. Gehe hierfür zu deinem GTM Server Container und öffne die Einstellungen über **Verwaltung** > **Containereinstellungen**. Klicke auf **URL hinzufügen** und **füge** die Servercontainer-URL **ein**. **Speicher** die Änderungen um den Schritt abzuschließen.

![ergänze die Servercontainer URL in den Einstellungen deines Servercontainers](/assets/images/gtm-tagging-server-hosting/get-started/add-tagging-server-url.webp)

In der Zwischenzeit sollten dein GTM Tagging Server bereitgestellt und einsatzbereit sein. Wenn du auf der Bestätigungsseite deines GTM Tagging Server auf **Go to GTM Tagging Server** klickst, wirst du zur Detailseite weitergeleitet. Bitte überprüfe hier den Status deines Servers. Falls dieser einen Fehler anzeigt, überprüfe den Wert der **Container Configuration** auf der Registerkarte **Settings**. Wenn du den Fehler nicht selbständig beheben kannst, [nimm bitte Kontakt mit uns auf](mailto:support@sooro.io?subject=Fehler%20bei%20der%20Konfiguration-%20GTM%20Tagging%20Server%20Hosting).

## Schritt 3: Konfiguration deines Web- und Servercontainers

Es ist an der Zeit, dass server-seitige Tracking zu implementieren. Im folgenden gehen wir zunächst auf die Änderungen im Webcontainer ein, um anschließend die notwendige Konfiguration im Servercontainer aufzuzeigen.

Gehe erneut zu https://tagmanager.google.com, wählen den Webcontainer aus und erstelle einen neuen Arbeitsbereich. Klicke auf **Tags** > **Neu**, um mit der Erstellung eines **Google-Tag** zu beginnen. Gebe deine **Google Analytics 4 - Mess-ID** als **Tag-ID** an. Füge unter **Konfigurationseinstellungen** > **Konfigurationsparameter** einen Eintrag für `server_container_url` hinzu. Als Wert verwendest du die URL, unter welcher dein Tagging-Server erreichbar ist (Servercontainer-URL). Es handelt sich dabei um die URL, welche du im vorherigen Schritts in den Containereinstellungen deines Servercontainers hinterlegt hast. Fügen den den auslösenden Trigger **All Page** hinzu und speichere dann den Tag.

![erstelle einen Google-Tag mit dem Parameter server_container_url](/assets/images/gtm-tagging-server-hosting/get-started/create-google-tag.webp)

Am besten öffnest du in einem weiteren Tab deines Browser deinen Servercontainer. Erstelle auch hier einen neuen Arbeitsbereich.

Damit dein Tagging-Server die eingehenden Ereignisse verarbeiten kann, muss ein sogenannter Client erstellt werden. Gehen dazu auf **Clients** > **Neu**, um einen **Google Analytics: GA4 (Web)** Client zu erstellen. Nach der Auswahl des Clienttyps muss außer dem Namen nichts weiter geändert werden, sodass du gleich **Speichern** kannst.

![erstelle einen "Google Analytics: GA4 (Web)" Client im Servercontainer](/assets/images/gtm-tagging-server-hosting/get-started/create-google-analytics-4-client.webp)

Wir brauchen noch ein letztes Element: einen Tag. Wie üblich kannst du mit dessen Erstellung beginnen, indem du auf **Tags** > **Neu** klickst. Wähle **Google Analytics: GA4** als **Tag-Typ** aus. Du musst dem Tag lediglich einen Namen geben und einen Trigger festlegen. Die Tag-Vorlage extrahiert automatisch alle relevanten Daten aus den Events und ermittelt die Werte für Felder, Eigenschaften und Parameter. Voraussetzung hierfür ist, dass das Event von einem GA4-Tag oder Google-Tag mit GA4-Konfiguration aus dem Webcontainer stammt.

Fügen den den auslösenden Trigger **All Pages** hinzu und klicke auf **Speichern**, um fortzufahren.

![erstelle einen GA4 Server Tag](/assets/images/gtm-tagging-server-hosting/get-started/create-google-analytics-4-page-view-at-server-side.webp)

## Schritt 4: Starten der Vorschau

Alle Elemente sind jetzt vorhanden, um dein server-seitiges Tagging in Aktion sehen zu können. Start den Vorschaumodus im Server- und Webcontainer.

Sobald du mit deiner Seite interagierst, werden verschiedene Ereignisse im Servercontainer angezeigt. Der Vorschaumodus des Server-Containers sieht etwas anders aus, als man es vom Web-Container gewohnt ist. Im Kern ist er jedoch sehr ähnlich. Schaue dir einmal die verschiedenen Reiter und Elemente im Detail an, um dich mit diesen vertraut zu machen.

Wenn du auf einen ausgelösten Tag klickst, kannst du dessen Details einsehen. Es besteht zudem die Möglichkeit den genauen HTTP-Request einzusehen, indem auf den ausgehenden Request klickst.

![du kannst mittels Klick auf den ausgehenden HTTP-Request einen detailierten Blick auf den Request erhalten](/assets/images/gtm-tagging-server-hosting/get-started/preview-mode-of-server-container.webp)

## Nächste Schritte

Du hat nun alle relevanten Elemente kennengelernt, um mit dem serverseitigen Tagging zu beginnen. Jetzt liegt es an dir, die gerade erstellte Integration zu erweitern oder mit einer völlig Neuen zu beginnen.
