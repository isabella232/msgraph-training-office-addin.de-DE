---
ms.openlocfilehash: 89bc4baff47ae895c7c0dfd34a8f8d4d0da091f5
ms.sourcegitcommit: 8a65c826f6b229c287a782d784b6d9629aa5a3d0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/20/2021
ms.locfileid: "51899433"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="e03df-101">In dieser Übung erstellen Sie eine neue Azure AD-Webanwendungsregistrierung mit dem Azure Active Directory Admin Center.</span><span class="sxs-lookup"><span data-stu-id="e03df-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="e03df-102">Öffnen Sie einen Browser, und navigieren Sie zum [Azure Active Directory Admin Center](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e03df-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="e03df-103">Melden Sie sich mit einem **persönlichen Konto** (auch: Microsoft-Konto) oder einem **Geschäfts- oder Schulkonto** an.</span><span class="sxs-lookup"><span data-stu-id="e03df-103">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="e03df-104">Wählen Sie in der linken Navigationsleiste **Azure Active Directory** aus, und wählen Sie dann **App-Registrierungen** unter **Verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="e03df-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="e03df-105">Screenshot der APP-Registrierungen</span><span class="sxs-lookup"><span data-stu-id="e03df-105">A screenshot of the App registrations</span></span> ](images/app-registrations.png)

1. <span data-ttu-id="e03df-106">Wählen Sie **Neue Registrierung** aus.</span><span class="sxs-lookup"><span data-stu-id="e03df-106">Select **New registration**.</span></span> <span data-ttu-id="e03df-107">Legen Sie auf der Seite **Anwendung registrieren** die Werte wie folgt fest.</span><span class="sxs-lookup"><span data-stu-id="e03df-107">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="e03df-108">Legen Sie **Name** auf `Office Add-in Graph Tutorial` fest.</span><span class="sxs-lookup"><span data-stu-id="e03df-108">Set **Name** to `Office Add-in Graph Tutorial`.</span></span>
    - <span data-ttu-id="e03df-109">Legen Sie **Unterstützte Kontotypen** auf **Konten in allen Organisationsverzeichnissen und persönliche Microsoft-Konten** fest.</span><span class="sxs-lookup"><span data-stu-id="e03df-109">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="e03df-110">Legen Sie unter **Umleitungs-URI** die erste Dropdownoption auf `Single-page application (SPA)` fest, und legen Sie den Wert auf `https://localhost:3000/consent.html` fest.</span><span class="sxs-lookup"><span data-stu-id="e03df-110">Under **Redirect URI**, set the first drop-down to `Single-page application (SPA)` and set the value to `https://localhost:3000/consent.html`.</span></span>

    ![Screenshot der Seite "Anwendung registrieren"](images/register-an-app.png)

1. <span data-ttu-id="e03df-112">Wählen Sie **Registrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="e03df-112">Select **Register**.</span></span> <span data-ttu-id="e03df-113">Kopieren Sie auf der **Seite Office-Add-In-Graph-Lernprogramm** den Wert der **Anwendungs-ID (Client-ID),** und speichern Sie sie, sie benötigen Sie im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="e03df-113">On the **Office Add-in Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Screenshot der Anwendungs-ID der neuen App-Registrierung](images/application-id.png)

1. <span data-ttu-id="e03df-115">Wählen Sie unter **Verwalten** die Option **Authentifizierung** aus.</span><span class="sxs-lookup"><span data-stu-id="e03df-115">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="e03df-116">Suchen Sie den **Abschnitt Implizite** Erteilung, und aktivieren **Sie Zugriffstoken und** **ID-Token.**</span><span class="sxs-lookup"><span data-stu-id="e03df-116">Locate the **Implicit grant** section and enable **Access tokens** and **ID tokens**.</span></span> <span data-ttu-id="e03df-117">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="e03df-117">Select **Save**.</span></span>

    ![Screenshot des Abschnitts "Implizite Gewährung"](./images/aad-implicit-grant.png)

