---
ms.openlocfilehash: b893966ceb65246ed6a7d214011b17ca14c50d5a
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85802851"
---

> [!WARNING]
> Quando <xref:System.Text.RegularExpressions> si usa per elaborare un input non attendibile, passare un timeout. Un utente malintenzionato può fornire l'input per `RegularExpressions` provocare un [attacco Denial of Service](https://www.us-cert.gov/ncas/tips/ST04-015). Le API di ASP.NET Core Framework che usano `RegularExpressions` passano un timeout.
