---
title: Einfarbige Lichtzuordnungen
description: Die einfarbige Lichtzuordnung ermöglicht älteren Adaptern das Ausführen der Vermischung von mehrlagigen Texturen, wenn eine ältere 3D-Beschleunigungsplatine die Texturvermischung mit dem Alphawert des Zielpixels nicht unterstützt.
ms.assetid: 60F8F8F6-9DB7-452B-8DC0-407FFAA4BFE1
keywords:
- Einfarbige Lichtzuordnungen
author: michaelfromredmond
ms.author: mithom
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: 67029443f59d87c7f3e38560595dca1b7b399632
ms.sourcegitcommit: 897a111e8fc5d38d483800288ad01c523e924ef4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2018
ms.locfileid: "1043319"
---
# <a name="monochrome-light-maps"></a>Einfarbige Lichtzuordnungen


Die einfarbige Lichtzuordnung ermöglicht älteren Adaptern das Ausführen der Vermischung von mehrlagigen Texturen, wenn eine ältere 3D-Beschleunigungsplatine die Texturvermischung mit dem Alphawert des Zielpixels nicht unterstützt.

Einige ältere 3D-Beschleunigungsplatinen unterstützen die Texturvermischung mit dem Alphawert des Zielpixels nicht. Diese Adapter unterstützen in der Regel auch nicht mehrere Texturvermischungen. Wenn Ihre Anwendung auf einen Adapter wie diesem läuft, kann sie die Vermischung mehrlagiger Texturen verwenden, um eine einfarbige Lichtzuordnung vorzunehmen.

Für eine einfarbige Lichtzuordnung speichert eine Anwendung die Beleuchtungsinformationen in die Alphadaten ihrer Lichtzuordnungstexturen. Die Anwendung verwendet die Texturfilterfunktionen von Direct3D, um jedes Pixel im Bild jeder Primitiven einem entsprechenden Texel in der Lichtzuordnung zuzuordnen. Sie setzt den Ursprungsvermischungsfaktor auf den Alphawert des entsprechenden Texels.

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>Verwandte Themen


[Lichtzuordnung mit Texturen](light-mapping-with-textures.md)

 

 



