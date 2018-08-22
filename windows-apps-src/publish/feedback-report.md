---
author: jnHs
Description: The Feedback report in the Windows Dev Center dashboard lets you see the problems, suggestions, and upvotes that your Windows 10 customers have submitted through Feedback Hub.
title: Feedbackbericht
ms.assetid: 9EA8B456-CA57-40CE-A55B-7BFDC55CA8A8
ms.author: wdg-dev-content
ms.date: 11/3/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows10, UWP
ms.localizationpriority: medium
ms.openlocfilehash: bceb1d2cc6682698d0ad06ed4b1865f3d6510442
ms.sourcegitcommit: f2f4820dd2026f1b47a2b1bf2bc89d7220a79c1a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2018
ms.locfileid: "2799491"
---
# <a name="feedback-report"></a>Feedbackbericht

Im **Feedback-Bericht** im Windows Dev Center-Dashboard werden die Probleme, Vorschläge und Zustimmungen angezeigt, die Ihre Windows 10-Kunden über den Feedback-Hub übermittelt haben. Sie können diese Informationen in Ihrem Dashboard anzeigen oder die Daten exportieren, um sie offline anzuzeigen.

> [!NOTE]
> Sie können über diesen Bericht auch [direkt auf Feedback reagieren](respond-to-customer-feedback.md), um Kunden zu signalisieren, dass Sie ihr Feedback ernst nehmen.

Ermuntern Sie Ihre Kunden, Ihnen Feedback zu Ihrer App zu geben. Dies ist eine hervorragende Möglichkeit, um mehr über die Probleme und Funktionen zu erfahren, die ihnen besonders wichtig sind. Wenn Ihre Kunden wissen, dass sie Ihnen ihr Feedback direkt senden können, geben sie mit höherer Wahrscheinlichkeit keine negative Bewertung im Store ab.

