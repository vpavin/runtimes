---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Lernprogramm 'Einführung'

* {: download} Herzlichen Glückwunsch! Sie haben die Hello World-Beispielanwendung unter {{site.data.keyword.Bluemix}} bereitgestellt!  Befolgen Sie diesen schrittweisen Leitfaden, um zu starten. Oder laden Sie den <a class="xref" href="http://bluemix.net" target="_blank" title="(Beispielcode herunterladen)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Anwendungscode herunterladen" />Beispielcode herunter</a> und beginnen Sie auf eigene Faust.

Wenn Sie dem Go-Lernprogramm zur Einführung folgen, werden Sie eine Entwicklungsumgebung einrichten, eine App lokal und unter {{site.data.keyword.Bluemix}} bereitstellen und einen {{site.data.keyword.Bluemix_notm}}-Datenbankservice in Ihre App integrieren.

## Vorbemerkungen
{: #prereqs}

Sie benötigen Folgendes:
* [{{site.data.keyword.Bluemix_notm}}-Konto](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry-CLI ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://git-scm.com/downloads){: new_window}
* [Go ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://golang.org/dl/){: new_window}

## Schritt 1: Klonen Sie die Beispielapp.
{: #clone}

Zuerst richten wir die lokale Umgebung ein, indem wir sicherstellen, dass alle GO-Umgebungsvariablen ordnungsgemäß definiert wurden. Beispiel:
```
mkdir $HOME/work
export GOPATH=$HOME/work
export PATH=$PATH:$GOPATH/bin
```

Ändern Sie den Pfad in $GOPATH/src
```
mkdir $GOPATH/src
cd $GOPATH/src
```

Jetzt können Sie beginnen, mit der einfachen Go-App *hello world* zu arbeiten. Klonen Sie das Repository und wechseln Sie in das Verzeichnis, in dem sich die Beispielapp befindet.
```
go get github.com/IBM-Bluemix/get-started-go
```
{: pre}
```
cd github.com/IBM-Bluemix/get-started-go
```
{: pre}

Lesen Sie die Dateien im Verzeichnis *get-started-go*, um sich mit deren Inhalt vertraut zu machen.

## Schritt 2: Führen Sie die App lokal aus.
{: #run_locally}

  {: pre}

  Erstellen Sie einen Build und führen Sie die App aus.
  ```
make
  ```
  {: pre}

  ```
go run main.go
  ```
  {: pre}

  Ihre App finden Sie unter http://localhost:8080.

Verwenden Sie *Strg-c* zum Stoppen der App in demselben Fenster, in dem Sie die App gestartet haben.
{: tip}

## Schritt 3: Bereiten Sie die App für die Bereitstellung vor.
{: #prepare}

Für die Bereitstellung unter {{site.data.keyword.Bluemix_notm}} kann es hilfreich sein, die Datei 'manifest.yml' zu installieren. Die Datei 'manifest.yml' enthält Basisinformationen zu Ihrer App wie den Namen, wieviel Speicher für jede Instanz zugeordnet werden soll und die Route. Wir haben eine Beispieldatei 'manifest.yml' im Verzeichnis `get-started-go` bereitgestellt.

Öffnen Sie die Datei 'manifest.yml' und ändern Sie die Angabe für `name` von `GetStartedGo` in den Namen Ihrer App <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedGo
   random-route: true
   memory: 128M
   buildpack: go_buildpack
  ```
  {: codeblock}

In dieser Datei 'manifest.yml' generiert **random-route: true** eine zufällige Route für Ihre App, um zu verhindern, dass Ihre Route mit anderen Routen kollidiert.  Wenn Sie möchten, können Sie **random-route: true** durch **host: myChosenHostName** ersetzen und einen Hostnamen Ihrer Wahl angeben. [Weitere Informationen...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## Schritt 4: Stellen Sie die App bereit.
{: #deploy}
Sie können die Cloud Foundry-CLI verwenden, um Apps bereitzustellen.

Wählen Sie Ihren API-Endpunkt aus.
   ```
cf api <API-endpoint>
   ```
   {: pre}

Ersetzen Sie *API-endpoint* im Befehl durch einen API-Endpunkt aus der folgenden Liste:

| **Name der Region** | **Standort** | **API-Endpunkt** |
|-----------------|-------------------------|-------------------|
| Region USA (Süden) | Dallas, USA | api.ng.bluemix.net |
| Region USA (Osten) | Washington, DC, USA | api.us-east.bluemix.net |
| Region Großbritannien | London, England | api.eu-gb.bluemix.net |
| Region Sydney | Sydney, Australien | api.au-syd.bluemix.net |
| Region Deutschland | Frankfurt, Deutschland | api.eu-de.bluemix.net |
{: caption="Tabelle 1. {{site.data.keyword.cloud_notm}}-Regionsliste" caption-side="top"}

Melden Sie sich an Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an.

  ```
cf login
  ```
  {: pre}

Wenn Sie sich nicht über den Befehl `cf login` oder `bx login` anmelden können, weil Sie über eine eingebundene Benutzer-ID verfügen, verwenden Sie entweder den Befehl `cf login --sso` oder den Befehl `bx login --sso`, um sich mit Ihrer Single-Sign-on-ID anzumelden. Weitere Informationen finden Sie unter [Mit eingebundener ID anmelden](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id).

Übertragen Sie Ihre App mit einer Push-Operation aus dem Verzeichnis *get-started-go* an {{site.data.keyword.Bluemix_notm}}.
  ```
cf push
  ```
  {: pre}

Dieser Vorgang kann einige Minuten dauern. Falls ein Fehler im Bereitstellungsprozess auftritt, können Sie mithilfe des Befehls `cf logs <Your-App-Name> --recent` nach dem Fehler suchen.

Wenn die Bereitstellung abgeschlossen ist, sollten Sie eine Nachricht sehen, die anzeigt, dass Ihre App ausgeführt wird.  Ihre App wird an der URL angezeigt, die in der Ausgabe der Push-Operation aufgelistet ist. Sie können auch den Befehl

   ```
cf apps
    ```
  {: pre}
ausgeben, um Ihren Appstatus und die URL anzuzeigen.

## Schritt 5: Fügen Sie eine Datenbank hinzu.
{: #add_database}

Als Nächstes werden wir eine NoSQL-Datenbank zu dieser Anwendung hinzufügen und die Anwendung so einrichten, dass sie lokal und unter {{site.data.keyword.Bluemix_notm}} ausgeführt werden kann.

1. Melden Sie sich in Ihrem Browser bei {{site.data.keyword.Bluemix_notm}} an und wechseln Sie in das Dashboard. Wählen Sie **Ressource erstellen** aus.
2. Wählen Sie den Abschnitt **Data and Analytics** und anschließend **Cloudant NoSQL DB** aus und erstellen Sie Ihren Service.
3. Rufen Sie die Ansicht **Verbindungen** auf. Wählen Sie Ihre Anwendung und anschließend **Verbindung erstellen** aus.
4. Wählen Sie **Erneutes Staging** aus, wenn Sie dazu aufgefordert werden. {{site.data.keyword.Bluemix_notm}} startet Ihre Anwendung erneut und bietet die Datenbankberechtigungsnachweise für Ihre Anwendung unter Verwendung der Umgebungsvariablen `VCAP_SERVICES`. Diese Umgebungsvariable ist nur dann für die Anwendung verfügbar, wenn Sie unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Umgebungsvariablen ermöglichen es Ihnen, die Bereitstellungseinstellungen von Ihrem Quellcode zu trennen. Anstelle der festen Codierung eines Datenbankkennworts können Sie dieses in einer Umgebungsvariablen speichern, auf die Sie in Ihrem Quellcode verweisen. [Weitere Informationen...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Schritt 6: Verwenden Sie die Datenbank.
{: #use_database}
Wir werden jetzt Ihren lokalen Code aktualisieren, um auf diese Datenbank zu verweisen. Wir erstellen nun eine json-Datei, die die Berechtigungsnachweise für die Services speichert, die die Anwendung verwendet. Diese Datei wird NUR dann verwendet, wenn die Anwendung lokal ausgeführt wird. Bei der Ausführung in {{site.data.keyword.Bluemix_notm}} werden die Berechtigungsnachweise aus der Umgebungsvariablen VCAP_SERVICES gelesen.

1. Erstellen Sie eine Datei mit dem Namen `.env` im Verzeichnis `get-started-go` mit dem folgenden Inhalt:
  ```
  CLOUDANT_URL=
  ```
  {: pre}

2. Kehren Sie in die Benutzerschnittstelle von {{site.data.keyword.Bluemix_notm}} zurück und wählen Sie Ihre App -> Verbindungen -> Cloudant -> Berechtigungsnachweise anzeigen aus.

3. Kopieren Sie einfach die `url` aus den Berechtigungsnachweisen in das Feld `CLOUDANT_URL` der Datei `.env` und speichern Sie die Änderungen.  Als Ergebnis erhalten Sie in etwa Folgendes:
  ```
  CLOUDANT_URL=https://123456789 ... bluemix.cloudant.com
  ```

4. Führen Sie Ihre Anwendung lokal aus.
  ```
go run main.go
  ```
  {: pre}

  Ihre App finden Sie unter: http://localhost:8080. Alle Namen, die Sie in die App eingegeben haben, werden jetzt zur Datenbank hinzugefügt.

  Ihre lokale App und die {{site.data.keyword.Bluemix_notm}}-App verwenden die Datenbank gemeinsam.  Ihre {{site.data.keyword.Bluemix_notm}}-App wird an der URL angezeigt, die in der Ausgabe der oben erwähnten Push-Operation aufgelistet ist.  Namen, die Sie in einer der Apps eingeben, sollten nach einer Aktualisierung des Browsers in beiden angezeigt werden.


Denken Sie daran, dass Sie Ihre App stoppen, wenn Sie nicht benötigt wird, damit Ihnen nicht unerwartete Gebühren belastet werden.
{: tip}

## Nächste Schritte

* [Lernprogramme](/docs/tutorials/index.html)
* [Beispiele ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
