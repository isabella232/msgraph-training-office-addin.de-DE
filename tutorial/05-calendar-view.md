---
ms.openlocfilehash: bd5901525561f7e169f2b7c71a280883dac8c762
ms.sourcegitcommit: 8a65c826f6b229c287a782d784b6d9629aa5a3d0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/20/2021
ms.locfileid: "51899415"
---
<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung werden Sie Microsoft Graph in die Anwendung integrieren. Für diese Anwendung verwenden Sie die [microsoft-graph-client-Bibliothek,](https://github.com/microsoftgraph/msgraph-sdk-javascript) um Aufrufe an Microsoft Graph zu senden.

## <a name="get-calendar-events-from-outlook"></a>Abrufen von Kalenderereignissen von Outlook

Fügen Sie zunächst eine API hinzu, um eine [Kalenderansicht aus](https://docs.microsoft.com/graph/api/user-list-calendarview) dem Kalender des Benutzers zu erhalten.

1. Öffnen **Sie ./src/api/graph.ts,** und fügen Sie die folgenden Anweisungen am oberen Rand `import` der Datei hinzu.

    ```typescript
    import { zonedTimeToUtc } from 'date-fns-tz';
    import { findIana } from 'windows-iana';
    import * as graph from '@microsoft/microsoft-graph-client';
    import { Event, MailboxSettings } from 'microsoft-graph';
    import 'isomorphic-fetch';
    import { getTokenOnBehalfOf } from './auth';
    ```

1. Fügen Sie die folgende Funktion hinzu, um das Microsoft Graph SDK zu initialisieren und einen **Client zurück zu geben.**

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="GetClientSnippet":::

1. Fügen Sie die folgende Funktion hinzu, um die Zeitzone des Benutzers aus den Postfacheinstellungen zu erhalten und diesen Wert in einen IANA-Zeitzonenbezeichner zu konvertieren.

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="GetTimeZonesSnippet":::

1. Fügen Sie die folgende Funktion (unterhalb der `const graphRouter = Router();` Zeile) hinzu, um einen API-Endpunkt ( ) zu `GET /graph/calendarview` implementieren.

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="GetCalendarViewSnippet":::

    Überlegen Sie, was dieser Code macht.

    - Es ruft die Zeitzone des Benutzers ab und verwendet diese, um start und end der angeforderten Kalenderansicht in UTC-Werte zu konvertieren.
    - Er führt eine `GET` für den `/me/calendarview` Graph-API-Endpunkt aus.
        - Mit der Funktion wird der Header festgelegt, wodurch die Start- und Endzeiten der zurückgegebenen Ereignisse an die Zeitzone des Benutzers `header` `Prefer: outlook.timezone` angepasst werden.
        - Sie verwendet die `query` -Funktion, um die Parameter und hinzuzufügen, indem `startDateTime` der Anfang und das Ende der `endDateTime` Kalenderansicht festgelegt werden.
        - Sie verwendet die `select` Funktion, um nur die felder an, die vom Add-In verwendet werden.
        - Sie verwendet die `orderby` Funktion, um die Ergebnisse nach der Startzeit zu sortieren.
        - Sie verwendet die `top` Funktion, um die Ergebnisse in einer einzelnen Anforderung auf 25 zu beschränken.
    - Es verwendet ein **PageIteratorCallback-Objekt,** um die Ergebnisse zu durchblättern und zusätzliche Anforderungen zu stellen, wenn weitere Seiten mit Ergebnissen verfügbar sind. [](https://docs.microsoft.com/graph/sdks/paging)

## <a name="update-the-ui"></a>Aktualisieren der Benutzeroberfläche

Nun aktualisieren wir den Aufgabenbereich, damit der Benutzer ein Start- und Enddatum für die Kalenderansicht angeben kann.

1. Öffnen **Sie ./src/addin/taskpane.js,** und ersetzen Sie die vorhandene `showMainUi` Funktion durch Folgendes.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="MainUiSnippet":::

    Dieser Code fügt ein einfaches Formular hinzu, damit der Benutzer ein Start- und Enddatum angeben kann. Außerdem wird ein zweites Formular zum Erstellen eines neuen Ereignisses implementiert. Dieses Formular führt vorerst nichts aus, Sie implementieren dieses Feature im nächsten Abschnitt.

1. Fügen Sie der Datei den folgenden Code hinzu, um eine Tabelle im aktiven Arbeitsblatt zu erstellen, die die ereignisse enthält, die aus der Kalenderansicht abgerufen wurden.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="WriteToSheetSnippet":::

1. Fügen Sie die folgende Funktion hinzu, um die Kalenderansichts-API auf aufruft.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="GetCalendarSnippet":::

1. Speichern Sie alle Änderungen, starten Sie den Server neu, und aktualisieren Sie den Aufgabenbereich in Excel (schließen Sie alle geöffneten Aufgabenbereiche, und öffnen Sie sie erneut).

    ![Screenshot des Importformulars](images/get-calendar-view-ui.png)

1. Wählen Sie Start- und Endtermine aus, und wählen Sie **Importieren aus.**

    ![Ein Screenshot der Tabelle mit Ereignissen](images/calendar-view-table.png)
