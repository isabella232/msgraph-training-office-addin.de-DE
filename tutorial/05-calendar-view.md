---
ms.openlocfilehash: ade142f1518d9bd56fa1472889721a4c8995bc3c
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274252"
---
<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung integrieren Sie Microsoft Graph in die Anwendung. Für diese Anwendung verwenden Sie die [Microsoft-graph-Clientbibliothek,](https://github.com/microsoftgraph/msgraph-sdk-javascript) um Aufrufe an Microsoft Graph zu senden.

## <a name="get-calendar-events-from-outlook"></a>Abrufen von Kalenderereignissen von Outlook

Fügen Sie zunächst eine API hinzu, um eine [Kalenderansicht aus](https://docs.microsoft.com/graph/api/user-list-calendarview) dem Kalender des Benutzers zu erhalten.

1. Öffnen **Sie ./src/api/graph.ts,** und fügen Sie die folgenden Anweisungen `import` am Oberen Rand der Datei hinzu.

    ```typescript
    import { zonedTimeToUtc } from 'date-fns-tz';
    import { findOneIana } from 'windows-iana';
    import * as graph from '@microsoft/microsoft-graph-client';
    import { Event, MailboxSettings } from 'microsoft-graph';
    import 'isomorphic-fetch';
    import { getTokenOnBehalfOf } from './auth';
    ```

1. Fügen Sie die folgende Funktion hinzu, um das Microsoft Graph SDK zu initialisieren und einen **Client zurückzukehren.**

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="GetClientSnippet":::

1. Fügen Sie die folgende Funktion hinzu, um die Zeitzone des Benutzers aus den Postfacheinstellungen zu erhalten und diesen Wert in einen IANA-Zeitzonenbezeichner zu konvertieren.

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="GetTimeZonesSnippet":::

1. Fügen Sie die folgende Funktion (unter der `const graphRouter = Router();` Zeile) hinzu, um einen API-Endpunkt ( ) zu `GET /graph/calendarview` implementieren.

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="GetCalendarViewSnippet":::

    Überlegen Sie, was dieser Code macht.

    - Sie ruft die Zeitzone des Benutzers ab und verwendet diese, um den Anfang und das Ende der angeforderten Kalenderansicht in UTC-Werte zu konvertieren.
    - Es führt eine Für `GET` den `/me/calendarview` Graph-API-Endpunkt aus.
        - Sie verwendet die Funktion, um die Kopfzeile zu setzen, wodurch die Start- und Endzeiten der zurückgegebenen Ereignisse an die Zeitzone des Benutzers `header` `Prefer: outlook.timezone` angepasst werden.
        - Sie verwendet die Funktion, um die Parameter und die Start- und Endwerte der `query` `startDateTime` `endDateTime` Kalenderansicht hinzuzufügen.
        - Sie verwendet die `select` Funktion, um nur die felder an fordern, die vom Add-in verwendet werden.
        - Die Funktion wird `orderby` verwendet, um die Ergebnisse nach Startzeit zu sortieren.
        - Sie verwendet die Funktion, um die Ergebnisse in einer einzelnen Anforderung auf `top` 25 zu beschränken.
    - Es verwendet ein **PageIteratorCallback -Objekt,** um die Ergebnisse zu durchblättern und zusätzliche Anforderungen zu stellen, wenn weitere Seiten mit Ergebnissen verfügbar sind. [](https://docs.microsoft.com/graph/sdks/paging)

## <a name="update-the-ui"></a>Aktualisieren der Benutzeroberfläche

Nun aktualisieren wir den Aufgabenbereich, damit der Benutzer ein Start- und Enddatum für die Kalenderansicht angeben kann.

1. Öffnen **Sie ./src/addin/taskpane.js,** und ersetzen Sie die vorhandene `showMainUi` Funktion durch Folgendes.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="MainUiSnippet":::

    Dieser Code fügt ein einfaches Formular hinzu, damit der Benutzer ein Start- und Enddatum angeben kann. Außerdem wird ein zweites Formular zum Erstellen eines neuen Ereignisses implementiert. Dieses Formular hat vorerst keine Funktion, Sie implementieren dieses Feature im nächsten Abschnitt.

1. Fügen Sie der Datei den folgenden Code hinzu, um eine Tabelle im aktiven Arbeitsblatt zu erstellen, die die aus der Kalenderansicht abgerufenen Ereignisse enthält.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="WriteToSheetSnippet":::

1. Fügen Sie die folgende Funktion zum Aufrufen der Kalenderansichts-API hinzu.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="GetCalendarSnippet":::

1. Speichern Sie alle Änderungen, starten Sie den Server neu, und aktualisieren Sie den Aufgabenbereich in Excel (schließen Sie alle geöffneten Aufgabenbereiche, und öffnen Sie sie erneut).

    ![Screenshot des Importformulars](images/get-calendar-view-ui.png)

1. Wählen Sie Start- und Enddaten und Importieren **aus.**

    ![Ein Screenshot der Tabelle mit Ereignissen](images/calendar-view-table.png)
