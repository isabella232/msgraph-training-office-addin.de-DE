---
ms.openlocfilehash: 2c323d61632c62c82af0561536656f1d68fe8938
ms.sourcegitcommit: 24bb4b3df6a035806a58b609e1d8078ac5505fa1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/17/2021
ms.locfileid: "50274288"
---
<!-- markdownlint-disable MD002 MD041 -->

In diesem Lernprogramm erfahren Sie, wie Sie ein Office-Add-In für Excel erstellen, das die Microsoft Graph-API zum Abrufen von Kalenderinformationen für einen Benutzer verwendet.

> [!TIP]
> Wenn Sie nur das abgeschlossene Lernprogramm herunterladen möchten, können Sie das [GitHub-Repository herunterladen oder klonen.](https://github.com/microsoftgraph/msgraph-training-office-addin)

## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie mit dieser Demo beginnen, sollten [ Sie ](https://nodejs.org)Node.js[Und Sichten](https://yarnpkg.com/) auf Ihrem Entwicklungscomputer installiert haben. Wenn Sie nicht über eine Node.js oder Einess verfügen, besuchen Sie den vorherigen Link, um Downloadoptionen zu erhalten.

> [!NOTE]
> #A0 müssen möglicherweise Python und Visual Studio Build Tools installieren, um #A1 zu unterstützen, die aus C/C++ kompiliert werden müssen. Das Node.js unter Windows bietet die Möglichkeit, diese Tools automatisch zu installieren. Alternativ können Sie den Anweisungen unter [https://github.com/nodejs/node-gyp#on-windows](https://github.com/nodejs/node-gyp#on-windows) folgen.

Sie sollten auch über ein persönliches Microsoft-Konto mit einem Postfach auf Outlook.com oder ein Microsoft-Arbeits- oder Schulkonto verfügen. Wenn Sie kein Microsoft-Konto haben, gibt es mehrere Optionen, um ein kostenloses Konto zu erhalten:

- Sie können [sich für ein neues persönliches Microsoft-Konto registrieren.](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)
- Sie können [sich für das Office 365-Entwicklerprogramm](https://developer.microsoft.com/office/dev-program) registrieren, um ein kostenloses Office 365-Abonnement zu erhalten.

> [!NOTE]
> Dieses Lernprogramm wurde mit Node Version 14.15.0 und Derzversion 1.22.0 geschrieben. Die Schritte in diesem Handbuch funktionieren möglicherweise mit anderen Versionen, wurden jedoch noch nicht getestet.

## <a name="feedback"></a>Feedback

Bitte geben Sie Feedback zu diesem Lernprogramm im [GitHub-Repository.](https://github.com/microsoftgraph/msgraph-training-office-addin)
