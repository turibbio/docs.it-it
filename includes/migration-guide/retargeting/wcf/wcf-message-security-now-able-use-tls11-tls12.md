---
ms.openlocfilehash: c646372104457e8bc5d418744847f3ee771c8d8b
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614803"
---
### <a name="wcf-message-security-now-is-able-to-use-tls11-and-tls12"></a><span data-ttu-id="2ef47-101">La sicurezza dei messaggi di WCF è ora in grado di usare TLS1.1 e TLS1.2</span><span class="sxs-lookup"><span data-stu-id="2ef47-101">WCF message security now is able to use TLS1.1 and TLS1.2</span></span>

#### <a name="details"></a><span data-ttu-id="2ef47-102">Dettagli</span><span class="sxs-lookup"><span data-stu-id="2ef47-102">Details</span></span>

<span data-ttu-id="2ef47-103">A partire da .NET Framework 4.7 i clienti possono configurare TLS1.1 o TLS1.2 nella sicurezza dei messaggi di WCF oltre a SSL3.0 e TLS1.0 usando le impostazioni di configurazione delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2ef47-103">Starting in the .NET Framework 4.7, customers can configure either TLS1.1 or TLS1.2 in WCF message security in addition to SSL3.0 and TLS1.0 through application configuration settings.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="2ef47-104">Suggerimento</span><span class="sxs-lookup"><span data-stu-id="2ef47-104">Suggestion</span></span>

<span data-ttu-id="2ef47-105">In .NET Framework 4.7 il supporto per TLS1.1 e TLS1.2 nella sicurezza dei messaggi di WCF è disattivato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2ef47-105">In the .NET Framework 4.7, support for TLS1.1 and TLS1.2 in WCF message security is disabled by default.</span></span> <span data-ttu-id="2ef47-106">Per attivarlo, aggiungendo la riga seguente alla sezione `<runtime>` del file app.config o web.config:</span><span class="sxs-lookup"><span data-stu-id="2ef47-106">You can enable it by adding the following line to the `<runtime>` section of the app.config or web.config file:</span></span>

```xml
<runtime>
<AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
</runtime>
```

| <span data-ttu-id="2ef47-107">Nome</span><span class="sxs-lookup"><span data-stu-id="2ef47-107">Name</span></span>    | <span data-ttu-id="2ef47-108">Valore</span><span class="sxs-lookup"><span data-stu-id="2ef47-108">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="2ef47-109">Scope</span><span class="sxs-lookup"><span data-stu-id="2ef47-109">Scope</span></span>   | <span data-ttu-id="2ef47-110">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="2ef47-110">Edge</span></span>        |
| <span data-ttu-id="2ef47-111">Version</span><span class="sxs-lookup"><span data-stu-id="2ef47-111">Version</span></span> | <span data-ttu-id="2ef47-112">4.7</span><span class="sxs-lookup"><span data-stu-id="2ef47-112">4.7</span></span>         |
| <span data-ttu-id="2ef47-113">Type</span><span class="sxs-lookup"><span data-stu-id="2ef47-113">Type</span></span>    | <span data-ttu-id="2ef47-114">Ridestinazione</span><span class="sxs-lookup"><span data-stu-id="2ef47-114">Retargeting</span></span> |
