---
demo:
  title: 'Demonstration 04: Erstellen und Konfigurieren von Verschlüsselung und sicherem App-Zugriff'
  module: Guided Project - Azure Files and Azure Blobs
--- 

## Demonstration – Erstellen und Konfigurieren von Verschlüsselung und sicherem App-Zugriff 

In dieser Demonstration sehen wir uns die Themen Verschlüsselung und App-Sicherheit genauer an.

> **Hinweis:** In dieser Demonstration erstellen Sie eine verwaltete Identität, einen Schlüsseltresor und einen Schlüssel. Um Zeit zu sparen, sollten Sie diese Ressourcen vorab erstellen. 

## Erstellen eines Schlüsseltresors, eines Schlüssels und einer verwalteten Identität

1. Erstellen Sie ein neues Azure Storage-Konto. Dies wird verwendet, um sichere Speicherfeatures anzuzeigen.

1. [Unterstützende Folie] Bevor Sie beginnen, sehen Sie sich an, inwiefern die neue Entwickler-App sicher auf den benötigten Speicher zugreifen muss. Auf die App wird über eine verwaltete Identität zugegriffen. Die verwaltete Identität verwendet einen Verschlüsselungsschlüssel, der in Azure Key Vault gespeichert ist. Azure Key Vault ist ein Clouddienst zum Verwalten von Schlüsseln, Geheimnissen und Zertifikaten. Durch diesen Vorgang erübrigt sich die Notwendigkeit, Sicherheitsinformationen im App-Code zu speichern.  Nicht alle Kursteilnehmenden sind mit diesen Konzepten vertraut.

