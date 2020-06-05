---
title: Oggetto My.Response
ms.date: 07/20/2015
f1_keywords:
- My.MyWebExtension.Response
- My.Response
helpviewer_keywords:
- My.Response object
ms.assetid: 626359bc-3165-40b4-bfaf-2c610e26eb5b
ms.openlocfilehash: 962108264563c5e0b2894c5c856a5f23a3c1a8b4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84372460"
---
# <a name="myresponse-object"></a><span data-ttu-id="0e2d9-102">Oggetto My.Response</span><span class="sxs-lookup"><span data-stu-id="0e2d9-102">My.Response Object</span></span>
<span data-ttu-id="0e2d9-103">Ottiene l' <xref:System.Web.HttpResponse> oggetto associato all'oggetto <xref:System.Web.UI.Page> .</span><span class="sxs-lookup"><span data-stu-id="0e2d9-103">Gets the <xref:System.Web.HttpResponse> object associated with the <xref:System.Web.UI.Page>.</span></span> <span data-ttu-id="0e2d9-104">Questo oggetto consente di inviare dati di risposta HTTP a un client e contiene informazioni su tale risposta.</span><span class="sxs-lookup"><span data-stu-id="0e2d9-104">This object allows you to send HTTP response data to a client and contains information about that response.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="0e2d9-105">Commenti</span><span class="sxs-lookup"><span data-stu-id="0e2d9-105">Remarks</span></span>  
 <span data-ttu-id="0e2d9-106">L' `My.Response` oggetto contiene l' <xref:System.Web.HttpResponse> oggetto corrente associato alla pagina.</span><span class="sxs-lookup"><span data-stu-id="0e2d9-106">The `My.Response` object contains the current <xref:System.Web.HttpResponse> object associated with the page.</span></span>  
  
 <span data-ttu-id="0e2d9-107">L' `My.Response` oggetto è disponibile solo per le applicazioni ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0e2d9-107">The `My.Response` object is only available for ASP.NET applications.</span></span>  
  
## <a name="example"></a><span data-ttu-id="0e2d9-108">Esempio</span><span class="sxs-lookup"><span data-stu-id="0e2d9-108">Example</span></span>  
 <span data-ttu-id="0e2d9-109">Nell'esempio seguente viene ottenuta la raccolta di intestazioni dall' `My.Request` oggetto e viene utilizzato l' `My.Response` oggetto per scriverlo nella pagina ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0e2d9-109">The following example gets the header collection from the `My.Request` object and uses the `My.Response` object to write it to the ASP.NET page.</span></span>  
  
 [!code-aspx-vb[VbVbalrMyWeb#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyWeb/VB/Default.aspx#1)]  
  
## <a name="see-also"></a><span data-ttu-id="0e2d9-110">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0e2d9-110">See also</span></span>

- <xref:System.Web.HttpResponse>
- [<span data-ttu-id="0e2d9-111">Oggetto My.Request</span><span class="sxs-lookup"><span data-stu-id="0e2d9-111">My.Request Object</span></span>](my-request-object.md)
