---
ms.openlocfilehash: fed56663591ac36e4defcae3a8d0a222f86e3026
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274284"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="0bc7a-101">Ausführen des abgeschlossenen Projekts</span><span class="sxs-lookup"><span data-stu-id="0bc7a-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bc7a-102">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="0bc7a-102">Prerequisites</span></span>

<span data-ttu-id="0bc7a-103">Zum Ausführen des abgeschlossenen Projekts in diesem Ordner benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="0bc7a-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="0bc7a-104">[Node.jsA0 ](https://nodejs.org) und [-2013](https://yarnpkg.com/) auf Ihrem Entwicklungscomputer installiert.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-104">[Node.js](https://nodejs.org) and [Yarn](https://yarnpkg.com/) installed on your development machine.</span></span> <span data-ttu-id="0bc7a-105">(**Hinweis:** Dieses Lernprogramm wurde mit Node Version 14.15.0 und Derzversion 1.22.0 geschrieben.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-105">(**Note:** This tutorial was written with Node version 14.15.0 and Yarn version 1.22.0.</span></span> <span data-ttu-id="0bc7a-106">Die Schritte in diesem Handbuch funktionieren möglicherweise mit anderen Versionen, wurden jedoch noch nicht getestet.)</span><span class="sxs-lookup"><span data-stu-id="0bc7a-106">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="0bc7a-107">Entweder ein persönliches Microsoft-Konto mit einem Postfach auf Outlook.com oder ein Microsoft-Arbeits- oder Schulkonto.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-107">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="0bc7a-108">Wenn Sie kein Microsoft-Konto haben, gibt es mehrere Optionen, um ein kostenloses Konto zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="0bc7a-108">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="0bc7a-109">Sie können [sich für ein neues persönliches Microsoft-Konto registrieren.](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)</span><span class="sxs-lookup"><span data-stu-id="0bc7a-109">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="0bc7a-110">Sie können [sich für das Office 365-Entwicklerprogramm](https://developer.microsoft.com/office/dev-program) registrieren, um ein kostenloses Office 365-Abonnement zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-110">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="0bc7a-111">Registrieren einer Webanwendung beim Azure Active Directory Admin Center</span><span class="sxs-lookup"><span data-stu-id="0bc7a-111">Register a web application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="0bc7a-112">Öffnen Sie einen Browser, und navigieren Sie zum [Azure Active Directory Admin Center](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0bc7a-112">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="0bc7a-113">Melden Sie sich mit einem **persönlichen Konto** (auch: Microsoft-Konto) oder einem **Geschäfts- oder Schulkonto** an.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-113">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="0bc7a-114">Wählen Sie in der linken Navigationsleiste **Azure Active Directory** aus, und wählen Sie dann **App-Registrierungen** unter **Verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-114">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="0bc7a-115">Screenshot der APP-Registrierungen</span><span class="sxs-lookup"><span data-stu-id="0bc7a-115">A screenshot of the App registrations</span></span> ](/tutorial/images/app-registrations.png)

1. <span data-ttu-id="0bc7a-116">Wählen Sie **Neue Registrierung** aus.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-116">Select **New registration**.</span></span> <span data-ttu-id="0bc7a-117">Legen Sie auf der Seite **Anwendung registrieren** die Werte wie folgt fest.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-117">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="0bc7a-118">Legen Sie **Name** auf `Office Add-in Graph Tutorial` fest.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-118">Set **Name** to `Office Add-in Graph Tutorial`.</span></span>
    - <span data-ttu-id="0bc7a-119">Legen Sie **Unterstützte Kontotypen** auf **Konten in allen Organisationsverzeichnissen und persönliche Microsoft-Konten** fest.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-119">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="0bc7a-120">Legen Sie unter **Umleitungs-URI** die erste Dropdownoption auf `Single-page application (SPA)` fest, und legen Sie den Wert auf `https://localhost:3000/consent.html` fest.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-120">Under **Redirect URI**, set the first drop-down to `Single-page application (SPA)` and set the value to `https://localhost:3000/consent.html`.</span></span>

    ![Screenshot der Seite "Anwendung registrieren"](/tutorial/images/register-an-app.png)

1. <span data-ttu-id="0bc7a-122">Wählen Sie **Registrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-122">Select **Register**.</span></span> <span data-ttu-id="0bc7a-123">Kopieren Sie auf der Lernprogrammseite des **Office-Add-In-Diagramms** den Wert der **Anwendungs-ID (Client-ID),** und speichern Sie ihn. Sie benötigen ihn im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-123">On the **Office Add-in Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Screenshot der Anwendungs-ID der neuen App-Registrierung](/tutorial/images/application-id.png)

