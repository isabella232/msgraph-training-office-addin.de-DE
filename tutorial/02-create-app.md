---
ms.openlocfilehash: 70df2dfceb1d2df527acfecab894b28019c6febb
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274292"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="0d301-101">In dieser Übung erstellen Sie eine Office-Add-In-Lösung mit [Express.](http://expressjs.com/)</span><span class="sxs-lookup"><span data-stu-id="0d301-101">In this exercise you will create an Office Add-in solution using [Express](http://expressjs.com/).</span></span> <span data-ttu-id="0d301-102">Die Lösung besteht aus zwei Teilen.</span><span class="sxs-lookup"><span data-stu-id="0d301-102">The solution will consist of two parts.</span></span>

- <span data-ttu-id="0d301-103">Das Als statische HTML- und JavaScript-Dateien implementierte Add-In.</span><span class="sxs-lookup"><span data-stu-id="0d301-103">The add-in, implemented as static HTML and JavaScript files.</span></span>
- <span data-ttu-id="0d301-104">Ein Node.js/Express-Server, der das Add-in bedient und eine Web-API zum Abrufen von Daten für das Add-In implementiert.</span><span class="sxs-lookup"><span data-stu-id="0d301-104">A Node.js/Express server that serves the add-in and implements a web API to retrieve data for the add-in.</span></span>

## <a name="create-the-server"></a><span data-ttu-id="0d301-105">Erstellen des Servers</span><span class="sxs-lookup"><span data-stu-id="0d301-105">Create the server</span></span>

1. <span data-ttu-id="0d301-106">Öffnen Sie die Befehlszeilenschnittstelle (CLI), navigieren Sie zu einem Verzeichnis, in dem Sie Ihr Projekt erstellen möchten, und führen Sie den folgenden Befehl aus, um eine Datei package.jsgenerieren.</span><span class="sxs-lookup"><span data-stu-id="0d301-106">Open your command-line interface (CLI), navigate to a directory where you want to create your project, and run the following command to generate a package.json file.</span></span>

    ```Shell
    yarn init
    ```

    <span data-ttu-id="0d301-107">Geben Sie gegebenenfalls Werte für die Eingabeaufforderungen ein.</span><span class="sxs-lookup"><span data-stu-id="0d301-107">Enter values for the prompts as appropriate.</span></span> <span data-ttu-id="0d301-108">Wenn Sie nicht sicher sind, sind die Standardwerte in Ordnung.</span><span class="sxs-lookup"><span data-stu-id="0d301-108">If you're unsure, the default values are fine.</span></span>

1. <span data-ttu-id="0d301-109">Führen Sie die folgenden Befehle aus, um Abhängigkeiten zu installieren.</span><span class="sxs-lookup"><span data-stu-id="0d301-109">Run the following commands to install dependencies.</span></span>

    ```Shell
    yarn add express@4.17.1 express-promise-router@4.0.1 dotenv@8.2.0 node-fetch@2.6.1 jsonwebtoken@8.5.1@
    yarn add jwks-rsa@1.11.0 @azure/msal-node@1.0.0-beta.1 @microsoft/microsoft-graph-client@2.1.1
    yarn add date-fns@2.16.1 date-fns-tz@1.0.12 isomorphic-fetch@3.0.0 windows-iana@4.2.1
    yarn add -D typescript@4.0.5 ts-node@9.0.0 nodemon@2.0.6 @types/node@14.14.7 @types/express@4.17.9
    yarn add -D @types/node-fetch@2.5.7 @types/jsonwebtoken@8.5.0 @types/microsoft-graph@1.26.0
    yarn add -D @types/office-js@1.0.147 @types/jquery@3.5.4 @types/isomorphic-fetch@0.0.35
    ```

1. <span data-ttu-id="0d301-110">Führen Sie den folgenden Befehl aus, um ein tsconfig.jsdatei zu generieren.</span><span class="sxs-lookup"><span data-stu-id="0d301-110">Run the following command to generate a tsconfig.json file.</span></span>

    ```Shell
    tsc --init
    ```

