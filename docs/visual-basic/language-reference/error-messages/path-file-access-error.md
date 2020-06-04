---
title: Errore di accesso al percorso/file
ms.date: 07/20/2015
f1_keywords:
- vbrID75
ms.assetid: 6ce3a161-7316-46bd-a785-0d50e5414020
ms.openlocfilehash: dfe96cd6eaa673438849fe8f799d46fa2617bfdd
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84387257"
---
# <a name="pathfile-access-error"></a><span data-ttu-id="3dce0-102">Errore di accesso al percorso/file</span><span class="sxs-lookup"><span data-stu-id="3dce0-102">Path/File access error</span></span>
<span data-ttu-id="3dce0-103">Durante un'operazione di accesso ai file o di accesso al disco, il sistema operativo non è in grado di effettuare una connessione tra il percorso e il nome del file.</span><span class="sxs-lookup"><span data-stu-id="3dce0-103">During a file-access or disk-access operation, the operating system could not make a connection between the path and the file name.</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="3dce0-104">Per correggere l'errore</span><span class="sxs-lookup"><span data-stu-id="3dce0-104">To correct this error</span></span>  
  
1. <span data-ttu-id="3dce0-105">Verificare che la specifica del file sia formattata correttamente.</span><span class="sxs-lookup"><span data-stu-id="3dce0-105">Make sure the file specification is correctly formatted.</span></span> <span data-ttu-id="3dce0-106">Un nome file può contenere un percorso completo (assoluto) o relativo.</span><span class="sxs-lookup"><span data-stu-id="3dce0-106">A file name can contain a fully qualified (absolute) or relative path.</span></span> <span data-ttu-id="3dce0-107">Un percorso completo inizia con il nome dell'unità (se il percorso si trova in un'altra unità) ed elenca il percorso esplicito dalla radice al file.</span><span class="sxs-lookup"><span data-stu-id="3dce0-107">A fully qualified path starts with the drive name (if the path is on another drive) and lists the explicit path from the root to the file.</span></span> <span data-ttu-id="3dce0-108">Qualsiasi percorso non completo è relativo all'unità e alla directory correnti.</span><span class="sxs-lookup"><span data-stu-id="3dce0-108">Any path that is not fully qualified is relative to the current drive and directory.</span></span>  
  
2. <span data-ttu-id="3dce0-109">Assicurarsi di non aver tentato di salvare un file che sostituirebbe un file di sola lettura esistente.</span><span class="sxs-lookup"><span data-stu-id="3dce0-109">Make sure that you did not attempt to save a file that would replace an existing read-only file.</span></span> <span data-ttu-id="3dce0-110">In tal caso, modificare l'attributo di sola lettura del file di destinazione oppure salvare il file con un nome di file diverso.</span><span class="sxs-lookup"><span data-stu-id="3dce0-110">If this is the case, change the read-only attribute of the target file, or save the file with a different file name.</span></span>  
  
3. <span data-ttu-id="3dce0-111">Assicurarsi che non si sia tentato di aprire un file di sola lettura in modalità sequenziale `Output` o `Append` .</span><span class="sxs-lookup"><span data-stu-id="3dce0-111">Make sure you did not attempt to open a read-only file in sequential `Output` or `Append` mode.</span></span> <span data-ttu-id="3dce0-112">In tal caso, aprire il file in `Input` modalità o modificare l'attributo di sola lettura del file.</span><span class="sxs-lookup"><span data-stu-id="3dce0-112">If this is the case, open the file in `Input` mode or change the read-only attribute of the file.</span></span>  
  
4. <span data-ttu-id="3dce0-113">Assicurarsi che non sia stato effettuato un tentativo di modifica di un progetto di Visual Basic all'interno di un database o di un documento.</span><span class="sxs-lookup"><span data-stu-id="3dce0-113">Make sure you did not attempt to change a Visual Basic project within a database or document.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3dce0-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3dce0-114">See also</span></span>

- [<span data-ttu-id="3dce0-115">Tipi di errore</span><span class="sxs-lookup"><span data-stu-id="3dce0-115">Error Types</span></span>](../../programming-guide/language-features/error-types.md)
