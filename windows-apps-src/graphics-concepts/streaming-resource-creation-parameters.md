---
title: Parameter für das Erstellen von Streamingressourcen
description: Es gibt einige Einschränkungen für den Typ der Direct3D-Ressourcen, die Sie als Streamingressource erstellen können.
ms.assetid: 6FC5AD93-6F47-479E-947C-895C99B427BC
keywords:
- Parameter für das Erstellen von Streamingressourcen
author: michaelfromredmond
ms.author: mithom
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: f2a17f69ae0353bb7682a1dbfa48d5909f48d4aa
ms.sourcegitcommit: 0ab8f6fac53a6811f977ddc24de039c46c9db0ad
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
ms.locfileid: "1652989"
---
# <a name="streaming-resource-creation-parameters"></a>Parameter für das Erstellen von Streamingressourcen


Es gibt einige Einschränkungen für den Typ der Direct3D-Ressourcen, die Sie als Streamingressource erstellen können.

<span id="Supported-Resource-Type"></span><span id="supported-resource-type"></span><span id="SUPPORTED-RESOURCE-TYPE"></span>**Unterstützter Ressourcentyp**  
Texture2D\ [Array\] (einschließlich TextureCube\[Array\], der eine Variante von Texture2D\[Array\]) oder Buffer ist.

**NICHT unterstützt: **Texture1D\[Array\].

<span id="Supported-Resource-Usage"></span><span id="supported-resource-usage"></span><span id="SUPPORTED-RESOURCE-USAGE"></span>**Unterstützte Ressourcenverwendung**  
Standardverwendung.

**NICHT unterstützt: **Dynamisch, Staging oder Unveränderlich.

<span id="Supported-Resource-Misc-Flags"></span><span id="supported-resource-misc-flags"></span><span id="SUPPORTED-RESOURCE-MISC-FLAGS"></span>**Sonstige unterstützte Ressourcen-Flags**  
Unterteilt; d.h. Streaming (gemäß Definition), Texturwürfel, indirekte Argumente zeichnen, Puffer lässt Rohdatenansichten zu, strukturierter Puffer, Ressourcenklammerung oder Mips generieren.

**NICHT unterstützt: **Freigegeben, freigegebenes Schlüsselmutex, GDI-kompatibel, freigegebenes NT-Handle, eingeschränkter Inhalt, eingeschränkte freigegebene Ressource, eingeschränkter freigegebener Ressourcentreiber, geschützt oder Kachelpool.

<span id="Supported-Bind-Flags"></span><span id="supported-bind-flags"></span><span id="SUPPORTED-BIND-FLAGS"></span>**Unterstützte Bindungsflags**  
Als Shaderressource binden, Renderziel, Tiefenschablone oder unsortierter Zugriff.

**NICHT unterstützt: **Als Konstantenpuffer binden, Vertexpuffer (Binden eines geteilten Puffers als SRV/UAV/RTV wird unterstützt), Indexpuffer, Streamausgabe, Decoder oder Video-Encoder.

<span id="Supported-Formats"></span><span id="supported-formats"></span><span id="SUPPORTED-FORMATS"></span>**Unterstützte Formate**  
Alle Formate, die für die gegebene Konfiguration verfügbar sind, unabhängig davon, ob sie eine geteilte Anordnung verwenden, mit einigen Ausnahmen.

<span id="Supported-Sample-Description--Multisample-count--quality-"></span><span id="supported-sample-description--multisample-count--quality-"></span><span id="SUPPORTED-SAMPLE-DESCRIPTION--MULTISAMPLE-COUNT--QUALITY-"></span>**Unterstützte Samplingbeschreibung (Multisampling-Anzahl, Qualität)**  
Alles, was für die gegebene Konfiguration unterstützt wird, unabhängig davon, ob eine geteilte Anordnung verwendet wird, mit einigen Ausnahmen.

<span id="Supported-Width-Height-MipLevels-ArraySize"></span><span id="supported-width-height-miplevels-arraysize"></span><span id="SUPPORTED-WIDTH-HEIGHT-MIPLEVELS-ARRAYSIZE"></span>**Unterstützte Width/Height/MipLevels/ArraySize**  
Im vollen Umfang von Direct3D unterstützt. Streamingressourcen unterliegen nicht der Beschränkung auf die Gesamtspeichergröße wie Nicht-Streamingressourcen. Streamingressourcen werden nur durch die Grenzen des virtuellen Gesamtadressraums beschränkt. Siehe [Zuordnen des verfügbaren Speicherplatzes für Streamingressourcen](address-space-available-for-streaming-resources.md).

Der anfängliche Inhalt des Kachelpoolspeichers ist nicht definiert.

## <a name="span-idin-this-sectionspanin-this-section"></a><span id="in-this-section"></span>Inhalt dieses Abschnitts


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Thema</th>
<th align="left">Beschreibung</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="address-space-available-for-streaming-resources.md">Zuordnen des verfügbaren Speicherplatzes für Streamingressourcen</a></p></td>
<td align="left"><p>In diesem Abschnitt wird der virtuelle Adressraum angegeben, der für Streamingressourcen verfügbar ist.</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>Verwandte Themen


[Erstellen von Streamingressourcen](creating-streaming-resources.md)

 

 



