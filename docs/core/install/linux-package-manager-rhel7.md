---
title: Installare .NET Core in Linux RHEL 7 gestore di pacchetti - .NET CoreInstall .NET Core on Linux RHEL 7 package manager - .NET Core
description: Usare un gestore di pacchetti per installare .NET Core SDK e runtime in RHEL 7.Use a package manager to install .NET Core SDK and runtime on RHEL 7.
author: thraka
ms.author: adegeo
ms.date: 03/17/2020
ms.openlocfilehash: d1f1372b32c7b2471a96492d48aab5533dadb64a
ms.sourcegitcommit: 07123a475af89b6da5bb6cc51ea40ab1e8a488f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/24/2020
ms.locfileid: "80134209"
---
# <a name="rhel-7-package-manager---install-net-core"></a><span data-ttu-id="622dd-103">RHEL 7 Gestione pacchetti - Installare .NET Core</span><span class="sxs-lookup"><span data-stu-id="622dd-103">RHEL 7 Package Manager - Install .NET Core</span></span>

[!INCLUDE [package-manager-switcher](includes/package-manager-switcher.md)]

<span data-ttu-id="622dd-104">In questo articolo viene descritto come utilizzare un gestore di pacchetti per installare .NET Core in RHEL 7.This article describes how to use a package manager to install .NET Core on RHEL 7.</span><span class="sxs-lookup"><span data-stu-id="622dd-104">This article describes how to use a package manager to install .NET Core on RHEL 7.</span></span>

[!INCLUDE [package-manager-intro-sdk-vs-runtime](includes/package-manager-intro-sdk-vs-runtime.md)]

## <a name="register-your-red-hat-subscription"></a><span data-ttu-id="622dd-105">Registra il tuo abbonamento Red Hat</span><span class="sxs-lookup"><span data-stu-id="622dd-105">Register your Red Hat subscription</span></span>

<span data-ttu-id="622dd-106">Per installare .NET Core da Red Hat in RHEL, è innanzitutto necessario eseguire la registrazione utilizzando Red Hat Subscription Manager.</span><span class="sxs-lookup"><span data-stu-id="622dd-106">To install .NET Core from Red Hat on RHEL, you first need to register using the Red Hat Subscription Manager.</span></span> <span data-ttu-id="622dd-107">Se questa operazione non è stata eseguita nel sistema o se non si è sicuri, vedere la [documentazione del prodotto Red Hat per .NET Core](https://access.redhat.com/documentation/net_core/).</span><span class="sxs-lookup"><span data-stu-id="622dd-107">If this hasn't been done on your system, or if you're unsure, see the [Red Hat Product Documentation for .NET Core](https://access.redhat.com/documentation/net_core/).</span></span>

## <a name="install-the-net-core-sdk"></a><span data-ttu-id="622dd-108">Installare .NET Core SDK.</span><span class="sxs-lookup"><span data-stu-id="622dd-108">Install the .NET Core SDK</span></span>

<span data-ttu-id="622dd-109">Dopo la registrazione con Gestione sottoscrizioni, è possibile installare e abilitare .NET Core SDK.</span><span class="sxs-lookup"><span data-stu-id="622dd-109">After registering with the Subscription Manager, you're ready to install and enable the .NET Core SDK.</span></span> <span data-ttu-id="622dd-110">Nel terminale, eseguire i seguenti comandi per abilitare il canale dotnet RHEL 7 e installare.</span><span class="sxs-lookup"><span data-stu-id="622dd-110">In your terminal, run the following commands to enable the RHEL 7 dotnet channel and install.</span></span>

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31 -y
scl enable rh-dotnet31 bash
```

## <a name="install-the-aspnet-core-runtime"></a><span data-ttu-id="622dd-111">Installare il runtime di ASP.NET CoreInstall the ASP.NET Core Runtime</span><span class="sxs-lookup"><span data-stu-id="622dd-111">Install the ASP.NET Core Runtime</span></span>

<span data-ttu-id="622dd-112">Dopo la registrazione con Subscription Manager, è possibile installare e abilitare il ASP.NET Core Runtime.</span><span class="sxs-lookup"><span data-stu-id="622dd-112">After registering with the Subscription Manager, you're ready to install and enable the ASP.NET Core Runtime.</span></span> <span data-ttu-id="622dd-113">Nel terminale, eseguire i seguenti comandi.</span><span class="sxs-lookup"><span data-stu-id="622dd-113">In your terminal, run the following commands.</span></span>

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31-aspnetcore-runtime-3.1 -y
scl enable rh-dotnet31 bash
```

## <a name="install-the-net-core-runtime"></a><span data-ttu-id="622dd-114">Installare .NET Core Runtime</span><span class="sxs-lookup"><span data-stu-id="622dd-114">Install the .NET Core Runtime</span></span>

<span data-ttu-id="622dd-115">Dopo la registrazione con Subscription Manager, è possibile installare e abilitare .NET Core Runtime.</span><span class="sxs-lookup"><span data-stu-id="622dd-115">After registering with the Subscription Manager, you're ready to install and enable the .NET Core Runtime.</span></span> <span data-ttu-id="622dd-116">Nel terminale, eseguire i seguenti comandi.</span><span class="sxs-lookup"><span data-stu-id="622dd-116">In your terminal, run the following commands.</span></span>

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31-dotnet-runtime-3.1 -y
scl enable rh-dotnet31 bash
```

## <a name="see-also"></a><span data-ttu-id="622dd-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="622dd-117">See also</span></span>

- [<span data-ttu-id="622dd-118">Utilizzo di .NET Core 3.1 su Red Hat Enterprise Linux 7</span><span class="sxs-lookup"><span data-stu-id="622dd-118">Using .NET Core 3.1 on Red Hat Enterprise Linux 7</span></span>](https://access.redhat.com/documentation/en-us/net_core/3.1/html/getting_started_guide/gs_install_dotnet)
