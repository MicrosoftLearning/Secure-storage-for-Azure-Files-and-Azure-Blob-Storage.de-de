---
lab:
  title: 'Übung 02b: Bereitstellen von privatem Speicher für interne Unternehmensdokumente'
  module: Guided Project - Azure Files and Azure Blobs
---


Das Unternehmen benötigt Speicher für seine Büros und Abteilungen. Diese Inhalte sind für das Unternehmen vertraulich und dürfen nicht ohne Zustimmung weitergegeben werden. Dieser Speicher erfordert Hochverfügbarkeit, wenn es zu einem regionalen Ausfall kommt. Das Unternehmen möchte diesen Speicher verwenden, um die öffentliche Website zu sichern. 

## Architekturdiagramm

![Diagramm mit einem Speicherkonto und zwei Blobcontainern](../Media/task-3.png)

## Qualifikationsaufgabe
- Erstellen eines Speicherkontos für die vertraulichen Dokumente des Unternehmens
- Konfigurieren von Redundanz für das Speicherkonto 
- Konfigurieren einer Shared Access Signature für eingeschränkten Partnerzugriff auf eine Datei 
- Sichern des Speichers der öffentlichen Website
- Implementieren der Lebenszyklusverwaltung, um Inhalte auf die kalte Zugriffsebene zu verschieben

## Übungsanweisungen

> **Hinweis**: Diese Anweisungen setzen voraus, dass Sie **Lab 02a**, Bereitstellen von Speicher für interne Dokumente, abgeschlossen haben.

## Erstellen eines Speicherkontos und Konfigurieren von hoher Verfügbarkeit

1. Erstellen Sie ein Speicherkonto für die internen, vertraulichen Dokumente des Unternehmens.
    - Suchen Sie im Portal nach der Option **Speicherkonten**, und wählen Sie sie aus.  
    - Wählen Sie **+ Erstellen** aus. 
    - Wählen Sie die **Ressourcengruppe** aus, die Sie im vorherigen Schritt erstellt haben.   
    - Legen Sie `private` als **Speicherkontonamen** fest. Fügen Sie dem Namen einen Bezeichner hinzu, um sicherzustellen, dass der Name eindeutig ist. 
    - Wählen Sie **Überprüfen** und dann **Erstellen** aus, um das Speicherkonto zu erstellen. 
    - Warten Sie, bis das Speicherkonto bereitgestellt ist, und wählen Sie dann **Zu Ressource wechseln** aus.

1. Dieser Speicher erfordert Hochverfügbarkeit, wenn es zu einem regionalen Ausfall kommt. Lesezugriff in der sekundären Region ist nicht erforderlich. Konfigurieren Sie die entsprechende Stufe der **Redundanz**. 

    - Wählen Sie im Speicherkonto unter dem Abschnitt **Datenverwaltung** das Blatt **Redundanz** aus. 
    - Stellen Sie sicher, dass **Georedundanter Speicher (GRS)** ausgewählt ist.
    - **Aktualisieren** Sie die Seite. 
    - Überprüfen Sie die primären und sekundären Standortinformationen. 
    - **Speichern** Sie die Änderungen.

## Erstellen eines Speichercontainers, Hochladen einer Datei und Einschränken des Dateizugriffs 

1. Erstellen Sie einen privaten Speichercontainer für die Unternehmensdaten. 

    - Wählen Sie im Speicherkonto unter dem Abschnitt **Datenspeicher** das Blatt **Container** aus. 
    - Wählen Sie **+ Container** aus. 
    - Stellen Sie sicher, dass der **Name** des Containers `private` ist.
    - Stellen Sie sicher, dass die **Öffentliche Zugriffsebene****Privat (kein anonymer Zugriff)** ist.
    - Wenn Sie Zeit haben, sehen Sie sich die **erweiterten** Einstellungen an, verwenden Sie aber die Standardwerte. 
    - Klicken Sie auf **Erstellen**. 

