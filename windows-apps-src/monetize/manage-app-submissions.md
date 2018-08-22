---
author: mcleanbyron
ms.assetid: C7428551-4B31-4259-93CD-EE229007C4B8
description: Verwenden Sie diese Methoden in der Microsoft Store-Übermittlungs-API, um Übermittlungen für Apps zu verwalten, die in Ihrem Windows Dev Center-Konto registriert wurden.
title: Verwalten von App-Übermittlungen
ms.author: mcleans
ms.date: 04/30/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows10, UWP, Microsoft Store-Übermittlungs-API, App-Übermittlungen
ms.localizationpriority: medium
ms.openlocfilehash: db74614c9455bfeffb9cfa286e84f4de6d97f52d
ms.sourcegitcommit: ab92c3e0dd294a36e7f65cf82522ec621699db87
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
ms.locfileid: "1832431"
---
# <a name="manage-app-submissions"></a>Verwalten von App-Übermittlungen

Mithilfe der Methoden der Microsoft Store-Übermittlungs-API können Sie Übermittlungen für Ihre Apps verwalten, einschließlich gradueller Paketrollouts. Eine Einführung in die Microsoft Store-Übermittlungs-API einschließlich der Voraussetzungen für die Verwendung der API finden Sie unter [Erstellen und Verwalten von Übermittlungen mit MicrosoftStore-Diensten](create-and-manage-submissions-using-windows-store-services.md).

> [!IMPORTANT]
> Wenn Sie die Microsoft Store-Übermittlungs-API zum Erstellen einer App-Übermittlung verwenden, stellen Sie sicher, dass Sie weitere Änderungen an der Übermittlung ausschließlich mithilfe der API und nicht mit dem Dev Center-Dashboard durchführen. Wenn Sie das Dashboard zum Ändern einer Übermittlung verwenden, die ursprünglich mit der API erstellt wurde, können Sie die Übermittlung nicht länger mithilfe der API ändern oder übermitteln. In einigen Fällen kann der Fehlerstatus der Übermittlung belassen werden, mit dem die Übermittlung nicht fortgesetzt werden kann. In diesem Fall müssen Sie die Übermittlung löschen und eine neue Übermittlung erstellen.

> [!IMPORTANT]
> Sie können mit dieser API weder Übermittlungen für [Volumeneinkäufe über den Microsoft Store für Unternehmen und Microsoft Store für Bildungseinrichtungen](../publish/organizational-licensing.md) veröffentlichen noch Übermittlungen für [Branchenanwendungen](../publish/distribute-lob-apps-to-enterprises.md) direkt an Unternehmen. In beiden Fällen müssen Sie das Windows Dev Center-Dashboard verwenden, um die Übermittlung zu veröffentlichen.


<span id="methods-for-app-submissions" />

## <a name="methods-for-managing-app-submissions"></a>Methoden zum Verwalten von App-Übermittlungen

Verwenden Sie die folgenden Methoden zum Abrufen, Erstellen, Aktualisieren, Committen oder Löschen einer App-Übermittlung. Bevor Sie diese Methoden verwenden können, muss die App bereits in Ihrem Dev Center-Konto vorhanden sein, und Sie müssen zunächst eine Übermittlung für die App im Dashboard erstellen. Weitere Informationen finden Sie unter [Voraussetzungen](create-and-manage-submissions-using-windows-store-services.md#prerequisites).

<table>
<colgroup>
<col width="10%" />
<col width="30%" />
<col width="60%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Methode</th>
<th align="left">URI</th>
<th align="left">Beschreibung</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">GET</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}</td>
<td align="left"><a href="get-an-app-submission.md">Abrufen einer vorhandenen App-Übermittlung</a></td>
</tr>
<tr>
<td align="left">GET</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/status</td>
<td align="left"><a href="get-status-for-an-app-submission.md">Abrufen des Status einer vorhandenen App-Übermittlung</a></td>
</tr>
<tr>
<td align="left">POST</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions</td>
<td align="left"><a href="create-an-app-submission.md">Erstellen einer neuen App-Übermittlung</a></td>
</tr>
<tr>
<td align="left">PUT</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}</td>
<td align="left"><a href="update-an-app-submission.md">Aktualisieren einer vorhandenen App-Übermittlung</a></td>
</tr>
<tr>
<td align="left">POST</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/commit</td>
<td align="left"><a href="commit-an-app-submission.md">Committen einer neuen oder aktualisierten App-Übermittlung</a></td>
</tr>
<tr>
<td align="left">DELETE</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}</td>
<td align="left"><a href="delete-an-app-submission.md">Löschen einer App-Übermittlung</a></td>
</tr>
</tbody>
</table>

<span id="create-an-app-submission">

### <a name="create-an-app-submission"></a>Erstellen einer App-Übermittlung

Gehen Sie folgendermaßen vor, um eine Übermittlung für eine App zu erstellen.

