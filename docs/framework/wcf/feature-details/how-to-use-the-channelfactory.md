---
title: 'Procedura: usare ChannelFactory'
description: Informazioni su come creare una channel factory per creare più di un canale per accedere ai servizi tramite un client WCF.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d48f01b5-582b-4c8b-b547-8adddae7e371
ms.openlocfilehash: 7c87026ca4cf7c739f4615da9bc7f0272a382392
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246662"
---
# <a name="how-to-use-the-channelfactory"></a><span data-ttu-id="5678c-103">Procedura: usare ChannelFactory</span><span class="sxs-lookup"><span data-stu-id="5678c-103">How to: Use the ChannelFactory</span></span>
<span data-ttu-id="5678c-104">La classe generica <xref:System.ServiceModel.ChannelFactory%601> viene usata in scenari avanzati che richiedono la creazione di una channel factory utilizzabile per creare più di un canale.</span><span class="sxs-lookup"><span data-stu-id="5678c-104">The generic <xref:System.ServiceModel.ChannelFactory%601> class is used in advanced scenarios that require the creation of a channel factory that can be used to create more than one channel.</span></span>  
  
### <a name="to-create-and-use-the-channelfactory-class"></a><span data-ttu-id="5678c-105">Per creare e usare la classe ChannelFactory</span><span class="sxs-lookup"><span data-stu-id="5678c-105">To create and use the ChannelFactory class</span></span>  
  
1. <span data-ttu-id="5678c-106">Compilazione ed esecuzione di un servizio Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="5678c-106">Build and run an Windows Communication Foundation (WCF) service.</span></span> <span data-ttu-id="5678c-107">Per ulteriori informazioni, vedere [progettazione e implementazione di servizi](../designing-and-implementing-services.md), [configurazione di servizi](../configuring-services.md)e [hosting di servizi](../hosting-services.md).</span><span class="sxs-lookup"><span data-stu-id="5678c-107">For more information, see [Designing and Implementing Services](../designing-and-implementing-services.md), [Configuring Services](../configuring-services.md), and [Hosting Services](../hosting-services.md).</span></span>  
  
2. <span data-ttu-id="5678c-108">Utilizzare lo [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) per generare il contratto (interfaccia) per il client.</span><span class="sxs-lookup"><span data-stu-id="5678c-108">Use the [ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) to generate the contract (interface) for the client.</span></span>  
  
3. <span data-ttu-id="5678c-109">Nel codice client, usare la classe <xref:System.ServiceModel.ChannelFactory%601> per creare più listener endpoint.</span><span class="sxs-lookup"><span data-stu-id="5678c-109">In the client code, use the <xref:System.ServiceModel.ChannelFactory%601> class to create multiple endpoint listeners.</span></span>  
  
## <a name="example"></a><span data-ttu-id="5678c-110">Esempio</span><span class="sxs-lookup"><span data-stu-id="5678c-110">Example</span></span>  
 [!code-csharp[c_HowToUseChannelFactory#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtousechannelfactory/cs/source.cs#1)]
 [!code-vb[c_HowToUseChannelFactory#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtousechannelfactory/vb/source.vb#1)]
