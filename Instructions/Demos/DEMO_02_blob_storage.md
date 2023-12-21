---
demo:
  title: Erstellen und Konfigurieren einer Blob Storage-Instanz
  module: Guided Project - Azure Files and Azure Blobs
---


## Demo: Konfigurieren von Blob Storage

In dieser Demo sehen wir uns Blob Storage genauer an.

## Blob Storage-Einstellungen überprüfen

1. [Unterstützende Folie] Bevor Sie mit der Demonstration beginnen, überprüfen Sie die Blob-Speicherverwendungen und die Organisation. Welche unserer Geschäftsgruppen benötigt BLOB-Speicher?

1. Öffnen Sie das **Azure-Portal**.

1. Sie können weiterhin das vorherige Speicherkonto verwenden. 

1. Klicken Sie auf die Registerkarte **Übersicht**.

1. [Unterstützende Folie] Markieren Sie im **Abschnitt "Blob-Dienst** " die Einstellung der **Standardzugriffsebene** . Erläutern, wie sich Unternehmensinhalte möglicherweise auf der Hot Access-Ebene befinden. Überwachungsinformationen könnten sich in der coolen Ebene befinden. Protokolle oder Saisonmarketingliteratur könnten sich auf der Archivebene befinden. Weitere Informationen finden Sie in [Access-Ebenen für blob-Speicher](https://docs.microsoft.com/azure/storage/blobs/access-tiers-overview).

1. [Unterstützende Folie] Markieren Sie im **Abschnitt "Blob-Dienst** " die **Einstellungen für das vorläufige Löschen**. Dies wäre für die öffentliche Website wichtig, falls etwas versehentlich gelöscht oder überschrieben wird. Die Kursteilnehmer üben das vorläufige Löschen im Labor. Weitere Informationen[Blob soft delete](https://learn.microsoft.com/azure/storage/blobs/soft-delete-blob-overview).

1. Verweisen Sie im **Abschnitt "Blob-Dienst** " auf die **Versionsverwaltungseinstellung** . Dies kann für die Marketingabteilung wichtig sein. Die Produktliteratur muss möglicherweise nachverfolgt werden.

## Erstellen Sie einen BLOB-Container, laden Sie eine Datei hoch, und konfigurieren Sie den Zugriff.

1. Suchen Sie in Ihrem Speicherkonto das Blatt**Datenspeicher**.

1. Wählen Sie **Container** und dann **+ Container**.

1. Geben Sie einen **Namen** für den Container an.
2. iner, **public**. Dies ist Speicher für die öffentliche Website.

1. Legen Sie die öffentliche Zugriffsebene auf **Container (Anonymer Lesezugriff für Container und Blobs)** fest. Beschreiben Sie kurz die Zugriffsebenen. Dies wird in der letzten Demonstration ausführlicher behandelt. 

1. Klicken Sie auf **Erstellen**.

1. Warten Sie, bis der Container bereitgestellt wird, und fahren Sie dann mit der Arbeit im **öffentlichen** Container fort.

1. **Hochladen eines Blobs** Während Sie Zeit haben, besprechen Sie die Optionen. 

1. Wählen Sie die **hochgeladene Datei** aus, und **kopieren Sie die URL**.

1. Öffnen Sie eine **neue Browserregisterkarte**, fügen Sie die URL ein, und stellen Sie sicher, dass die hochgeladene Datei angezeigt wird.

1. Kehren Sie zum**öffentlichen**Container zurück und **Ändern Sie die Zugriffsstufe **auf **Privat (kein anonymer Zugriff**.

1. **Aktualisieren Sie die Registerkarte "URL"** , und bestätigen Sie, dass der Zugriff auf die Ressource jetzt **verweigert** wurde.

## Konfigurieren der Lebenszyklusverwaltung

1. [Unterstützende Folie] Beginnen Sie mit einer Diskussion über die Lebenszyklusverwaltung. Die Marketinggruppe hat Produktliteratur, die saisonal ist. Zum Beispiel die Winterbekleidungs- und Zubehörlinie. Dieser Inhalt kann bis zur nächsten Saison archiviert werden. Das Archivieren von Inhalten ist mit einer Lebenszyklusverwaltungsregel einfach zu erledigen. Weitere Informationen finden [Sie in den Richtlinien für die Blob-Lebenszyklusverwaltung](https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-overview).

1. Arbeiten Sie mit dem Speicherkonto fort.

1. Wählen Sie im Abschnitt **Datenverwaltung** die Option **Lebenszyklusverwaltung** aus.

1. Benennen Sie auf der **Registerkarte "Details** " die Regel **"movetoarchive"**.

1. Besprechen Sie den **Regelbereich** und wie Sie Blobs mit Filtern** einschränken können**. Beispielsweise wird nur der Inhalt im bestimmten Container verschoben.

1. Wechseln zur Registerkarte " **Basisblobs** ".

1. Besprechen Sie, wie die Regel Blobs basierend auf der letzten Änderung oder vor mehr als Tagen automatisch verschieben wird.

1. Öffnen Sie dann** die **Dropdownliste, und besprechen Sie die Optionen. Versuchen Sie, Beispiele basierend auf unserem Laborszenario zu geben. Die IT-Abteilung kann z. B. blobs nach 30 Tagen löschen, da es sich um ein Testkonto handelt.

## Konfigurieren sie eingeschränkten Zugriff auf Inhalte.

1. Überprüfen Sie Nutzungsfälle für eingeschränkten Zugriff. Beispielsweise muss der Unternehmensinhalt für Drittanbieter oder Partner freigegeben werden. Access kann auf einen bestimmten Zeitrahmen und eine bestimmte Aktion (Lese-, Schreibzugriff) beschränkt sein. Weitere Informationen zu [SAS (Shared Access Signature)](https://learn.microsoft.com/azure/storage/common/storage-sas-overview).

1. Fahren Sie mit dem **Speicherkonto** fort.

1. Wählen Sie im Abschnitt **Sicherheit + Netzwerkbetrieb** die Option **Shared Access Signature** aus.

1. Überprüfen Sie die **Zulässigen Dienste** und **Zulässigen Ressourcentypen**. Erläutern, dass ein SAS auf ein Speicherkonto, einen Container, eine Datei oder eine einzelne BLOB-Datei festgelegt werden kann.

1. Überprüfen Sie die **zulässigen Berechtigungen**.

1. Wählen Sie**Blob und Container**aus un0 **lesen Sie sie**

1. Überprüfen Sie die Einstellung für das **Start-** und**Ablaufdatum**

1. Klicken Sie auf **SAS und Verbindungszeichenfolge generieren**.

1. Wählen Sie **Speichern** aus, um die Änderungen zu speichern. 

1. Kopieren Sie die **URL des Blob-Dienstes SAS**in eine neue Browser-Registrierkarte.

1. Diskutieren Sie, wie der Inhalt angezeigt wird, obwohl es sich um einen privaten Container handelt.

## Konfigurieren der Objektreplikation für Blobs 

1. [Unterstützende Folie] Bevor Sie die Demonstration fortsetzen, überprüfen Sie die Verwendungsfälle für die Blobobjektreplikation. Beispielsweise muss der Inhalt der öffentlichen Website gesichert werden. Erläutern Sie, dass Speicherkonten in verschiedenen Azure-Regionen vorhanden sein können, dies ist jedoch nicht erforderlich. Weitere Informationen finden Sie in der [Objektreplikation](https://learn.microsoft.com/azure/storage/blobs/object-replication-overview).

1. Erstellen Sie ein **neues** Speicherkonto.

1. **Erstellen Sie** eine **** **Containersicherung** im Speicherkonto.

1. Kehren Sie zum ersten Speicherkonto und zum **öffentlichen** Container zurück. 

1. Wählen Sie unter **Datenverwaltung** die Option **Objektreplikation** aus.

1. Wählen Sie **Replikationsregeln erstellen** aus.

    - Zielspeicherkonto: Ihr zweite Speicherkonto.

    - Quellcontainer: **öffentlich**

    - Zielcontainer:**Sicherung**

1. **Erstellen **Sie die Regel. Erläutern, dass das Replizieren des Quellcontainers 5 bis 10 Minuten dauern kann. Erklären Sie, dass die Kursteilnehmer diese Zeit während des Labors in Anspruch nehmen. 

> **Hinweis:** Kursteilnehmer sollten jetzt in der Lage sein, LAB_02a und LAB_02b abzuschließen. 

  
