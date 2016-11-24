---
author: joannaleecy
title: "Monetarisierung für Spiele"
description: "Implementieren Sie Banneranzeigen, Videointerstitialanzeigen und In-App-Käufe für Universal Spiele für die universelle Windows-Plattform (UWP) unter Windows10."
ms.assetid: 79f4e177-d8e7-45d3-8a78-31d4c2fe298a
translationtype: Human Translation
ms.sourcegitcommit: 1afcb25eeacadee89097a69ca64404f1102b3e57
ms.openlocfilehash: 00ab2e2f8b9b086bfcfe31972816a56f7e043d5c

---
#  Monetarisierung für Spiele

Als Spieleentwickler müssen Sie Ihre Monetisierungsoptionen kennen, um die Rentabilität Ihres Unternehmens gewährleisten und weiterhin Ihrer Leidenschaft nachgehen zu können: der Entwicklung großartiger Spiele. Dieser Artikel enthält eine Übersicht über die Monetarisierungsmethoden für ein Spiel für die universelle Windows-Plattform (UWP) und ihre Implementierung.

Bisher haben Sie Ihr Spiel einfach mit einem Preis versehen und gewartet, dass es von Benutzern in einem Geschäft erworben wird. Heute haben Sie jedoch verschiedene Optionen. Sie können ein Spiel in einem normalen Geschäft anbieten, es online (als physische Version oder als Softcopy) verkaufen oder Benutzer das Spiel kostenlos spielen lassen, dabei aber gewisse Anzeigen oder In-Game-Gegenstände integrieren, die erworben werden können. Spiele sind auch nicht mehr einfach eigenständige Produkte. Sie werden häufig mit zusätzlichem Inhalt bereitgestellt, der zusätzlich zum Hauptspiel erworben werden kann. 

