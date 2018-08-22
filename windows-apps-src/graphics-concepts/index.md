---
title: Direct3D-Grafikkonzepte
description: Beschreibt das Grafikkonzept, auf dem Microsoft Direct3D aufgebaut ist.
ms.assetid: c3850a92-4d05-4f72-bf0f-6a0c79e841eb
keywords:
- Direct3D-Grafik – Lernanleitung
author: michaelfromredmond
ms.author: mithom
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: 3e1fed9eaf3003bc67a86a5282fccbb923019a36
ms.sourcegitcommit: 0ab8f6fac53a6811f977ddc24de039c46c9db0ad
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
ms.locfileid: "1653019"
---
# <a name="direct3d-graphics-concepts"></a>Direct3D-Grafikkonzepte


Beschreibt Microsoft Direct3D-Grafikkonzepte. Dieses Handbuch erklärt die allgemeinen Direct3D-Computer-Grafikkonzepte, die in der Direct3D-Spiele- und App-Entwicklung verwendet werden.

## <a name="span-idin-this-sectionspanin-this-section"></a><span id="in-this-section"></span>In diesem Abschnitt


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
<td align="left"><p><a href="coordinate-systems-and-geometry.md">Koordinatensystem und Geometrie</a></p></td>
<td align="left"><p>Für das Programmieren von Direct3D-Anwendungen muss der Anwender mit geometrischen 3D-Prinzipien vertraut sein. Dieser Abschnitt stellt die wichtigsten geometrischen Konzepte zum Erstellen von 3D-Szenen vor.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="vertex-and-index-buffers.md">Vertex- und Indexpuffer</a></p></td>
<td align="left"><p><em>Scheitelpunktpuffer</em> sind Speicherpuffer, die Scheitelpunktdaten enthalten. Scheitelpunkte in einem Scheitelpunktpuffer werden verarbeitet, um Transformation, Beleuchtung und Zuschneiden auszuführen. <em>Indexpuffer</em> sind Speicherpuffer mit Indexdaten, die Ganzzahl-Offsets in Vertexpuffer darstellen, und zum Rendern von Grundtypen verwendet werden.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="devices.md">Geräte</a></p></td>
<td align="left"><p>Ein Direct3D-Gerät ist die Komponente zum Rendern von Direct3D. Ein Gerät kapselt und speichert den Renderstatus, führt Transformationen und Beleuchtungsvorgänge aus, und rastert ein Bild zu einer Oberfläche.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="lights-and-materials.md">Beleuchtung</a></p></td>
<td align="left"><p>Lichter werden verwendet, um Objekte in einer Szene zu beleuchten. Die Farbe jedes Objektscheitelpunkts basiert auf der aktuellen Texturzuordnung, Scheitelpunktfarben und Lichtquellen.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="depth-and-stencil-buffers.md">Tiefen- und Schablonenpuffer</a></p></td>
<td align="left"><p>Ein <em>Tiefenpuffer</em> speichert Tiefeninformationen. Diese steuern, welche Bereiche von Polygonen dargestellt werden. Ein <em>Schablonenpuffer</em> wird Maskieren von Pixeln in einem Bild verwendet. So können Spezialeffekte erstellt werden (z. B. Stanzeffekte; Decaling; Transparenzen, Ausblenden und Verwischen; Außenlinien und Silhouetten und zweiseitige Schablonen).</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="textures.md">Texturen</a></p></td>
<td align="left"><p>Texturen sind ein leistungsstarkes Tool, um mit dem Computer realistische 3D-Bilder zu erzeugen. Direct3D unterstützt einen umfangreichen Texturfunktionssatz, und ermöglicht Entwicklern einfach auf erweiterte Texturtechniken zuzugreifen.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="graphics-pipeline.md">Grafik-Pipeline</a></p></td>
<td align="left"><p>Die Direct3D-Grafikpipeline dient zum Generieren von Grafiken für Echtzeitspiele. Datenflüsse vom Eingang zum Ausgang durch jede konfigurierbare oder programmierbare Phase</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="views.md">Ansichten</a></p></td>
<td align="left"><p>Der Begriff &quot;Ansicht&quot; wird für &quot;Daten im erforderlichen Format&quot; verwendet. Eine Konstantenpufferansicht (CBV) beispielweise, sind ordnungsgemäß formatierte, konstante Pufferdaten. Dieser Abschnitt beschreibt die gängigsten und hilfreichsten Ansichten.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="compute-pipeline.md">Berechnungs-Pipeline</a></p></td>
<td align="left"><p>Die Direct3D-Berechnungs-Pipeline wurde entwickelt, um Berechnungen zu erledigen, die meist parallel mit der Grafik-Pipeline ausgeführt werden können.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="resources.md">Ressourcen</a></p></td>
<td align="left"><p>Eine Ressource ist ein Bereich im Speicher, auf den die Direct3D-Pipeline zugreifen kann. Damit die Pipeline effizient auf den Speicher zugreifen kann, müssen für die Pipeline bereitgestellte Daten (wie z.B. Input-Geometrie, Shader-Ressourcen und Texturen) in einer Ressource gespeichert werden. Es gibt zwei Arten von Ressourcen, aus denen alle Direct3D-Ressourcen abgeleitet sind: ein Puffer oder eine Textur. Bis zu 128 Ressourcen können für jede Pipeline-Phase aktiv sein.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="streaming-resources.md">Streaming-Ressourcen</a></p></td>
<td align="left"><p><em>Streamingressourcen</em> sind große logische Ressourcen, die wenig physischen Speicher belegen.. Anstatt die gesamte große Ressource zu übergeben, werden nur kleine Teile der Ressource bei Bedarf gestreamt. Streaming-Ressourcen wurden vorher als <em>unterteilte Ressourcen</em> bezeichnet.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="appendix.md">Anhänge</a></p></td>
<td align="left"><p>Diese Abschnitte enthalten tiefergehende technische Details.</p></td>
</tr>
</tbody>
</table>

 

 

 