---
title: -nowin32manifest
ms.date: 03/13/2018
helpviewer_keywords:
- /nowin32manifest compiler option [Visual Basic]
- nowin32manifest compiler option [Visual Basic]
- -nowin32manifest compiler option [Visual Basic]
ms.assetid: c0528aae-83b3-4425-99f0-19448e9843e3
ms.openlocfilehash: d9323cd541eaf611551de90e58a181f6915fad89
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397454"
---
# <a name="-nowin32manifest-visual-basic"></a><span data-ttu-id="7a159-102">-nowin32manifest (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="7a159-102">-nowin32manifest (Visual Basic)</span></span>
<span data-ttu-id="7a159-103">Indica al compilatore di non incorporare un manifesto dell'applicazione nel file eseguibile.</span><span class="sxs-lookup"><span data-stu-id="7a159-103">Instructs the compiler not to embed any application manifest into the executable file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7a159-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="7a159-104">Syntax</span></span>  
  
```console  
-nowin32manifest  
```  
  
## <a name="remarks"></a><span data-ttu-id="7a159-105">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="7a159-105">Remarks</span></span>  
 <span data-ttu-id="7a159-106">Quando viene usata questa opzione, l'applicazione è soggetta a virtualizzazione in Windows Vista a meno che non venga specificato un manifesto dell'applicazione in un file di risorsa Win32 file o durante una istruzione di compilazione successiva.</span><span class="sxs-lookup"><span data-stu-id="7a159-106">When this option is used, the application will be subject to virtualization on Windows Vista unless you provide an application manifest in a Win32 Resource file or during a later build step.</span></span> <span data-ttu-id="7a159-107">Per altre informazioni sulla virtualizzazione, vedere [Distribuzione ClickOnce in Windows Vista](/visualstudio/deployment/clickonce-deployment-on-windows-vista).</span><span class="sxs-lookup"><span data-stu-id="7a159-107">For more information about virtualization, see [ClickOnce Deployment on Windows Vista](/visualstudio/deployment/clickonce-deployment-on-windows-vista).</span></span>  
  
 <span data-ttu-id="7a159-108">Per altre informazioni sulla creazione di manifesti, vedere [-win32manifest (Visual Basic)](win32manifest.md).</span><span class="sxs-lookup"><span data-stu-id="7a159-108">For more information about manifest creation, see [-win32manifest (Visual Basic)](win32manifest.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7a159-109">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7a159-109">See also</span></span>

- [<span data-ttu-id="7a159-110">Compilatore della riga di comando di Visual Basic</span><span class="sxs-lookup"><span data-stu-id="7a159-110">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="7a159-111">Application Page, Project Designer (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="7a159-111">Application Page, Project Designer (Visual Basic)</span></span>](/visualstudio/ide/reference/application-page-project-designer-visual-basic)
