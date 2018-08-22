---
title: Von den Streamingressourcen nicht unterstützte Schablonenformate
description: Formate, die Schablonen enthalten, werden von Streamingressourcen nicht unterstützt.
ms.assetid: 90A572A4-3C76-4795-BAE9-FCC72B5F07AD
keywords:
- Von den Streamingressourcen nicht unterstützte Schablonenformate
author: michaelfromredmond
ms.author: mithom
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
ms.localizationpriority: medium
ms.openlocfilehash: 330b768c0f00f36ce8ce539b9ce41c7ac812e6fc
ms.sourcegitcommit: 897a111e8fc5d38d483800288ad01c523e924ef4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2018
ms.locfileid: "1043229"
---
# <a name="stencil-formats-not-supported-with-streaming-resources"></a>Von den Streamingressourcen nicht unterstützte Schablonenformate


Formate, die Schablonen enthalten, werden von Streamingressourcen nicht unterstützt.

Zu den Formaten, die Schablonen enthalten, gehören DXGI\_FORMAT\_D24\_UNORM\_S8\_UINT (sowie zugehörige Formate in der R24G8-Familie) und DXGI\_FORMAT\_D32\_FLOAT\_S8X24\_UINT (sowie zugehörige Formate in der R32G8X24-Familie).

Einige Implementierungen speichern Tiefen- und Schabloneninformationen in separaten Zuordnungen, andere speichern sie zusammen. Die Kachelverwaltung für die beiden Schemas müsste unterschiedlich sein, und keine API kann die Unterschiede abstrahieren oder rationalisieren. Wir empfehlen für zukünftige Hardware die Unterstützung unabhängiger Tiefen- und Schablonenoberflächen, die voneinander unabhängige Kacheln verwenden.

Die 32-Bit-Tiefe müsste 128x128Kacheln und die 8-BitSchablone müsste 256x256 Kacheln haben. Daher würde es Anwendungen mit einer Diskrepanz in der Kachelform zwischen Tiefe und Schablone geben. Aber das gleiche Problem besteht bereits bei anderen Formaten von Renderzieloberflächen.

## <a name="span-idrelated-topicsspanrelated-topics"></a><span id="related-topics"></span>Verwandte Themen


[Geräte- und prozessübergreifende Streamingressourcen](streaming-resource-cross-process-and-device-sharing.md)

 

 



