---
ms.openlocfilehash: 87ada29e70a94c39e7ffb74767b99d49c52444af
ms.sourcegitcommit: 348bb052d5cef109a61a3d5253faa5d7167d55ac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2020
ms.locfileid: "82021570"
---
### <a name="floating-point-parsing-operations-no-longer-fail-or-throw-an-overflowexception"></a><span data-ttu-id="def25-101">Le operazioni di analisi a virgola mobile non hanno più esito negativo o generano un'eccezione OverflowException</span><span class="sxs-lookup"><span data-stu-id="def25-101">Floating-point parsing operations no longer fail or throw an OverflowException</span></span>

<span data-ttu-id="def25-102">I metodi di analisi a virgola <xref:System.OverflowException> mobile `false` non generano più un o restituito quando <xref:System.Single> <xref:System.Double> analizzano una stringa il cui valore numerico non è compreso nell'intervallo del tipo o a virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="def25-102">The floating-point parsing methods no longer throw an <xref:System.OverflowException> or return `false` when they parse a string whose numeric value is outside the range of the <xref:System.Single> or <xref:System.Double> floating-point type.</span></span>

#### <a name="change-description"></a><span data-ttu-id="def25-103">Descrizione modifica:</span><span class="sxs-lookup"><span data-stu-id="def25-103">Change description</span></span>

<span data-ttu-id="def25-104">In .NET Core 2.2 e <xref:System.Double.Parse%2A?displayProperty=nameWithType> <xref:System.Single.Parse%2A?displayProperty=nameWithType> versioni precedenti, i metodi e generano un <xref:System.OverflowException> for valori che non rientrano nell'intervallo del rispettivo tipo.</span><span class="sxs-lookup"><span data-stu-id="def25-104">In .NET Core 2.2 and earlier versions, the <xref:System.Double.Parse%2A?displayProperty=nameWithType> and <xref:System.Single.Parse%2A?displayProperty=nameWithType> methods throw an <xref:System.OverflowException> for values that outside the range of their respective type.</span></span> <span data-ttu-id="def25-105">I <xref:System.Double.TryParse%2A?displayProperty=nameWithType> <xref:System.Single.TryParse%2A?displayProperty=nameWithType> metodi `false` e restituiscono per le rappresentazioni di stringa di valori numerici non compresi nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="def25-105">The <xref:System.Double.TryParse%2A?displayProperty=nameWithType> and <xref:System.Single.TryParse%2A?displayProperty=nameWithType> methods return `false` for the string representations of out-of-range numeric values.</span></span>

<span data-ttu-id="def25-106">A partire da .NET Core <xref:System.Double.Parse%2A?displayProperty=nameWithType> <xref:System.Double.TryParse%2A?displayProperty=nameWithType>3.0, i metodi , , <xref:System.Single.Parse%2A?displayProperty=nameWithType>e <xref:System.Single.TryParse%2A?displayProperty=nameWithType> non hanno più esito negativo durante l'analisi di stringhe numeriche non di intervallo.</span><span class="sxs-lookup"><span data-stu-id="def25-106">Starting with .NET Core 3.0, the <xref:System.Double.Parse%2A?displayProperty=nameWithType>, <xref:System.Double.TryParse%2A?displayProperty=nameWithType>, <xref:System.Single.Parse%2A?displayProperty=nameWithType>, and <xref:System.Single.TryParse%2A?displayProperty=nameWithType> methods no longer fail when parsing out-of-range numeric strings.</span></span> <span data-ttu-id="def25-107">Al contrario, <xref:System.Double> i <xref:System.Double.PositiveInfinity?displayProperty=nameWithType> metodi di <xref:System.Double.MaxValue?displayProperty=nameWithType>analisi restituiscono <xref:System.Double.NegativeInfinity?displayProperty=nameWithType> valori che superano e restituiscono valori minori di <xref:System.Double.MinValue?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="def25-107">Instead, the <xref:System.Double> parsing methods return <xref:System.Double.PositiveInfinity?displayProperty=nameWithType> for values that exceed <xref:System.Double.MaxValue?displayProperty=nameWithType>, and they return <xref:System.Double.NegativeInfinity?displayProperty=nameWithType> for values that are less than <xref:System.Double.MinValue?displayProperty=nameWithType>.</span></span> <span data-ttu-id="def25-108">Analogamente, <xref:System.Single> i metodi <xref:System.Single.PositiveInfinity?displayProperty=nameWithType> di analisi <xref:System.Single.MaxValue?displayProperty=nameWithType>restituiscono valori <xref:System.Single.NegativeInfinity?displayProperty=nameWithType> che superano <xref:System.Single.MinValue?displayProperty=nameWithType>e restituiscono valori minori di .</span><span class="sxs-lookup"><span data-stu-id="def25-108">Similarly, the <xref:System.Single> parsing methods return <xref:System.Single.PositiveInfinity?displayProperty=nameWithType> for values that exceed <xref:System.Single.MaxValue?displayProperty=nameWithType>, and they return <xref:System.Single.NegativeInfinity?displayProperty=nameWithType> for values that are less than <xref:System.Single.MinValue?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="def25-109">Questa modifica è stata apportata per migliorare la conformità IEEE 754:2008.</span><span class="sxs-lookup"><span data-stu-id="def25-109">This change was made for improved IEEE 754:2008 compliance.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="def25-110">Versione introdotta</span><span class="sxs-lookup"><span data-stu-id="def25-110">Version introduced</span></span>

