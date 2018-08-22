---
author: mijacobs
description: Erfahren Sie, wie Sie die Typografie in Ihrer App verwenden, um Benutzern Inhalte leicht verständlich zu machen.
title: Typografie in UWP-Apps
ms.author: mijacobs
ms.date: 04/06/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 505167775b61908be7f47068dbf3221c293f6112
ms.sourcegitcommit: 517c83baffd344d4c705bc644d7c6d2b1a4c7e1a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2018
ms.locfileid: "1843370"
---
# <a name="typography"></a>Typografie

![Favoritenbild](images/header-typography.svg)

Typografie muss übersichtlich sein, da sie zur visuellen Darstellung von Sprache dient, um Informationen zu kommunizieren. Ihr Stil darf diesem Ziel nie im Wege stehen. In diesem Artikel erläutern wir, wie Sie die Typografie in Ihre UWP-App formatieren, damit Benutzer Inhalte schnell und effizient verstehen.

## <a name="font"></a>Font

Verwenden Sie eine Schriftart in der gesamten Benutzeroberfläche Ihrer App. Es wird empfohlen, wenn möglich, die Standardschriftart für UWP-Apps **Segoe UI** zu verwenden. Sie wurde entwickelt, um eine optimale Lesbarkeit für Größe und Pixeldichte zu wahren und bietet eine klare, ansprechende und offene Ästhetik, die den Inhalt des Systems ergänzt.

![Beispieltext für die Schriftart „SegoeUI“](images/type/segoe-sample.svg)

