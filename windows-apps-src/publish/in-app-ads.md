---
author: jnHs
Description: Wenn Ihre App Anzeigen mit Microsoft Advertising-SDK anzeigt, verwenden Sie die Seite In-App-Anzeige im Dev Center-Dashboard, um die Verwendung Ihrer Anzeigen zu verwalten.
title: In-App-Anzeigen
ms.assetid: 09970DE3-461A-4E2A-88E3-68F2399BBCC8
ms.author: wdg-dev-content
ms.date: 10/26/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows10, UWP
localizationpriority: high
ms.openlocfilehash: eb835269cd9df7385d8d03e032d8b41cb7f92a19
ms.sourcegitcommit: 44a24b580feea0f188c7eae36e72e4a4f412802b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/31/2017
---
# <a name="in-app-ads"></a>In-App-Anzeigen

Verwenden Sie die Seite **Monetarisieren** &gt; **In-App-Anzeige** im Dev Center-Dashboard, um Anzeigeneinheiten zu erstellen und verwalten:

* Apps für die universelle Windows-Plattform (UWP), die [Microsoft Advertising-SDK](http://aka.ms/ads-sdk-uwp) verwenden.
* Apps für Windows8.x und Windows Phone8.x, die [Microsoft Advertising-SDK für Windows und Windows Phone 8.x](http://aka.ms/store-8-sdk) verwenden.

Weitere Informationen dazu, wie Sie diese SDKs in Ihren Apps zu Werbezwecken integrieren, finden Sie unter [Anzeigen von Werbung in Ihrer App mit dem Microsoft Advertising-SDK](../monetize/display-ads-in-your-app.md).

<span id="create-ad-unit" />
## <a name="create-ad-units"></a>Erstellen von Anzeigeneinheiten

So erstellen Sie eine Anzeigeeinheit für eine [Banneranzeige](../monetize/banner-ads.md), [Interstitialwerbung](../monetize/interstitial-ads.md) oder [native Anzeige](../monetize/native-ads.md) in Ihrer App:

1.  Wechseln Sie auf die Seite **Monetarisieren** &gt; **In-App-Anzeige** im Dashboard und klicken Sie auf **Anzeigeneinheit erstellen**.

2.  Wählen Sie in der Dropdownliste **App-Name** die App aus, in der die Anzeigeneinheit verwendet werden soll.

3.  Geben Sie im Feld **Name der Anzeigeneinheit** einen Namen für die Anzeigeneinheit ein. Dies kann eine beliebige beschreibende Zeichenfolge sein, die Sie verwenden, um die Anzeigeneinheit zu Berichterstellungszwecken zu identifizieren.

4.  Wählen Sie in der Dropdownliste **Art der Anzeigeneinheit** den Anzeigentyp aus.

    * Wenn Sie in Ihrer App ein [AdControl](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.adcontrol.aspx) zum Anzeigen von Banneranzeigen verwenden, wählen Sie **Banner** aus.

    * Wenn Sie in Ihrer App ein [InterstitialAd](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.interstitialad.aspx) zum Anzeigen von Videoanzeigen oder von Interstitial-Banneranzeigen verwenden, wählen Sie **Interstitialvideo** oder **Interstitialbanner** aus (achten Sie darauf, dass Sie die der Art der Interstitialwerbung, die Sie anzeigen möchten, entsprechende Option auswählen).

    * Wenn Sie in Ihrer App ein [NativeAd](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.nativead.aspx) zum Anzeigen von nativen Anzeigen verwenden, wählen Sie **Nativ** aus.
      > [!NOTE]
      > Die Möglichkeit zum Erstellen von **nativen** Anzeigeeinheiten steht derzeit nur für Entwickler zur Verfügung, die an einem Pilotprogramm teilnehmen, wir möchten dieses Feature allerdings bald für alle Entwickler zur Verfügung stellen. Wenn Sie an unserem Pilotprogramms teilnehmen möchten, wenden Sie sich an aiacare@microsoft.com.

5. Wählen Sie in der Dropdownliste **Gerätefamilie** die Gerätefamilie aus, auf die Ihre App ausgerichtet ist, in der die Anzeigeneinheit verwendet werden. Folgende Optionen sind verfügbar: **UWP (Windows 10)**, **PC/Tablet (Windows 8.1)** oder **Mobile (Windows Phone 8.x)**.

6. Konfigurieren Sie die folgenden zusätzlichen Einstellungen wie gewünscht:

    * Wenn Sie eine **UWP (Windows10)**-Gerätefamilie für die Anzeigeneinheit auswählen, können Sie optional die [Vermittlungseinstellungen](#mediation) für die Anzeigeneinheit konfigurieren.

    * Wenn Sie die **PC/Tablet (Windows8.1)** oder **Mobile (Windows Phone8.x)**-Gerätefamilie für eine Banneranzeigeneinheit auswählen, können Sie optional **Community-Anzeigen in Ihrer App anzeigen** auswählen, um sich bei [Community-Anzeigen](about-community-ads.md) anzumelden.

7.  Wenn Sie die COPPA-Compliance für die ausgewählte App noch nicht eingerichtet haben, wählen Sie eine Option im Abschnitt [COPPA-Compliance](#coppa) aus.

8.  Klicken Sie auf **Anzeigeneinheit erstellen**.

Nachdem Sie die neue Anzeigeneinheit erstellen, wird diese in der Tabelle der verfügbaren Anzeigeneinheiten auf der Seite **Monetisierung** &gt; **In-App-Werbung** angezeigt.

<span id="available-ad-units" />
## <a name="review-and-edit-ad-units"></a>Überprüfen und Bearbeiten von Anzeigeneinheiten

Nach dem Erstellung von Anzeigeneinheiten für eine oder mehrere Apps auf Ihrem Konto , werden diese Anzeigeeinheiten in einer Tabelle am unteren Rand der Seite **Monetisierung** &gt; **In-App-Werbung** angezeigt. Diese Tabelle zeigt die **Anwendungs-ID** und **Anzeigeneinheits-ID** für jede Anzeigeneinheit zusammen mit anderen Informationen an. Zum Einblenden von Anzeigen in Ihrer App müssen Sie diese Werte in Ihrem Code verwenden. Weitere Informationen finden Sie unter [Einrichten von Anzeigeneinheiten in der App](../monetize/set-up-ad-units-in-your-app.md).

* Wenn Ihre App [Banneranzeigen](../monetize/banner-ads.md) anzeigt, weisen Sie diese Werte den Eigenschaften [ApplicationId](https://msdn.microsoft.com/library/mt313174.aspx) und [AdUnitId](https://msdn.microsoft.com/library/mt313171.aspx) Ihres [AdControl](https://msdn.microsoft.com/library/mt313154.aspx)-Objekts hinzu.

* Wenn Ihre App [Interstitialwerbung](../monetize/interstitial-ads.md) anzeigt, übergeben Sie diese Werte an die [RequestAd](https://msdn.microsoft.com/library/mt313192.aspx)-Method Ihres [InterstitialAd](https://msdn.microsoft.com/library/mt313189.aspx)-Objekts.

* Wenn Ihre App [native Anzeigen](../monetize/native-ads.md) anzeigt, weisen Sie diese Werte den Parametern *applicationId* und *adUnitId* des [NativeAdsManager](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.nativeadsmanager.nativeadsmanager.aspx)-Konstruktors hinzu.
  > [!IMPORTANT]
  > Sie können jede Anzeigeneinheit in nur einer App verwenden. Wenn Sie eine Anzeigeneinheit in mehr als einer App verwenden, werden für die Ad-Einheit keine Anzeigen platziert.

  > [!NOTE]
  > Können mehrere Steuerelemente für Banner-, Interstitialwerbungen und native Anzeigen in einer einzelnen App verwenden. In diesem Fall wird empfohlen, dass Sie jedem Steuerelement eine andere Anzeigeneinheit zuweisen. Durch das Verwenden verschiedener Anzeigeeinheiten für jedes Steuerelement können Sie für jedes Steuerelement [die Einstellungen für die Anzeigenvermittlung konfigurieren](../publish/in-app-ads.md#mediation) und diskrete [Berichtsdaten](../publish/advertising-performance-report.md). Außerdem können unsere Dienste so die Werbung optimieren, die wir in Ihrer App anzeigen.

Um die [Vermittlungseinstellungen](#mediation) für eine UWP-Anzeigeneinheit oder die [COPPA-Compliance](#coppa) für die App, in denen die Anzeigeneinheit verwendet wird, zu bearbeiten, klicken Sie auf den Namen der Anzeigeneinheit.

<span id="mediation" />
## <a name="mediation-settings"></a>Einstellungen der Anzeigenvermittlung

Wenn Sie [Eine neue UWP-Anzeigeneinheit erstellen](#create-ad-unit) oder [Eine vorhandene UWP-Anzeigeneinheit bearbeiten](#available-ad-units), verwenden Sie die Optionen in diesem Abschnitt zum Konfigurieren der Anzeigenvermittlung für die Anzeigeneinheit. Mit der Anzeigenvermittlung können Sie Ihre Anzeigenumsätze maximieren und Werbefunktionen optimal nutzen, indem Sie Anzeigen aus mehreren Anzeigennetzwerken anzeigen, einschließlich Anzeigen aus anderen kostenpflichtigen Anzeigennetzwerken und Anzeigen ohne Umsatzgenerierung zu Werbekampagnen für Microsoft-Apps. Wir kümmern uns um die Vermittlung von Banneranzeigenanforderungen von den gewählten Anzeigennetzwerken. Wenn Sie eine UWP-Anzeigeneinheit haben, die bereits mit einer Banner-, Interstitial oder nativen Anzeige in Ihrer App verbunden ist, erfordert das Aktivieren der Anzeigenvermittlung keine Codeänderungen in Ihrer App.

> [!NOTE]
> Wenn Sie die Anzeigenvermittlung für eine UWP-Anzeigeneinheit aktivieren, müssen Sie keine Anzeigeneinheit von Drittanbieter-Anzeigennetzwerken erhalten. Unser Anzeigenvermittlungsdienst erstellt automatisch alle erforderlichen Drittanbieter-Anzeigeneinheiten.

So konfigurieren Sie die Anzeigenvermittlung für eine UWP-Anzeigeneinheit in Ihrer App:

1. [Eine Anzeigeneinheit erstellen](#create-ad-unit) oder [Eine vorhandene Anzeigeneinheit auswählen](#available-ad-units).

2. Wechseln Sie auf der Seite **In-App-Anzeige** zum Abschnitt **Vermittlungseinstellungen**.

3. Standardmäßig ist das Kontrollkästchen **Let Microsoft choose the best mediation settings for your app** aktiviert. Diese Option verwendet Machine Learning-Algorithmen, um automatisch die Anzeigenvermittlungseinstellungen für Ihre App auszuwählen, um Ihnen beim Optimieren der Anzeigenumsätze in den verschiedenen Märkten zu helfen, die Ihre App unterstützt. Es wird empfohlen, diese Option zu verwenden. Wenn Sie Ihre eigenen Anzeigenvermittlungseinstellungen auswählen möchten, deaktivieren Sie das Kontrollkästchen.
    > [!NOTE]
    > Die verbleibenden Schrittein diesem Abschnittgelten nur, wenn Sie dieses Kontrollkästchen deaktivieren und eigene Anzeigenvermittlungseinstellungen auswählen.

4. Wählen Sie in der Dropdownliste **Ziel** die Option **Basisplan**, um die Standardkonfiguration für Ihre Anzeigenvermittlungseinstellungen zu konfigurieren. Diese Standardkonfiguration wird auf alle Märkte angewendet, mit Ausnahme von Märkten, für die Sie marktspezifische Konfigurationen definieren.

6. Geben Sie dann das Verhältnis der Anzeigen an, die Sie auf dem Steuerelement von kostenpflichtigen Netzwerken (die Sie für Aufrufe bezahlen) und anderen Anzeigennetzwerken (die Sie nicht für Aufrufe bezahlen) anzeigen möchten. Geben Sie hierzu einen Wert zwischen 0 und 100 im Feld **Gewichtung** für **Paid ad networks** und **Weitere Anzeigennetzwerke** ein.  

7. Aktivieren Sie im Abschnitt **Paid ad networks** das Kontrollkästchen in der Spalte **Aktiv** für jedes [kostenpflichtige Netzwerk](#paid-networks), das Sie verwenden möchten, und sortieren Sie die Netzwerke dann mithilfe der Pfeile in der Spalte **Rang** nach Rang. (Dies gibt an,wie oft jedes Netzwerk von Ihrem Steuerelement verwendet werden soll.)

8. Wenn Sie eine **Banner** oder **Interstitialwerbung**-Anzeigeneinheit ausgewählt haben, sehen Sie außerdem einen Abschnitt namens **Weitere Anzeigennetzwerke **. Mit den Netzwerken in diesem Abschnitt erzielen Sie keine Einnahmen für Anzeigenaufrufe. Stattdessen zeigen diese Netzwerke Werbung aus Quellen wie Werbekampagnen für Apps an.

    Aktivieren Sie im Abschnitt **Weitere Anzeigennetzwerke** das Kontrollkästchen in der Spalte **Aktiv** für jedes [weitere Netzwerk](#other-networks), das Sie verwenden möchten, und sortieren Sie die Netzwerke dann mithilfe der Pfeile in der Spalte **Rang** nach Rang. (Dies gibt an,wie oft jedes Netzwerk von Ihrem Steuerelement verwendet werden soll.) Die folgenden weiteren Netzwerke werden derzeit unterstützt:

9. Für jeden Markt, in dem Sie die Standardvermittlungskonfiguration außer Kraft setzen möchten, wählen Sie den Markt in der Dropdownliste **Ziel**, und aktualisieren Sie die Anzeigennetzwerkauswahl und den Rang.

10. Klicken Sie auf **Anzeigeneinheit erstellen** (wenn Sie eine neue Anzeigeneinheit erstellen) oder **Speichern** (wenn Sie eine vorhandene Anzeigeneinheit bearbeiten).

<span id="paid-networks" />
### <a name="supported-paid-ad-networks"></a>Unterstützte Anzeigennetzwerke

Die folgende Tabelle enthält die kostenpflichtigen Netzwerke, die wir derzeit für jeden Anzeigentyp unterstützen. Beachten Sie, dass einige dieser Netzwerke [nicht in allen Märkten verfügbar](#network-markets) sind.

|  Anzeigennetzwerk  |  Beschreibung  |  Unterstützte Anzeigentypen  |
|--------------|---------------|---------------------|
| AOL and AppNexus |  Dies ist ein von Microsoft verwaltetes Anzeigennetzwerk, das Anzeigen über unsere Partnernetzwerke AOL und AppNexus bereitstellt.<p/>**Hinweis**: AOL und AppNexus haben in der Liste **Paid ad networks** für Banner-Anzeigeneinheiten stets an erster Stelle. Für diese Art von Anzeigen kann kein niedrigerer Rang festgelegt werden. | Banneranzeigen, Video-Interstitialanzeigen |
| AppNexus (direkt) | Wählen Sie diese Option, um Video-Interstitialanzeigen von [AppNexus](https://www.appnexus.com) anzuzeigen. | Video-Interstitialanzeigen, native Anzeigen  |
| Microsoft-Anzeigen für die App-Installation | Wählen Sie diese Option, um Anzeigen für die App-Installation oder das Wiedereinschalten von Anzeigen in Apps anzuzeigen, die von anderen Entwicklern im Windows-Ökosystem erstellt wurden, die [Werbeanzeigenkampagnen für ihre Apps erstellen](create-an-ad-campaign-for-your-app.md).  |  Banneranzeigen, Banner-Interstitialwerbung, native Anzeigen  |
| Smaato |  Wählen Sie diese Option zum Bereitstellen von Anzeigen von [Smaato](https://www.smaato.com/). |  Banner  |
| Smartclip |  Wählen Sie diese Option zum Bereitstellen von Anzeigen von [Smartclip](http://www.smartclip.com/). |  Video-Interstitialanzeigen  |
| SpotX |  Wählen Sie diese Option zum Bereitstellen von Anzeigen von [SpotX](https://www.spotx.tv/). |  Video-Interstitialanzeigen  |
| Taboola |  Wählen Sie diese Option zum Bereitstellen von Anzeigen von [Taboola](https://www.taboola.com/). |  Banner  |

<span id="other-networks" />
### <a name="other-ad-networks"></a>Weitere Anzeigennetzwerke

Die folgende Tabelle enthält die anderen Netzwerke, die wir derzeit für jeden Anzeigentyp unterstützen.

|  Anzeigennetzwerk  |  Beschreibung  |  Unterstützte Anzeigentypen  |
|--------------|---------------|---------------------|
| MicrosoftCommunity-Anzeigen |  Wenn Sie [eine Anzeigenkampagne für eine Ihrer Apps erstellen](create-an-ad-campaign-for-your-app.md) und diese Kampagne als [Kampagne für Community-Anzeigen](about-community-ads.md) konfigurieren, wählen Sie diese Optionen, um Anzeigen aus dieser Kampagne anzuzeigen. | Banneranzeigen, Banner-Interstitialwerbung |
| Microsoft-Eigenwerbung | Wenn Sie [eine Anzeigenkampagne für eine Ihrer Apps erstellen](create-an-ad-campaign-for-your-app.md) und diese Kampagne als [Kampagne für Eigenwerbung](about-house-ads.md) konfigurieren, wählen Sie diese Optionen, um Anzeigen aus dieser Kampagne anzuzeigen. | Banneranzeigen, Banner-Interstitialwerbung  |


<span id="network-markets" />
### <a name="supported-markets-for-ad-networks"></a>Unterstützte Märkte für Anzeigennetzwerke

Die verfügbaren Anzeigennetzwerke schalten Anzeigen in allen [unterstützten Märkten](define-pricing-and-market-selection.md#microsoft-store-consumer-markets) mit den folgenden Ausnahmen.

|  Anzeigennetzwerk  |  Unterstützte Märkte  |
|--------------|---------------------|
| Smaato | Brasilien, Kanada, Frankreich, Deutschland, Italien, Japan, Spanien, Großbritannien, USA |
| smartclip | Österreich, Belgien, Dänemark, Finnland, Deutschland, Italien, Niederlande, Norwegen, Schweden, Schweiz  |

<span id="coppa" />
## <a name="coppa-compliance"></a>COPPA-Compliance

Um die Einhaltung der Richtlinien des Children's Online Privacy Protection Act („COPPA“) sicherzustellen, müssen Sie Microsoft benachrichtigen, wenn Ihre App an Kinder unter 13 Jahren gerichtet ist. Wenn unter Verwendung von Dev Center Microsoft mitteilen, dass Ihre App an Kinder unter 13 Jahren gerichtet ist, deaktiviert Microsoft die verhaltensorientierten Werbedienste bei der Übermittlung von Werbung an Ihre App. Wenn Ihre App an Kinder unter 13 Jahren gerichtet ist, ergeben sich aus COPPA bestimmte Verpflichtungen für Sie.

Weitere Informationen über Ihre Verpflichtungen im Rahmen von COPPA finden Sie [auf dieser Seite](http://go.microsoft.com/fwlink/p/?linkid=536558).