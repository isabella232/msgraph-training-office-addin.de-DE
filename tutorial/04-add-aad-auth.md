---
ms.openlocfilehash: 69d77c19cb2c589086df2b4bf19eeadf41aad58a
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274393"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="ecc24-101">In dieser Übung aktivieren Sie [einmaliges Anmelden (Single Sign-On, SSO) für Office-Add-Ins](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins) im Add-In und erweitern die Web-API so, dass sie den [On-Behalf-of-Fluss unterstützt.](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)</span><span class="sxs-lookup"><span data-stu-id="ecc24-101">In this exercise you will enable [Office Add-in single sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins) in the add-in, and extend the web API to support [on-behalf-of flow](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow).</span></span> <span data-ttu-id="ecc24-102">Dies ist erforderlich, um das erforderliche OAuth-Zugriffstoken zum Aufrufen von Microsoft Graph abzurufen.</span><span class="sxs-lookup"><span data-stu-id="ecc24-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span>

## <a name="overview"></a><span data-ttu-id="ecc24-103">Übersicht</span><span class="sxs-lookup"><span data-stu-id="ecc24-103">Overview</span></span>

<span data-ttu-id="ecc24-104">Office-Add-In-SSO stellt ein Zugriffstoken bereit, dieses Token ermöglicht es dem Add-In jedoch nur, seine eigene Web-API auf aufruft.</span><span class="sxs-lookup"><span data-stu-id="ecc24-104">Office Add-in SSO provides an access token, but that token is only enables the add-in to call it's own web API.</span></span> <span data-ttu-id="ecc24-105">Es ermöglicht nicht den direkten Zugriff auf Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ecc24-105">It does not enable direct access to the Microsoft Graph.</span></span> <span data-ttu-id="ecc24-106">Der Vorgang funktioniert wie folgt.</span><span class="sxs-lookup"><span data-stu-id="ecc24-106">The process works as follows.</span></span>