1. Falls noch nicht geschehen, erfüllen Sie alle [Voraussetzungen](create-and-manage-submissions-using-windows-store-services.md#prerequisites) für die Microsoft Store-Übermittlungs-API.
    > [!NOTE]
    > Stellen Sie sicher, dass für die App mindestens eine abgeschlossene Übermittlung mit abgeschlossenen Informationen zu den [Altersfreigaben](https://msdn.microsoft.com/windows/uwp/publish/age-ratings) vorhanden ist.

2. [Rufen Sie ein Azure AD-Zugriffstoken ab](create-and-manage-submissions-using-windows-store-services.md#obtain-an-azure-ad-access-token). Sie müssen dieses Zugriffstoken an die Methoden in der Microsoft Store-Übermittlungs-API übergeben. Nachdem Sie ein Zugriffstoken abgerufen haben, können Sie es 60Minuten lang verwenden, bevor es abläuft. Wenn das Token abgelaufen ist, können Sie ein neues abrufen.

3. [Erstellen Sie eine App-Übermittlung](create-an-app-submission.md) mithilfe der folgenden Methode in der Microsoft Store-Übermittlungs-API. Diese Methode erstellt eine neue laufende Übermittlung, die eine Kopie der letzten veröffentlichten Übermittlung ist.

    ```
    POST https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions
    ```

    Der Antworttext enthält eine [App-Übermittlungs](#app-submission-object)-Ressource, die die ID der neuen Übermittlung enthält, die SAS-URI (Shared Access Signature) zum Hochladen aller entsprechenden Dateien für die Übermittlung an Azure Blob Storage (z. B. App-Pakete, Eintragsbilder und Trailer-Dateien) und alle Daten für die neue Übermittlung (z. B. Eintrags- und Preisinformationen).

    > [!NOTE]
    > Ein SAS-URI ermöglicht den Zugriff auf eine sichere Ressource in Azure Storage, ohne dass Kontoschlüssel benötigt werden. Hintergrundinformationen zu SAS-URIs und deren Verwendung mit Azure Blob Storage finden Sie unter [Shared Access Signatures, Teil 1: Verstehen des SAS-Modells](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1) und [Shared Access Signatures, Teil 2: Erstellen und Verwenden einer SAS mit BLOB-Speicher](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-2/).

4. Wenn Sie neue Pakete, Eintragsbilder oder Trailer-Dateien für die Übermittlung hinzufügen, [müssen Sie die App-Pakete vorbereiten](https://msdn.microsoft.com/windows/uwp/publish/app-package-requirements) und auch [die App-Screenshots, -Bilder und -Trailer vorbereiten](https://msdn.microsoft.com/windows/uwp/publish/app-screenshots-and-images). Fügen Sie all diese Dateien einem ZIP-Archiv hinzu.

5. Revidieren Sie die [App-Übermittlungsdaten](#app-submission-object) mit allen erforderlichen Änderungen für die neue Übermittlung, und führen Sie die folgende Methode aus, um die [Übermittlung zu aktualisieren](update-an-app-submission.md).

    ```
    PUT https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}
    ```
      > [!NOTE]
      > Wenn Sie neue Dateien für die Übermittlung hinzufügen, müssen Sie die Übermittlungsdaten aktualisieren, damit diese auf den Namen und den relativen Pfad dieser Dateien im ZIP-Archiv verweisen.

4. Wenn Sie neue Pakete, Eintragsbilder oder Trailer-Dateien für die Übermittlung hinzufügen, müssen Sie das ZIP-Archiv mit dem SAS-URI auf [Azure Blob Storage](https://docs.microsoft.com/azure/storage/storage-introduction#blob-storage) hochladen, der im Antworttext der POST-Methode bereitgestellt wurde, die Sie zuvor aufgerufen haben. Zu diesem Zweck können Sie verschiedene Azure-Bibliotheken auf unterschiedlichen Plattformen verwenden, darunter:

    * [Azure Storage-Clientbibliothek für .NET](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-blobs)
    * [Azure Storage SDK für Java](https://docs.microsoft.com/azure/storage/storage-java-how-to-use-blob-storage)
    * [Azure Storage SDK für Python](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-blob-storage)

    Das folgende C#-Codebeispiel zeigt, wie Sie ein ZIP-Archiv mithilfe der [CloudBlockBlob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx)-Klasse in der Azure Storage-Clientbibliothek für .NET auf Azure Blob Storage hochladen. Im Beispiel wird davon ausgegangen, dass das ZIP-Archiv bereits in ein Datenstromobjekt geschrieben wurde.

    ```csharp
    string sasUrl = "https://productingestionbin1.blob.core.windows.net/ingestion/26920f66-b592-4439-9a9d-fb0f014902ec?sv=2014-02-14&sr=b&sig=usAN0kNFNnYE2tGQBI%2BARQWejX1Guiz7hdFtRhyK%2Bog%3D&se=2016-06-17T20:45:51Z&sp=rwl";
    Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob blockBob =
        new Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob(new System.Uri(sasUrl));
    await blockBob.UploadFromStreamAsync(stream);
    ```

5. Führen Sie folgende Methode aus, um [die App-Übermittlung zu committen](commit-an-app-submission.md). Hierdurch wird Dev Center darüber benachrichtigt, dass Sie Ihre Übermittlung fertig gestellt haben und die Updates nun auf Ihr Konto jetzt angewendet werden sollen.

    ```
    POST https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/commit
    ```

6. Überprüfen Sie den Commit-Status, indem Sie die folgende Methode ausführen, um [den Status der App-Übermittlung abzurufen](get-status-for-an-app-submission.md).

    ```
    GET https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/status
    ```

    Um den Status der Übermittlung zu überprüfen, zeigen Sie den Wert *status* im Antworttext an. Dieser Wert sollte von **CommitStarted** entweder in **PreProcessing** geändert worden sein, wenn die Anforderung erfolgreich war, oder in **CommitFailed**, wenn die Anforderung Fehler enthalten hat. Wenn Fehler aufgetreten sind, enthält das Feld *StatusDetails* Feld weitere Details zu den Fehlern.

7. Nachdem das Commit erfolgreich abgeschlossen wurde, wird die Übermittlung zur Aufnahme an den Store gesendet. Sie können den Übermittlungsstatus mithilfe der vorherigen Methode oder mithilfe des Dev Center-Dashboards weiter überwachen.

<span id="manage-gradual-package-rollout">

## <a name="methods-for-managing-a-gradual-package-rollout"></a>Methoden zum Verwalten eines graduellen Paketrollouts

Sie können die aktualisierten Pakete in einer App-Übermittlung graduell für einen bestimmten Prozentsatz der Kunden Ihrer App unter Windows 10 einführen. So können Sie Feedback und Analysedaten für die jeweiligen Pakete überwachen und vor einem umfassenden Rollout sicherstellen, dass das Update ordnungsgemäß funktioniert. Sie können den Rollout-Prozentwert für eine veröffentlichte Übermittlung ändern (oder die Aktualisierung anhalten), ohne dass Sie eine neue Übermittlung erstellen müssen. Weitere Informationen und Anleitungen zur Aktivierung und Verwaltung eines graduellen Paketrollouts im Dev Center-Dashboard finden Sie in [diesem Artikel](../publish/gradual-package-rollout.md).

Um ein graduelles Paketrollout für eine App-Übermittlung programmgesteuert zu aktivieren, gehen Sie wie folgt vor, und verwenden Sie dabei Methoden in der Microsoft Store-Übermittlungs-API:

  1. [Erstellen Sie eine App-Übermittlung](create-an-app-submission.md), oder [rufen Sie eine vorhandene App-Übermittlung ab](get-an-app-submission.md).
  2. Suchen Sie in den Antwortdaten die [packageRollout](#package-rollout-object)-Ressource, legen Sie das Feld *isPackageRollout* auf **true** und das Feld *packageRolloutPercentage* auf den Prozentsatz der Kunden Ihrer App fest, die die aktualisierten Pakete erhalten sollen.
  3. Übergeben Sie die aktualisierten App-Übermittlungsdaten an die Methode zum [Aktualisieren einer App-Übermittlung](update-an-app-submission.md).

Nachdem ein graduelles Paketrollout für eine App-Übermittlung aktiviert wurde, können Sie das graduelle Rollout mithilfe der folgenden Methoden programmgesteuert abrufen, aktualisieren, anhalten oder abschließen.

<table>
<colgroup>
<col width="10%" />
<col width="30%" />
<col width="60%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Methode</th>
<th align="left">URI</th>
<th align="left">Beschreibung</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">GET</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/packagerollout</td>
<td align="left"><a href="get-package-rollout-info-for-an-app-submission.md">Abrufen von Informationen zum graduellen Rollout einer App-Übermittlung</a></td>
</tr>
<tr>
<td align="left">POST</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/updatepackagerolloutpercentage</td>
<td align="left"><a href="update-the-package-rollout-percentage-for-an-app-submission.md">Aktualisieren des Prozentsatzes eines graduellen Rollouts einer App-Übermittlung</a></td>
</tr>
<tr>
<td align="left">POST</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/haltpackagerollout</td>
<td align="left"><a href="halt-the-package-rollout-for-an-app-submission.md">Anhalten des graduellen Rollouts einer App-Übermittlung</a></td>
</tr>
<tr>
<td align="left">POST</td>
<td align="left">https://manage.devcenter.microsoft.com/v1.0/my/applications/{applicationId}/submissions/{submissionId}/finalizepackagerollout</td>
<td align="left"><a href="finalize-the-package-rollout-for-an-app-submission.md">Abschließen des graduellen Rollouts einer App-Übermittlung</a></td>
</tr>
</tbody>
</table>


## <a name="code-examples-for-managing-app-submissions"></a>Codebeispiele für die Verwaltung von App-Übermittlungen

Die folgenden Artikel enthalten ausführliche Codebeispiele, die zeigen, wie Sie eine App-Übermittlung in verschiedenen Programmiersprachen erstellen:

* [C#-Beispiel: Übermittlungen für Apps, Add-Ons und Flights](csharp-code-examples-for-the-windows-store-submission-api.md)
* [C#-Beispiel: App-Übermittlung mit Spieloptionen und Trailer](csharp-code-examples-for-submissions-game-options-and-trailers.md)
* [Java-Beispiel: Übermittlungen für Apps, Add-Ons und Flights](java-code-examples-for-the-windows-store-submission-api.md)
* [Java-Beispiel: App-Übermittlung mit Spieloptionen und Trailer](java-code-examples-for-submissions-game-options-and-trailers.md)
* [Python-Beispiel: Übermittlungen für Apps, Add-Ons und Flights](python-code-examples-for-the-windows-store-submission-api.md)
* [Python-Beispiel: App-Übermittlung mit Spieloptionen und Trailer](python-code-examples-for-submissions-game-options-and-trailers.md)

## <a name="storebroker-powershell-module"></a>StoreBroker PowerShell-Modul

Als Alternative zum direkten Aufruf der Microsoft Store-Übermittlungs-API stellen wir ein PowerShell-Modul (Open Source) bereit, das eine Befehlszeilenschnittstelle über der API implementiert. Dieses Modul heißt [StoreBroker](https://aka.ms/storebroker). Sie können dieses Modul verwenden, um Ihre App-, Flight- und Add-On-Übermittlungen über die Befehlszeile anstatt über die Microsoft Store-Übermittlungs-API direkt zu verwalten. Sie können auch ganz einfach die Quelle durchsuchen, um weitere Beispiele für das Aufrufen dieser API zu erhalten. Das StoreBroker-Modul wird innerhalb von Microsoft aktiv als primäre Methode verwendet, durch die viele Erstanbieter-Apps an den Store übermittelt werden.

Weitere Informationen finden Sie auf unserer [StoreBroker-Seite auf GitHub](https://aka.ms/storebroker).

<span/>

## <a name="data-resources"></a>Datenressourcen
Die Methoden der Microsoft Store-Übermittlungs-API für das Verwalten von App-Übermittlungen verwenden die folgenden JSON-Datenressourcen.

<span id="app-submission-object" />

### <a name="app-submission-resource"></a>Ressource für App-Übermittlungen

Diese Ressource beschreibt eine App-Übermittlung.

```json
{
  "id": "1152921504621243540",
  "applicationCategory": "BooksAndReference_EReader",
  "pricing": {
    "trialPeriod": "FifteenDays",
    "marketSpecificPricings": {},
    "sales": [],
    "priceId": "Tier2",
    "isAdvancedPricingModel": true
  },
  "visibility": "Public",
  "targetPublishMode": "Manual",
  "targetPublishDate": "1601-01-01T00:00:00Z",
  "listings": {
    "en-us": {
      "baseListing": {
        "copyrightAndTrademarkInfo": "",
        "keywords": [
          "epub"
        ],
        "licenseTerms": "",
        "privacyPolicy": "",
        "supportContact": "",
        "websiteUrl": "",
        "description": "Description",
        "features": [
          "Free ebook reader"
        ],
        "releaseNotes": "",
        "images": [
          {
            "fileName": "contoso.png",
            "fileStatus": "Uploaded",
            "id": "1152921504672272757",
            "description": "Main page",
            "imageType": "Screenshot"
          }
        ],
        "recommendedHardware": [],
        "title": "Contoso ebook reader"
      },
      "platformOverrides": {
        "Windows81": {
          "description": "Ebook reader for Windows 8.1"
        }
      }
    }
  },
  "hardwarePreferences": [
    "Touch"
  ],
  "automaticBackupEnabled": false,
  "canInstallOnRemovableMedia": true,
  "isGameDvrEnabled": false,
  "gamingOptions": [],
  "hasExternalInAppProducts": false,
  "meetAccessibilityGuidelines": true,
  "notesForCertification": "",
  "status": "PendingCommit",
  "statusDetails": {
    "errors": [],
    "warnings": [],
    "certificationReports": []
  },
  "fileUploadUrl": "https://productingestionbin1.blob.core.windows.net/ingestion/387a9ea8-a412-43a9-8fb3-a38d03eb483d?sv=2014-02-14&sr=b&sig=sdd12JmoaT6BhvC%2BZUrwRweA%2Fkvj%2BEBCY09C2SZZowg%3D&se=2016-06-17T18:32:26Z&sp=rwl",
  "applicationPackages": [
    {
      "fileName": "contoso_app.appx",
      "fileStatus": "Uploaded",
      "id": "1152921504620138797",
      "version": "1.0.0.0",
      "architecture": "ARM",
      "languages": [
        "en-US"
      ],
      "capabilities": [
        "ID_RESOLUTION_HD720P",
        "ID_RESOLUTION_WVGA",
        "ID_RESOLUTION_WXGA"
      ],
      "minimumDirectXVersion": "None",
      "minimumSystemRam": "None",
      "targetDeviceFamilies": [
        "Windows.Mobile min version 10.0.10240.0"
      ]
    }
  ],
  "packageDeliveryOptions": {
    "packageRollout": {
        "isPackageRollout": false,
        "packageRolloutPercentage": 0.0,
        "packageRolloutStatus": "PackageRolloutNotStarted",
        "fallbackSubmissionId": "0"
    },
    "isMandatoryUpdate": false,
    "mandatoryUpdateEffectiveDate": "1601-01-01T00:00:00.0000000Z"
  },
  "enterpriseLicensing": "Online",
  "allowMicrosoftDecideAppAvailabilityToFutureDeviceFamilies": true,
  "allowTargetFutureDeviceFamilies": {
    "Desktop": false,
    "Mobile": true,
    "Holographic": true,
    "Xbox": false,
    "Team": true
  },
  "friendlyName": "Submission 2",
  "trailers": []
}
```

Die Ressource hat die folgenden Werte.

| Wert      | Typ   | Beschreibung      |
|------------|--------|-------------------|
| id            | string  | Die ID der Übermittlung. Diese ID ist in den Antwortdaten für Anforderungen verfügbar, um [eine App-Übermittlung zu erstellen](create-an-app-submission.md), [alle Apps abzurufen](get-all-apps.md) und [eine App abzurufen](get-an-app.md). Für eine Übermittlung, die im Dev Center-Dashboard erstellt wurde, ist diese ID auch in der URL für die Übermittlungsseite im Dashboard verfügbar.  |
| applicationCategory           | string  |   Eine Zeichenfolge, die [Kategorie und/oder Unterkategorie](https://msdn.microsoft.com/windows/uwp/publish/category-and-subcategory-table) für Ihre App angibt. Kategorien und Unterkategorien werden mit einem Unterstrich "_" zu einer einzigen Zeichenfolge zusammengefasst, z.B. **BooksAndReference_EReader**.      |  
| pricing           |  object  | Eine [Preisressource](#pricing-object), die Preisinformationen für die App enthält.        |   
| visibility           |  string  |  Die Sichtbarkeit der App. Folgende Werte sind möglich: <ul><li>Hidden</li><li>Public</li><li>Private</li><li>NotSet</li></ul>       |   
| targetPublishMode           | string  | Der Publish-Modus für die Übermittlung. Folgende Werte sind möglich: <ul><li>Immediate</li><li>Manual</li><li>SpecificDate</li></ul> |
| targetPublishDate           | string  | Das Veröffentlichungsdatum der Übermittlung im ISO 8601-Format, wenn *TargetPublishMode* den Wert SpecificDate hat.  |  
| listings           |   object  |  Ein Verzeichnis von Schlüssel-Wert-Paaren, wobei ein Schlüssel ein Ländercode und ein Wert eine [Eintragsressource](#listing-object) ist, die Eintragsinfos für die App enthält.       |   
| hardwarePreferences           |  array  |   Ein Array von Zeichenfolgen, die die [Hardwareeinstellungen](https://msdn.microsoft.com/windows/uwp/publish/enter-app-properties#hardware_preferences) für die App definieren. Folgende Werte sind möglich: <ul><li>Touch</li><li>Keyboard</li><li>Mouse</li><li>Camera</li><li>NfcHce</li><li>Nfc</li><li>BluetoothLE</li><li>Telephony</li></ul>     |   
| automaticBackupEnabled           |  boolean  |   Gibt an, ob Windows die App-Daten in automatische Sicherungen auf OneDrive aufnehmen können. Weitere Informationen finden Sie unter [App-Deklarationen](https://msdn.microsoft.com/windows/uwp/publish/app-declarations).   |   
| canInstallOnRemovableMedia           |  boolean  |   Gibt an, ob Kunden die App auf Wechselmedien installieren können. Weitere Informationen finden Sie unter [App-Deklarationen](https://msdn.microsoft.com/windows/uwp/publish/app-declarations).     |   
| isGameDvrEnabled           |  boolean |   Gibt an, ob game DVR für die App aktiviert ist.    |   
| gamingOptions           |  Array |   Ein Array mit einer [Gaming-Options-Ressource](#gaming-options-object), die die spielbezogenen Einstellungen für die App darstellt.     |   
| hasExternalInAppProducts           |     Boolescher Wert          |   Gibt an, ob die App Benutzern Käufe außerhalb des Microsoft Store-e-Commerce-Systems gestattet. Weitere Informationen finden Sie unter [App-Deklarationen](https://msdn.microsoft.com/windows/uwp/publish/app-declarations).     |   
| meetAccessibilityGuidelines           |    boolean           |  Gibt an, ob getestet wurde, ob die App die Richtlinien zur Barrierefreiheit erfüllt. Weitere Informationen finden Sie unter [App-Deklarationen](https://msdn.microsoft.com/windows/uwp/publish/app-declarations).      |   
| notesForCertification           |  string  |   Enthält [Hinweise zur Zertifizierung](https://msdn.microsoft.com/windows/uwp/publish/notes-for-certification) für Ihre App.    |    
| status           |   string  |  Der Status der Übermittlung. Folgende Werte sind möglich: <ul><li>None</li><li>Canceled</li><li>PendingCommit</li><li>CommitStarted</li><li>CommitFailed</li><li>PendingPublication</li><li>Publishing</li><li>Published</li><li>PublishFailed</li><li>PreProcessing</li><li>PreProcessingFailed</li><li>Certification</li><li>CertificationFailed</li><li>Release</li><li>ReleaseFailed</li></ul>      |    
| statusDetails           |   object  | Eine [Ressource für Statusdetails](#status-details-object), die zusätzliche Details über den Status der Übermittlung enthält, einschließlich Fehlerinformationen.       |    
| fileUploadUrl           |   string  | Der Shared Access Signature (SAS)-URI für das Hochladen der Pakete für die Übermittlung. Wenn Sie neue Pakete, Eintragsbilder oder Trailer-Dateien für die Übermittlung hinzufügen, müssen Sie das ZIP-Archiv, das die Pakete und Bilder enthält, zu dieser URI hochladen. Weitere Informationen finden Sie unter [Erstellen einer App-Übermittlung](#create-an-app-submission).       |    
| applicationPackages           |   array  | Ein Array von [Ressourcen für Anwendungspakete](#application-package-object), die Details über die einzelnen Pakete in der Übermittlung bereitstellen. |    
| packageDeliveryOptions    | object  | Eine [Ressource für Paketübermittlungsoptionen](#package-delivery-options-object), die Einstellungen zu graduellen Paketrollouts und zu verpflichtenden Updates für die Übermittlung enthält.  |
| enterpriseLicensing           |  string  |  Einer der [Werte für Enterprise-Lizenzierung](#enterprise-licensing), die das Verhalten der Enterprise-Lizenzierung für die App angeben.  |    
| allowMicrosoftDecideAppAvailabilityToFutureDeviceFamilies           |  Boolescher Wert   |  Gibt an, ob Microsoft [die App für zukünftige Windows10-Gerätefamilien verfügbar machen](https://msdn.microsoft.com/windows/uwp/publish/set-app-pricing-and-availability#windows-10-device-families) darf.    |    
| allowTargetFutureDeviceFamilies           | object   |  Ein Verzeichnis von Schlüssel-Wert-Paaren, wobei jeder Schlüssel eine [Windows10-Gerätefamilie](https://msdn.microsoft.com/windows/uwp/publish/set-app-pricing-and-availability#windows-10-device-families) ist und jeder Wert ein boolescher Wert ist, der angibt, ob Ihre App auf die angegebene Gerätefamilie ausgerichtet werden darf.     |    
| friendlyName           |   String  |  Der Anzeigename der Übermittlung, wie er im Dev Center-Dashboard erscheint. Dieser Wert wird beim Erstellen der Übermittlung für Sie generiert.       |  
| trailers           |  Array |   Ein Array mit bis zu 15 [Trailer-Ressourcen](#trailer-object), die Videotrailer für den App-Eintrag darstellen.<br/><br/>   |  


<span id="pricing-object" />

### <a name="pricing-resource"></a>Preisressource

Diese Ressource enthält Preisinformationen für die App. Die Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung        |
|-----------------|---------|------|
|  trialPeriod               |    string     |  Eine Zeichenfolge, die den Testzeitraum für die App angibt. Folgende Werte sind möglich: <ul><li>NoFreeTrial</li><li>OneDay</li><li>TrialNeverExpires</li><li>SevenDays</li><li>FifteenDays</li><li>ThirtyDays</li></ul>    |
|  marketSpecificPricings               |    object     |  Ein Verzeichnis von Schlüssel-Wert-Paaren, wobei jeder Schlüssel ein aus zwei Buchstaben bestehender ISO3166-1-Alpha-2-Ländercode ist und jeder Wert ein [Preisniveau](#price-tiers) ist. Diese Elemente stellen die [benutzerdefinierten Preise für Ihre App in bestimmten Märkten](https://msdn.microsoft.com/windows/uwp/publish/define-pricing-and-market-selection#markets-and-custom-prices) dar. Alle Elemente in diesem Verzeichnis überschreiben den durch den Wert *priceId* angegebenen Basispreis für den angegebenen Markt.      |     
|  sales               |   array      |  **Veraltet** Ein Array von [Verkaufsressourcen](#sale-object), die Verkaufsinformationen für die App enthalten.   |     
|  priceId               |   string      |  Ein [Preisniveau](#price-tiers), das den [Basispreis](https://msdn.microsoft.com/windows/uwp/publish/define-pricing-and-market-selection#base-price) für die App angibt.   |     
|  isAdvancedPricingModel               |   Boolean      |  Bei **true** hat Ihr Entwicklerkonto Zugriff auf die erweiterten Spanne von Preisstufen von 0,99 US-Dollar bis 1.999,99 US-Dollar. Bei **false** hat Ihr Entwicklerkonto Zugriff auf die ursprüngliche Spanne von Preisstufen von 0,99 US-Dollar bis 999,99 US-Dollar. Weitere Informationen zu den verschiedenen Stufen finden Sie unter [Preisstufen](#price-tiers).<br/><br/>**Hinweis**&nbsp;&nbsp;Dieses Feld ist schreibgeschützt.   |


<span id="sale-object" />

### <a name="sale-resource"></a>Verkaufsressource

Diese Ressource enthält die Verkaufsinformationen für eine App.

> [!IMPORTANT]
> Die **Verkaufsressource** wird nicht mehr unterstützt. Zurzeit können Sie die Verkaufsdaten einer App-Übermittlung nicht mithilfe der Microsoft Store-Übermittlungs-API abrufen oder ändern. Die Microsoft Store-Übermittlungs-API wird in der Zukunft aktualisiert werden, um ein neues Verfahren für den programmgesteuerten Zugriff auf Verkaufsinformationen für App-Übermittlungen einzuführen.
>    * Nach dem Aufrufen der [GET-Methode zum Abrufen einer App-Übermittlung](get-an-app-submission.md) ist der Wert *sales* leer. Sie können weiterhin das Dev Center-Dashboard verwenden, um die Verkaufsdaten für Ihre App-Übermittlung abzurufen.
>    * Beim Aufrufen der [PUT-Methode zum Aktualisieren einer App-Übermittlung](update-an-app-submission.md) werden die Informationen im Wert *sales* ignoriert. Sie können weiterhin das Dev Center-Dashboard verwenden, um die Verkaufsdaten für Ihre App-Übermittlung zu ändern.

Diese Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung    |
|-----------------|---------|------|
|  name               |    string     |   Der Name des Verkaufs.    |     
|  basePriceId               |   string      |  Das [Preisniveau](#price-tiers), das für den Basispreis des Verkaufs verwendet werden soll.    |     
|  startDate               |   string      |   Das Startdatum für den Verkauf im Format ISO8601.  |     
|  endDate               |   string      |  Das Enddatum für den Verkauf im Format ISO8601.      |     
|  marketSpecificPricings               |   object      |   Ein Verzeichnis von Schlüssel-Wert-Paaren, wobei jeder Schlüssel ein aus zwei Buchstaben bestehender ISO3166-1-Alpha-2-Ländercode ist und jeder Wert ein [Preisniveau](#price-tiers) ist. Diese Elemente stellen die [benutzerdefinierten Preise für Ihre App in bestimmten Märkten](https://msdn.microsoft.com/windows/uwp/publish/define-pricing-and-market-selection#markets-and-custom-prices) dar. Alle Elemente in diesem Verzeichnis überschreiben den durch den Wert *basePriceId* angegebenen Basispreis für den angegebenen Markt.    |


<span id="listing-object" />

### <a name="listing-resource"></a>Eintragsressource

Diese Ressource enthält die Eintragsinformationen für eine App. Die Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung                  |
|-----------------|---------|------|
|  baseListing               |   object      |  Die Informationen für den [Basiseintrag](#base-listing-object) für die App, die die standardmäßigen Eintragsinformationen für alle Plattformen definiert.   |     
|  platformOverrides               | object |   Ein Verzeichnis von Schlüssel-Wert-Paaren, in denen jeder Schlüssel eine Zeichenfolge ist, die eine Plattform identifiziert, für die die Eintragsinformationen überschrieben werden sollen, und jeder Wert eine [Basiseintragsressource](#base-listing-object) ist (die nur die Werte von Beschreibung bis Titel enthält), die die Eintragsinformationen angibt, die für die angegebene Plattform überschrieben werden sollen. Die Schlüssel können die folgenden Werte haben: <ul><li>Unknown</li><li>Windows80</li><li>Windows81</li><li>WindowsPhone71</li><li>WindowsPhone80</li><li>WindowsPhone81</li></ul>     |      |     

<span id="base-listing-object" />

### <a name="base-listing-resource"></a>Ressource für Basiseinträge

Diese Ressource enthält die Basiseintragsinformationen für eine App. Die Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung       |
|-----------------|---------|------|
|  copyrightAndTrademarkInfo                |   string      |  Optionale [Copyright- und/oder Markeninformationen](https://msdn.microsoft.com/windows/uwp/publish/create-app-descriptions#copyright-and-trademark-info).  |
|  keywords                |  array       |  Ein Array von [keyword](https://msdn.microsoft.com/windows/uwp/publish/create-app-descriptions#keywords), um die Anzeige Ihrer App in Suchergebnissen zu unterstützen.    |
|  licenseTerms                |    string     | Die optionalen [Lizenzbestimmungen](https://msdn.microsoft.com/windows/uwp/publish/create-app-descriptions#additional-license-terms) für Ihre App.     |
|  privacyPolicy                |   String      |   Dieser Wert ist veraltet. Um die URL zur Datenschutzrichtlinie für Ihre App festzulegen oder zu ändern, müssen Sie dies auf der [Eigenschaften](../publish/enter-app-properties.md#privacy-policy-url)-Seite im Dev Center-Dashboard ausführen. Sie können diesen Wert aus den Aufrufen an die Übermittlungs-API weglassen. Wenn Sie diesen Wert festlegen, wird er ignoriert werden.       |
|  supportContact                |   string      |  Dieser Wert ist veraltet. Um die URL für den Support-Kontakt oder eine E-Mail-Adresse für Ihre App festzulegen oder zu ändern, müssen Sie dies auf der [Eigenschaften](../publish/enter-app-properties.md#support-contact-info)-Seite im Dev Center-Dashboard ausführen. Sie können diesen Wert aus den Aufrufen an die Übermittlungs-API weglassen. Wenn Sie diesen Wert festlegen, wird er ignoriert werden.        |
|  websiteUrl                |   string      |  Dieser Wert ist veraltet. Um die URL der Webseite für Ihre App festzulegen oder zu ändern, müssen Sie dies auf der [Eigenschaften](../publish/enter-app-properties.md#website)-Seite im Dev Center-Dashboard ausführen. Sie können diesen Wert aus den Aufrufen an die Übermittlungs-API weglassen. Wenn Sie diesen Wert festlegen, wird er ignoriert werden.      |    
|  Beschreibung               |    string     |   Die [Beschreibung](https://msdn.microsoft.com/windows/uwp/publish/create-app-descriptions#description) für den App-Eintrag.   |     
|  features               |    array     |  Ein Array von bis zu 20Zeichenfolgen, die die [Features](https://msdn.microsoft.com/windows/uwp/publish/create-app-descriptions#app-features) für Ihre App auflisten.     |
|  releaseNotes               |  string       |  Die [Versionshinweise](https://msdn.microsoft.com/windows/uwp/publish/create-app-descriptions#release-notes) für Ihre App.    |
|  images               |   array      |  Ein Array von [Bild- und Symbolressourcen](#image-object) für den App-Eintrag.  |
|  recommendedHardware               |   array      |  Ein Array von bis zu 11Zeichenfolgen, die die [empfohlenen Hardwarekonfigurationen](../publish/create-app-store-listings.md#additional-information) für Ihre App auflisten.     |
|  minimumHardware               |     string    |  Ein Array von bis zu 11Zeichenfolgen, die die [minimalen Hardwarekonfigurationen](../publish/create-app-store-listings.md#additional-information) für Ihre App auflisten.    |  
|  title               |     String    |   Der Titel für den App-Eintrag.   |  
|  shortDescription               |     String    |  Wird nur für Spiele verwendet. Diese Beschreibung wird im Abschnitt **Informationen** im Spielehub auf Xbox One angezeigt und gibt weitere Informationen über Ihr Spiel an.   |  
|  shortTitle               |     String    |  Eine kürzere Version des Produktnamens. Wenn vorhanden, kann dieser kürzere Namen anstelle des Produkttitels an verschiedenen Stellen auf Xbox One angezeigt werden (während der Installation, in Ihren Erfolgen usw.).    |  
|  sortTitle               |     String    |   Wenn Ihr Produkt auf unterschiedliche Weise alphabetisch sortiert werden kann, können Sie hier eine andere Version eingeben. Dies kann Kunden bei der Suche helfen, das Produkt schneller zu finden.    |  
|  voiceTitle               |     String    |   Ein alternativer Name für das Produkt, das ggf. als Audio-Erlebnis auf Xbox One verwendet werden kann, wenn Kinect oder ein Kopfhörer genutzt wird.    |  
|  devStudio               |     String    |   Geben Sie diesen Wert an, wenn Sie ein **Entwickelt von**-Feld in den Eintrag aufnehmen möchten. (Das Feld **Veröffentlicht von** zeigt den mit Ihrem Konto verknüpften Anzeigename des Herausgebers an, wenn Sie einen Wert für das Feld *devStudio* angeben.)    |  

<span id="image-object" />

### <a name="image-resource"></a>Bildressource

Diese Ressource enthält Bild- und Symboldaten für einen App-Eintrag. Weitere Informationen zu Bildern und Symbolen für eine App finden Sie unter [App-Screenshots und -Bilder](../publish/app-screenshots-and-images.md). Diese Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung           |
|-----------------|---------|------|
|  fileName               |    string     |   Der Name der Bilddatei im ZIP-Archiv, das Sie für die Übermittlung hochgeladen haben.    |     
|  fileStatus               |   string      |  Der Status der Bilddatei. Folgende Werte sind möglich: <ul><li>None</li><li>PendingUpload</li><li>Uploaded</li><li>PendingDelete</li></ul>   |
|  id  |  String  | Die ID für das Bild. Dieser Wert wird von Dev Center bereitgestellt.  |
|  description  |  string  | Die Beschreibung für das Bild.  |
|  imageType  |  string  | Gibt den Typ des Bildes an. Die folgenden Strings werden derzeit unterstützt. <p/>[Bildschirmfoto-Bilder](../publish/app-screenshots-and-images.md#screenshots): <ul><li>Screenshot (verwenden Sie diesen Wert für den Desktop-Bildschirmfotos)</li><li>MobileScreenshot</li><li>XboxScreenshot</li><li>SurfaceHubScreenshot</li><li>HoloLensScreenshot</li></ul><p/>[Store-Logos](../publish/app-screenshots-and-images.md#store-logos):<ul><li>StoreLogo9x16 </li><li>StoreLogoSquare</li><li>Icon (verwenden Sie diesen Wert für die 1:1 300x300 Pixel-Logos)</li></ul><p/>[Werbebilder](../publish/app-screenshots-and-images.md#promotional-images): <ul><li>PromotionalArt16x9</li><li>PromotionalArtwork2400X1200</li></ul><p/>[Xbox-Bilder](../publish/app-screenshots-and-images.md#xbox-images): <ul><li>XboxBrandedKeyArt</li><li>XboxTitledHeroArt</li><li>XboxFeaturedPromotionalArt</li></ul><p/>[Optionale Werbebilder](../publish/app-screenshots-and-images.md#optional-promotional-images): <ul><li>SquareIcon358X358</li><li>BackgroundImage1000X800</li><li>PromotionalArtwork414X180</li></ul><p/> <!-- The following strings are also recognized for this field, but they correspond to image types that are no longer for listings in the Store.<ul><li>PromotionalArtwork846X468</li><li>PromotionalArtwork558X756</li><li>PromotionalArtwork414X468</li><li>PromotionalArtwork558X558</li><li>WideIcon358X173</li><li>Unknown</li></ul> -->   |


<span id="gaming-options-object" />

### <a name="gaming-options-resource"></a>Gaming-Optionsressource

Diese Ressource enthält Gaming-Einstellungen für die App. Die Werte in dieser Ressource entsprechen den [Spieleinstellungen](../publish/enter-app-properties.md#game-settings) für Übermittlungen im Dev Center-Dashboard.

```json
{
  "gamingOptions": [
    {
      "genres": [
        "Games_ActionAndAdventure",
        "Games_Casino"
      ],
      "isLocalMultiplayer": true,
      "isLocalCooperative": true,
      "isOnlineMultiplayer": false,
      "isOnlineCooperative": false,
      "localMultiplayerMinPlayers": 2,
      "localMultiplayerMaxPlayers": 12,
      "localCooperativeMinPlayers": 2,
      "localCooperativeMaxPlayers": 12,
      "isBroadcastingPrivilegeGranted": true,
      "isCrossPlayEnabled": false,
      "kinectDataForExternal": "Enabled"
    }
  ],
}
```

Diese Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung        |
|-----------------|---------|------|
|  genres               |    array     |  Ein Array aus einem oder mehreren der folgenden Zeichenfolgen, die die Genres des Spiels beschreiben: <ul><li>Games_ActionAndAdventure</li><li>Games_CardAndBoard</li><li>Games_Casino</li><li>Games_Educational</li><li>Games_FamilyAndKids</li><li>Games_Fighting</li><li>Games_Music</li><li>Games_Platformer</li><li>Games_PuzzleAndTrivia</li><li>Games_RacingAndFlying</li><li>Games_RolePlaying</li><li>Games_Shooter</li><li>Games_Simulation</li><li>Games_Sports</li><li>Games_Strategy</li><li>Games_Word</li></ul>    |
|  isLocalMultiplayer               |    Boolean     |  Gibt an, ob das Spiel lokale Multiplayer-Spiele unterstützt.      |     
|  isLocalCooperative               |   Boolean      |  Gibt an, ob das Spiel lokale Co-Op-Spiele unterstützt.    |     
|  isOnlineMultiplayer               |   Boolean      |  Gibt an, ob das Spiel Online-Multiplayer-Spiele unterstützt.    |     
|  isOnlineCooperative               |   Boolean      |  Gibt an, ob das Spiel Online-Co-Op-Spiele unterstützt.    |     
|  localMultiplayerMinPlayers               |   Int      |   Gibt die minimale Anzahl von Spielern an, die das Spiel für lokale Multiplayer-Spiele unterstützt.   |     
|  localMultiplayerMaxPlayers               |   Int      |   Gibt die maximale Anzahl von Spielern an, die das Spiel für lokale Multiplayer-Spiele unterstützt.  |     
|  localCooperativeMinPlayers               |   Int      |   Gibt die minimale Anzahl von Spielern an, die das Spiel für lokale Co-Op-Spiele unterstützt.  |     
|  localCooperativeMaxPlayers               |   Int      |   Gibt die maximale Anzahl von Spielern an, die das Spiel für lokale Co-Op-Spiele unterstützt.  |     
|  isBroadcastingPrivilegeGranted               |   Boolean      |  Gibt an, ob das Spiel Übertragungen unterstützt.   |     
|  isCrossPlayEnabled               |   Boolean      |   Gibt an, ob das Spiel Multiplayer-Sitzungen zwischen Spieler auf Windows10-PCs und Xbox unterstützt.  |     
|  kinectDataForExternal               |   String      |  Eine der folgenden Werte, der angibt, ob das Spiel Kinect-Daten sammeln und an externe Dienste senden kann: <ul><li>NotSet</li><li>Unknown</li><li>Enabled</li><li>Disabled</li></ul>   |

> [!NOTE]
> Die *gamingOptions*-Ressource wurde im Mai2017 nach der ersten Veröffentlichung der Microsoft Store-Übermittlungs-API für Entwickler hinzugefügt. Wenn Sie eine Übermittlung für eine App über die Übermittlungs-API erstellt haben bevor diese Ressource eingeführt wurden und die Übermittlung befindet sich noch in Bearbeitung, wird diese Ressource für Übermittlungen für die App Null sein, bis Sie die Übermittlung erfolgreich ausgeführt oder sie gelöscht haben. Wenn die *gamingOptions*-Ressource für Übermittlungen für eine App nicht verfügbar ist, ist das Feld *hasAdvancedListingPermission* der [Anwendungsressource](get-app-data.md#application_object), das von der [Eine App abrufen](get-an-app.md)-Methode zurückgegeben wird, falsch.

<span id="status-details-object" />

### <a name="status-details-resource"></a>Ressource für Statusdetails

Diese Ressource enthält weitere Informationen über den Status einer Übermittlung. Die Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung         |
|-----------------|---------|------|
|  errors               |    object     |   Ein Array von [Ressourcen für einzelne Statusdetails](#status-detail-object), die Fehlerdetails zur Übermittlung enthalten.    |     
|  warnings               |   object      | Ein Array von [Ressourcen für einzelne Statusdetails](#status-detail-object), die Warnungsdetails zur Übermittlung enthalten.      |
|  certificationReports               |     object    |   Ein Array von [Ressourcen für Zertifizierungsberichte](#certification-report-object), die den Zugriff auf die Zertifizierungsberichtsdaten für die Übermittlung ermöglichen. Sie können diese Berichte auf weitere Informationen überprüfen, wenn die Zertifizierung nicht erfolgreich ist.   |  


<span id="status-detail-object" />

### <a name="status-detail-resource"></a>Ressource für einzelne Statusdetails

Diese Ressource enthält weitere Informationen zu Fehlern oder Warnungen für eine Übermittlung. Die Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung        |
|-----------------|---------|------|
|  code               |    string     |   Ein [Übermittlungsstatuscode](#submission-status-code), der den Fehler- oder Warnungstyp beschreibt.   |     
|  details               |     string    |  Eine Meldung mit weiteren Details zum Problem.     |


<span id="application-package-object" />

### <a name="application-package-resource"></a>Ressource für Anwendungspakete

Diese Ressource enthält Details zu einem App-Paket für die Übermittlung.

```json
{
  "applicationPackages": [
    {
      "fileName": "contoso_app.appx",
      "fileStatus": "Uploaded",
      "id": "1152921504620138797",
      "version": "1.0.0.0",
      "architecture": "ARM",
      "languages": [
        "en-US"
      ],
      "capabilities": [
        "ID_RESOLUTION_HD720P",
        "ID_RESOLUTION_WVGA",
        "ID_RESOLUTION_WXGA"
      ],
      "minimumDirectXVersion": "None",
      "minimumSystemRam": "None",
      "targetDeviceFamilies": [
        "Windows.Mobile min version 10.0.10240.0"
      ]
    }
  ],
}
```

Diese Ressource hat die folgenden Werte.  

> [!NOTE]
> Beim Aufruf der Methode für das [Aktualisieren einer App-Übermittlung](update-an-app-submission.md) sind im Anforderungstext nur die Werte *fileName*, *fileStatus*, *minimumDirectXVersion* und *minimumSystemRam* dieses Objekts erforderlich. Die übrigen Werte werden von Dev Center aufgefüllt.

| Wert           | Typ    | Beschreibung                   |
|-----------------|---------|------|
| fileName   |   string      |  Der Name des Pakets.    |  
| fileStatus    | string    |  Der Status des Pakets. Folgende Werte sind möglich: <ul><li>None</li><li>PendingUpload</li><li>Uploaded</li><li>PendingDelete</li></ul>    |  
| id    |  string   |  Eine ID, die das Paket eindeutig identifiziert. Dieser Wert wird von Dev Center bereitgestellt.   |     
| version    |  string   |  Die Version des App-Pakets. Weitere Informationen finden Sie unter [Paketversionsnummern](https://msdn.microsoft.com/windows/uwp/publish/package-version-numbering).   |   
| architecture    |  string   |  Die Architektur des Pakets (z.B. ARM).   |     
| languages    | array    |  Ein Array von Sprachcodes für die Sprachen, die von der App unterstützt werden. Weitere Informationen finden Sie unter [Unterstützte Dateitypen](https://msdn.microsoft.com/windows/uwp/publish/supported-languages).    |     
| capabilities    |  array   |  Ein Array von Funktionen, die für das Paket erforderlich sind. Weitere Informationen zu Funktionen finden Sie unter [Deklaration der App-Funktionen](https://msdn.microsoft.com/windows/uwp/packaging/app-capability-declarations).   |     
| minimumDirectXVersion    |  string   |  Die DirectX-Version, die vom App-Paket mindestens unterstützt wird. Dies kann nur für Apps für Windows8.x festgelegt werden. Für Apps, die für andere Betriebssystemversionen bestimmt sind, muss dieser Wert beim Aufruf der [Aktualisieren einer App-Übermittlung](update-an-app-submission.md)-Methode vorhanden sein, aber der von Ihnen angegebene Wert wird ignoriert. Folgende Werte sind möglich: <ul><li>None</li><li>DirectX93</li><li>DirectX100</li></ul>   |     
| minimumSystemRam    | string    |  Die Menge an RAM, die für das App-Paket mindestens erforderlich ist. Dies kann nur für Apps für Windows8.x festgelegt werden. Für Apps, die für andere Betriebssystemversionen bestimmt sind, muss dieser Wert beim Aufruf der [Aktualisieren einer App-Übermittlung](update-an-app-submission.md)-Methode vorhanden sein, aber der von Ihnen angegebene Wert wird ignoriert. Folgende Werte sind möglich: <ul><li>None</li><li>Memory2GB</li></ul>   |       
| targetDeviceFamilies    | array    |  Ein Array von Zeichenfolgen, die die Gerätefamilien darstellen, auf die das Paket ausgerichtet ist. Dieser Wert wird nur für Pakete verwendet, die für Windows10 bestimmt sind. Im Fall von Paketen, die für frühere Versionen bestimmt sind, hat dieser Wert den Wert **None**. Die folgenden Gerätefamilienzeichenfolgen werden zurzeit für Windows10-Pakete unterstützt, wobei *{0}* eine Zeichenfolge für Windows10-Versionen ist, z.B. 10.0.10240.0, 10.0.10586.0 oder 10.0.14393.0: <ul><li>Windows.Universal min version *{0}*</li><li>Windows.Desktop min version *{0}*</li><li>Windows.Mobile min version *{0}*</li><li>Windows.Xbox min version *{0}*</li><li>Windows.Holographic min version *{0}*</li></ul>   |    

<span/>

<span id="certification-report-object" />

### <a name="certification-report-resource"></a>Ressource für Zertifizierungsberichte

Diese Ressource stellt den Zugriff auf die Zertifizierungsberichtsdaten für eine Übermittlung bereit. Die Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung             |
|-----------------|---------|------|
|     date            |    string     |  Das Datum und die Zeit im Format ISO8601, an dem und zu der der Bericht erstellte wurde.    |
|     reportUrl            |    string     |  Die URL, unter der Sie auf den Bericht zugreifen können.    |


<span id="package-delivery-options-object" />

### <a name="package-delivery-options-resource"></a>Ressource für Paketübermittlungsoptionen

Diese Ressource enthält Einstellungen zu graduellen Paketrollouts und zu verpflichtenden Updates für die Übermittlung.

```json
{
  "packageDeliveryOptions": {
    "packageRollout": {
        "isPackageRollout": false,
        "packageRolloutPercentage": 0,
        "packageRolloutStatus": "PackageRolloutNotStarted",
        "fallbackSubmissionId": "0"
    },
    "isMandatoryUpdate": false,
    "mandatoryUpdateEffectiveDate": "1601-01-01T00:00:00.0000000Z"
  },
}
```

Die Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung        |
|-----------------|---------|------|
| packageRollout   |   object      |  Eine [Ressource für Paketrollouts](#package-rollout-object), die Einstellungen zu graduellen Paketrollouts für die Übermittlung enthält.   |  
| isMandatoryUpdate    | boolean    |  Gibt an, ob die Pakete in dieser Übermittlung für automatisch installierte App-Updates als verpflichtend behandelt werden sollen. Weitere Informationen zu verpflichtenden Paketen für automatisch installierte App-Aktualisierungen finden Sie unter [Herunterladen und Installieren von Paketupdates für Ihre App](../packaging/self-install-package-updates.md).    |  
| mandatoryUpdateEffectiveDate    |  date   |  Zeitpunkt (Datum und Uhrzeit), zu dem die Pakete in dieser Übermittlung verpflichtend werden, im ISO 8601-Format und gemäß UTC-Zeitzone.   |        

<span id="package-rollout-object" />

### <a name="package-rollout-resource"></a>Ressource für Paketrollouts

Diese Ressource enthält [Einstellungen für graduelle Paketrollouts](#manage-gradual-package-rollout) für die Übermittlung. Die Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung        |
|-----------------|---------|------|
| isPackageRollout   |   boolean      |  Gibt an, ob für die Übermittlung der graduelle Paketrollout aktiviert ist.    |  
| packageRolloutPercentage    | float    |  Der Prozentsatz der Benutzer, die im Rahmen des graduellen Paketrollouts die Pakete erhalten.    |  
| packageRolloutStatus    |  string   |  Eine der folgenden Zeichenfolgen, die den Status des graduellen Paketrollouts angeben: <ul><li>PackageRolloutNotStarted</li><li>PackageRolloutInProgress</li><li>PackageRolloutComplete</li><li>PackageRolloutStopped</li></ul>  |  
| fallbackSubmissionId    |  string   |  Die ID der Übermittlung, die die Kunden erhalten, die keine Pakete im Rahmen des graduellen Paketrollouts erhalten.   |          

> [!NOTE]
> Die Werte *packageRolloutStatus* und *fallbackSubmissionId* werden von Dev Center zugewiesen und sollen nicht vom Entwickler festgelegt werden. Wenn Sie diese Werte in einen Anforderungstext einfügen, werden diese Werte ignoriert.

<span id="trailer-object" />

### <a name="trailers-resource"></a>Trailers-Ressource

Diese Ressource stellt ein Video-Trailer für den App-Eintrag dar. Die Werte in dieser Ressource entsprechen den [trailers](../publish/app-screenshots-and-images.md#trailers)-Optionen für Übermittlungen im Dev Center-Dashboard.

Sie können bis zu 15 Trailer Ressourcen zum Hinzufügen zum *Trailer*-Array in eine [App-Übermittlungsressource](#app-submission-object) einbeziehen. Um Videotrailer und Miniaturansichten für eine Übermittlung hochzuladen, fügen Sie diese Dateien zum selben ZIP-Archiv hinzu, das die Pakete und Bilder der Übermittlung enthält, und laden Sie dann das ZIP-Archiv über die SAS-URI (Shared Access Signature) für die Übermittlung hoch. Weitere Informationen zum Hochladen von ZIP-Archiv zu der SAS-URIs finden Sie unter [Erstellen einer App-Übermittlung](#create-an-app-submission).

```json
{
  "trailers": [
    {
      "id": "1158943556954955699",
      "videoFileName": "Trailers\\ContosoGameTrailer.mp4",
      "videoFileId": "1159761554639123258",
      "trailerAssets": {
        "en-us": {
          "title": "Contoso Game",
          "imageList": [
            {
              "fileName": "Images\\ContosoGame-Thumbnail.png",
              "id": "1155546904097346923",
              "description": "This is a still image from the video."
            }
          ]
        }
      }
    }
  ]
}
```

Diese Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung        |
|-----------------|---------|------|
|  id               |    String     |   Die ID für den Trailer. Dieser Wert wird von Dev Center bereitgestellt.   |
|  videoFileName               |    String     |    Der Name der Trailer-Videodatei im ZIP-Archiv, das die Dateien für die Übermittlung enthält.    |     
|  videoFileId               |   String      |  Die ID für die Videodatei. Dieser Wert wird von Dev Center bereitgestellt.   |     
|  trailerAssets               |   Objekt      |  Ein Wörterbuch von Schlüssel-Wert-Paaren, wobei ein Schlüssel ein Sprachcode und ein Wert eine [„trailer assets“-Ressource](#trailer-assets-object), die weitere gebietsschemaspezifischen Ressourcen für den Trailer enthält. Weitere Informationen zu den unterstützten Sprachcodes finden Sie unter [Unterstützte Sprachen](https://msdn.microsoft.com/windows/uwp/publish/supported-languages).    |     

> [!NOTE]
> Die *trailers*-Ressource wurde im Mai2017 nach der ersten Veröffentlichung der Microsoft Store-Übermittlungs-API für Entwickler hinzugefügt. Wenn Sie eine Übermittlung für eine App über die Übermittlungs-API erstellt haben bevor diese Ressource eingeführt wurden und die Übermittlung befindet sich noch in Bearbeitung, wird diese Ressource für Übermittlungen für die App Null sein, bis Sie die Übermittlung erfolgreich ausgeführt oder sie gelöscht haben. Wenn die *trailers*-Ressource für Übermittlungen für eine App nicht verfügbar ist, ist das Feld *hasAdvancedListingPermission* der [Anwendungsressource](get-app-data.md#application_object), das von der [Eine App abrufen](get-an-app.md)-Methode zurückgegeben wird, falsch.

<span id="trailer-assets-object" />

### <a name="trailer-assets-resource"></a>Trailer Assets-Ressource

Diese Ressource enthält weitere gebietsschemaspezifische Ressourcen für eine Trailer, der in einer [Trailer-Ressource](#trailer-object) definiert ist. Die Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung        |
|-----------------|---------|------|
| title   |   String      |  Der lokalisierte Titel des Trailers. Der Titel wird angezeigt, wenn der Benutzer den Trailer im Vollbildmodus anzeigt.     |  
| imageList    | Array    |   Ein Array mit einer [Bild](#image-for-trailer-object) Ressource, die das Miniaturbild für den Trailer bereitstellt. Sie können nur ein [Image](#image-for-trailer-object)-Ressource in diesem Array haben.  |   


<span id="image-for-trailer-object" />

### <a name="image-resource-for-a-trailer"></a>Image-Ressource (für eine Trailer)

Diese Ressource beschreibt die Miniaturansicht für ein Trailer. Die Ressource hat die folgenden Werte.

| Wert           | Typ    | Beschreibung           |
|-----------------|---------|------|
|  fileName               |    String     |   Der Name der Miniaturansicht im ZIP-Archiv, das Sie für die Übermittlung hochgeladen haben.    |     
|  id  |  String  | Die ID für die Miniaturansicht. Dieser Wert wird von Dev Center bereitgestellt.  |
|  description  |  String  | Die Beschreibung für die Miniaturansicht. Dieser Wert wird nur Metadaten verwendet und den Benutzern nicht angezeigt.   |

<span/>

## <a name="enums"></a>Enumerationen

Diese Methoden verwenden die folgenden Enumerationen.

<span id="price-tiers" />

### <a name="price-tiers"></a>Preisstufen

Die folgenden Werte stellen die verfügbaren Preisstufen in der [Ressource für Preise](#pricing-object) Ressource für eine App-Übermittlung dar.

| Wert           | Beschreibung        |
|-----------------|------|
|  Base               |   Das Preisniveau ist nicht festgelegt. Verwenden Sie den Basispreis für die App.      |     
|  NotAvailable              |   Die App ist für die angegebene Region nicht verfügbar.    |     
|  Free              |   Die App ist kostenlos.    |    
|  Stufe*xxx*               |   Eine Zeichenfolge, die die Preisstufe für die App im Format **Stufe<em>xxxx</em>** angibt. Derzeit werden die folgenden Spannen von Preisstufen unterstützt:<br/><br/><ul><li>Wenn der Wert *IsAdvancedPricingModel* für die [Ressource für Preise](#pricing-object) **true** ist, sind die für Ihr Konto verfügbaren Werte für Preisstufen **Stufe1012** - **Stufe1424**.</li><li>Wenn der Wert *IsAdvancedPricingModel* für die [Ressource für Preise](#pricing-object) **false** ist, sind die für Ihr Konto verfügbaren Werte für Preisstufen **Stufe1012** - **Stufe1424**.</li></ul>Eine vollständige Übersicht an Preisstufen, die für Ihr Entwicklerkonto verfügbar sind, einschließlich der marktspezifische Preise, die jeder Stufe zugeordnet sind, finden Sie auf der Seite **Preise und Verfügbarkeit** Ihrer App-Übermittlungen im Dev Center-Dashboard. Klicken Sie auf den Link **Tabelle anzeigen** im Abschitt **Märkte und benutzerdefinierte Preise** (bei einigen Entwicklerkonten befindet sich dieser Link im Abschnitt **Preise**).    |


<span id="enterprise-licensing" />

### <a name="enterprise-licensing-values"></a>Enterprise-Lizenzwerte

Die folgenden Werte stellen das Verhalten der App für die Unternehmenslizenzierung dar. Weitere Informationen zu diesen Optionen finden Sie unter [Lizenzierungsoptionen für Unternehmen](https://msdn.microsoft.com/windows/uwp/publish/organizational-licensing).

> [!NOTE]
> Obwohl Sie die Lizenzierungsoptionen für Unternehmen für eine App-Übermittlung über der Übermittlungs-API konfigurieren können, können Sie diese API nicht verwenden, um Übermittlungen für [Volumenkäufe über den Microsoft Store für Unternehmen und Microsoft Store für Bildungseinrichtungen](../publish/organizational-licensing.md) zu veröffentlichen. Um Übermittlungen an den Microsoft Store für Unternehmen und Microsoft Store für Bildungseinrichtungen zu veröffentlichen, müssen Sie das Windows Dev Center-Dashboard verwenden.


| Wert           |  Beschreibung      |
|-----------------|---------------|
| None            |     Ihre App soll Unternehmen nicht über die Store-verwaltete Volumenlizenzierung (Onlinevolumenlizenzierung) zur Verfügung gestellt werden.         |     
| Online        |     Ihre App soll Unternehmen über die Store-verwaltete Volumenlizenzierung (Onlinevolumenlizenzierung) zur Verfügung gestellt werden.  |
| OnlineAndOffline | Ihre App soll Unternehmen über die Store-verwaltete Volumenlizenzierung (Onlinevolumenlizenzierung) sowie über die Offlinelizenzierung zur Verfügung gestellt werden. |


<span id="submission-status-code" />

### <a name="submission-status-code"></a>Übermittlungsstatuscode

Die folgenden Werte stellen den Statuscode einer Übermittlung dar.

| Wert           |  Beschreibung      |
|-----------------|---------------|
| None            |     Es wurde kein Code angegeben.         |     
| InvalidArchive        |     Das ZIP-Archiv, das das Paket enthält, ist ungültig oder hat ein unbekanntes Archivformat.  |
| MissingFiles | Das ZIP-Archiv enthält nicht alle Dateien, die in den Übermittlungsdaten aufgeführt sind, oder sie befinden sich am falschen Speicherort im Archiv. |
| PackageValidationFailed | Mindestens ein Paket in der Übermittlung konnte nicht überprüft werden. |
| InvalidParameterValue | Einer der Parameter im Anforderungstext ist ungültig. |
| InvalidOperation | Der von Ihnen versuchte Vorgang ist ungültig. |
| InvalidState | Der von Ihnen versuchte Vorgang ist für den aktuellen Zustand des Flight-Pakets ungültig. |
| ResourceNotFound | Das angegebene Flight-Paket konnte nicht gefunden werden. |
| ServiceError | Ein interner Dienstfehler hat verhindert, dass die Anforderung erfolgreich ausgeführt wurde. Führen Sie die Anforderung erneut aus. |
| ListingOptOutWarning | Der Entwickler hat einen Eintrag aus einer vorherigen Übermittlung entfernt oder Eintragsinformationen nicht hinzugefügt, die vom Paket unterstützt werden. |
| ListingOptInWarning  | Der Entwickler hat einen Eintrag hinzugefügt. |
| UpdateOnlyWarning | Der Entwickler versucht, etwas einzufügen, für das nur Aktualisierungsunterstützung verfügbar ist. |
| Other  | Die Übermittlung befindet sich in einem nicht erkannten oder nicht kategorisierten Zustand. |
| PackageValidationWarning | Der Paketüberprüfungsvorgang hat zu einer Warnung geführt. |

<span/>

## <a name="related-topics"></a>Verwandte Themen

* [Erstellen und Verwalten von Übermittlungen mit Microsoft Store-Diensten](create-and-manage-submissions-using-windows-store-services.md)
* [Abrufen von App-Daten mit der Microsoft Store-Übermittlungs-API](get-app-data.md)
* [App-Übermittlungen im Dev Center-Dashboard](https://msdn.microsoft.com/windows/uwp/publish/app-submissions)