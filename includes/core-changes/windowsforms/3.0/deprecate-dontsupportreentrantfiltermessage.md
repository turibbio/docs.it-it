---
ms.openlocfilehash: 55c13aa70a03bcc548ce1d096cca8f40de6cda84
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2020
ms.locfileid: "83720892"
---
### <a name="dontsupportreentrantfiltermessage-compatibility-switch-not-supported"></a><span data-ttu-id="e5bf1-101">Opzione di compatibilità DontSupportReentrantFilterMessage non supportata</span><span class="sxs-lookup"><span data-stu-id="e5bf1-101">DontSupportReentrantFilterMessage compatibility switch not supported</span></span>

<span data-ttu-id="e5bf1-102">L' `Switch.System.Windows.Forms.DontSupportReentrantFilterMessage` opzione di compatibilità, introdotta in .NET Framework 4.6.1, non è supportata in Windows Forms in .NET Core 3,0.</span><span class="sxs-lookup"><span data-stu-id="e5bf1-102">The `Switch.System.Windows.Forms.DontSupportReentrantFilterMessage` compatibility switch, which was introduced in .NET Framework 4.6.1, is not supported in Windows Forms on .NET Core 3.0.</span></span>

#### <a name="change-description"></a><span data-ttu-id="e5bf1-103">Descrizione modifica:</span><span class="sxs-lookup"><span data-stu-id="e5bf1-103">Change description</span></span>

<span data-ttu-id="e5bf1-104">A partire da .NET Framework 4.6.1, l' `Switch.System.Windows.Forms.DontSupportReentrantFilterMessage` opzione di compatibilità risolve le possibili <xref:System.IndexOutOfRangeException> eccezioni quando il <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType> messaggio viene chiamato con un' <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType> implementazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="e5bf1-104">Starting with the .NET Framework 4.6.1, the `Switch.System.Windows.Forms.DontSupportReentrantFilterMessage` compatibility switch addresses possible <xref:System.IndexOutOfRangeException> exceptions when the <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType> message is called with a custom <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType> implementation.</span></span> <span data-ttu-id="e5bf1-105">Per altre informazioni, vedere [Mitigazione: Implementazioni IMessageFilter.PreFilterMessage personalizzate](~/docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md).</span><span class="sxs-lookup"><span data-stu-id="e5bf1-105">For more information, see [Mitigation: Custom IMessageFilter.PreFilterMessage Implementations](~/docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md).</span></span>

<span data-ttu-id="e5bf1-106">In .NET Core l' `Switch.System.Windows.Forms.DontSupportReentrantFilterMessage` opzione non è supportata.</span><span class="sxs-lookup"><span data-stu-id="e5bf1-106">In .NET Core, the `Switch.System.Windows.Forms.DontSupportReentrantFilterMessage` switch is not supported.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="e5bf1-107">Versione introdotta</span><span class="sxs-lookup"><span data-stu-id="e5bf1-107">Version introduced</span></span>

<span data-ttu-id="e5bf1-108">3,0 Preview 9</span><span class="sxs-lookup"><span data-stu-id="e5bf1-108">3.0 Preview 9</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="e5bf1-109">Azione consigliata</span><span class="sxs-lookup"><span data-stu-id="e5bf1-109">Recommended action</span></span>

<span data-ttu-id="e5bf1-110">Rimuovere l'opzione.</span><span class="sxs-lookup"><span data-stu-id="e5bf1-110">Remove the switch.</span></span> <span data-ttu-id="e5bf1-111">L'opzione non è supportata e non è disponibile alcuna funzionalità alternativa.</span><span class="sxs-lookup"><span data-stu-id="e5bf1-111">The switch is not supported, and no alternative functionality is available.</span></span>

#### <a name="category"></a><span data-ttu-id="e5bf1-112">Category</span><span class="sxs-lookup"><span data-stu-id="e5bf1-112">Category</span></span>

<span data-ttu-id="e5bf1-113">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="e5bf1-113">Windows Forms</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="e5bf1-114">API interessate</span><span class="sxs-lookup"><span data-stu-id="e5bf1-114">Affected APIs</span></span>

- <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType>

<!-- 

#### Affected APIs

- `M:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message)`

-->