1. <span data-ttu-id="0d301-111">Öffnen **Sie ./tsconfig.js** in einem Text-Editor, und nehmen Sie die folgenden Änderungen vor.</span><span class="sxs-lookup"><span data-stu-id="0d301-111">Open **./tsconfig.json** in a text editor and make the following changes.</span></span>

    - <span data-ttu-id="0d301-112">Ändern Sie den `target` Wert in `es6` .</span><span class="sxs-lookup"><span data-stu-id="0d301-112">Change the `target` value to `es6`.</span></span>
    - <span data-ttu-id="0d301-113">Auskommentierung des `outDir` Werts auskomment, und legen Sie ihn auf `./dist` .</span><span class="sxs-lookup"><span data-stu-id="0d301-113">Uncomment the `outDir` value and set it to `./dist`.</span></span>
    - <span data-ttu-id="0d301-114">Auskommentierung des `rootDir` Werts auskomment, und legen Sie ihn auf `./src` .</span><span class="sxs-lookup"><span data-stu-id="0d301-114">Uncomment the `rootDir` value and set it to `./src`.</span></span>

1. <span data-ttu-id="0d301-115">Öffnen **Sie ./package.json,** und fügen Sie die folgende Eigenschaft zu JSON hinzu.</span><span class="sxs-lookup"><span data-stu-id="0d301-115">Open **./package.json** and add the following property to the JSON.</span></span>

    ```json
    "scripts": {
      "start": "nodemon ./src/server.ts",
      "build": "tsc --project ./"
    },
    ```

1. <span data-ttu-id="0d301-116">Führen Sie den folgenden Befehl aus, um Entwicklungszertifikate für Ihr Add-in zu generieren und zu installieren.</span><span class="sxs-lookup"><span data-stu-id="0d301-116">Run the following command to generate and install development certificates for your add-in.</span></span>

    ```Shell
    npx office-addin-dev-certs install
    ```

    <span data-ttu-id="0d301-117">Bestätigen Sie die Aktionen, wenn Sie zur Bestätigung aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="0d301-117">If prompted for confirmation, confirm the actions.</span></span> <span data-ttu-id="0d301-118">Sobald der Befehl abgeschlossen ist, wird eine Ausgabe wie die folgende angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0d301-118">Once the command completes, you will see output similar to the following.</span></span>

    ```Shell
    You now have trusted access to https://localhost.
    Certificate: <path>\localhost.crt
    Key: <path>\localhost.key
    ```

1. <span data-ttu-id="0d301-119">Erstellen Sie eine neue Datei mit dem Namen **".env"** im Stammverzeichnis Ihres Projekts, und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="0d301-119">Create a new file named **.env** in the root of your project and add the following code.</span></span>

    :::code language="ini" source="../demo/graph-tutorial/example.env":::

    <span data-ttu-id="0d301-120">Ersetzen Sie dies durch den Pfad zu "localhost.crt" und durch den Pfad zur `PATH_TO_LOCALHOST.CRT` `PATH_TO_LOCALHOST.KEY` Localhost.key-Ausgabe durch den vorherigen Befehl.</span><span class="sxs-lookup"><span data-stu-id="0d301-120">Replace `PATH_TO_LOCALHOST.CRT` with the path to localhost.crt and `PATH_TO_LOCALHOST.KEY` with the path to localhost.key output by the previous command.</span></span>

1. <span data-ttu-id="0d301-121">Erstellen Sie ein neues Verzeichnis im Stammverzeichnis Des Projekts mit dem Namen **src**.</span><span class="sxs-lookup"><span data-stu-id="0d301-121">Create a new directory in the root of your project named **src**.</span></span>

1. <span data-ttu-id="0d301-122">Erstellen Sie zwei Verzeichnisse im **Verzeichnis ./src:** **addin** und **api**.</span><span class="sxs-lookup"><span data-stu-id="0d301-122">Create two directories in the **./src** directory: **addin** and **api**.</span></span>

1. <span data-ttu-id="0d301-123">Erstellen Sie eine neue Datei mit dem Namen **"auth.ts"** im **Verzeichnis ./src/api,** und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="0d301-123">Create a new file named **auth.ts** in the **./src/api** directory and add the following code.</span></span>

    ```typescript
    import Router from 'express-promise-router';

    const authRouter = Router();

    // TODO: Implement this router

    export default authRouter;
    ```

