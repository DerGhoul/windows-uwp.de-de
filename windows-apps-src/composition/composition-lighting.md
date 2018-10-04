---
author: daneuber
title: Kompositionsbeleuchtung
description: Die Komposition Beleuchtung APIs kann zum Hinzufügen von dynamischen 3D Beleuchtung für Ihre Anwendung verwendet werden.
ms.author: jimwalk
ms.date: 07/16/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows10, UWP
ms.localizationpriority: medium
ms.openlocfilehash: e634b18fffc4f601f6512d6ceeed51efbe9c1886
ms.sourcegitcommit: 5c9a47b135c5f587214675e39c1ac058c0380f4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/04/2018
ms.locfileid: "4351425"
---
# <a name="using-lights-in-windows-ui"></a>Verwendung von Licht in Windows-Benutzeroberfläche

Die Windows.UI.Composition-APIs können Sie in Echtzeit Animationen und Effekte erzeugen. Kompositionsbeleuchtung ermöglicht 3D Beleuchtung in 2D Anwendungen. In dieser Übersicht wird wir führen Sie über die Funktionen des setup-Komposition Licht, visuelle Elemente zum Empfangen von einzelnen Lichtquellen identifizieren und Effekte verwenden, um Materialien für Ihre Inhalte zu definieren.

> [!NOTE]
> Wenden Sie [XamlLight](/uwp/api/windows.ui.xaml.media.xamllight) Objekte wie [CompositionLights](/uwp/api/Windows.UI.Composition.CompositionLight) um XAML-UI-Elemente beleuchtet finden Sie in [XAML-Beleuchtung](xaml-lighting.md).

Kompositionsbeleuchtung ermöglicht die Erstellung interessante UI ermöglichen:

- Die Transformation von einem hellen unabhängig von anderen Objekte in der Szene immersive Szenarien wie Musik Wiedergabe Szenen ermöglichen.
- Die Möglichkeit, ein Objekt mit einem Licht zu koppeln, sodass sie zusammen verschoben unabhängig vom Rest der Szene Szenarien wie Fluent- [Reveal-](/design/style/reveal.md) Highlight ermöglichen.
- Transformation der Licht und ganze Szene als Gruppe Materialien und Tiefe zu erstellen.

Kompositionsbeleuchtung unterstützt drei wichtige Konzepte: **Light**, **Ziele**und **SceneLightingEffect**.

## <a name="light"></a>Licht

