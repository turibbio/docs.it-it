---
title: Globalizzazione e localizzazione di applicazioni .NET
ms.date: 06/08/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- international applications [.NET]
- globalization [.NET], encoding
- global applications
- internationalization
- world-ready applications
- application development [.NET], globalization
- multilingual application development
ms.assetid: 9a59696b-d89b-45bd-946d-c75da4732d02
ms.openlocfilehash: c5c601d18d92d9b57781bc8a09f26f0bc3a9216a
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842010"
---
# <a name="globalizing-and-localizing-net-applications"></a><span data-ttu-id="beaab-102">Globalizzazione e localizzazione di applicazioni .NET</span><span class="sxs-lookup"><span data-stu-id="beaab-102">Globalizing and localizing .NET applications</span></span>

<span data-ttu-id="beaab-103">Lo sviluppo di applicazioni internazionali, tra cui un'applicazione che può essere localizzata in una o più lingue, include tre passaggi: globalizzazione, analisi della localizzabilità e localizzazione.</span><span class="sxs-lookup"><span data-stu-id="beaab-103">Developing a world-ready application, including an application that can be localized into one or more languages, involves three steps: globalization, localizability review, and localization.</span></span>

[<span data-ttu-id="beaab-104">Globalizzazione</span><span class="sxs-lookup"><span data-stu-id="beaab-104">Globalization</span></span>](globalization.md)

<span data-ttu-id="beaab-105">Questo passaggio implica la progettazione e la codifica di un'applicazione indipendente dalle impostazioni cultura e dalla lingua che supporti le interfacce utente e i dati internazionali localizzati per tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="beaab-105">This step involves designing and coding an application that is culture-neutral and language-neutral, and that supports localized user interfaces and regional data for all users.</span></span> <span data-ttu-id="beaab-106">Comporta decisioni di progettazione e programmazione non basate su presupposti impostazioni cultura specifiche.</span><span class="sxs-lookup"><span data-stu-id="beaab-106">It involves making design and programming decisions that are not based on culture-specific assumptions.</span></span> <span data-ttu-id="beaab-107">Quando un'applicazione globalizzata non viene localizzata, è tuttavia progettata e scritta in modo da poter essere successivamente localizzata in una o più lingue in modo relativamente semplice.</span><span class="sxs-lookup"><span data-stu-id="beaab-107">While a globalized application is not localized, it nevertheless is designed and written so that it can be subsequently localized into one or more languages with relative ease.</span></span>

[<span data-ttu-id="beaab-108">Revisione della localizzabilità</span><span class="sxs-lookup"><span data-stu-id="beaab-108">Localizability review</span></span>](localizability-review.md)

<span data-ttu-id="beaab-109">Questo passaggio prevede la revisione del codice e del progetto di un'applicazione per verificare che possa essere localizzata facilmente e per identificare potenziali problemi per la localizzazione e la verifica che il codice eseguibile dell'applicazione sia separato dalle relative risorse.</span><span class="sxs-lookup"><span data-stu-id="beaab-109">This step involves reviewing an application's code and design to ensure that it can be localized easily and to identify potential roadblocks for localization, and verifying that the application's executable code is separated from its resources.</span></span> <span data-ttu-id="beaab-110">Se la fase di globalizzazione ha avuto effetto, l'analisi della localizzabilità confermerà le scelte di codifica e di progettazione effettuate durante la globalizzazione.</span><span class="sxs-lookup"><span data-stu-id="beaab-110">If the globalization stage was effective, the localizability review will confirm the design and coding choices made during globalization.</span></span> <span data-ttu-id="beaab-111">La fase di localizzabilità può inoltre identificare eventuali problemi rimanenti. In questo modo, il codice sorgente di un'applicazione non deve necessariamente essere modificato durante la fase di localizzazione.</span><span class="sxs-lookup"><span data-stu-id="beaab-111">The localizability stage may also identify any remaining issues so that an application's source code doesn't have to be modified during the localization stage.</span></span>

[<span data-ttu-id="beaab-112">Localizzazione</span><span class="sxs-lookup"><span data-stu-id="beaab-112">Localization</span></span>](localization.md)

<span data-ttu-id="beaab-113">Questo passaggio prevede la personalizzazione di un'applicazione per impostazioni cultura e aree specifiche.</span><span class="sxs-lookup"><span data-stu-id="beaab-113">This step involves customizing an application for specific cultures or regions.</span></span> <span data-ttu-id="beaab-114">Se i passaggi di globalizzazione e possibilità di localizzazione sono stati eseguiti correttamente, la localizzazione consiste principalmente nella traduzione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="beaab-114">If the globalization and localizability steps have been performed correctly, localization consists primarily of translating the user interface.</span></span>

