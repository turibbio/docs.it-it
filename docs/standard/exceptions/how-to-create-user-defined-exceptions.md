---
title: "Procedura: creare eccezioni definite dall'utente"
description: Informazioni su come creare eccezioni definite dall'utente, che rappresentano un'alternativa alla gerarchia di classi di eccezioni derivate dalla classe di base Exception in .NET.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- user-defined exceptions
- exceptions, examples
- exceptions, user-defined
ms.assetid: 25819a5a-f915-4fc8-b924-a76915674e04
ms.openlocfilehash: 14eb6246ba4347f33766f7dff36463f2bf996330
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2020
ms.locfileid: "84662797"
---
# <a name="how-to-create-user-defined-exceptions"></a><span data-ttu-id="651bc-103">Come creare eccezioni definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="651bc-103">How to create user-defined exceptions</span></span>

<span data-ttu-id="651bc-104">.NET offre una gerarchia di classi di eccezioni derivate dalla classe di base <xref:System.Exception>.</span><span class="sxs-lookup"><span data-stu-id="651bc-104">.NET provides a hierarchy of exception classes ultimately derived from the base class <xref:System.Exception>.</span></span> <span data-ttu-id="651bc-105">Tuttavia, se nessuna delle eccezioni predefinite soddisfa le proprie esigenze, è possibile creare classi di eccezioni personalizzate mediante la derivazione dalla classe <xref:System.Exception>.</span><span class="sxs-lookup"><span data-stu-id="651bc-105">However, if none of the predefined exceptions meets your needs, you can create your own exception classes by deriving from the <xref:System.Exception> class.</span></span>

<span data-ttu-id="651bc-106">Quando si creano eccezioni personalizzate, terminare il nome della classe dell'eccezione definita dall'utente con la parola "Exception" e implementare i tre costruttori comuni, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="651bc-106">When creating your own exceptions, end the class name of the user-defined exception with the word "Exception", and implement the three common constructors, as shown in the following example.</span></span> <span data-ttu-id="651bc-107">L'esempio definisce una nuova classe di eccezione denominata `EmployeeListNotFoundException`.</span><span class="sxs-lookup"><span data-stu-id="651bc-107">The example defines a new exception class named `EmployeeListNotFoundException`.</span></span> <span data-ttu-id="651bc-108">La classe è derivata da <xref:System.Exception> e include tre costruttori.</span><span class="sxs-lookup"><span data-stu-id="651bc-108">The class is derived from <xref:System.Exception> and includes three constructors.</span></span>

[!code-cpp[dg_exceptionDesign#14](../../../samples/snippets/cpp/VS_Snippets_CLR/dg_exceptionDesign/cpp/example2.cpp#14)]
[!code-csharp[dg_exceptionDesign#14](../../../samples/snippets/csharp/VS_Snippets_CLR/dg_exceptionDesign/cs/example2.cs#14)]
[!code-vb[dg_exceptionDesign#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/dg_exceptionDesign/vb/example2.vb#14)]  

> [!NOTE]
> <span data-ttu-id="651bc-109">Nei casi in cui viene usata la comunicazione remota, è necessario assicurarsi che i metadati di tutte le eccezioni definite dall'utente siano disponibili nel server chiamato e nel client (oggetto proxy o chiamante).</span><span class="sxs-lookup"><span data-stu-id="651bc-109">In situations where you are using remoting, you must ensure that the metadata for any user-defined exceptions is available at the server (callee) and to the client (the proxy object or caller).</span></span> <span data-ttu-id="651bc-110">Per ulteriori informazioni, vedere [procedure consigliate per le eccezioni](best-practices-for-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="651bc-110">For more information, see [Best practices for exceptions](best-practices-for-exceptions.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="651bc-111">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="651bc-111">See also</span></span>

- [<span data-ttu-id="651bc-112">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="651bc-112">Exceptions</span></span>](index.md)
