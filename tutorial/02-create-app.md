---
ms.openlocfilehash: 70df2dfceb1d2df527acfecab894b28019c6febb
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274292"
---
<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung erstellen Sie eine Office-Add-In-Lösung mit [Express.](http://expressjs.com/) Die Lösung besteht aus zwei Teilen.

- Das Als statische HTML- und JavaScript-Dateien implementierte Add-In.
- Ein Node.js/Express-Server, der das Add-in bedient und eine Web-API zum Abrufen von Daten für das Add-In implementiert.

## <a name="create-the-server"></a>Erstellen des Servers

1. Öffnen Sie die Befehlszeilenschnittstelle (CLI), navigieren Sie zu einem Verzeichnis, in dem Sie Ihr Projekt erstellen möchten, und führen Sie den folgenden Befehl aus, um eine Datei package.jsgenerieren.

    ```Shell
    yarn init
    ```

    Geben Sie gegebenenfalls Werte für die Eingabeaufforderungen ein. Wenn Sie nicht sicher sind, sind die Standardwerte in Ordnung.

1. Führen Sie die folgenden Befehle aus, um Abhängigkeiten zu installieren.

    ```Shell
    yarn add express@4.17.1 express-promise-router@4.0.1 dotenv@8.2.0 node-fetch@2.6.1 jsonwebtoken@8.5.1@
    yarn add jwks-rsa@1.11.0 @azure/msal-node@1.0.0-beta.1 @microsoft/microsoft-graph-client@2.1.1
    yarn add date-fns@2.16.1 date-fns-tz@1.0.12 isomorphic-fetch@3.0.0 windows-iana@4.2.1
    yarn add -D typescript@4.0.5 ts-node@9.0.0 nodemon@2.0.6 @types/node@14.14.7 @types/express@4.17.9
    yarn add -D @types/node-fetch@2.5.7 @types/jsonwebtoken@8.5.0 @types/microsoft-graph@1.26.0
    yarn add -D @types/office-js@1.0.147 @types/jquery@3.5.4 @types/isomorphic-fetch@0.0.35
    ```

1. Führen Sie den folgenden Befehl aus, um ein tsconfig.jsdatei zu generieren.

    ```Shell
    tsc --init
    ```

1. Öffnen **Sie ./tsconfig.js** in einem Text-Editor, und nehmen Sie die folgenden Änderungen vor.

    - Ändern Sie den `target` Wert in `es6` .
    - Auskommentierung des `outDir` Werts auskomment, und legen Sie ihn auf `./dist` .
    - Auskommentierung des `rootDir` Werts auskomment, und legen Sie ihn auf `./src` .

1. Öffnen **Sie ./package.json,** und fügen Sie die folgende Eigenschaft zu JSON hinzu.

    ```json
    "scripts": {
      "start": "nodemon ./src/server.ts",
      "build": "tsc --project ./"
    },
    ```

1. Führen Sie den folgenden Befehl aus, um Entwicklungszertifikate für Ihr Add-in zu generieren und zu installieren.

    ```Shell
    npx office-addin-dev-certs install
    ```

    Bestätigen Sie die Aktionen, wenn Sie zur Bestätigung aufgefordert werden. Sobald der Befehl abgeschlossen ist, wird eine Ausgabe wie die folgende angezeigt.

    ```Shell
    You now have trusted access to https://localhost.
    Certificate: <path>\localhost.crt
    Key: <path>\localhost.key
    ```

1. Erstellen Sie eine neue Datei mit dem Namen **".env"** im Stammverzeichnis Ihres Projekts, und fügen Sie den folgenden Code hinzu.

    :::code language="ini" source="../demo/graph-tutorial/example.env":::

    Ersetzen Sie dies durch den Pfad zu "localhost.crt" und durch den Pfad zur `PATH_TO_LOCALHOST.CRT` `PATH_TO_LOCALHOST.KEY` Localhost.key-Ausgabe durch den vorherigen Befehl.

1. Erstellen Sie ein neues Verzeichnis im Stammverzeichnis Des Projekts mit dem Namen **src**.

1. Erstellen Sie zwei Verzeichnisse im **Verzeichnis ./src:** **addin** und **api**.

1. Erstellen Sie eine neue Datei mit dem Namen **"auth.ts"** im **Verzeichnis ./src/api,** und fügen Sie den folgenden Code hinzu.

    ```typescript
    import Router from 'express-promise-router';

    const authRouter = Router();

    // TODO: Implement this router

    export default authRouter;
    ```

1. Erstellen Sie eine neue Datei mit dem Namen **"graph.ts"** im **Verzeichnis ./src/api,** und fügen Sie den folgenden Code hinzu.

    ```typescript
    import Router from 'express-promise-router';

    const graphRouter = Router();

    // TODO: Implement this router

    export default graphRouter;
    ```

1. Erstellen Sie eine neue Datei mit dem Namen **"server.ts"** im **Verzeichnis ./src,** und fügen Sie den folgenden Code hinzu.

    :::code language="typescript" source="../demo/graph-tutorial/src/server.ts" id="ServerSnippet":::

## <a name="create-the-add-in"></a>Erstellen des Add-Ins

1. Erstellen Sie eine neue Datei **namenstaskpane.html** im Verzeichnis **./src/addin,** und fügen Sie den folgenden Code hinzu.

    :::code language="html" source="../demo/graph-tutorial/src/addin/taskpane.html" id="TaskPaneHtmlSnippet":::

1. Erstellen Sie eine neue Datei namens **taskpane.css** im **Verzeichnis ./src/addin,** und fügen Sie den folgenden Code hinzu.

    :::code language="css" source="../demo/graph-tutorial/src/addin/taskpane.css":::

1. Erstellen Sie eine neue Datei **namenstaskpane.js** im Verzeichnis **./src/addin,** und fügen Sie den folgenden Code hinzu.

    ```javascript
    // TEMPORARY CODE TO VERIFY ADD-IN LOADS
    'use strict';

    Office.onReady(info => {
      if (info.host === Office.HostType.Excel) {
        $(function() {
          $('p').text('Hello World!!');
        });
      }
    });
    ```

1. Erstellen Sie ein neues Verzeichnis im **Verzeichnis .src/addin** mit dem Namen **Assets**.

1. Fügen Sie in diesem Verzeichnis gemäß der folgenden Tabelle drei PNG-Dateien hinzu.

    | Dateiname   | Größe in Pixeln |
    |-------------|----------------|
    | icon-80.png | 80x80          |
    | icon-32.png | 32x32          |
    | icon-16.png | 16x16          |

    > [!NOTE]
    > Sie können für diesen Schritt ein beliebiges Bild verwenden. Sie können die in diesem Beispiel verwendeten Bilder auch direkt von [GitHub herunterladen.](https://github.com/microsoftgraph/msgraph-training-office-addin/demo/graph-tutorial/src/addin/assets)

1. Erstellen Sie ein neues Verzeichnis im Stammverzeichnis des Projekts namens **Manifest**.

1. Erstellen Sie eine neue Datei **namensmanifest.xml** im Ordner **"./manifest",** und fügen Sie den folgenden Code hinzu. Ersetzen `NEW_GUID_HERE` Sie diese durch eine neue GUID, z. `b4fa03b8-1eb6-4e8b-a380-e0476be9e019` B. .

    :::code language="xml" source="../demo/graph-tutorial/manifest/manifest.xml":::

## <a name="side-load-the-add-in-in-excel"></a>Side-load the add-in in Excel

1. Starten Sie den Server, indem Sie den folgenden Befehl ausführen.

    ```Shell
    yarn start
    ```

1. Öffnen Sie Ihren Browser, und navigieren Sie zu `https://localhost:3000/taskpane.html` . Es sollte eine Meldung `Not loaded` angezeigt werden.

1. Wechseln Sie in Ihrem Browser zu [Office.com](https://www.office.com/) und melden Sie sich an. Wählen **Sie auf** der linken Symbolleiste "Erstellen" und dann "Tabelle" **aus.**

    ![Screenshot des Menüs "Erstellen" auf Office.com](images/office-select-excel.png)

1. Wählen Sie die **Registerkarte** "Einfügen" und dann **"Office-Add-Ins" aus.**

1. Wählen **Sie "Mein Add-In hochladen"** und dann **"Durchsuchen" aus.** Laden Sie **Ihre ./manifest/manifest.xml** hoch.

1. Wählen Sie **auf der Registerkarte "Start"** die Schaltfläche "Kalender **importieren"** aus, um den Aufgabenfeld zu öffnen.

    ![Screenshot der Schaltfläche "Kalender importieren" auf der Registerkarte "Start"](images/get-started.png)

1. Nachdem der Aufgabenpan geöffnet wurde, sollte eine Meldung `Hello World!` angezeigt werden.

    ![Screenshot der Nachricht "Hello World"](images/hello-world.png)