1. <span data-ttu-id="e03df-119">Wählen Sie unter **Verwalten** die Option **Zertifikate und Geheime Clientschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="e03df-119">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="e03df-120">Wählen Sie die Schaltfläche **Neuen geheimen Clientschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="e03df-120">Select the **New client secret** button.</span></span> <span data-ttu-id="e03df-121">Geben Sie einen Wert in **Beschreibung** ein, wählen Sie eine der Optionen für **Gilt bis** aus, und wählen Sie dann **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="e03df-121">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

1. <span data-ttu-id="e03df-122">Kopieren Sie den Wert des geheimen Clientschlüssels, bevor Sie diese Seite verlassen.</span><span class="sxs-lookup"><span data-stu-id="e03df-122">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="e03df-123">Sie benötigen ihn im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="e03df-123">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e03df-124">Dieser geheime Clientschlüssel wird nicht noch einmal angezeigt, stellen Sie daher sicher, dass Sie ihn jetzt kopieren.</span><span class="sxs-lookup"><span data-stu-id="e03df-124">This client secret is never shown again, so make sure you copy it now.</span></span>

1. <span data-ttu-id="e03df-125">Wählen **Sie unter** Verwalten die Option **API-Berechtigungen** aus, und wählen Sie dann Berechtigung **hinzufügen aus.**</span><span class="sxs-lookup"><span data-stu-id="e03df-125">Select **API permissions** under **Manage**, then select **Add a permission**.</span></span>

1. <span data-ttu-id="e03df-126">Wählen **Sie Microsoft Graph** und dann Delegierte Berechtigungen **aus.**</span><span class="sxs-lookup"><span data-stu-id="e03df-126">Select **Microsoft Graph**, then **Delegated permissions**.</span></span>