<span data-ttu-id="def25-111">3.0</span><span class="sxs-lookup"><span data-stu-id="def25-111">3.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="def25-112">Azione consigliata</span><span class="sxs-lookup"><span data-stu-id="def25-112">Recommended action</span></span>

<span data-ttu-id="def25-113">Questa modifica può influire sul codice in due modi:This change can affect your code in either of two ways:</span><span class="sxs-lookup"><span data-stu-id="def25-113">This change can affect your code in either of two ways:</span></span>

- <span data-ttu-id="def25-114">Il codice dipende dal <xref:System.OverflowException> gestore per l'esecuzione quando si verifica un overflow.</span><span class="sxs-lookup"><span data-stu-id="def25-114">Your code depends on the handler for the <xref:System.OverflowException> to execute when an overflow occurs.</span></span> <span data-ttu-id="def25-115">In questo caso, è `catch` necessario rimuovere l'istruzione `If` e inserire <xref:System.Double.IsInfinity%2A?displayProperty=nameWithType> <xref:System.Single.IsInfinity%2A?displayProperty=nameWithType> il `true`codice necessario in un'istruzione che verifica se o è .</span><span class="sxs-lookup"><span data-stu-id="def25-115">In this case, you should remove the `catch` statement and place any necessary code in an `If` statement that tests whether <xref:System.Double.IsInfinity%2A?displayProperty=nameWithType> or <xref:System.Single.IsInfinity%2A?displayProperty=nameWithType> is `true`.</span></span>

- <span data-ttu-id="def25-116">Il codice presuppone che i valori `Infinity`a virgola mobile non siano .</span><span class="sxs-lookup"><span data-stu-id="def25-116">Your code assumes that floating-point values are not `Infinity`.</span></span> <span data-ttu-id="def25-117">In questo caso, è necessario aggiungere il codice necessario `PositiveInfinity` `NegativeInfinity`per verificare la presenza di valori a virgola mobile di e .</span><span class="sxs-lookup"><span data-stu-id="def25-117">In this case, you should add the necessary code to check for floating-point values of `PositiveInfinity` and `NegativeInfinity`.</span></span>

#### <a name="category"></a><span data-ttu-id="def25-118">Category</span><span class="sxs-lookup"><span data-stu-id="def25-118">Category</span></span>

<span data-ttu-id="def25-119">Librerie .NET di base</span><span class="sxs-lookup"><span data-stu-id="def25-119">Core .NET libraries</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="def25-120">API interessate</span><span class="sxs-lookup"><span data-stu-id="def25-120">Affected APIs</span></span>

- <xref:System.Double.Parse%2A?displayProperty=nameWithType>
- <xref:System.Double.TryParse%2A?displayProperty=nameWithType>
- <xref:System.Single.Parse%2A?displayProperty=nameWithType>
- <xref:System.Single.TryParse%2A?displayProperty=nameWithType>

<!--

### Affected APIs

- `Overload:System.Double.Parse`
- `Overload:System.Double.TryParse`
- `Overload:System.Single.Parse`
- `Overload:System.Single.TryParse`

-->
