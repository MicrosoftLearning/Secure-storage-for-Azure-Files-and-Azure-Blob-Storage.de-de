---
lab:
  title: 'Übung 02a: Bereitstellen von Speicher für die öffentliche Website'
  module: Guided Project - Azure Files and Azure Blobs
---
Die Unternehmenswebsite bietet Produktbilder, Videos, Marketingunterlagen und Kundenerfolgsgeschichten. Kund*innen gibt es auf der ganzen Welt und die Nachfrage wächst rasant. Die Inhalte sind unternehmenskritisch und erfordern Ladezeiten mit geringer Latenz. Es ist wichtig, die Dokumentversionen nachzuverfolgen und Dokumente schnell wiederherzustellen, wenn sie gelöscht werden.

## Architekturdiagramm

![Diagramm mit einem Speicherkonto und einem Blobcontainer](../Media/task-2.png)

## Qualifikationsaufgabe
- Erstellen eines Speicherkontos mit hoher Verfügbarkeit
- Sicherstellen von anonymem öffentlichem Zugriff für das Speicherkonto
- Erstellen eines Blobspeichercontainers für die Websitedokumente
- Aktivieren von vorläufigem Löschen zur einfachen Wiederherstellung von Dateien
- Aktivieren der Blobversionsverwaltung 

## Übungsanweisungen

## Erstellen eines Speicherkontos mit hoher Verfügbarkeit

1. Erstellen Sie ein Speicherkonto zur Unterstützung der öffentlichen Website.

    - Suchen Sie im Portal die Option `Storage accounts` und wählen Sie sie aus.  
    - Wählen Sie **+ Erstellen** aus. 
    - Wählen Sie unter **Ressourcengruppe** die Option **Neu** aus. Geben Sie einen **Namen** für Ihre Ressourcengruppe ein, und wählen Sie **OK** aus. 
    - Legen Sie `publicwebsite` als **Speicherkontonamen** fest. Stellen Sie sicher, dass der Name des Speicherkontos eindeutig ist, indem Sie einen Bezeichner hinzufügen.
    - Verwenden Sie bei den anderen Einstellungen die Standardwerte. 
    - Wählen Sie **Überprüfen** und danach **Erstellen** aus.
    - Warten Sie, bis das Speicherkonto bereitgestellt ist, und wählen Sie dann **Zu Ressource wechseln** aus.
         
