---
title: Configurazione di Internet Information Services 7.0 per Windows Communication Foundation
ms.date: 03/30/2017
ms.assetid: 1050d395-092e-44d3-b4ba-66be3b039ffb
ms.openlocfilehash: 6343049e2a21b06965a8c7851d891303a49c82b5
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597566"
---
# <a name="configuring-internet-information-services-70-for-windows-communication-foundation"></a><span data-ttu-id="51608-102">Configurazione di Internet Information Services 7.0 per Windows Communication Foundation</span><span class="sxs-lookup"><span data-stu-id="51608-102">Configuring Internet Information Services 7.0 for Windows Communication Foundation</span></span>

<span data-ttu-id="51608-103">Internet Information Services (IIS) 7.0 dispone di una progettazione modulare che consente di installare in modo selettivo i componenti necessari.</span><span class="sxs-lookup"><span data-stu-id="51608-103">Internet Information Services (IIS) 7.0 has a modular design that allows you to selectively install components that are required.</span></span> <span data-ttu-id="51608-104">Questa progettazione è basata sulla nuova tecnologia di componentizzazione basata su manifesto introdotta in Windows Vista.</span><span class="sxs-lookup"><span data-stu-id="51608-104">This design is based on the new manifest-driven componentization technology introduced in Windows Vista.</span></span> <span data-ttu-id="51608-105">Sono presenti più di 40 componenti di funzionalità autonomi di IIS 7,0 che possono essere installati in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="51608-105">There are more than 40 standalone feature components of IIS 7.0 that can be installed independently.</span></span> <span data-ttu-id="51608-106">I professionisti IT possono così personalizzare con facilità l'installazione in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="51608-106">This allows IT professionals to easily customize the installation as required.</span></span> <span data-ttu-id="51608-107">In questo argomento viene illustrato come configurare IIS 7,0 per l'utilizzo con Windows Communication Foundation (WCF) e come determinare i componenti necessari.</span><span class="sxs-lookup"><span data-stu-id="51608-107">This topic discusses how to configure IIS 7.0 for use with Windows Communication Foundation (WCF) and determine which components are required.</span></span>

## <a name="minimal-installation-installing-was"></a><span data-ttu-id="51608-108">Installazione minima: installazione di WAS</span><span class="sxs-lookup"><span data-stu-id="51608-108">Minimal Installation: Installing WAS</span></span>
 <span data-ttu-id="51608-109">L'installazione minima dell'intero pacchetto IIS 7,0 consiste nell'installare il servizio Attivazione processo Windows (WAS).</span><span class="sxs-lookup"><span data-stu-id="51608-109">The minimal installation of the whole IIS 7.0 package is to install the Windows Process Activation Service (WAS).</span></span> <span data-ttu-id="51608-110">WAS è una funzionalità autonoma ed è l'unica funzionalità di IIS 7,0 disponibile per tutti i sistemi operativi Windows Vista (Home Basic, Home Premium, business, Ultimate ed Enterprise).</span><span class="sxs-lookup"><span data-stu-id="51608-110">WAS is a standalone feature and it is the only feature from the IIS 7.0 that is available for all Windows Vista operating systems (Home Basic, Home Premium, Business, and Ultimate and Enterprise).</span></span>

 <span data-ttu-id="51608-111">Nel pannello di controllo fare clic su **programmi** e quindi **su attivazione o disattivazione delle funzionalità Windows** elencate in **programmi e funzionalità**. il componente was viene visualizzato nell'elenco, come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="51608-111">From the Control Panel, click **Programs** and then click **Turn Windows features on or off** which is listed under **Programs and Features**, the WAS component is shown in the list as in the following illustration.</span></span>

 <span data-ttu-id="51608-112">![Finestra di dialogo di attivazione o disattivazione delle funzionalità](media/wcfc-turnfeaturesonoroffs.gif "wcfc_TurnFeaturesOnOrOffs")</span><span class="sxs-lookup"><span data-stu-id="51608-112">![Turn Features On or Off Dialog](media/wcfc-turnfeaturesonoroffs.gif "wcfc_TurnFeaturesOnOrOffs")</span></span>

 <span data-ttu-id="51608-113">Questa funzionalità presenta i sottocomponenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="51608-113">This feature has the following sub-components:</span></span>

- <span data-ttu-id="51608-114">Ambiente .NET</span><span class="sxs-lookup"><span data-stu-id="51608-114">.NET Environment</span></span>

- <span data-ttu-id="51608-115">API di configurazione</span><span class="sxs-lookup"><span data-stu-id="51608-115">Configuration APIs</span></span>

