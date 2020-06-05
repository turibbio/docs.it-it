---
title: Sviluppo con My
ms.date: 07/20/2015
f1_keywords:
- My.MyWpfExtension.Windows
helpviewer_keywords:
- My object
- My namespace
- My feature
- Visual Basic, programming in
ms.assetid: f1d04509-5e46-4551-9f9f-94334a121fca
ms.openlocfilehash: 3befac591de8fbc7250777a8b87247ee395abf25
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411705"
---
# <a name="development-with-my-visual-basic"></a><span data-ttu-id="ec6e6-102">Sviluppo con My (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="ec6e6-102">Development with My (Visual Basic)</span></span>

<span data-ttu-id="ec6e6-103">Visual Basic fornisce nuove funzionalità per lo sviluppo rapido di applicazioni che migliorano la produttività e aumentano la facilità d'uso, garantendo al tempo stesso maggiore potenza.</span><span class="sxs-lookup"><span data-stu-id="ec6e6-103">Visual Basic provides new features for rapid application development that improve productivity and ease of use while delivering power.</span></span> <span data-ttu-id="ec6e6-104">Una di queste funzionalità, denominata `My`, consente di accedere a informazioni e istanze di oggetti predefinite correlate all'applicazione e al relativo ambiente di run-time.</span><span class="sxs-lookup"><span data-stu-id="ec6e6-104">One of these features, called `My`, provides access to information and default object instances that are related to the application and its run-time environment.</span></span> <span data-ttu-id="ec6e6-105">Queste informazioni sono organizzate in un formato riconoscibile tramite IntelliSense e delineato in modo logico in base all'uso.</span><span class="sxs-lookup"><span data-stu-id="ec6e6-105">This information is organized in a format that is discoverable through IntelliSense and logically delineated according to use.</span></span>  
  
 <span data-ttu-id="ec6e6-106">I membri di `My` di primo livello sono esposti come oggetti.</span><span class="sxs-lookup"><span data-stu-id="ec6e6-106">Top-level members of `My` are exposed as objects.</span></span> <span data-ttu-id="ec6e6-107">Ogni oggetto si comporta in modo analogo a uno spazio dei nomi o a una classe con membri `Shared` ed espone un set di membri correlati.</span><span class="sxs-lookup"><span data-stu-id="ec6e6-107">Each object behaves similarly to a namespace or a class with `Shared` members, and it exposes a set of related members.</span></span>  
  
 <span data-ttu-id="ec6e6-108">Questa tabella mostra gli oggetti `My` di primo livello e le relazioni tra tali oggetti.</span><span class="sxs-lookup"><span data-stu-id="ec6e6-108">This table shows the top-level `My` objects and their relationship to each other.</span></span>  
  
 ![Il diagramma mostra il modello a oggetti per My.](./media/index/my-object-model-relationships.gif)  
  
## <a name="in-this-section"></a><span data-ttu-id="ec6e6-110">Contenuto della sezione</span><span class="sxs-lookup"><span data-stu-id="ec6e6-110">In This Section</span></span>  

 [<span data-ttu-id="ec6e6-111">Esecuzione di attività mediante My.Application, My.Computer e My.User</span><span class="sxs-lookup"><span data-stu-id="ec6e6-111">Performing Tasks with My.Application, My.Computer, and My.User</span></span>](performing-tasks-with-my-application-my-computer-and-my-user.md)  
 <span data-ttu-id="ec6e6-112">Vengono descritti i tre principali oggetti `My`, `My.Application`, `My.Computer` e `My.User`, che consentono di accedere a informazioni e funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ec6e6-112">Describes the three central `My` objects, `My.Application`, `My.Computer`, and `My.User`, which provide access to information and functionality</span></span>  
  
 [<span data-ttu-id="ec6e6-113">Istanze predefinite degli oggetti fornite da My.Forms e My.WebServices</span><span class="sxs-lookup"><span data-stu-id="ec6e6-113">Default Object Instances Provided by My.Forms and My.WebServices</span></span>](default-object-instances-provided-by-my-forms-and-my-webservices.md)  
 <span data-ttu-id="ec6e6-114">Vengono descritti gli oggetti `My.Forms` e `My.WebServices`, che consentono di accedere a form, origini dati e servizi Web XML usati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ec6e6-114">Describes the `My.Forms` and `My.WebServices` objects, which provide access to forms, data sources, and XML Web services used by your application.</span></span>  
  
 [<span data-ttu-id="ec6e6-115">Sviluppo rapido di applicazioni con My.Resources e My.Settings</span><span class="sxs-lookup"><span data-stu-id="ec6e6-115">Rapid Application Development with My.Resources and My.Settings</span></span>](rapid-application-development-with-my-resources-and-my-settings.md)  
 <span data-ttu-id="ec6e6-116">Vengono descritti gli oggetti `My.Resources` e `My.Settings`, che consentono di accedere alle risorse e alle impostazioni di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ec6e6-116">Describes the `My.Resources` and `My.Settings` objects, which provide access to an application's resources and settings.</span></span>  
  
 [<span data-ttu-id="ec6e6-117">Cenni preliminari sul modello di applicazione Visual Basic</span><span class="sxs-lookup"><span data-stu-id="ec6e6-117">Overview of the Visual Basic Application Model</span></span>](overview-of-the-visual-basic-application-model.md)  
 <span data-ttu-id="ec6e6-118">Viene descritto il modello di avvio/arresto dell'applicazione Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="ec6e6-118">Describes the Visual Basic Application Startup/Shutdown model.</span></span>  
  
 [<span data-ttu-id="ec6e6-119">Dipendenza di My dal tipo di progetto</span><span class="sxs-lookup"><span data-stu-id="ec6e6-119">How My Depends on Project Type</span></span>](how-my-depends-on-project-type.md)  
 <span data-ttu-id="ec6e6-120">Vengono forniti dettagli sulle caratteristiche di `My` disponibili per i diversi tipi di progetto.</span><span class="sxs-lookup"><span data-stu-id="ec6e6-120">Gives details on which `My` features are available in different project types.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ec6e6-121">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ec6e6-121">See also</span></span>

- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>
- <xref:Microsoft.VisualBasic.Devices.Computer>
- <xref:Microsoft.VisualBasic.ApplicationServices.User>
- [<span data-ttu-id="ec6e6-122">Oggetto My.Forms</span><span class="sxs-lookup"><span data-stu-id="ec6e6-122">My.Forms Object</span></span>](../../language-reference/objects/my-forms-object.md)
- [<span data-ttu-id="ec6e6-123">Oggetto My.WebServices</span><span class="sxs-lookup"><span data-stu-id="ec6e6-123">My.WebServices Object</span></span>](../../language-reference/objects/my-webservices-object.md)
- [<span data-ttu-id="ec6e6-124">Dipendenza di My dal tipo di progetto</span><span class="sxs-lookup"><span data-stu-id="ec6e6-124">How My Depends on Project Type</span></span>](how-my-depends-on-project-type.md)
