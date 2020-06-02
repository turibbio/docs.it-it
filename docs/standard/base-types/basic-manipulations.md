---
title: Modifiche di base delle stringhe in .NET
description: Esempio in cui vengono chiamati molti metodi per stringhe.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [.NET Framework], examples
ms.assetid: 121d1eae-251b-44c0-8818-57da04b8215e
ms.openlocfilehash: 54de6451029fb268beb7ebe4ded0d7b437c3df3c
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289863"
---
# <a name="how-to-perform-basic-string-manipulations-in-net"></a><span data-ttu-id="cff76-103">Procedura: Eseguire modifiche di base delle stringhe in .NET</span><span class="sxs-lookup"><span data-stu-id="cff76-103">How to: Perform Basic String Manipulations in .NET</span></span>

<span data-ttu-id="cff76-104">Nell'esempio seguente vengono usati alcuni dei metodi descritti nell'argomento [Operazioni di base su stringhe](basic-string-operations.md) per costruire una classe con la quale modificare le stringhe, come può avvenire in un'applicazione reale.</span><span class="sxs-lookup"><span data-stu-id="cff76-104">The following example uses some of the methods discussed in the [Basic String Operations](basic-string-operations.md) topics to construct a class that performs string manipulations in a manner that might be found in a real-world application.</span></span> <span data-ttu-id="cff76-105">Nella classe `MailToData` vengono archiviati il nome e l'indirizzo di un utente in proprietà separate e viene usato un modo per combinare i campi `City`, `State` e `Zip` in una singola stringa da visualizzare all'utente.</span><span class="sxs-lookup"><span data-stu-id="cff76-105">The `MailToData` class stores the name and address of an individual in separate properties and provides a way to combine the `City`, `State`, and `Zip` fields into a single string for display to the user.</span></span> <span data-ttu-id="cff76-106">Questa classe consente anche all'utente di immettere la città, lo stato e il codice postale ZIP (Stati Uniti) sotto forma di singola stringa. L'applicazione automaticamente analizza la singola stringa e immette le informazioni corrette nella proprietà corrispondente.</span><span class="sxs-lookup"><span data-stu-id="cff76-106">Furthermore, the class allows the user to enter the city, state, and ZIP Code information as a single string; the application automatically parses the single string and enters the proper information into the corresponding property.</span></span>  
  
<span data-ttu-id="cff76-107">Per semplicità, in questo esempio viene usata un'applicazione console con un'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="cff76-107">For simplicity, this example uses a console application with a command-line interface.</span></span>  
  
## <a name="example"></a><span data-ttu-id="cff76-108">Esempio</span><span class="sxs-lookup"><span data-stu-id="cff76-108">Example</span></span>  

[!code-csharp[Conceptual.String.BasicOps#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/basicops.cs#1)]
[!code-vb[Conceptual.String.BasicOps#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/basicops.vb#1)]  
  
<span data-ttu-id="cff76-109">Quando viene eseguito il codice precedente, all'utente viene richiesto di immettere il nome e l'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="cff76-109">When the preceding code is executed, the user is asked to enter their name and address.</span></span> <span data-ttu-id="cff76-110">L'applicazione inserisce le informazioni nelle proprietà corrette e visualizza le informazioni all'utente, creando una singola stringa che contiene la città, lo stato e il codice postale ZIP (Stati Uniti).</span><span class="sxs-lookup"><span data-stu-id="cff76-110">The application places the information in the appropriate properties and displays the information back to the user, creating a single string that displays the city, state, and ZIP Code information.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="cff76-111">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cff76-111">See also</span></span>

- [<span data-ttu-id="cff76-112">Operazioni di base sulle stringhe</span><span class="sxs-lookup"><span data-stu-id="cff76-112">Basic String Operations</span></span>](basic-string-operations.md)
