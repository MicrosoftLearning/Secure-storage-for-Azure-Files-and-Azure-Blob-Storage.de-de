---
lab:
  title: 'Übung 03: Bereitstellen von freigegebenem Dateispeicher für die Unternehmensstandorte'
  module: Guided Project - Azure Files and Azure Blobs
---


Das Unternehmen besitzt Niederlassungen an verschiedenen geografischen Standorten.  Diese Niederlassungen benötigen eine Möglichkeit, um Dateien zu teilen und Informationen zu verbreiten. Beispielsweise muss die Finanzabteilung Kosteninformationen zwecks Revision und Compliance bestätigen. Diese Dateifreigaben sollten problemlos zugänglich sein und ohne Verzögerung geladen werden können. Einige Inhalte sollte nur über ausgewählte virtuelle Unternehmensnetzwerke verfügbar sein.


## Architekturdiagramm

![Abbildung mit einem Speicherkonto, einer Dateifreigabe und einem Verzeichnis](../Media/task-4.png)

## Qualifikationsaufgabe
- Erstellen eines Speicherkontos speziell für Dateifreigaben 
- Konfigurieren Sie eine Dateifreigabe und ein Verzeichnis.  
- Konfigurieren sie Momentaufnahmen und üben Sie das Wiederherstellen von Dateien. 
- Schränken Sie den Zugriff auf ein bestimmtes virtuelles Netzwerk und ein Subnetz ein. 

## Übungsanweisungen

>**Hinweis**: Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/free/).

## Erstellen und Konfigurieren eines Speicherkontos für Azure Files 

