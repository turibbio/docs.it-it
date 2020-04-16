---
title: Comando dotnet nuget delete
description: Il comando dotnet-nuget-delete rimuove dall'elenco o elimina un pacchetto dal server.
author: karann-msft
ms.date: 06/26/2019
ms.openlocfilehash: 4fa4f24adba251d7872986de4a8b1a63203c36c3
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463589"
---
# <a name="dotnet-nuget-delete"></a>dotnet nuget delete

**Questo articolo si applica a:** ✔️ .NET Core 1.x SDK e versioni successive

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## <a name="name"></a>Nome

`dotnet nuget delete`: rimuove dall'elenco o elimina un pacchetto dal server.

## <a name="synopsis"></a>Riepilogo

```dotnetcli
dotnet nuget delete [<PACKAGE_NAME> <PACKAGE_VERSION>] [--force-english-output]
    [--interactive] [-k|--api-key <API_KEY>] [--no-service-endpoint]
    [--non-interactive] [-s|--source <SOURCE>]

dotnet nuget delete -h|--help
```

## <a name="description"></a>Descrizione

Il comando `dotnet nuget delete` rimuove dall'elenco o elimina un pacchetto dal server. Per [nuget.org](https://www.nuget.org/), l'azione consiste nell'annullare l'elenco del pacchetto.

## <a name="arguments"></a>Argomenti

* **`PACKAGE_NAME`**

  Nome/ID del pacchetto da eliminare.

* **`PACKAGE_VERSION`**

  Versione del pacchetto da eliminare.

## <a name="options"></a>Opzioni

* **`--force-english-output`**

  Impone all'applicazione l'esecuzione con una cultura invariante e di lingua inglese.

* **`-h|--help`**

  Stampa una breve guida per il comando.

* **`--interactive`**

  Consente al comando di bloccare operazioni quali l'autenticazione e richiede un intervento manuale. Opzione disponibile a partire da .NET Core 2.2 SDK.

* **`-k|--api-key <API_KEY>`**

  Chiave API per il server.

* **`--no-service-endpoint`**

  Non aggiunge "api/v2/package" all'URL di origine. Opzione disponibile a partire da .NET Core 2.1 SDK.

* **`--non-interactive`**

  Non richiede input o conferme dell'utente.

* **`-s|--source <SOURCE>`**

  Specifica l'URL del server. Gli URL supportati per nuget.org includono `https://www.nuget.org`, `https://www.nuget.org/api/v3` e `https://www.nuget.org/api/v2/package`. Per i feed privati, sostituire il nome host (ad esempio, `%hostname%/api/v3`).

## <a name="examples"></a>Esempi

* Elimina la versione 1.0 del pacchetto `Microsoft.AspNetCore.Mvc`:

  ```dotnetcli
  dotnet nuget delete Microsoft.AspNetCore.Mvc 1.0
  ```

* Elimina la versione 1.0 del pacchetto `Microsoft.AspNetCore.Mvc` senza richiedere all'utente credenziali o altro input:

  ```dotnetcli
  dotnet nuget delete Microsoft.AspNetCore.Mvc 1.0 --non-interactive
  ```
