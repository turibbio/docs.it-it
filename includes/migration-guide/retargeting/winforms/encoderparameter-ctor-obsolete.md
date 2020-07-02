---
ms.openlocfilehash: 4ad7c4c2781480c08ad4cf27e40de445b1c50671
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617243"
---
### <a name="encoderparameter-ctor-is-obsolete"></a><span data-ttu-id="eb789-101">Il costruttore EncoderParameter è obsoleto</span><span class="sxs-lookup"><span data-stu-id="eb789-101">EncoderParameter ctor is obsolete</span></span>

#### <a name="details"></a><span data-ttu-id="eb789-102">Dettagli</span><span class="sxs-lookup"><span data-stu-id="eb789-102">Details</span></span>

<span data-ttu-id="eb789-103">Il costruttore <xref:System.Drawing.Imaging.EncoderParameter.%23ctor(System.Drawing.Imaging.Encoder,System.Int32,System.Int32,System.Int32,System.Int32)> è ora obsoleto e l'eventuale uso causerà avvisi di compilazione.</span><span class="sxs-lookup"><span data-stu-id="eb789-103">The <xref:System.Drawing.Imaging.EncoderParameter.%23ctor(System.Drawing.Imaging.Encoder,System.Int32,System.Int32,System.Int32,System.Int32)> constructor is obsolete now and will introduce build warnings if used.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="eb789-104">Suggerimento</span><span class="sxs-lookup"><span data-stu-id="eb789-104">Suggestion</span></span>

<span data-ttu-id="eb789-105">Anche se il costruttore <xref:System.Drawing.Imaging.EncoderParameter.%23ctor(System.Drawing.Imaging.Encoder,System.Int32,System.Int32,System.Int32,System.Int32)> continuerà a funzionare, è necessario usare il costruttore seguente per evitare l'avviso di compilazione obsoleto durante la ricompilazione del codice con gli strumenti di .NET Framework 4.5: <xref:System.Drawing.Imaging.EncoderParameter.%23ctor(System.Drawing.Imaging.Encoder,System.Int32,System.Drawing.Imaging.EncoderParameterValueType,System.IntPtr)>.</span><span class="sxs-lookup"><span data-stu-id="eb789-105">Although the <xref:System.Drawing.Imaging.EncoderParameter.%23ctor(System.Drawing.Imaging.Encoder,System.Int32,System.Int32,System.Int32,System.Int32)>constructor will continue to work, the following constructor should be used instead to avoid the obsolete build warning when re-compiling code with .NET Framework  4.5 tools: <xref:System.Drawing.Imaging.EncoderParameter.%23ctor(System.Drawing.Imaging.Encoder,System.Int32,System.Drawing.Imaging.EncoderParameterValueType,System.IntPtr)>.</span></span>

| <span data-ttu-id="eb789-106">Nome</span><span class="sxs-lookup"><span data-stu-id="eb789-106">Name</span></span>    | <span data-ttu-id="eb789-107">Valore</span><span class="sxs-lookup"><span data-stu-id="eb789-107">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="eb789-108">Scope</span><span class="sxs-lookup"><span data-stu-id="eb789-108">Scope</span></span>   | <span data-ttu-id="eb789-109">Minorenne</span><span class="sxs-lookup"><span data-stu-id="eb789-109">Minor</span></span>       |
| <span data-ttu-id="eb789-110">Version</span><span class="sxs-lookup"><span data-stu-id="eb789-110">Version</span></span> | <span data-ttu-id="eb789-111">4.5</span><span class="sxs-lookup"><span data-stu-id="eb789-111">4.5</span></span>         |
| <span data-ttu-id="eb789-112">Type</span><span class="sxs-lookup"><span data-stu-id="eb789-112">Type</span></span>    | <span data-ttu-id="eb789-113">Ridestinazione</span><span class="sxs-lookup"><span data-stu-id="eb789-113">Retargeting</span></span> |

#### <a name="affected-apis"></a><span data-ttu-id="eb789-114">API interessate</span><span class="sxs-lookup"><span data-stu-id="eb789-114">Affected APIs</span></span>

- <xref:System.Drawing.Imaging.EncoderParameter.%23ctor(System.Drawing.Imaging.Encoder,System.Int32,System.Int32,System.Int32,System.Int32)>
