---
title: Installare .NET Core in Linux CentOS 8 Package Manager-.NET Core
description: Usare uno Gestione pacchetti per installare .NET Core SDK e Runtime in CentOS 8.
author: thraka
ms.author: adegeo
ms.date: 05/01/2020
ms.openlocfilehash: b4cf5975e18aa8dfa8649c0d038caf38d648ad86
ms.sourcegitcommit: 7370aa8203b6036cea1520021b5511d0fd994574
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/02/2020
ms.locfileid: "82728519"
---
# <a name="centos-8-package-manager---install-net-core"></a><span data-ttu-id="ecb02-103">Gestione pacchetti CentOS 8-installare .NET Core</span><span class="sxs-lookup"><span data-stu-id="ecb02-103">CentOS 8 Package Manager - Install .NET Core</span></span>

[!INCLUDE [package-manager-switcher](includes/package-manager-switcher.md)]

<span data-ttu-id="ecb02-104">Questo articolo descrive come usare un gestore di pacchetti per installare .NET Core in CentOS 8.</span><span class="sxs-lookup"><span data-stu-id="ecb02-104">This article describes how to use a package manager to install .NET Core on CentOS 8.</span></span>

[!INCLUDE [package-manager-intro-sdk-vs-runtime](includes/package-manager-intro-sdk-vs-runtime.md)]

## <a name="install-the-net-core-sdk"></a><span data-ttu-id="ecb02-105">Installare il .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="ecb02-105">Install the .NET Core SDK</span></span>

<span data-ttu-id="ecb02-106">Nel terminale eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="ecb02-106">In your terminal, run the following command.</span></span>

```bash
sudo dnf install dotnet-sdk-3.1
```

## <a name="install-the-aspnet-core-runtime"></a><span data-ttu-id="ecb02-107">Installare il runtime di ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ecb02-107">Install the ASP.NET Core Runtime</span></span>

<span data-ttu-id="ecb02-108">Nel terminale eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="ecb02-108">In your terminal, run the following command.</span></span>

```bash
sudo dnf install aspnetcore-runtime-3.1
```

## <a name="install-the-net-core-runtime"></a><span data-ttu-id="ecb02-109">Installare il runtime di .NET Core</span><span class="sxs-lookup"><span data-stu-id="ecb02-109">Install the .NET Core Runtime</span></span>

<span data-ttu-id="ecb02-110">Nel terminale eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="ecb02-110">In your terminal, run the following command.</span></span>

```bash
sudo dnf install dotnet-runtime-3.1
```

## <a name="how-to-install-other-versions"></a><span data-ttu-id="ecb02-111">Come installare altre versioni</span><span class="sxs-lookup"><span data-stu-id="ecb02-111">How to install other versions</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]
