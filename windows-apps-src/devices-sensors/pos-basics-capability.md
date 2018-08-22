---
author: TerryWarwick
title: PointOfService-Gerätefunktion
description: Die PointOfService-Gerätefunktion wird für die Verwendung des Windows.Devices.PointOfService-Namespace benötigt.
ms.author: jken
ms.date: 05/1/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, UWP, Point Of Service, POS
ms.localizationpriority: medium
ms.openlocfilehash: 564c7686cef4815e9ca1bfd0af82c4577852b8a4
ms.sourcegitcommit: 633dd07c3a9a4d1c2421b43c612774c760b4ee58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2018
ms.locfileid: "1976737"
---
# <a name="pointofservice-device-capability"></a>PointOfService-Gerätefunktion
Sie fordern Zugriff auf die PointOfService-APIs an, indem Sie die Funktion in Ihrem Anwendungspaketmanifest deklarieren. Sie können die meisten Funktionen mithilfe des Manifest-Designers in Microsoft Visual Studio deklarieren, oder Sie können sie manuell hinzufügen.  

> [!Important]
> Sie erhalten die Fehlermeldung **System.UnauthorizedAccessException**, wenn Sie versuchen, eine API im Namespace Windows.Devices.PointOfService zu verwenden, wenn Sie keine **pointOfService**-Funktion in Ihrem Anwendungsmanifest deklarieren. 

## <a name="declare-capability-using-manifest-designer"></a>Deklarieren von Funktionen mithilfe des Manifest-Designers

1. Erweitern Sie im **Projektmappen-Explorer** den Projektknoten Ihrer UWP-Anwendung.
2. Doppelklicken Sie auf die Datei **Package.appxmanifest**.  
*Wenn die Manifestdatei bereits in der XML-Codeansicht geöffnet ist, werden Sie von Visual Studio zum Schließen der Datei aufgefordert.*
3. Öffnen Sie die Registerkarte **Funktionen**.
4. Klicken Sie auf das Kontrollkästchen neben **Point of Service** in der Liste der Funktionen, um die Funktionalität des Point-of-Service-Geräts zu aktivieren.


## <a name="declare-capability-manually"></a>Manuelles Deklarieren eines Funktion

1. Erweitern Sie im **Projektmappen-Explorer** den Projektknoten Ihrer UWP-Anwendung.
2. Klicken Sie mit der rechten Maustaste auf die Datei **Package.appxmanifest**, und wählen Sie die Option **Code anzeigen** aus.
3. Fügen Sie das PointOfService DeviceCapability-Element zum Abschnitt mit den Funktionen Ihres Anwendungsmanifests hinzu.  

```xml
  <Capabilities>
    <DeviceCapability Name="pointOfService" />
  </Capabilities>
   ```