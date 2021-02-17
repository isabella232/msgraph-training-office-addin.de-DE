---
ms.openlocfilehash: ade142f1518d9bd56fa1472889721a4c8995bc3c
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274252"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="b99fc-101">In dieser Übung integrieren Sie Microsoft Graph in die Anwendung.</span><span class="sxs-lookup"><span data-stu-id="b99fc-101">In this exercise you will incorporate Microsoft Graph into the application.</span></span> <span data-ttu-id="b99fc-102">Für diese Anwendung verwenden Sie die [Microsoft-graph-Clientbibliothek,](https://github.com/microsoftgraph/msgraph-sdk-javascript) um Aufrufe an Microsoft Graph zu senden.</span><span class="sxs-lookup"><span data-stu-id="b99fc-102">For this application, you will use the [microsoft-graph-client](https://github.com/microsoftgraph/msgraph-sdk-javascript) library to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="b99fc-103">Abrufen von Kalenderereignissen von Outlook</span><span class="sxs-lookup"><span data-stu-id="b99fc-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="b99fc-104">Fügen Sie zunächst eine API hinzu, um eine [Kalenderansicht aus](https://docs.microsoft.com/graph/api/user-list-calendarview) dem Kalender des Benutzers zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="b99fc-104">Start by adding an API to get a [calendar view](https://docs.microsoft.com/graph/api/user-list-calendarview) from the user's calendar.</span></span>

1. <span data-ttu-id="b99fc-105">Öffnen **Sie ./src/api/graph.ts,** und fügen Sie die folgenden Anweisungen `import` am Oberen Rand der Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="b99fc-105">Open **./src/api/graph.ts** and add the following `import` statements to the top of the file.</span></span>

    ```typescript
    import { zonedTimeToUtc } from 'date-fns-tz';
    import { findOneIana } from 'windows-iana';
    import * as graph from '@microsoft/microsoft-graph-client';
    import { Event, MailboxSettings } from 'microsoft-graph';
    import 'isomorphic-fetch';
    import { getTokenOnBehalfOf } from './auth';
    ```

1. <span data-ttu-id="b99fc-106">Fügen Sie die folgende Funktion hinzu, um das Microsoft Graph SDK zu initialisieren und einen **Client zurückzukehren.**</span><span class="sxs-lookup"><span data-stu-id="b99fc-106">Add the following function to initialize the Microsoft Graph SDK and return a **Client**.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="GetClientSnippet":::

1. <span data-ttu-id="b99fc-107">Fügen Sie die folgende Funktion hinzu, um die Zeitzone des Benutzers aus den Postfacheinstellungen zu erhalten und diesen Wert in einen IANA-Zeitzonenbezeichner zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="b99fc-107">Add the following function to get the user's time zone from their mailbox settings, and to convert that value to an IANA time zone identifier.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="GetTimeZonesSnippet":::

1. <span data-ttu-id="b99fc-108">Fügen Sie die folgende Funktion (unter der `const graphRouter = Router();` Zeile) hinzu, um einen API-Endpunkt ( ) zu `GET /graph/calendarview` implementieren.</span><span class="sxs-lookup"><span data-stu-id="b99fc-108">Add the following function (below the `const graphRouter = Router();` line) to implement an API endpoint (`GET /graph/calendarview`).</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="GetCalendarViewSnippet":::

    <span data-ttu-id="b99fc-109">Überlegen Sie, was dieser Code macht.</span><span class="sxs-lookup"><span data-stu-id="b99fc-109">Consider what this code does.</span></span>

    - <span data-ttu-id="b99fc-110">Sie ruft die Zeitzone des Benutzers ab und verwendet diese, um den Anfang und das Ende der angeforderten Kalenderansicht in UTC-Werte zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="b99fc-110">It gets the user's time zone and uses that to convert the start and end of the requested calendar view into UTC values.</span></span>
    - <span data-ttu-id="b99fc-111">Es führt eine Für `GET` den `/me/calendarview` Graph-API-Endpunkt aus.</span><span class="sxs-lookup"><span data-stu-id="b99fc-111">It does a `GET` to the `/me/calendarview` Graph API endpoint.</span></span>
        - <span data-ttu-id="b99fc-112">Sie verwendet die Funktion, um die Kopfzeile zu setzen, wodurch die Start- und Endzeiten der zurückgegebenen Ereignisse an die Zeitzone des Benutzers `header` `Prefer: outlook.timezone` angepasst werden.</span><span class="sxs-lookup"><span data-stu-id="b99fc-112">It uses the `header` function to set the `Prefer: outlook.timezone` header, causing the start and end times of the returned events to be adjusted to the user's time zone.</span></span>
        - <span data-ttu-id="b99fc-113">Sie verwendet die Funktion, um die Parameter und die Start- und Endwerte der `query` `startDateTime` `endDateTime` Kalenderansicht hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="b99fc-113">It uses the `query` function to add the `startDateTime` and `endDateTime` parameters, setting the start and end of the calendar view.</span></span>
        - <span data-ttu-id="b99fc-114">Sie verwendet die `select` Funktion, um nur die felder an fordern, die vom Add-in verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="b99fc-114">It uses the `select` function to request only the fields used by the add-in.</span></span>
        - <span data-ttu-id="b99fc-115">Die Funktion wird `orderby` verwendet, um die Ergebnisse nach Startzeit zu sortieren.</span><span class="sxs-lookup"><span data-stu-id="b99fc-115">It uses the `orderby` function to sort the results by the start time.</span></span>
        - <span data-ttu-id="b99fc-116">Sie verwendet die Funktion, um die Ergebnisse in einer einzelnen Anforderung auf `top` 25 zu beschränken.</span><span class="sxs-lookup"><span data-stu-id="b99fc-116">It uses the `top` function to limit the results in a single request to 25.</span></span>
    - <span data-ttu-id="b99fc-117">Es verwendet ein **PageIteratorCallback -Objekt,** um die Ergebnisse zu durchblättern und zusätzliche Anforderungen zu stellen, wenn weitere Seiten mit Ergebnissen verfügbar sind. [](https://docs.microsoft.com/graph/sdks/paging)</span><span class="sxs-lookup"><span data-stu-id="b99fc-117">It uses a **PageIteratorCallback** object to [iterate through the results](https://docs.microsoft.com/graph/sdks/paging) and to make additional requests if more pages of results are available.</span></span>

## <a name="update-the-ui"></a><span data-ttu-id="b99fc-118">Aktualisieren der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="b99fc-118">Update the UI</span></span>

<span data-ttu-id="b99fc-119">Nun aktualisieren wir den Aufgabenbereich, damit der Benutzer ein Start- und Enddatum für die Kalenderansicht angeben kann.</span><span class="sxs-lookup"><span data-stu-id="b99fc-119">Now let's update the task pane to allow the user to specify a start and end date for the calendar view.</span></span>

1. <span data-ttu-id="b99fc-120">Öffnen **Sie ./src/addin/taskpane.js,** und ersetzen Sie die vorhandene `showMainUi` Funktion durch Folgendes.</span><span class="sxs-lookup"><span data-stu-id="b99fc-120">Open **./src/addin/taskpane.js** and replace the existing `showMainUi` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="MainUiSnippet":::

    <span data-ttu-id="b99fc-121">Dieser Code fügt ein einfaches Formular hinzu, damit der Benutzer ein Start- und Enddatum angeben kann.</span><span class="sxs-lookup"><span data-stu-id="b99fc-121">This code adds a simple form so the user can specify a start and end date.</span></span> <span data-ttu-id="b99fc-122">Außerdem wird ein zweites Formular zum Erstellen eines neuen Ereignisses implementiert.</span><span class="sxs-lookup"><span data-stu-id="b99fc-122">It also implements a second form for creating a new event.</span></span> <span data-ttu-id="b99fc-123">Dieses Formular hat vorerst keine Funktion, Sie implementieren dieses Feature im nächsten Abschnitt.</span><span class="sxs-lookup"><span data-stu-id="b99fc-123">That form doesn't do anything for now, you'll implement that feature in the next section.</span></span>

1. <span data-ttu-id="b99fc-124">Fügen Sie der Datei den folgenden Code hinzu, um eine Tabelle im aktiven Arbeitsblatt zu erstellen, die die aus der Kalenderansicht abgerufenen Ereignisse enthält.</span><span class="sxs-lookup"><span data-stu-id="b99fc-124">Add the following code to the file to create a table in the active worksheet containing the events retrieved from the calendar view.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="WriteToSheetSnippet":::

1. <span data-ttu-id="b99fc-125">Fügen Sie die folgende Funktion zum Aufrufen der Kalenderansichts-API hinzu.</span><span class="sxs-lookup"><span data-stu-id="b99fc-125">Add the following function to call the calendar view API.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="GetCalendarSnippet":::

1. <span data-ttu-id="b99fc-126">Speichern Sie alle Änderungen, starten Sie den Server neu, und aktualisieren Sie den Aufgabenbereich in Excel (schließen Sie alle geöffneten Aufgabenbereiche, und öffnen Sie sie erneut).</span><span class="sxs-lookup"><span data-stu-id="b99fc-126">Save all of your changes, restart the server, and refresh the task pane in Excel (close any open task panes and re-open).</span></span>

    ![Screenshot des Importformulars](images/get-calendar-view-ui.png)

1. <span data-ttu-id="b99fc-128">Wählen Sie Start- und Enddaten und Importieren **aus.**</span><span class="sxs-lookup"><span data-stu-id="b99fc-128">Choose start and end dates and choose **Import**.</span></span>

    ![Ein Screenshot der Tabelle mit Ereignissen](images/calendar-view-table.png)
