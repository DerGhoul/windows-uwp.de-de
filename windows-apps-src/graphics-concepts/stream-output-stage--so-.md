---
title: Streamausgabephase (SO)
description: Die Streamausgabephase (Stream Output, SO) gibt (oder streamt) kontinuierlich Vertexdaten aus der vorherigen aktiven Phase an einen oder mehrere Puffer im Speicher aus. In den Arbeitsspeicher gestreamte Daten können als Eingabedaten der Pipeline wieder zugeführt oder von der CPU eingelesen werden.
ms.assetid: DE89E99F-39BC-4B34-B80F-A7D373AA7C0A
keywords:
- Streamausgabephase (SO)
author: michaelfromredmond
ms.author: mithom
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: 30c3ed335360d7b259c045722b65bb08a71b6e0c
ms.sourcegitcommit: 897a111e8fc5d38d483800288ad01c523e924ef4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2018
ms.locfileid: "1044039"
---
# <a name="stream-output-so-stage"></a>Streamausgabephase (SO)


Die Streamausgabephase (Stream Output, SO) gibt (oder streamt) kontinuierlich Vertexdaten aus der vorherigen aktiven Phase an einen oder mehrere Puffer im Speicher aus. In den Arbeitsspeicher gestreamte Daten können als Eingabedaten der Pipeline wieder zugeführt oder von der CPU eingelesen werden.

## <a name="span-idpurposeandusesspanspan-idpurposeandusesspanspan-idpurposeandusesspanpurpose-and-uses"></a><span id="Purpose_and_uses"></span><span id="purpose_and_uses"></span><span id="PURPOSE_AND_USES"></span>Zweck und Verwendung


![Diagramm der Position der Streamausgabephase in der Pipeline](images/d3d10-pipeline-stages-so.png)

Die Streamausgabephase streamt Grundtypdaten auf dem Weg zum Rasterizer aus der Pipeline in den Arbeitsspeicher. Daten aus der vorherigen Phase können in den Arbeitsspeicher gestreamt und/oder in den Rasterizer übergeben werden. In den Arbeitsspeicher gestreamte Daten können als Eingabedaten der Pipeline wieder zugeführt oder von der CPU eingelesen werden.

In den Arbeitsspeicher gestreamte Daten können in einem nachfolgenden Renderingdurchlauf zurück in die Pipeline gelesen oder in eine Stagingressource kopiert werden (damit sie von der CPU gelesen werden können). Die Menge der gestreamten Daten kann variieren. Direct3D behandelt die Daten, ohne dass die GPU abgefragt werden muss, welche Menge an Daten geschrieben wurde.&gt;

Es gibt zwei Möglichkeiten, die Streamausgabedaten in die Pipeline zu stellen:

-   Streamausgabedaten können der Eingabeassemblerphase (IA) wieder zugeführt werden.
-   Streamausgabedaten können von programmierbaren Shadern mit [Load](https://msdn.microsoft.com/library/windows/desktop/bb509694)-Funktionen gelesen werden.

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>Eingabe


Vertexdaten aus einer vorherigen Shaderphase.

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>Ausgabe


Die Streamausgabephase (SO) gibt (oder streamt) kontinuierlich Vertexdaten aus der vorherigen aktiven Phase, z.B. der Geometry-Shaderphase (GS), in einen oder mehrere Puffer im Arbeitsspeicher aus. Wenn die Geometry-Shaderphase (GS) inaktiv ist, gibt die Streamausgabephase (SO) kontinuierlich Vertexdaten aus der Domänen-Shaderphase (DS) an Puffer im Arbeitsspeicher aus (oder wenn DS auch inaktiv ist, aus der Vertex-Shaderphase (VS)).

Wenn ein Streifen Dreieck oder in der Zeile in die Phase Eingabe Assembler (IA) gebunden ist, wird jede Streifen in eine Liste konvertiert, bevor sie out gestreamt werden. Scheitelpunkte werden immer als vollständige Primitives (beispielsweise 3 Scheitelpunkte zu einem Zeitpunkt für Dreiecke); ausgegeben. Unvollständige Primitives werden nie out gestreamt. Grundtypen mit Nähe die Nähe Daten vor streaming von Daten zu löschen.

Die Streamausgabephase unterstützt gleichzeitig bis zu 4Puffer.

-   Wenn Sie Daten in mehrere Puffer streamen, kann jeder Puffer nur ein einzelnes Element (bis zu 4Komponenten) pro Vertexdaten erfassen, mit einem impliziten Datenversatz, der der Elementbreite im jedem Puffer entspricht (kompatibel mit der Art, wie einzelne Elementpuffer für die Eingabe in Shaderphasen gebunden werden können). Wenn Puffer unterschiedliche Größen haben, wird darüber hinaus der Schreibvorgang angehalten, sobald einer der Puffer voll ist.
-   Wenn Sie Daten in einen einzelnen Puffer streamen, kann der Puffer bis zu 64skalare Komponenten pro Vertexdaten erfassen (256Byte oder weniger) oder der Vertexversatz kann bis zu 2048Byte betragen.

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>Verwandte Themen


[Grafikpipeline](graphics-pipeline.md)

 

 