- <span data-ttu-id="51608-116">Modello di processo</span><span class="sxs-lookup"><span data-stu-id="51608-116">Process Model</span></span>

 <span data-ttu-id="51608-117">Se si seleziona il nodo radice di WAS, per impostazione predefinita viene selezionato solo il sottonodo del **modello di processo** .</span><span class="sxs-lookup"><span data-stu-id="51608-117">If you select the root node of WAS, only the **Process Model** sub-node is checked by default.</span></span> <span data-ttu-id="51608-118">Si noti che con questa installazione verrà installato solo il servizio WAS poiché non è disponibile alcun supporto per un server Web.</span><span class="sxs-lookup"><span data-stu-id="51608-118">Please note that with this installation you are only installing WAS, because there is no support for a Web server.</span></span>

 <span data-ttu-id="51608-119">Per far funzionare WCF o qualsiasi applicazione ASP.NET, selezionare la casella di controllo **ambiente .NET** .</span><span class="sxs-lookup"><span data-stu-id="51608-119">To make WCF or any ASP.NET application work, check the **.NET Environment** checkbox.</span></span> <span data-ttu-id="51608-120">Ciò significa che tutti i componenti di WAS sono necessari per garantire il corretto funzionamento di WCF e ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="51608-120">This means that all of WAS components are required to make WCF and ASP.NET to work well.</span></span> <span data-ttu-id="51608-121">Questi verranno selezionati automaticamente una volta installati tali componenti.</span><span class="sxs-lookup"><span data-stu-id="51608-121">These are automatically checked once you install any of those components.</span></span>

## <a name="iis-70-default-installation"></a><span data-ttu-id="51608-122">IIS 7.0: installazione predefinita</span><span class="sxs-lookup"><span data-stu-id="51608-122">IIS 7.0: Default Installation</span></span>
 <span data-ttu-id="51608-123">Controllando la funzionalità **Internet Information Services** , alcuni dei sottonodi vengono controllati automaticamente, come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="51608-123">By checking the **Internet Information Services** feature, some of the sub-nodes are automatically checked as shown in the following illustration.</span></span>

 <span data-ttu-id="51608-124">![Impostazioni predefinite per le funzionalità di IIS 7.0](media/wcfc-turningfeaturesonoroff2.gif "wcfc_TurningFeaturesOnOrOff2")</span><span class="sxs-lookup"><span data-stu-id="51608-124">![Default settings for IIS 7.0 features](media/wcfc-turningfeaturesonoroff2.gif "wcfc_TurningFeaturesOnOrOff2")</span></span>

 <span data-ttu-id="51608-125">Questa è l'installazione predefinita di IIS 7,0.</span><span class="sxs-lookup"><span data-stu-id="51608-125">This is the default installation of IIS 7.0.</span></span> <span data-ttu-id="51608-126">Con questa installazione è possibile usare IIS 7,0 per il servizio di contenuto statico, ad esempio pagine HTML e altro contenuto.</span><span class="sxs-lookup"><span data-stu-id="51608-126">With this installation, you can use IIS 7.0 to service static content (such as HTML pages and other content).</span></span> <span data-ttu-id="51608-127">Tuttavia, non è possibile eseguire applicazioni ASP.NET o CGI né ospitare servizi WCF.</span><span class="sxs-lookup"><span data-stu-id="51608-127">However, you cannot run ASP.NET or CGI applications or host WCF services.</span></span>

## <a name="iis-70-installation-with-aspnet-support"></a><span data-ttu-id="51608-128">IIS 7.0: installazione con supporto ASP.NET</span><span class="sxs-lookup"><span data-stu-id="51608-128">IIS 7.0: Installation with ASP.NET Support</span></span>
 <span data-ttu-id="51608-129">È necessario installare ASP.NET per fare in modo che ASP.NET funzioni in IIS 7,0.</span><span class="sxs-lookup"><span data-stu-id="51608-129">You must install ASP.NET to make ASP.NET work on IIS 7.0.</span></span> <span data-ttu-id="51608-130">Dopo aver controllato **ASP.NET**, la schermata dovrebbe essere simile alla figura seguente.</span><span class="sxs-lookup"><span data-stu-id="51608-130">After checking **ASP.NET**, your screen should look like the following illustration.</span></span>

 <span data-ttu-id="51608-131">![Impostazioni obbligatorie per ASP.NET](media/wcfc-trunfeaturesonoroff3s.gif "wcfc_TrunFeaturesOnOrOFf3s")</span><span class="sxs-lookup"><span data-stu-id="51608-131">![Asp.NET required settings](media/wcfc-trunfeaturesonoroff3s.gif "wcfc_TrunFeaturesOnOrOFf3s")</span></span>

 <span data-ttu-id="51608-132">Si tratta dell'ambiente minimo per le applicazioni WCF e ASP.NET per il funzionamento in IIS 7,0.</span><span class="sxs-lookup"><span data-stu-id="51608-132">This is the minimal environment for both WCF and ASP.NET applications to work in IIS 7.0.</span></span>

