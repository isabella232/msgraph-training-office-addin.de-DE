---
ms.openlocfilehash: facdbb5c42e60e5bb0ee98b06ef68939a6010a67
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274251"
---
<!-- markdownlint-disable MD002 MD041 -->

In diesem Abschnitt fügen Sie die Möglichkeit zum Erstellen von Ereignissen im Kalender des Benutzers hinzu.

## <a name="implement-the-api"></a>Implementieren der API

1. Öffnen **Sie ./src/api/graph.ts,** und fügen Sie den folgenden Code hinzu, um eine neue Ereignis-API ( ) zu `POST /graph/newevent` implementieren.

    :::code language="typescript" source="../demo/graph-tutorial/src/api/graph.ts" id="CreateEventSnippet":::

1. Öffnen **Sie ./src/addin/taskpane.js,** und fügen Sie die folgende Funktion zum Aufrufen der neuen Ereignis-API hinzu.

    :::code language="javascript" source="../demo/graph-tutorial/src/addin/taskpane.js" id="CreateEventSnippet":::

1. Speichern Sie alle Änderungen, starten Sie den Server neu, und aktualisieren Sie den Aufgabenbereich in Excel (schließen Sie alle geöffneten Aufgabenbereiche, und öffnen Sie sie erneut).

    ![Screenshot des Formulars zum Erstellen eines Ereignisses](images/create-event-ui.png)

1. Füllen Sie das Formular aus, und wählen Sie **"Erstellen" aus.** Stellen Sie sicher, dass das Ereignis dem Kalender des Benutzers hinzugefügt wird.
