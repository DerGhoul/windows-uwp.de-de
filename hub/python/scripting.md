---
title: Skripterstellung und Automatisierung mit Python unter Windows
description: Erfahren Sie mehr über die ersten Schritte bei der Verwendung von Python für die Skripterstellung, Automatisierung und Systemverwaltung unter Windows.
author: mattwojo
ms.author: mattwoj
manager: jken
ms.topic: article
keywords: python, Windows 10, Microsoft, python-Systemverwaltung, python-Datei Automatisierung, python-Skripts unter Windows, Einrichten von Python unter Windows, python-Entwicklerumgebung unter Windows, python-Entwicklungsumgebung unter Windows, Python mit PowerShell, python-Skripts für Dateisystem Tasks
ms.localizationpriority: medium
ms.date: 07/19/2019
ms.openlocfilehash: 3f8a17de8121fed27e69442d5560f702a04c8e42
ms.sourcegitcommit: 13faf9dab9946295986f8edd79b5fae0db4ed0f6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/15/2019
ms.locfileid: "72314864"
---
# <a name="get-started-using-python-on-windows-for-scripting-and-automation"></a>Einstieg in die Verwendung von Python unter Windows für die Skripterstellung und Automatisierung

Im folgenden finden Sie eine Schritt-für-Schritt-Anleitung für das Einrichten Ihrer Entwicklerumgebung und den Einstieg in die Verwendung von Python für die Skripterstellung und Automatisierung von Dateisystem Vorgängen unter Windows.