Weitere Informationen zum Anzeigen anderer Sprachen als Englisch oder um eine andere Schriftart für Ihre App auszuwählen finden Sie unter [Sprachen](#Languages) und [Schriftarten](#Fonts) für unsere empfohlenen Schriftarten für UWP-Apps.

:::row::: :::column::: ![Ja](images/do.svg) Wählen Sie eine Schriftart für Ihre Benutzeroberfläche aus.
:::column-end::: :::column::: ![Nein](images/dont.svg) Mischen Sie nicht mehrere Schriftarten.
:::column-end::: :::row-end:::

## <a name="size-and-scaling"></a>Größe und Skalierung

Schriftgrade in UWP-Apps werden automatisch auf allen Geräten skaliert. Mit dem Skalierungsalgorithmus wird sichergestellt, dass der Schriftgrad 24 Pixel auf einem 3 Meter entfernten Surface Hub genauso lesbar ist wie der Schriftgrad 24 Pixel auf einem 5-Zoll-Smartphone, das nur einige Zentimeter entfernt ist.

![Sichtabstände für verschiedene Geräte](images/type/scaling-chart.svg)

Aufgrund der Funktionsweise der Skalierung, entwerfen Sie in effektiven Pixeln, nicht in den tatsächlichen physischen Pixeln, und Sie müssen den Schriftgrad für unterschiedliche Bildschirmgrößen und Auflösungen nicht ändern.

::: Zeile:::::: Spalte::: ![Ja](images/do.svg) Folgen Sie der UWP-[Typhierarchie](#type-ramp)-Größe.
::: Spalte End:::::: Spalte::: ![Nein](images/dont.svg) Verwenden Sie einen Schriftgrad, der kleiner als 12 Pixel ist.
:::column-end::: :::row-end:::

## <a name="hierarchy"></a>Hierarchie

:::row::: :::column::: Benutzer verlassen Sie sich auf die visuelle Hierarchie beim Scannen eines Seitenabschnitts: Header fassen Inhalte zusammen und Textkörper enthalten weitere Details. Um eine klare visuelle Hierarchie in Ihrer App zu erstellen, folgen Sie der UWP-Typhierarchie.
:::column-end::: :::column::: ![Textblock-Stile](images/type/type-hierarchy.svg) :::column-end::: :::row-end:::

### <a name="type-ramp"></a>Typhierarchie

Die UWP-Typhierarchie stellt wichtige Beziehungen zwischen den Schriftschnitte auf einer Seite her, damit der Benutzer den Inhalt einfach lesen kann. Alle Größen werden in effektiven Pixeln angegeben und sind für UWP-Apps optimiert, die auf allen Geräten ausgeführt werden.

![Typhierarchie](images/type/type-ramp.svg)

### <a name="using-the-type-ramp"></a>Die Typhierarchie verwenden

:::row::: :::column::: Sie können Ebenen der Typhierarchie als [statische Ressourcen](../controls-and-patterns/xaml-theme-resources.md#the-xaml-type-ramp) für XAML erreichen. Stile folgen der `*TextBlockStyle` Namenskonvention
:::column-end::: :::column::: ![Textblock-Stile](images/type/text-block-type-ramp.svg) :::column-end::: :::row-end:::

```XAML
<TextBlock Text="Header" Style="{StaticResource HeaderTextBlockStyle}"/>
<TextBlock Text="SubHeader" Style="{StaticResource SubheaderTextBlockStyle}"/>
<TextBlock Text="Title" Style="{StaticResource TitleTextBlockStyle}"/>
<TextBlock Text="SubTitle" Style="{StaticResource SubtitleTextBlockStyle}"/>
<TextBlock Text="Base" Style="{StaticResource BaseTextBlockStyle}"/>
<TextBlock Text="Body" Style="{StaticResource BodyTextBlockStyle}"/>
<TextBlock Text="Caption" Style="{StaticResource CaptionTextBlockStyle}"/>
```

:::row::: :::column::: ![Ja](images/do.svg) Verwenden Sie den "Inhalt" für den meisten Text.

        Use "Base" for titles when space is constrained.
    :::column-end:::
    :::column:::
        ![don't](images/dont.svg)
        Use "Caption" for primary action or any long strings.

        Use "Header" or "Subheader" if text needs to wrap.
    :::column-end:::
:::row-end:::

## <a name="alignment"></a>Ausrichtung

Standardmäßig ist das [TextAlignment](https://docs.microsoft.com/uwp/api/windows.ui.xaml.textalignment) links. In den meisten Fällen sorgt das Konzept „links bündig, rechts mit Flatterrand“ für eine konsistente Verankerung des Inhalts und für ein einheitliches Layout. Weitere Informationen für RTL-Sprachen finden Sie unter [Anpassen von Layout und Schriftarten zur Globalisierungsunterstützung](../globalizing/adjust-layout-and-fonts--and-support-rtl.md).

![Zeigt linksbündigen Text.](images/type/alignment.svg)

```xaml
<TextBlock TextAlignment="Left">
```

## <a name="character-count"></a>Zeichenanzahl

:::row::: :::column::: ![Ja](images/do.svg) Bleiben Sie bei 50 bis 60 Wörtern pro Zeile zur besseren Lesbarkeit.
:::column-end::: :::column::: ![Nein](images/dont.svg) Weniger als 20 Zeichen oder mehr als 60 Zeichen pro Zeile lassen sich schwer lesen.
:::column-end::: :::row-end:::

## <a name="clipping-and-ellipses"></a>Beschnitt und Ellipsen

Wenn die Textmenge den verfügbaren Speicherplatz überschreitet, wird empfohlen, den Text zuzuschneiden, was das Standardverhalten der meisten [UWP-Textsteuerelemente](../controls-and-patterns/text-controls.md)ist.

![Gerät mit abgeschnittenem Text](images/type/clipping.svg)

```xaml
<TextBlock TextWrapping="WrapWholeWords" TextTrimming="Clip"/>
```

:::row::: :::column::: ![Ja](images/do.svg) Text zuschneiden und umbrechen, wenn mehrere Zeilen vorhanden sind.
:::column-end::: :::column::: ![Nein](images/dont.svg) Verwenden Sie Ellipsen für mehr Übersichtlichkeit.
:::column-end::: :::row-end:::

**Hinweis**: Bei Containern, die nicht klar definiert sind (also sich etwa nicht durch eine andere Hintergrundfarbe abheben) oder wenn ein Link zu mehr Text existiert, kann eine Ellipse verwendet werden.

## <a name="languages"></a>Sprachen 

Segoe UI ist unsere Schriftart für Englisch, für europäische Sprachen, Griechisch, Hebräisch, Armenisch, Georgisch und Arabisch. Lesen Sie die folgenden Empfehlungen für andere Sprachen.

### <a name="globalizinglocalizing-fonts"></a>Globalisierung/Lokalisierung von Schriftarten

Verwenden Sie die [LanguageFont-Schriftartenersetzungs-APIs](https://docs.microsoft.com/uwp/api/Windows.Globalization.Fonts.LanguageFont) für den programmgesteuerten Zugriff auf die Empfohlenen Einstellungen für Familie, Grad, Breite und Schnitt der Schriftart für eine spezielle Sprache. Das LanguageFont-Objekt ermöglicht den Zugriff auf die richtigen Schriftartinformationen für verschiedene Inhaltskategorien: UI-Kopfzeilen, Benachrichtigungen, Textkörper und Schriftarten für den Textkörper, die vom Benutzer bearbeitet werden können. Weitere Informationen finden Sie unter [Anpassen von Layout und Schriftarten zur Globalisierungsunterstützung](../globalizing/adjust-layout-and-fonts--and-support-rtl.md).

### <a name="fonts-for-non-latin-languages"></a>Schriftarten für nicht lateinische Sprachen

<table>
<thead>
<tr class="header">
<th align="left">Schriftfamilie</th>
<th align="left">Stile</th>
<th align="left">Hinweise</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="font-family: Embrima;">Ebrima</td>
<td align="left">Normal, fett</td>
<td align="left">Benutzeroberflächen-Schriftart für afrikanische Schriften (Äthiopisch, N'Ko, Osmanya, Tifinagh, Vai).</td>
</tr>
<tr class="even">
<td style="font-family: Gadugi;">Gadugi</td>
<td align="left">Normal, fett</td>
<td align="left">Benutzeroberflächen-Schriftart für nordamerikanische Schriften (Kanadische Silbenschrift, Cherokee).</td>
</tr>
<tr class="odd">
<td align="left" style="font-family: Leelawadee UI;">LeelawadeeUI</td>
<td align="left">Normal, Semilight, fett</td>
<td align="left">Benutzeroberflächen-Schriftart für südostasiatische Schriften (Buginesisch, Laotisch, Khmer, Thailändisch).</td>
</tr>
<tr class="odd">
<td align="left" style="font-family: Malgun Gothic;">Malgun Gothic</td>
<td align="left">Regular</td>
<td align="left">Benutzeroberflächen-Schriftart für Koreanisch.</td>
</tr>
<tr class="even">
<td align="left" style="font-family: Microsoft JhengHei UI;">Microsoft JhengHei UI</td>
<td align="left">Normal, fett, Light</td>
<td align="left">Benutzeroberflächen-Schriftart für Chinesisch (traditionell).</td>
</tr>
<tr class="odd">
<td align="left" style="font-family: Microsoft YaHei UI;">Microsoft YaHei UI</td>
<td align="left">Normal, fett, Light</td>
<td align="left">Benutzeroberflächen-Schriftart für Chinesisch (vereinfacht).</td>
</tr>
<tr class="odd">
<td align="left" style="font-family: Myanmar Text;">Myanmar Text</td>
<td align="left">Regular</td>
<td align="left">Fallbackschriftart für die Myanmar-Schrift.</td>
</tr>
<tr class="even">
<td align="left" style="font-family: Nirmala UI;">Nirmala UI</td>
<td align="left">Normal, Semilight, fett</td>
<td align="left">Benutzeroberflächen-Schriftart für südasiatische Schriften (Bangla, Devanagari, Gujarati, Gurmukhi, Kannada, Malayalam, Odia, Ol Chiki, Singhalesisch, Sora Sompeng, Tamil, Telugu)</td>
</tr>
<tr class="odd">
<td align="left" style="font-family: SimSun;">SimSun</td>
<td align="left">Regular</td>
<td align="left">Eine ältere chinesische UI-Schriftart. </td>
</tr>
<tr class="even">
<td align="left" style="font-family: Yu Gothic UI;">Yu Gothic UI</td>
<td align="left">Light, Semilight, normal, Semibold, fett</td>
<td align="left">Benutzeroberflächen-Schriftart für Japanisch.</td>
</tr>
</tbody>
</table>

## <a name="fonts"></a>Schriftarten

### <a name="sans-serif-fonts"></a>Serifenlose Schriftarten

Serifenlose Schriftarten eignen sich für Überschriften und UI-Elemente. 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Schriftfamilie</th>
<th align="left">Stile</th>
<th align="left">Hinweise</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left" style="font-family: Arial;">Arial</td>
<td align="left">Normal, kursiv, fett, fett kursiv, schwarz</td>
<td align="left">Unterstützung für europäische und nahöstliche Schriften (Lateinisch, Griechisch, Kyrillisch, Arabisch, Armenisch und Hebräisch). Die Schriftbreite „Black“ unterstützt nur europäische Schriften.</td>
</tr>
<tr class="even">
<td align="left" style="font-family: Calibri;">Calibri</td>
<td align="left">Normal, kursiv, fett, fett kursiv, dünn, dünn kursiv</td>
<td align="left">Unterstützung für europäische und nahöstliche Schriften (Lateinisch, Griechisch, Kyrillisch, Arabisch und Hebräisch). Arabisch nur in gerader Schrift verfügbar.</td>
</tr>
<td style="font-family: Consolas;">Consolas</td>
<td>Normal, kursiv, fett, fett kursiv</td>
<td>Schriftart mit fester Breite mit Unterstützung für europäische Schriften (Lateinisch, Griechisch und Kyrillisch).</td>
</tr>

<tr>
<td style="font-family: Segoe UI;">Segoe UI</td>
<td>Normal, kursiv, Light kursiv, Black kursiv, fett, fett kursiv, Light, Semilight, Semibold, Black</td>
<td>Benutzeroberflächen-Schriftart für europäische und nahöstliche Schriften (Arabisch, Armenisch, Kyrillisch, Georgisch, Griechisch, Hebräisch, Lateinisch) und auch Lisu-Schrift.</td>
</tr>

<tr class="even">
<td style="font-family: Selawik;">Selawik</td>
<td align="left">Normal, Semilight, Light, fett, Semibold</td>
<td align="left">Open-Source-Schriftart, die metrisch kompatibel mit SegoeUI ist. Vorgesehen für Apps auf anderen Plattformen, auf denen SegoeUI nicht verfügbar ist. <a href="https://github.com/Microsoft/Selawik">Laden Sie Selawik über GitHub herunter.</a></td>
</tr>

</tbody>
</table>

### <a name="serif-fonts"></a>Serifenschriftarten

Mit Serifenschriftarten lassen sich größere Textmengen gut darstellen. 

<table>
<thead>
<tr class="header">
<th align="left">Schriftfamilie</th>
<th align="left">Stile</th>
<th align="left">Hinweise</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="font-family: Cambria;">Cambria</td>
<td align="left">Regular</td>
<td align="left">Serifenschriftart mit Unterstützung für europäischen Schriften (Lateinisch, Griechisch, Kyrillisch).</td>
</tr>
<tr class="even">
<td style="font-family: Courier New;">Courier New</td>
<td align="left">Normal, kursiv, fett, fett kursiv</td>
<td align="left">Serifenschriftart mit fester Breite und Unterstützung für europäische und nahöstliche Schriften (Lateinisch, Griechisch, Kyrillisch, Arabisch, Armenisch und Hebräisch).</td>
</tr>
<tr class="odd">
<td style="font-family: Georgia;">Georgia</td>
<td align="left">Normal, kursiv, fett, fett kursiv</td>
<td align="left">Unterstützung für europäische Schriften (Lateinisch, Griechisch und Kyrillisch).</td>
</tr>

<tr class="even">
<td style="font-family: Times New Roman;">Times New Roman</td>
<td align="left">Normal, kursiv, fett, fett kursiv</td>
<td align="left">Ältere Schriftart mit Unterstützung für europäische Schriften (Lateinisch, Griechisch, Kyrillisch, Arabisch, Armenisch, Hebräisch).</td>
</tr>

</tbody>
</table>

### <a name="symbols-and-icons"></a>Symbole

<table>
<thead>
<tr class="header">
<th align="left">Schriftfamilie</th>
<th align="left">Stile</th>
<th align="left">Hinweise</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Segoe MDL2-Ressourcen</td>
<td align="left">Regular</td>
<td align="left">Benutzeroberflächen-Schriftart für App-Symbole. Weitere Informationen finden Sie im Artikel <a href="segoe-ui-symbol-font.md">Segoe MDL2 Assets</a>.</td>
</tr>
<tr class="even">
<td align="left">Segoe UI-Emoji</td>
<td align="left">Regular</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">Segoe UI Symbol</td>
<td align="left">Regular</td>
<td align="left">Fallbackschriftart für Symbole</td>
</tr>
</tbody>
</table>

## <a name="related-articles"></a>Verwandte Artikel

* [Textsteuerelemente](../controls-and-patterns/text-controls.md)
* [XAML-Designressourcen](../controls-and-patterns/xaml-theme-resources.md#the-xaml-type-ramp)
* [XAML-Formatvorlagen](../controls-and-patterns/xaml-styles.md)
* [Microsoft Typografie](https://docs.microsoft.com/typography/)