1. Dieser Speicher erfordert Hochverfügbarkeit, wenn es zu einem regionalen Ausfall kommt. Aktivieren Sie außerdem den Lesezugriff auf die sekundäre Region. Lesen Sie mehr über [Speicherkontoredundanz](https://learn.microsoft.com/azure/storage/common/storage-redundancy#geo-redundant-storage).

    - Wählen Sie im Speicherkonto unter dem Abschnitt **Datenverwaltung** das Blatt **Redundanz** aus. 
    - Stellen Sie sicher, dass **Georedundanter Speicher mit Lesezugriff** ausgewählt ist.
    - Überprüfen Sie die primären und sekundären Standortinformationen. 

1. Informationen auf der öffentlichen Website sollten zugänglich sein, ohne dass sich Kund*innen anmelden müssen.
    - Wählen Sie im Speicherkonto unter dem Abschnitt **Einstellungen** das Blatt **Konfiguration** aus.
    - Stellen Sie sicher, dass die Einstellung **Anonymen Blob-Zugriff zulassen** auf **  Aktiviert** festgelegt ist.
    - Klicken Sie auf **Speichern**, um die Änderungen zu speichern. 
  
   
## Erstellen eines Blobspeichercontainers mit anonymem Lesezugriff

1. Die öffentliche Website enthält verschiedene Bilder und Dokumente. Erstellen Sie einen Blobspeichercontainer für den Inhalt. Lesen Sie mehr über [Speichercontainer](https://learn.microsoft.com/azure/storage/blobs/storage-blobs-introduction#containers).
    - Wählen Sie im Speicherkonto unter dem Abschnitt **Datenspeicher** das Blatt **Container** aus. 
    - Wählen Sie **+ Container** aus. 
    - Stellen Sie sicher, dass der **Name** des Containers `public` ist. 
    - Klicken Sie auf **Erstellen**. 
    
1. Kund*innen sollten die Bilder anzeigen können, ohne authentifiziert zu werden. Konfigurieren Sie den anonymen Lesezugriff für die öffentlichen Containerblobs.  Lesen Sie mehr über das [Konfigurieren des anonymen öffentlichen Zugriffs](https://learn.microsoft.com/azure/storage/blobs/anonymous-read-access-configure?tabs=portal).
    - Wählen Sie Ihren **öffentlichen** Container aus. 
    - Wählen Sie auf dem Blatt **Übersicht** die Option **Zugriffsebene ändern** aus. 
    - Legen Sie für **Öffentliche Zugriffsebene** die Einstellung **Blob (Anonymer Lesezugriff nur für Blobs)** fest.
    - Wählen Sie **OK** aus. 

## Üben des Dateiuploads und Testen des Zugriffs

1. Laden Sie eine Datei in den **öffentlichen** Container hoch. Der Dateityp spielt keine Rolle. Eine kleine Bild- oder Textdatei ist hierfür gut geeignet.  
    - Stellen Sie sicher, dass Sie Ihren Container anzeigen. 
    - Wählen Sie die Option **Hochladen**. 
    - **Navigieren Sie zu Dateien**, und wählen Sie eine Datei aus. Navigieren Sie zu einer Datei Ihrer Wahl. 
    - Wählen Sie die Option **Hochladen**.
    - Schließen Sie das Uploadfenster, **aktualisieren Sie, **und stellen Sie sicher, dass Ihre Datei hochgeladen wurde 

1. Ermitteln Sie die URL für Ihre hochgeladene Datei. Öffnen Sie einen Browser, und testen Sie die URL. 
    - Wählen Sie Ihre hochgeladene Datei aus.
    - Kopieren Sie auf der Registerkarte **Übersicht** die **URL**.
    - Fügen Sie die URL in einen neuen Browsertab ein.
    - Wenn Sie eine Bilddatei hochgeladen haben, wird sie im Browser angezeigt. Andere Dateitypen sollten heruntergeladen werden. 

## Konfigurieren des Softlöschens

1. Es ist wichtig, dass die Bilder wiederhergestellt werden können, wenn sie gelöscht werden. Konfigurieren Sie das vorläufige Löschen von Blobs für 21 Tage. Weitere Informationen über das [Softlöschen für Blobs](https://learn.microsoft.com/azure/storage/blobs/soft-delete-container-enable?tabs=azure-portal).
    - Gehen Sie zum **Übersichtsblatt**des **Speicherkontos**.
    - Suchen Sie auf der **Seite "Eigenschaften"** den Abschnitt ** "Blob-Dienst**".
    - Wälhlen Sie die Einstellung **Blob softläschen**aus.
    - Stellen Sie sicher, dass die Option **Softlöschen für Blobs aktivieren**aktiviert** ist**.
    - Ändern Sie die **Gelöschte Blobs beibehalten für (in Tagen** 21 **21 ist**.
    - Beachten Sie, dass Sie auch **Softlöschen für Container** aktivieren können. 
    - Vergessen Sie nicht, Ihre Änderungen zu **speichern**. 

1. Wenn etwas gelöscht wird, sollten Sie die Verwendung des Softlöschens üben, um die Dateien wiederherzustellen.
    - Navigieren Sie zu Ihrem Container, in den Sie eine Datei hochgeladen haben.
    - Wählen sie die hochgeladene Datei und wählen Sie **Löschen**
    - Wählen Sie **OK** , um den Löschvorgang zu bestätigen.  
    - Schalten Sie auf der Seite **Übersicht** des Containers den Schieberegler **Gelöschte Blobs anzeigen** um. Dieser Umschalter befindet sich rechts neben dem Suchfeld. 
    - Wählen Sie Ihre gelöschte Datei aus, und verwenden Sie die Auslassungspunkte ganz rechts, um für die Datei die Option **Löschvorgang rückgängig machen** zu wählen. 
    - Aktualisieren Sie den Container, und vergewissern Sie sich, dass die Datei wiederhergestellt wurde.     

## Konfigurieren der Blobversionsverwaltung
1. Es ist wichtig, die verschiedenen Versionen der Produktunterlagen nachzuverfolgen. Weitere Informationen zur [Blobversionsverwaltung](https://learn.microsoft.com/azure/storage/blobs/versioning-enable?tabs=portal).
    - Gehen Sie zum **Übersichtsblatt**des **Speicherkontos**.
    - Suchen Sie im Abschnitt **Eigenschaften** den Abschnitt **Blob-Dienst**.
    - Wählen Sie die **Versionsverwaltungseinstellung **aus.
    - Stellen Sie sicher, dass das Kontrollkästchen **Versionsverwaltung für BLOBs aktivieren**  aktiviert ist.
    - Beachten Sie Ihre Optionen, ** um alle Versionen beizubehalten **oder **Versionen nach** zu löschen. 
    - Vergessen Sie nicht, Ihre Änderungen zu **speichern**. 

1. Während Sie Zeit haben, mit der Wiederherstellung früherer BLOB-Versionen zu experimentieren.
   - **Laden Sie** eine andere Version Ihrer Containerdatei hoch. Dadurch wird Ihre vorhandene Datei überschrieben. 
   - Ihre vorherige Dateiversion wird auf de Seite **Gelöschte Blobs anzeigen** aufgeführt. 
    
## Erweitern Ihrer Lernerfahrung mit Copilot

Copilot kann Sie bei Ihrem Lernprozess unterstützen. Copilot kann grundlegende technische Informationen, allgemeine Schritte, Vor- und Nachteile, Hilfe zur Problembehandlung, Anwendungsfälle, Codebeispiele und vieles mehr bereitstellen. Um auf Copilot zuzugreifen, öffnen Sie einen Edge-Browser, und wählen Sie "Copilot" (oben rechts) aus. Nehmen Sie sich einige Minuten Zeit, um diese Prompts auszuprobieren.
+ Was ist Azure Blob Storage und wann sollte es verwendet werden?
+ Vergleichen Sie die verschiedenen Azure-Storage-Redundanzmodelle und heben Sie deren Hauptmerkmale und Anwendungsfälle hervor.
+ Was sind die Azure-Speicherebenen und wie können diese Ebenen Geld sparen?

## Weiterlernen im eigenen Tempo

+ [Erkunden von in Azure Blob Storage](https://learn.microsoft.com/training/modules/explore-azure-blob-storage/) In diesem Abschitt lernen Sie die wichtigsten Features und Funktionen von Azure Blob Storage kennen.

## Wichtige Erkenntnisse

Herzlichen Glückwunsch zum erfolgreichen Abschluss des Labs. Hier sind die wichtigsten Erkenntnisse für dieses Lab. 
+ Azure Blob Storage ist für die Speicherung großer Mengen unstrukturierter Daten optimiert. Unstrukturierte Daten sind Daten, die keinem bestimmten Datenmodell und keiner bestimmten Definition entsprechen (also beispielsweise Text- oder Binärdaten).
+ Das Feature für das vorläufige Löschen von Blobs schützt einzelne Blobs, Momentaufnahmen oder Versionen vor einer versehentlichen Löschung oder Überschreibung, weil die gelöschten Daten für einen angegebenen Zeitraum im System beibehalten werden. 
+ Bei der Blobversionierung werden frühere Versionen eines Blobs beibehalten. Wenn die BLOB-Versionierung aktiviert ist, können Sie eine frühere Version eines BLOBs wiederherstellen, um Ihre Daten wiederherzustellen, wenn sie geändert oder gelöscht wurden.
+ Wenn ein Container für den anonymen Zugriff konfiguriert ist, kann jeder Client Daten in diesem Container lesen.
