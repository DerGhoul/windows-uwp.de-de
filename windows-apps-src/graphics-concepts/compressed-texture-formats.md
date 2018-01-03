---
title: Komprimierte Texturformate
description: "Dieser Abschnitt enthält Informationen über die interne Organisation komprimierter Texturformate."
ms.assetid: 24D17B9F-8CA7-4006-9E0F-178C6B3CAEC9
keywords: Komprimierte Texturformate
author: PeterTurcan
ms.author: pettur
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.openlocfilehash: 1bf94307093913c3b89b1d2a80e1e77d8dec81eb
ms.sourcegitcommit: 909d859a0f11981a8d1beac0da35f779786a6889
translationtype: HT
---
# <a name="compressed-texture-formats"></a>Komprimierte Texturformate


Dieser Abschnitt enthält Informationen über die interne Organisation komprimierter Texturformate. Diese Informationen sind nicht zur Verwendung von komprimierten Texturen notwendig, da Sie die Direct3D-Funktionen für eine Konvertierung in und von komprimierten Formate verwenden können. Sie sind jedoch hilfreich, wenn Sie direkt auf komprimierten Oberflächendaten arbeiten möchten.

Direct3D verwendet ein Komprimierungsformat, das Texturabbildungen in 4x4-Texel-Blöcke unterteilt. Wenn die Textur keine Transparenz enthält - wenn sie undurchsichtig ist - oder die Transparenz von einem 1-Bit-Alpha angegeben wird, stellt ein 8-Byte-Block den Texturabbildungsblock dar. Enthält die Texturabbildung transparente Texel, stellt ein 16-Byte-Block mittels eines Alpha-Kanals den Block dar.

Jede einzelne Textur muss angeben, dass die Daten als 64 oder 128Bit pro Gruppe von 16Texeln gespeichert werden. Wenn 64-Bit-Blöcke - im BC1-Format – für die Textur verwendet werden, ist es möglich, undurchsichtige und 1-Bit-Alpha-Kanal-Formate auf einer pro-Block-Basis innerhalb der gleichen Textur zu kombinieren. Der Vergleich der Größe der Ganzzahl ohne Vorzeichen für die Farbe\_0 und Farbe\_1 wird eindeutig für jeden Block mit 16 Texeln ausgeführt.

Wenn 128-Bit-Blöcke verwendet werden, muss der Alphakanal entweder im expliziten ( BC2-Format) oder interpolierten Modus (BC3-Format) für die gesamte Textur angegeben werden. Was die Farbe anbetrifft, können beim aktiven interpolierten Modus entweder acht interpolierte Alphamodi oder sechs interpolierte Alphamodi auf einer nach Blöcken gestaffelten Basis verwendet werden. Bei einem Größenvergleich von alpha\_0 und alpha\_1 wird ein einzig nach Blöcken gestaffelter Größenvergleich ausgeführt.

Der Neigungswinkel für BCn-Formate wird in Bytes (nicht Blöcken) gemessen. Wenn beispielsweise eine Breite von 16 vorliegt, haben Sie einen Neigungswinkel von vier Blöcken (4\*8 für BC1, 4\*16 für BC2 oder BC3).

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>Verwandte Themen


[Komprimierte Texturressourcen](compressed-texture-resources.md)

 

 