1. <span data-ttu-id="0bc7a-125">Wählen Sie unter **Verwalten** die Option **Zertifikate und Geheime Clientschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-125">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="0bc7a-126">Wählen Sie die Schaltfläche **Neuen geheimen Clientschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-126">Select the **New client secret** button.</span></span> <span data-ttu-id="0bc7a-127">Geben Sie einen Wert in **Beschreibung** ein, wählen Sie eine der Optionen für **Gilt bis** aus, und wählen Sie dann **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-127">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

1. <span data-ttu-id="0bc7a-128">Kopieren Sie den Wert des geheimen Clientschlüssels, bevor Sie diese Seite verlassen.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-128">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="0bc7a-129">Sie benötigen ihn im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-129">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0bc7a-130">Dieser geheime Clientschlüssel wird nicht noch einmal angezeigt, stellen Sie daher sicher, dass Sie ihn jetzt kopieren.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-130">This client secret is never shown again, so make sure you copy it now.</span></span>

1. <span data-ttu-id="0bc7a-131">Wählen Sie unter **"Verwalten"** die Berechtigung **"API"** und dann **"Berechtigung hinzufügen" aus.**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-131">Select **API permissions** under **Manage**, then select **Add a permission**.</span></span>

1. <span data-ttu-id="0bc7a-132">Wählen **Sie Microsoft Graph** und dann delegierte Berechtigungen **aus.**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-132">Select **Microsoft Graph**, then **Delegated permissions**.</span></span>