Sie können ein UWP-Spiel folgendermaßen bewerben und monetisieren:
* Veröffentlichen Sie Ihr Spiel im Windows Store, einem sicheren Onlinestore, der die [weltweite Verteilung](#worldwide-distribution-channel) ermöglicht. Spieler auf der ganzen Welt können Ihr Spiel online zu dem von Ihnen [festgelegten Preis](#set-a-price-for-your-game) kaufen.
* Verwenden Sie APIs im Windows SDK zum Erstellen von [In-Game-Käufen](#in-game-purchases). Spieler können In-Game-Käufe tätigen oder ergänzende Inhalte wie zusätzliche Ausstattung, Designs, Karten oder Spiellevels kaufen.
* Verwenden Sie APIs im [Microsoft Store Services SDK](https://visualstudiogallery.msdn.microsoft.com/229b7858-2c6a-4073-886e-cbb79e851211), um Anzeigen aus Anzeigennetzwerken anzuzeigen. Sie können [Anzeigen in Ihrem Spiel anzeigen](#display-ads-in-your-game) und Spielern die Option anbieten, Videoanzeigen im Austausch für In-Game-Belohnungen anzusehen.
* [Maximieren Sie das Potenzial des Spiels über Anzeigenkampagnen](#maximize-your-games-potential-through-ad-campaigns). Bewerben Sie Ihr Spiel mithilfe von kostenpflichtigen Anzeigenkampagnen, kostenlosen Community-Anzeigenkampagnen oder kostenloser Eigenwerbung, um die Benutzeranzahl zu steigern.
 
## Weltweiter Vertriebskanal

Im Windows Store kann Ihr Spiel zum Download in mehr als 200Ländern und Regionen weltweit zur Verfügung gestellt werden, und für die Abrechnung werden verschiedene Zahlungsmethoden (einschließlich Visa, MasterCard und PayPal) unterstützt. Eine vollständige Liste der Länder und Regionen finden Sie unter [Märkte und angepasste Preise](https://msdn.microsoft.com/windows/uwp/publish/define-pricing-and-market-selection#markets-and-custom-prices).

## Festlegen eines Preises für Ihr Spiel 

Im Store veröffentlichte UWP-Spiele können _kostenpflichtig_ oder _kostenlos_ sein. Bei einem kostenpflichtigen Spiel können Sie fordern, dass Spieler vorab einen von Ihnen festgelegten Preis für Ihr Spiel zahlen. Kostenlose Spiele hingegen können von Benutzern heruntergeladen und gespielt werden, ohne dass sie dafür bezahlen müssen.

Hier sind einige wichtige Konzepte bezüglich der Preise für Ihr Spiel im Store aufgeführt.

### Grundpreis 

Der Grundpreis für das Spiel bestimmt, ob Ihr Spiel als _bezahlt_ oder _kostenlos_ eingestuft wird. Sie können den Grundpreis basierend auf Land und Region mithilfe des [Dev Center-Dashboards](https://developer.microsoft.com/windows) konfigurieren. Beim Festlegen des Preises müssen unter Umständen [Steuerpflichten beim Verkauf in anderen Ländern](https://msdn.microsoft.com/windows/uwp/publish/tax-details-for-paid-apps) und [Kostenüberlegungen für bestimmte Märkte](https://msdn.microsoft.com/windows/uwp/publish/define-pricing-and-market-selection#price-considerations-for-specific-markets) in Betracht gezogen werden. Sie können auch [angepasste Preise für spezifische Märkte](https://msdn.microsoft.com/windows/uwp/publish/define-pricing-and-market-selection#markets-and-custom-prices) festlegen. Weitere Informationen erhalten Sie unter [Festlegen des Preises und Auswählen der Märkte](https://msdn.microsoft.com/windows/uwp/publish/define-pricing-and-market-selection).

### Angebotspreis

Eine Werbemöglichkeit für Ihr Spiel besteht beispielsweise in der Senkung des Preises für einen bestimmten Zeitraum. Sie können als Angebotspreis auch __Kostenlos__ festlegen, damit Ihr Spiel kostenlos heruntergeladen werden kann.
Sie können Angebotskampagnen im Voraus planen, indem Sie Start- und Enddatum des Angebots festlegen. Weitere Informationen finden Sie unter [Anbieten von Apps und Add-Ons](https://msdn.microsoft.com/windows/uwp/publish/put-apps-and-add-ons-on-sale).

## In-Game-Käufe

Bei In-Game-Käufen handelt es sich um Produkte, die in einem Spiel gekauft werden. Sie werden allgemein auch als _In-App-Käufe_ bezeichnet. Im Windows Store heißen diese Produkte _Add-Ons_. [Add-Ons werden über das Windows Dev Center-Dashboard veröffentlicht](https://msdn.microsoft.com/windows/uwp/publish/add-on-submissions). Sie müssen die Add-Ons außerdem im Code Ihres Spiels aktivieren.

### Arten von Add-Ons

Sie können zwei Arten von Add-Ons im Store erstellen: _Gebrauchsgüter_ oder _Verbrauchsartikel_. Gebrauchsgüter sind Elemente, die bis zu ihrem Ablauf für einen angegebenen Zeitraum erhalten bleiben und nur einmal erworben werden können. Verbrauchsartikel sind Elemente, die gekauft und immer wieder verwendet werden können.

Beim Erstellen von Verbrauchsartikeln entscheiden Sie, wie Sie sie nachverfolgen möchten, d.h. ob sie _vom Entwickler verwaltet_ oder _vom Store verwaltet_ werden. (Dieses Feature ist ab Windows10, Version 1607, verfügbar). Bei einem vom Entwickler verwalteten Verbrauchsartikel sind Sie für die Nachverfolgung des Guthabens des Benutzers an Elementen zuständig. Bei einem vom Store verwalteten Verbrauchsartikel verfolgt der Windows Store das Elementguthaben für Sie. Weitere Informationen finden Sie unter [Übersicht über Endverbraucher-Add-Ons](https://msdn.microsoft.com/windows/uwp/monetize/enable-consumable-add-on-purchases#overview-of-consumable-add-ons).

### Erstellen von In-Game-Käufen

Die aktuellen APIs für In-App-Käufe und Lizenzinformationen sind Teil des [Windows.Services.Store](https://msdn.microsoft.com/library/windows/apps/windows.services.store.aspx)-Namespace im Windows SDK (ab Windows10, Version 1607). Bei der Entwicklung eines neuen Spiels für 1607 oder eine höhere Version wird empfohlen, den __Windows.Services.Store__-Namespace zu verwenden, da er die aktuellen Add-On-Typen unterstützt und eine bessere Leistung bietet.
Darüber hinaus wurde er für die Kompatibilität mit künftigen Arten von Produkten und Features entwickelt, die von Windows Dev Center und vom Store unterstützt werden. Verwenden Sie bei der Entwicklung für vorherige Windows10-Versionen stattdessen den [Windows.ApplicationModel.Store](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.store.aspx)-Namespace.

Weitere Informationen finden Sie unter [In-App-Käufe und Testversionen](https://msdn.microsoft.com/windows/uwp/monetize/in-app-purchases-and-trials).

#### Vereinfachtes Kaufbeispiel

In diesem Abschnitt wird anhand eines vereinfachten Kaufbeispiels die Verwendung verschiedener Methodenaufrufe für die Implementierung des Kaufablaufs veranschaulicht.

|In-Game-Aktionen/-Aktivität                                                | Hintergrundaufgaben                  |
|--------------------------------------------------------------------------|----------------------------------------|
|Ein Spieler betritt ein Geschäft. Das Einkaufsmenü mit den verfügbaren Add-Ons und dem jeweiligen Kaufpreis wird angezeigt. |  Das Spiel [ruft die Produktinfos](https://msdn.microsoft.com/windows/uwp/monetize/get-product-info-for-apps-and-add-ons) des Add-Ons ab, [bestimmt, ob die Add-Ons über die entsprechende Lizenz verfügen](https://msdn.microsoft.com/windows/uwp/monetize/get-license-info-for-apps-and-add-ons) und zeigt im Einkaufsmenü die Add-Ons an, die für den Spieler zum Kauf zur Verfügung stehen.                           |
|Der Spieler klickt auf __Kaufen__um ein Element zu kaufen.             |Die Aktion __Kaufen__ sendet eine Anforderung zum Kauf des Elements und beginnt den Zahlungsprozess, um es zu erwerben. Die Implementierung variiert je nach Elementtyp. Handelt es sich um ein [Gebrauchsgut oder ein einmalig erworbenes Element](https://msdn.microsoft.com/windows/uwp/monetize/enable-in-app-purchases-of-apps-and-add-ons), kann der Kunde nur ein einzelnes Element besitzen, bis es abläuft. Ist das Element ein [Verbrauchsartikel](https://msdn.microsoft.com/windows/uwp/monetize/enable-consumable-add-on-purchases), kann der Kunde mehrere davon besitzen. |

### Testen von In-Game-Käufen während der Spieleentwicklung

Da ein Add-On im Zusammenhang mit einem Spiel erstellt werden muss, muss das Spiel im Store veröffentlicht worden und verfügbar sein. Die Schritte in diesem Abschnitt zeigen, wie Add-Ons erstellt werden, während sich das Spiel noch in der Entwicklung befindet.
(Wenn Ihr fertiges Spiel bereits im Store veröffentlicht wurde, können Sie die ersten drei Schritte überspringen und direkt mit [Erstellen eines Add-Ons im Store](#create-an-add-on-in-the-store) fortfahren.)

So erstellen Sie Add-Ons, während sich das Spiel noch in der Entwicklung befindet: 
1. [Erstellen eines Pakets](#create-a-package)
2. [Veröffentlichen des Spiels als ausgeblendet](#publish-the-game-as-hidden)
3. [Verknüpfen Ihrer Spielelösung in Visual Studio mit dem Store](#associate-your-game-solution-with-the-store)
4. [Erstellen eines Add-Ons im Store](#create-an-add-on-in-the-store)

#### Erstellen eines Pakets

Damit ein Spiel veröffentlicht werden kann, muss es die Mindestanforderungen der Zertifizierung für Windows-Apps erfüllen. Sie können das [Zertifizierungskit für Windows-Apps](https://msdn.microsoft.com/windows/uwp/debug-test-perf/windows-app-certification-kit) (Teil des Windows 10 SDK) verwenden, um Tests für das Spiel durchzuführen und somit sicherzustellen, dass es für die Veröffentlichung im Store vorbereitet ist. Falls Sie das Windows 10 SDK, das das Zertifizierungskit für Windows-Apps enthält, noch nicht heruntergeladen haben, rufen Sie [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) auf.

So erstellen Sie ein Paket, das in den Store hochgeladen werden kann:

1. Öffnen Sie Ihre Spielelösung in Visual Studio.
2. Navigieren Sie in Visual Studio zu __Projekt__ > __Store__ > __App-Pakete erstellen...__.
3. Wählen Sie für __Möchten Sie ein Paket zum Hochladen in den Windows Store erstellen?__ die Option __Ja__.
4. Melden Sie sich bei Ihrem Dev Center-Entwicklerkonto an. Oder [registrieren](https://developer.microsoft.com/store/register) Sie sich für ein Entwicklerkonto, falls Sie keins besitzen.
5. Wählen Sie eine App aus, für die das Uploadpaket erstellt werden soll. Falls Sie noch keine App-Übermittlung erstellt haben, geben Sie einen neuen App-Namen ein, um eine neue Übermittlung zu erstellen. Weitere Informationen finden Sie unter [Erstellen einer App durch Reservieren eines Namens](https://msdn.microsoft.com/windows/uwp/publish/create-your-app-by-reserving-a-name).
6. Nachdem das Paket erfolgreich erstellt wurde, klicken Sie auf __Zertifizierungskit für Windows-Apps starten__, um den Testprozess zu starten.
7. Beheben Sie mögliche Fehler, um ein Spielpaket zu erstellen.

#### Veröffentlichen des Spiels als ausgeblendet

1. Wechseln Sie zu [Dev Center](https://developer.microsoft.com/store), und melden Sie sich an.
2. Klicken Sie in der __Dashboardübersicht__ oder auf der Seite __Alle Apps__ auf die App, die Sie verwenden möchten. Falls Sie noch keine App-Übermittlung erstellt haben, klicken Sie auf __Neue App erstellen__, und reservieren Sie einen Namen.
3. Klicken Sie auf der Seite __App-Übersicht__ auf __Übermittlung starten__.
4. Konfigurieren Sie diese neue Übermittlung. Auf der Übermittlungsseite: 
    * Klicken Sie auf __Preise und Verfügbarkeit__. Wählen Sie im Abschnitt __Sichtbarkeit__ die Option __Diese App ausblenden und den Erwerb verhindern...__. Auf diese Weise stellen Sie sicher, dass Ihr Entwicklerteam Zugriff auf das Spiel hat. Weitere Informationen finden Sie unter [Verteilung und Sichtbarkeit](https://msdn.microsoft.com/windows/uwp/publish/set-app-pricing-and-availability#distribution-and-visibility).
    * Klicken Sie auf __Eigenschaften__. Wählen Sie im Abschnitt __Kategorie und Unterkategorie__ die Option __Spiele__ und anschließend eine geeignete Unterkategorie für Ihr Spiel aus.
    * Klicken Sie auf __Altersfreigaben__. Füllen Sie den Fragebogen ordnungsgemäß aus.
    * Klicken Sie auf __Pakete__. Laden Sie das zuvor erstellte Spielpaket hoch.
5. Befolgen Sie alle anderen Übermittlungsaufforderungen auf dem Dashboard, damit dieses Spiel veröffentlicht werden kann, dabei aber für die Öffentlichkeit ausgeblendet bleibt.
6. Klicken Sie auf __An Store übermitteln__.

Weitere Informationen finden Sie unter [App-Übermittlungen](https://msdn.microsoft.com/windows/uwp/publish/app-submissions).

Nachdem das Spiel an den Store übermittelt wurde, beginnt der [App-Zertifizierungsprozess](https://msdn.microsoft.com/windows/uwp/publish/the-app-certification-process). Dieser Prozess kann bis zu 16Stunden dauern, und das Spiel wird erst nach Abschluss des Prozesses aufgeführt.

#### Verknüpfen Ihrer Spielelösung mit dem Store

Bei in Visual Studio geöffneter Spielelösung:

1. Navigieren Sie zu __Projekt__ > __Store__ > __App mit Store verknüpfen...__.
2. Melden Sie sich bei Ihrem Dev Center-Entwicklerkonto an, und wählen Sie den App-Namen, dem diese Lösung zugeordnet werden soll.
3. Doppelklicken Sie auf die Datei __Package.appxmanifest.xml__, und wechseln Sie zur Registerkarte __Verpacken__, um zu überprüfen, ob das Spiel richtig zugeordnet wurde.

Wenn Sie die Lösung einem veröffentlichten Spiel zugeordnet haben, das im Store aufgeführt ist, verfügt Ihre Lösung über eine aktive Lizenz und Sie sind dem Erstellen von Add-Ons für Ihr Spiel einen Schritt näher. Weitere Informationen finden Sie unter [Verpacken von Apps](https://msdn.microsoft.com/windows/uwp/packaging/index).

#### Erstellen eines Add-Ons im Store

Stellen Sie beim Erstellen von Add-Ons sicher, dass Sie sie der richtigen Spieleübermittlung zuordnen. Ausführliche Informationen zum Konfigurieren aller Informationen für ein Add-On finden Sie unter [Add-On-Übermittlungen](https://msdn.microsoft.com/windows/uwp/publish/add-on-submissions).

1. Rufen Sie [Dev Center](https://developer.microsoft.com/store) auf, und melden Sie sich an.
2. Klicken Sie in der __Dashboardübersicht__ oder auf der Seite __Alle Apps__ auf die App, für die Sie das Add-On erstellen möchten.
3. Wählen Sie auf der Seite __App-Übersicht__ im Abschnitt __Add-Ons__ die Option __Neues Add-On erstellen__.
4. Wählen Sie den Produkttyp für das Add-On aus: __von Entwicklern verwaltete Verbrauchsartikel__, __vom Store verwalteter Verbrauchsartikel__ oder __Gebrauchsgut__.
5. Geben Sie eine eindeutige Produkt-ID ein, die beim Integrieren dieses Add-Ons in den Spielcode als Zeichenfolgenvariable verwendet wird. Diese ID ist für Kunden nicht sichtbar. Weitere Informationen finden Sie unter [Festlegen von Produkttyp und Produkt-ID für Apps](https://msdn.microsoft.com/windows/uwp/publish/set-your-add-on-product-id).

Weitere Konfigurationen für Add-Ons:
* [Eigenschaften](https://msdn.microsoft.com/windows/uwp/publish/enter-add-on-properties)
* [Preise und Verfügbarkeit](https://msdn.microsoft.com/windows/uwp/publish/set-add-on-pricing-and-availability)
* [Store-Eintrag](https://msdn.microsoft.com/windows/uwp/publish/create-add-on-store-listings)

Verfügt Ihr Spiel über viele Add-Ons, können Sie sie mithilfe der __Windows Store-Übermittlungs-API__ programmgesteuert erstellen. Weitere Informationen finden Sie unter [Erstellen und Verwalten von Übermittlungen mit WindowsStore-Diensten](https://msdn.microsoft.com/windows/uwp/monetize/create-and-manage-submissions-using-windows-store-services).

## Anzeigen von Werbung in Ihrem Spiel

Die Bibliotheken und Tools im Microsoft Store Services SDK unterstützen Sie beim Einrichten eines Diensts in Ihrem Spiel, über den Sie Anzeigen von einem Anzeigennetzwerk empfangen. Spielern werden Liveanzeigen angezeigt, und Sie erhalten Geld von den Inserenten, wenn Ihre Spieler die dargestellten Anzeigen ansehen oder mit ihnen interagieren. Weitere Informationen finden Sie unter [Workflows für das Erstellen von Apps mit Anzeigen](https://msdn.microsoft.com/windows/uwp/monetize/workflows-for-creating-apps-with-ads).

### Anzeigenformate

Mit dem Microsoft Store Services SDK können zwei Arten von Anzeigen angezeigt werden:

* Banneranzeigen: Anzeigen, die einen Teil des Spielbildschirms einnehmen und in der Regel in einem Spiel geschaltet werden.
* Videointerstitialanzeigen: Vollbildanzeigen, die sehr effektiv zwischen Leveln eingesetzt werden können. Werden Sie richtig implementiert, können Sie weniger störend als Banneranzeigen wirken.

### Welche Anzeigen werden angezeigt?

Bei Verwendung des Microsoft Store Services SDK werden Anzeigen derzeit über unsere Partnernetzwerke bereitgestellt. Weitere Informationen zu aktuellen Angeboten finden Sie unter [Monetisierung Ihrer App mit Anzeigen](https://developer.microsoft.com/store/monetize/ads-in-apps).
Wenn Sie AdControl zum Schalten von Anzeigen verwenden, können Sie die Anzeige von [Partneranzeigen](https://msdn.microsoft.com/windows/uwp/publish/about-affiliate-ads) aktivieren, indem Sie die in Ihrem Spiel dargestellten Produktanzeigen erweitern.

### Auf welchen Märkten ist die Schaltung von Anzeigen erlaubt?

Banneranzeigen und Videointerstitialanzeigen können Benutzern in ausgewählten Ländern angezeigt werden. Die vollständige Liste der Länder und Regionen, die Anzeigen unterstützen, finden Sie unter [Unterstützte Märkte für Microsoft Advertising](https://msdn.microsoft.com/windows/uwp/monetize/supported-markets-for-microsoft-advertising).

### APIs zum Einblenden von Anzeigen

Die Klassen [AdControl](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.adcontrol.aspx) und [InterstitialAd](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.interstitialad.aspx) im Microsoft Store Services SDK sind Teil des [Microsoft.Advertising.WinRT.UI](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.aspx)-Namespace und werden zum Einblenden von Anzeigen in Spielen verwendet.

Laden Sie zunächst mit Visual Studio 2015 das [Microsoft Store Services SDK](http://aka.ms/store-em-sdk) herunter, und installieren Sie es. Weitere Informationen finden Sie unter [Im SDK verfügbare Features](https://msdn.microsoft.com/windows/uwp/monetize/microsoft-store-services-sdk#features-available-in-the-sdk).

#### Implementierungshandbücher

In diesen exemplarischen Vorgehensweisen wird die Implementierung von Anzeigen mithilfe von __AdControl__ und __InterstitialAd__ veranschaulicht:

* [Erstellen von Banneranzeigen mithilfe der AdControl-Klasse in XAML und .NET](https://msdn.microsoft.com/windows/uwp/monetize/adcontrol-in-xaml-and--net)
* [Erstellen von Banneranzeigen mithilfe der AdControl-Klasse in HTML5 und JavaScript](https://msdn.microsoft.com/windows/uwp/monetize/adcontrol-in-html-5-and-javascript)
* [Erstellen von Videointerstitialanzeigen mithilfe der InterstitialAd-Klasse](https://msdn.microsoft.com/windows/uwp/monetize/interstitial-ads)

Sie können während der Entwicklung mit diesen Testwerten überprüfen, wie die Anzeigen gerendert werden. Dieselben Werte werden auch oben in den exemplarischen Vorgehensweisen verwendet.

|AdType             | AdUnitId  | AppId                              |
|-------------------|-----------|------------------------------------|
|Banneranzeigen         |10865270   |3f83fe91-d6be-434d-a0ae-7351c5a997f1|
|Interstitielle Anzeigen   |11389925   |d25517cb-12d4-4699-8bdc-52040c712cab|

Hier sind einige bewährte Methoden aufgeführt, die Sie beim Entwurfs- und Implementierungsprozess unterstützen.

* [Bewährte Methoden für Banneranzeigen unter Verwendung der AdControl-Klasse](https://msdn.microsoft.com/windows/uwp/monetize/ui-and-user-experience-guidelines)
* [Bewährte Methoden für interstitielle Anzeigen unter Verwendung der InterstitialAd-Klasse](https://msdn.microsoft.com/windows/uwp/monetize/ui-and-user-experience-guidelines#interstitialbestpractices10)

Wenn bei der Entwicklung Probleme auftreten, beispielsweise wenn Anzeigen nicht eingeblendet werden, die Blackbox blinkt und wieder verschwindet oder Anzeigen nicht aktualisiert werden, finden Sie Lösungen in den [Handbüchern zur Problembehandlung](https://msdn.microsoft.com/windows/uwp/monetize/troubleshooting-guides).

### Vorbereiten auf die Veröffentlichung durch Ersetzen der Testwerte für Anzeigeneinheiten

Wenn Sie bereit sind, mit Livetests fortzufahren oder Anzeigen in veröffentlichten Spielen zu empfangen, müssen Sie die Testwerte der Anzeigeneinheiten auf die tatsächlichen, für Ihr Spiel angegebenen Werte aktualisieren.
Informationen zum Erstellen von Anzeigeneinheiten für Ihr Spiel finden Sie unter [Einrichten von Anzeigeneinheiten in der App](https://msdn.microsoft.com/windows/uwp/monetize/set-up-ad-units-in-your-app).

### Weitere Anzeigennetzwerke

Hier sehen Sie weitere Anzeigennetzwerke, die die Schaltung von Anzeigen in UWP-Apps und -Spielen unterstützen.

#### Vungle

Das Vungle SDK für Windows bietet Videoanzeigen in Apps und Spielen. Das SDK können Sie unter [Vungle SDK](https://v.vungle.com/sdk) herunterladen.

#### Smaato

Smaato ermöglicht die Integration von Banneranzeigen in UWP-Apps und -Spiele. Laden Sie das [SDK](https://www.smaato.com/resources/sdks/) herunter. Weitere Informationen finden Sie in der [Dokumentation](https://wiki.smaato.com/display/SPX/Windows+Phone).

#### AdDuplex

Mit AdDuplex können Sie Banner- oder Interstitialanzeigen in Ihrem Spiel implementieren.

Weitere Informationen zum Integrieren von AdDuplex direkt in ein Windows10-XAML-Projekt finden Sie auf der AdDuplex-Website:
* Banneranzeigen: [Windows10 SDK für XAML](https://adduplex.zendesk.com/hc/en-us/articles/204849031-Windows-10-SDK-for-XAML-apps-installation-and-usage) 
* Interstitielle Anzeigen: [Windows 10 XAML AdDuplex Interstitial Ad Installation and Usage](https://adduplex.zendesk.com/hc/en-us/articles/204849091-Windows-10-XAML-AdDuplex-Interstitial-Ad-Installation-and-Usage) (Implementierung und Verwendung von AdDuplex-Interstitialanzeigen in Windows10-XAML-Projekten)

Informationen zum Integrieren des AdDuplex SDK in Windows10-UWP-Spiele, die mit Unity erstellt wurden, finden Sie unter [Windows 10 SDK for Unity apps installation and usage](https://adduplex.zendesk.com/hc/en-us/articles/207279435-Windows-10-SDK-for-Unity-apps-installation-and-usage) (Windows 10 SDK für Unity-Apps: Installation und Nutzung).

## Maximieren des Potenzials Ihres Spiels über Anzeigenkampagnen

Gehen Sie noch einen Schritt weiter, und bewerben Sie Ihr Spiel mithilfe von Anzeigen. Wenn Sie für Ihr Spiel eine [Anzeigenkampagne erstellen](https://msdn.microsoft.com/windows/uwp/publish/create-an-ad-campaign-for-your-app), zeigen anderen Apps und Spiele Werbung für Ihr Spiel an. 

Wählen Sie zwischen verschiedenen Kampagnenarten, mit denen Sie die Zahl von Spielern erhöhen können.

|Kampagnentyp             | Anzeigen für Ihr Spiel werden in folgenden Apps angezeigt:                                                                                                                                                                   |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|Kostenpflichtig                      |Apps, die dem Gerät oder der Kategorie Ihres Spiels entsprechen                                                                                                                                                   |
|Kostenlose Community-Anzeigen            |Apps, die von anderen Entwicklern veröffentlicht werden, die ebenfalls Community-Anzeigenkampagnen nutzen. Weitere Informationen finden Sie unter [Informationen zu Community-Anzeigen](https://msdn.microsoft.com/windows/uwp/publish/about-community-ads).|
|Kostenlose Eigenwerbung                |Nur in Apps, die Sie veröffentlicht haben. Weitere Informationen finden Sie unter [Über Eigenwerbung](https://msdn.microsoft.com/windows/uwp/publish/about-house-ads).                                                            |

## Verwandte Links

* [Bezahlung](https://msdn.microsoft.com/windows/uwp/publish/getting-paid-apps)
* [Kontotypen, Standorte und Gebühren](https://msdn.microsoft.com/windows/uwp/publish/account-types-locations-and-fees)
* [Analysen](https://msdn.microsoft.com/windows/uwp/publish/analytics)
* [Globalisierung und Lokalisierung](https://msdn.microsoft.com/windows/uwp/globalizing/globalizing-portal)
* [Implementieren einer Testversion Ihrer App](https://msdn.microsoft.com/windows/uwp/monetize/implement-a-trial-version-of-your-app)
* [Ausführen von Experimenten mit A/B-Tests](https://msdn.microsoft.com/windows/uwp/monetize/run-app-experiments-with-a-b-testing)


<!--HONumber=Nov16_HO1-->

