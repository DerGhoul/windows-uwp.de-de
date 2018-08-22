---
author: Karl-Bridge-Microsoft
Description: This topic describes the new Windows UI for rotation and provides user experience guidelines that should be considered when using this new interaction mechanism in your UWP app.
title: Drehung
ms.assetid: f098bc05-35b3-46b2-9e9b-9ff292d067ca
label: Rotation
template: detail.hbs
ms.author: kbridge
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows10, UWP
ms.localizationpriority: medium
ms.openlocfilehash: 9cc30dbd9fd501d310bb037726414356354af294
ms.sourcegitcommit: 0ab8f6fac53a6811f977ddc24de039c46c9db0ad
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
ms.locfileid: "1653419"
---
# <a name="rotation"></a>Drehung


In diesem Artikel wird die neue Windows-Benutzeroberfläche beschrieben, die Drehungen unterstützt. Außerdem enthält das Thema Richtlinien für die Benutzeroberfläche, die Sie berücksichtigen sollten, wenn Sie diesen neuen Interaktionsmechanismus in einer UWP-App verwenden.

> **Wichtige APIs**: [**Windows.UI.Input**](https://msdn.microsoft.com/library/windows/apps/br242084), [**Windows.UI.Xaml.Input**](https://msdn.microsoft.com/library/windows/apps/br227994)

## <a name="dos-and-donts"></a>Empfohlene und nicht empfohlene Vorgehensweisen

-   Verwenden Sie Drehung, damit Benutzer leichter UI-Elemente direkt drehen können.

## <a name="additional-usage-guidance"></a>Weitere Hinweise zur Verwendung


**Übersicht über Drehung**

Die Drehung ist eine für Touchscreens optimierte Technik, die von UWP-Apps verwendet wird und mit der Benutzer ein Objekt kreisförmig drehen können (im Uhrzeigersinn oder gegen den Uhrzeigersinn).

Abhängig vom Eingabegerät wird für die Drehungsinteraktion Folgendes verwendet:

-   Eine Maus oder ein aktiver Zeichenstift/Eingabestift zum Verschieben des Drehungsziehelements eines ausgewählten Objekts.
-   Berührung oder passiver Zeichen-/Eingabestift zum Drehen des Objekts in die gewünschte Richtung mit der Drehbewegung.

**Gründe für die Verwendung von Drehung**

Verwenden Sie Drehung, damit Benutzer leichter UI-Elemente direkt drehen können. In den folgenden Diagrammen sehen Sie einige der unterstützten Fingerpositionen für die Drehungsinteraktion.

![Diagramm zur Veranschaulichung verschiedener Fingerhaltungen, die für Drehungen unterstützt werden](images/ux-rotate-positions.png)

**Hinweis**  
Intuitiv ist der Drehungspunkt in den meisten Fällen einer der zwei Berührungspunkte, es sei denn, der Benutzer kann einen Drehungspunkt angeben, der in keinem Bezug zu den Kontaktpunkten steht (beispielsweise in einer Zeichen- oder Layoutanwendung). In den folgenden Abbildungen wird gezeigt, wie die Benutzeroberfläche beeinträchtigt werden kann, wenn der Drehungspunkt nicht auf diese Weise eingeschränkt ist.

In der ersten Abbildung sehen Sie den ersten (Daumen) und den zweiten Berührungspunkt (Zeigefinger): Der Zeigefinger berührt einen Baum, und der Daumen berührt einen Holzblock.

![Abbildung mit den zwei anfänglichen Berührungspunkten für die Drehbewegung](images/ux-rotate-points1.png)
In dieser zweiten Abbildung wird die Drehung um den anfänglichen Berührungspunkt (Daumen) ausgeführt. Nach der Drehung berührt immer noch der Zeigefinger den Baumstamm und der Daumen den Holzblock (Drehungspunkt).

![Abbildung mit einem gedrehten Bild, dessen Drehungspunkt durch einen der zwei anfänglichen Berührungspunkte eingeschränkt ist](images/ux-rotate-points2.png)
In dieser dritten Abbildung wurde der Mittelpunkt der Drehung durch die Anwendung als Mittelpunkt des Bilds definiert (oder vom Benutzer entsprechend festgelegt). Da das Bild nicht um einen der Finger gedreht wurde, hat der Benutzer nach der Drehung nicht das Gefühl, direkt etwas geändert zu haben (es sei denn, er hat diese Einstellung ausgewählt).

![Abbildung mit einem gedrehten Bild, dessen Drehungspunkt durch den Mittelpunkt des Bilds anstatt durch die zwei anfänglichen Berührungspunkte eingeschränkt ist](images/ux-rotate-points3.png)
In dieser letzten Abbildung wurde der Mittelpunkt der Drehung durch die Anwendung als Mittelpunkt des Bilds definiert (oder vom Benutzer entsprechend festgelegt). Auch in diesem Fall hat der Benutzer nicht das Gefühl, direkt etwas geändert zu haben (es sei denn, er hat diese Einstellung ausgewählt).

![Abbildung mit einem gedrehten Bild, dessen Drehungspunkt durch den am weitesten links angeordneten Mittelpunkt des Bilds anstatt durch die zwei anfänglichen Berührungspunkte eingeschränkt ist](images/ux-rotate-points4.png)

 

Windows8 unterstützt drei Drehungsarten: frei, eingeschränkt und kombiniert.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Typ</th>
<th align="left">Beschreibung</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Freie Drehung</td>
<td align="left"><p>Mit der freien Drehung können Benutzer Inhalte frei in einem beliebigen Bereich von 360Grad drehen. Wenn der Benutzer das Objekt ablegt, bleibt das Objekt in der ausgewählten Position. Die freie Drehung ist hilfreich in Zeichen- und Layoutanwendungen wie beispielsweise MicrosoftPowerPoint, Word, Visio und Paint sowie Adobe Photoshop, Illustrator und Flash.</p></td>
</tr>
<tr class="even">
<td align="left">Eingeschränkte Drehung</td>
<td align="left"><p>Die eingeschränkte Drehung unterstützt freie Drehung während der Änderung, erzwingt aber beim Loslassen Andockpunkte in 90-Grad-Schritten (0, 90, 180 und 270). Wenn Benutzer das Objekt loslassen, wird es automatisch zum nächsten Andockpunkt gedreht.</p>
<p>Die eingeschränkte Drehung ist die gängigste Drehungsmethode und funktioniert ähnlich wie ein Bildlauf in Inhalten. Dank der Andockpunkte müssen Benutzer nicht präzise arbeiten und können trotzdem ihr Ziel erreichen. Die eingeschränkte Drehung ist hilfreich für Anwendungen wie beispielsweise Webbrowser und Fotoalben.</p></td>
</tr>
<tr class="odd">
<td align="left">Kombinierte Drehung</td>
<td align="left"><p>Die kombinierte Drehung unterstützt freie Drehung mit Zonen (ähnlich wie Führungsschienen unter <a href="guidelines-for-panning.md">Richtlinien für Verschiebung</a>) an jedem der 90-Grad-Andockpunkte, die durch die eingeschränkte Drehung erzwungen werden. Wenn das Objekt außerhalb einer der 90-Grad-Zonen losgelassen wird, bleibt das Objekt in dieser Position. Anderenfalls wird das Objekt automatisch zu einem Andockpunkt gedreht.</p>
<div class="alert">
<strong>Hinweis</strong> Eine Benutzeroberflächen-Führungsschiene ist ein Feature, bei dem ein Bereich um ein Ziel die Bewegung zu einem bestimmten Wert oder einer bestimmten Stelle hin einschränkt, um die Auswahl zu beeinflussen.
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>Verwandte Themen


**Beispiele**
* [Einfaches Eingabebeispiel](http://go.microsoft.com/fwlink/p/?LinkID=620302)
* [Beispiel für Eingabe mit niedriger Latenz](http://go.microsoft.com/fwlink/p/?LinkID=620304)
* [Beispiel für den Benutzerinteraktionsmodus](http://go.microsoft.com/fwlink/p/?LinkID=619894)
* [Beispiel für visuelle Fokuselemente](http://go.microsoft.com/fwlink/p/?LinkID=619895)

**Archivbeispiele**
* [Eingabe: Beispiel für XAML-Benutzereingabeereignisse](http://go.microsoft.com/fwlink/p/?linkid=226855)
* [Eingabe: Beispiel für Gerätefunktionen](http://go.microsoft.com/fwlink/p/?linkid=231530)
* [Eingabe: Beispiel für Fingereingabe-Treffertests](http://go.microsoft.com/fwlink/p/?linkid=231590)
* [Beispiel für XAML-Bildlauf, -Verschiebung und -Zoom](http://go.microsoft.com/fwlink/p/?linkid=251717)
* [Eingabe: vereinfachtes Freihandbeispiel](http://go.microsoft.com/fwlink/p/?linkid=246570)
* [Eingabe: Gesten und Manipulationen mit GestureRecognizer](http://go.microsoft.com/fwlink/p/?LinkId=264995)
* [Eingabe: Beispiel für Manipulationen und Gesten (C++)](http://go.microsoft.com/fwlink/p/?linkid=231605)
* [Beispiel für die DirectX-Fingereingabe](http://go.microsoft.com/fwlink/p/?LinkID=231627)
 

 



