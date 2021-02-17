---
ms.openlocfilehash: a336095a238eefeae22dac86d29e3140e8d94bf1
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274263"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="a2a02-101">In dieser Übung erstellen Sie eine neue Azure AD-Webanwendungsregistrierung mithilfe des Azure Active Directory Admin Centers.</span><span class="sxs-lookup"><span data-stu-id="a2a02-101">In this exercise, you will create a new Azure AD web application registration using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="a2a02-102">Öffnen Sie einen Browser, und navigieren Sie zum [Azure Active Directory Admin Center](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2a02-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="a2a02-103">Melden Sie sich mit einem **persönlichen Konto** (auch: Microsoft-Konto) oder einem **Geschäfts- oder Schulkonto** an.</span><span class="sxs-lookup"><span data-stu-id="a2a02-103">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="a2a02-104">Wählen Sie in der linken Navigationsleiste **Azure Active Directory** aus, und wählen Sie dann **App-Registrierungen** unter **Verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="a2a02-104">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="a2a02-105">Screenshot der APP-Registrierungen</span><span class="sxs-lookup"><span data-stu-id="a2a02-105">A screenshot of the App registrations</span></span> ](images/app-registrations.png)

1. <span data-ttu-id="a2a02-106">Wählen Sie **Neue Registrierung** aus.</span><span class="sxs-lookup"><span data-stu-id="a2a02-106">Select **New registration**.</span></span> <span data-ttu-id="a2a02-107">Legen Sie auf der Seite **Anwendung registrieren** die Werte wie folgt fest.</span><span class="sxs-lookup"><span data-stu-id="a2a02-107">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="a2a02-108">Legen Sie **Name** auf `Office Add-in Graph Tutorial` fest.</span><span class="sxs-lookup"><span data-stu-id="a2a02-108">Set **Name** to `Office Add-in Graph Tutorial`.</span></span>
    - <span data-ttu-id="a2a02-109">Legen Sie **Unterstützte Kontotypen** auf **Konten in allen Organisationsverzeichnissen und persönliche Microsoft-Konten** fest.</span><span class="sxs-lookup"><span data-stu-id="a2a02-109">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="a2a02-110">Legen Sie unter **Umleitungs-URI** die erste Dropdownoption auf `Single-page application (SPA)` fest, und legen Sie den Wert auf `https://localhost:3000/consent.html` fest.</span><span class="sxs-lookup"><span data-stu-id="a2a02-110">Under **Redirect URI**, set the first drop-down to `Single-page application (SPA)` and set the value to `https://localhost:3000/consent.html`.</span></span>

    ![Screenshot der Seite "Anwendung registrieren"](images/register-an-app.png)

1. <span data-ttu-id="a2a02-112">Wählen Sie **Registrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="a2a02-112">Select **Register**.</span></span> <span data-ttu-id="a2a02-113">Kopieren Sie auf der Lernprogrammseite des **Office-Add-In-Diagramms** den Wert der **Anwendungs-ID (Client-ID),** und speichern Sie ihn. Sie benötigen ihn im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="a2a02-113">On the **Office Add-in Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Screenshot der Anwendungs-ID der neuen App-Registrierung](images/application-id.png)

1. <span data-ttu-id="a2a02-115">Wählen Sie unter **Verwalten** die Option **Zertifikate und Geheime Clientschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="a2a02-115">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="a2a02-116">Wählen Sie die Schaltfläche **Neuen geheimen Clientschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="a2a02-116">Select the **New client secret** button.</span></span> <span data-ttu-id="a2a02-117">Geben Sie einen Wert in **Beschreibung** ein, wählen Sie eine der Optionen für **Gilt bis** aus, und wählen Sie dann **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="a2a02-117">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

