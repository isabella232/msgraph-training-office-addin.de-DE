---
ms.openlocfilehash: 09ef719985094d87c438b6f98b931865dbd59c75
ms.sourcegitcommit: 8a65c826f6b229c287a782d784b6d9629aa5a3d0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/20/2021
ms.locfileid: "51899422"
---
<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung erstellen Sie mithilfe von [Express](http://expressjs.com/)eine Office-Add-In-Lösung. Die Lösung besteht aus zwei Teilen.

- Das Als statische HTML- und JavaScript-Dateien implementierte Add-In.
- Ein Node.js/Express-Server, der das Add-In bedient und eine Web-API zum Abrufen von Daten für das Add-In implementiert.

## <a name="create-the-server"></a>Erstellen des Servers

1. Öffnen Sie die Befehlszeilenschnittstelle (CLI), navigieren Sie zu einem Verzeichnis, in dem Sie Ihr Projekt erstellen möchten, und führen Sie den folgenden Befehl aus, um eine package.jszu generieren.

    ```Shell
    yarn init
    ```

    Geben Sie gegebenenfalls Werte für die Eingabeaufforderungen ein. Wenn Sie unsicher sind, sind die Standardwerte in Ordnung.

1. Führen Sie die folgenden Befehle aus, um Abhängigkeiten zu installieren.

    ```Shell
    yarn add express@4.17.1 express-promise-router@4.1.0 dotenv@8.2.0 node-fetch@2.6.1 jsonwebtoken@8.5.1@
    yarn add jwks-rsa@2.0.2 @azure/msal-node@1.0.2 @microsoft/microsoft-graph-client@2.2.1
    yarn add date-fns@2.21.1 date-fns-tz@1.1.4 isomorphic-fetch@3.0.0 windows-iana@5.0.1
    yarn add -D typescript@4.2.4 ts-node@9.1.1 nodemon@2.0.7 @types/node@14.14.41 @types/express@4.17.11
    yarn add -D @types/node-fetch@2.5.10 @types/jsonwebtoken@8.5.1 @types/microsoft-graph@1.35.0
    yarn add -D @types/office-js@1.0.174 @types/jquery@3.5.5 @types/isomorphic-fetch@0.0.35
    ```

1. Führen Sie den folgenden Befehl aus, um eine tsconfig.jszu generieren.

    ```Shell
    tsc --init
    ```

1. Öffnen **Sie ./tsconfig.jsin** einem Texteditor, und nehmen Sie die folgenden Änderungen vor.

    - Ändern Sie `target` den Wert in `es6` .
    - Entkomment den `outDir` Wert, und legen Sie ihn auf . `./dist`
    - Entkomment den `rootDir` Wert, und legen Sie ihn auf . `./src`

1. Öffnen **Sie ./package.jsein,** und fügen Sie der JSON die folgende Eigenschaft hinzu.

    ```json
    "scripts": {
      "start": "nodemon ./src/server.ts",
      "build": "tsc --project ./"
    },
    ```

1. Führen Sie den folgenden Befehl aus, um Entwicklungszertifikate für Ihr Add-In zu generieren und zu installieren.

    ```Shell
    npx office-addin-dev-certs install
    ```

    Wenn Sie zur Bestätigung aufgefordert werden, bestätigen Sie die Aktionen. Sobald der Befehl abgeschlossen ist, wird die Ausgabe ähnlich der folgenden angezeigt.

    ```Shell
    You now have trusted access to https://localhost.
    Certificate: <path>\localhost.crt
    Key: <path>\localhost.key
    ```

1. Erstellen Sie eine neue Datei namens **.env** im Stammverzeichnis Ihres Projekts, und fügen Sie den folgenden Code hinzu.

    :::code language="ini" source="../demo/graph-tutorial/example.env":::

    Ersetzen Sie durch den Pfad zu localhost.crt und durch den Pfad zur `PATH_TO_LOCALHOST.CRT` `PATH_TO_LOCALHOST.KEY` localhost.key-Ausgabe durch den vorherigen Befehl.

1. Erstellen Sie ein neues Verzeichnis im Stammverzeichnis Ihres Projekts mit dem Namen **src**.

1. Erstellen Sie zwei Verzeichnisse im **Verzeichnis ./src:** **addin** und **api**.

1. Erstellen Sie eine neue Datei mit dem Namen **auth.ts** im **Verzeichnis ./src/api,** und fügen Sie den folgenden Code hinzu.

    ```typescript
    import Router from 'express-promise-router';

    const authRouter = Router();

    // TODO: Implement this router

    export default authRouter;
    ```

1. Erstellen Sie eine neue Datei mit dem Namen **graph.ts** im **Verzeichnis ./src/api,** und fügen Sie den folgenden Code hinzu.

    ```typescript
    import Router from 'express-promise-router';

    const graphRouter = Router();

    // TODO: Implement this router

    export default graphRouter;
    ```

1. Erstellen Sie eine neue Datei mit dem Namen **server.ts** im **Verzeichnis ./src,** und fügen Sie den folgenden Code hinzu.

    :::code language="typescript" source="../demo/graph-tutorial/src/server.ts" id="ServerSnippet":::

## <a name="create-the-add-in"></a>Erstellen des Add-Ins

1. Erstellen Sie eine neue Datei **namenstaskpane.html** im Verzeichnis **./src/addin,** und fügen Sie den folgenden Code hinzu.

    :::code language="html" source="../demo/graph-tutorial/src/addin/taskpane.html" id="TaskPaneHtmlSnippet":::

1. Erstellen Sie eine neue Datei **mit dem Namen taskpane.css** im **Verzeichnis ./src/addin,** und fügen Sie den folgenden Code hinzu.

    :::code language="css" source="../demo/graph-tutorial/src/addin/taskpane.css":::

1. Erstellen Sie eine neue Datei **namenstaskpane.js** im **Verzeichnis ./src/addin,** und fügen Sie den folgenden Code hinzu.

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

1. Fügen Sie in diesem Verzeichnis drei PNG-Dateien gemäß der folgenden Tabelle hinzu.

    | Dateiname   | Größe in Pixeln |
    |-------------|----------------|
    | icon-80.png | 80x80          |
    | icon-32.png | 32x32          |
    | icon-16.png | 16x16          |

    > [!NOTE]
    > Sie können ein beliebiges Bild für diesen Schritt verwenden. Sie können die in diesem Beispiel verwendeten Bilder auch direkt aus [GitHub herunterladen.](https://github.com/microsoftgraph/msgraph-training-office-addin/demo/graph-tutorial/src/addin/assets)

1. Erstellen Sie ein neues Verzeichnis im Stammverzeichnis des Projekts namens **Manifest**.

1. Erstellen Sie eine neue Datei **namensmanifest.xml** im Ordner **./manifest,** und fügen Sie den folgenden Code hinzu. Ersetzen `NEW_GUID_HERE` Sie durch eine neue GUID, z. `b4fa03b8-1eb6-4e8b-a380-e0476be9e019` B. .

    :::code language="xml" source="../demo/graph-tutorial/manifest/manifest.xml":::

## <a name="side-load-the-add-in-in-excel"></a>Seitenladen des Add-Ins in Excel

1. Starten Sie den Server, indem Sie den folgenden Befehl ausführen.

    ```Shell
    yarn start
    ```

1. Öffnen Sie Ihren Browser, und navigieren Sie zu `https://localhost:3000/taskpane.html` . Es sollte eine Meldung `Not loaded` angezeigt werden.

1. Wechseln Sie in Ihrem Browser [zu Office.com](https://www.office.com/) und melden Sie sich an. Wählen **Sie** in der linken Symbolleiste Erstellen aus, und wählen Sie dann **Tabellenkalkulation aus.**

    ![Screenshot des Menüs Erstellen auf Office.com](images/office-select-excel.png)

1. Wählen Sie die **Registerkarte** Einfügen und dann **Office-Add-Ins aus.**

1. Wählen **Sie Mein Add-In hochladen** aus, und wählen Sie dann Durchsuchen **aus.** Laden Sie **Die Datei ./manifest/manifest.xml** hoch.

1. Wählen Sie **auf der Registerkarte** Start die Schaltfläche Kalender importieren **aus,** um den Aufgabenfeld zu öffnen.

    ![Screenshot der Schaltfläche Kalender importieren auf der Registerkarte Start](images/get-started.png)

1. Nachdem der Taskpane geöffnet wurde, sollte eine Meldung `Hello World!` angezeigt werden.

    ![Screenshot der Hello World-Nachricht](images/hello-world.png)
