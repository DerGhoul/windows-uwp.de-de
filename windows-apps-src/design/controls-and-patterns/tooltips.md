---
author: Jwmsft
Description: Use a tooltip to reveal more info about a control before asking the user to perform an action.
title: QuickInfos
ms.assetid: A21BB12B-301E-40C9-B84B-C055FD43D307
label: Tooltips
template: detail.hbs
ms.author: jimwalk
ms.date: 05/19/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows10, UWP
pm-contact: yulikl
design-contact: kimsea
dev-contact: stpete
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: dfd702f9ba6e28e1902ea8e595287ba10b46f4bb
ms.sourcegitcommit: 588171ea8cb629d2dd6aa2080e742dc8ce8584e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/17/2018
ms.locfileid: "1895282"
---
# <a name="tooltips"></a>QuickInfos

Eine QuickInfo ist eine kurze Beschreibung, die mit einem anderen Steuerelement oder Objekt verknüpft ist. QuickInfos erläutern Benutzern unbekannte Objekte, die in der Benutzeroberfläche nicht direkt beschrieben werden. Sie wird automatisch angezeigt, wenn der Benutzer den Fokus auf ein Steuerelement verschiebt, es gedrückt hält oder mit dem Mauszeiger darauf zeigt. Sie wird nach einigen Sekunden wieder ausgeblendet, wenn der Benutzer den Finger, den Mauszeiger oder den Tastatur-/Gamepad-Fokus bewegt.

![Eine QuickInfo](images/controls/tool-tip.png)

> **Wichtige APIs**: [ToolTip-Klasse](/uwp/api/Windows.UI.Xaml.Controls.ToolTip), [ToolTipService-Klasse](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.tooltipservice)

## <a name="is-this-the-right-control"></a>Ist dies das richtige Steuerelement?

Verwenden Sie eine QuickInfo, damit der Benutzer weitere Informationen über ein Steuerelement erhält, bevor er zum Ausführen einer Aktion aufgefordert wird. QuickInfo-Steuerelemente sollten sparsam verwendet werden, vor allem nur dann, wenn sie für Benutzer, die eine bestimmte Aufgabe ausführen möchten, wirklich nützlich sind. Es gilt folgende Faustregel: Für Informationen, die bereits an einer anderen Stelle derselben Benutzeroberfläche vermittelt werden, benötigen Sie keine QuickInfo. Eine nützliche QuickInfo bietet klärende Informationen zu einer unklaren Aktion.

Wann sollten Sie eine QuickInfo verwenden? Orientieren Sie sich an folgenden Fragen:

- **Sollen die Informationen beim Daraufzeigen sichtbar werden?**
    Wenn dies nicht erwünscht ist, verwenden Sie ein anderes Steuerelement. QuickInfos sollte niemals ohne vorhergehende Aktion angezeigt werden, sondern immer als Ergebnis einer Benutzerinteraktion.

- **Ist das Steuerelement mit Text beschriftet?**
    Wenn dies nicht der Fall ist, fügen Sie die Beschriftung als QuickInfo hinzu. Beim UX-Entwurf empfiehlt es sich, die meisten Steuerelemente inline zu beschriften, sodass QuickInfos dafür nicht erforderlich sind. Steuerelemente in Symbolleisten sowie nur Symbole zeignde Befehlsschaltflächen müssen dagegen mit QuickInfos versehen werden.

- **Wären eine Beschreibung oder zusätzliche Informationen zu einem Objekt hilfreich?**
    Verwenden Sie in diesem Fall eine QuickInfo. Der Text ist aber nur als Ergänzung gedacht – wichtige Informationen für die Hauptaufgaben dürfen nicht nur als QuickInfo vorhanden sein. Fügen Sie wichtige Informationen direkt in die Benutzeroberfläche ein, damit Benutzer nicht erst danach suchen müssen.

- **Handelt es sich bei den ergänzenden Informationen um Fehler-, Warn- oder Statusmeldungen?**
    Verwenden Sie in diesem Fall ein anderes Benutzeroberflächenelement, beispielsweise ein Flyout.

- **Müssen die Benutzer mit den Informationen interagieren?**
    Verwenden Sie in diesem Fall ein anderes Steuerelement. Eine Benutzerinteraktion mit QuickInfo ist nicht möglich, da die Informationen beim Bewegen der Maus ausgeblendet werden.

- **Müssen die Benutzer die ergänzenden Informationen drucken?**
    Verwenden Sie in diesem Fall ein anderes Steuerelement.

- **Ist anzunehmen, dass sich die Benutzer durch QuickInfo gestört oder abgelenkt fühlen?**
    Ziehen Sie in diesem Fall eine andere Lösung in Betracht. Möglicherweise können Sie ganz auf die zusätzlichen Informationen verzichten. Wenn Sie QuickInfos verwenden, obwohl dies die Benutzer möglicherweise irritiert, geben Sie den Benutzern die Möglichkeit, die QuickInfos zu deaktivieren.

## <a name="example"></a>Beispiel

<table>
<th align="left">XAML-Steuerelementekatalog<th>
<tr>
<td><img src="images/xaml-controls-gallery-sm.png" alt="XAML controls gallery"></img></td>
<td>
    <p>Wenn Sie die App <strong style="font-weight: semi-bold">XAML-Steuerelementekatalog</strong> installiert haben, klicken Sie hier, um <a href="xamlcontrolsgallery:/item/ToolTip">die App zu öffnen und ToolTip in Aktion zu sehen</a>.</p>
    <ul>
    <li><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Erwerben Sie die XAML-Steuerelementekatalog-App (Microsoft Store)</a></li>
    <li><a href="https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlUIBasics">Erwerben Sie den Quellcode (GitHub)</a></li>
    </ul>
