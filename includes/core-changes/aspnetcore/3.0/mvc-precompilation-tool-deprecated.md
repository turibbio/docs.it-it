---
ms.openlocfilehash: 8395428e1729a00fc1af72cf53fe689ee95b5fdf
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721010"
---
### <a name="mvc-precompilation-tool-deprecated"></a>MVC: strumento di precompilazione deprecato

In ASP.NET Core 1,1, il `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation` pacchetto (strumento di precompilazione MVC) è stato introdotto per aggiungere il supporto per la compilazione in fase di pubblicazione dei file Razor (file con*estensione cshtml* ). In ASP.NET Core 2,1, [Razor SDK](/aspnet/core/razor-pages/sdk?view=aspnetcore-2.1) è stato introdotto per espandersi sulle funzionalità dello strumento di precompilazione. Razor SDK ha aggiunto il supporto per la compilazione in fase di compilazione e di pubblicazione dei file Razor. L'SDK verifica la correttezza dei file con *estensione cshtml* in fase di compilazione, migliorando al tempo stesso l'avvio dell'app. Razor SDK è attiva per impostazione predefinita e non è necessario alcun movimento per iniziare a usarlo.

In ASP.NET Core 3,0 è stato rimosso lo strumento di precompilazione MVC ASP.NET Core 1,1-era. Le versioni precedenti del pacchetto continueranno a ricevere importanti correzioni di bug e sicurezza nella versione patch.

#### <a name="version-introduced"></a>Versione introdotta

3.0

#### <a name="old-behavior"></a>Comportamento precedente

Il `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation` pacchetto è stato usato per pre-compilare le visualizzazioni Razor MVC.

#### <a name="new-behavior"></a>Nuovo comportamento

Razor SDK supporta questa funzionalità in modo nativo. Il `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation` pacchetto non viene più aggiornato.

#### <a name="reason-for-change"></a>Motivo della modifica

Razor SDK offre più funzionalità e verifica la correttezza dei file con *estensione cshtml* in fase di compilazione. L'SDK migliora anche il tempo di avvio dell'app.

#### <a name="recommended-action"></a>Azione consigliata

Per gli utenti di ASP.NET Core 2,1 o versioni successive, eseguire l'aggiornamento per usare il supporto nativo per la precompilazione in [Razor SDK](/aspnet/core/razor-pages/sdk?view=aspnetcore-3.0). Se i bug o le funzionalità mancanti impediscono la migrazione a Razor SDK, aprire un problema in [DotNet/aspnetcore](https://github.com/dotnet/aspnetcore/issues).

#### <a name="category"></a>Category

ASP.NET Core

#### <a name="affected-apis"></a>API interessate

Nessuno

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
