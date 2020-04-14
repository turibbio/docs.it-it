---
title: Esposizione di componenti .NET Core a COM
description: In questa esercitazione viene illustrato come esporre una classe a COM da .NET Core.This tutorial shows you how to expose a class to COM from .NET Core. Generare un server COM e un manifesto del server side-by-side per COM senza Registro di sistema.
ms.date: 07/12/2019
helpviewer_keywords:
- exposing .NET Core components to COM
- interoperation with unmanaged code, exposing .NET Core components
- COM interop, exposing COM components
ms.assetid: 21271167-fe7f-46ba-a81f-a6812ea649d4
author: jkoritzinsky
ms.author: jekoritz
ms.openlocfilehash: 17d85b9e9734fae0bb69f94da8c08669216ab0ae
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/13/2020
ms.locfileid: "81242868"
---
# <a name="exposing-net-core-components-to-com"></a><span data-ttu-id="17975-104">Esposizione di componenti .NET Core a COM</span><span class="sxs-lookup"><span data-stu-id="17975-104">Exposing .NET Core components to COM</span></span>

<span data-ttu-id="17975-105">In .NET Core, il processo di esposizione degli oggetti .NET a COM è stato significativamente semplificato rispetto a .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="17975-105">In .NET Core, the process for exposing your .NET objects to COM has been significantly streamlined in comparison to .NET Framework.</span></span> <span data-ttu-id="17975-106">Nel processo seguente viene illustrato come esporre una classe a COM.</span><span class="sxs-lookup"><span data-stu-id="17975-106">The following process will walk you through how to expose a class to COM.</span></span> <span data-ttu-id="17975-107">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="17975-107">This tutorial shows you how to:</span></span>

- <span data-ttu-id="17975-108">Esporre una classe a COM da .NET Core.</span><span class="sxs-lookup"><span data-stu-id="17975-108">Expose a class to COM from .NET Core.</span></span>
- <span data-ttu-id="17975-109">Generare un server COM nell'ambito della creazione della libreria .NET Core.</span><span class="sxs-lookup"><span data-stu-id="17975-109">Generate a COM server as part of building your .NET Core library.</span></span>
- <span data-ttu-id="17975-110">Generare automaticamente un manifesto del server affiancato per COM senza Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="17975-110">Automatically generate a side-by-side server manifest for Registry-Free COM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17975-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="17975-111">Prerequisites</span></span>