> [!NOTE]
> In diesem Artikel wird beschrieben, wie Sie Ihre Umgebung einrichten, um einige der nützlichen Bibliotheken in Python zu verwenden, die Aufgaben plattformübergreifend automatisieren können, wie z. b. das Durchsuchen des Dateisystems, das Zugreifen auf das Internet, das Auswerten von Dateitypen usw., von einem Windows-zentrierten Informationen zu Windows-spezifischen Vorgängen finden Sie unter [ctypes](https://docs.python.org/3/library/ctypes.html), eine C-kompatible fremd Funktionsbibliothek für python, [winreg](https://docs.python.org/3/library/winreg.html), Funktionen, die die Windows-Registrierungs-API für python und [python/WinRT](https://pypi.org/project/winrt/)verfügbar machen, sodass der Zugriff Windows-Runtime APIs von Thon.

## <a name="set-up-your-development-environment"></a>Einrichten der Entwicklungsumgebung

Wenn Sie python zum Schreiben von Skripts verwenden, die Dateisystem Vorgänge ausführen, wird empfohlen, [python über den Microsoft Store zu installieren](https://www.microsoft.com/en-us/p/python-37/9nj46sx7x90p?activetab=pivot:overviewtab). Bei der Installation über das Microsoft Store wird der grundlegende Python3-Interpreter verwendet. es werden jedoch die Pfad Einstellungen für den aktuellen Benutzer eingerichtet (wodurch kein Administrator Zugriff erforderlich ist) und automatische Updates bereitgestellt.

Wenn Sie python für die **Webentwicklung** unter Windows verwenden, empfehlen wir eine andere Einrichtung mithilfe des Windows-Subsystems für Linux. Eine exemplarische Vorgehensweise finden Sie in unserem Handbuch: [Beginnen Sie mit der Verwendung von Python für die Webentwicklung unter Windows](./web-frameworks.md). Wenn Sie noch nicht mit python vertraut sind, testen Sie unser Handbuch: [Beginnen Sie mit der Verwendung von Python unter Windows für Einsteiger](./beginners.md). Für einige erweiterte Szenarien (z. b. die Notwendigkeit, auf installierte Dateien von python zuzugreifen oder diese zu ändern, Kopien von Binärdateien zu erstellen oder python-DLLs direkt zu verwenden), empfiehlt es sich, eine bestimmte Python-Version direkt von [python.org](https://www.python.org/downloads/) herunterzuladen oder die Installation von eine [Alternative](https://www.python.org/download/alternatives), wie z. b. Anaconda, jython, pypy, winpython, IronPython usw. Dies wird nur empfohlen, wenn Sie ein fortschrittlicher python-Programmierer mit einem bestimmten Grund für die Auswahl einer alternativen Implementierung sind.

## <a name="install-python"></a>Installieren von python

So installieren Sie python mithilfe der Microsoft Store:

1. Wechseln Sie zu Ihrem **Startmenü** (unten links Windows-Symbol), geben Sie "Microsoft Store" ein, und wählen Sie den Link zum Öffnen des Stores aus.

2. Nachdem der Speicher geöffnet ist, wählen Sie im Menü oben rechts die Option **Suchen** aus, und geben Sie "python" ein. Öffnen Sie "Python 3,7" in den Ergebnissen unter apps. Wählen Sie **Get**aus.

3. Nachdem python den Download-und Installationsprozess abgeschlossen hat, öffnen Sie Windows PowerShell über das **Startmenü** (unten links Windows-Symbol). Nachdem PowerShell geöffnet ist, geben Sie `Python --version` ein, um zu bestätigen, dass Python3 auf Ihrem Computer installiert wurde.

4. Die Microsoft Store Installation von python umfasst **PIP**, den Standardpaket-Manager. PIP ermöglicht Ihnen, zusätzliche Pakete zu installieren und zu verwalten, die nicht Teil der python-Standardbibliothek sind. Geben Sie `pip --version` ein, um zu bestätigen, dass Sie auch PIP zum Installieren und Verwalten von Paketen zur Verfügung haben.

## <a name="install-visual-studio-code"></a>Installieren von Visual Studio Code

Wenn Sie vs Code als Text-Editor/integrierte Entwicklungsumgebung (Integrated Development Environment, IDE) verwenden, können Sie [IntelliSense](https://code.visualstudio.com/docs/editor/intellisense) (eine Code Vervollständigungs Hilfe), [linting](https://code.visualstudio.com/docs/python/linting) (hilft, Fehler in Ihrem Code zu vermeiden) und [Debugunterstützung](https://code.visualstudio.com/docs/python/debugging) nutzen (hilft beim Auffinden von Fehlern in Ihren Code nach dem Ausführen), [Code Ausschnitte](https://code.visualstudio.com/docs/editor/userdefinedsnippets) (Vorlagen für kleine wiederverwendbare Code Blöcke) und Komponenten [Tests](https://code.visualstudio.com/docs/python/unit-testing) (Testen Sie die Schnittstelle Ihres Codes mit verschiedenen Eingabetypen).

Laden Sie vs Code für Windows herunter, und befolgen Sie die Installationsanweisungen: [https://code.visualstudio.com](https://code.visualstudio.com).

## <a name="install-the-microsoft-python-extension"></a>Installieren der Microsoft python-Erweiterung

Sie müssen die Microsoft python-Erweiterung installieren, um die Features für die vs Code-Unterstützung nutzen zu können. [Weitere Informationen](https://code.visualstudio.com/docs/languages/python).

1. Öffnen Sie das Fenster vs Code Erweiterungen, indem Sie **STRG + UMSCHALT + X** eingeben (oder verwenden Sie das Menü, um zu **Ansicht** > -**Erweiterungen**zu navigieren).

2. Geben Sie im Feld Top **Search Extensions in Marketplace** Folgendes ein:  **Python**.

3. Suchen Sie die **python-Erweiterung (MS-python. python) nach Microsoft** , und wählen Sie die grüne Schaltfläche **Installieren** aus.

## <a name="open-the-integrated-powershell-terminal-in-vs-code"></a>Öffnen Sie das integrierte PowerShell-Terminal in vs Code

VS Code enthält ein [integriertes Terminal](https://code.visualstudio.com/docs/editor/integrated-terminal) , mit dem Sie eine python-Befehlszeile mit PowerShell öffnen und einen nahtlosen Workflow zwischen dem Code-Editor und der Befehlszeile einrichten können.

1. Öffnen Sie das Terminal in vs Code, wählen Sie  > -**Terminal** **anzeigen**aus, oder verwenden Sie alternativ die Tastenkombination **Strg + "** (mit dem Graviszeichen-Zeichen).

    > [!NOTE]
    > Das Standardterminal sollte PowerShell lauten. Wenn Sie es jedoch ändern müssen, verwenden Sie **STRG + UMSCHALT + P** , um die Befehls-Pallette einzugeben. Geben Sie **terminal ein: Wählen Sie Standardshell @ no__t-0 aus, und eine Liste der Terminal Optionen wird mit PowerShell, Eingabeaufforderung, WSL usw. angezeigt. Wählen Sie das gewünschte, das Sie verwenden möchten, und drücken Sie **STRG + UMSCHALT + "** (mit dem Backtick), um ein neues Terminal zu erstellen.

2. Öffnen Sie in Ihrem vs Code Terminal python, indem Sie Folgendes eingeben: `python`

3. Probieren Sie den Python-Interpreter aus, indem Sie Folgendes eingeben: `print("Hello World")`. Python gibt Ihre Anweisung "Hallo Welt" zurück.

    ![Python-Befehlszeile in vs Code](../images/python-in-vscode.png)

4. Um Python zu beenden, geben Sie `exit()`, `quit()` ein, oder wählen Sie STRG + Z aus.

## <a name="install-git-optional"></a>Installieren von git (optional)

Wenn Sie beabsichtigen, mit anderen in Ihrem Python-Code zusammenzuarbeiten oder das Projekt auf einem Open-Source-Standort (wie GitHub) zu hosten, unterstützt vs Code die [Versionskontrolle mit git](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support). Auf der Registerkarte Quell Code Verwaltung in vs Code werden alle Änderungen nachverfolgt, und es werden allgemeine git-Befehle (Add, Commit, Push, Pull) direkt in die Benutzeroberfläche integriert. Sie müssen zuerst git installieren, um die Quell Code Verwaltung zu über schalten.

1. Laden Sie git für Windows von [der git-SCM-Website](https://git-scm.com/download/win)herunter, und installieren Sie es.

2. Ein Installations-Assistent ist enthalten, mit dem Sie eine Reihe von Fragen zu den Einstellungen für die git-Installation erhalten. Es wird empfohlen, alle Standardeinstellungen zu verwenden, es sei denn, Sie haben einen bestimmten Grund, etwas zu ändern.

3. Wenn Sie noch nie mit git gearbeitet haben, können Ihnen [GitHub-Leitfäden](https://guides.github.com/) beim Einstieg helfen.

## <a name="example-script-to-display-the-structure-of-your-file-system-directory"></a>Beispielskript zum Anzeigen der Struktur des Dateisystem Verzeichnisses

Allgemeine Systemverwaltungsaufgaben können sehr lange dauern, aber mit einem Python-Skript können Sie diese Aufgaben automatisieren, sodass Sie überhaupt keine Zeit benötigen. Python kann z. b. den Inhalt des Dateisystems Ihres Computers lesen und Vorgänge wie das Drucken eines Gliederung Ihrer Dateien und Verzeichnisse, das Verschieben von Ordnern von einem Verzeichnis in ein anderes oder das Umbenennen von Hunderten von Dateien durchführen. Normalerweise können solche Aufgaben einige Zeit in Anspruch nehmen, wenn Sie Sie manuell ausführen würden. Verwenden Sie stattdessen ein Python-Skript.

Beginnen wir mit einem einfachen Skript, das eine Verzeichnisstruktur durchläuft und die Verzeichnisstruktur anzeigt.

1. Öffnen Sie PowerShell über das **Startmenü** (unten links Windows-Symbol).

2. Erstellen Sie ein Verzeichnis für Ihr Projekt: `mkdir python-scripts`, und öffnen Sie dann das Verzeichnis: `cd python-scripts`.

3. Erstellen Sie einige Verzeichnisse, die mit unserem Beispielskript verwendet werden:

    ```powershell
    mkdir food, food\fruits, food\fruits\apples, food\fruits\oranges, food\vegetables
    ```

4. Erstellen Sie einige Dateien in diesen Verzeichnissen, die mit unserem Skript verwendet werden sollen:

    ```powershell
    new-item food\fruits\banana.txt, food\fruits\strawberry.txt, food\fruits\blueberry.txt, food\fruits\apples\honeycrisp.txt, food\fruits\oranges\mandarin.txt, food\vegetables\carrot.txt
    ```

5. Erstellen Sie eine neue python-Datei in Ihrem python-Scripts-Verzeichnis:

    ```powershell
    mkdir src
    new-item src\list-directory-contents.py
    ```

6. Öffnen Sie das Projekt in vs Code, indem Sie Folgendes eingeben: `code .`

7. Öffnen Sie das Fenster vs Code Datei-Explorer, indem Sie **STRG + UMSCHALT + E** drücken (oder über das Menü zu **Ansicht** > -**Explorer**navigieren) und die soeben erstellte List-Directory-Contents.py-Datei auswählen. Die Microsoft python-Erweiterung lädt automatisch einen Python-Interpreter. Sie können sehen, welcher Interpreter am unteren Rand des vs Code Fensters geladen wurde.

    > [!NOTE]
    > Python ist eine interpretierte Sprache, d. h., Sie fungiert als virtueller Computer und emuttet einen physischen Computer. Es gibt verschiedene Arten von python-Interpretern, die Sie verwenden können: Python 2, Python 3, Anaconda, pypy usw. Zum Ausführen von Python-Code und zum Herunterladen von python IntelliSense müssen Sie vs Code, welcher Interpreter verwendet werden soll. Es wird empfohlen, den Interpreter, den vs Code standardmäßig auswählt (in unserem Fall python 3), zu halten, es sei denn, Sie haben einen bestimmten Grund für die Auswahl etwas anderes. Um den Python-Interpreter zu ändern, wählen Sie den Interpreter, der derzeit in der blauen Leiste am unteren Rand des vs Code Fensters angezeigt wird, oder öffnen Sie die **Befehls Palette** (STRG + UMSCHALT + P), und geben Sie den Befehl **python ein: Wählen Sie Interpreter @ no__t-0 aus. Dadurch wird eine Liste der derzeit installierten Python-Interpreter angezeigt. [Erfahren Sie mehr über das Konfigurieren von python-Umgebungen](https://code.visualstudio.com/docs/python/environments).

    ![Python-Interpreter in vs Code auswählen](../images/interpreterselection.gif)

8. Fügen Sie den folgenden Code in die List-Directory-Contents.py-Datei ein, und wählen Sie dann **Speichern**aus:

    ```python
    import os

    root = os.path.join('..', 'food')
    for directory, subdir_list, file_list in os.walk(root):
        print('Directory:', directory)
        for name in subdir_list:
            print('Subdirectory:', name)
        for name in file_list:
            print('File:', name)
        print()
    ```

9. Öffnen Sie das vs Code integrierte Terminal (**Strg + "** , verwenden Sie das Graviszeichen-Zeichen), und geben Sie das Verzeichnis src ein, in dem Sie soeben das Python-Skript gespeichert haben:

    ```powershell
    cd src
    ```

10. Führen Sie das Skript in PowerShell mit folgenden Aktionen aus:

    ```powershell
    python3 .\list-directory-contents.py
    ```

    Daraufhin sollte eine Ausgabe angezeigt werden, die wie folgt aussieht:

    ```powershell
    Directory: ..\food
    Subdirectory: fruits
    Subdirectory: vegetables

    Directory: ..\food\fruits
    Subdirectory: apples
    Subdirectory: oranges
    File: banana.txt
    File: blueberry.txt
    File: strawberry.txt

    Directory: ..\food\fruits\apples
    File: honeycrisp.txt

    Directory: ..\food\fruits\oranges
    File: mandarin.txt

    Directory: ..\food\vegetables
    File: carrot.txt
    ```

11. Verwenden Sie Python, um die Ausgabe des Dateisystem Verzeichnisses in der eigenen Textdatei auszugeben, indem Sie diesen Befehl direkt in Ihrem PowerShell-Terminal eingeben: `python3 list-directory-contents.py > food-directory.txt`

Herzlichen Glückwunsch! Sie haben soeben ein automatisiertes System Verwaltungs Skript geschrieben, das die erstellten Verzeichnisse und Dateien liest und python zum Anzeigen und anschließenden Ausdrucken der Verzeichnisstruktur in der eigenen Textdatei verwendet.

## <a name="example-script-to-modify-all-files-in-a-directory"></a>Beispielskript zum Ändern aller Dateien in einem Verzeichnis

In diesem Beispiel werden die Dateien und Verzeichnisse verwendet, die Sie soeben erstellt haben. dabei wird jede der Dateien umbenennen, indem das Datum der letzten Änderung am Anfang des Datei namens hinzugefügt wird.

1. Erstellen Sie im Ordner **src** in Ihrem **python-Scripts-** Verzeichnis eine neue python-Datei für das Skript:

    ```powershell
    new-item update-filenames.py
    ```

2. Öffnen Sie die Datei Update-filenames.py, fügen Sie den folgenden Code in die Datei ein, und speichern Sie Sie:

    > [!NOTE]
    > OS. getmtime gibt einen Zeitstempel in Ticks zurück, der nicht leicht lesbar ist. Er muss zuerst in eine standardmäßige DateTime-Zeichenfolge konvertiert werden.

    ```python
    import datetime
    import os

    root = os.path.join('..', 'food')
    for directory, subdir_list, file_list in os.walk(root):
        for name in file_list:
            source_name = os.path.join(directory, name)
            timestamp = os.path.getmtime(source_name)
            modified_date = str(datetime.datetime.fromtimestamp(timestamp)).replace(':', '.')
            target_name = os.path.join(directory, f'{modified_date}_{name}')

            print(f'Renaming: {source_name} to: {target_name}')

            os.rename(source_name, target_name)
    ```

3. Testen Sie das Update-filenames.py-Skript, indem Sie es ausführen: `python3 update-filenames.py`, und führen Sie dann das List-Directory-Contents.py-Skript erneut aus: `python3 list-directory-contents.py`

4. Daraufhin sollte eine Ausgabe angezeigt werden, die wie folgt aussieht:

    ```powershell
    Renaming: ..\food\fruits\banana.txt to: ..\food\fruits\2019-07-18 12.24.46.385185_banana.txt
    Renaming: ..\food\fruits\blueberry.txt to: ..\food\fruits\2019-07-18 12.24.46.391170_blueberry.txt
    Renaming: ..\food\fruits\strawberry.txt to: ..\food\fruits\2019-07-18 12.24.46.389174_strawberry.txt
    Renaming: ..\food\fruits\apples\honeycrisp.txt to: ..\food\fruits\apples\2019-07-18 12.24.46.395160_honeycrisp.txt
    Renaming: ..\food\fruits\oranges\mandarin.txt to: ..\food\fruits\oranges\2019-07-18 12.24.46.398151_mandarin.txt
    Renaming: ..\food\vegetables\carrot.txt to: ..\food\vegetables\2019-07-18 12.24.46.402496_carrot.txt

    PS C:\src\python-scripting\src> python3 .\list-directory-contents.py
    ..\food\
    Directory: ..\food
    Subdirectory: fruits
    Subdirectory: vegetables

    Directory: ..\food\fruits
    Subdirectory: apples
    Subdirectory: oranges
    File: 2019-07-18 12.24.46.385185_banana.txt
    File: 2019-07-18 12.24.46.389174_strawberry.txt
    File: 2019-07-18 12.24.46.391170_blueberry.txt

    Directory: ..\food\fruits\apples
    File: 2019-07-18 12.24.46.395160_honeycrisp.txt

    Directory: ..\food\fruits\oranges
    File: 2019-07-18 12.24.46.398151_mandarin.txt

    Directory: ..\food\vegetables
    File: 2019-07-18 12.24.46.402496_carrot.txt

    ```

5. Verwenden Sie Python, um die neuen Dateisystem-Verzeichnisnamen mit dem Zeitstempel der letzten Änderung, der der eigenen Textdatei vorangestellt ist, auszugeben, indem Sie diesen Befehl direkt in das PowerShell-Terminal eingeben: `python3 list-directory-contents.py > food-directory-last-modified.txt`

Wir hoffen, dass Sie mit der Verwendung von python-Skripts für die Automatisierung grundlegender Systemverwaltungsaufgaben etwas interessantes gelernt haben. Natürlich gibt es noch eine Menge mehr zu wissen, aber wir hoffen, dass dies auf dem richtigen Fuß gestartet wurde. Wir haben einige zusätzliche Ressourcen freigegeben, um weiter unten zu lernen.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [python-Dokumente: Datei-und Verzeichnis Zugriff @ no__t-0: Python-Dokumentation zum Arbeiten mit Dateisystemen und zum Verwenden von Modulen zum Lesen der Eigenschaften von Dateien, zum Ändern von Pfaden auf portablen und zum Erstellen temporärer Dateien.
- [learn python: String_Formatting Tutorial @ no__t-0: Weitere Informationen zur Verwendung des Operators "%" für die Zeichen folgen Formatierung.
- [10 python-Datei System Methoden, die Sie kennen sollten](https://towardsdatascience.com/10-python-file-system-methods-you-should-know-799f90ef13c2): Mittlerer Artikel zur Bearbeitung von Dateien und Ordnern mit `os` und `shutil`.
- [the hitchwanderguide to python: Systemverwaltung @ no__t-0: Ein "wertenführungs Handbuch", das Übersichten und bewährte Methoden für Themen im Zusammenhang mit python bietet. In diesem Abschnitt werden die System Administrator Tools und-Frameworks behandelt. Dieses Handbuch wird auf GitHub gehostet, damit Sie Probleme beheben und Beiträge leisten können.