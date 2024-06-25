---
lab:
  title: 'Übung 04: Bereitstellen von Speicher für eine neue Unternehmens-App'
  module: Guided Project - Azure Files and Azure Blobs
---
Das Unternehmen entwirft und entwickelt eine neue App. Das Entwicklerteam muss sicherstellen, dass nur mithilfe von Schlüsseln und verwalteten Identitäten auf den Speicher zugegriffen wird. Das Entwicklerteam möchte die rollenbasierte Zugriffssteuerung verwenden. Zum Testen wird ein geschützter unveränderlicher Speicher benötigt. 

## Architekturdiagramm

![Diagramm mit einem Speicherkonto, verwalteten Identitäten und einem Schlüsseltresor](../Media/task-5.png)

## Qualifikationsaufgaben

- Erstellen eines Speicherkontos mit einer vom System verwalteten Identität.
- Sicherer Zugriff auf das Speicherkonto mit einem Schlüsseltresor und Schlüssel.
- Konfigurieren Sie das Speicherkonto, um kundenseitig verwaltete Schlüssel im Schlüsseltresor zu verwenden.
- Konfigurieren Sie eine zeitbasierte Aufbewahrungsrichtlinie und einen Verschlüsselungsbereich.

## Übungsanweisungen

## Erstellen eines Speicherkontos mit einer vom System verwalteten Identität.

1. Geben Sie ein Speicherkonto für die Web-App an. 
    - Suchen Sie im Portal nach der Option **Speicherkonten**, und wählen Sie sie aus. 
    - Wählen Sie **+ Erstellen** aus.
    - Für **Ressourcengruppe** wählen Sie **Neu erstellen**. Geben Sie Ihrer Ressourcengruppe einen **Namen**, und wählen Sie **OK** aus, um Ihre Änderungen zu speichern.
    - Geben Sie einen **Speicherkontonamen** an. Der Name muss eindeutig sein und die Anforderungen in Bezug auf die Benennung erfüllen.
    - Wechseln Sie zur Registerkarte **Verschlüsselung**.
    - Aktivieren Sie das Kontollkästchen **Infrastrukturverschlüsselung aktivieren**.
    - Beachten Sie die Warnung: *Diese Option kann nach dem Erstellen dieses Speicherkontos nicht mehr geändert werden*.
    - Klicken Sie auf **Überprüfen + erstellen**.
    - Warten Sie, bis die Ressource bereitgestellt wurde.