1. <span data-ttu-id="0bc7a-133">Wählen Sie die folgenden Berechtigungen und dann "Berechtigungen **hinzufügen" aus.**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-133">Select the following permissions, then select **Add permissions**.</span></span>

    - <span data-ttu-id="0bc7a-134">**Calendars.ReadWrite** – Dadurch kann die App den Kalender des Benutzers lesen und in den Kalender schreiben.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-134">**Calendars.ReadWrite** - this will allow the app to read and write to the user's calendar.</span></span>
    - <span data-ttu-id="0bc7a-135">**MailboxSettings.Read** – Dadurch kann die App die Zeitzone des Benutzers aus seinen Postfacheinstellungen erhalten.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-135">**MailboxSettings.Read** - this will allow the app to get the user's time zone from their mailbox settings.</span></span>

    ![Screenshot der konfigurierten Berechtigungen](/tutorial/images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a><span data-ttu-id="0bc7a-137">Konfigurieren des einmaligen Anmeldens für Office-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="0bc7a-137">Configure Office Add-in single sign-on</span></span>

<span data-ttu-id="0bc7a-138">Aktualisieren Sie die App-Registrierung, um [einmaliges Anmelden (Single Sign-On, SSO) für Office-Add-Ins zu unterstützen.](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins)</span><span class="sxs-lookup"><span data-stu-id="0bc7a-138">Update the app registration to support [Office Add-in single sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins).</span></span>

1. <span data-ttu-id="0bc7a-139">Select **Expose an API**.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-139">Select **Expose an API**.</span></span> <span data-ttu-id="0bc7a-140">Wählen Sie **in den durch diesen ABSCHNITT definierten** Bereiche die Option **"Bereich hinzufügen" aus.**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-140">In the **Scopes defined by this API** section, select **Add a scope**.</span></span> <span data-ttu-id="0bc7a-141">Wenn Sie aufgefordert werden, einen **Anwendungs-ID-URI festlegen,** legen Sie den Wert auf , ersetzt durch `api://localhost:3000/YOUR_APP_ID_HERE` die `YOUR_APP_ID_HERE` Anwendungs-ID.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-141">When prompted to set an **Application ID URI**, set the value to `api://localhost:3000/YOUR_APP_ID_HERE`, replacing `YOUR_APP_ID_HERE` with the application ID.</span></span> <span data-ttu-id="0bc7a-142">Wählen Sie **"Speichern" aus, und fahren Sie fort.**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-142">Choose **Save and continue**.</span></span>

1. <span data-ttu-id="0bc7a-143">Füllen Sie die Felder wie folgt aus, und wählen Sie Bereich **hinzufügen aus.**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-143">Fill in the fields as follows and select **Add scope**.</span></span>

    - <span data-ttu-id="0bc7a-144">**Bereichsname:**`access_as_user`</span><span class="sxs-lookup"><span data-stu-id="0bc7a-144">**Scope name:** `access_as_user`</span></span>
    - <span data-ttu-id="0bc7a-145">**Wer kann zustimmen?: Administratoren und Benutzer**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-145">**Who can consent?: Admins and users**</span></span>
    - <span data-ttu-id="0bc7a-146">**Anzeigename der Administrator-Zustimmung:**`Access the app as the user`</span><span class="sxs-lookup"><span data-stu-id="0bc7a-146">**Admin consent display name:** `Access the app as the user`</span></span>
    - <span data-ttu-id="0bc7a-147">**Beschreibung der Administrator-Zustimmung:**`Allows Office Add-ins to call the app's web APIs as the current user.`</span><span class="sxs-lookup"><span data-stu-id="0bc7a-147">**Admin consent description:** `Allows Office Add-ins to call the app's web APIs as the current user.`</span></span>
    - <span data-ttu-id="0bc7a-148">**Anzeigename der Benutzer zustimmung:**`Access the app as you`</span><span class="sxs-lookup"><span data-stu-id="0bc7a-148">**User consent display name:** `Access the app as you`</span></span>
    - <span data-ttu-id="0bc7a-149">**Beschreibung der Benutzer zustimmung:**`Allows Office Add-ins to call the app's web APIs as you.`</span><span class="sxs-lookup"><span data-stu-id="0bc7a-149">**User consent description:** `Allows Office Add-ins to call the app's web APIs as you.`</span></span>
    - <span data-ttu-id="0bc7a-150">**Status: Aktiviert**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-150">**State: Enabled**</span></span>

    ![Screenshot des Bereichsformulars hinzufügen](/tutorial/images/add-scope.png)

1. <span data-ttu-id="0bc7a-152">Wählen Sie **im Abschnitt "Autorisierte Clientanwendungen"** die Option **"Clientanwendung hinzufügen" aus.**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-152">In the **Authorized client applications** section, select **Add a client application**.</span></span> <span data-ttu-id="0bc7a-153">Geben Sie eine Client-ID aus der folgenden Liste ein, aktivieren Sie den Bereich unter **"Autorisierte Bereiche",** und wählen Sie **"Anwendung hinzufügen" aus.**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-153">Enter a client ID from the following list, enable the scope under **Authorized scopes**, and select **Add application**.</span></span> <span data-ttu-id="0bc7a-154">Wiederholen Sie diesen Vorgang für jede der Client-IDs in der Liste.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-154">Repeat this process for each of the client IDs in the list.</span></span>

    - <span data-ttu-id="0bc7a-155">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="0bc7a-155">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span></span>
    - <span data-ttu-id="0bc7a-156">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="0bc7a-156">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span></span>
    - <span data-ttu-id="0bc7a-157">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office im Web)</span><span class="sxs-lookup"><span data-stu-id="0bc7a-157">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office on the web)</span></span>
    - <span data-ttu-id="0bc7a-158">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office im Web)</span><span class="sxs-lookup"><span data-stu-id="0bc7a-158">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office on the web)</span></span>

