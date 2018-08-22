---
author: laurenhughes
ms.assetid: ee51eae3-ed55-419e-ad74-6adf1e1fb8b9
title: Manuelles Verpacken von Apps
description: Dieser Abschnitt enthält Artikel oder Links zum manuellen Verpacken von UWP (Universelle Windows-Plattform)-Apps.
ms.author: lahugh
ms.date: 04/30/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows10, UWP, Verpacken
ms.localizationpriority: medium
ms.openlocfilehash: 5f8a9c7f504584f64bb561a01170c965aa9d3983
ms.sourcegitcommit: 91511d2d1dc8ab74b566aaeab3ef2139e7ed4945
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/30/2018
ms.locfileid: "1815825"
---
# <a name="manual-app-packaging"></a>Manuelles Verpacken von Apps

Wenn Sie ein App-Paket erstellen und signieren möchten, für die Entwicklung der App aber nicht Visual Studio verwendet haben, müssen Sie die Tools für die manuelle App-Verpackung verwenden.

> [!IMPORTANT] 
> Wenn Sie Visual Studio zum Entwickeln der App verwendet haben, wird empfohlen, dass Sie den Visual Studio-Assistenten zum Erstellen und Signieren des App-Pakets verwenden. Weitere Informationen finden Sie unter [Verpacken einer UWP-App mit Visual Studio](https://msdn.microsoft.com/windows/uwp/packaging/packaging-uwp-apps).

## <a name="purpose"></a>Zweck

Dieser Abschnitt enthält Artikel oder Links zum manuellen Verpacken von UWP (Universelle Windows-Plattform)-Apps.

| Thema | Beschreibung |
|-------|-------------|
| [Erstellen eines App-Pakets mit dem Tool „MakeAppx.exe“](create-app-package-with-makeappx-tool.md) | MakeAppx.exe erstellt, verschlüsselt, entschlüsselt und extrahiert Dateien aus App-Paketen und -Bündeln. |
| [Erstellen von Zertifikaten für die Paketsignatur](create-certificate-package-signing.md) | Erstellen und Exportieren eines Zertifikats für die App-Paketsignatur mit PowerShell-Tools. |
| [Signieren eines App-Pakets mit SignTool](sign-app-package-using-signtool.md) | Verwenden von SignTool zur manuellen Signatur eines App-Pakets mit einem Zertifikat. |

### <a name="advanced-topics"></a>Fortgeschrittene Themen

Dieser Abschnittenthält fortgeschrittene Themen zum Aufschlüsseln einer großen und/oder komplexen App für eine effizientere Verpackung und Installation. 

> [!IMPORTANT]
> Wenn Sie Ihre App an den Store übermitteln möchten, müssen Sie sich an den [Windows-Support für Entwickler](https://developer.microsoft.com/windows/support) wenden und eine Genehmigung für die Verwendung der erweiterten Funktionen in diesem Abschnitt erhalten.


| Thema | Beschreibung |
|-------|-------------|
| [Einführung zu Bestandspaketen](asset-packages.md) | Asset-Pakete sind ein Pakettyp, der als zentraler Speicherort für die gemeinsamen Dateien einer Anwendung fungiert. Dadurch wird die Notwendigkeit doppelter Dateien in allen Architekturpaketen effektiv eliminiert. |
| [Entwickeln mit Bestandspaketen und Paketfaltung](package-folding.md) | Hier erfahren Sie, wie Sie Ihre App mit Bestandspaketen und Paketfaltung effizient organisieren. |
| [Flat-Bundle App-Pakete](flat-bundles.md) | Beschreibt, wie ein Flat-Bundle erstellt wird, um die .appx-Paketdateien Ihrer App mit Verweisen auf App-Pakete zu bündeln. |
| [Paketerstellung mit dem Verpackungslayout](packaging-layout.md) | Das Verpackungslayout ist ein Dokument, das die Verpackungsstruktur der App beschreibt. Es gibt die Bündel einer App („primär” und „optional”), die Pakete in den Bündeln sowie die Dateien in den Paketen an. |