[CompositionLight](https://docs.microsoft.com/uwp/api/windows.ui.composition.compositionlight) ermöglicht Ihnen das Erstellen von verschiedenen Lichter und platzieren Sie sie im Koordinatenbereich. Diese Lichtquellen abzielen visuelle Elemente, die zu identifizieren, wenn vom Licht beleuchtet werden soll.

### <a name="light-types"></a>Lichttypen

| Typ | Beschreibung |
| --- | --- |
| [AmbientLight](/uwp/api/windows.ui.composition.ambientlight) | Von alles in der Szene reflektiert wird eine Lichtquelle, die nichtdirektionale Licht ausgibt, die angezeigt wird. |
| [DistantLight](/uwp/api/windows.ui.composition.distantlight) | Ein unendlich Lichtquelle, die Licht in einer Richtung ausgibt. Wie der Sonne. |
| [PointLight](/uwp/api/windows.ui.composition.pointlight) | Ein Punkt Quelle des Lichts, die Licht in alle Richtungen ausgibt. Wie eine Glühbirne. |
| [SpotLight](/uwp/api/windows.ui.composition.spotlight) | Eine Lichtquelle, die inneren und äußeren Kegel des Lichts ausgibt. Wie eine Taschenlampe. |

## <a name="targets"></a>Ziele

Wenn Licht ein visuelles Ziel (Hinzufügen zur Liste der [Ziele](/uwp/api/windows.ui.composition.compositionlight.targets) ), die visuelle Bearbeitung und alle seine untergeordneten Elemente bekannt und reagieren auf diese Lichtquelle. Dies kann so einfache Dinge wie eine Einstellung PointLight Quelle im Stamm der eine Struktur und alle visuellen Elemente, die folgenden reagieren auf die Animation der Richtung Licht Punkt sein.

**ExclusionsFromTargets** bietet Ihnen die Möglichkeit, die Belichtung eines visuellen oder einer Teilstruktur von visuellen Elementen auf ähnliche Weise wie das Hinzufügen von Zielen zu entfernen. Untergeordnete Elemente in der Struktur von der visuellen, der ausgeschlossen ist daher nicht leuchtet.

### <a name="sample-targets"></a>Beispiel für (Ziele)

Im folgenden Beispiel verwenden wir ein CompositionPointLight Ziel einer XAML-TextBlock.

```cs
    _pointLight = _compositor.CreatePointLight();
    _pointLight.Color = Colors.White;
    _pointLight.CoordinateSpace = text; //set up co-ordinate space for offset
    _pointLight.Targets.Add(text); //target XAML TextBlock
```

Durch Hinzufügen von Animationen auf den Offset der Punktlichter, ist ein schimmernde Effekt ganz einfach.

```cs
_pointLight.Offset = new Vector3(-(float)TextBlock.ActualWidth, (float)TextBlock.ActualHeight / 2, (float)TextBlock.FontSize);
```

Finden Sie unter der vollständige [Text zu Schimmern](https://github.com/Microsoft/WindowsUIDevLabs/tree/master/SampleGallery/Samples/SDK%2014393/TextShimmer) Beispiel an die Küche WindowUIDevLabs Beispiel, um mehr zu erfahren.

## <a name="restrictions"></a>Einschränkungen

Es gibt mehrere Faktoren zu berücksichtigen, wenn Sie bestimmen, welche Inhalte durch CompositionLight beleuchtet wird.

Konzept | Details
--- | ---
**Umgebungslicht** | Hinzufügen einer nicht-Umgebungslicht Ihrer Szene wird deaktiviert, wenn alle vorhandenen Licht.  Elemente, die nicht durch einen nicht-Umgebungslicht gezielte werden schwarz angezeigt.  Um umgebenden visuelle Elemente, die nicht vom Licht auf natürliche Weise als Ziel zu beleuchten, verwenden Sie ein Umgebungslicht in Verbindung mit anderen Lichter.
**Anzahl von Lichtern** | Alle zwei nicht-ambient Komposition Lichter können in beliebiger Kombination Sie Ihre Benutzeroberfläche als Ziel. Umgebungslicht Licht sind nicht beschränkt. Volltonfarben, sind Punkt und entfernte Licht.
**Lebensdauer** | CompositionLight auftreten Lebensdauer Startbedingungen (Beispiel: der Garbage Collector kann das Lichtobjekt wiederverwenden, bevor sie verwendet wird).  Es wird empfohlen, einen Verweis auf die Lichtquellen durch Hinzufügen von Lichtquellen als Mitglied der Anwendung Verwalten der Lebensdauer zu halten.
**Transformationen** | Lichter müssen in einem Knoten über UI platziert werden, die Effekte wie [perspektivische Transformationen](/design/layout/3-d-perspective-effects.md) in der visuellen Struktur verwendet wird, ordnungsgemäß gezeichnet werden.
**Ziele und Koordinatenraum** | CoordinateSpace ist den Platz in dem alle die Lichter-Eigenschaften festgelegt werden müssen. CompositionLight.Targets muss innerhalb der CoordinateSpace-Struktur.

## <a name="lighting-properties"></a>Beleuchtungseigenschaften

Je nach Art des Lichts verwendet kann ein Licht über Eigenschaften für Dämpfung und Speicherplatz verfügen. Nicht alle Lichtarten verwenden alle Eigenschaften.

Eigenschaft | Beschreibung
--- | ---
**Farbe** | Die [Farbe](/uwp/api/windows.ui.color) des Lichts. Beleuchtung Farbe, die Werte von [D3D](https://docs.microsoft.com/windows/uwp/graphics-concepts/light-properties) "Diffus" Umgebung und Glanzlicht, die die abgestrahlte Farbe definiert definiert sind. Beleuchtung verwendet RGBA-Werte für Licht. die alpha-Farbkomponente wird nicht verwendet.
**Richtung** | Die Richtung des Lichts. Die Richtung, in die das Licht strahlt, ist relativ zu seiner [CoordinateSpace](/uwp/api/windows.ui.composition.distantlight.coordinatespace) Visual angegeben.
**Koordinatenraum** | Jedes Visual verfügt über eine implizite 3D-Koordinatensystem. X-Richtung ist von links nach rechts. Y-Richtung wird von oben nach unten. Z-Richtung ist ein Punkt außerhalb der Ebene. Die ursprüngliche diese Koordinate ist die linke obere Ecke des visuellen Elements, und die Einheit ist Device Independent Pixel (DIP). Ein Licht Offset in diese Koordinate definiert.
**Inneren und äußeren Kegel** | Spotlights strahlen einen zweitteiligen Lichtkegel ab: einen hellen inneren Kegel und einen äußeren Kegel. Komposition ermöglicht, dass Sie die Kontrolle über inneren und äußeren Kegelwinkel und Farbe.
**Offset** | Offset der Lichtquelle relativ zum Koordinatenraums Visual.

> [!NOTE]
> Wenn mehrere Lichtquellen das gleiche visuelle erreicht, oder Farbwert eines Lichts groß genug, um 1.0 überschreiten erhält, kann die Farbe des Lichts aufgrund der Klammerung von einer Lichter Farbkanal ändern.

### <a name="advanced-lighting-properties"></a>Erweiterte Eigenschaften Beleuchtung

Eigenschaft | Beschreibung
--- | ---
**Intensität** | Steuert die Helligkeit des Lichts.
**Dämpfung** | Die Dämpfung steuert, wie die Intensität eines Lichts gegenüber der maximalen Entfernung, angegeben durch die Eigenschaft „Reichweite“, abnimmt.  Konstante, können Quadradic und Linear Dämpfungseigenschaften verwendet werden.

## <a name="getting-started-with-lighting"></a>Erste Schritte mit Beleuchtung

Führen Sie diese allgemeinen Schritte, um die Lichter hinzufügen:

- Erstellen und speichern Sie die Lichter: Licht zu erstellen und speichern Sie sie in einem angegebenen Koordinatenraum.
- Objekte, um Licht zu identifizieren: Licht am relevante visuelle Elemente als Ziel.
- [Optional] Definieren, wie einzelne Objekte reagieren auf Lichter: Verwendung SceneLightingEffect mit einer EffectBrush lichtreflektion zum Anzeigen der SpriteVisual anpassen. Reflektion Standardwerte unterstützen die Beleuchtung der untergeordneten Elemente einer Lichtquelle CoordinateSpace.  Ein visuelles Element, das mit einem SceneLightingEffect überschreibt die Standard-Beleuchtung für dieses Visual.

## <a name="scenelightingeffect"></a>SceneLightingEffect

[SceneLightingEffect](/uwp/api/Windows.UI.Composition.Effects.SceneLightingEffect) wird verwendet, um die Standard-Beleuchtung angewendet auf den Inhalt des ein [SpriteVisual](/uwp/api/Windows.UI.Composition.SpriteVisual) Ziel von einer [CompositionLight](/uwp/api/windows.ui.composition.compositionlight)zu ändern.

[SceneLightingEffect](/uwp/api/Windows.UI.Composition.Effects.SceneLightingEffect) wird häufig für Material Erstellung verwendet. Ein SceneLightingEffect ist ein Effekt verwendet, wenn Sie etwas komplexer sein, z. B. reflektierende Eigenschaften eines Bilds aktivieren bzw. eine Illusion von Tiefe mit einer normalen Zuordnung bereitstellen erreichen möchten. Ein SceneLightingEffect bietet die Möglichkeit, Ihre Benutzeroberfläche anpassen, indem Sie mithilfe der Beleuchtungseigenschaften wie und diffuse Beträge. Sie können weitere Beleuchtungseffekte mit dem Rest der Pipeline Effekte ermöglicht einzeln mischen und verfassen unterschiedliche Beleuchtung Reaktionen durch Ihren Inhalt anpassen.

> [!NOTE]
> Beleuchtung der Szene erzeugt keine Schatten; Es ist ein Effekt, 2D Rendering konzentriert.  Es ist nicht berücksichtigt 3D Beleuchtung Szenarien berücksichtigen, die tatsächliche Beleuchtung Modelle, einschließlich der Schatten enthalten.


Eigenschaft | Beschreibung
--- | ---
**Normale Karte** | NormalMaps erstellen Sie einen Effekt einer Textur, in denen ein normaler zeigt in Richtung der Lichtquelle heller und eine normale zeigen entfernt wird dunkler. Eine NormalMap Ihre benutzerorientierte visual verwenden eine [CompositionSurfaceBrush](/uwp/api/Windows.UI.Composition.CompositionSurfaceBrush) mithilfe Loadedimagesource zum Laden von einer Ressource NormalMap hinzu.
**Umgebung** | Ambiente-Eigenschaften sind hauptsächlich zum Steuern der gesamten Farbe Reflektion verwendet.
**Spiegelnde** | Spiegelnden Reflektion erstellt Lichter auf Objekte, wodurch sie glänzende angezeigt werden. Sie können die Ebene der spiegelnden Reflektion sowie der Ebene der Glanz steuern.  Diese Eigenschaften sind bearbeitet, um Material Effekte wie Shinny Metalle oder glänzende Papier zu erstellen.
**Diffuse** | Diffuse Reflektion Streut Licht in alle Richtungen.
**Reflexionsgrad-Modell** | [Reflexionsgrad Modell](/uwp/api/windows.ui.composition.effects.scenelightingeffectreflectancemodel) können Sie zwischen [Blinn Phong](https://docs.microsoft.com/visualstudio/designers/how-to-create-a-basic-phong-shader) und physikalisch basierten Blinn Phong auswählen.  Wenn Sie Glanzlichter zusammengefasst haben möchten, würden Sie physikalisch basierten Blinn Phong auswählen.

### <a name="sample-scenelightingeffect"></a>Beispiel (SceneLightingEffect)

Das folgende Beispiel zeigt, wie ein SceneLightingEffect eine normale Karte hinzu.

```cs
CompositionBrush CreateNormalMapBrush(ICompositionSurface normalMapImage)
{
    var colorSourceEffect = new ColorSourceEffect()
    {
        Color = Colors.White
    };
    var sceneLightingEffect = new SceneLightingEffect()
    {
        NormalMapSource = new CompositionEffectSourceParameter("NormalMap")
    };

    var compositeEffect = new ArithmeticCompositeEffect()
    {
        Source1 = colorSourceEffect,
        Source2 = sceneLightingEffect,
    };

    var factory = _compositor.CreateEffectFactory(sceneLightingEffect);

    var normalMapBrush = _compositor.CreateSurfaceBrush();
    normalMapBrush.Surface = normalMapImage;
    normalMapBrush.Stretch = CompositionStretch.Fill;

    var brush = factory.CreateBrush();
    brush.SetSourceParameter("NormalMap", normalMapBrush);

    return brush;
}
```

## <a name="related-articles"></a>Verwandte Artikel

- [Erstellen von Materialien und Lichter in der visuellen Ebene](https://blogs.windows.com/buildingapps/2017/08/04/creating-materials-lights-visual-layer/)
- [Übersicht über die Beleuchtung](https://docs.microsoft.com/windows/uwp/graphics-concepts/lighting-overview)
- [CompositionCapabilities-API](https://docs.microsoft.com/uwp/api/windows.ui.composition.compositioncapabilities)
- [Beleuchtungsmathematik](https://docs.microsoft.com/windows/uwp/graphics-concepts/mathematics-of-lighting)
- [SceneLightingEffect](https://docs.microsoft.com/uwp/api/windows.ui.composition.effects.scenelightingeffect)
- [WindowsUIDevLabs-GitHub-Repository](https://github.com/Microsoft/WindowsUIDevLabs)