</td>
</tr>
</table>

Eine QuickInfo in der App „Bing Karten”.

![Eine QuickInfo in der App „Bing Karten”](images/control-examples/tool-tip-maps.png)

## <a name="create-a-tooltip"></a>Erstellen einer QuickInfo

Eine [QuickInfo](/uwp/api/Windows.UI.Xaml.Controls.ToolTip) muss einem anderen Benutzeroberflächenelement zugewiesen werden, das deren Eigentümer ist. Die [ToolTipService](/uwp/api/windows.ui.xaml.controls.tooltipservice)-Klasse bietet statische Methoden zum Anzeigen einer QuickInfo.

Verwenden Sie in XAML die angefügte **ToolTipService.Tooltip**-Eigenschaft, um die QuickInfo einem Eigentümer zuzuweisen.

```xaml
<Button Content="Submit" ToolTipService.ToolTip="Click to submit"/>
```

Verwenden Sie im Code die Methode [ToolTipService.SetToolTip](/uwp/api/windows.ui.xaml.controls.tooltipservice.settooltip), um die QuickInfo einem Eigentümer zuzuweisen.

```xaml
<Button x:Name="submitButton" Content="Submit"/>
```

```csharp
ToolTip toolTip = new ToolTip();
toolTip.Content = "Click to submit";
ToolTipService.SetToolTip(submitButton, toolTip);
```

### <a name="content"></a>Inhalt

Sie können jedes beliebige Objekt als [Inhalt](/uwp/api/windows.ui.xaml.controls.contentcontrol.content) einer QuickInfo verwenden. Hier ist ein Beispiel für die Verwendung eines [Bilds](/uwp/api/windows.ui.xaml.controls.image) in einer QuickInfo.

```xaml
<TextBlock Text="store logo">
    <ToolTipService.ToolTip>
        <Image Source="Assets/StoreLogo.png"/>
    </ToolTipService.ToolTip>
</TextBlock>
```

### <a name="placement"></a>Platzierung

Standardmäßig wird eine QuickInfo über dem Zeiger zentriert angezeigt. Die Platzierung wird nicht durch das App-Fenster eingeschränkt, sodass die QuickInfo möglicherweise teilweise oder komplett außerhalb der Grenzen des App-Fensters angezeigt wird.

Wenn eine QuickInfo die Inhalte verdeckt, auf die sie sich bezieht, können Sie ihre Position anpassen. Verwenden Sie die Eigenschaft [Placement](/uwp/api/windows.ui.xaml.controls.tooltip.placement) oder die angefügte **ToolTipService.Placement**-Eigenschaft, um die QuickInfo über, unter, links oder rechts neben dem Zeiger zu platzieren. Sie können die Eigenschaften [VerticalOffset](/uwp/api/windows.ui.xaml.controls.tooltip.verticaloffset) und [HorizontalOffset](/uwp/api/windows.ui.xaml.controls.tooltip.horizontaloffset) so festlegen, dass der Abstand zwischen dem Zeiger und der QuickInfo geändert wird.

```xaml
<!-- A TextBlock with an offset ToolTip. -->
<TextBlock Text="TextBlock with an offset ToolTip.">
    <ToolTipService.ToolTip>
        <ToolTip Content="Offset ToolTip."
                 HorizontalOffset="20" VerticalOffset="30"/>
    </ToolTipService.ToolTip>
</TextBlock>
```

## <a name="recommendations"></a>Empfehlungen

- Verwenden Sie QuickInfos sparsam (oder gar nicht). QuickInfos stellen eine Unterbrechung dar. Eine QuickInfo kann genauso ablenkend wirken wie ein Popup. Verwenden Sie sie daher nur, wenn sie wirklich von Bedeutung sind.
- Halten Sie den QuickInfo-Text kurz. QuickInfos eignen sich gut für kurze Sätze und Satzfragmente. Längere Textblöcke können überfrachtet wirken, sodass ein Timeout für die QuickInfo auftritt, bevor der Benutzer sie zu Ende gelesen hat.
- Erstellen Sie hilfreiche QuickInfo-Texte mit ergänzenden Informationen. Der QuickInfo-Text muss informativ sein. Verwenden Sie keine selbstverständlichen oder bereits auf dem Bildschirm vorhandenen Informationen als QuickInfo-Text. Da der QuickInfo-Text nicht immer angezeigt wird, sollte er nur ergänzende Informationen enthalten, die nicht unbedingt gelesen werden müssen. Teilen Sie wichtige Informationen in Form von selbsterklärenden Beschriftungen für Steuerelemente oder direkt eingefügtem ergänzendem Text mit.
- Verwenden Sie ggf. Bilder als QuickInfo. Manchmal ist ein Bild aussagekräftiger als Text. Wenn der Benutzer z.B. auf einen Hyperlink zeigt, können Sie als QuickInfo eine Vorschau der verknüpften Seite anzeigen.
- Verwenden Sie die QuickInfo nicht, um bereits in der UI vorhandene Informationen anzuzeigen. Versehen Sie z.B. keine Schaltfläche mit QuickInfo-Text, der bereits auf der Schaltfläche selbst angezeigt wird.
- Fügen Sie in QuickInfos keine interaktiven Steuerelemente ein.
- Fügen Sie in QuickInfos keine Bilder ein, die wie interaktive Steuerelemente aussehen.

## <a name="get-the-sample-code"></a>Beispielcode herunterladen

- [Beispiel eines XAML-Steuerelementkatalogs](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/XamlUIBasics) – Hier werden alle XAML-Steuerelemente in einem interaktiven Format dargestellt.

## <a name="related-articles"></a>Verwandte Artikel

- [QuickInfo-Klasse](https://msdn.microsoft.com/library/windows/apps/br227608)