1. Bereitstellen einer verwalteten Dienstidentität für die zu verwendende Web-App.  Weitere Informationen zu [verwalteten Identitäten](https://learn.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).

    - Suchen Sie nach **Verwaltete Identitäten**, und wählen Sie diese aus.
    - Klicken Sie auf **Erstellen**.
        - Wählen Sie Ihre **Ressourcengruppe** aus. 
        - Geben Sie Ihrer verwalteten Identität einen Namen.
    - Wählen Sie **Überprüfen und erstellen** und dann **Erstellen** aus. 

1. Weisen Sie der verwalteten Identität die richtigen Berechtigungen zu. Die Identität benötigt nur Lese- und Listencontainer sowie Blobs. Weitere Informationen zum [Zuweisen von Azure-Rollen](https://learn.microsoft.com/azure/role-based-access-control/role-assignments-portal).
    
    - Suchen Sie nach Ihrem **Speicherkonto**, und wählen Sie es aus.
    - Wählen Sie das Blatt **Zugriffssteuerung (IAM)** aus.
    - Klicken Sie auf **Rollenzuweisung hinzufügen** (Mitte der Seite).
    - Suchen Sie auf der Seite **Rollen für Auftragsfunktionen** nach der Rolle **Leser von Speicherblobdaten**, und wählen Sie sie aus. 
    - Wählen Sie auf der Seite **Mitglieder** die Option **Verwaltete Identität** aus.
    - Wählen Sie **Mitglieder auswählen** aus, in der Dropdownliste **Verwaltete Identität** wählen Sie die Option **Benutzerseitig zugewiesene verwaltete Identität** aus.
    - Wählen Sie die verwaltete Identität aus, die Sie im vorherigen Schritt erstellt haben. 
    - Klicken Sie auf **Auswählen**, und dann auf **Überprüfen und zuweisen** der Rolle. 
    - Wählen Sie ein zweites Mal **Überprüfen und zuweisen** aus, um die Rollenzuweisung hinzuzufügen.
    - Auf Ihr Speicherkonto kann jetzt über eine verwaltete Identität mit den Berechtigungen eines Speicher-Blob-Datenlesers zugegriffen werden. 

## Sicherer Zugriff auf das Speicherkonto mit einem Schlüsseltresor und Schlüssel

1. Zum Erstellen des Schlüsseltresors und des Schlüssels, der für diesen Teil des Labs erforderlich ist, muss Ihr Benutzerkonto über Key Vault-Administratorberechtigungen verfügen. Weitere Informationen über das [Gewähren des Zugriffs auf Key Vault-Schlüssel, -Zertifikate und -Geheimnisse mit der rollenbasierten Zugriffssteuerung in Azure](https://learn.microsoft.com/azure/key-vault/general/rbac-guide?tabs=azure-cli)
    - Suchen Sie im Portal nach **Ressourcengruppen**, und wählen Sie die Option aus. 
    - Wählen Sie die **Ressourcengruppe**und dann **Zugriffsänderung (AM)** aus.
    - Klicken Sie auf **Rollenzuweisung hinzufügen** (Mitte der Seite).
    - Suchen Sie auf der Seite **Auftragsfunktionsrollen** nach **Key Vault-Administrator**, und wählen Sie diese Option dann aus.
    - Wählen Sie auf der Registerkarte **Mitglieder** die Option **Benutzer, Gruppe oder Dienstprinzipal** aus.
    - Wählen Sie **Mitglieder auswählen**.
    - Suchen Sie nach Ihrem Konto, und wählen Sie es aus. Wählen Sie in der oberen rechten Ecke des Portals Ihr Benutzerkonto aus.
    - Klicken Sie auf **Auswählen** und dann auf **Überprüfen+Zuweisen**.
    - Wählen Sie ein zweites Mal **Überprüfen und zuweisen** aus, um die Rollenzuweisung hinzuzufügen.
    - Sie können die Failoverclusterinstanz nun konfigurieren.

1. Erstellen Sie einen Schlüsseltresor, um die Zugriffsschlüssel zu speichern. 

    - Suchen Sie nach  und wählen Sie die Option**Schlüsseltresore**,
    - Klicken Sie auf **Erstellen**.
    - Wählen Sie Ihre **Ressourcengruppe** aus.
    - Geben Sie den **Namen**für den Schlüsseltresor an. Der Name muss eindeutig sein.
    - Stellen Sie auf der Registerkarte **Zugriffskonfiguration** sicher, dass **Rollenbasierte Zugriffssteuerung in Azure (empfohlen)** ausgewählt ist. 
    - Klicken Sie auf **Überprüfen + erstellen**.
    - Warten Sie, bis die Überprüfung erfolgreich abgeschlossen ist, und wählen Sie dann **Erstellen** aus.
    - Wählen Sie nach der erfolgreichen Bereitstellung **Zu Ressource wechseln** aus.
    - **Vergewisser Sie sich auf dem**Overview-Blade, dass sowohl**Soft Delete**als auch**der Purge Schutz****aktiviert sind.** 

1. Erstellen Sie einen kundenseitig verwalteten Schlüssel im Schlüsseltresor. 

    - **Wählen Sie im Schlüsseltresor** im **Abschnitt "Objekte**" das **Blatt "Schlüssel**" aus.
    - Klicken Sie auf **Generieren/Importieren** und dann auf **Benennen**, um dem Schlüssel einen Namen zu geben.
    - Verwenden Sie die Standardwerte für den Rest der Parameter, und erstellen Sie den Schlüssel über **Erstellen**.

## Konfigurieren Sie das Speicherkonto, um kundenseitig verwaltete Schlüssel im Schlüsseltresor zu verwenden.

1. Bevor Sie die nächsten Schritte ausführen können, müssen Sie der verwalteten Identität die Rolle "Key Vault Crypto Service Encryption User" zuweisen. Weitere Informationen zur [Verwendung einer vom System zugewiesenen verwalteten Identität zum Autorisieren des Zugriffs](https://learn.microsoft.com/azure/storage/common/customer-managed-keys-configure-existing-account?tabs=azure-portal#use-a-system-assigned-managed-identity-to-authorize-access)
    - Suchen Sie im Portal nach **Ressourcengruppen**, und wählen Sie die Option aus. 
    - Wählen Sie die **Ressourcengruppe**und dann **Zugriffsänderung (AM)** aus.
    - Klicken Sie auf **Rollenzuweisung hinzufügen** (Mitte der Seite).
    - Suchen Und wählen Sie auf der **Seite "Rollen für Auftragsfunktionen** " die Rolle " **Key Vault Crypto Service Encryption User** " aus.
    - Wählen Sie auf der Seite **Mitglieder** die Option **Verwaltete Identität** aus.
    - Wählen Sie **Mitglieder auswählen** aus, in der Dropdownliste **Verwaltete Identität** wählen Sie die Option **Benutzerseitig zugewiesene verwaltete Identität** aus.
    - Wählen Sie Verwaltete Identität aus.  
    - Klicken Sie auf **Auswählen** und dann auf **Überprüfen+Zuweisen**.
    - Wählen Sie ein zweites Mal **Überprüfen und zuweisen** aus, um die Rollenzuweisung hinzuzufügen.
    
1. Konfigurieren Sie die Speicherkontoverschlüsselung, um kundenseitig verwaltete Schlüssel in Ihrem Schlüsseltresor zu verwenden. Weitere Informationen zu[zu kundenseitig verwalteten Schlüsseln in einem vorhandenen Speicherkonto.](https://learn.microsoft.com/azure/storage/common/customer-managed-keys-configure-existing-account?WT.mc_id=Portal-Microsoft_Azure_Storage&tabs=azure-portal)
    - Kehren Sie zu Ihrem Speicherkonto zurück.
    - Wählen Sie im Abschnitt **Sicherheit + Netzwerk** das Blatt **Verschlüsselung** aus.
    - Wählen Sie **Von Kunden verwaltete Schlüssel** aus.
    - **Schlüsseltresor und Schlüssel auswählen**. Wählen Sie Schlüsseltresor und Schlüssel aus.
    - Bestätigen Sie Ihre Auswahl mit**Auswählen**. 
    - Stellen Sie sicher, dass der **Identitätstyp****dem Benutzer zugewiesen** ist.
    - **Wählen Sie eine Identität**.
    - Wählen Sie Ihre verwaltete Identität und dann **Hinzufügen**aus. 
    - **Speichern** Sie die Änderungen.
    - Wenn Sie eine Fehlermeldung erhalten, dass Ihre Identität nicht über die richtigen Berechtigungen verfügt, warten Sie eine Minute, und versuchen Sie es erneut. 

## Konfigurieren Sie eine zeitbasierte Aufbewahrungsrichtlinie und einen Verschlüsselungsbereich.

1. Das Entwicklerteam benötigt einen Speichercontainer, in dem Dateien nicht geändert werden können, auch nicht vom Administrator. Weitere Informationen zum[unveränderlichem Blobspeicher](https://learn.microsoft.com/azure/storage/blobs/immutable-storage-overview)

    - Navigieren Sie zum **Speicherkonto**.
    - Wählen Sie im Abschnitt **Datenspeicher** die Option **Container** aus. 
    - Erstellen Sie einen Container, der als Halteraum** Halteraum**bezeichnet wird. Standardwerte übernehmen Achten Sie darauf, den Container zu **erstellen** . 
    - Laden Sie eine Datei in den Container hoch. 
    - Wählen Sie im **Abschnitt Einstellungen** das **Access-Richtlinienblatt** aus. 
    - Wählen Sie im Abschnitt **Unveränderlicher Blobspeicher** die Option **Richtlinie hinzufügen** aus. 
    - Wählen Sie als **Richtlinientyp****die Option Zeitbasierte Aufbewahrung** aus. 
    - Legen Sie den **Aufbewahrungszeitraum** auf **5 Tage** fest. 
    - Klicken Sie auf **Speichern**, um die Änderungen zu speichern. 
    - Versuchen Sie, die Datei aus dem Container zu** entfernen**. 
    - Stellen Sie sicher, dass Sie aufgrund der Richtlinie nicht benachrichtigt **werden konnten, blobs** zu löschen.  

1. Das Entwicklerteam benötigt einen Verschlüsselungsbereich, der die Infrastrukturverschlüsselung ermöglicht. Weitere Informationen zur [Infrastrukturverschlüsselung](https://learn.microsoft.com/azure/storage/common/infrastructure-encryption-enable?tabs=portal).

    - Navigieren Sie zurück zu Ihrem Speicherkonto. 
    - Wählen Sie im Bereich**Sicherheit + Netzwerk**die Option**Verschlüsselung**aus.
    - – Klicken Sie auf der Registerkarte **Verschlüsselungsbereiche** auf **Hinzufügen**.
    - Geben Sie Ihrem Verschlüsselungsbereich einen **Namen**. 
    - Der **Verschlüsselungstyp**ist**on Microsoft verwalteter Schlüssel**.
    - Legen Sie die **Infrastrukturverschlüsselung**auf**Aktivieren**fest.
    - Verschlüsselungsbereich **erstellen**.
    - Navigieren Sie zu Ihrem Speicherkonto und erstellen Sie einen neuen Container.
    - Beachten Sie auf der **Seite "Neuer Container** " die **Ebene "Name** " und **"Öffentlicher Zugriff"**.
    - Beachten Sie im **Abschnitt "Erweitert** ", dass Sie den **von Ihnen erstellten Verschlüsselungsbereich** auswählen und auf alle Blobs im Container anwenden können. 


>**Hinweis**Für zusätzliche Übungen vervollständigen Sie das Modul [Sichern und Isolieren des Zugriffs auf Azure-Ressoursen mit Hilfe von Netzwerkgruppen und Dienstenpunkten](https://learn.microsoft.com/training/modules/secure-and-isolate-with-nsg-and-service-endpoints/). Das Modul verfügt über eine Sandbox, in der Sie mehr Übung beim Einschränken des Zugriffs auf Speicher erhalten können.