1. Erstellen Sie ein Speicherkonto für die freigegebenen Dateien der Finanzabteilung.  Lesen Sie mehr zu Speicherkonten für [Azure Files-Bereitstellungen](https://learn.microsoft.com/azure/storage/files/storage-files-planning#management-concepts).

    - Suchen Sie im Portal die Option `Storage accounts`, und wählen Sie sie aus.
    - Wählen Sie **+ Erstellen** aus.
    - Für **Ressourcengruppe** wählen Sie **Neu erstellen**. Geben Sie Ihrer Ressourcengruppe einen **Namen**, und wählen Sie **OK** aus, um Ihre Änderungen zu speichern. 
    - Geben Sie einen **Speicherkontonamen** an. Stellen Sie sicher, dass der Name die Benennungsanforderungen erfüllt. 
    - Legen Sie unter **Leistung** die Option **Premium** fest.
    - Legen Sie unter **Premium-Kontotyp** die Option **Dateifreigaben** fest.
    - Legen Sie unter **Redundanz** die Option **Zonenredundanter Speicher** fest.
    - Wählen Sie **Überprüfen** und dann **Erstellen** aus, um das Speicherkonto zu erstellen.
    - Warten Sie, bis die Ressource bereitgestellt wurde.
    - Wählen Sie **Zu Ressource wechseln** aus. 

## Erstellen und Konfigurieren einer Dateifreigabe mit Verzeichnis

1. Erstellen Sie eine Dateifreigabe für die Niederlassung. Lesen Sie mehr über [Azure-Dateiebenen](https://learn.microsoft.com/azure/storage/files/storage-files-planning#storage-tiers).

    - Wählen Sie im Speicherkonto unter dem Abschnitt **Datenspeicher** das Blatt **Dateifreigaben** aus. 
    - Wählen Sie **+ Dateifreigabe** aus, und geben Sie einen **Namen** an.
    - Sehen Sie sich die anderen Optionen an, übernehmen Sie aber die Standardwerte.
    - Klicken Sie auf **Erstellen**

1. Fügen Sie der Dateifreigabe für die Finanzabteilung ein Verzeichnis hinzu. Laden Sie für zukünftige Tests eine Datei hoch. 

    - Wählen Sie Ihre Dateifreigabe und dann **+ Verzeichnis hinzufügen** aus. 
    - Nennen Sie das neue Verzeichnis `finance`.
    - Wählen Sie **Durchsuchen** und dann das Verzeichnis **finance** aus.
    - Sie können ein **Verzeichnis hinzufügen**, um Ihre Dateifreigabe weiter zu organisieren.
    - **Laden Sie eine Datei Ihrer Wahl hoch**. 

## Konfigurieren und Testen von Momentaufnahmen

1. Ähnlich wie beim Blobspeicher müssen Sie einen Schutz vor versehentlichem Löschen von Dateien hinzufügen. Sie entscheiden sich für das Verwenden von Momentaufnahmen. Lesen Sie mehr über [Dateimomentaufnahmen](https://learn.microsoft.com/azure/storage/files/storage-snapshots-files).
    
    - Wählen Sie Ihre Dateifreigabe aus.
    - Wählen Sie im Abschnitt **Vorgänge** das Blatt **Momentaufnahmen** aus. 
    - Wählen Sie **+ Momentaufnahme hinzufügen** aus. Der Kommentar ist optional. Klickan Sie auf **OK**.
    - Wählen Sie Ihre Momentaufnahme aus, und überprüfen Sie, ob das Dateiverzeichnis und die hochgeladene Datei enthalten sind.
  
1. Üben Sie die Verwendung von Momentaufnahmen zum Wiederherstellen einer Datei.
    - Kehren Sie zur **Dateifreigabe** zurück.
    - **Navigieren** Sie zu Ihrem Dateiverzeichnis. 
    - Suchen Sie Ihre hochgeladene Datei, und wählen Sie im Bereich **Eigenschaften** die Option **Löschen** aus. Wählen Sie **Ja** aus, um den Löschvorgang zu bestätigen. 
    - Wählen Sie das Blatt **Momentaufnahmen** und dann Ihre Momentaufnahme aus. 
    - Navigieren Sie zu der Datei, die Sie wiederherstellen möchten.
    - Wählen Sie die Datei und dann die Option **Wiederherstellen** aus.
    - Geben Sie einen **Namen für die wiederhergestellte Datei** an. 
    - Überprüfen Sie, ob im Dateiverzeichnis die wiederhergestellte Datei vorhanden ist.  

## Konfigurieren einer Speicherzugriffsbeschränkung für ausgewählte virtuelle Netzwerke

1. Für die Aufgaben in diesem Abschnitt ist ein virtuelles Netzwerk mit Subnetz erforderlich. In einer Produktionsumgebung würde es diese Ressourcen bereits geben.
    - Suchen Sie nach **Virtuelle Netzwerke**, und wählen Sie diese Option aus.
        - Klicken Sie auf **Erstellen**. Wählen Sie Ihre Ressourcengruppe aus. Geben Sie dem virtuellen Netzwerk einen **Namen**.
        - Übernehmen Sie die Standardwerte für andere Parameter, und wählen Sie **Überprüfen + erstellen** und dann **Erstellen** aus.
        - Warten Sie, bis die Ressource bereitgestellt wurde.
        - Wählen Sie **Zu Ressource wechseln** aus. 
    - Wählen Sie im Abschnitt **Einstellungen** das Blatt **Subnetze** aus.
        - Wählen Sie das Subnetz **Standard** aus.
        - Wählen Sie im Abschnitt **Dienstendpunkte** im Dropdown **Dienste** die Option **Microsoft.Storage** aus.
        - Nehmen Sie keine weiteren Änderungen vor.    
        - Klicken Sie auf **Speichern**, um die Änderungen zu speichern. 
   
1. Auf das Speicherkonto sollte nur über das virtuelle Netzwerk zugegriffen werden, das Sie gerade erstellt haben. Lesen Sie mehr über die Verwendung [privater Speicherendpunkte](https://learn.microsoft.com/azure/storage/common/storage-private-endpoints).

    - Kehren Sie zu Ihrem **Dateispeicherkonto** zurück. 
    - Wählen Sie im Abschnitt **Sicherheit + Netzwerk** das Blatt **Netzwerk** aus.
        - Ändern Sie **Öffentlicher Netzwerkzugang** in **Von ausgewählten virtuellen Netzwerken und IP-Adressen aktiviert** aus.
        - Wählen Sie im Abschnitt **Virtuelle Netzwerke** die Option **Vorhandenes virtuelles Netzwerk hinzufügen** aus.
        - Wählen Sie erst Ihr virtuelles Netzwerk und das Subnetz aus und dann **Hinzufügen**.
        - Klicken Sie auf **Speichern**, um die Änderungen zu speichern. 
    - Wählen Sie den **Speicherbrowser** aus, und navigieren Sie zu Ihrer Dateifreigabe. 
    - Überprüfen Sie die Meldung *keine ausreichenden Berechtigungen zum Ausführen dieses Vorgangs*. Sie verbinden sich nicht über das virtuelle Netzwerk. 


>**Hinweis**: Weitere Vorgehensweisen finden Sie im Modul [Konfigurieren der Sicherheit von Azure Storage](https://learn.microsoft.com/training/modules/configure-storage-security/). Das Modul verfügt über eine interaktive Labsimulation, in der Sie das Erstellen von sicheren Speichern weiter üben können. 
