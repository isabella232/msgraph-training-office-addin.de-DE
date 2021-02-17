---
ms.openlocfilehash: 69d77c19cb2c589086df2b4bf19eeadf41aad58a
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274393"
---
<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung aktivieren Sie [einmaliges Anmelden (Single Sign-On, SSO) für Office-Add-Ins](https://docs.microsoft.com/office/dev/add-ins/develop/sso-in-office-add-ins) im Add-In und erweitern die Web-API so, dass sie den [On-Behalf-of-Fluss unterstützt.](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) Dies ist erforderlich, um das erforderliche OAuth-Zugriffstoken zum Aufrufen von Microsoft Graph abzurufen.

## <a name="overview"></a>Übersicht

Office-Add-In-SSO stellt ein Zugriffstoken bereit, dieses Token ermöglicht es dem Add-In jedoch nur, seine eigene Web-API auf aufruft. Es ermöglicht nicht den direkten Zugriff auf Microsoft Graph. Der Vorgang funktioniert wie folgt.

1. Das Add-in ruft ein Token durch Aufrufen von [getAccessToken ab.](https://docs.microsoft.com/javascript/api/office-runtime/officeruntime.auth?view=common-js#getaccesstoken-options-) Die Zielgruppe dieses Tokens (der Anspruch) ist die `aud` Anwendungs-ID der App-Registrierung des Add-Ins.
1. Das Add-in sendet dieses Token in der `Authorization` Kopfzeile, wenn es einen Aufruf an die Web-API macht.
1. Die Web-API überprüft das Token und verwendet dann den Im-Auftrag-von-Fluss, um dieses Token gegen ein Microsoft Graph-Token zu tauschen. Die Zielgruppe dieses neuen Tokens ist `https://graph.microsoft.com` .
1. Die Web-API verwendet das neue Token, um Aufrufe an Microsoft Graph zu senden, und gibt die Ergebnisse an das Add-In zurück.

## <a name="configure-the-solution"></a>Konfigurieren der Lösung

1. Öffnen **Sie ./.env,** und aktualisieren Sie die Anwendungs-ID und den `AZURE_APP_ID` geheimen Clientgeheimnis aus Ihrer `AZURE_CLIENT_SECRET` App-Registrierung.

    > [!IMPORTANT]
    > Wenn Sie Quellcodeverwaltung wie Git verwenden, wäre es jetzt ein guter Zeitpunkt, die **env-Datei** aus der Quellcodeverwaltung auszuschließen, um zu verhindern, dass versehentlich Ihre App-ID und der geheime Client geheimen Clientdatenlecks ans Licht kommen.

1. Öffnen **Sie ./manifest/manifest.xml,** und ersetzen Sie alle Instanzen durch die Anwendungs-ID `YOUR_APP_ID_HERE` aus Ihrer App-Registrierung.

1. Erstellen Sie eine neue Datei im Verzeichnis **./src/addin** mit dem Namen **config.js,** und fügen Sie den folgenden Code hinzu, und ersetzen Sie dabei die Anwendungs-ID aus `YOUR_APP_ID_HERE` Ihrer App-Registrierung.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/config.example.js":::

## <a name="implement-sign-in"></a>Implementieren der Anmeldung

1. Öffnen **Sie ./src/api/auth.ts,** und fügen Sie die folgenden Anweisungen `import` am Anfang der Datei hinzu.

    ```typescript
    import jwt, { SigningKeyCallback, JwtHeader } from 'jsonwebtoken';
    import jwksClient from 'jwks-rsa';
    import * as msal from '@azure/msal-node';
    ```

1. Fügen Sie den folgenden Code nach den Anweisungen `import` hinzu.

    :::code language="typescript" source="../demo/graph-tutorial/src/api/auth.ts" id="TokenExchangeSnippet":::

    Dieser Code [initialisiert einen vertraulichen MSAL-Client](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md)und exportiert eine Funktion, um ein Graph-Token aus dem Token abzurufen, das vom Add-in gesendet wurde.

1. Fügen Sie den folgenden Code vor der `export default authRouter;` Zeile hinzu.

    :::code language="typescript" source="../demo/graph-tutorial/src/api/auth.ts" id="GetAuthStatusSnippet":::

    Dieser Code implementiert eine API ( ), die überprüft, ob das Add-In-Token im Hintergrund gegen ein `GET /auth/status` Graph-Token ausgetauscht werden kann. Das Add-in verwendet diese API, um zu bestimmen, ob es dem Benutzer eine interaktive Anmeldung präsentieren muss.

1. Öffnen **Sie ./src/addin/taskpane.js,** und fügen Sie der Datei den folgenden Code hinzu.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="AuthUiSnippet":::

    Dieser Code fügt Funktionen hinzu, um die Benutzeroberfläche zu aktualisieren und die [Office-Dialog-API](https://docs.microsoft.com/office/dev/add-ins/develop/dialog-api-in-office-add-ins) zum Initiieren eines interaktiven Authentifizierungsflusses zu verwenden.

1. Fügen Sie die folgende Funktion hinzu, um eine temporäre Hauptbenutzeroberfläche zu implementieren.

    ```javascript
    function showMainUi() {
      $('.container').empty();
      $('<p/>', {
        class: 'ms-fontSize-24 ms-fontWeight-bold',
        text: 'Authenticated!'
      }).appendTo('.container');
    }
    ```

1. Ersetzen Sie den `Office.onReady` vorhandenen Anruf durch Folgendes.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="OfficeReadySnippet":::

    Überlegen Sie, was dieser Code macht.

    - Wenn der Aufgabenbereich zum ersten Mal geladen wird, ruft er ein Token ab, das auf die `getAccessToken` Web-API des Add-Ins ausgelegt ist.
    - Dieses Token wird zum Aufrufen der API verwendet, um zu überprüfen, ob der Benutzer den Microsoft Graph-Bereich `/auth/status` noch seine Zustimmung erteilt hat.
        - Wenn der Benutzer nicht zugestimmt hat, verwendet er ein Popupfenster, um die Zustimmung des Benutzers über eine interaktive Anmeldung einzuholen.
        - Wenn der Benutzer seine Zustimmung gegeben hat, wird die Hauptbenutzeroberfläche geladen.

### <a name="getting-user-consent"></a>Einholen der Zustimmung des Benutzers

Obwohl das Add-in SSO verwendet, muss der Benutzer dem Add-In, das über Microsoft Graph auf seine Daten zutritt, dennoch zustimmen. Das Einholen der Zustimmung ist ein einmaler Prozess. Nachdem der Benutzer seine Zustimmung erteilt hat, kann das SSO-Token ohne Benutzerinteraktion gegen ein Graph-Token ausgetauscht werden. In diesem Abschnitt implementieren Sie die Zustimmungserfahrung im Add-In mit [msal-browser.](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)

1. Erstellen Sie eine neue Datei im **Verzeichnis "./src/addin"** consent.js **und** fügen Sie den folgenden Code hinzu.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/consent.js" id="ConsentJsSnippet":::

    Dieser Code anmeldet sich für den Benutzer und fordert den Satz von Microsoft Graph-Berechtigungen an, die für die Registrierung der App konfiguriert sind.

1. Erstellen Sie eine neue Datei im Verzeichnis **./src/addin** mit dem Namen **consent.html,** und fügen Sie den folgenden Code hinzu.

    :::code language="html" source="../demo/graph-tutorial/src/addin/consent.html" id="ConsentHtmlSnippet":::

    Dieser Code implementiert eine einfache HTML-Seite, um die **consent.js** laden. Diese Seite wird in einem Popupdialogfeld geladen.

1. Speichern Sie alle Änderungen, und starten Sie den Server neu.

1. Laden Sie Ihre **manifest.xml** mit den gleichen Schritten in [Side-Load the add-in in Excel erneut hoch.](02-create-app.md#side-load-the-add-in-in-excel)

1. Wählen Sie auf **der Registerkarte "Start"** die Schaltfläche "Kalender **importieren"** aus, um den Aufgabenbereich zu öffnen.

1. Wählen Sie **die Schaltfläche "Berechtigung erteilen"** im Aufgabenbereich aus, um das Zustimmungsdialogfeld in einem Popupfenster zu starten. Melden Sie sich an, und erteilen Sie ihre Zustimmung.

1. Der Aufgabenbereich wird mit "Authentifiziert!" aktualisiert. Nachricht. Sie können die Token wie folgt überprüfen.

    - In den Entwicklertools Ihres Browsers wird das API-Token in der Konsole angezeigt.
    - In Ihrer CLI, in der Sie den Node.js ausführen, wird das Graph-Token gedruckt.

    Sie können dieses Token unter [https://jwt.ms](https://jwt.ms) vergleichen. Beachten Sie, dass die Zielgruppe des API-Tokens ( ) auf die Anwendungs-ID Ihrer App-Registrierung und der Bereich `aud` ( `scp` ) festgelegt `access_as_user` ist.