<span data-ttu-id="beaab-115">Se si ci attiene ai seguenti tre passaggi verranno offerti due vantaggi:</span><span class="sxs-lookup"><span data-stu-id="beaab-115">Following these three steps provides two advantages:</span></span>

- <span data-ttu-id="beaab-116">In questo modo, non è necessario adattare un'applicazione progettata per supportare singole lingue, ad esempio Inglese US (Stati Uniti), per supportare le lingue aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="beaab-116">It frees you from having to retrofit an application that is designed to support a single culture, such as U.S. English, to support additional cultures.</span></span>

- <span data-ttu-id="beaab-117">Restituisce applicazioni localizzate che sono più stabile e con meno bug.</span><span class="sxs-lookup"><span data-stu-id="beaab-117">It results in localized applications that are more stable and have fewer bugs.</span></span>

<span data-ttu-id="beaab-118">In .NET viene fornito ampio supporto per lo sviluppo di applicazioni internazionali e localizzate.</span><span class="sxs-lookup"><span data-stu-id="beaab-118">.NET provides extensive support for the development of world-ready and localized applications.</span></span> <span data-ttu-id="beaab-119">In particolare, molti membri del tipo nella libreria di classi .NET facilitano la globalizzazione restituendo valori che riflettono le convenzioni delle impostazioni cultura dell'utente o di impostazioni cultura specifiche.</span><span class="sxs-lookup"><span data-stu-id="beaab-119">In particular, many type members in the .NET class library aid globalization by returning values that reflect the conventions of either the current user's culture or a specified culture.</span></span> <span data-ttu-id="beaab-120">.NET supporta inoltre gli assembly satellite che semplificano il processo di localizzazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="beaab-120">Also, .NET supports satellite assemblies, which facilitate the process of localizing an application.</span></span>

<span data-ttu-id="beaab-121">Per altre informazioni, vedere la [documentazione sulla globalizzazione](/globalization/).</span><span class="sxs-lookup"><span data-stu-id="beaab-121">For additional information, see the [Globalization documentation](/globalization/).</span></span>

## <a name="in-this-section"></a><span data-ttu-id="beaab-122">Contenuto della sezione</span><span class="sxs-lookup"><span data-stu-id="beaab-122">In this section</span></span>

[<span data-ttu-id="beaab-123">Globalizzazione</span><span class="sxs-lookup"><span data-stu-id="beaab-123">Globalization</span></span>](globalization.md)

<span data-ttu-id="beaab-124">Viene descritta la prima fase di creazione di un'applicazione internazionale, che include la progettazione e la codifica di un'applicazione indipendente dalla lingua e dalle impostazioni cultura.</span><span class="sxs-lookup"><span data-stu-id="beaab-124">Discusses the first stage of creating a world-ready application, which involves designing and coding an application that is culture-neutral and language-neutral.</span></span>

[<span data-ttu-id="beaab-125">Globalizzazione .NET e ICU</span><span class="sxs-lookup"><span data-stu-id="beaab-125">.NET globalization and ICU</span></span>](globalization-icu.md)