1. <span data-ttu-id="0d301-124">Erstellen Sie eine neue Datei mit dem Namen **"graph.ts"** im **Verzeichnis ./src/api,** und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="0d301-124">Create a new file named **graph.ts** in the **./src/api** directory and add the following code.</span></span>

    ```typescript
    import Router from 'express-promise-router';

    const graphRouter = Router();

    // TODO: Implement this router

    export default graphRouter;
    ```

1. <span data-ttu-id="0d301-125">Erstellen Sie eine neue Datei mit dem Namen **"server.ts"** im **Verzeichnis ./src,** und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="0d301-125">Create a new file named **server.ts** in the **./src** directory and add the following code.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/server.ts" id="ServerSnippet":::

## <a name="create-the-add-in"></a><span data-ttu-id="0d301-126">Erstellen des Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0d301-126">Create the add-in</span></span>

1. <span data-ttu-id="0d301-127">Erstellen Sie eine neue Datei **namenstaskpane.html** im Verzeichnis **./src/addin,** und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="0d301-127">Create a new file named **taskpane.html** in the **./src/addin** directory and add the following code.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/addin/taskpane.html" id="TaskPaneHtmlSnippet":::

1. <span data-ttu-id="0d301-128">Erstellen Sie eine neue Datei namens **taskpane.css** im **Verzeichnis ./src/addin,** und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="0d301-128">Create a new file named **taskpane.css** in the **./src/addin** directory and add the following code.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/addin/taskpane.css":::

1. <span data-ttu-id="0d301-129">Erstellen Sie eine neue Datei **namenstaskpane.js** im Verzeichnis **./src/addin,** und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="0d301-129">Create a new file named **taskpane.js** in the **./src/addin** directory and add the following code.</span></span>

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

1. <span data-ttu-id="0d301-130">Erstellen Sie ein neues Verzeichnis im **Verzeichnis .src/addin** mit dem Namen **Assets**.</span><span class="sxs-lookup"><span data-stu-id="0d301-130">Create a new directory in the **.src/addin** directory named **assets**.</span></span>

