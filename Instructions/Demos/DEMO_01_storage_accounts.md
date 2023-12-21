---
demo:
  title: 'Demonstration 01: Erstellen und Konfigurieren von Speicherkonten'
  module: Guided Project - Azure Files and Azure Blobs
---
## Demonstration - Erstellen und Konfigurieren von Speicherkonten 

In dieser Demonstration werden Speicherkonten untersucht.

1. [Unterstützende Folie] Bevor Sie mit dieser Demonstration beginnen, sollten Sie diskutieren, wie Speicher organisiert ist und welche Faktoren berücksichtigt werden sollen. 

1. Öffnen Sie das **Azure-Portal**.

1. Wählen Sie im Suchfeld **Speicherkonton** aus. Sobald Sie mit der Eingabe beginnen, wird die Liste auf der Grundlage Ihrer Eingabe gefiltert.

1. Wählen Sie **Speicherkonten**.

1. Klicken Sie auf **Erstellen**.

1. Erläutern, wie die Azure-Portal eine benutzerfreundliche Assistentenschnittstelle bereitstellt. Erforderliche Elemente sind durch ein rotes Sternchen (*) gekennzeichnet.

1. Wählen Sie das **Abonnement** aus.

1. Wählen Sie die **Ressourcengruppe**.

1. Geben Sie einen Namen für Ihr Speicherkonto ein. Besprechen Sie die Benennungseinschränkungen für Speicherkonten.

1. Wählen Sie eine Region für Ihr Speicherkonto aus. Überprüfen Sie, welche Region Schüler im Labor verwenden sollen. Lesen Sie mehr über [Azure-Geografien](https://azure.microsoft.com/explore/global-infrastructure/geographies/).

1. [Unterstützende Folie] Wählen Sie die **Standardleistung** aus. Weitere Informationen zu [Speicherkontentypen](https://learn.microsoft.com/azure/storage/common/storage-account-overview).

1. [Unterstützende Folie] Wählen Sie **Redundanz** als **lokal redundanten** Speicher aus. Weitere Informationen zur [Redundanz in Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-redundancy)

1. Wechseln zur **Registerkarte "Erweitert** ". Markieren Sie im **Abschnitt "Sicherheit** " diese Einstellungen. Beachten Sie, dass wir nur einige Dinge behandeln, um den Kursteilnehmer in ihrem ersten Labor zu starten. 

    - **Sichere Übertragung für REST-API-Vorgänge erforderlich**. Standardmäßig sollte das Speicherkonto nur Anforderungen von sicheren Verbindungen akzeptieren. Erfahren Sie mehr, [sichere Übertragung](https://learn.microsoft.com/azure/storage/common/storage-require-secure-transfer).

    - **Zugriff auf Speicherkontoschlüssel aktivieren**. Besprechen Sie, wie diese Einstellung den Zugriff auf das Speicherkonto deaktivieren kann. Beispielsweise kann der Zugriff auf das Speicherkonto der IT-Abteilung deaktiviert werden. Diskutieren Sie, wie wichtig der Schutz des Schlüssels ist. Weitere Informationen zum [Verwalten von Zugriffsschlüsseln für Speicherkonten](https://learn.microsoft.com/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).

    - **TLS-Mindestversion** Erläutern Sie, dass Transport Layer Service für die Sicherung der Kommunikation über das Netzwerk dient. TLS ist eine verbesserte Version von SSL. Ihre Entwickler fragen möglicherweise, welche Versionen verfügbar sind. Weitere Informationen finden Sie im [Transport Layer Service](https://learn.microsoft.com/azure/storage/common/transport-layer-security-configure-minimum-version).

1. Erklären Sie, dass andere Registerkarten behandelt werden, wenn Die Schüler durch die Labore gehen.

1. Wählen Sie** "Überprüfen" aus, ** und stellen Siesicher, dass keine Überprüfungsfehler aufgetreten sind. Mögliche Überprüfungsfehler werden erläutert. 

1. Wählen Sie **Erstellen** aus, und warten Sie während das Speicherkonto bereitgestellt wird. Verweisen Sie auf die Benachrichtigungen.

1. Zeigen Sie, wie Sie **zur Ressource** wechseln. Diskutieren Sie andere Möglichkeiten, um zur Ressource zu gelangen.

>**Hinweis**: Die Kursteilnehmer sollten jetzt in der Lage sein, LAB_01 abzuschließen.
