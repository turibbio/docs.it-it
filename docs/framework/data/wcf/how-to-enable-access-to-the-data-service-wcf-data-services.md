---
title: "Procedura: abilitare l'accesso al servizio dati (WCF Data Services)"
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, configuring
ms.assetid: 3d830bcd-32b4-4f26-9287-d58a071452c6
ms.openlocfilehash: 0ec9c9a730516b22b4eaa215e042e9393c01d752
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2019
ms.locfileid: "74569099"
---
# <a name="how-to-enable-access-to-the-data-service-wcf-data-services"></a>Procedura: abilitare l'accesso al servizio dati (WCF Data Services)
In WCF Data Services, è necessario concedere in modo esplicito l'accesso alle risorse esposte da un servizio dati. In altre parole, dopo aver creato un nuovo servizio dati, è necessario fornire in modo esplicito l'accesso alle singole risorse come set di entità. In questo argomento viene illustrato come abilitare l'accesso in lettura e scrittura a cinque dei set di entità nel servizio dati Northwind creato al completamento della [Guida introduttiva](quickstart-wcf-data-services.md). Poiché l'enumerazione <xref:System.Data.Services.EntitySetRights> viene definita tramite <xref:System.FlagsAttribute>, è possibile utilizzare un operatore logico OR per specificare più autorizzazioni per un solo set di entità.  
  
> [!NOTE]
> I client che possono accedere all'applicazione ASP.NET saranno inoltre in grado di accedere alle risorse esposte dal servizio dati. Per impedire l'accesso non autorizzato alle risorse in un servizio dati di produzione, è inoltre necessario proteggere l'applicazione stessa. Per ulteriori informazioni, vedere [protezione di siti Web ASP.NET](https://docs.microsoft.com/previous-versions/aspnet/91f66yxt(v=vs.100)).  
  
### <a name="to-enable-access-to-the-data-service"></a>Per abilitare l'accesso al servizio dati  
  
- Nel codice per il servizio dati sostituire il codice segnaposto nella funzione `InitializeService` con il codice seguente:  
  
     [!code-csharp[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_service/cs/northwind.svc.cs#allreadconfig)]
     [!code-vb[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_service/vb/northwind.svc.vb#allreadconfig)]  
  
     In questo modo i client saranno in grado di accedere in lettura e scrittura ai set di entità `Orders` e `Order_Details` e solo in lettura ai set di entità `Customers`.  
  
## <a name="see-also"></a>Vedere anche

- [Procedura: sviluppare un servizio WCF in esecuzione in IIS](how-to-develop-a-wcf-data-service-running-on-iis.md)
- [Configurazione del servizio dati](configuring-the-data-service-wcf-data-services.md)