Verwenden Sie die Feedback-API im [Microsoft Store Services SDK](http://aka.ms/store-em-sdk), um es Ihren Kunden zu ermöglichen, den [Feedback-Hub direkt aus Ihrer App heraus zu starten](../monetize/launch-feedback-hub-from-your-app.md). Bedenken Sie, dass jeder Kunde, der Ihre App auf einem Windows 10-Gerät heruntergeladen hat, das den Feedback-Hub unterstützt, mithilfe der Feedback-Hub-App ein Feedback abgeben kann. Aus diesem Grund möglicherweise Feedback von Kunden in diesem Bericht angezeigt werden, selbst wenn Sie nicht speziell für Feedback von Ihrer App gebeten haben.

Feedback ist ebenfalls wertvoll, wenn Sie [Flight-Pakete](package-flights.md) verwenden, da im Feedbackbericht das spezifische Paket aufgeführt wird, das auf dem Gerät des jeweiligen Kunden installiert war, als er das Feedback abgegeben hat.

> [!TIP]
> Für einen schnellen Blick auf Berichte, Bewertungen und Feedback der Benutzer über alle Ihre apps in den letzten 30 Tagen, erweitern Sie im linken Navigationsbereich Menü **einbeziehen** , und wählen **Bewertungen und Feedback.** 


## <a name="apply-filters"></a>Anwenden von Filtern

Im oberen Bereich der Seite können Sie den Zeitraum auswählen, für den die Daten angezeigt werden sollen. Die Standardeinstellung ist **Lebensdauer**, aber Sie können festlegen, ob die Daten für 30Tage, 3Monate, 6 oder 12Monate angezeigt werden sollen.

Sie können ebenfalls **Filter** erweitern, um alle Daten auf dieser Seite mit den folgenden Optionen zu filtern.

- **Feedbacktyp**: Die Standardeinstellung ist **Alle**. Sie können **Problem** oder **Vorschlag** auswählen, um nur diese Art von Feedback anzuzeigen.
- **Gerätetyp**: Die Standardeinstellung ist **Alle Geräte**. Sie können einen bestimmten Gerätetyp auswählen, wenn auf dieser Seite nur Feedback von Kunden angezeigt werden sollen, die ein Gerät dieses Typs verwenden.
- **Paketversion**: Die Standardeinstellung ist **Alle Pakete**. Sie können eines Ihrer Pakete auswählen, damit nur Feedback von Kunden angezeigt wird, die dieses Paket verwendet haben, als sie ihr Feedback abgegeben haben.
- **Markt**: Die Standardeinstellung ist **Alle Märkte**. Sie können einen bestimmten Markt auswählen, um nur Feedback von den in diesem Markt ansässigen Kunden anzuzeigen.
- **Gruppe**: Die Standardeinstellung ist **Alle**. Sie können festlegen, dass nur das Feedback angezeigt werden soll, das [Windows-Insider](http://insider.windows.com) abgeben.

> [!TIP]
> Wenn auf der Seite kein Feedback zu sehen ist, stellen Sie sicher, dass Sie mit Ihrer Filterauswahl nicht sämtliches Feedback ausgeschlossen haben. Wenn Sie z. B. nach einem **Gerätetyp** filtern, der von Ihrer App nicht unterstützt wird, wird kein Feedback angezeigt.


## <a name="viewing-feedback-details"></a>Anzeigen von Feedbackdetails

Im Bericht finden Sie das jeweilige Feedback von Ihren Kunden. Links neben dem Feedbacktext jedes Elements wird angezeigt, wie oft das Feedback von anderen Kunden im Feedback-Hub bewertet wurde. Sie können das Feedback auf drei Arten sortieren:

- **Zustimmung** (Standard): Zeigt Feedback, das von anderen Kunden bewertet wurde, beginnend mit dem Feedback, das die meisten Zustimmungen erhalten hat.
- **Populär**: Zeigt Feedback, das von anderen Kunden in den letzten sieben Tagen bewertet wurde, beginnend mit dem Feedback, das die letzte Aktivität aufweist.
- **Aktuellste**: Zeigt sämtliches Feedback, beginnend mit dem zuletzt abgegebenen Feedback an.

Neben jedem Kommentar werden der Typ des Feedbacks sowie das Datum angezeigt, an dem das Feedback abgegeben wurde. Sie werden auch der Kunde Land/Ihrer Region, die bestimmte Paket sehen, die auf dem Gerät installiert wurde, den sie verwenden würde, wenn sie das Feedback und den Typ des, Gerät, und klicken Sie auf **Windows-Insider** gelassen, senden Sie Feedback von Kunden ist ein Mitglied der Windows-Insider Programm.

Hier sehen Sie auch eine Option, um auf das [Feedback zu antworten](respond-to-customer-feedback.md).


## <a name="translating-feedback"></a>Übersetzen von Feedback

Standardmäßig wird für Sie Feedback, die nicht in Ihrer bevorzugten Sprache geschrieben wurde übersetzt. Falls gewünscht, können Sie die Übersetzung von Feedback deaktivieren, indem Sie das Kontrollkästchen **Feedback übersetzen** neben der Seitenfilter deaktivieren.

Da das Feedback durch ein automatisches Übersetzungssystem übersetzt wird, sind die resultierenden Übersetzungen u. U. nicht immer exakt. Für den Fall, dass sie ihn mit der Übersetzung vergleichen oder auf andere Weise übersetzen lassen möchten, steht der Originaltext zur Verfügung.


## <a name="launching-feedback-hub-directly-from-your-app"></a>Starten des Feedback-Hubs direkt in der App

Wie bereits erwähnt, wird empfohlen, direkt in Ihrer App einen Link zum Feedback-Hub einzufügen, um die Benutzer zu ermuntern, Feedback abzugeben. Weitere Informationen finden Sie unter [Feedback-Hub in Ihrer App starten](../monetize/launch-feedback-hub-from-your-app.md).