## <a name="install-development-certificates"></a><span data-ttu-id="0bc7a-159">Installieren von Entwicklungszertifikaten</span><span class="sxs-lookup"><span data-stu-id="0bc7a-159">Install development certificates</span></span>

1. <span data-ttu-id="0bc7a-160">Führen Sie den folgenden Befehl aus, um Entwicklungszertifikate für Ihr Add-in zu generieren und zu installieren.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-160">Run the following command to generate and install development certificates for your add-in.</span></span>

    ```Shell
    npx office-addin-dev-certs install
    ```

    <span data-ttu-id="0bc7a-161">Bestätigen Sie die Aktionen, wenn Sie zur Bestätigung aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-161">If prompted for confirmation, confirm the actions.</span></span> <span data-ttu-id="0bc7a-162">Sobald der Befehl abgeschlossen ist, wird eine Ausgabe wie die folgende angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-162">Once the command completes, you will see output similar to the following.</span></span>

    ```Shell
    You now have trusted access to https://localhost.
    Certificate: <path>\localhost.crt
    Key: <path>\localhost.key
    ```

1. <span data-ttu-id="0bc7a-163">Kopieren Sie die Pfade zu "localhost.crt" und "localhost.key", sie werden im nächsten Schritt benötigt.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-163">Copy the paths to localhost.crt and localhost.key, you'll need them in the next step.</span></span>

## <a name="update-the-manifest"></a><span data-ttu-id="0bc7a-164">Aktualisieren des Manifests</span><span class="sxs-lookup"><span data-stu-id="0bc7a-164">Update the manifest</span></span>

1. <span data-ttu-id="0bc7a-165">Öffnen Sie **manifest.xml** Datei, und nehmen Sie die folgenden Änderungen vor.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-165">Open the **manifest.xml** file and make the following changes.</span></span>
    1. <span data-ttu-id="0bc7a-166">Ersetzen `NEW_GUID_HERE` Sie diese durch eine neue GUID, z. `b4fa03b8-1eb6-4e8b-a380-e0476be9e019` B. .</span><span class="sxs-lookup"><span data-stu-id="0bc7a-166">Replace `NEW_GUID_HERE` with a new GUID, like `b4fa03b8-1eb6-4e8b-a380-e0476be9e019`.</span></span>
    1. <span data-ttu-id="0bc7a-167">Ersetzen Sie alle Instanzen ihrer `YOUR_APP_ID_HERE` App-Registrierung durch die Anwendungs-ID.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-167">Replace all instances of `YOUR_APP_ID_HERE` with the application ID from your app registration.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="0bc7a-168">Konfigurieren des Beispiels</span><span class="sxs-lookup"><span data-stu-id="0bc7a-168">Configure the sample</span></span>

1. <span data-ttu-id="0bc7a-169">Benennen Sie die `example.env` Datei um in `.env` .</span><span class="sxs-lookup"><span data-stu-id="0bc7a-169">Rename the `example.env` file to `.env`.</span></span>
1. <span data-ttu-id="0bc7a-170">Bearbeiten Sie `.env` die Datei, und nehmen Sie die folgenden Änderungen vor.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-170">Edit the `.env` file and make the following changes.</span></span>
    1. <span data-ttu-id="0bc7a-171">Ersetzen `YOUR_APP_ID_HERE` Sie diese durch die **Anwendungs-ID,** die Sie aus dem App-Registrierungsportal erhalten haben.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-171">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
    1. <span data-ttu-id="0bc7a-172">Ersetzen `YOUR_CLIENT_SECRET_HERE` Sie den geheimen Clientgeheimnis, den Sie aus dem App-Registrierungsportal erhalten haben.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-172">Replace `YOUR_CLIENT_SECRET_HERE` with the client secret you got from the App Registration Portal.</span></span>
    1. <span data-ttu-id="0bc7a-173">Ersetzen `PATH_TO_LOCALHOST.CRT` Sie dies durch den Pfad zur Datei "localhost.crt" aus der Ausgabe des `npx office-addin-dev-certs install` Befehls.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-173">Replace `PATH_TO_LOCALHOST.CRT` with the path to your localhost.crt file from the output of the `npx office-addin-dev-certs install` command.</span></span>
    1. <span data-ttu-id="0bc7a-174">Ersetzen `PATH_TO_LOCALHOST.KEY` Sie dies durch den Pfad zur Datei "localhost.key" aus der Ausgabe des `npx office-addin-dev-certs install` Befehls.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-174">Replace `PATH_TO_LOCALHOST.KEY` with the path to your localhost.key file from the output of the `npx office-addin-dev-certs install` command.</span></span>