## <a name="iis-70-installation-with-iis-60-compatibility-components"></a><span data-ttu-id="51608-133">IIS 7.0: installazione con componenti compatibilità gestione IIS 6.0</span><span class="sxs-lookup"><span data-stu-id="51608-133">IIS 7.0: Installation with IIS 6.0 Compatibility Components</span></span>
 <span data-ttu-id="51608-134">Quando si installa IIS 7,0 in un sistema con Visual Studio 2005 o altri script o strumenti di automazione (ad esempio adsutil. vbs) che configurano le applicazioni virtuali che utilizzano l'API metabase di IIS 6,0, assicurarsi di controllare gli **strumenti di script**di IIS 6,0.</span><span class="sxs-lookup"><span data-stu-id="51608-134">When installing IIS 7.0 on a system with Visual Studio 2005 or some other automation scripts or tools (such as Adsutil.vbs) that configure virtual applications that use IIS 6.0 Metabase API, ensure that you check the IIS 6.0 **Scripting Tools**.</span></span> <span data-ttu-id="51608-135">Questa operazione Controlla automaticamente gli altri sottonodi della compatibilità di **gestione**con IIS 6,0.</span><span class="sxs-lookup"><span data-stu-id="51608-135">This automatically checks the other sub-nodes of IIS 6.0 **Management Compatibility**.</span></span> <span data-ttu-id="51608-136">Nella figura seguente viene mostrata la schermata dopo questa operazione:</span><span class="sxs-lookup"><span data-stu-id="51608-136">The following illustration shows the screen after this is done:</span></span>

 <span data-ttu-id="51608-137">![Impostazioni di Compatibilità di gestione con IIS 6.0](media/scfc-turnfeaturesonoroff5s.gif "scfc_TurnFeaturesOnOrOff5s")</span><span class="sxs-lookup"><span data-stu-id="51608-137">![IIS 6.0 Management Compatibility Settings](media/scfc-turnfeaturesonoroff5s.gif "scfc_TurnFeaturesOnOrOff5s")</span></span>

 <span data-ttu-id="51608-138">Con questa installazione, sono disponibili tutti gli elementi necessari per usare le funzionalità e gli esempi di IIS 7,0, ASP.NET e WCF disponibili sul Web.</span><span class="sxs-lookup"><span data-stu-id="51608-138">With this installation, you have everything required to use IIS 7.0, ASP.NET and WCF features and samples available on the Web.</span></span>

## <a name="request-limits"></a><span data-ttu-id="51608-139">Limiti di richiesta.</span><span class="sxs-lookup"><span data-stu-id="51608-139">Request Limits</span></span>
 <span data-ttu-id="51608-140">In Windows Vista con IIS 7 il valore predefinito delle `maxUri` Impostazioni e `maxQueryStringSize` è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="51608-140">On Windows Vista with IIS 7 the default value of the `maxUri` and `maxQueryStringSize` settings have been changed.</span></span> <span data-ttu-id="51608-141">Per impostazione predefinita, il filtro di richiesta in IIS 7.0 consente una lunghezza dell'URL di 4096 caratteri e una lunghezza della stringa di query di 2048 caratteri.</span><span class="sxs-lookup"><span data-stu-id="51608-141">By default, request filtering in IIS 7.0 allows a URL length of 4096 characters and a query string length of 2048 characters.</span></span> <span data-ttu-id="51608-142">Per modificare questi valori predefiniti, aggiungere il codice XML seguente al file App.config:</span><span class="sxs-lookup"><span data-stu-id="51608-142">To change these defaults add the following XML to your App.config file.</span></span>

```xml
 <system.webServer>
    <security>
        <requestFiltering>
            <requestLimits maxUrl="8192" maxQueryString="8192" />
        </requestFiltering>
    </security>
 </system.webServer>
 ```

## <a name="see-also"></a><span data-ttu-id="51608-143">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="51608-143">See also</span></span>

- [<span data-ttu-id="51608-144">Architettura di attivazione WAS</span><span class="sxs-lookup"><span data-stu-id="51608-144">WAS Activation Architecture</span></span>](was-activation-architecture.md)
- [<span data-ttu-id="51608-145">Configurazione di WAS per l'uso con WCF</span><span class="sxs-lookup"><span data-stu-id="51608-145">Configuring WAS for Use with WCF</span></span>](configuring-the-wpa--service-for-use-with-wcf.md)
- [<span data-ttu-id="51608-146">Procedura: installare e configurare componenti di attivazione WCF</span><span class="sxs-lookup"><span data-stu-id="51608-146">How to: Install and Configure WCF Activation Components</span></span>](how-to-install-and-configure-wcf-activation-components.md)
- <span data-ttu-id="51608-147">[Funzionalità di hosting di Windows Server AppFabric](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="51608-147">[Windows Server App Fabric Hosting Features](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))</span></span>
