---
title: Installare .NET Core in Linux RHEL 8 gestione pacchetti - .NET CoreInstall .NET Core on Linux RHEL 8 package manager - .NET Core
description: Usare un gestore di pacchetti per installare .NET Core SDK e runtime in RHEL 8.Use a package manager to install .NET Core SDK and runtime on RHEL 8.
author: thraka
ms.author: adegeo
ms.date: 03/17/2020
ms.openlocfilehash: b564a386eb67b6e414a832ad3bca10d3d09022bd
ms.sourcegitcommit: 07123a475af89b6da5bb6cc51ea40ab1e8a488f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/24/2020
ms.locfileid: "80134188"
---
# <a name="rhel-8-package-manager---install-net-core"></a><span data-ttu-id="4b5ba-103">RHEL 8 Gestione pacchetti - Installare .NET Core</span><span class="sxs-lookup"><span data-stu-id="4b5ba-103">RHEL 8 Package Manager - Install .NET Core</span></span>

[!INCLUDE [package-manager-switcher](includes/package-manager-switcher.md)]

<span data-ttu-id="4b5ba-104">In questo articolo viene descritto come utilizzare un gestore di pacchetti per installare .NET Core in RHEL 8.This article describes how to use a package manager to install .NET Core on RHEL 8.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-104">This article describes how to use a package manager to install .NET Core on RHEL 8.</span></span>

[!INCLUDE [package-manager-intro-sdk-vs-runtime](includes/package-manager-intro-sdk-vs-runtime.md)]

## <a name="register-your-red-hat-subscription"></a><span data-ttu-id="4b5ba-105">Registra il tuo abbonamento Red Hat</span><span class="sxs-lookup"><span data-stu-id="4b5ba-105">Register your Red Hat subscription</span></span>

<span data-ttu-id="4b5ba-106">Per installare .NET Core da Red Hat in RHEL, è innanzitutto necessario eseguire la registrazione utilizzando Red Hat Subscription Manager.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-106">To install .NET Core from Red Hat on RHEL, you first need to register using the Red Hat Subscription Manager.</span></span> <span data-ttu-id="4b5ba-107">Se questa operazione non è stata eseguita nel sistema o se non si è sicuri, vedere la [documentazione del prodotto Red Hat per .NET Core](https://access.redhat.com/documentation/net_core/).</span><span class="sxs-lookup"><span data-stu-id="4b5ba-107">If this hasn't been done on your system, or if you're unsure, see the [Red Hat Product Documentation for .NET Core](https://access.redhat.com/documentation/net_core/).</span></span>

## <a name="install-the-net-core-sdk"></a><span data-ttu-id="4b5ba-108">Installare .NET Core SDK.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-108">Install the .NET Core SDK</span></span>

<span data-ttu-id="4b5ba-109">Dopo la registrazione con Gestione sottoscrizioni, è possibile installare e abilitare .NET Core SDK.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-109">After registering with the Subscription Manager, you're ready to install and enable the .NET Core SDK.</span></span> <span data-ttu-id="4b5ba-110">Nel terminale, eseguire i seguenti comandi.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-110">In your terminal, run the following commands.</span></span>

```bash
sudo dnf update
sudo dnf install dotnet-sdk-3.1
```

## <a name="install-the-aspnet-core-runtime"></a><span data-ttu-id="4b5ba-111">Installare il runtime di ASP.NET CoreInstall the ASP.NET Core Runtime</span><span class="sxs-lookup"><span data-stu-id="4b5ba-111">Install the ASP.NET Core Runtime</span></span>

<span data-ttu-id="4b5ba-112">Dopo la registrazione con Subscription Manager, è possibile installare e abilitare il ASP.NET Core Runtime.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-112">After registering with the Subscription Manager, you're ready to install and enable the ASP.NET Core Runtime.</span></span> <span data-ttu-id="4b5ba-113">Nel terminale, eseguire i seguenti comandi.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-113">In your terminal, run the following commands.</span></span>

```bash
sudo dnf update
sudo dnf install aspnetcore-runtime-3.1
```

## <a name="install-the-net-core-runtime"></a><span data-ttu-id="4b5ba-114">Installare .NET Core Runtime</span><span class="sxs-lookup"><span data-stu-id="4b5ba-114">Install the .NET Core Runtime</span></span>

<span data-ttu-id="4b5ba-115">Dopo la registrazione con Subscription Manager, è possibile installare e abilitare .NET Core Runtime.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-115">After registering with the Subscription Manager, you're ready to install and enable the .NET Core Runtime.</span></span> <span data-ttu-id="4b5ba-116">Nel terminale, eseguire i seguenti comandi.</span><span class="sxs-lookup"><span data-stu-id="4b5ba-116">In your terminal, run the following commands.</span></span>

```bash
sudo dnf update
sudo dnf install dotnet-runtime-3.1
```

## <a name="see-also"></a><span data-ttu-id="4b5ba-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="4b5ba-117">See also</span></span>

- [<span data-ttu-id="4b5ba-118">Utilizzo di .NET Core 3.1 in Red Hat Enterprise Linux 8</span><span class="sxs-lookup"><span data-stu-id="4b5ba-118">Using .NET Core 3.1 on Red Hat Enterprise Linux 8</span></span>](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/developing_.net_applications_in_rhel_8/index)
