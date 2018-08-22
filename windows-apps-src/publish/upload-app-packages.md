---
author: jnHs
Description: The Packages page is where you upload all of the package files (.appxupload, .appx, .appxbundle, and/or .xap) for the app that you're submitting.
title: Hochladen von App-Paketen
ms.assetid: B1BB810D-3EAA-4FB5-B03C-1F01AFB2DE36
ms.author: wdg-dev-content
ms.date: 5/10/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, Uwp, Pakete, hochladen, Paket hochladen
ms.localizationpriority: medium
ms.openlocfilehash: 6013a238cff8db3b85dd98af58cccaf344a72f51
ms.sourcegitcommit: f2f4820dd2026f1b47a2b1bf2bc89d7220a79c1a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2018
ms.locfileid: "2791782"
---
# <a name="upload-app-packages"></a>Hochladen von App-Paketen

Auf der Seite **Pakete** werden alle Paketdateien (APPX, APPXUPLOAD, APPXBUNDLE und XAP) für die App hochgeladen, die Sie übermitteln. Sie können in diesem Schritt Pakete für jedes Betriebssystem hochladen, auf das die App ausgerichtet ist. Wenn ein Kunde Ihre App herunterlädt, stellt der Store automatisch für jeden Kunden das Paket bereit, das am besten für sein Gerät geeignet ist. Nachdem Sie Ihre Pakete hochgeladen haben, sehen Sie eine Tabelle, in der angegeben wird, [welche Pakete für bestimmte Windows10-Gerätefamilien angeboten werden](#device-family-availability) (und ggf. für frühere Betriebssystemversionen).

Ausführliche Informationen zu Inhalt und Struktur der Pakete finden Sie unter [App-Paketanforderungen](app-package-requirements.md). Sie sollten auch weitere Informationen zu [auswirkt wie Versionsnummern von Paketen an bestimmten Kunden übermittelt werden](package-version-numbering.md) und [wie Pakete auf verschiedenen Betriebssystemen verteilt werden](guidance-for-app-package-management.md).

## <a name="uploading-packages-to-your-submission"></a>Hochladen von Paketen für Ihre Übermittlung

Um Pakete hochzuladen, ziehen Sie sie in das Uploadfeld oder klicken Sie, um Ihre Dateien zu durchsuchen. Auf der Seite **Pakete** können Sie die XAP-, APPX-, APPXUPLOAD- und/oder APPXBUNDLE-Dateien hochladen.

> [!IMPORTANT]
> Es wird empfohlen, für Windows10 die .appxupload-Datei anstelle einer.appx oder .appxbundle hochzuladen.  Weitere Informationen zum Verpacken von UWP-Apps für den Store finden Sie untere [Verpacken von UWP-App mit Visual Studio](../packaging/packaging-uwp-apps.md).

Falls Sie [Flight-Pakete](package-flights.md) für Ihre App erstellt haben, wird eine Dropdownliste mit der Option zum Kopieren von Paketen aus einem Ihrer Flight-Pakete angezeigt. Wählen Sie das Flight-Paket mit den Paketen aus, die Sie übertragen möchten. Anschließend können Sie einige oder alle der Pakete auswählen, um sie in diese Übermittlung aufzunehmen.

Wenn wir Fehler mit einem Paket erkennen, während überprüft wird, werden wir zeigt eine Meldung, damit Sie wissen, was falsch ist. Sie müssen das Paket entfernen, beheben Sie das Problem, und versuchen Sie es erneut hochladen. In anderen Fällen werden Warnungen zu Fehlern angezeigt, die Probleme verursachen können, Sie jedoch nicht daran hindern, Ihre Übermittlung fortzusetzen.


## <a name="device-family-availability"></a>Verfügbarkeit von Gerätefamilien

Nachdem die Pakete erfolgreich hochgeladen wurden, wird im Abschnitt **Gerätefamilienverfügbarkeit** eine Tabelle angezeigt, die angibt, welche Pakete für bestimmte Windows10-Gerätefamilien (und ggf. für frühere Betriebssystemversionen) angeboten werden. In diesem Abschnittkönnen Sie auswählen, ob die Übermittlung Kunden mit bestimmten Windows10-Gerätefamilien angeboten werden soll oder nicht.

Weitere Informationen finden Sie unter [Verfügbarkeit von Gerätefamilien](device-family-availability.md).


## <a name="package-details"></a>Paketdetails

Die übertragenen Pakete sind hier aufgeführt, gruppiert nach Ziel-Betriebssystem. Name, Version und Architektur des Pakets werden angezeigt. Klicken Sie auf **Details anzeigen**, um weitere Informationen zu erhalten, z. B. die unterstützten Sprachen, die App-Funktionen oder die Dateigröße der einzelnen Pakete.

Wenn Sie ein Paket aus der Einsendung entfernen müssen, klicken Sie dazu im Abschnitt **Details** des Pakets unten auf den Link **Entfernen**.


## <a name="removing-redundant-packages"></a>Entfernen redundanter Pakete

Wenn wir feststellen, dass mindestens eines Ihrer Pakete redundant ist, wird eine Warnung mit dem Vorschlag angezeigt, die redundanten Pakete aus dieser Übermittlung zu entfernen. Dieser Fehler tritt häufig auf, wenn Sie über zuvor hochgeladene Pakete verfügen und nun Pakete mit einer höheren Versionsnummer bereitstellen, die die gleiche Kundengruppe unterstützen. In diesem Fall würde das redundante Paket keinem Kunde bereitgestellt, weil nun ein besseres Paket (mit einer höheren Versionsnummer) verfügbar ist, um diese Kunden zu unterstützen.

Wenn wir feststellen, dass redundante Pakete vorhanden sind, wird eine Option bereitgestellt, um die redundanten Pakete aus dieser Übermittlung zu entfernen. Sie können die Pakete jedoch auch einzeln aus der Übermittlung entfernen.


## <a name="gradual-package-rollout"></a>Schrittweises Paketrollout

Wenn Ihre Übermittlung ein Update einer bereits veröffentlichte App ist, wird ein Kontrollkästchen mit der Bezeichnung **Update-Rollout schrittweise nach Veröffentlichung dieser Übermittlung (nur für Windows10-Kunden)** angezeigt. Dadurch können Sie den Prozentsatz von Kunden auswählen, die die Pakete aus der Übermittlung erhalten. So können Sie Feedback und Analysedaten beobachten und vor einem umfassenden Rollout sicherstellen, dass das Update verlässlich ist. Sie können den Prozentsatz jederzeit erhöhen (oder das Update stoppen), ohne eine neue Übermittlung zu erstellen. 

Weitere Informationen finden Sie unter [Schrittweises Paketrollout](gradual-package-rollout.md).


## <a name="mandatory-update"></a>Erforderliches Update

Wenn die Übermittlung ein Update für eine bereits veröffentlichte App ist, wird ein Kontrollkästchen mit der Bezeichnung **Dieses Update obligatorisch machen** angezeigt. Damit können Sie Datum und Uhrzeit für ein obligatorisches Update festlegen, vorausgesetzt, Sie haben Ihrer App mithilfe der Windows.Services.Store-APIs erlaubt, programmgesteuert nach Paketupdates zu suchen und die aktualisierten Pakete herunterzuladen und zu installieren. Ihre App kann diese Option nur dann verwenden, wenn sie für Windows10, Version 1607 oder höher, bestimmt ist.

Weitere Informationen finden Sie unter [Herunterladen und Installieren von Paketupdates für Ihre App](../packaging/self-install-package-updates.md).

 