1. <span data-ttu-id="0d301-131">Fügen Sie in diesem Verzeichnis gemäß der folgenden Tabelle drei PNG-Dateien hinzu.</span><span class="sxs-lookup"><span data-stu-id="0d301-131">Add three PNG files in this directory according to the following table.</span></span>

    | <span data-ttu-id="0d301-132">Dateiname</span><span class="sxs-lookup"><span data-stu-id="0d301-132">File name</span></span>   | <span data-ttu-id="0d301-133">Größe in Pixeln</span><span class="sxs-lookup"><span data-stu-id="0d301-133">Size in pixels</span></span> |
    |-------------|----------------|
    | <span data-ttu-id="0d301-134">icon-80.png</span><span class="sxs-lookup"><span data-stu-id="0d301-134">icon-80.png</span></span> | <span data-ttu-id="0d301-135">80x80</span><span class="sxs-lookup"><span data-stu-id="0d301-135">80x80</span></span>          |
    | <span data-ttu-id="0d301-136">icon-32.png</span><span class="sxs-lookup"><span data-stu-id="0d301-136">icon-32.png</span></span> | <span data-ttu-id="0d301-137">32x32</span><span class="sxs-lookup"><span data-stu-id="0d301-137">32x32</span></span>          |
    | <span data-ttu-id="0d301-138">icon-16.png</span><span class="sxs-lookup"><span data-stu-id="0d301-138">icon-16.png</span></span> | <span data-ttu-id="0d301-139">16x16</span><span class="sxs-lookup"><span data-stu-id="0d301-139">16x16</span></span>          |

    > [!NOTE]
    > <span data-ttu-id="0d301-140">Sie können für diesen Schritt ein beliebiges Bild verwenden.</span><span class="sxs-lookup"><span data-stu-id="0d301-140">You can use any image you want for this step.</span></span> <span data-ttu-id="0d301-141">Sie können die in diesem Beispiel verwendeten Bilder auch direkt von [GitHub herunterladen.](https://github.com/microsoftgraph/msgraph-training-office-addin/demo/graph-tutorial/src/addin/assets)</span><span class="sxs-lookup"><span data-stu-id="0d301-141">You can also download the images used in this sample directly from [GitHub](https://github.com/microsoftgraph/msgraph-training-office-addin/demo/graph-tutorial/src/addin/assets).</span></span>

1. <span data-ttu-id="0d301-142">Erstellen Sie ein neues Verzeichnis im Stammverzeichnis des Projekts namens **Manifest**.</span><span class="sxs-lookup"><span data-stu-id="0d301-142">Create a new directory in the root of the project named **manifest**.</span></span>

1. <span data-ttu-id="0d301-143">Erstellen Sie eine neue Datei **namensmanifest.xml** im Ordner **"./manifest",** und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="0d301-143">Create a new file named **manifest.xml** in the **./manifest** folder and add the following code.</span></span> <span data-ttu-id="0d301-144">Ersetzen `NEW_GUID_HERE` Sie diese durch eine neue GUID, z. `b4fa03b8-1eb6-4e8b-a380-e0476be9e019` B. .</span><span class="sxs-lookup"><span data-stu-id="0d301-144">Replace `NEW_GUID_HERE` with a new GUID, like `b4fa03b8-1eb6-4e8b-a380-e0476be9e019`.</span></span>

    :::code language="xml" source="../demo/graph-tutorial/manifest/manifest.xml":::

## <a name="side-load-the-add-in-in-excel"></a><span data-ttu-id="0d301-145">Side-load the add-in in Excel</span><span class="sxs-lookup"><span data-stu-id="0d301-145">Side-load the add-in in Excel</span></span>

1. <span data-ttu-id="0d301-146">Starten Sie den Server, indem Sie den folgenden Befehl ausführen.</span><span class="sxs-lookup"><span data-stu-id="0d301-146">Start the server by running the following command.</span></span>

    ```Shell
    yarn start
    ```

1. <span data-ttu-id="0d301-147">Öffnen Sie Ihren Browser, und navigieren Sie zu `https://localhost:3000/taskpane.html` .</span><span class="sxs-lookup"><span data-stu-id="0d301-147">Open your browser and browse to `https://localhost:3000/taskpane.html`.</span></span> <span data-ttu-id="0d301-148">Es sollte eine Meldung `Not loaded` angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="0d301-148">You should see a `Not loaded` message.</span></span>

1. <span data-ttu-id="0d301-149">Wechseln Sie in Ihrem Browser zu [Office.com](https://www.office.com/) und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="0d301-149">In your browser, go to [Office.com](https://www.office.com/) and sign in.</span></span> <span data-ttu-id="0d301-150">Wählen **Sie auf** der linken Symbolleiste "Erstellen" und dann "Tabelle" **aus.**</span><span class="sxs-lookup"><span data-stu-id="0d301-150">Select **Create** in the left-hand toolbar, then select **Spreadsheet**.</span></span>

    ![Screenshot des Menüs "Erstellen" auf Office.com](images/office-select-excel.png)

1. <span data-ttu-id="0d301-152">Wählen Sie die **Registerkarte** "Einfügen" und dann **"Office-Add-Ins" aus.**</span><span class="sxs-lookup"><span data-stu-id="0d301-152">Select the **Insert** tab, then select **Office Add-ins**.</span></span>

1. <span data-ttu-id="0d301-153">Wählen **Sie "Mein Add-In hochladen"** und dann **"Durchsuchen" aus.**</span><span class="sxs-lookup"><span data-stu-id="0d301-153">Select **Upload My Add-in**, then select **Browse**.</span></span> <span data-ttu-id="0d301-154">Laden Sie **Ihre ./manifest/manifest.xml** hoch.</span><span class="sxs-lookup"><span data-stu-id="0d301-154">Upload your **./manifest/manifest.xml** file.</span></span>

1. <span data-ttu-id="0d301-155">Wählen Sie **auf der Registerkarte "Start"** die Schaltfläche "Kalender **importieren"** aus, um den Aufgabenfeld zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="0d301-155">Select the **Import Calendar** button on the **Home** tab to open the taskpane.</span></span>

    ![Screenshot der Schaltfläche "Kalender importieren" auf der Registerkarte "Start"](images/get-started.png)

1. <span data-ttu-id="0d301-157">Nachdem der Aufgabenpan geöffnet wurde, sollte eine Meldung `Hello World!` angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="0d301-157">After the taskpane opens, you should see a `Hello World!` message.</span></span>

    ![Screenshot der Nachricht "Hello World"](images/hello-world.png)
