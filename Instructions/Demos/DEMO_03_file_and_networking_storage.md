---
demo:
  title: 'Demonstration 03: Erstellen und Konfigurieren von Dateien und Speichernetzwerken'
  module: Guided Project - Azure Files and Azure Blobs
--- 

## Demonstration – Erstellen und Konfigurieren von Dateien und Speichernetzwerken.

Erkunden Sie in dieser Demonstration Azure Files-Speicher und Speichernetzwerke.

> **Hinweis:** In dieser Demo erstellen Sie ein neues Speicherkonto und ein virtuelles Netzwerk mit Subnetz. Diese können vorab erstellt werden, um Zeit zu sparen. 

## Überprüfen Sie Azure Files, und erstellen Sie ein Speicherkonto speziell für Dateifreigaben.

1. [Unterstützende Folie] Bevor Sie mit der Demonstration beginnen, besprechen Sie, was Azure File Storage ist und wie es sich von Azure Blob Storage unterscheidet. Weitere Informationen finden Sie in [Szenarien für Azure Storage](https://learn.microsoft.com/azure/storage/common/storage-introduction).

1. Öffnen Sie das **Azure-Portal**.

1. Erstellen Sie ein **neues** Azure Storage-Konto. Dieses Konto wird verwendet, um die Anforderungen für freigegebene Dateien zu erfüllen.

1. [Unterstützende Folie] Wählen Sie für **Leistung** die Option **Premium** aus. 

1. Wählen Sie für **Premium-Kontotyp** die Option **Dateifreigaben** aus. Premium-Dateifreigaben sind für Enterprise- oder Hochleistungs-Dateifreigabeanwendungen. Unser Szenario gilt für eine Unternehmensdateifreigabe. 

1. Wählen Sie für **Redundanz** die Option **zonenredundanter** Speicher aus. Erinnern Sie die Kursteilnehmer daran, dass dies für Hochverfügbarkeitsszenarien empfohlen wird und vor Rechenzentrumsausfällen schützt.

1. Wechsel zur Registerkarte **Datenschutz**.

1. Weisen Sie darauf hin, dass die Option **Vorläufiges Löschen für Dateifreigaben aktivieren** **aktiviert** ist.

1. Wählen Sie **Überprüfen** und dann **Erstellen** aus, um das Speicherkonto zu erstellen.

## Konfigurieren der Dateifreigabe.

1. Im Speicherkonto fortfahren.

1. Wählen Sie im Blatt **Datenspeicher** die Option **Dateifreigaben** aus.

1. Wählen Sie **Dateifreigabe** aus, und geben Sie der Dateifreigabe einen Namen, **Finanzierung**.

1. Besprechen der **Bereitgestellten Kapazität** und wie eine Premium-Dateifreigabe unabhängig von der genutzten Kapazität nach der Größe der bereitgestellten Datei abgerechnet wird. Wenn Sie Zeit haben, besprechen Sie andere Einstellungen. 

1. Zum Besprechen von**Protokoll**, die Option **SMB** auswählen.

1. Klicken Sie auf **Erstellen**.

## Konfigurieren der Dateifreigabeeinstellungen und Erstellen einer Momentaufnahme.

1. Wählen Sie die **Finanzen** Dateifreigabe aus.

1. Überprüfen Sie die Einstellungen oben auf der Seite. Beispiel: **Hochladen** und **Ändern der Größe und Leistung**.

1. [Ergänzende Folie] Besprechen Sie den Zweck von Momentaufnahmen. Weitere Informationen finden Sie unter [Dateifreigabemomentaufnahmen](https://learn.microsoft.com/azure/storage/files/storage-snapshots-files).

1. Wählen Sie Blatt **Vorgänge** die Option **Momentaufnahmen** aus.

1. Wählen Sie **Momentaufnahme hinzufügen** und dann **OK** aus. Das Hinzufügen eines Kommentars ist optional.

1. Die Kursteilnehmer werden im Lab Dateien hochladen, Momentaufnahmen erstellen und wiederherstellen.

## Konfigurieren des Netzwerkzugriffs für Speicher.

1. [Unterstützende Folie] Besprechen Sie vor dem Konfigurieren des Speichernetzwerks die verschiedenen Optionen. Überprüfen Sie einige der vorherigen Netzwerkoptionen, die konfiguriert wurden. 

1. Suchen Sie im Portal nach der Option **Virtuelle Netzwerke**.

1. Verwenden Sie die Registerkarte **Grundlagen**, um ein virtuelles Netzwerk mit dem Namen **Corpnet** zu erstellen. Erstellen Sie ein **Subnetz**, **Finanzierung**. Weisen Sie darauf hin, dass dieses Netzwerk bereits erstellt wurde.

1. Kehren Sie zum Speicherkonto zurück.

1. Wählen Sie auf dem Blatt **Sicherheit und Netzwerk** die Option **Netzwerk** aus.

1. Wählen Sie **Aktiviert von ausgewählten virtuellen Netzwerken und IP-Adressen** aus.

1. Fügen Sie auf der Seite **Netzwerk hinzufügen** das virtuelle Netzwerk **Corpnet** und das Subnet **Finanzen** hinzu.

1. **Den Endpunkt aktivieren**. Erläutern Sie, dass das Erstellen eines neuen Dienstendpunkts bis zu 15 Minuten dauern kann.

1. Überprüfen Sie die **Firewalleinstellungen**.

1. Überprüfen Sie den Abschnitt **Netzwerkrouting**, und vergewissern Sie sich, dass das Microsoft-Netzwerkrouting verwendet wird.



1. Wenn Sie Zeit haben, stellen Sie kurz den **Speicherbrowser** vor. 

>**Hinweis**: Die Kursteilnehmenden sollten jetzt in der Lage sein, LAB_03 abzuschließen. 
