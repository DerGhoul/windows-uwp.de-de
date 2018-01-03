---
author: laurenhughes
title: Signieren eines App-Pakets mit SignTool
description: Verwenden Sie SignTool, um ein App-Paket manuell mit einem Zertifikat zu signieren.
ms.author: lahugh
ms.date: 02/08/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Windows 10, UWP
ms.assetid: 171f332d-2a54-4c68-8aa0-52975d975fb1
ms.openlocfilehash: 5cbff0011a4a96c61d7f7bad7e57bd130e09c39b
ms.sourcegitcommit: 909d859a0f11981a8d1beac0da35f779786a6889
translationtype: HT
---
# <a name="sign-an-app-package-using-signtool"></a>Signieren eines App-Pakets mit SignTool

\[ Aktualisiert für UWP-Apps unter Windows10. Artikel zu Windows8.x finden Sie im [Archiv](http://go.microsoft.com/fwlink/p/?linkid=619132). \]

**SignTool** ist ein Befehlszeilentool, mit dem ein App-Paket oder -Bündel mit einem Zertifikat digital signiert wird. Das Zertifikat kann vom Benutzer (zu Testzwecken) erstellt oder von einem Unternehmen (für die Verteilung) ausgestellt sein. Die Signierung eines App-Pakets bietet dem Benutzer den Nachweis, dass die App-Daten nach der Signierung nicht geändert wurden, sowie die Bestätigung der Identität des Benutzers oder Unternehmens, die es signiert haben. **SignTool** kann verschlüsselte oder unverschlüsselte App-Pakete und -Bündel signieren.

> [!IMPORTANT] 
> Wenn Sie Visual Studio zum Entwickeln der App verwendet haben, wird empfohlen, dass Sie den Visual Studio-Assistenten zum Erstellen und Signieren des App-Pakets verwenden. Weitere Informationen finden Sie unter [Verpacken einer UWP-App mit Visual Studio](https://msdn.microsoft.com/windows/uwp/packaging/packaging-uwp-apps).

Weitere Informationen zur Codesignatur und zu Zertifikaten im Allgemeinen finden Sie unter [Einführung in die Codesignatur](https://msdn.microsoft.com/library/windows/desktop/aa380259.aspx#introduction_to_code_signing).

## <a name="prerequisites"></a>Voraussetzungen
- **Ein App-Paket**  
    Weitere Informationen über das manuelle Erstellen eines App-Pakets finden Sie unter [Erstellen eines App-Pakets mit dem Tool „MakeAppx.exe“](https://msdn.microsoft.com/windows/uwp/packaging/create-app-package-with-makeappx-tool). 

- **Ein gültiges Signaturzertifikat**  
    Weitere Informationen zum Erstellen oder Importieren ein gültiges Signaturzertifikats finden Sie unter [Erstellen oder Importieren eines Zertifikats für die Paketsignierung](https://msdn.microsoft.com/windows/uwp/packaging/create-certificate-package-signing).

- **SignTool.exe**  
    Abhängig vom Installationspfad des SDK befindet sich **SignTool** an folgenden Speicherorten auf Ihrem Windows10-PC:
    - x86: C:\Programme (x86)\Windows Kits\10\bin\x86\SignTool.exe
    - x64: C:\Programme (x86)\Windows Kits\10\bin\x64\SignTool.exe

## <a name="using-signtool"></a>Verwenden von SignTool

**SignTool** kann zum Signieren von Dateien, Überprüfen von Signaturen oder Zeitstempeln, Entfernen von Signaturen und mehr verwendet werden. Um ein App-Paket zu signieren, benötigen Sie den Befehl **sign**. Vollständige Informationen zu **SignTool** finden Sie auf der [SignTool](https://msdn.microsoft.com/library/windows/desktop/aa387764.aspx)-Referenzseite. 

### <a name="determine-the-hash-algorithm"></a>Ermitteln des Hashalgorithmus
Wenn Sie mit **SignTool** Ihr App-Paket oder -Bündel signieren, muss der in **SignTool** verwendete Hashalgorithmus derselbe Algorithmus sein, den Sie beim Packen Ihre App verwendet haben. Wenn Sie z.B. **MakeAppx.exe** verwendet haben, um Ihr App-Paket mit den Standardeinstellungen zu erstellen, müssen Sie SHA256 in **SignTool** angeben, da das der von **MakeAppx.exe** verwendete Standardalgorithmus ist.

Um herauszufinden, welcher Hashalgorithmus beim Packen einer App verwendet wurde, extrahieren Sie den Inhalt des App-Pakets und überprüfen die Datei AppxBlockMap.xml. Weitere Informationen zum Entpacken/Extrahieren eines App-Pakets finden Sie unter [Extrahieren von Dateien aus einem Paket oder Bündel](https://msdn.microsoft.com/windows/uwp/packaging/create-app-package-with-makeappx-tool#extract-files-from-a-package-or-bundle). Die Hashmethode befindet sich im BlockMap-Element und besitzt dieses Format:
```
<BlockMap xmlns="http://schemas.microsoft.com/appx/2010/blockmap" 
HashMethod="http://www.w3.org/2001/04/xmlenc#sha256">
```

Die folgende Tabelle enthält alle HashMethod-Werte und den entsprechenden Hashalgorithmus:
| HashMethod-Wert                              | Hashalgorithmus |
|-----------------------------------------------|----------------|
| http://www.w3.org/2001/04/xmlenc#sha256       | SHA256         |
| http://www.w3.org/2001/04/xmldsig-more#sha384 | SHA384         |
| http://www.w3.org/2001/04/xmlenc#sha512       | SHA512         |

> **Hinweis** Da der Standardalgorithmus von **SignTool** SHA1 ist (nicht verfügbar in **MakeAppx.exe**), müssen Sie immer einen Hashalgorithmus angeben, wenn Sie **SignTool** verwenden.

### <a name="sign-the-app-package"></a>Signieren des App-Pakets

Wenn Sie über alle benötigten Voraussetzungen verfügen und festgestellt haben, welcher Hashalgorithmus beim Packen der App verwendet wurde, können Sie mit dem Signieren der App beginnen. 

Die allgemeine Befehlszeilensyntax für die Paketsignierung mit **SignTool** lautet:
```
SignTool sign [options] <filename(s)>
```

Das Zertifikat zum Signieren Ihrer App muss entweder eine PFX-Datei sein oder in einem Zertifikatspeicher installiert sein.

Um Ihr App-Paket mit einem Zertifikat aus einer PFX-Datei zu signieren, verwenden Sie die folgende Syntax:
```
SignTool sign /fd <Hash Algorithm> /a /f <Path to Certificate>.pfx /p <Your Password> <File path>.appx
```
Beachten Sie, dass **SignTool** mit der Option `/a` automatisch das beste Zertifikat auswählt.

Wenn das Zertifikat keine PFX-Datei ist, verwenden Sie die folgende Syntax:
```
SignTool sign /fd <Hash Algorithm> /n <Name of Certificate> <File Path>.appx
```

Alternativ können Sie den SHA1-Hash des gewünschten Zertifikats anstelle von &lt;Name of Certificate&gt; mit der folgenden Syntax angeben:
```
SignTool sign /fd <Hash Algorithm> /sha1 <SHA1 hash> <File Path>.appx
```

Beachten Sie, dass einige Zertifikate kein Kennwort verwenden. Wenn Ihr Zertifikat über kein Kennwort verfügt, geben Sie „/p &lt;Your Password&gt;” in der Beispielbefehle nicht an.

Wenn Ihr App-Paket mit einem gültigen Zertifikat signiert ist, können Sie das Paket in den Store hochladen. Weitere Informationen zum Hochladen und Übermitteln von Apps an den Store finden Sie unter [App-Übermittlungen](https://msdn.microsoft.com/windows/uwp/publish/app-submissions).

## <a name="common-errors-and-troubleshooting"></a>Häufige Fehler und Problembehandlung
Die häufigsten Fehlertypen bei der Verwendung von **SignTool** sind interne Fehler, die in der Regel wie folgt aussehen:

```
SignTool Error: An unexpected internal error has occurred.
Error information: "Error: SignerSign() failed." (-2147024885 / 0x8007000B) 
```

Wenn der Fehlercode mit 0x8008 beginnt, z.B. 0x80080206 (APPX_E_CORRUPT_CONTENT), ist das Paket, das gerade signiert wird, nicht gültig. Wenn Sie diesen Fehlertyp erhalten, müssen Sie das Paket neu erstellen und **SignTool** erneut ausführen.

**SignTool** verfügt über eine Debugoption, um Zertifikatfehler anzuzeigen und zu filtern. Um die Debugfunktion zu verwenden, geben Sie die Option `/debug` direkt hinter `sign` und dann den vollständigen **SignTool**-Befehl an.
```
SignTool sign /debug [options]
``` 

Ein allgemeinerer Fehler ist 0x8007000B. Zu diesem Fehlertyp finden Sie weitere Informationen im Ereignisprotokoll.
 
So suchen Sie weitere Informationen im Ereignisprotokoll
- Führen Sie Eventvwr.msc aus.
- Öffnen Sie das Ereignisprotokoll: Ereignisanzeige (Lokal) -> Anwendungs- und Dienstprotokolle -> Microsoft -> Windows--> AppxPackagingOM -> Microsoft-Windows-AppxPackaging/Operational.
- Suchen Sie das letzte Fehlerereignis.

Der interne Fehler 0x8007000B entspricht in der Regel einem der folgenden Werte:

| **Ereignis-ID** | **Beispiel der Ereigniszeichenfolge** | **Vorschlag** |
|--------------|--------------------------|----------------|
| 150          | Fehler 0x8007000B: Der Name des Herausgebers des App-Manifests (CN=Contoso) muss mit dem Namen des Antragstellers des Signaturzertifikats (CN=Contoso, C=US) übereinstimmen. | Der Name des Herausgebers des App-Manifests muss exakt mit dem Namen des Antragstellers der Signatur übereinstimmen.               |
| 151          | Fehler 0x8007000B: Die angegebene Hashmethode der Signatur (SHA512) muss mit der Hashmethode, die in der App-Paketblockzuordnung (SHA256) verwendet wurde, übereinstimmen.     | Der im Parameter /fd angegebene Hashalgorithmus ist falsch. Führen Sie **SignTool** erneut mit dem Hashalgorithmus aus, der mit der App-Paketblockzuordnung übereinstimmt (mit dem das App-Paket erstellt wurde).  |
| 152          | Fehler 0x8007000B: Der Inhalt des App-Pakets muss für die Blockzuordnung gültig sein.                                                           | Das App-Paket ist beschädigt und muss neu erstellt werden, um eine neue Blockzuordnung zu generieren. Weitere Informationen zum Erstellen eines App-Pakets finden Sie unter [Erstellen eines App-Pakets mit dem Tool „MakeAppx.exe“](https://msdn.microsoft.com/windows/uwp/packaging/create-app-package-with-makeappx-tool). |