1. Erstellen Sie eine **verwaltete Identität**. Weitere Informationen finden Sie unter [Verwaltete Identitäten](https://learn.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview).

1. Erstellen Sie einen **Schlüsseltresor**. Übernehmen Sie die Standardeinstellungen, **außer** auf der Registerkarte **Zugriffskonfiguration**. Stellen Sie sicher, dass dort **Tresorzugriffsrichtlinie** ausgewählt ist. Weitere Informationen finden Sie unter [Azure Key Vault](https://learn.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).

1. Warten Sie, bis der Schlüsseltresor bereitgestellt wurde, und wählen Sie dann **Zu Ressource wechseln** aus.

1. Weisen Sie auf dem Blatt ** Objekte** auf die **Schlüssel, Geheimnisse und Zertifikate** hin.

1. Wählen Sie **Schlüssel** und dann **+ Generieren/Importieren** aus.

1. Geben Sie dem Schlüssel einen **Namen**, und wählen Sie dann **Erstellen** aus, um den Schlüssel zu erstellen. Standardwerte übernehmen

## Konfigurieren des Speicherkontos für die verwaltete Identität und den Schlüsseltresor, Zuweisen von Berechtigungen

1. Kehren Sie zum Speicherkonto zurück.

1. Wählen Sie im Bereich**Sicherheit + Netzwerk**die Option**Verschlüsselung**aus.

    - Wählen Sie **Von Kunden verwaltete Schlüssel** aus. Diskutieren Sie den Unterschied zwischen einem von Microsoft verwalteten Schlüssel und kundenseitig verwalteten Schlüsseln. Beispielsweise wird ein von Microsoft verwalteter Schlüssel für die automatische Verschlüsselung und Entschlüsselung von Speicher verwendet. Ein kundenseitig verwalteter Schlüssel kann von einer App verwendet werden. Weitere Informationen finden Sie unter [Kundenseitig verwaltete Schlüssel](https://learn.microsoft.com/azure/storage/common/customer-managed-keys-overview).

    - Wählen Sie unter **Schlüsselspeichertyp** die Option **Schlüsseltresor** aus. Schlüssel können in Software (Schlüsseltresor) oder in Hardware (Hardwaresicherheitsmodul) gespeichert werden. Wir verwenden den Schlüsseltresor.

    - Wählen Sie **Schlüsseltresor** und **Schlüssel** aus.

    - Wählen Sie unter **Identitätstyp** die Option **Systemseitig zugewiesene verwaltete Identität** aus. Dies ist der Standardwert, der die verwaltete Identität konfiguriert, damit sie auf den Schlüsseltresor zugreifen kann.

1. [Unterstützende Folie] An diesem Punkt haben Sie der verwalteten Identität Zugriff auf den Schlüsseltresor gegeben und die Identität mit dem Speicherkonto verknüpft. Nun müssen wir der verwalteten Identität Zugriff auf das Speicherkonto geben. Weitere Informationen finden Sie unter [Azure-Rollenzuweisungen](https://learn.microsoft.com/azure/role-based-access-control/role-assignments).

1. Kehren Sie zu Ihrem Speicherkonto zurück, und wählen Sie die Option **Zugriffssteuerung (IAM)** aus. Weitere Informationen finden Sie unter [Integrierte Azure-Rollen](https://learn.microsoft.com/azure/role-based-access-control/built-in-roles)

    - Klicken Sie auf **Hinzufügen**, und wählen Sie dann **Rollenzuweisung hinzufügen** aus. Weisen Sie auf der Registerkarte **Zuweisungstyp** darauf hin, dass wir eine Positionsrolle zuweisen.

    - Wechseln Sie zur **Registerkarte Rolle**, und suchen Sie nach **BLOB**. Wählen Sie die Rolle **Storage-Blobdatenleser** aus.

    - Wechseln Sie zur Registerkarte **Mitglieder**, und weisen Sie den Zugriff der **verwalteten Identität** zu.

    - Wählen Sie **Mitglieder auswählen** und dann Ihre **benutzerseitig zugewiesene verwaltete Identität** aus.

## Konfigurieren von unveränderlichem Speicher

1. [Unterstützende Folie] Entwickler*innen müssen die Möglichkeit haben, geschäftskritische Daten zu speichern, die während eines benutzerseitig festgelegten Zeitraums weder geändert noch gelöscht werden können. Mit unveränderlichem Speicher können Sie Ihre Daten davor schützen, überschrieben oder gelöscht zu werden. Diskutieren Sie zeitbasierte und gesetzliche Aufbewahrungsrichtlinien. Erfahren Sie mehr, [Unveränderlicher Speicher](https://learn.microsoft.com/azure/storage/blobs/immutable-storage-overview).

1. Wählen Sie in Ihrem**Speicherkonto** das Blat t**Container**aus.

1. **Erstellen Sie** einen Container namens **Hold** und **laden** , Sie eine Datei in den Container hoch.

1. Greifen Sie auf Ihren **Haltecontainer**zu, und wählen Sie das **Access-Richtlinienblatt** aus.

1. Wählen Sie im Abschnitt **Unveränderlicher Blobspeicher** die Option **Richtlinie hinzufügen** aus.

1. Wählen Sie als **Richtlinientyp**die Option **Zeitbasierte Aufbewahrung** aus.

1. Legen Sie den **Aufbewahrungszeitraum** auf **5 Tage** fest.

1. Klicken Sie auf **Speichern**, um die Änderungen zu speichern.

1. Versuchen Sie, die Datei aus dem Container zu entfernen.

1. Vergewissern Sie sich, dass Sie die Datei aufgrund der Richtlinie nicht löschen können.

## Konfigurieren Sie einen Verschlüsselungsbereich für die Infrastrukturverschlüsselung.

1. Die Entwickler müssen auch die Infrastrukturverschlüsselung auf Containerebene festlegen. Diskutieren Sie Verschlüsselungsbereiche und Infrastrukturverschlüsselung. Erfahren Sie mehr, [Verschlüsselungsbereiche](https://learn.microsoft.com/azure/storage/blobs/encryption-scope-overview).

1. Container im **Speicherkonto**

1. Wählen Sie im Abschnitt **Sicherheit + Netzwerkbetrieb** die Option **Verschlüsselung** aus.

1. Wechseln Sie zur Registrierkarte **Verschlüsselungsbereich**, und wählen Sie "**+Hinzufügen**aus.

1. Geben Sie Ihrem **Verschlüsselungsbereich** einen **Namen**.

1. Vergewissern Sie sich, dass die **Infrastrukturverschlüsselung**aktiviert**ist**. Weisen Sie auf den Hinweis hin: "Diese Option kann nicht geändert werden, nachdem dieser Verschlüsselungsbereich erstellt wurde."

>**Hinweis**: Die Kursteilnehmer sollten jetzt in der Lage sein, LAB_04 zu kompleieren. 
