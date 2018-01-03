---
title: Konfliktnachverfolgung und Tile-Pool-Ressourcen
description: "Für Nicht-Streamingressourcen kann Direct3D bestimmte Konflikte (Hazards) während des Renderns verhindern. Für Streamingressourcen müsste die Nachverfolgung von Konflikten jedoch auf Tile-Ebene erfolgen, was zu aufwändig wäre."
ms.assetid: 8B0C73D3-3F77-41E8-B17D-C595DEE39E49
keywords: Konfliktnachverfolgung und Tile-Pool-Ressourcen
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.openlocfilehash: 2bdec458e13e3f2df54555716d59aefcc946ef7b
ms.sourcegitcommit: 909d859a0f11981a8d1beac0da35f779786a6889
translationtype: HT
---
# <a name="hazard-tracking-versus-tile-pool-resources"></a>Konfliktnachverfolgung und Tile-Pool-Ressourcen


Für Nicht-Streamingressourcen kann Direct3D bestimmte Konflikte (Hazards) während des Renderns verhindern. Für Streamingressourcen müsste die Nachverfolgung von Konflikten jedoch auf Tile-Ebene erfolgen, was zu aufwändig wäre.

Beispielsweise erlaubt die Runtime für Nicht-Streamingressourcen nicht, dass eine Unterressource gleichzeitig als Eingabe (z.B. als Shaderressourcenansicht) und als Ausgabe (z.B. als Renderzielansicht) gebunden wird. In einem solchen Fall würde die Runtime die Bindung der Eingabe aufheben. Dieser Nachverfolgungsaufwand in der Runtime ist gering und erfolgt auf der Ebene von Unterressourcen. Einer der Vorteile dieses durch die Nachverfolgung bedingten Mehraufwands ist die Minimierung der Wahrscheinlichkeit, dass Apps versehentlich von der Ausführungsreihenfolge der Hardwareshader abhängig sind. Die Ausführungsreihenfolge der Hardwareshader kann variieren – wenn nicht für eine bestimmte GPU (Graphics Processing Unit), so doch bestimmt für verschiedene GPUs.

Nachzuverfolgen, wie Ressourcen gebunden sind, kann für Streamingressourcen zu aufwändig sein, da die Überwachung auf Tile-Ebene erfolgt. Und es können weitere Probleme auftreten. Möglichweise müssen Versuche unterbunden werden, in eine Render Target View zu rendern, wenn eine Tile gleichzeitig mehreren Bereichen der Oberfläche zugeordnet ist. Wenn diese Konfliktnachverfolgung pro Tile für die Runtime zu aufwändig ist, wäre das eine Option für die Debug-Ebene.

Eine Anwendung, die mit einem Schreib-oder Lesevorgang auf eine Streamingressource zugreift, die den Tile-Pool-Speicher referenziert, der auch von anderen Streamingressourcen in anschließenden Schreib- oder Lesevorgängen referenziert wird, muss den Grafiktreiber darüber informieren, dass sie erwartet, den ersten Vorgang abschließen zu können, bevor die folgenden Vorgänge beginnen.

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>Verwandte Themen


[Zuordnungen in einem Tile-Pool](mappings-are-into-a-tile-pool.md)

 

 



