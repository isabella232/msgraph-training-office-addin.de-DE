---
ms.openlocfilehash: fed56663591ac36e4defcae3a8d0a222f86e3026
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274284"
---
# <a name="how-to-run-the-completed-project"></a>Ausführen des abgeschlossenen Projekts

## <a name="prerequisites"></a>Voraussetzungen

Zum Ausführen des abgeschlossenen Projekts in diesem Ordner benötigen Sie Folgendes:

- [Node.jsA0 ](https://nodejs.org) und [-2013](https://yarnpkg.com/) auf Ihrem Entwicklungscomputer installiert. (**Hinweis:** Dieses Lernprogramm wurde mit Node Version 14.15.0 und Derzversion 1.22.0 geschrieben. Die Schritte in diesem Handbuch funktionieren möglicherweise mit anderen Versionen, wurden jedoch noch nicht getestet.)
- Entweder ein persönliches Microsoft-Konto mit einem Postfach auf Outlook.com oder ein Microsoft-Arbeits- oder Schulkonto.

Wenn Sie kein Microsoft-Konto haben, gibt es mehrere Optionen, um ein kostenloses Konto zu erhalten:

- Sie können [sich für ein neues persönliches Microsoft-Konto registrieren.](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)
- Sie können [sich für das Office 365-Entwicklerprogramm](https://developer.microsoft.com/office/dev-program) registrieren, um ein kostenloses Office 365-Abonnement zu erhalten.

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a>Registrieren einer Webanwendung beim Azure Active Directory Admin Center

1. Öffnen Sie einen Browser, und navigieren Sie zum [Azure Active Directory Admin Center](https://aad.portal.azure.com). Melden Sie sich mit einem **persönlichen Konto** (auch: Microsoft-Konto) oder einem **Geschäfts- oder Schulkonto** an.

1. Wählen Sie in der linken Navigationsleiste **Azure Active Directory** aus, und wählen Sie dann **App-Registrierungen** unter **Verwalten** aus.

    ![Screenshot der APP-Registrierungen ](/tutorial/images/app-registrations.png)

1. Wählen Sie **Neue Registrierung** aus. Legen Sie auf der Seite **Anwendung registrieren** die Werte wie folgt fest.

    - Legen Sie **Name** auf `Office Add-in Graph Tutorial` fest.
    - Legen Sie **Unterstützte Kontotypen** auf **Konten in allen Organisationsverzeichnissen und persönliche Microsoft-Konten** fest.
    - Legen Sie unter **Umleitungs-URI** die erste Dropdownoption auf `Single-page application (SPA)` fest, und legen Sie den Wert auf `https://localhost:3000/consent.html` fest.

    ![Screenshot der Seite "Anwendung registrieren"](/tutorial/images/register-an-app.png)

1. Wählen Sie **Registrieren** aus. Kopieren Sie auf der Lernprogrammseite des **Office-Add-In-Diagramms** den Wert der **Anwendungs-ID (Client-ID),** und speichern Sie ihn. Sie benötigen ihn im nächsten Schritt.

    ![Screenshot der Anwendungs-ID der neuen App-Registrierung](/tutorial/images/application-id.png)

1. Wählen Sie unter **Verwalten** die Option **Zertifikate und Geheime Clientschlüssel** aus. Wählen Sie die Schaltfläche **Neuen geheimen Clientschlüssel** aus. Geben Sie einen Wert in **Beschreibung** ein, wählen Sie eine der Optionen für **Gilt bis** aus, und wählen Sie dann **Hinzufügen** aus.

1. Kopieren Sie den Wert des geheimen Clientschlüssels, bevor Sie diese Seite verlassen. Sie benötigen ihn im nächsten Schritt.

    > [!IMPORTANT]
    > Dieser geheime Clientschlüssel wird nicht noch einmal angezeigt, stellen Sie daher sicher, dass Sie ihn jetzt kopieren.

1. Wählen Sie unter **"Verwalten"** die Berechtigung **"API"** und dann **"Berechtigung hinzufügen" aus.**

1. Wählen **Sie Microsoft Graph** und dann delegierte Berechtigungen **aus.**

1. Wählen Sie die folgenden Berechtigungen und dann "Berechtigungen **hinzufügen" aus.**

    - **Calendars.ReadWrite** – Dadurch kann die App den Kalender des Benutzers lesen und in den Kalender schreiben.
    - **MailboxSettings.Read** – Dadurch kann die App die Zeitzone des Benutzers aus seinen Postfacheinstellungen erhalten.

    ![Screenshot der konfigurierten Berechtigungen](/tutorial/images/configured-permissions.png)

## <a name="configure-office-add-in-single-sign-on"></a>Konfigurieren des einmaligen Anmeldens für Office-Add-Ins

Aktualisieren Sie die App-Registrierung, um [einmaliges Anmelden (Single Sign-On, SSO) für Office-Add-Ins zu unterstützen.](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins)

1. Select **Expose an API**. Wählen Sie **in den durch diesen ABSCHNITT definierten** Bereiche die Option **"Bereich hinzufügen" aus.** Wenn Sie aufgefordert werden, einen **Anwendungs-ID-URI festlegen,** legen Sie den Wert auf , ersetzt durch `api://localhost:3000/YOUR_APP_ID_HERE` die `YOUR_APP_ID_HERE` Anwendungs-ID. Wählen Sie **"Speichern" aus, und fahren Sie fort.**

1. Füllen Sie die Felder wie folgt aus, und wählen Sie Bereich **hinzufügen aus.**

    - **Bereichsname:**`access_as_user`
    - **Wer kann zustimmen?: Administratoren und Benutzer**
    - **Anzeigename der Administrator-Zustimmung:**`Access the app as the user`
    - **Beschreibung der Administrator-Zustimmung:**`Allows Office Add-ins to call the app's web APIs as the current user.`
    - **Anzeigename der Benutzer zustimmung:**`Access the app as you`
    - **Beschreibung der Benutzer zustimmung:**`Allows Office Add-ins to call the app's web APIs as you.`
    - **Status: Aktiviert**

    ![Screenshot des Bereichsformulars hinzufügen](/tutorial/images/add-scope.png)

1. Wählen Sie **im Abschnitt "Autorisierte Clientanwendungen"** die Option **"Clientanwendung hinzufügen" aus.** Geben Sie eine Client-ID aus der folgenden Liste ein, aktivieren Sie den Bereich unter **"Autorisierte Bereiche",** und wählen Sie **"Anwendung hinzufügen" aus.** Wiederholen Sie diesen Vorgang für jede der Client-IDs in der Liste.

    - `d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)
    - `ea5a67f6-b6f3-4338-b240-c655ddc3cc8e` (Microsoft Office)
    - `57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office im Web)
    - `08e18876-6177-487e-b8b5-cf950c1e598c` (Office im Web)

## <a name="install-development-certificates"></a>Installieren von Entwicklungszertifikaten

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

1. Kopieren Sie die Pfade zu "localhost.crt" und "localhost.key", sie werden im nächsten Schritt benötigt.

## <a name="update-the-manifest"></a>Aktualisieren des Manifests

1. Öffnen Sie **manifest.xml** Datei, und nehmen Sie die folgenden Änderungen vor.
    1. Ersetzen `NEW_GUID_HERE` Sie diese durch eine neue GUID, z. `b4fa03b8-1eb6-4e8b-a380-e0476be9e019` B. .
    1. Ersetzen Sie alle Instanzen ihrer `YOUR_APP_ID_HERE` App-Registrierung durch die Anwendungs-ID.

## <a name="configure-the-sample"></a>Konfigurieren des Beispiels

1. Benennen Sie die `example.env` Datei um in `.env` .
1. Bearbeiten Sie `.env` die Datei, und nehmen Sie die folgenden Änderungen vor.
    1. Ersetzen `YOUR_APP_ID_HERE` Sie diese durch die **Anwendungs-ID,** die Sie aus dem App-Registrierungsportal erhalten haben.
    1. Ersetzen `YOUR_CLIENT_SECRET_HERE` Sie den geheimen Clientgeheimnis, den Sie aus dem App-Registrierungsportal erhalten haben.
    1. Ersetzen `PATH_TO_LOCALHOST.CRT` Sie dies durch den Pfad zur Datei "localhost.crt" aus der Ausgabe des `npx office-addin-dev-certs install` Befehls.
    1. Ersetzen `PATH_TO_LOCALHOST.KEY` Sie dies durch den Pfad zur Datei "localhost.key" aus der Ausgabe des `npx office-addin-dev-certs install` Befehls.

1. Benennen Sie die `config.example.js` Datei um in `config.js` .
1. Bearbeiten Sie `config.js` die Datei, und nehmen Sie die folgenden Änderungen vor.
    1. Ersetzen `YOUR_APP_ID_HERE` Sie diese durch die **Anwendungs-ID,** die Sie aus dem App-Registrierungsportal erhalten haben.
1. Navigieren Sie in der Befehlszeilenschnittstelle (CLI) zu diesem Verzeichnis, und führen Sie den folgenden Befehl aus, um die Installationsanforderungen zu erfüllen.

    ```Shell
    yarn install
    ```

## <a name="run-the-sample"></a>Ausführen des Beispiels

1. Führen Sie den folgenden Befehl in Ihrer CLI aus, um die Anwendung zu starten.

    ```Shell
    yarn start
    ```

1. Wechseln Sie in Ihrem Browser zu [Office.com](https://www.office.com/) und melden Sie sich an. Wählen **Sie auf** der linken Symbolleiste "Erstellen" und dann "Tabelle" **aus.**

    ![Screenshot des Menüs "Erstellen" auf Office.com](/tutorial/images/office-select-excel.png)

1. Wählen Sie die **Registerkarte** "Einfügen" und dann **"Office-Add-Ins" aus.**

1. Wählen **Sie "Mein Add-In hochladen"** und dann **"Durchsuchen" aus.** Laden Sie ihre **manifest.xml** hoch.

1. Wählen Sie **auf der Registerkarte "Start"** die Schaltfläche "Kalender **importieren"** aus, um den Aufgabenfeld zu öffnen.

    ![Screenshot der Schaltfläche "Kalender importieren" auf der Registerkarte "Start"](/tutorial/images/get-started.png)