1. <span data-ttu-id="a2a02-118">Kopieren Sie den Wert des geheimen Clientschlüssels, bevor Sie diese Seite verlassen.</span><span class="sxs-lookup"><span data-stu-id="a2a02-118">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="a2a02-119">Sie benötigen ihn im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="a2a02-119">You will need it in the next step.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a2a02-120">Dieser geheime Clientschlüssel wird nicht noch einmal angezeigt, stellen Sie daher sicher, dass Sie ihn jetzt kopieren.</span><span class="sxs-lookup"><span data-stu-id="a2a02-120">This client secret is never shown again, so make sure you copy it now.</span></span>

1. <span data-ttu-id="a2a02-121">Wählen Sie **unter** **"Verwalten"** die BERECHTIGUNG "API-Berechtigungen" und dann **"Berechtigung hinzufügen" aus.**</span><span class="sxs-lookup"><span data-stu-id="a2a02-121">Select **API permissions** under **Manage**, then select **Add a permission**.</span></span>

1. <span data-ttu-id="a2a02-122">Wählen **Sie Microsoft Graph** und dann delegierte Berechtigungen **aus.**</span><span class="sxs-lookup"><span data-stu-id="a2a02-122">Select **Microsoft Graph**, then **Delegated permissions**.</span></span>