1. <span data-ttu-id="e03df-127">Wählen Sie die folgenden Berechtigungen aus, und wählen Sie **dann Berechtigungen hinzufügen aus.**</span><span class="sxs-lookup"><span data-stu-id="e03df-127">Select the following permissions, then select **Add permissions**.</span></span>

    - <span data-ttu-id="e03df-128">**offline_access** : Dadurch kann die App Zugriffstoken aktualisieren, wenn sie ablaufen.</span><span class="sxs-lookup"><span data-stu-id="e03df-128">**offline_access** - this will allow the app to refresh access tokens when they expire.</span></span>
    - <span data-ttu-id="e03df-129">**Calendars.ReadWrite** – dadurch kann die App den Kalender des Benutzers lesen und schreiben.</span><span class="sxs-lookup"><span data-stu-id="e03df-129">**Calendars.ReadWrite** - this will allow the app to read and write to the user's calendar.</span></span>
    - <span data-ttu-id="e03df-130">**MailboxSettings.Read** – Dadurch kann die App die Zeitzone des Benutzers aus den Postfacheinstellungen erhalten.</span><span class="sxs-lookup"><span data-stu-id="e03df-130">**MailboxSettings.Read** - this will allow the app to get the user's time zone from their mailbox settings.</span></span>

    ![Screenshot der konfigurierten Berechtigungen](images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a><span data-ttu-id="e03df-132">Konfigurieren des einmaligen Anmeldens für Office-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="e03df-132">Configure Office Add-in single sign-on</span></span>

<span data-ttu-id="e03df-133">In diesem Abschnitt aktualisieren Sie die App-Registrierung, um [office add-in single sign-on (SSO) zu unterstützen.](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins)</span><span class="sxs-lookup"><span data-stu-id="e03df-133">In this section you'll update the app registration to support [Office Add-in single sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins).</span></span>

1. <span data-ttu-id="e03df-134">Wählen Sie **API verfügbar machen aus.**</span><span class="sxs-lookup"><span data-stu-id="e03df-134">Select **Expose an API**.</span></span> <span data-ttu-id="e03df-135">Wählen Sie **im Abschnitt Durch diese API definierte** Bereiche die Option Bereich hinzufügen **aus.**</span><span class="sxs-lookup"><span data-stu-id="e03df-135">In the **Scopes defined by this API** section, select **Add a scope**.</span></span> <span data-ttu-id="e03df-136">Wenn Sie zum Festlegen eines **Anwendungs-ID-URI** aufgefordert werden, legen Sie den Wert auf , und ersetzen Sie durch `api://localhost:3000/YOUR_APP_ID_HERE` die `YOUR_APP_ID_HERE` Anwendungs-ID.</span><span class="sxs-lookup"><span data-stu-id="e03df-136">When prompted to set an **Application ID URI**, set the value to `api://localhost:3000/YOUR_APP_ID_HERE`, replacing `YOUR_APP_ID_HERE` with the application ID.</span></span> <span data-ttu-id="e03df-137">Wählen **Sie Speichern aus, und fahren Sie fort.**</span><span class="sxs-lookup"><span data-stu-id="e03df-137">Choose **Save and continue**.</span></span>

1. <span data-ttu-id="e03df-138">Füllen Sie die Felder wie folgt aus, und wählen **Sie Bereich hinzufügen aus.**</span><span class="sxs-lookup"><span data-stu-id="e03df-138">Fill in the fields as follows and select **Add scope**.</span></span>

    - <span data-ttu-id="e03df-139">**Bereichsname:**`access_as_user`</span><span class="sxs-lookup"><span data-stu-id="e03df-139">**Scope name:** `access_as_user`</span></span>
    - <span data-ttu-id="e03df-140">**Wer kann zustimmen?: Administratoren und Benutzer**</span><span class="sxs-lookup"><span data-stu-id="e03df-140">**Who can consent?: Admins and users**</span></span>
    - <span data-ttu-id="e03df-141">**Anzeigename der Administrator-Zustimmung:**`Access the app as the user`</span><span class="sxs-lookup"><span data-stu-id="e03df-141">**Admin consent display name:** `Access the app as the user`</span></span>
    - <span data-ttu-id="e03df-142">**Administrator-Zustimmungsbeschreibung:**`Allows Office Add-ins to call the app's web APIs as the current user.`</span><span class="sxs-lookup"><span data-stu-id="e03df-142">**Admin consent description:** `Allows Office Add-ins to call the app's web APIs as the current user.`</span></span>
    - <span data-ttu-id="e03df-143">**Anzeigename der Benutzer zustimmung:**`Access the app as you`</span><span class="sxs-lookup"><span data-stu-id="e03df-143">**User consent display name:** `Access the app as you`</span></span>
    - <span data-ttu-id="e03df-144">**Benutzer-Zustimmungsbeschreibung:**`Allows Office Add-ins to call the app's web APIs as you.`</span><span class="sxs-lookup"><span data-stu-id="e03df-144">**User consent description:** `Allows Office Add-ins to call the app's web APIs as you.`</span></span>
    - <span data-ttu-id="e03df-145">**Status: Aktiviert**</span><span class="sxs-lookup"><span data-stu-id="e03df-145">**State: Enabled**</span></span>

    ![Screenshot des Bereichsformulars hinzufügen](images/add-scope.png)

1. <span data-ttu-id="e03df-147">Wählen Sie **im Abschnitt Autorisierte Clientanwendungen** die Option **Clientanwendung hinzufügen aus.**</span><span class="sxs-lookup"><span data-stu-id="e03df-147">In the **Authorized client applications** section, select **Add a client application**.</span></span> <span data-ttu-id="e03df-148">Geben Sie eine Client-ID aus der folgenden Liste ein, aktivieren Sie den Bereich unter **Autorisierte** Bereiche, und wählen Sie **Anwendung hinzufügen aus.**</span><span class="sxs-lookup"><span data-stu-id="e03df-148">Enter a client ID from the following list, enable the scope under **Authorized scopes**, and select **Add application**.</span></span> <span data-ttu-id="e03df-149">Wiederholen Sie diesen Vorgang für alle Client-IDs in der Liste.</span><span class="sxs-lookup"><span data-stu-id="e03df-149">Repeat this process for each of the client IDs in the list.</span></span>

    - <span data-ttu-id="e03df-150">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="e03df-150">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span></span>
    - <span data-ttu-id="e03df-151">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="e03df-151">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span></span>
    - <span data-ttu-id="e03df-152">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office im Web)</span><span class="sxs-lookup"><span data-stu-id="e03df-152">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office on the web)</span></span>
    - <span data-ttu-id="e03df-153">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office im Web)</span><span class="sxs-lookup"><span data-stu-id="e03df-153">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office on the web)</span></span>