1. <span data-ttu-id="0bc7a-175">Benennen Sie die `config.example.js` Datei um in `config.js` .</span><span class="sxs-lookup"><span data-stu-id="0bc7a-175">Rename the `config.example.js` file to `config.js`.</span></span>
1. <span data-ttu-id="0bc7a-176">Bearbeiten Sie `config.js` die Datei, und nehmen Sie die folgenden Änderungen vor.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-176">Edit the `config.js` file and make the following changes.</span></span>
    1. <span data-ttu-id="0bc7a-177">Ersetzen `YOUR_APP_ID_HERE` Sie diese durch die **Anwendungs-ID,** die Sie aus dem App-Registrierungsportal erhalten haben.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-177">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
1. <span data-ttu-id="0bc7a-178">Navigieren Sie in der Befehlszeilenschnittstelle (CLI) zu diesem Verzeichnis, und führen Sie den folgenden Befehl aus, um die Installationsanforderungen zu erfüllen.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-178">In your command-line interface (CLI), navigate to this directory and run the following command to install requirements.</span></span>

    ```Shell
    yarn install
    ```

## <a name="run-the-sample"></a><span data-ttu-id="0bc7a-179">Ausführen des Beispiels</span><span class="sxs-lookup"><span data-stu-id="0bc7a-179">Run the sample</span></span>

1. <span data-ttu-id="0bc7a-180">Führen Sie den folgenden Befehl in Ihrer CLI aus, um die Anwendung zu starten.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-180">Run the following command in your CLI to start the application.</span></span>

    ```Shell
    yarn start
    ```

1. <span data-ttu-id="0bc7a-181">Wechseln Sie in Ihrem Browser zu [Office.com](https://www.office.com/) und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-181">In your browser, go to [Office.com](https://www.office.com/) and sign in.</span></span> <span data-ttu-id="0bc7a-182">Wählen **Sie auf** der linken Symbolleiste "Erstellen" und dann "Tabelle" **aus.**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-182">Select **Create** in the left-hand toolbar, then select **Spreadsheet**.</span></span>

    ![Screenshot des Menüs "Erstellen" auf Office.com](/tutorial/images/office-select-excel.png)

1. <span data-ttu-id="0bc7a-184">Wählen Sie die **Registerkarte** "Einfügen" und dann **"Office-Add-Ins" aus.**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-184">Select the **Insert** tab, then select **Office Add-ins**.</span></span>

1. <span data-ttu-id="0bc7a-185">Wählen **Sie "Mein Add-In hochladen"** und dann **"Durchsuchen" aus.**</span><span class="sxs-lookup"><span data-stu-id="0bc7a-185">Select **Upload My Add-in**, then select **Browse**.</span></span> <span data-ttu-id="0bc7a-186">Laden Sie ihre **manifest.xml** hoch.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-186">Upload your **manifest.xml** file.</span></span>

1. <span data-ttu-id="0bc7a-187">Wählen Sie **auf der Registerkarte "Start"** die Schaltfläche "Kalender **importieren"** aus, um den Aufgabenfeld zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="0bc7a-187">Select the **Import Calendar** button on the **Home** tab to open the taskpane.</span></span>

    ![Screenshot der Schaltfläche "Kalender importieren" auf der Registerkarte "Start"](/tutorial/images/get-started.png)