1.  Laden Sie zum Testen eine Datei in den **privaten** Container hoch. Der Dateityp spielt keine Rolle. Eine kleine Bild- oder Textdatei ist hierfür gut geeignet. Prüfen Sie, ob die Datei wirklich nicht öffentlich zugänglich ist. 

    - Wählen Sie den Container aus.
    - Wählen Sie die Option **Hochladen**.
    - **Navigieren Sie zu Dateien**, und wählen Sie eine Datei aus.
    - **Laden Sie die Datei hoch**.
    - Wählen Sie die hochgeladene Datei aus.
    - Kopieren Sie auf der Registerkarte **Übersicht** die **URL**.
    - Fügen Sie die **URL** in einen neuen Browsertab ein. 
    - Überprüfen Sie, ob die Datei nicht angezeigt wird, und Sie erhalten eine Fehlermeldung. 

1. Ein externer Partner benötigt mindestens für die nächsten 24 Stunden Lese- und Schreibzugriff auf die Datei. Konfigurieren und testen Sie eine SAS (Shared Access Signature). Weitere Informationen zu [SAS (Shared Access Signature)](https://learn.microsoft.com/azure/storage/common/storage-sas-overview).

    - Wählen Sie Ihre hochgeladene Blobdatei aus, und wechseln Sie zur Registerkarte **SAS generieren**. 
    - Stellen Sie in de Dropdownlister ** Berechtigungen ** sicher, dass der Partner nur **über Leseberechtigungen** verfügt.
    - Vergewissern Sie sich, dass **Datum/Uhrzeit für Start und Ablauf** für die nächsten 24 Stunden eingestellt ist. 
    - Wählen Sie **SAS-Token und URL erzeugen** aus.
    - Kopieren Sie die **BLOB SAS-URL** in eine neue Browserregisterkarte.
    - Vergewissern Sie sich, dass Sie nicht mehr auf die Datei zugreifen können. Wenn Sie eine Bilddatei hochgeladen haben, wird sie im Browser angezeigt. Die  Datei wird heruntergeladen.

## Konfigurieren von Speicherzugriffsebenen und Inhaltsreplikation.

1. Um Kosten zu sparen, verschieben Sie Blobs nach 30 Tagen von der heißen auf die kalte Zugriffsebene. Weitere Informationen finden Sie unter [Verwalten des Azure Blob Storage-Lebenszyklus](https://learn.microsoft.com/azure/storage/blobs/lifecycle-management-policy-configure?tabs=azure-portal).

    - Navigieren Sie zum **Speicherkonto**.
    - Beachten Sie im Abschnitt **Übersicht** , dass die **Standardzugriffsebene** auf  **Hot** festgelegt ist. 
    - Wählen Sie im Abschnitt **Datenverwaltung** die Option **Lebenszyklusverwaltung** aus.
    - Wählen Sie **Regel hinzufügen** aus. 
    - Legen Sie den **Regelnamen** auf `movetocool`fest.
    - Legen Sie den **Regelbereich** auf **Regel auf alle Blobs im Speicherkonto anwenden** fest.
    - Wählen Sie **Weiter** aus.
    - Stellen Sie sicher, dass **Letzte Änderung** ausgewählt ist.
    - Legen Sie **Vor mehr als (Tagen)** auf **30** fest.
    - Wählen Sie in der Dropdownliste **Dann** die Option **In kalte Speicherebene verschieben** aus.
    - Überprüfen Sie während der Zeit andere Lebenszyklusoptionen in der Dropdownliste. 
    - Fügen Sie die Regel über **Hinzufügen** hinzu.
  
1. Die Dateien der öfffentlichen Website müssen auf einem anderen Speicherkonto gesichert werten (Erfahren Sie mehr [Objektreplikationen](https://learn.microsoft.com/azure/storage/blobs/object-replication-configure?tabs=portal).

    - Erstellen Sie in Ihrem Speicherkonto **einen** neuen Container`backup`. Verwenden Sie die Standardwerte. Wenn Sie detaillierte Anweisungen benötigen, lesen Sie bitte in Labor 02a nach. 
    - Navigieren Sie zu Ihrem Speicherkonto auf der **öffentlichen**Website. Dieses Speicherkonto wurde in der vorherigen Übung erstellt. 
        - Wählen Sie auf dem Blatt für die Datenbank unter **Datenverwaltung** die Option **Replikate** aus. 
        - Wählen Sie **Replikationsregeln erstellen** aus.
        - Legen Sie das **Zielspeicherkonto** auf das **private** Speicherkonto fest.
        - Legen Sie den **Quellcontainer** auf **öffentlich** und den **Zielcontainer** auf **Sicherung** fest.
        - **Erstellen** Sie die Replikationsregel. 
    - Wenn Sie Zeit haben, laden Sie optional eine Datei in den **öffentlichen** Container hoch. Kehren Sie zum**privaten** Speicherkonto zurück, und aktualisieren Sie den **Sicherungscontainer**. Innerhalb weniger Minuten wird die Datei Ihrer öffentlichen Website im Sicherungsordner angezeigt. 

>**Hinweis**Weitere Vorgehensweisen finden Sie im Modul [Konfigurieren von Azure Blob Storage](https://learn.microsoft.com/training/modules/configure-blob-storage/). Das Modul verfügt über eine interaktive Labsimulation, in der Sie das Erstellen von Blobspeichern weiter üben können. 

## Erweitern Ihrer Lernerfahrung mit Copilot

Copilot kann Sie bei Ihrem Lernprozess unterstützen. Copilot kann grundlegende technische Informationen, allgemeine Schritte, Vor- und Nachteile, Hilfe zur Problembehandlung, Anwendungsfälle, Codebeispiele und vieles mehr bereitstellen. Um auf Copilot zuzugreifen, öffnen Sie einen Edge-Browser, und wählen Sie "Copilot" (oben rechts) aus. Nehmen Sie sich einige Minuten Zeit, um diese Prompts auszuprobieren.
+ Welche Sicherheitsfeatures stehen zum Schutz von Azure Storage zur Verfügung?
+ Was ist ein Azure SAS und wie wird es verwendet?

## Weiterlernen im eigenen Tempo

+ [Konfigurieren der Sicherheit von Azure Storage](https://learn.microsoft.com/training/modules/configure-storage-security/) In diesem Abschnitt erfahren Sie, wie Sie allgemeine Sicherheitsfunktionen von Azure Storage wie Speicherzugriffssignaturen konfigurieren.
+ [Verwalten des Azure Blob Storage-Lebenszyklus](https://learn.microsoft.com/training/modules/configure-storage-security/) In diesem Abschnitt erfahren Sie, wie Sie die Datenverfügbarkeit während des gesamten Lebenszyklus von Azure Blob Storage verwalten.

## Wichtige Erkenntnisse

Herzlichen Glückwunsch zum erfolgreichen Abschluss des Labs. Hier sind die wichtigsten Erkenntnisse für dieses Lab. 
+ Azure Storage verfügt über viele Datenschutzfunktionen, darunter Verschlüsselung, Zugriffssteuerung, Netzwerksicherheit, Überwachung und Warnungen. 
+ Eine Shared Access Signature (SAS) ermöglicht den sicheren delegierten Zugriff auf Ressourcen in Ihrem Speicherkonto. Mit SAS können Sie genau steuern, wie ein Client auf Ihre Daten zugreifen kann.
+ Die Azure Blob Storage-Lebenszyklusverwaltung bietet eine regelbasierte Richtlinie, mit deren Hilfe Sie den Übergang von Blob-Daten auf die entsprechenden Zugriffsebenen und den Ablauf der Daten am Ende des Datenlebenszyklus umsetzen können.
+ Die Objektreplikation kopiert Blockblobs asynchron zwischen einem Quellspeicherkonto und einem Zielkonto.