- <span data-ttu-id="17975-112">Installare [.NET Core 3.0 SDK](https://dotnet.microsoft.com/download) o una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="17975-112">Install [.NET Core 3.0 SDK](https://dotnet.microsoft.com/download) or a newer version.</span></span>

## <a name="create-the-library"></a><span data-ttu-id="17975-113">Creare la libreria</span><span class="sxs-lookup"><span data-stu-id="17975-113">Create the library</span></span>

<span data-ttu-id="17975-114">Il primo passaggio consiste nel creare la libreria.</span><span class="sxs-lookup"><span data-stu-id="17975-114">The first step is to create the library.</span></span>

1. <span data-ttu-id="17975-115">Creare una nuova cartella e in tale cartella eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="17975-115">Create a new folder, and in that folder run the following command:</span></span>

    ```dotnetcli
    dotnet new classlib
    ```

2. <span data-ttu-id="17975-116">Aprire `Class1.cs`.</span><span class="sxs-lookup"><span data-stu-id="17975-116">Open `Class1.cs`.</span></span>
3. <span data-ttu-id="17975-117">Aggiungere `using System.Runtime.InteropServices;` all'inizio del file.</span><span class="sxs-lookup"><span data-stu-id="17975-117">Add `using System.Runtime.InteropServices;` to the top of the file.</span></span>
4. <span data-ttu-id="17975-118">Creare un'interfaccia denominata `IServer`.</span><span class="sxs-lookup"><span data-stu-id="17975-118">Create an interface named `IServer`.</span></span> <span data-ttu-id="17975-119">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="17975-119">For example:</span></span>

   ```csharp
   using System;
   using System.Runtime.InteropServices;

   [ComVisible(true)]
   [Guid(ContractGuids.ServerInterface)]
   [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
   public interface IServer
   {
       /// <summary>
       /// Compute the value of the constant Pi.
       /// </summary>
       double ComputePi();
   }
   ```

5. <span data-ttu-id="17975-120">Aggiungere l'attributo `[Guid("<IID>")]` all'interfaccia con il GUID di interfaccia per l'interfaccia COM che si sta implementando.</span><span class="sxs-lookup"><span data-stu-id="17975-120">Add the `[Guid("<IID>")]` attribute to the interface, with the interface GUID for the COM interface you're implementing.</span></span> <span data-ttu-id="17975-121">Ad esempio: `[Guid("fe103d6e-e71b-414c-80bf-982f18f6c1c7")]`.</span><span class="sxs-lookup"><span data-stu-id="17975-121">For example, `[Guid("fe103d6e-e71b-414c-80bf-982f18f6c1c7")]`.</span></span> <span data-ttu-id="17975-122">Si noti che questo GUID deve essere univoco perché è l'unico identificatore di questa interfaccia per COM.</span><span class="sxs-lookup"><span data-stu-id="17975-122">Note that this GUID needs to be unique since it is the only identifier of this interface for COM.</span></span> <span data-ttu-id="17975-123">In Visual Studio è possibile generare un GUID passando a Strumenti > Crea GUID per aprire lo strumento Crea GUID.</span><span class="sxs-lookup"><span data-stu-id="17975-123">In Visual Studio, you can generate a GUID by going to Tools > Create GUID to open the Create GUID tool.</span></span>
6. <span data-ttu-id="17975-124">Aggiungere l'attributo `[InterfaceType]` all'interfaccia e specificare le interfacce COM di base che l'interfaccia deve implementare.</span><span class="sxs-lookup"><span data-stu-id="17975-124">Add the `[InterfaceType]` attribute to the interface and specify what base COM interfaces your interface should implement.</span></span>
7. <span data-ttu-id="17975-125">Creare una classe denominata `Server` che implementi `IServer`.</span><span class="sxs-lookup"><span data-stu-id="17975-125">Create a class named `Server` that implements `IServer`.</span></span>
8. <span data-ttu-id="17975-126">Aggiungere l'attributo `[Guid("<CLSID>")]` alla classe con il GUID dell'identificatore di classe per la classe COM che si sta implementando.</span><span class="sxs-lookup"><span data-stu-id="17975-126">Add the `[Guid("<CLSID>")]` attribute to the class, with the class identifier GUID for the COM class you're implementing.</span></span> <span data-ttu-id="17975-127">Ad esempio: `[Guid("9f35b6f5-2c05-4e7f-93aa-ee087f6e7ab6")]`.</span><span class="sxs-lookup"><span data-stu-id="17975-127">For example, `[Guid("9f35b6f5-2c05-4e7f-93aa-ee087f6e7ab6")]`.</span></span> <span data-ttu-id="17975-128">Come per il GUID dell'interfaccia, questo GUID deve essere univoco perché è l'unico identificatore di questa interfaccia per COM.</span><span class="sxs-lookup"><span data-stu-id="17975-128">As with the interface GUID, this GUID must be unique since it is the only identifier of this interface to COM.</span></span>
9. <span data-ttu-id="17975-129">Aggiungere l'attributo `[ComVisible(true)]` sia all'interfaccia che alla classe.</span><span class="sxs-lookup"><span data-stu-id="17975-129">Add the `[ComVisible(true)]` attribute to both the interface and the class.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17975-130">Diversamente da quanto avviene in .NET Framework, .NET Core richiede di specificare il CLSID di qualsiasi classe che si vuole rendere attivabile tramite COM.</span><span class="sxs-lookup"><span data-stu-id="17975-130">Unlike in .NET Framework, .NET Core requires you to specify the CLSID of any class you want to be activatable via COM.</span></span>

## <a name="generate-the-com-host"></a><span data-ttu-id="17975-131">Generare l'host COM</span><span class="sxs-lookup"><span data-stu-id="17975-131">Generate the COM host</span></span>

1. <span data-ttu-id="17975-132">Aprire il file di progetto `.csproj` e aggiungere `<EnableComHosting>true</EnableComHosting>` all'interno di un tag `<PropertyGroup></PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="17975-132">Open the `.csproj` project file and add `<EnableComHosting>true</EnableComHosting>` inside a `<PropertyGroup></PropertyGroup>` tag.</span></span>
2. <span data-ttu-id="17975-133">Compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="17975-133">Build the project.</span></span>

<span data-ttu-id="17975-134">L'output risultante includerà un file `ProjectName.dll`, `ProjectName.deps.json`, `ProjectName.runtimeconfig.json` e `ProjectName.comhost.dll`.</span><span class="sxs-lookup"><span data-stu-id="17975-134">The resulting output will have a `ProjectName.dll`, `ProjectName.deps.json`, `ProjectName.runtimeconfig.json` and `ProjectName.comhost.dll` file.</span></span>

## <a name="register-the-com-host-for-com"></a><span data-ttu-id="17975-135">Registrare l'host COM per COM</span><span class="sxs-lookup"><span data-stu-id="17975-135">Register the COM host for COM</span></span>

<span data-ttu-id="17975-136">Aprire un prompt dei comandi con privilegi elevati ed eseguire `regsvr32 ProjectName.comhost.dll`.</span><span class="sxs-lookup"><span data-stu-id="17975-136">Open an elevated command prompt and run `regsvr32 ProjectName.comhost.dll`.</span></span> <span data-ttu-id="17975-137">Tutti gli oggetti .NET esposti verranno così registrati in COM.</span><span class="sxs-lookup"><span data-stu-id="17975-137">That will register all of your exposed .NET objects with COM.</span></span>

## <a name="enabling-regfree-com"></a><span data-ttu-id="17975-138">Abilitazione di COM RegFree</span><span class="sxs-lookup"><span data-stu-id="17975-138">Enabling RegFree COM</span></span>

1. <span data-ttu-id="17975-139">Aprire il file di progetto `.csproj` e aggiungere `<EnableRegFreeCom>true</EnableRegFreeCom>` all'interno di un tag `<PropertyGroup></PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="17975-139">Open the `.csproj` project file and add `<EnableRegFreeCom>true</EnableRegFreeCom>` inside a `<PropertyGroup></PropertyGroup>` tag.</span></span>
2. <span data-ttu-id="17975-140">Compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="17975-140">Build the project.</span></span>

<span data-ttu-id="17975-141">L'output risultante includerà ora anche un file `ProjectName.X.manifest`.</span><span class="sxs-lookup"><span data-stu-id="17975-141">The resulting output will now also have a `ProjectName.X.manifest` file.</span></span> <span data-ttu-id="17975-142">Questo file è il manifesto affiancato da usare con COM senza Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="17975-142">This file is the side-by-side manifest for use with Registry-Free COM.</span></span>

## <a name="sample"></a><span data-ttu-id="17975-143">Esempio</span><span class="sxs-lookup"><span data-stu-id="17975-143">Sample</span></span>

<span data-ttu-id="17975-144">È disponibile un [esempio di server COM](https://github.com/dotnet/samples/tree/master/core/extensions/COMServerDemo) funzionante nel repository dotnet/samples in GitHub.</span><span class="sxs-lookup"><span data-stu-id="17975-144">There is a fully functional [COM server sample](https://github.com/dotnet/samples/tree/master/core/extensions/COMServerDemo) in the dotnet/samples repository on GitHub.</span></span>

## <a name="additional-notes"></a><span data-ttu-id="17975-145">Note aggiuntive</span><span class="sxs-lookup"><span data-stu-id="17975-145">Additional notes</span></span>

<span data-ttu-id="17975-146">Diversamente da .NET Framework, in .NET Core non è disponibile alcun supporto per la generazione di una libreria dei tipi COM (TLB) da un assembly .NET Core.</span><span class="sxs-lookup"><span data-stu-id="17975-146">Unlike in .NET Framework, there is no support in .NET Core for generating a COM Type Library (TLB) from a .NET Core assembly.</span></span> <span data-ttu-id="17975-147">La guida consiste nel scrivere manualmente un file IDL o un'intestazione C/C, per le dichiarazioni native delle interfacce COM.</span><span class="sxs-lookup"><span data-stu-id="17975-147">The guidance is to either manually write an IDL file or a C/C++ header for the native declarations of the COM interfaces.</span></span>

<span data-ttu-id="17975-148">[Le distribuzioni autonome](../deploying/index.md#publish-self-contained) dei componenti COM non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="17975-148">[Self-contained deployments](../deploying/index.md#publish-self-contained) of COM components are not supported.</span></span> <span data-ttu-id="17975-149">Sono supportate solo [le distribuzioni dipendenti dal runtime](../deploying/index.md#publish-runtime-dependent) dei componenti COM.</span><span class="sxs-lookup"><span data-stu-id="17975-149">Only [runtime-dependent deployments](../deploying/index.md#publish-runtime-dependent) of COM components are supported.</span></span>

<span data-ttu-id="17975-150">Inoltre, il caricamento di .NET Framework e .NET Core nello stesso processo ha limitazioni diagnostiche.</span><span class="sxs-lookup"><span data-stu-id="17975-150">Additionally, loading both .NET Framework and .NET Core into the same process does have diagnostic limitations.</span></span> <span data-ttu-id="17975-151">La limitazione principale è il debug dei componenti gestiti in quanto non è possibile eseguire il debug contemporaneamente di .NET Framework e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="17975-151">The primary limitation is the debugging of managed components as it is not possible to debug both .NET Framework and .NET Core at the same time.</span></span> <span data-ttu-id="17975-152">Inoltre, le due istanze di runtime non condividono assembly gestiti.</span><span class="sxs-lookup"><span data-stu-id="17975-152">In addition, the two runtime instances don't share managed assemblies.</span></span> <span data-ttu-id="17975-153">Ciò significa che non è possibile condividere i tipi .NET effettivi tra i due runtime e invece tutte le interazioni devono essere limitate ai contratti di interfaccia COM esposti.</span><span class="sxs-lookup"><span data-stu-id="17975-153">This means that it isn't possible to share actual .NET types across the two runtimes and instead all interactions must be restricted to the exposed COM interface contracts.</span></span>
