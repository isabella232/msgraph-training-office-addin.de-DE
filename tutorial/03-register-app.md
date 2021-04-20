---
ms.openlocfilehash: 89bc4baff47ae895c7c0dfd34a8f8d4d0da091f5
ms.sourcegitcommit: 8a65c826f6b229c287a782d784b6d9629aa5a3d0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/20/2021
ms.locfileid: "51899433"
---
<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung erstellen Sie eine neue Azure AD-Webanwendungsregistrierung mit dem Azure Active Directory Admin Center.

1. Öffnen Sie einen Browser, und navigieren Sie zum [Azure Active Directory Admin Center](https://aad.portal.azure.com). Melden Sie sich mit einem **persönlichen Konto** (auch: Microsoft-Konto) oder einem **Geschäfts- oder Schulkonto** an.

1. Wählen Sie in der linken Navigationsleiste **Azure Active Directory** aus, und wählen Sie dann **App-Registrierungen** unter **Verwalten** aus.

    ![Screenshot der APP-Registrierungen ](images/app-registrations.png)

1. Wählen Sie **Neue Registrierung** aus. Legen Sie auf der Seite **Anwendung registrieren** die Werte wie folgt fest.

    - Legen Sie **Name** auf `Office Add-in Graph Tutorial` fest.
    - Legen Sie **Unterstützte Kontotypen** auf **Konten in allen Organisationsverzeichnissen und persönliche Microsoft-Konten** fest.
    - Legen Sie unter **Umleitungs-URI** die erste Dropdownoption auf `Single-page application (SPA)` fest, und legen Sie den Wert auf `https://localhost:3000/consent.html` fest.

    ![Screenshot der Seite "Anwendung registrieren"](images/register-an-app.png)

1. Wählen Sie **Registrieren** aus. Kopieren Sie auf der **Seite Office-Add-In-Graph-Lernprogramm** den Wert der **Anwendungs-ID (Client-ID),** und speichern Sie sie, sie benötigen Sie im nächsten Schritt.

    ![Screenshot der Anwendungs-ID der neuen App-Registrierung](images/application-id.png)

1. Wählen Sie unter **Verwalten** die Option **Authentifizierung** aus. Suchen Sie den **Abschnitt Implizite** Erteilung, und aktivieren **Sie Zugriffstoken und** **ID-Token.** Klicken Sie auf **Speichern**.

    ![Screenshot des Abschnitts "Implizite Gewährung"](./images/aad-implicit-grant.png)

1. Wählen Sie unter **Verwalten** die Option **Zertifikate und Geheime Clientschlüssel** aus. Wählen Sie die Schaltfläche **Neuen geheimen Clientschlüssel** aus. Geben Sie einen Wert in **Beschreibung** ein, wählen Sie eine der Optionen für **Gilt bis** aus, und wählen Sie dann **Hinzufügen** aus.

1. Kopieren Sie den Wert des geheimen Clientschlüssels, bevor Sie diese Seite verlassen. Sie benötigen ihn im nächsten Schritt.

    > [!IMPORTANT]
    > Dieser geheime Clientschlüssel wird nicht noch einmal angezeigt, stellen Sie daher sicher, dass Sie ihn jetzt kopieren.

1. Wählen **Sie unter** Verwalten die Option **API-Berechtigungen** aus, und wählen Sie dann Berechtigung **hinzufügen aus.**

1. Wählen **Sie Microsoft Graph** und dann Delegierte Berechtigungen **aus.**

1. Wählen Sie die folgenden Berechtigungen aus, und wählen Sie **dann Berechtigungen hinzufügen aus.**

    - **offline_access** : Dadurch kann die App Zugriffstoken aktualisieren, wenn sie ablaufen.
    - **Calendars.ReadWrite** – dadurch kann die App den Kalender des Benutzers lesen und schreiben.
    - **MailboxSettings.Read** – Dadurch kann die App die Zeitzone des Benutzers aus den Postfacheinstellungen erhalten.

    ![Screenshot der konfigurierten Berechtigungen](images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a>Konfigurieren des einmaligen Anmeldens für Office-Add-Ins

In diesem Abschnitt aktualisieren Sie die App-Registrierung, um [office add-in single sign-on (SSO) zu unterstützen.](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins)

1. Wählen Sie **API verfügbar machen aus.** Wählen Sie **im Abschnitt Durch diese API definierte** Bereiche die Option Bereich hinzufügen **aus.** Wenn Sie zum Festlegen eines **Anwendungs-ID-URI** aufgefordert werden, legen Sie den Wert auf , und ersetzen Sie durch `api://localhost:3000/YOUR_APP_ID_HERE` die `YOUR_APP_ID_HERE` Anwendungs-ID. Wählen **Sie Speichern aus, und fahren Sie fort.**

1. Füllen Sie die Felder wie folgt aus, und wählen **Sie Bereich hinzufügen aus.**

    - **Bereichsname:**`access_as_user`
    - **Wer kann zustimmen?: Administratoren und Benutzer**
    - **Anzeigename der Administrator-Zustimmung:**`Access the app as the user`
    - **Administrator-Zustimmungsbeschreibung:**`Allows Office Add-ins to call the app's web APIs as the current user.`
    - **Anzeigename der Benutzer zustimmung:**`Access the app as you`
    - **Benutzer-Zustimmungsbeschreibung:**`Allows Office Add-ins to call the app's web APIs as you.`
    - **Status: Aktiviert**

    ![Screenshot des Bereichsformulars hinzufügen](images/add-scope.png)

1. Wählen Sie **im Abschnitt Autorisierte Clientanwendungen** die Option **Clientanwendung hinzufügen aus.** Geben Sie eine Client-ID aus der folgenden Liste ein, aktivieren Sie den Bereich unter **Autorisierte** Bereiche, und wählen Sie **Anwendung hinzufügen aus.** Wiederholen Sie diesen Vorgang für alle Client-IDs in der Liste.

    - `d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)
    - `ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)
    - `57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office im Web)
    - `08e18876-6177-487e-b8b5-cf950c1e598c` (Office im Web)