1. <span data-ttu-id="ecc24-107">Das Add-in ruft ein Token durch Aufrufen von [getAccessToken ab.](https://docs.microsoft.com/javascript/api/office-runtime/officeruntime.auth?view=common-js#getaccesstoken-options-)</span><span class="sxs-lookup"><span data-stu-id="ecc24-107">The add-in gets a token by calling [getAccessToken](https://docs.microsoft.com/javascript/api/office-runtime/officeruntime.auth?view=common-js#getaccesstoken-options-).</span></span> <span data-ttu-id="ecc24-108">Die Zielgruppe dieses Tokens (der Anspruch) ist die `aud` Anwendungs-ID der App-Registrierung des Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="ecc24-108">This token's audience (the `aud` claim) is the application ID of the add-in's app registration.</span></span>
1. <span data-ttu-id="ecc24-109">Das Add-in sendet dieses Token in der `Authorization` Kopfzeile, wenn es einen Aufruf an die Web-API macht.</span><span class="sxs-lookup"><span data-stu-id="ecc24-109">The add-in sends this token in the `Authorization` header when it makes a call to the web API.</span></span>
1. <span data-ttu-id="ecc24-110">Die Web-API überprüft das Token und verwendet dann den Im-Auftrag-von-Fluss, um dieses Token gegen ein Microsoft Graph-Token zu tauschen.</span><span class="sxs-lookup"><span data-stu-id="ecc24-110">The web API validates the token, then uses the on-behalf-of flow to exchange this token for a Microsoft Graph token.</span></span> <span data-ttu-id="ecc24-111">Die Zielgruppe dieses neuen Tokens ist `https://graph.microsoft.com` .</span><span class="sxs-lookup"><span data-stu-id="ecc24-111">This new token's audience is `https://graph.microsoft.com`.</span></span>
1. <span data-ttu-id="ecc24-112">Die Web-API verwendet das neue Token, um Aufrufe an Microsoft Graph zu senden, und gibt die Ergebnisse an das Add-In zurück.</span><span class="sxs-lookup"><span data-stu-id="ecc24-112">The web API uses the new token to make calls to the Microsoft Graph, and returns the results back to the add-in.</span></span>

## <a name="configure-the-solution"></a><span data-ttu-id="ecc24-113">Konfigurieren der Lösung</span><span class="sxs-lookup"><span data-stu-id="ecc24-113">Configure the solution</span></span>

1. <span data-ttu-id="ecc24-114">Öffnen **Sie ./.env,** und aktualisieren Sie die Anwendungs-ID und den `AZURE_APP_ID` geheimen Clientgeheimnis aus Ihrer `AZURE_CLIENT_SECRET` App-Registrierung.</span><span class="sxs-lookup"><span data-stu-id="ecc24-114">Open **./.env** and update the `AZURE_APP_ID` and `AZURE_CLIENT_SECRET` with the application ID and client secret from your app registration.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ecc24-115">Wenn Sie Quellcodeverwaltung wie Git verwenden, wäre es jetzt ein guter Zeitpunkt, die **env-Datei** aus der Quellcodeverwaltung auszuschließen, um zu verhindern, dass versehentlich Ihre App-ID und der geheime Client geheimen Clientdatenlecks ans Licht kommen.</span><span class="sxs-lookup"><span data-stu-id="ecc24-115">If you're using source control such as git, now would be a good time to exclude the **.env** file from source control to avoid inadvertently leaking your app ID and client secret.</span></span>

1. <span data-ttu-id="ecc24-116">Öffnen **Sie ./manifest/manifest.xml,** und ersetzen Sie alle Instanzen durch die Anwendungs-ID `YOUR_APP_ID_HERE` aus Ihrer App-Registrierung.</span><span class="sxs-lookup"><span data-stu-id="ecc24-116">Open **./manifest/manifest.xml** and replace all instances of `YOUR_APP_ID_HERE` with the application ID from your app registration.</span></span>

1. <span data-ttu-id="ecc24-117">Erstellen Sie eine neue Datei im Verzeichnis **./src/addin** mit dem Namen **config.js,** und fügen Sie den folgenden Code hinzu, und ersetzen Sie dabei die Anwendungs-ID aus `YOUR_APP_ID_HERE` Ihrer App-Registrierung.</span><span class="sxs-lookup"><span data-stu-id="ecc24-117">Create a new file in the **./src/addin** directory named **config.js** and add the following code, replacing `YOUR_APP_ID_HERE` with the application ID from your app registration.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/config.example.js":::

## <a name="implement-sign-in"></a><span data-ttu-id="ecc24-118">Implementieren der Anmeldung</span><span class="sxs-lookup"><span data-stu-id="ecc24-118">Implement sign-in</span></span>

1. <span data-ttu-id="ecc24-119">Öffnen **Sie ./src/api/auth.ts,** und fügen Sie die folgenden Anweisungen `import` am Anfang der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="ecc24-119">Open **./src/api/auth.ts** and add the following `import` statements at the top of the file.</span></span>

    ```typescript
    import jwt, { SigningKeyCallback, JwtHeader } from 'jsonwebtoken';
    import jwksClient from 'jwks-rsa';
    import * as msal from '@azure/msal-node';
    ```

1. <span data-ttu-id="ecc24-120">Fügen Sie den folgenden Code nach den Anweisungen `import` hinzu.</span><span class="sxs-lookup"><span data-stu-id="ecc24-120">Add the following code after the `import` statements.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/auth.ts" id="TokenExchangeSnippet":::

    <span data-ttu-id="ecc24-121">Dieser Code [initialisiert einen vertraulichen MSAL-Client](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md)und exportiert eine Funktion, um ein Graph-Token aus dem Token abzurufen, das vom Add-in gesendet wurde.</span><span class="sxs-lookup"><span data-stu-id="ecc24-121">This code [initializes an MSAL confidential client](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md), and exports a function to get a Graph token from the token sent by the add-in.</span></span>

1. <span data-ttu-id="ecc24-122">Fügen Sie den folgenden Code vor der `export default authRouter;` Zeile hinzu.</span><span class="sxs-lookup"><span data-stu-id="ecc24-122">Add the following code before the `export default authRouter;` line.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/auth.ts" id="GetAuthStatusSnippet":::

    <span data-ttu-id="ecc24-123">Dieser Code implementiert eine API ( ), die überprüft, ob das Add-In-Token im Hintergrund gegen ein `GET /auth/status` Graph-Token ausgetauscht werden kann.</span><span class="sxs-lookup"><span data-stu-id="ecc24-123">This code implements an API (`GET /auth/status`) that checks if the add-in token can be silently exchanged for a Graph token.</span></span> <span data-ttu-id="ecc24-124">Das Add-in verwendet diese API, um zu bestimmen, ob es dem Benutzer eine interaktive Anmeldung präsentieren muss.</span><span class="sxs-lookup"><span data-stu-id="ecc24-124">The add-in will use this API to determine if it needs to present an interactive login to the user.</span></span>

1. <span data-ttu-id="ecc24-125">Öffnen **Sie ./src/addin/taskpane.js,** und fügen Sie der Datei den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="ecc24-125">Open **./src/addin/taskpane.js** and add the following code to the file.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="AuthUiSnippet":::

    <span data-ttu-id="ecc24-126">Dieser Code fügt Funktionen hinzu, um die Benutzeroberfläche zu aktualisieren und die [Office-Dialog-API](https://docs.microsoft.com/office/dev/add-ins/develop/dialog-api-in-office-add-ins) zum Initiieren eines interaktiven Authentifizierungsflusses zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="ecc24-126">This code adds functions to update the UI, and to use the [Office Dialog API](https://docs.microsoft.com/office/dev/add-ins/develop/dialog-api-in-office-add-ins) to initiate an interactive authentication flow.</span></span>

1. <span data-ttu-id="ecc24-127">Fügen Sie die folgende Funktion hinzu, um eine temporäre Hauptbenutzeroberfläche zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="ecc24-127">Add the following function to implement a temporary main UI.</span></span>

    ```javascript
    function showMainUi() {
      $('.container').empty();
      $('<p/>', {
        class: 'ms-fontSize-24 ms-fontWeight-bold',
        text: 'Authenticated!'
      }).appendTo('.container');
    }
    ```

1. <span data-ttu-id="ecc24-128">Ersetzen Sie den `Office.onReady` vorhandenen Anruf durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="ecc24-128">Replace the existing `Office.onReady` call with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="OfficeReadySnippet":::

    <span data-ttu-id="ecc24-129">Überlegen Sie, was dieser Code macht.</span><span class="sxs-lookup"><span data-stu-id="ecc24-129">Consider what this code does.</span></span>

    - <span data-ttu-id="ecc24-130">Wenn der Aufgabenbereich zum ersten Mal geladen wird, ruft er ein Token ab, das auf die `getAccessToken` Web-API des Add-Ins ausgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="ecc24-130">When the task pane first loads, it calls `getAccessToken` to get a token scoped for the add-in's web API.</span></span>
    - <span data-ttu-id="ecc24-131">Dieses Token wird zum Aufrufen der API verwendet, um zu überprüfen, ob der Benutzer den Microsoft Graph-Bereich `/auth/status` noch seine Zustimmung erteilt hat.</span><span class="sxs-lookup"><span data-stu-id="ecc24-131">It uses that token to call the `/auth/status` API to check if the user has given consent to the Microsoft Graph scopes yet.</span></span>
        - <span data-ttu-id="ecc24-132">Wenn der Benutzer nicht zugestimmt hat, verwendet er ein Popupfenster, um die Zustimmung des Benutzers über eine interaktive Anmeldung einzuholen.</span><span class="sxs-lookup"><span data-stu-id="ecc24-132">If the user has not consented, it uses a pop-up window to get the user's consent through an interactive login.</span></span>
        - <span data-ttu-id="ecc24-133">Wenn der Benutzer seine Zustimmung gegeben hat, wird die Hauptbenutzeroberfläche geladen.</span><span class="sxs-lookup"><span data-stu-id="ecc24-133">If the user has consented, it loads the main UI.</span></span>

### <a name="getting-user-consent"></a><span data-ttu-id="ecc24-134">Einholen der Zustimmung des Benutzers</span><span class="sxs-lookup"><span data-stu-id="ecc24-134">Getting user consent</span></span>

<span data-ttu-id="ecc24-135">Obwohl das Add-in SSO verwendet, muss der Benutzer dem Add-In, das über Microsoft Graph auf seine Daten zutritt, dennoch zustimmen.</span><span class="sxs-lookup"><span data-stu-id="ecc24-135">Even though the add-in is using SSO, the user still has to consent to the add-in accessing their data via Microsoft Graph.</span></span> <span data-ttu-id="ecc24-136">Das Einholen der Zustimmung ist ein einmaler Prozess.</span><span class="sxs-lookup"><span data-stu-id="ecc24-136">Getting consent is a one-time process.</span></span> <span data-ttu-id="ecc24-137">Nachdem der Benutzer seine Zustimmung erteilt hat, kann das SSO-Token ohne Benutzerinteraktion gegen ein Graph-Token ausgetauscht werden.</span><span class="sxs-lookup"><span data-stu-id="ecc24-137">Once the user has granted consent, the SSO token can be exchanged for a Graph token without any user interaction.</span></span> <span data-ttu-id="ecc24-138">In diesem Abschnitt implementieren Sie die Zustimmungserfahrung im Add-In mit [msal-browser.](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)</span><span class="sxs-lookup"><span data-stu-id="ecc24-138">In this section you'll implement the consent experience in the add-in using [msal-browser](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser).</span></span>

1. <span data-ttu-id="ecc24-139">Erstellen Sie eine neue Datei im **Verzeichnis "./src/addin"** consent.js **und** fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="ecc24-139">Create a new file in the **./src/addin** directory named **consent.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/consent.js" id="ConsentJsSnippet":::

    <span data-ttu-id="ecc24-140">Dieser Code anmeldet sich für den Benutzer und fordert den Satz von Microsoft Graph-Berechtigungen an, die für die Registrierung der App konfiguriert sind.</span><span class="sxs-lookup"><span data-stu-id="ecc24-140">This code does login for the user, requesting the set of Microsoft Graph permissions that are configured on the app registration.</span></span>

1. <span data-ttu-id="ecc24-141">Erstellen Sie eine neue Datei im Verzeichnis **./src/addin** mit dem Namen **consent.html,** und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="ecc24-141">Create a new file in the **./src/addin** directory named **consent.html** and add the following code.</span></span>

    :::code language="html" source="../demo/graph-tutorial/src/addin/consent.html" id="ConsentHtmlSnippet":::

    <span data-ttu-id="ecc24-142">Dieser Code implementiert eine einfache HTML-Seite, um die **consent.js** laden.</span><span class="sxs-lookup"><span data-stu-id="ecc24-142">This code implements a basic HTML page to load the **consent.js** file.</span></span> <span data-ttu-id="ecc24-143">Diese Seite wird in einem Popupdialogfeld geladen.</span><span class="sxs-lookup"><span data-stu-id="ecc24-143">This page will be loaded in a pop-up dialog.</span></span>

1. <span data-ttu-id="ecc24-144">Speichern Sie alle Änderungen, und starten Sie den Server neu.</span><span class="sxs-lookup"><span data-stu-id="ecc24-144">Save all of your changes and restart the server.</span></span>

1. <span data-ttu-id="ecc24-145">Laden Sie Ihre **manifest.xml** mit den gleichen Schritten in [Side-Load the add-in in Excel erneut hoch.](02-create-app.md#side-load-the-add-in-in-excel)</span><span class="sxs-lookup"><span data-stu-id="ecc24-145">Re-upload your **manifest.xml** file using the same steps in [Side-load the add-in in Excel](02-create-app.md#side-load-the-add-in-in-excel).</span></span>

1. <span data-ttu-id="ecc24-146">Wählen Sie auf **der Registerkarte "Start"** die Schaltfläche "Kalender **importieren"** aus, um den Aufgabenbereich zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="ecc24-146">Select the **Import Calendar** button on the **Home** tab to open the task pane.</span></span>

1. <span data-ttu-id="ecc24-147">Wählen Sie **die Schaltfläche "Berechtigung erteilen"** im Aufgabenbereich aus, um das Zustimmungsdialogfeld in einem Popupfenster zu starten.</span><span class="sxs-lookup"><span data-stu-id="ecc24-147">Select the **Give permission** button in the task pane to launch the consent dialog in a pop-up window.</span></span> <span data-ttu-id="ecc24-148">Melden Sie sich an, und erteilen Sie ihre Zustimmung.</span><span class="sxs-lookup"><span data-stu-id="ecc24-148">Sign in and grant consent.</span></span>

1. <span data-ttu-id="ecc24-149">Der Aufgabenbereich wird mit "Authentifiziert!" aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="ecc24-149">The task pane updates with an "Authenticated!"</span></span> <span data-ttu-id="ecc24-150">Nachricht.</span><span class="sxs-lookup"><span data-stu-id="ecc24-150">message.</span></span> <span data-ttu-id="ecc24-151">Sie können die Token wie folgt überprüfen.</span><span class="sxs-lookup"><span data-stu-id="ecc24-151">You can check the tokens as follows.</span></span>

    - <span data-ttu-id="ecc24-152">In den Entwicklertools Ihres Browsers wird das API-Token in der Konsole angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ecc24-152">In your brower's developer tools, the API token is shown in the Console.</span></span>
    - <span data-ttu-id="ecc24-153">In Ihrer CLI, in der Sie den Node.js ausführen, wird das Graph-Token gedruckt.</span><span class="sxs-lookup"><span data-stu-id="ecc24-153">In your CLI where you are running the Node.js server, the Graph token is printed.</span></span>

    <span data-ttu-id="ecc24-154">Sie können dieses Token unter [https://jwt.ms](https://jwt.ms) vergleichen.</span><span class="sxs-lookup"><span data-stu-id="ecc24-154">You can compare these token at [https://jwt.ms](https://jwt.ms).</span></span> <span data-ttu-id="ecc24-155">Beachten Sie, dass die Zielgruppe des API-Tokens ( ) auf die Anwendungs-ID Ihrer App-Registrierung und der Bereich `aud` ( `scp` ) festgelegt `access_as_user` ist.</span><span class="sxs-lookup"><span data-stu-id="ecc24-155">Notice that the API token's audience (`aud`) is set to the application ID of your app registration, and the scope (`scp`) is `access_as_user`.</span></span>
