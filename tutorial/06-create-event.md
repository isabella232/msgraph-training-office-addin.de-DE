---
ms.openlocfilehash: facdbb5c42e60e5bb0ee98b06ef68939a6010a67
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274251"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="55e49-101">In diesem Abschnitt fügen Sie die Möglichkeit zum Erstellen von Ereignissen im Kalender des Benutzers hinzu.</span><span class="sxs-lookup"><span data-stu-id="55e49-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="implement-the-api"></a><span data-ttu-id="55e49-102">Implementieren der API</span><span class="sxs-lookup"><span data-stu-id="55e49-102">Implement the API</span></span>

1. <span data-ttu-id="55e49-103">Öffnen **Sie ./src/api/graph.ts,** und fügen Sie den folgenden Code hinzu, um eine neue Ereignis-API ( ) zu `POST /graph/newevent` implementieren.</span><span class="sxs-lookup"><span data-stu-id="55e49-103">Open **./src/api/graph.ts** and add the following code to implement a new event API (`POST /graph/newevent`).</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="CreateEventSnippet":::

1. <span data-ttu-id="55e49-104">Öffnen **Sie ./src/addin/taskpane.js,** und fügen Sie die folgende Funktion zum Aufrufen der neuen Ereignis-API hinzu.</span><span class="sxs-lookup"><span data-stu-id="55e49-104">Open **./src/addin/taskpane.js** and add the following function to call the new event API.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="CreateEventSnippet":::

1. <span data-ttu-id="55e49-105">Speichern Sie alle Änderungen, starten Sie den Server neu, und aktualisieren Sie den Aufgabenbereich in Excel (schließen Sie alle geöffneten Aufgabenbereiche, und öffnen Sie sie erneut).</span><span class="sxs-lookup"><span data-stu-id="55e49-105">Save all of your changes, restart the server, and refresh the task pane in Excel (close any open task panes and re-open).</span></span>

    ![Screenshot des Formulars zum Erstellen eines Ereignisses](images/create-event-ui.png)

1. <span data-ttu-id="55e49-107">Füllen Sie das Formular aus, und wählen Sie **"Erstellen" aus.**</span><span class="sxs-lookup"><span data-stu-id="55e49-107">Fill in the form and choose **Create**.</span></span> <span data-ttu-id="55e49-108">Stellen Sie sicher, dass das Ereignis dem Kalender des Benutzers hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="55e49-108">Verify that the event is added to the user's calendar.</span></span>
