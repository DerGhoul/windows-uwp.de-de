---
title: Ebenen der Features von Streamingressourcen
description: "Direct3D unterstützt Streamingressourcen in drei Featureebenen."
ms.assetid: 6AE7EA72-3929-4BB4-8780-F0CF26192D87
keywords: Ebenen der Features von Streamingressourcen
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.openlocfilehash: 671c679938860057a5fe8f083eebfe47dc518e05
ms.sourcegitcommit: 909d859a0f11981a8d1beac0da35f779786a6889
translationtype: HT
---
# <a name="streaming-resources-features-tiers"></a>Ebenen der Features von Streamingressourcen


Direct3D unterstützt Streamingressourcen in drei Featureebenen.

Ebene1 stellt grundlegende Funktionen für Streamingressourcen bereit.

Ebene2 fügt über die Ebene1 hinausgehende Funktionen hinzu, z.B. Garantieren eines nicht gepackten Textur-Mipmap, wenn die Größe mindestens eine Standardkachelform beträgt, Shaderanweisungen zur Klammerung der Detailebene (Level-of-Detail, LOD) und zum Abrufen des Status des Shadervorgangs sowie das Lesen aus NULL-zugeordneten Kacheln behandeln, deren Samplingwert null ergab.

Ebene3 fügt über Ebene2 hinausgehende Texture3D-Funktionen hinzu.

In den Versionen von Direct3D sind Abfragefunktionen zum Überprüfen der Hardware und der Treiberunterstützung für Streamingressourcen sowie der Ebene verfügbar.

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
<td align="left"><p>[Ebene1](tier-1.md)</p></td>
<td align="left"><p>In diesem Abschnitt wird die Unterstützung für die Ebene1 beschrieben.</p></td>
</tr>
<tr class="even">
<td align="left"><p>[Ebene2](tier-2.md)</p></td>
<td align="left"><p>Die Unterstützung der Ebene2 für Streamingressourcen fügt über die Ebene1 hinausgehende Funktionen hinzu, z.B. Garantieren eines nicht gepackten Textur-Mipmap, wenn die Größe mindestens eine Standardkachelform beträgt, Shaderanweisungen zur Klammerung der Detailebene (Level-of-Detail, LOD) und zum Abrufen des Status des Shadervorgangs sowie das Lesen aus NULL-zugeordneten Kacheln behandeln, deren Samplingwert null ergab.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[Ebene3](tier-3.md)</p></td>
<td align="left"><p>Ebene3 fügt zusätzlich zu den Funktionen der [Ebene2](tier-2.md) die Unterstützung für Texture3D für Streamingressourcen hinzu.</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>Verwandte Themen


[Streamingressourcen](streaming-resources.md)

 

 