<span data-ttu-id="beaab-126">Viene descritto in che modo la globalizzazione di .NET usa [i componenti internazionali per Unicode (ICU)](http://site.icu-project.org/home).</span><span class="sxs-lookup"><span data-stu-id="beaab-126">Describes how .NET globalization uses [International Components for Unicode (ICU)](http://site.icu-project.org/home).</span></span>

[<span data-ttu-id="beaab-127">Revisione della localizzabilità</span><span class="sxs-lookup"><span data-stu-id="beaab-127">Localizability review</span></span>](localizability-review.md)

<span data-ttu-id="beaab-128">Viene descritta la seconda fase di creazione di un'applicazione localizzata, che include l'identificazione dei potenziali blocchi stradali per la localizzazione.</span><span class="sxs-lookup"><span data-stu-id="beaab-128">Discusses the second stage of creating a localized application, which involves identifying potential roadblocks to localization.</span></span>

[<span data-ttu-id="beaab-129">Localizzazione</span><span class="sxs-lookup"><span data-stu-id="beaab-129">Localization</span></span>](localization.md)

<span data-ttu-id="beaab-130">Viene illustrata la fase finale della creazione di un'applicazione localizzata, che include la personalizzazione di un'interfaccia utente dell'applicazione per le aree o le impostazioni cultura specifiche.</span><span class="sxs-lookup"><span data-stu-id="beaab-130">Discusses the final stage of creating a localized application, which involves customizing an application's user interface for specific regions or cultures.</span></span>

[<span data-ttu-id="beaab-131">Operazioni sulle stringhe indipendenti dalle impostazioni cultura</span><span class="sxs-lookup"><span data-stu-id="beaab-131">Culture-insensitive string operations</span></span>](culture-insensitive-string-operations.md)

<span data-ttu-id="beaab-132">Viene descritto come usare metodi e classi di .NET definiti come dipendenti dalle impostazioni cultura per impostazione predefinita per ottenere risultati indipendenti dalle impostazioni cultura.</span><span class="sxs-lookup"><span data-stu-id="beaab-132">Describes how to use .NET methods and classes that are culture-sensitive by default to obtain culture-insensitive results.</span></span>

[<span data-ttu-id="beaab-133">Procedure consigliate per lo sviluppo di applicazioni internazionali</span><span class="sxs-lookup"><span data-stu-id="beaab-133">Best practices for developing world-ready applications</span></span>](best-practices-for-developing-world-ready-apps.md)

<span data-ttu-id="beaab-134">Vengono forniti alcuni suggerimenti per la globalizzazione, la localizzazione e lo sviluppo di applicazioni ASP.NET internazionali.</span><span class="sxs-lookup"><span data-stu-id="beaab-134">Describes the best practices to follow for globalization, localization, and developing world-ready ASP.NET applications.</span></span>

## <a name="reference"></a><span data-ttu-id="beaab-135">Riferimento</span><span class="sxs-lookup"><span data-stu-id="beaab-135">Reference</span></span>

- <span data-ttu-id="beaab-136">Spazio dei nomi <xref:System.Globalization?displayProperty=nameWithType></span><span class="sxs-lookup"><span data-stu-id="beaab-136"><xref:System.Globalization?displayProperty=nameWithType> namespace</span></span>

   <span data-ttu-id="beaab-137">Contiene classi che definiscono informazioni sulle impostazioni cultura, tra cui la lingua, il paese, il calendario, il formato delle date, delle valute e dei numeri e il criterio di ordinamento delle stringhe.</span><span class="sxs-lookup"><span data-stu-id="beaab-137">Contains classes that define culture-related information, including the language, the country/region, the calendars in use, the format patterns for dates, currency, and numbers, and the sort order for strings.</span></span>

- <span data-ttu-id="beaab-138">Spazio dei nomi <xref:System.Resources></span><span class="sxs-lookup"><span data-stu-id="beaab-138"><xref:System.Resources> namespace</span></span>

   <span data-ttu-id="beaab-139">Vengono fornite le classi per la creazione, la manipolazione e l'uso di risorse.</span><span class="sxs-lookup"><span data-stu-id="beaab-139">Provides classes for creating, manipulating, and using resources.</span></span>

- <span data-ttu-id="beaab-140">Spazio dei nomi <xref:System.Text></span><span class="sxs-lookup"><span data-stu-id="beaab-140"><xref:System.Text> namespace</span></span>

   <span data-ttu-id="beaab-141">Contiene le classi che rappresentano le codifiche dei caratteri ASCII, ANSI, Unicode e altri tipi di codifiche.</span><span class="sxs-lookup"><span data-stu-id="beaab-141">Contains classes representing ASCII, ANSI, Unicode, and other character encodings.</span></span>

- [<span data-ttu-id="beaab-142">Resgen. exe (Generatore di file di risorse)</span><span class="sxs-lookup"><span data-stu-id="beaab-142">Resgen.exe (Resource File Generator)</span></span>](../../../docs/framework/tools/resgen-exe-resource-file-generator.md)

   <span data-ttu-id="beaab-143">Viene descritto l'utilizzo di Resgen.exe per convertire i file con estensione txt e resx (formato risorse basato su XML) in file binari con estensione resources di Common Language Runtime.</span><span class="sxs-lookup"><span data-stu-id="beaab-143">Describes how to use Resgen.exe to convert .txt files and XML-based resource format (.resx) files to common language runtime binary .resources files.</span></span>

- [<span data-ttu-id="beaab-144">Winres. exe (editor di risorse Windows Forms)</span><span class="sxs-lookup"><span data-stu-id="beaab-144">Winres.exe (Windows Forms Resource Editor)</span></span>](../../../docs/framework/tools/winres-exe-windows-forms-resource-editor.md)

   <span data-ttu-id="beaab-145">Viene descritto l'uso di Winres.exe per localizzare i form di Windows Form.</span><span class="sxs-lookup"><span data-stu-id="beaab-145">Describes how to use Winres.exe to localize Windows Forms forms.</span></span>