1. <span data-ttu-id="a2a02-123">Wählen Sie die folgenden Berechtigungen und dann "Berechtigungen **hinzufügen" aus.**</span><span class="sxs-lookup"><span data-stu-id="a2a02-123">Select the following permissions, then select **Add permissions**.</span></span>

    - <span data-ttu-id="a2a02-124">**offline_access** - Dadurch kann die App Zugriffstoken aktualisieren, wenn sie ablaufen.</span><span class="sxs-lookup"><span data-stu-id="a2a02-124">**offline_access** - this will allow the app to refresh access tokens when they expire.</span></span>
    - <span data-ttu-id="a2a02-125">**Calendars.ReadWrite** – Dadurch kann die App den Kalender des Benutzers lesen und in den Kalender schreiben.</span><span class="sxs-lookup"><span data-stu-id="a2a02-125">**Calendars.ReadWrite** - this will allow the app to read and write to the user's calendar.</span></span>
    - <span data-ttu-id="a2a02-126">**MailboxSettings.Read** – Dadurch kann die App die Zeitzone des Benutzers aus seinen Postfacheinstellungen erhalten.</span><span class="sxs-lookup"><span data-stu-id="a2a02-126">**MailboxSettings.Read** - this will allow the app to get the user's time zone from their mailbox settings.</span></span>

    ![Screenshot der konfigurierten Berechtigungen](images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a><span data-ttu-id="a2a02-128">Konfigurieren des einmaligen Anmeldens für Office-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="a2a02-128">Configure Office Add-in single sign-on</span></span>

<span data-ttu-id="a2a02-129">In diesem Abschnitt aktualisieren Sie die App-Registrierung, um [einmaliges Anmelden (Single Sign-On, SSO) für Office-Add-Ins zu unterstützen.](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins)</span><span class="sxs-lookup"><span data-stu-id="a2a02-129">In this section you'll update the app registration to support [Office Add-in single sign-on (SSO)](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins).</span></span>

1. <span data-ttu-id="a2a02-130">Select **Expose an API**.</span><span class="sxs-lookup"><span data-stu-id="a2a02-130">Select **Expose an API**.</span></span> <span data-ttu-id="a2a02-131">Wählen Sie **in den durch diesen ABSCHNITT definierten** Bereiche die Option **"Bereich hinzufügen" aus.**</span><span class="sxs-lookup"><span data-stu-id="a2a02-131">In the **Scopes defined by this API** section, select **Add a scope**.</span></span> <span data-ttu-id="a2a02-132">Wenn Sie aufgefordert werden, einen **Anwendungs-ID-URI festlegen,** legen Sie den Wert auf , ersetzt durch `api://localhost:3000/YOUR_APP_ID_HERE` die `YOUR_APP_ID_HERE` Anwendungs-ID.</span><span class="sxs-lookup"><span data-stu-id="a2a02-132">When prompted to set an **Application ID URI**, set the value to `api://localhost:3000/YOUR_APP_ID_HERE`, replacing `YOUR_APP_ID_HERE` with the application ID.</span></span> <span data-ttu-id="a2a02-133">Wählen Sie **"Speichern" aus, und fahren Sie fort.**</span><span class="sxs-lookup"><span data-stu-id="a2a02-133">Choose **Save and continue**.</span></span>

1. <span data-ttu-id="a2a02-134">Füllen Sie die Felder wie folgt aus, und wählen Sie Bereich **hinzufügen aus.**</span><span class="sxs-lookup"><span data-stu-id="a2a02-134">Fill in the fields as follows and select **Add scope**.</span></span>

    - <span data-ttu-id="a2a02-135">**Bereichsname:**`access_as_user`</span><span class="sxs-lookup"><span data-stu-id="a2a02-135">**Scope name:** `access_as_user`</span></span>
    - <span data-ttu-id="a2a02-136">**Wer kann zustimmen?: Administratoren und Benutzer**</span><span class="sxs-lookup"><span data-stu-id="a2a02-136">**Who can consent?: Admins and users**</span></span>
    - <span data-ttu-id="a2a02-137">**Anzeigename der Administrator-Zustimmung:**`Access the app as the user`</span><span class="sxs-lookup"><span data-stu-id="a2a02-137">**Admin consent display name:** `Access the app as the user`</span></span>
    - <span data-ttu-id="a2a02-138">**Beschreibung der Administrator-Zustimmung:**`Allows Office Add-ins to call the app's web APIs as the current user.`</span><span class="sxs-lookup"><span data-stu-id="a2a02-138">**Admin consent description:** `Allows Office Add-ins to call the app's web APIs as the current user.`</span></span>
    - <span data-ttu-id="a2a02-139">**Anzeigename der Benutzer zustimmung:**`Access the app as you`</span><span class="sxs-lookup"><span data-stu-id="a2a02-139">**User consent display name:** `Access the app as you`</span></span>
    - <span data-ttu-id="a2a02-140">**Beschreibung der Benutzer zustimmung:**`Allows Office Add-ins to call the app's web APIs as you.`</span><span class="sxs-lookup"><span data-stu-id="a2a02-140">**User consent description:** `Allows Office Add-ins to call the app's web APIs as you.`</span></span>
    - <span data-ttu-id="a2a02-141">**Status: Aktiviert**</span><span class="sxs-lookup"><span data-stu-id="a2a02-141">**State: Enabled**</span></span>

    ![Screenshot des Bereichsformulars hinzufügen](images/add-scope.png)

1. <span data-ttu-id="a2a02-143">Wählen Sie **im Abschnitt "Autorisierte Clientanwendungen"** die Option **"Clientanwendung hinzufügen" aus.**</span><span class="sxs-lookup"><span data-stu-id="a2a02-143">In the **Authorized client applications** section, select **Add a client application**.</span></span> <span data-ttu-id="a2a02-144">Geben Sie eine Client-ID aus der folgenden Liste ein, aktivieren Sie den Bereich unter **"Autorisierte Bereiche",** und wählen Sie **"Anwendung hinzufügen" aus.**</span><span class="sxs-lookup"><span data-stu-id="a2a02-144">Enter a client ID from the following list, enable the scope under **Authorized scopes**, and select **Add application**.</span></span> <span data-ttu-id="a2a02-145">Wiederholen Sie diesen Vorgang für alle Client-IDs in der Liste.</span><span class="sxs-lookup"><span data-stu-id="a2a02-145">Repeat this process for each of the client IDs in the list.</span></span>

    - <span data-ttu-id="a2a02-146">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="a2a02-146">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span></span>
    - <span data-ttu-id="a2a02-147">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="a2a02-147">`ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)</span></span>
    - <span data-ttu-id="a2a02-148">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office im Web)</span><span class="sxs-lookup"><span data-stu-id="a2a02-148">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office on the web)</span></span>
    - <span data-ttu-id="a2a02-149">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office im Web)</span><span class="sxs-lookup"><span data-stu-id="a2a02-149">`08e18876-6177-487e-b8b5-cf950c1e598c` (Office on the web)</span></span>
