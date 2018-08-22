---
author: mathy
title: Geräteportal – HTTP-Monitor-API-Referenz
description: Erfahren Sie mehr über den Zugriff von HTTP-Datenverkehr aus der fokussierten App auf einer Xbox.
ms.localizationpriority: medium
ms.openlocfilehash: e7ce2ba75eb24f3963818935a7172b25114fd144
ms.sourcegitcommit: f9a4854b6aecfda472fb3f8b4a2d3b271b327800
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
ms.locfileid: "1397293"
---
# <a name="http-monitor-api-reference"></a>HTTP-Monitor-API-Referenz   
Sie können mit dieser API auf Echtzeit-HTTP-Datenverkehr für die fokussierte App zugreifen, wenn der HTTP-Monitor auf der Xbox-Konsole aktiviert wurde, indem Sie das Kontrollkästchen in Dev Home aktivieren.

## <a name="get-if-the-http-monitor-is-enabled"></a>Abrufen, ob der HTTP-Monitor aktiviert ist

**Anforderung**

Sie können abrufen, ob der HTTP-Monitor in Dev Home aktiviert wurde.

Methode      | Anforderungs-URI
:------     | :-----
GET | /ext/httpmonitor/sessions
<br />
**URI-Parameter**

- Keine

**Anforderungsheader**

- Keine

**Anforderungstext**

- Keine

**Antwort**   
Ein JSON-Objekt mit den folgenden Feldern:

* Aktiviert – (Bool) Ob der HTTP-Monitor auf der Xbox-Konsole aktiviert wurde, indem das Kontrollkästchen in Dev Home markiert wurde.

**Statuscode**

Diese API hat die folgenden erwarteten Statuscodes:

HTTP-Statuscode      | Beschreibung
:------     | :-----
200 | Die Anforderung war erfolgreich.
4XX | Fehlercodes
5XX | Fehlercodes

## <a name="get-http-traffic-from-the-focused-app"></a>Abrufen des HTTP-Datenverkehr aus der fokussierten App
**Anforderung**

Rufen Sie in Echtzeit HTTP-Datenverkehr von der fokussierten App auf der Xbox ab, sofern es keine System-App ist, wenn der HTTP-Monitor über Dev Home aktiviert wurde.

Methode      | Anforderungs-URI
:------     | :-----
Websocket | /ext/httpmonitor/sessions
<br />
**URI-Parameter**

- Keine

**Anforderungsheader**

- Keine

**Anforderungstext**

- Keine

**Antwort**   
Ein JSON-Objekt mit den folgenden Feldern:

* Sessions
    * RequestHeaders – (JSON-Objekt) Die Anforderungsheader aus der HTTP-Anforderung.
    * RequestContentHeaders – (JSON-Objekt) Die Anforderungsinhaltsheader aus der HTTP-Anforderung.
    * RequestURL - (Zeichenfolge) Die Anforderungs-URL.
    * RequestMethod – (Zeichenfolge) Die Anforderungsmethode.
    * RequestMessage – (Zeichenfolge) Die Anforderungsnachricht, unterstützt derzeit nur JSON- und Textinhalt.
    * ResponseHeaders – (JSON-Objekt) Die Antwortheader der HTTP-Antwort.
    * ResponseContentHeaders – (JSON-Objekt) Die Antwortinhaltsheader der HTTP-Antwort.
    * StatusCode – (Zahl) Der Antwortstatuscode.
    * ReasponsePhrase – (Zeichenfolge) Der Antwortgrundausdruck.
    * ResponseMessage – (Zeichenfolge) Die Antwortnachricht, unterstützt derzeit nur JSON- und Textinhalt.

**Statuscode**

Diese API hat die folgenden erwarteten Statuscodes:

HTTP-Statuscode      | Beschreibung
:------     | :-----
200 | Die Anforderung war erfolgreich.
4XX | Fehlercodes
403 | HTTP-Monitor ist deaktiviert, muss in Dev Home aktiviert werden.
5XX | Fehlercodes

<br />
**Verfügbare Gerätefamilien**

* Windows Xbox